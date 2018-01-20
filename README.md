# Installing Spark environment in Vagrant
The goal of this post is to setup spark environment in vagrant environment, so that it doesn't corrupt of affect the base OS. 

Vagrant is an open-source software product for building and maintaining portable virtual software development environments,[4] e.g. for VirtualBox, Hyper-V, Docker, VMware, and AWS. More information can be found on https://www.vagrantup.com/intro/getting-started/index.html

## Installing vagrant
Follow the vagrant getting started guide (https://www.vagrantup.com/intro/getting-started/index.html)

Below are the steps:
* Install vagrant
Download package from (https://www.vagrantup.com/downloads.html)
* Project Setup
```shell
$ mkdir vagrant_getting_started
$ cd vagrant_getting_started
$ vagrant init
```
* Installing Vagrant Box
```shell
$ vagrant box add hashicorp/precise64
```

Edit the Vagrantfile

```vim
Vagrant.configure("2") do |config|
  config.vm.box = "hashicorp/precise64"
end
```

* Starting the machine

```shell
$ vagrant up
$ vagrant ssh
```

Once we have logged into the vagrant machine we can install the other components.

## Installing Java
To download JDK we need to accept the license term. In the below wget we are accepting the license term by setting the cookie in header.
```shell
wget --no-check-certificate -c --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/9.0.4+11/c2514751926b4512b076cc82f959763f/jdk-9.0.4_linux-x64_bin.tar.gz
```

Add lines in /home/vagrant/.bashrc
```vim
export JAVA_HOME=/home/vagrant/jdk-9.0.4
export PATH=$PATH:/home/vagrant/jdk-9.0.4/bin
```
## Installing Scala
Downlaod sbt
```shell
wget https://github.com/sbt/sbt/releases/download/v1.1.0/sbt-1.1.0.tgz
```

untar 
```shell
tar -zxvf sbt-1.1.0.tgz
```

Add sbt in path: add below line in /home/vagrant/bashrc
```vim
export PATH=$PATH:/home/vagrant/sbt/bin
```
## Installing Hadoop

## Installing Apache Spark
## Installing Apache Livy
## Installing Mysql

