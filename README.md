# django3-ubuntu64-box-vagrant

Quickly build a clean virtual environment ready for Django development.
Vagrant Box, Ubuntu 64 bits, Python3, Virtualenv, Postgres9.4, Django 1.8.5
(Based on aminehaddad's https://github.com/aminehaddad/django-environment-in-vagrant)

## Getting started

Install the following applications in your host operating system:

* [VirtualBox](https://www.virtualbox.org/)
* [Vagrant](https://www.vagrantup.com/)

The following Vagrant plugin is recommended to keep the VirtualBox guest additions automatically updated:

* [vagrant-vbguest](https://github.com/dotless-de/vagrant-vbguest)

This is how you install vagrant-vbguest:

	vagrant plugin install vagrant-vbguest

## Getting the source code

Retrieve the source code:

	git clone https://github.com/ealanisg/django3-ubuntu64-box-vagrant.git my-project
	cd my-project

After clone edit file _conf/vagrant_setup.sh (line 45)
In order to apply correct user and password

	echo "Configuring postgres.."
	sudo -u postgres psql -c "create user vagrant with password 'vagrant';"
	sudo -u postgres psql -c "create database vagrant;"
	sudo -u postgres psql -c "grant all privileges on database vagrant to vagrant;"

Where `my-project` is the name of your new website or project.

## Starting the virtual machine development environment

The following command will start the environment:

	vagrant up

The installation script will run within the virtual machine if it is the first time it is started (in order to install the required packages).

## Setting up the virtual machine development environment

SSH into the virtual machine:

	vagrant ssh

The source code is shared with the virtual machine in this directory:

	cd site

Always run the following command to use the proper python virtual environment:

	workon site

Install the required python packages:

	pip install -r requirements.txt

## Setting up a Django project

Create a new Django project. Pay attention to the `.` at the end of that command if you did `cd site`:

	django-admin.py startproject my_site .

Setup the database models and run migrations:

	./manage.py migrate

You can now start the development web server:

	./manage.py runserver 0.0.0.0:8080

Access this URL:

* [http://10.10.10.10:8080](http://10.10.10.10:8080/)

To turn off the virtual machine, run the following from your host terminal:

	vagrant halt -f

To turn on the virtual machine, run the following:

	vagrant up

## Troubleshooting

This section is reserved for common troubleshooting problems or hints.

#### Question: How can I change the git repository this is committing to?

Answer: You can fix that in the virtual environment by deleting the `.git` directory and re-initializing it. Example:

	vagrant ssh
	cd site
	rm -rf .git
