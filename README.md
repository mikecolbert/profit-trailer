# profit-trailer
Setup of ProfitTrailer on Raspberry Pi

Raspberry Pi 3+ base setup and Java configuration:

Clone OS to microSD card and boot up Pi with a keyboard and mouse.
Pi will boot into GUI. Configure timezone, wireless network, and other settings. Allow it to check for updates.
Preferences --> Raspberry Pi Configuration
 - System --> Boot: To CLI
 - Interfaces --> SSH: enable
Get the IP address (ifconfig)
Reboot (sudo reboot)
Disconnect keyboard, mouse, and monitor


Login via SSH:
ssh pi@<<ip address>>


Remove existing versions of Java:
```
sudo apt-get purge openjdk
sudo apt-get purge java7
sudo apt-get autoremove
```


Install necessary package:
``` sudo apt-get install dirmngr ```


Add necessary Ubuntu keyservers:
```
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-key EEA14886
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-key C2518248EEA14886
```
If you get a message that you are missing one, just run the command again with the public key shown in the message.


Add these lines to the bottom of /etc/apt/sources.list
```
deb http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main
deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main
```

Install Java:
```
sudo apt-get update
sudo apt-get install openjdk-8-jre-headless -y
sudo apt-get install oracle-java8-set-default
```


Check the Java version:
``` java -version ```

Displays:
openjdk version "1.8.0_212"
OpenJDK Runtime Environment (build 1.8.0_212-8u212-b01-1+rpi1-b01)
OpenJDK Client VM (build 25.212-b01, mixed mode)


Final cleanup and update:
```
sudo apt-get update
sudo apt-get dist-upgrade
sudo apt-get clean
```


Reboot:
``` sudo reboot ```



Install ProfitTrailer:
``` 
wget https://download.profittrailer.com/ProfitTrailer.zip 
unzip ProfitTrailer.zip
rm -r ProfitTrailer.zip
```
ls to see folder name:
```
mv ProfitTrailer0x.x.x/ ProfitTrailer
cd ProfitTrailer
chmod +x ProfitTrailer.jar
```


Install nodejs (npm is also installed with nodejs):
```
sudo apt-get install -y nodejs

node --version
npm --version
```

Install pm:
``` sudo npm install pm2@latest -g ```

```
# edit pm2-ProfitTrailer.json to set a unique name in the name property then save (this may cause errors if done in nano)
pm2 start pm2-ProfitTrailer.json

pm2 start --no-daemon pm2-ProfitTrailer.json (to troubleshoot errors)
pm2 save
pm2 startup
pm2 list
```









