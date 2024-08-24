## Flow of Devops
![flow diagram](image.png)

## Shell Types
* Bourne Shell (Sh Shell)
* C Shell (csh or tcsh)
* Z Shell (Zsh)
* Bourne again Shell (Bash)

**To check your current shell**
> echo $SHELL

## Basic Commands

Print to Screen
> echo hi

List files & Folders
> ls

Change directory
> cd my_dir

Present Working Dir
>pwd

Make Dir
>mkdir new_dir

Make Dir Hierarchy
~~~
mkdir /tmp/asia
mkdir /tmp/asia/india
mkdir /tmp/asia/india/banglore
~~~

**OR**

~~~
mkdir -p /tmp/asia/india/banglore
~~~

Remove dir
> rm -r /temp/my_dir

Copy dir
>cp -r my_dir /tmp/my_dir

Create a new file (no content)
>touch new_file.txt

Add content to file 
~~~
cat > new_file.txt
This is some sample text
CTRL+D (to save and exit)
~~~

View contents of the file
>cat new_file.txt

Copy files
>cp new_file.txt copy_file.txt

Move (rename) file
>mv new_file.txt samplt_file.txt

Remove file
rm new_file.txt

**VI Editor**

* When we type **vi index.html** , it shows the file content and in vi editor there is 2 mode Command & Insert , when we open file it is default in *Command Mode to switch Command to Insert Mode we have to Press i and to back to command mode press esc.* 

### Command Mode 
~~~
To delete a character Press x
To delete whole line Press dd
To copy Press yy
To Paste Press p
To Scroll up ctrl+u
To Scroll Down ctrl+d
To command Press :
To Save Press :w
To Quit Press :q
To Save & Quit Press :wq
To find the word Press /your_word
~~~

### User Account Related Command

To know the user
>whoami

For id
>id

To switch user
>su aparna

To Ssh in diffrent account
>ssh aparna@192.168.1.2

To access the root previlage
>sudo ls/root

**Download File**
~~~
curl http://www.some-site.com/some-file.txt -O
OR
wget http://www.some-site.com/some-file.txt -O some-file.txt
~~~

**Check Os Version**
~~~
ls /etc/*release*
cat /etc/*release*
~~~

### Package Management

**RPM ( RED HAT Package manager)**

install package
>rpm -i telnet.rpm

Uninstall package
>rpm -e telnet

Query Package
>rpm -q telnet

**YUM Package manager**

install package
>yum install ansible

To view & list the repolist
~~~
yum repolist
ls /etc/yum.repos.d/
~~~

To list the package detail
>yum list ansible

To remove the package
>yum remove ansible

To list all the package version 
>yum --showduplicates list ansible

To install specific version 
>yum install ansible-2.4.2.0

## Services

Start Httpd Services
~~~
service httpd start
or
systemctl start httpd
~~~ 

Stop Httpd Services
>systemctl stop httpd

Check Httpd Service Status
>systemctl status httpd 

Configure httpd to start at Startup
>systemctl enable httpd

Congigure httpd to not start at Startup
>systemctl disable httpd

**How do you configure a program or software as a service?**

For this we will create a file with name of app , Let's say if our app name is my_app then file name is my_app.services.

And in the file we will define multiple parameter to start or stop our service with systemctl command.

~~~
my_app.services
[Unit]
Description=My python web application

[Service]
ExecStart=/usr/bin/python3 /opt/code/my_app.py
ExecStartPre=/opt/code/configure_db.sh
ExecStartPost=/opt/code/email_status.sh

Restart=always

[Install]
WantedBy=multi-user.target
~~~

After creating our service file we will directly start or stop using **systemctl** command.

To fetch the changes run
>systemctl daemon-reload
