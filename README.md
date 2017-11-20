# shotcaller-vagrant
Initializes a Vagrant box provisioned for development on Shotcaller


# Prerequisites

* Chocolatey (Run from elevated Powershell)  
```
Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```

* Vagrant
* ChefDK
* VirtualBox Guest Additions plugin
* Omnibus plugin
* Berkshelf plugin

```
$ choco install vagrant
$ choco install chefdk
$ vagrant plugin install vagrant-vbguest
$ vagrant plugin install vagrant-omnibus
$ vagrant plugin install vagrant-berkshelf
```
# Usage

`$ vagrant up`


