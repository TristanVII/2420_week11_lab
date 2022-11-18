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

* How/where to download your program
* Any modifications needed to be made to files/folders

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
