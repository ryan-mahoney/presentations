# Vagrant
---

## What is Vagrant

From the official website:

Create and configure lightweight, reproducible, and portable development environments.

Runs on Mac, Linux and Windows.

Built in ruby, free, open-source.

Compatible with mainstream hypervisors, ie, VirtualBox, VMware and even Docker.

---
## Problem Solved: Reproducible

A reproducible local dev server environment, that can be re-created from the ground up at any time.

Story: AddUp.org QA person... 

Story: SoulCycle "right of passage"

---

## Problem Solved: Light-Weight

Light-weight local server environment. 

Working inside a virtualized environment is unnecessarily tedious.

Work using the full power of your "host" operating system, test your applications on a small local container.

---

## Problem Solved: Sharing

Developers need to share their environments with their team.

Vagrant files are a few small text files.

No more distributing huge virtual appliances.

---

## Problem Solved: Containment

Some people install PHP (for example) locally on their own machine using a tool like MAMP.

This may work great for some people, until they are working on two projects simultaneously that have conflicting dependencies.

Case in point, when I do hobbyist PHP, I use PHP 5.6, HHVM or even 7.  To run our work environment, we need PHP 5.3.

Solution, don't run any PHP on host, run 2 separate containers.

---

## Basics: Host vs Guest

There are two operating systems, your "host" or you actual PC, and another one running virtually, typically some flavor of Linux, this is your "guest" operating system.

Personally I run a Ubuntu 12 Guest inside a Ubuntu 14 Host, but it is very common to run a Mac OS host, annecdotaly, most Vagrant users are running a Mac OS host. 

Mac may be Unix-like, but it's still a ghetto for running and managing a server.

---

## Basics: Virtualization

Vagrant is basically a utility to make it easier to spin up, down and suspend virtual machines of different flavors running different configurations. When you run Vagrant, you still need a VM.

I run VirtualBox, but VMWare is also popular. 

Docker is gaining momentum and is supported, I haven't gotten it to work as of yet. My understanding is that it is more light weight than traditional VMs.  One day :)

---

## Basics: Installed Software

Host: Sublime, Git and your source code
Guest: Apache, MySQL, PHP, Memcache, Redis, etc.

---

## Basics: Synchronization

This is a sore spot for Vagrant. Files needs to be synchronized between guest and host. Although the VMs themselves have support for this, it tends to be too slow for quickly catching file changes in large code-bases.

Currently, I run an extension called gatling that watches my local code repositories and synchronized modified files to the VM.

---

## In Action: Vagrantfile

```ruby
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    config.vm.box = "hashicorp/precise64"
    config.vm.provision "shell", path: "provision.sh"
    config.vm.network "forwarded_port", guest: 80, host: 8080

    config.vm.synced_folder "./betterlesson", "/var/www/betterlesson", 
        type: "rsync", rsync__exclude: [".vagrant/", ".git/"], 
        rsync__args: ["--verbose", "--archive", "-z", "--copy-links", "--copy-dirlinks"]

    config.vm.provider "virtualbox" do |vb|
        vb.customize ["modifyvm", :id, "--memory", "4096"]
    end
end
```

---

## In Action: provision.sh

```bash
#!/bin/sh
sudo apt-get update
sudo apt-get install -y pv git vim curl multitail apache2 php5 php5-curl \
     php5-mysql php-apc ruby1.8 rubygems1.8 ruby1.8-dev default-jdk

sudo mkdir /var/www/betterlesson/app/tmp/logs

echo "ServerName betterlesson
<VirtualHost *:80>
    DocumentRoot /var/www/betterlesson/
</VirtualHost>
" | sudo tee -a /etc/apache2/sites-available/betterlesson.conf

# database
sudo debconf-set-selections <<< 'mysql-server mysql-server/root_password password root'
sudo debconf-set-selections <<< 'mysql-server mysql-server/root_password_again password root'
sudo apt-get -y install mysql-server
echo "create database betterlesson_dev;" | mysql -u root -proot
zcat /var/www/dbdump/dump_for_dev_vm.sql.gz | mysql -u root -proot betterlesson_dev

exit 0
```

---

## Usage

```bash
vagrant provision
vagrant up
vagrant ssh
vagrant suspend
vagrant halt
vagrant destroy

vagrant rsync
vagrant gatling-rsync-auto
```
