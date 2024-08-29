## Flow of Devops
![flow diagram](https://slidebazaar.com/wp-content/uploads/2023/05/DevOps-Process-Flow-PowerPoint-Template-Dark.jpg)

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

### Networking Basics Commands

To list and modify interfaces on the host IP
>ip link

To see the IP addresses asigned to those interfaces.
>ip addr

To set the IP addresses on the interfaces.
>ip addr add 192.168.1.10/24 dev eth0

To view the routing table
~~~
ip route
or 
route       
~~~

To add entries into the routing table
>ip route add 192.168.1.0/24 via 192.168.2.1

To check if ip forwarding is enable on the host
>cat /proc/sys/net/ipv4/ip_forward

### DNS

TO ping the one system from another we use
~~~
ping 192.168.1.11
but let suppose i have a database configure on this ip so instead of pinging to ip every time i can also give it a name.
To set the name we can use
cat >> /etc/hosts
192.168.1.11   db
~~~

But if we have a lot of ip mapping it will be diffult to manage all that so to tackle this we will use a DNS server.
SO for this add all the IP mapping in the dns server and update the host system with the following command pointing to the server DNS
~~~
cat /etc/resolv.conf
nameserver    192.168.1.100

Here 192.168.1.100 is the ip of DNS Server
~~~

Lets- suppose we have added a entry in our DNS server i.e *192.168.1.10     web.mycompany.com* , so now for pinging we have to write *ping web.mycompany.com*.
But if you simply want to write *ping web* , we have to add another entry in our host resolv.conf file using below command.
~~~
cat >> /etc/resolv.conf
search     mycompany.com  prod.mycompany.com
~~~

There are some other tool also to test DNS resolution
~~~
nslookup www.google.com
Note - it will not comsider entry in local host file, it will only comsider the entry in DNS Server.

dig www.google.com
Same goes for this.
~~~

## Application Basics

**Install & Extract Java**
~~~
wget https://download.java.net....
Now to extract
tar -xvf openjdk-13.0.2_linux-x64_bin.tar.gz
Now to check version
jdk-13.0.2/bin/java -version
jdk -version
~~~

**Build and Packaging**

Compile java source code file into bytecode(.class file)
>javac MyClass.java

Run a java application
>java MyClass

Packages compiled Java classes and resources into a JAR file
>jar cvf myapp.jar -C bin/ .

Generate APi documentation 
>javadoc -d docs/ MyClass.java

Run jar file
>java -jar myapp.jar

**Install NodeJs**

~~~
First add repsitory
curl -sL https://rpm.nodesource.com/setup_13.x | bash -
After this install
yum install nodejs
~~~

**NPM Commands**

To check version
>npm -v

To search file
>npm search file

To install
>npm install file

To install globally
>npm install file -g

**Python commands**
~~~
To install
yum install python2 or python3
(Provide the perticular version you want to install)
To check version
python -V
To run python file
python2 or python3 file_name
~~~

To get list of path that python look for
>python2 -c "import sys; print(sys.path)"

**PIP Commands**
~~~
To install dependencies
pip install flask
To show where it is installed
pip show flask
To install multiple dependencies at once we can defined all that in requirement.txt and run command-
pip install -r requirement.txt
To upgrade package
pip install flask --upgrade
To unistall
pip uninstall flask
~~~

## Git Commands

You can go through all the important git command using this document [Github Document](https://education.github.com/git-cheat-sheet-education.pdf)


## Jenkins Commands to Run and configure
![Jenkins commands](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/10/Slide1-11.jpg)
