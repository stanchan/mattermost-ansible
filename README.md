# mattermost-ansible
This is an Ansible Playbook that installs a standalone version of Mattermost, which is an open-source Slack alternative.
This playbook installs Mattermost Team Edition version 3.9.0 by default.

It downloads the binary from [mattermost.org](https://www.mattermost.org/download/). This playbook installs
 * `postgresql` - Database Server
 * `nginx` - Web Server (acts as a reverse proxy)
 * SSL certificates are automatically generated from the [letsencrypt](https://letsencrypt.org) project. A cron job is
 created that automatically renews the SSL certificates once a week.

---

This is a fork of [tjtoml/mattermost-ansible](https://github.com/tjtoml/mattermost-ansible) that seems
inactive since the end of 2016. This fork only supports Ubuntu 16.04.
For Ansible to be able to do its job you need in install Python first: `apt-get install python`.

---

## Usage
* Install Ansible with your package manager of choice. Ansible can also be installed via `pip`. This playbook was first
written and tested with Ansible 2.3.0. If you can, I would recommend running the most recent version of Ansible.

* Clone this repository.

* Make sure that the server you are installing Mattermost is properly configured with a FQDN. You should also have root
 access via ssh.

* Copy `play.example.yml` to `play.yml` and change the `vars` to reflect any changes you may want to make for your system.
This playbook does not do a complete installation with full configuration of all of the Mattermost options, but rather 
installs it to the point where you can edit the relevant settings from within the web browser.

* **You should *always* edit the email address and db_password fields.** 

* Create a `hosts` file in the project directory. It only needs to contain one line, which is the IP address of the server
you wish to install Mattermost on.

* Run `ansible-playbook play.yml -i hosts` from the top of level of the project directory.

* Navigate to the FQDN of your server in a web browser. Consult the Mattermost documentation for further configuration
options.

---

## Post-Install
If you are planning to use MatterMost for any length of time, you should probably change the location of the
data directory. A large volume of attached block storage would not be a bad idea. A working email server should also
be configured for email notifications and invites.  You can do most of this from within the browser without manually editing
configuration files.

---

### Contributing  
Please submit pull requests! They make my day. 

### Moving Forward
I am currently working on porting this standalone playbook into a more defined Ansible role with a complete implementation of all the options in the Mattermost `config` file. You can check on the status of this project [here.](https://github.com/tjtoml/ansible-role-mattermost)
