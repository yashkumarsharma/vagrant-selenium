It's a merged repo of https://github.com/Slayer911/vagrant-selenium.git and  https://github.com/vorachet/vagrant-e2etesting-protractor.git
Parent repository of both forks: https://github.com/Anomen/vagrant-selenium

Features :
- coping hosts file from host machine to guest
- updated java to 8 version, which compile with the last selenium app
- set correct permissions for vagrant user


# Pre-installed Selenium & Protractor Vagrant configuration

This project is designed for Selenium beginners who want to install a complete Selenium infrastructure including real and headless browser support within minutes without knowing in the technical detail of Selenium installation. E2E-Testing experts who are a minimalist can also choose to add this project to your minimal set in deploying a complete Selenium infrastructure for Protractor users and you can also consider to extend this project for your advanced test automation. Everyting can be installed with single npm install command which allows AngularJS developers and testers perform the E2E-testing life-cycle with consistent Protractor environment.

# Prerequisite Software

  * [Vagrant - https://www.vagrantup.com/downloads.html](https://www.vagrantup.com/downloads.html)
  * [VirtualBox - https://www.virtualbox.org/wiki/Downloads](https://www.virtualbox.org/wiki/Downloads)

# Install 

1. Install [Vagrant](https://www.vagrantup.com)
2. Clone this git repository
3. Run the command `vagrant plugin install vagrant-triggers`
4. Run the command `vagrant up`


There are two folders named "TESTS" and "GettingStarted" configured in the Vagrant configuration. The default sync method is rsync. It does not require you give root password. The rsync synced folder does a one-time one-way sync from the machine running to the machine being started by Vagrant.  

The default Sync folder settings.


```
./vagrant-selenium/TESTS --> VM --> /home/vagrant/TESTS
./vagrant-selenium/GettingStarted --> VM --> /home/vagrant/GettingStarted
```

You can change type: "rsync" to type: "nfs" in Vagrantfile for allowing you have real-time sync without reloading Vagrant. For Windows users: NFS folders do not work on Windows hosts. Vagrant will ignore your request for NFS synced folders on Windows.

In order to manage the collection of Protractor files in your project, you can also choose to make a symbolic link from the TESTES folder to your project workspace outside the node_modules folder for doing file sync between your test files and the VM.

```
$ cd YourNodeJSProject
$ ln -s vagrant-selenium/TESTS  MyProtractorTests
```

All files under MyProtractorTests will be synced to the VM fodler "/home/vagrant/TESTS/""

# Software Specifications

```
OS: Ubuntu trusty 64-bit (Ubuntu 14.04.3 LTS)
WindowMgr: Fluxbox
Default Storage: 40GB
Default Memory: 500Mb
Java: OpenJDK 1.7.0_91
SeleniumServer: v2.48.2
Protractor: v3.0.0
ChromeDriver: v2.20.353124
Node.js:  v4.2.4  (NPM 2.14.12)
Git: v1.9.1
Installed Browsers:
  - Firefox (v.43.0)
  - Google Chrome (v.47.0.2526.106 64bit)
NetworkInterfaces:
  NATAdapter: eth0: 10.x.x.x 
  HostOnlyAdapter: eth1: 192.168.33.10
```

# Network Configuration

```
              Internet
                 ^
                 | 
         [  Host ]
         |       ^
         v       |
    [VirtualBoxSoftware]  
         |       ^
         v       |
       [eth1]  [eth0]         
       [     VM     ]  
         eth0: 10.x.x.x  (NAT)
         eth1: 192.168.33.10  (HostOnly)
         lo: 127.0.0.1
         LocalSelenium: http://localhost:4444/wd/hub
         RemoteSelenium: http://192.168.33.10:4444/wd/hub
```

# Run VM

```
$ cd {YourNodeJSProject}/node_modules/vagrant-e2etesting-protractor
$ vagrant up
```

# Stop VM

```
$ cd {YourNodeJSProject}/node_modules/vagrant-e2etesting-protractor
$ vagrant halt
```

# Reload VM

```
$ cd {YourNodeJSProject}/node_modules/vagrant-e2etesting-protractor
$ vagrant reload
```

Selenium server will be started automatically on boot.

# Access VM using SSH

Username: vagrant  Password: vagrant

## Access VM using VagrantSSH (does not require password):

```   
$ cd {YourNodeJSProject}/node_modules/vagrant-e2etesting-protractor
$ vagrant ssh
```

## Access VM using SSH client (requires password):

```   
ssh vagrant@192.168.33.10
```

# Selenium addresses

There are two options you can set Selenium address of Protractor configuration.

### If you run Protractor inside the VM which is provided a complete Selenium infrastructure and Protractor, use this address

```
exports.config = {
  ...
  seleniumAddress: 'http://localhost:4444/wd/hub',
  ...
}
```

Running example 

```
$ cd {YourNodeJSProject}/node_modules/vagrant-e2etesting-protractor
$ vagrant ssh
$ cd ~/GettingStarted/runProtractorInsideVM
$ protractor conf.js
```

### If you run Protractor on your physical computer and use Selenium infrastructure inside the VM , use this address

```
exports.config = {
  ...
  seleniumAddress: 'http://192.168.33.10:4444/wd/hub',
  ...
}
```

Running example 

```
$ cd {YourNodeJSProject}/node_modules/vagrant-e2etesting-protractor/GettingStarted/runProtractorOutsideVM
$ protractor conf.js
```
If you dont have "protractor" command on your physical machine, Use npm to install Protractor globally with "npm install -g protractor"


# Modify Vagrant configuration 

### Memory provisioning

```
# Go to edit Vagrantfile (vb.memory = <MemoryInMB>)
$ vagrant reload
```

### Use NFS for folder sync

```
# Go to edit Vagrantfile with following lines
# config.vm.synced_folder "GettingStarted/", "/home/vagrant/GettingStarted" ,  type: "nfs"
# config.vm.synced_folder "TESTS/", "/home/vagrant/TESTS" ,  type: "nfs"

$ vagrant reload
```

### Use headless browser

```
# Go to edit Vagrantfile (vb.gui = false)
$ vagrant reload
```

### Use real browser

```
# Go to edit Vagrantfile (vb.gui = true)
$ vagrant reload
```

# Demo

It takes time for the first "vagrant up". You need to download BaseBox (the Ubuntu server) and to execute provisioning script to install a complete Selenium infrastructure and Protractor.

This screen recording demonstrates simplified Protractor test cases that borrow from [http://www.protractortest.org/#/tutorial](http://www.protractortest.org/#/tutorial). The screen recording shows you the steps to run test examples using real and headless browser.
 