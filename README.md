# Backup-Server

Script that backups directories to a server 


## Description

Backup server is a bashscript that allows users to backup chosen directories to a server's ip address. The program comes with the bash scrip, a .service file and a .timer file. The service will run the bashscript as a service and the ti
mer file will define when it is ran. The default values for the timer will execute the *backup-server* script every Friday between 01:00:00 and 01:30:00.

## Getting Started

### Dependencies

* Ability to use rsync
* IP address of a server's virtual machine (I.E user@147.182.243.30)
* The ssh key pair on the device running the script and the host  you are trying to connect to

### Installing

* Program files are downloadable at https://github.com/TristanVII/2420_week11_lab.git 
* The *backup-server.service* and the *backup-sever.timer* must be placed on your local machines /home/user/etc/systemd/system directory
* The *backup-server* bashscript must be placed on your local machines /home/user/opt directory
* The *backup-server.conf* must be placed on your local machines /home/user/etc directory
   * To configure the destination IP address, and directories to backup, you must edit the *backup-server.conf* file's **IPADDR** and **DIRECTORIES** variables
   * Directories must be seperated by spaces 
   
<img width="650" alt="Screenshot 2022-11-17 at 10 26 59 PM" src="https://user-images.githubusercontent.com/100272904/202638967-a06ad637-c7e1-41d6-b663-925a216d9d53.png">

### Files Setup & Executing the program

* The *backup-server.service* and *backup-server.timer* files must be enabled in order to create a symlink
```
sudo systemctl enable --now backup-server.service
sudo systemctl enable --now backup-server.timer
```
* After each command you should execute the systemctl daemon-reload command to reload the systemd manager configuration
```
sudo systemctl daemon-reload
```

* Execute the following command to check the status of your service in order to make sur it is enabled
```
sudo systemctl status backup-server.service
```

Succesful output:

<img width="883" alt="Screenshot 2022-11-17 at 10 59 18 PM" src="https://user-images.githubusercontent.com/100272904/202640907-d6239039-df84-4478-bf70-24d3c7f71db5.png">

* Execute the following command to run your backup-server service now
```
sudo systemctl start backup-server.service
```

* Execute the following command to check the the active timer for your service
```
sudo systemctl list-timers
```

If the timer for *backup-server.service* is enabled succesfully, you should see it's timer after executing the above command like so:

<img width="1470" alt="Screenshot 2022-11-17 at 11 06 54 PM" src="https://user-images.githubusercontent.com/100272904/202642228-4f2b2a56-9cce-41da-bf8d-5a0b6eb66185.png">

At this point the service and timer for the *backup-server* script should be enabled.
Your machine will automatically run the script every Friday between 01:00:00 and 01:30:00

### Help

## Issues with the *backup-server* bash script

* Make sure you have the server's IP address you are trying to backup files to private key inside your *.ssh* directory and the the server has the public key inside this *.ssh/authorized_keys*
* Make sure the *backup-server.conf* variables have the correct syntax. Directories should be seperated by spaces, inside parentheses '()' and no spaces between the variable and the equals sign
* Make sure you have the correct IPADDR inside the *backup-server.conf*
* Make sure the *backup-server* bash script is executable, if it isn't execute the command ```chmod +x backup-server ```

To test the *server-backup* script by itself, run the command:
```
/home/user/opt/backup-server
```

Succesful output: 

<img width="582" alt="Screenshot 2022-11-17 at 11 23 07 PM" src="https://user-images.githubusercontent.com/100272904/202644762-ff67e6c3-f29b-408d-8629-a8d22bd02403.png">


### Authors

Tristan Davis
Sandeep Kaur

