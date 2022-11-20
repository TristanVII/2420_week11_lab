# Backup-Server

Script that backups directories to a server 


## Description

Backup server is a bashscript that allows users to backup chosen directories to a remote system's ip address. The program comes with the bash script, a .service file and a .timer file. The service will run the bashscript as a service and the timer file will define when it is ran. The default values for the timer will execute the *backup-server* script every Friday between 01:00:00 and 01:30:00.

## Getting Started

### Dependencies

* Ability to use rsync
* File editor such as Vim or Nano to edit files
* IP address of remote system (I.E user@147.182.243.30) # Change this ip address to the public ip address of your droplet. 
* The ssh key pair on the device running the script and the host you are trying to connect to

### Installing
* Do the setup for the droplets by following the video below.

  https://vimeo.com/758870226/f75da348fc?embedded=true&source=vimeo_logo&owner=17609105
* After following the video you will have 1 regular user which is allowed to ssh into th droplet while the root user will not have access to the droplet. 
* Repeat the steps in the video and create a new droplet. 
* After completing the steps 2 time you will have 2 droplets with 2 regular users. 
* Rename one of the droplet's name to server-one using 
```
sudo hostnamectl set-hostname server-one
```
* Rename the other droplets name to backup-server using 
```
sudo hostnamectl set-hostname backup-server
```
* Now create a new key pair on server-one and copy the the public key to the backup-server.
* Once you have copied the key you can append the new public key to the authorized keys file with ``` >> ``` to append.
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

* Execute the following command to check the status of your service in order to make sure it is enabled
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

### How the Script Works

* The script first declares a Variable named *CONFIG_FILE* which is the path to the *backup-server.conf*
* If the path provided is correct, the script will source it to get its variables that are written inside if the path is incorrect, the script will exit and output "Configuration file not found!"
* For every directory listed in the *DIRECTORIES* variable in the *backup-server.conf* the script will loop through them and execute the following command
```
rsync -auvz -e "ssh -i /home/server-one/.ssh/backup-server" $DIRECTORY "backup-server@$IPADDR:/home/backup-server/backup"
```
* *rsync* is a command which copies files or directories to a remote system
* For more information on the rsync function do ``` man rsync ``` 
* The first argument is used to provide the ssh key needed to connect to the remove system **make sure this is the correct path to your private key**
* The second argument is a directory from the directories listed in the *DIRECTORIES* variable inside the *backup-server.conf*
* The last argument is the remote systems full IP address to connect to **user@ip** followed by the path you wish to copy the directory to
* Make sure you have the correct IP address declared as the variable *IPADDR* inside the *backup-server.conf* file and that you have the correct user name of your for your remote machine

**backup-server bash script code**

<img width="1132" alt="Screenshot 2022-11-18 at 7 49 18 PM" src="https://user-images.githubusercontent.com/100272904/202832920-1358daef-c7c3-4b15-8d97-ba637b9c153a.png">


## Help

### Issues with the *backup-server* bash script

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

Tristan Davis & Sandeep Kaur

