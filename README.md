# Elasticsearch Vagrant Box

This vagrant box installs elasticsearch on Ubuntu 16.04 

## Disclaimer

This install is not secured and should *not* be used in a production setting. It is only suitable for local machine learning activities.

## Prerequisites

[VirtualBox](https://www.virtualbox.org/) and [Vagrant](http://www.vagrantup.com/) (minimum version 1.6)

Mac quickstart with [HomeBrew](http://brew.sh/):
```
brew cask install virtualbox
brew cask install vagrant
brew cask install vagrant-manager
```

## Getting Started

To start the vagrant box run:
```
vagrant up
```
To log in to the machine run:
```
vagrant ssh
```
Elasticsearch will be available on the host machine at [http://localhost:9200/](http://localhost:9200/) 

## Vagrant commands

```
vagrant up # starts the machine
vagrant ssh # ssh to the machine
vagrant halt # shut down the machine
vagrant up --provision # re-applies provisioning
```

##Elasticsearch commands

Installed via debian package and automatically started on boot.
Elasticsearch control:
```bash
sudo service elasticsearch (start/stop/restart)
```
