# termux-ngrok-configuration
Procedures to configure ngrok on termux to run nginx webserver

Configure Nginx on Termux with ngrok

1. Download Termux at Playstore
2. Open Termux app after download
3. Update apt-get or pkg using this command  you can use apt-get or pkg in installing package
  
```console  
    apt-get update
    pkg upgrade
```

4. Access shared and external storage using this command

```console
  termux-setup-storage
```

 And navigate to home directory to check if we found the internal storage folder

```console
   cd ~
   ls
```

If storage folder is in the list then it's good

5. Install nginx 

```console
   pkg install nginx
```

6. After you install nginx, you can run localhost using your phone browser just type: localhost:8080


7. If the Welcome nginx appears, then the nginx installation succeed

Note: you can also stop the nginx in service by typing this command

```console
    nginx -s stop
```

8. The default storage of nginx html files can be found on /usr/share/nginx/html directory. You can use this command to navigate on that directory

```console
   cd ~
   cd ..
   cd /usr/share/nginx/html
```

to view what's inside the folder, type this command

```console
  ls
```

Note: this is where we deploy html files to run on nginx web server. You can find the default web page of nginx named index.html in that directory.

8.1 if you want to configure the .conf file of nginx , just in case you want to change the port, you can navigate to /usr/etc/nginx to locate the nginx.conf file. To do it type this command

```console
   cd ~
   cd ..
   cd /usr/etc/nginx
   ls
```

and you can find the nginx.conf there.. to view the contents of that file type

```console
   cat nginx.conf
```

If you want to edit the file, make sure you install the nano package

```console
   pkg install nano
```

Then after you install nano, you can now edit the file using this command

```console
   nano nginx.conf
```

Note: locate the 

```console
server {
   
   listen     8080;
   server_name    localhost;
```

To edit the port from 8080 to your choice

Warning: Editing this file can damage the service of the web server. So be careful on  editing the conf file.


9. To access the localhost on different device, we will use the ngrok.

Ngrok is a cross-platform application that exposes local server ports to the Internet. 

To do it, download the ngrok on : https://ngrok.com/download

Note: Register on the ngrok website because we will use your own Auth Token to save it on termux and to have at least free plan

Note: make sure that the zip file of ngrok is in the Download folder of your internal storage so that we can easily access it on termux
  

10. After installing the ngrok, navigate to download folder of your internal storage.

```console
  cd ~
  cd storage
  ls   //to check if the download folder exists

  cd download
  ls // to check the ngrok zip file
```

After that type this command to unzip the file and extract it to home 

```console
unzip ngrok.zip -d ~
```

Note: file name of ngrok may be differs so you need to type the exact filename of that zip file in order to unzip it

11. After you unzipped the file, lets go to home folder

```console
   cd ~ 
   ls
```

12.If you see ngrok in the list then it's good..
And, let's change it's permission to execute it.. type this command 

```console
   chmod +x ngrok
    ls
```

If ngrok is now in color green, then it is ready to fire it up.


13. Now, it is time to login on ngrok website to copy your auth_token to termux.

In the dashboard, you will find the command on how to save your token in termux. To do it type:

```console
  ./ngrok <auth_token>
```

Example: 

```console
 ./ngrok 3yfi69Hf9ekfpsh&dhjPsnfu&dhdoapBs7znao7adn
```

And make you you will see a success or at least Auth Saved after you do it.

14. Now, let's try to connect our localhost to ngrok.. we all know that it uses port  8080 . To do so, type 

```console
   ./ngrok http 8080
```

Then the termux will change to ngrok connection service where you can see: 

ngrok by @inconshreveable, Version Status, Region and etc.

Now, let's look on Session Status. It always  says Reconnecting and it loops on Reconnecting. That is because latest Ngrok may not work in Termux directly as requires /etc/resolv.conf . To do it lets install another package

```console
    pkg install proot
    pkg install proot resolve-conf
```

Note: (important)And after we install proot, everytime we use ngrok, everytime we close the termux, always run this command to use ngrok properly

```console
  termux-chroot
```

termux-chroot gives access to ngrok to start a tunneling service to expose our localhost in the internet


15. After that, we are now ready to use ngrok anytime anywhere as long as you have internet. Type this command again 

```console
    ngrok http 8080
```

And now the Session Status becomes green and it says online. And you can now find 2 Forwarding with http and https. We will use the http one to browse it in your browser.


 Now, lets open it to your browser.. just copy the domain in http and paste it on search bar

Example:

 http://4488-136-158-8-66.ngrok.io

And you will see the Welcome to Nginx page.

Remember:

 In order to deploy web files, always refer to the number 8 procedure

 The default storage of nginx html files can be found on /usr/share/nginx/html directory. You can use this command to navigate on that directory

```console
   cd ~
   cd ..
   cd /usr/share/nginx/html
```

And always remember to type

```console
   termux-chroot
```
Everytime we open termux app to run ngrok


That's all thank you.


Prepared by (Christopher Robin Chase)[https://github.com/chrischase011]
