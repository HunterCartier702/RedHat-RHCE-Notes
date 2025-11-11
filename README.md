# RedHat-RHCE-Notes

## Table of Contents

  - [Introduction](#intro)
  - [Lab Setup](#lab)
  - [Inventory and Ansible.cfg](#files)


## <a name="intro"></a>Introduction 
I passed the RHCSA exam 300/300. Now I am taking on the RHCE certification. This is a compilation of my lab setup, notes, and some playbooks. 

## <a name="lab"></a>Lab Setup
For the lab I decided to use VirtualBox. I downloaded a rhel-9.6.iso with my Red Hat developer account. I setup a control node with a GUI to run ansible and 2 managed nodes with the minimal install (no gui).

***I configured the managed nodes with 2 network interfaces each on their own network for any networking playbooks. I will use the "192" network for the main communication and the "10" network to run any networking playbooks on***
<p align="center"><img alt="Network" src="RHCE/1networks.png" height="auto" width="800"></p>

***I added an extra hard disk which will be on /dev/sdb for any Partitioning and LVM playbooks. I added the rhel iso to mount and create a local repository for each node to install packages from which will be on /dev/sr0. I also practiced with using the control node to mount the rhel iso and to host an HTTP repo and connect the nodes to it.***
<p align="center"><img alt="storage" src="RHCE/2storage.png" height="auto" width="800"></p>

***After I had configured everything I made sure to take snapshots, so that I could easily start over with a fresh lab and not have to setup all the minuscule tidbits again. Highly recommend***
<p align="center"><img alt="snapshots" src="RHCE/3snapshots.png" height="auto" width="800"></p>

***I now have the lab setup with the user "ansible" on all nodes who has NOPASSWD sudo privs(insecure) but great for RHCE and convenience. I used ssh-keygen then ssh-copy-id for user ansible to copy the key over on both nodes. Everything is now setup and working.***
<p align="center"><img alt="snapshots" src="RHCE/4pong.png" height="auto" width="800"></p>

## <a name="files"></a>Inventory, Ansible.cfg, and Hosts Files
For this simple network I used a static inventory file in my current project directory. In a minimal form, a static inventory is a list of hostnames to be managed by Ansible.

```shell
$ mkdir rhce && cd rhce
$ cat inventory 
[dev]
node1

[prod]
node2

[servers:children]
dev
prod
```

The ansible.cfg file defines Ansible’s configuration settings — it controls things like inventory location, privilege escalation, logging, and connection options.

```shell
$ cat ansible.cfg
[defaults]
# (pathlist) Comma separated list of Ansible inventory sources
inventory = inventory

# (string) Sets the login user for the target machines
# # When blank it uses the connection plugin's default, normally the user currently executing Ansible.
remote_user = ansible

# (boolean) This controls whether an Ansible playbook should prompt for a login password.
# If using SSH keys for authentication, you probably do not need to change this setting.
ask_pass = false

[privilege_escalation]
# (boolean) Toggles the use of privilege escalation, allowing you to 'become' another user after login.
become = true

# (string) Privilege escalation method to use when `become` is enabled.
become_method = sudo

# (string) The user your login/remote user 'becomes' when using privilege escalation, most systems will use 'root' when no user is specified.
become_user = root

# (boolean) Toggle to prompt for privilege escalation password.
become_ask_pass = false
```

We also need hostname resolution to address managed hosts by name. I will use /etc/hosts for this

```shell
$ cat /etc/hosts
127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
::1         localhost localhost.localdomain localhost6 localhost6.localdomain6
192.168.1.100	control.server control
192.168.1.10	node1.local node1
192.168.1.20	node2.local node2
```

[Back to Top](https://github.com/HunterCartier702/RedHat-RHCE-Notes/blob/main/README.md#intro)
