# Simple Ansible Infrastructure Orchestration Example

Ansible playbooks are flexible and powerful. But sometimes, you just need to run a single command on a set of hosts. That's where the simple `ansible` command comes in handy.

Just like the device in Ender's Game, the `ansible` command allows you to run commands or call Ansible modules immediately on one or one hundred of servers.

This project configures three Virtual Machines using Vagrant and VirtualBox: `app1`, `app2`, and `db`, to emulate a small-scale real-world infrastructure (two application servers and a database server), so you can practice running `ansible` commands across them, and work on a flexible Ansible inventory.

## Quick Start Guide

### 1 - Install dependencies (VirtualBox, Vagrant, Ansible)

  1. Download and install [VirtualBox](https://www.virtualbox.org/wiki/Downloads).
  2. Download and install [Vagrant](http://www.vagrantup.com/downloads.html).
  3. [Mac/Linux only] Install [Ansible](http://docs.ansible.com/intro_installation.html).

Note for Windows users: *This guide assumes you're on a Mac or Linux host. Windows hosts are unsupported at this time.*

### 2 - Build the Virtual Machine

  1. Download this project and put it wherever you want.
  2. Open Terminal, cd to this directory (containing the `Vagrantfile` and this README file).
  3. Type in `vagrant up`, and let Vagrant do its magic.

Note: *If there are any errors during the course of running `vagrant up`, and it drops you back to your command prompt, just run `vagrant provision` to continue building the VM from where you left off. If there are still errors after doing this a few times, post an issue to this project's issue queue on GitHub with the error.*

### 3 - Create an Inventory file, and run `ansible` commands

Read through the third chapter of [Ansible for DevOps](https://www.ansiblefordevops.com/) for details.


ansible multi -a "hostname"
ansible multi -a "hostname" -f 1

ansible multi -a "df -h"
ansible multi -a "free -m"

ansible multi -m setup

ansible multi -a "date"
ansible multi -a "bash -c 'rm /etc/localtime && cp /usr/share/zoneinfo/Asia/Riyadh /etc/localtime'" -b
ansible multi -a "date" --limit "192.168.60.4"
ansible multi -a "free -h" --limit "*.4"

#### Other commands from the book:
ansible multi -b -m yum -a "name=chrony state=present"
ansible multi -b -m service -a "name=chronyd state=started enabled=yes"
ansible multi -b -m service -a "name=chronyd state=stopped"
ansible multi -b -m service -a "name=chronyd state=started"

ansible app -b -m yum -a "name=mysql-python state=present"
ansible app -b -m yum -a "name=python-setuptools state=present"
ansible app -b -m easy_install -a "name=django"


ansible multi -m stat -a "path=/etc/environment"
ansible multi -m copy -a "src=/etc/hosts dest=/tmp/hosts"
ansible multi -b -m fetch -a "src=/etc/hosts dest=/tmp"
ansible multi -m file -a "dest=/tmp/test mode=644 state=directory"
ansible multi -m file -a "dest=/tmp/test state=absent"
ansible multi -b -B 3600 -P 0 -a "yum -y update"