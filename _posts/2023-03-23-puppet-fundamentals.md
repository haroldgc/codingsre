---
layout: post
title: Puppet Fundamentals
date: 2023-03-23 22:42 +0100
categories: [Systems, IaC]
tags: [iac, puppet, cheatsheet]  
---

> "The real voyage of discovery consists not in seeking new landscapes, but in having new eyes." ― Marcel Proust

Puppet is a configuration management tool. It uses a client-server model consisting of the Puppet server and Puppet agents. I has its own declarative language to describe systems configuration.

![Puppet client server model](/assets/img/posts/2023-03-23-puppet-client-server-model.png)
_Puppet client server model_

The Puppet Server is in charge of collecting system information from Puppet agents. And Puppet Agents collect and modify system configuration and send the status to the Puppet Server. The communication is done using SSL over TCP ports 8140 and 8142.

Some of the Operating Systems supported by Puppet are:

* Linux
* Windows
* macOS
* Many network devices
* Solaris
* AIX
* Raspberry Pi

It uses a declarative approach in which you define the way you want a system to be configured (*desired state*) and Puppet will enforce the configuration.

There are two available Puppet distribution: Open Source Puppet, and Puppet Enterprises (PE). Where PE provides a set of features like: PuppetDB built-in, Web UI, RBAC, and others.

# System prerequisites

* Ensure time is in sync between Server and Agents. Issues with certificates can arise if there is time drifts.
* The primary server must be able to resolve its own hostname.
* Agents must reach primary server during installation.
* Network ports that needs to be enables: 
  * **443** Web console
  * **8140** Agent management: Inbound traffic/requests from agent nodes
  * **8141** Run actions remotely against target agent nodes via the PXP agent service

# Deployment

## Puppet Server install

1. Download installer (URL may varies).

```bash
$ curl -JLO 'https://pm.puppet.com/cgi-bin/download.cgi?dist=el&rel=7&arch=x86_64&ver=2019.8.6'
```

2. Unpack the installer.

```bash
$ tar -xf puppet-enterprise-2019.8.6-el-7-x86_64.tar.gz
```

3. Run the installer.

```bash
$ ./puppet-enterprise-2019.8.6-el-7-x86_64/puppet-enterprise-installer
```

4. Set the password for the Puppet Enterprise console.

```bash
$ puppet infrastructure console_password --password=<PASSWORD>
```

5. Run Puppet by executing the following command twice. Running Puppet twice ensures that all of the post-configuration operations are complete and that PE is running.

```bash
$ puppet agent -t
```

6. Check the status of Puppet service.

```bash
$ puppet infrastructure status
```

7. After this the Web console login should be available on port **443**.

![Puppet client server model](/assets/img/posts/2023-03-23-puppet-web-console-login.png)
_Web console login_

8. You should be able to login into the web console, and clicking in *Puppet Services status* should show you all of them Operational.

![Puppet client server model](/assets/img/posts/2023-03-23-puppet-web-console.png)
_Web console_