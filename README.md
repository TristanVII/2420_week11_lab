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

### Files Setup

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


### Executing program

* How to run the program
* Step-by-step bullets
```
code blocks for commands
```

## Help

Any advise for common problems or issues.
```
command to run if program contains helper info
```

## Authors

Contributors names and contact info

ex. Dominique Pizzie  
ex. [@DomPizzie](https://twitter.com/dompizzie)

## Version History

* 0.2
    * Various bug fixes and optimizations
    * See [commit change]() or See [release history]()
* 0.1
    * Initial Release

## License

This project is licensed under the [NAME HERE] License - see the LICENSE.md file for details

## Acknowledgments

Inspiration, code snippets, etc.
* [awesome-readme](https://github.com/matiassingers/awesome-readme)
* [PurpleBooth](https://gist.github.com/PurpleBooth/109311bb0361f32d87a2)
* [dbader](https://github.com/dbader/readme-template)
* [zenorocha](https://gist.github.com/zenorocha/4526327)
* [fvcproductions](https://gist.github.com/fvcproductions/1bfc2d4aecb01a834b46)
