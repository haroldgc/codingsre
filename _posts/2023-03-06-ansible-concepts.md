---
layout: post
title: Ansible concepts
date: 2023-03-06 23:06 +0100
---


# Installing Ansible

1. On all nodes Create user.

```zsh
❯ sudo useradd ansible
❯ echo ansible123 | sudo passwd --stdin ansible
❯ echo "ansible ALL=(ALL) NOPASSWD:ALL" | sudo tee /etc/sudoers.d/ansible
```

2. On control node generate ssh key

```zsh
❯ su - ansible
❯ ssh-keygen
```

3. Distribute to other nodes

```zsh
❯ ssh-copy-id <hostname/IP>
```

4. Install python3

```zsh
❯ sudo yum install python3
❯ sudo yum -y install python3-pip
❯ sudo alternatives --set python /usr/bin/python3
```

5. Install ansible with ansible user

```zsh
❯ su - ansible
❯ pip3 install ansible --user
❯ ansible --version
```


# Inventory

Is a list of hostname and IP addresses managed by Ansible

+ Useful for:
  + Define groups
  + ~~Set variables (not best approach)~~

+ Types:
  + __Static inventory__ : File with names or IP servers.
  + __Dynamic inventory__ : Scripts that discover servers in a cloud environment.


##  Static inventory

+ Hosts can be grouped
+ A host can be member of multiple groups
+ Nested groups are allowed
+ Common pattern project-based inventory files
+ Ranges can be used, eg: server[1:10], 192.168.[4:5].[0:255]
+ Default location: __/etc/ansible/hosts__
+ Alternative inventory location can be specified in ansible.cfg. Or use option __-i inventory__

Example of static inventory file:

```ini
[webservers]
web01.example.com
web02.example.com

[databases]
db01.example.com
db02.exanoke.com

[servers:children]
webservers
databases
```

Types of organizations can be:

+ Functional host groups
  + web
  + databases
+ Regional host groups
  + europe
  + america
+ Staging host groups
    + test
    + development
    + production

## Dynamic inventory

+ Can be used to discover inventory in dynamic environments such as cloud.

+ There are community-provided inventory scripts.

# Configuration files

## ansible.cfg example

```ini
[defaults]
inventory = inventory
remote_user = ansible
host_key_checking = false

[privilege_escalation]
become = True
become_method = sudo
become_user = root
become_ask_pass = False
```

## Common options

+ inventory: path to inventory file.
+ remote_user: user that logs in on the remote host.
+ ask_pass: specifies whether or not to prompt for a password.
+ become: indicate if you want to automatically switch to the become_user.
+ become_method: hot to become the other user. sudo is the default.
+ become_user: target remote user.
+ become_ask_pass: if password should be asked for when escalating.

## localhost

+ Ansible has an implicit localhost entry to run Ansible commands on the localhost.
+ default __become__ settings are not used.
+ need to ensure the account used has sudo privileges.

## Managing configuration files

Order of precendence is as follow:

1. ```/etc/ansible/ansible.cfg``` is the default.
2. ```~/.ansible.cfg``` overwrite the default if exist.
3. ```./ansible.cfg``` always have precedence if exist.
4. ```ANSIBLE_CONFIG``` environment variable always have precedence.

Use command ```ansible --version``` to find which configuration file is currently being used.

```zsh
❯ ansible --version
ansible [core 2.13.5]
  config file = None
  configured module search path = ['/home/ansible/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /home/ansible/.local/lib/python3.10/site-packages/ansible
  ansible collection location = /home/ansible/.ansible/collections:/usr/share/ansible/collections
  executable location = /home/ansible/.local/bin/ansible
  python version = 3.10.7 (main, Sep  7 2022, 00:00:00) [GCC 12.2.1 20220819 (Red Hat 12.2.1-1)]
  jinja version = 3.1.2
  libyaml = True
```

# Using AdHoc commands and ansible modules

Execute a command agains a group of hosts.
```zsh
❯ ansible hosts -m module [-a 'mudule args'] [-i inventory]
```

Example:

+ To create and delete an user:
```zsh
❯ ansible all -m user -a "name=testUser"
❯ ansible all -m user -a "name=testUser state=absent"
❯ ansible all -m command -a "id ansible"
```

+ Run a command in hosts:
```zsh
❯ ansible all -m command -a "uname -a"
❯ ansible all -m command -a "cat /proc/cpuinfo"
```

+ Ping remote hosts:
```zsh
❯ ansible all -m ping
```

# Modules

## Getting module's help

What do you want to do? Many modules out of the box.

To list available modules:
```zsh
❯ ansible-doc -l
```

To get documentation for one particular module:
```zsh
❯ ansible-doc <module_name>
```

## Essential Ansible modules

+ **ping**: Verify connectivity with hosts.
  ```zsh
  ❯ ansible all -m ping
  ```

+ **service**: Check if a service is currently running.
  ```zsh
  ❯ ansible all -m service -a "name=httpd state=started"
  ```

+ **command**: Runs any command. It makes use of python.
  ```zsh
  ❯ ansible all -m command -a "cat /proc/meminfo"
  ```

+ **shell**: Runs any command. It makes use of shell.
  ```zsh
  ❯ ansible all -m shell -a set
  ```

+ **raw**: Runs a command on a remote host without a need for Python.

+ **copy**: Copies a file to managed host.
  ```zsh
  ❯ ansible all -m copy -a 'content="Welcome to Host" dest=/etc/motd'
  ```



# Playbooks, plays and tasks

+ Used to run multiple tasks agains managed hosts in an automatic way.
+ **Playbooks** are composed of one or more **plays**.
+ **Play** are a series of tasks that are executed agains selected hosts. Each **play** runs one or more **tasks**.
+ and **tasks** use different modules to perform the actual work.

## Playbook's anatomy
```yml
---
- play 1 
  --- 
  tasks:
  - name 1:
    module:
      arg 1
      arg 2
  - name 2:
    modules:
      arg 1
      arg 2
- play 2
  ---
  task 1:
  - name 1:
    module:
      arg 1
      arg 2
  - name 2:
      arg 1
      arg 2
```

## Playbooks commands

**Syntax check command:**
```zsh
❯ ansible-playbook [-vvvv] [-C] --syntax-check dev.ansible.yml
```

+ ```-v```: Show task results.
+ ```-vv```: Show task results and task configuration.
+ ```-vvv```: Add information about connections to managed hosts.
+ ```-vvvv```: Add information about plug-ins, users used to run scripts and names of scripts that are executed.
+ ```-C```: Dry run.

**Dry run command:**
```zsh
❯ ansible-playbook [-vvvv] -C dev.ansible.yml
```

**Run a playbook:**
```zsh
❯ ansible-playbook dev.ansible.yml
```

## Plays
### Usefull plays parameters

+ ```remote_user```: The name of the remote user.
+ ```become```: Enable or disable privilege escalation.
+ ```become_method```: Alternative become method. Default is **sudo**.
+ ```become_user```: Target user for privilege escalation.

# Variables

To refer to a variable use:
```yml
{ { variable } }
```

Can be set a different levels: 

+ Playbook (not very flexible)
+ Inventory (depracated)
+ Inclusion files (recommended)
+ Localfact (facts are special type of variables to represent current state of managed devices)

Variable names restrictions:

+ Start with letter.
+ Can only contain letters, numbers and underscores.

Variables in playbooks example:
``` yml
- hosts: all
  vars:
    web_package: httpd
```

Variables in include file:
```yml
- hosts: all
  vars_files:
    - vars/users.yml
```
