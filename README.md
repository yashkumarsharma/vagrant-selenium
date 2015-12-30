```
Tested on MacOS 10.11.2 , Vagrant 1.7.4, VirtualBox 5.0.12 
```

# Pre-installed Selenium server Vagrant configuration for a complete AngularJS E2E Testing with Protractor (ubuntu/trusty64)

# Install

```
$ git clone https://github.com/vorachet/vagrant-e2etesting-protractor.git
$ cd vagrant-e2etesting-protractor
$ vagrant up
```

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
    [       Host       ]
         |       ^
         v       |
    [VirtualBoxSoftware]  
         |       ^
         v       |
       [eth1]  [eth0]         
       [    VM      ]  
         eth0: 10.0.2.15  (NAT)
         eth1: 192.168.33.10  (HostOnly)
         lo: 127.0.0.1
         LocalSelenium: http://localhost:4444/wd/hub
         RemoteSelenium: http://192.168.33.10:4444/wd/hub
```


# Running VM

```
$ vagrant up
```

Selenium server will be started automatically on boot.

# Accessing VM using SSH

Username: vagrant  Password: vagrant

Use VagrantSSH (does not require password):

```   
$ vagrant ssh
```

Use SSH client (requires password):

```   
ssh vagrant@192.168.33.10
```

# Pre-installed Selenium server Vagrant configuration for a complete AngularJS E2E Testing with Protractor (ubuntu/trusty64) 


# Running Protractor inside VM

Set Selenium address to [http://localhost:4444/wd/hub]()

# Running Protractor outside VM

Set Selenium address to [http://192.168.33.10:4444/wd/hub]()

# Running test script examples

```
$ cd ~/GettingStarted/examples/SimpleTest
$ protractor conf.js
```

# Modifying Vagrant configuration 

### Memory provisioning

```
$ vagrant halt
# Go to edit Vagrantfile (vb.memory = <MemoryInMB>)
$ vagrant up
```

### E2E Testing Headless mode

```
$ vagrant halt
# Go to edit Vagrantfile (vb.gui = false)
$ vagrant up
```

### E2E Testing GUI mode

```
$ vagrant halt
# Go to edit Vagrantfile (vb.gui = true)
$ vagrant up
```

