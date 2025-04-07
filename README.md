# termux-ngrok-configuration
## Procedures to configure ngrok on termux to run nginx webserver

__Steps to Configure Nginx on Termux with Ngrok__

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

  Then navigate to the home directory to check if the internal storage folder is present.
  
  ```console
  cd ~
  ls
  ```

  If the `storage` folder is in the list, then you're good to go.

5. Install nginx 

```console
pkg install nginx
```

6. After installing Nginx, you can access localhost using your phone's browser. Just type: `localhost:8080`.


7. If the Nginx welcome page appears, then the installation was successful.

  __Note__: You can also stop the Nginx service by typing the following command

  ```console
  nginx -s stop
  ```

8. The default location for Nginx HTML files is `/usr/share/nginx/html`. You can use the following command to navigate to that directory:

```console
cd ~
cd ..
cd /usr/share/nginx/html
```

To view the contents of the folder, type the following command:

```console
ls
```

__Note__: This is where you deploy HTML files to run on the Nginx web server. You’ll find the default Nginx web page named `index.html` in this directory.

8.1 If you want to configure the Nginx `.conf` file (for example, to change the port), you can navigate to `/etc/nginx` to locate the `nginx.conf file`. To do so, type the following command:

```console
cd ~
cd ..
cd /usr/etc/nginx
ls
```

Then, you can find the nginx.conf file there. To view its contents, type the following command:

```console
cat nginx.conf
```

If you want to edit the file, make sure to install the `nano` package.

```console
pkg install nano
```

After installing nano, you can now edit the file using the following command:

```console
nano nginx.conf
```

__Note__: locate the 

```console
server {
   
   listen     8080;
   server_name    localhost;
```

To edit the port from 8080 to your choice.

__Warning__: Editing this file can disrupt the `web server service`, so be careful when modifying the `conf` file.


9. To access localhost on a different device, we will use `ngrok`.

`Ngrok` is a cross-platform application that exposes local server ports to the internet.

To get started, download `ngrok` from: https://ngrok.com/download.

__Note__: Register on the `ngrok` website, as we will use your own `Auth Token` to save it on Termux and enable at least the free plan.

__Note__: Make sure that the `ngrok` zip file is in the `Download` folder of your internal storage so that it can be easily accessed from Termux.
  

10. After installing `ngrok`, navigate to the "Download" folder in your internal storage.

```console
cd ~
cd storage
ls   // to check if the download folder exists

cd download
ls // to check the ngrok zip file
```

After that, type the following command to unzip the file and extract it to the home directory:

```console
unzip ngrok.zip -d ~
```

__Note__: The file name of ngrok may differ, so you need to type the exact filename of the zip file in order to unzip it.

11. After you unzipped the file, lets go to home folder.

```console
cd ~ 
ls
```

12. If you see ngrok in the list, then it's good.
Next, let's change its permissions to make it executable. Type the following command:

```console
chmod +x ngrok
ls
```

If ngrok is now displayed in green, it is ready to be launched.


13. Now, it's time to log in to the ngrok website and copy your `auth_token` to Termux.

In the dashboard, you will find the command to save your `token` in Termux. To do this, type the following command:

```console
./ngrok <auth_token>
```

Example: 

```console
./ngrok 3yfi69Hf9ekfpsh&dhjPsnfu&dhdoapBs7znao7adn
```

Make sure you see a success message or at least "Auth Saved" after doing this.

14. Now, let's try to connect our localhost to ngrok. We know that it uses port `8080`. To do so, type the following command:

```console
./ngrok http 8080
```

Then, `Termux` will switch to the ngrok connection service, where you can see:

- ngrok by @inconshreveable

- Version

- Status

- Region, etc.

Now, let's look at the Session Status. It will always say "Reconnecting" and loop indefinitely. This happens because the latest version of ngrok may not work directly in Termux as it requires `/etc/resolv.conf`. To resolve this, let's install another package.

```console
pkg install proot
pkg install proot resolve-conf
```


__Note (Important)__: After installing proot, every time you use `ngrok`, you must run this command to use `ngrok` properly each time you close Termux.

```console
termux-chroot
```

`termux-chroot` gives ngrok access to start a tunneling service, allowing us to expose our localhost to the internet.


15. After that, you are now ready to use `ngrok` anytime, anywhere, as long as you have an internet connection. Type this command again:

```console
ngrok http 8080
```

Now, the Session Status will turn green and say "online." You will see two Forwarding links, one for HTTP and one for HTTPS. We will use the HTTP link to browse it in your browser.

Now, let's open it in your browser. Just copy the HTTP domain and paste it into the search bar.

Example:

 `http://4488-136-158-8-66.ngrok.io`

And you will see the `Welcome to Nginx page`.

__Remember__:

To deploy web files, always refer to procedure number 8.

The default location for Nginx HTML files is `/usr/share/nginx/html`. You can use the following command to navigate to that directory:

```console
cd ~
cd ..
cd /usr/share/nginx/html
```

And always remember to type

```console
   termux-chroot
```
Everytime we open termux app to run ngrok.


That's all thank you.


Prepared by [Christopher Robin Chase](https://github.com/chrischase011)
