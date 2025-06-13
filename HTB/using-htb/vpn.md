## Connecting to HTB VPN

HTB and other services offering purposefully vulnerable VMs/networks require players to connect to the target network via a VPN to access the private lab network. Hosts within HTB networks cannot connect directly out to the internet. When connected to HTB VPN (or any penetration testing/hacking-focused lab), we should always consider the network to be "hostile." We should only connect from a virtual machine, disallow password authentication if SSH is enabled on our attacking VM, lockdown any web servers, and not leave sensitive information on our attack VM (i.e., do not play HTB or other vulnerable networks with the same VM that we use to perform client assessments). When connecting to a VPN (either within HTB Academy or the main HTB platform), we connect using the following command:

```shell-session
cdeez@htb[/htb]$ sudo openvpn user.ovpn

Thu Dec 10 18:42:41 2020 OpenVPN 2.4.9 x86_64-pc-linux-gnu [SSL (OpenSSL)] [LZO] [LZ4] [EPOLL] [PKCS11] [MH/PKTINFO] [AEAD] built on Apr 21 2020
Thu Dec 10 18:42:41 2020 library versions: OpenSSL 1.1.1g  21 Apr 2020, LZO 2.10
Thu Dec 10 18:42:41 2020 Outgoing Control Channel Authentication: Using 256 bit message hash 'SHA256' for HMAC authentication
Thu Dec 10 18:42:41 2020 Incoming Control Channel Authentication: Using 256 bit message hash 'SHA256' for HMAC authentication
Thu Dec 10 18:42:41 2020 TCP/UDP: Preserving recently used remote address: [AF_INET]
Thu Dec 10 18:42:41 2020 Socket Buffers: R=[212992->212992] S=[212992->212992]
Thu Dec 10 18:42:41 2020 UDP link local: (not bound)
<SNIP>
Thu Dec 10 18:42:41 2020 Initialization Sequence Completed
```

The last line `Initialization Sequence Completed` tells us that we successfully connected to the VPN.

Where `sudo` tells our host to run the command as the elevated root user, `openvpn` is the VPN client, and the `user.ovpn` file is the VPN key that we download from either the Academy module section or the main HTB platform [Access page](https://www.hackthebox.eu/home/htb/access). If we type `ifconfig` in another terminal window, we will see a `tun` adapter if we successfully connected to the VPN.

```shell-session
cdeez@htb[/htb]$ ifconfig

<SNIP>

tun0: flags=4305<UP,POINTOPOINT,RUNNING,NOARP,MULTICAST>  mtu 1500
        inet 10.10.x.2  netmask 255.255.254.0  destination 10.10.x.2
        inet6 dead:beef:1::2000  prefixlen 64  scopeid 0x0<global>
        inet6 fe80::d82f:301a:a94a:8723  prefixlen 64  scopeid 0x20<link>
        unspec 00-00-00-00-00-00-00-00-00-00-00-00-00-00-00-00  txqueuelen
```

Typing `netstat -rn` will show us the networks accessible via the VPN.

```shell-session
cdeez@htb[/htb]$ netstat -rn

Kernel IP routing table
Destination     Gateway         Genmask         Flags   MSS Window  irtt Iface
0.0.0.0         192.168.1.2     0.0.0.0         UG        0 0          0 eth0
10.10.14.0      0.0.0.0         255.255.254.0   U         0 0          0 tun0
10.129.0.0      10.10.14.1      255.255.0.0     UG        0 0          0 tun0
192.168.1.0     0.0.0.0         255.255.255.0   U         0 0          0 eth0
```

Here can see that the 10.129.0.0/16 network used for HTB Academy machines is accessible via the `tun0` adapter via the 10.10.14.0/23 network.

---


## ip namespaces

```bash
#!/bin/bash

NS_NAME="htb"
TUN_DEV="veth-htb"
TUN_PEER="veth-main"
NS_IP="10.200.200.2/30"
MAIN_IP="10.200.200.1/30"
WAN_IF="wlan0" # your normal internet interface

# Clean up
ip netns del "$NS_NAME" 2>/dev/null
ip link del "$TUN_PEER" 2>/dev/null

# Create namespace and loopback
ip netns add "$NS_NAME"
ip netns exec "$NS_NAME" ip link set lo up

# Create veth pair
ip link add "$TUN_DEV" type veth peer name "$TUN_PEER"
ip link set "$TUN_DEV" netns "$NS_NAME"

# Assign IPs
ip addr add "$MAIN_IP" dev "$TUN_PEER"
ip link set "$TUN_PEER" up
ip netns exec "$NS_NAME" ip addr add "$NS_IP" dev "$TUN_DEV"
ip netns exec "$NS_NAME" ip link set "$TUN_DEV" up

# Default route in namespace
ip netns exec "$NS_NAME" ip route add default via 10.200.200.1

# Enable forwarding
sysctl -w net.ipv4.ip_forward=1

# NAT out through your  WAN 
iptables -t nat -C POSTROUTING -s 10.200.200.0/30 -o "$WAN_IF" -j MASQUERADE 2>/dev/null ||
    iptables -t nat -A POSTROUTING -s 10.200.200.0/30 -o "$WAN_IF" -j MASQUERADE

# DNS for namespace
mkdir -p /etc/netns/$NS_NAME
echo "nameserver 1.1.1.1" >/etc/netns/$NS_NAME/resolv.conf

echo "[+] Namespace '$NS_NAME' is isolated and routes out via '$WAN_IF'."
echo "    Run OpenVPN with:"
echo "    sudo ip netns exec $NS_NAME openvpn --config /path/to/htb.ovpn"
```

run this
```bash
sudo ip netns exec htb openvpn --config academy-regular.ovpn
```


in .zshrc add 

```zsh
#htb namespace 
htbuser() {
  sudo ip netns exec htb env $(env | grep -E '^(SHELL|HOME|PATH|ZDOTDIR|USER|LOGNAME|USERNAME|PYENV|VIRTUAL_ENV|SDKMAN|GRADLE_HOME|JAVA_HOME|PERL|PICO|DISPLAY|WAYLAND|XDG|TERM|COLORTERM|LS_COLORS|OO_PS4_TOOLCHAIN|KITTY|HYPRLAND|LANG|SSH_AUTH_SOCK|DBUS_SESSION_BUS_ADDRESS)=' | xargs) \
  sudo -u "$USER" "$@"
}
```

source `.zshrc`

and then run commands prefixed with `htbuser`

to use `pyenv` set the global pyenv to the virtualenv you need

