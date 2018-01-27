---
layout: post
title: Vagrant - 用黑盒子(box CLI)操作 virtualbox
excerpt: "透過很方便的可以透過 command line 來啟動 virtualbox"
categories: articles
tags: [vagrant, vitrualbox, docker]
comments: true
---

# Vagrant - 用黑盒子(box CLI)操作 virtualbox

- vagrant 支持 Virtualbox 及 VMWare, 是很方便的虛擬機管理程式，讓程式開發人員使用虛擬機(VM)就像本機一樣方便
- vagrant 裡的 **box** 是已經準備好了的 VM, 有現成的可以下載不需要自己安裝 linux
- Vagrantfile, 用來定義 VM 的配置

```txt
    Vagrant.configure("2") do |config|
      config.vm.box = "centos/7"
      config.vm.box_version ="1704.01"
      config.vm.provision :shell, path: "bootstrap.sh"
      config.vm.network :forwarded_port, guest: 80, host: 4567
    end
```
- **Provision** - 卜設定 VM 啟動後執行 bootstrap.sh

```bash
    #!/usr/bin/env bash
    sudo yum install -y httpd.x86_64
    sudo service httpd start
    if ! [ -L /var/www ]; then
      rm -rf /var/www
      ln -fs /vagrant /var/www
    fi
```
- 常用指令
  - vagrant init - Create Vagrantfile
  - vagrant box add <boxName> - 建立一個 box ( 例如:  “cantos/7”)
  - vagrant up - 啟動 VM (若 box 不存在則重新下載，並執行 provision)
  - vagrant ssh - 進入VM 的命令列 
  - vagrant box remove <boxName>
  - VM 操作

```bash
    > vagrant reload --provision
    > vagrant halt
    > vagrant suspend
```
  - 全部刪除, 只要有 Vagrantfile, 透過 vagrant up 可以重新下載及 provision

```bash
    >vagrant destory
```

