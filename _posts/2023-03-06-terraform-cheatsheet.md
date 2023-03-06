---
layout: post
title: Terraform Cheatsheet
date: 2023-03-06 21:45 +0100
categories: [Systems, IaC]
tags: [iac, terraform]     # TAG names should always be lowercase
---
# Frequently used commands

Most basic workflow:
```zsh
❯ terraform plan
❯ terraform apply
❯ terraform destroy
```

List state of resources:
```zsh
❯ terraform state list
```

Destroy an specific resource:
```zsh
❯ terraform destroy -target nutanix_virtual_machine.vm
```