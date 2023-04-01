---
layout: post
title: Ansible Fundamentals
date: 2023-03-29 23:15 +0100
categories: [Systems, IaC]
tags: [iac, ansible, cheatsheet]  
---

This is a cheatsheet for ansible to help remember the most common commands.

# Ansible adhoc command sheet

With `ansible` adhoc commands you can run ansible modules without the need of a playbook.

| Command                                                                    | Operation                                                   |
| -------------------------------------------------------------------------- | ----------------------------------------------------------- |
| ```ansible hosts -m module [-a 'mudule args'] [-i inventory]```            | Run a module on hosts                                       |
| ```ansible all -m ping```                                                  | Ping remote hosts                                           |
| ```ansible all -m service -a "name=httpd state=started"```                 | Check if a service is currently running                     |
| ```ansible all -m command -a "cat /proc/meminfo"```                        | Runs any command. It makes use of python                    |
| ```ansible all -m shell -a set```                                          | Runs any command. It makes use of shell                     |
| ```ansible all -m raw -a "cat /proc/meminfo"```                            | Runs any command. It makes use of shell. Don't need Python. |
| ```ansible all -m user -a "name=testUser"```                               | Create and delete an user                                   |
| ```ansible all -m user -a "name=testUser state=absent"```                  | Delete an user                                              |
| ```ansible all -m copy -a "src=/etc/hosts dest=/tmp/hosts"```              | Copy a file from local to remote                            |
| ```ansible all -m copy -a "content='Message of the day' dest=/etc/motd"``` | Copy a file from local to remote                            |

# Ansible playbook

With `ansible-playbook` you can run a playbook.

| Command                                                                 | Operation                                               |
| ----------------------------------------------------------------------- | ------------------------------------------------------- |
| ```ansible-playbook playbook.yml```                                     | Run a playbook                                          |
| ```ansible-playbook playbook.yml --syntax-check```                      | Check syntax of a playbook                              |
| ```ansible-playbook playbook.yml --list-hosts```                        | List hosts in a playbook                                |
| ```ansible-playbook playbook.yml --list-tasks```                        | List tasks in a playbook                                |
| ```ansible-playbook playbook.yml --list-tags```                         | List tags in a playbook                                 |
| ```ansible-playbook playbook.yml --tags "tag1,tag2"```                  | Run only tasks with tag1 and tag2                       |
| ```ansible-playbook playbook.yml --skip-tags "tag1,tag2"```             | Skip tasks with tag1 and tag2                           |
| ```ansible-playbook playbook.yml --start-at-task "task name"```         | Start at a specific task                                |
| ```ansible-playbook playbook.yml --step```                              | Run playbook in step-by-step mode                       |
| ```ansible-playbook playbook.yml --diff```                              | Show diff of changes                                    |
| ```ansible-playbook playbook.yml --check```                             | Run a playbook in check mode                            |
| ```ansible-playbook playbook.yml --limit "host1,host2"```               | Run a playbook on specific hosts                        |
| ```ansible-playbook playbook.yml --limit "host1,host2" --tags "tag1"``` | Run a playbook on specific hosts and with specific tags |

# ansible-doc

With `ansible-doc` you can get documentation for one particular module.

| Command                            | Operation                                         |
| ---------------------------------- | ------------------------------------------------- |
| ```ansible-doc -l```               | List available modules                            |
| ```ansible-doc <module_name>```    | Get documentation for one particular module       |
| ```ansible-doc -s <module_name>``` | Get short documentation for one particular module |