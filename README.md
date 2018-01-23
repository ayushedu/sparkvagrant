# Installing Spark environment in Vagrant
The goal of this post is to setup single node spark cluster in vagrant. Vagrant will prevent the the base OS from getting corrupted.

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
$ wget --no-check-certificate -c --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/9.0.4+11/c2514751926b4512b076cc82f959763f/jdk-9.0.4_linux-x64_bin.tar.gz
$ tar -zxvf jdk-9.0.4_linux-x64_bin.tar.gz
```

Add lines in /home/vagrant/.bashrc
```vim
export JAVA_HOME=/home/vagrant/jdk-9.0.4
export PATH=$PATH:/home/vagrant/jdk-9.0.4/bin
```
## Installing Scala
```shell
$ wget https://github.com/sbt/sbt/releases/download/v1.1.0/sbt-1.1.0.tgz
$ tar -zxvf sbt-1.1.0.tgz
```

Add sbt in path: add below line in /home/vagrant/bashrc
```vim
export PATH=$PATH:/home/vagrant/sbt/bin
```
## Installing Hadoop
1. Download and extract hadoop
```shell
$ wget http://www-us.apache.org/dist/hadoop/common/hadoop-3.0.0/hadoop-3.0.0.tar.gz
$ tar -zxvf hadoop-3.0.0.tar.gz
$ ln -s hadoop-3.0.0 hadoop
```

2. Modify JAVA_HOME value in hadoop/etc/hadoop/hadoop-env.sh
```vim
export JAVA_HOME=/home/vagrant/jdk-9.0.4
```

3. Open port 9870 in vagrnt

## Installing Apache Spark
```shell
$ wget http://www-eu.apache.org/dist/spark/spark-2.2.1/spark-2.2.1-bin-hadoop2.7.tgz
$ tar -zxvf spark-2.2.1-bin-hadoop2.7.tgz
```
## Installing Apache Livy
```shell
$ sudo apt-get install unzip
$ wget http://www-eu.apache.org/dist/incubator/livy/0.4.0-incubating/livy-0.4.0-incubating-bin.zip
$ unzip livy-0.4.0-incubating-bin.zip
```

## Setup passphraseless ssh
```shell
$ ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa
$ cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
$ chmod 0600 ~/.ssh/authorized_keys
