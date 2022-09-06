# JavaScript-Integration-with-Docker

📌 In this task, you have to create a Web Application for Docker (one of the great Containerization Tool which provides the user Platform as a Service (PaaS)) by showing your own creativity and UI/UX designing skills to make the web portal user friendly.

📌 This app will help the user to run all the docker commands like:

👉docker images

👉docker ps

👉docker run

👉docker rm -f

👉docker exec

👉 add more if you want. (Optional)

👉 Make a blog/article/video explaining this task step by step.

⚙️ Task 7.2 -

📌 Write a blog explaining the use-case of javascript in any of your favorite industries.

Task 7.1

In this part of the task, I have integrated Javascript with docker so that users can use docker and use its commands more easily and effectively.

To start this task we have to first start our VM and OS(RHEL8) and install ‘httpd’ service in our OS.

‘httpd’ is the Apache HyperText Transfer Protocol (HTTP) server program. It is designed to be run as a standalone daemon process. When used like this it will create a pool of child processes or threads to handle requests.

yum install httpd
Then we have to disable our firewall and start the httpd service.

systemctl disable firewalld
setenforce 0
systemctl start httpd
Now we have to go in the directory “/var/www/html” and create a file using ‘gedit’ command.

cd /var/www/html
gedit <file_Name>.html
This file contains all the front-end of our website and should also include the script to connect our server to OS.

The script part given below is from the code that I have shared in my GitHub repository below.

<script>
         function lw()
        {
        
        var xhr=new XMLHttpRequest();
        i=document.getElementById("in1").value;
        
        xhr.open("GET","http://192.168.43.104/cgi-bin/lw.py?x="+i,true);
        xhr.send();
        
        xhr.onload=function (){
        var output=xhr.responseText;
        document.getElementById("d1").innerHTML=output;
                    }
        }
        
</script>
Now change the directory to “var/www/cgi-bin” and make a Python file using ‘gedit’ command with “.py” extension to write our backend code.

cd /var/www/cgi-bin
gedit <file_Name.py>
This file contains the backend code(in Python).

#!/usr/bin/python3
import cgi
import subprocess
import time
print("content-type: text/html")
print()
print("Hello from backend")
print()
f=cgi.FieldStorage()
cmd=f.getvalue("x")
o=subprocess.getoutput("sudo "+ cmd)
print(o)
After this so that any non-root user can access from my server, I made changes as follows so that using the “sudo” command the non-root user can access the docker services.

In the terminal, we have to go to file-path ‘/etc/group’.

vim /etc/group
Now we have to make the following change to allow our non-root users to access docker.


Now we have to again change the directory from terminal to “/etc/sudoers” and make the following changes over there.

vim /etc/sudoers

We have to give access to our python file to be executable from the guest user. So for this, we have to give access to it by going into the directory where it was stored and then using the command given below.

chmod +x <file_name>.py
Now we are all set and can use our application in Windows web browser (Chrome or Edge) with the help of URL.

http://<IP Address>/<file_Name>.html
