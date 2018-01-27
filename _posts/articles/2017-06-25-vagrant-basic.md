---
layout: post
title: Vagrant - 用黑盒子(box CLI)操作 virtualbox
excerpt: "透過很方便的可以透過 command line 來啟動 virtualbox"
categories: articles
tags: [vagant, vitrualbox, docker]
comments: true
---

# Vagrant - 用黑盒子(box CLI)操作 virtualbox

- vagrant 支持 Virtualbox 及 VMWare
- box 是已經準備好了的 VM
- Vagrantfile, 用來定義 VM 的配置
    Vagrant.configure("2") do |config|
      config.vm.box = "centos/7"
      config.vm.box_version ="1704.01"
      config.vm.provision :shell, path: "bootstrap.sh"
      config.vm.network :forwarded_port, guest: 80, host: 4567
    end
- **Provision** - 卜設定 VM 啟動後執行 bootstrap.sh
    #!/usr/bin/env bash
    sudo yum install -y httpd.x86_64
    sudo service httpd start
    if ! [ -L /var/www ]; then
      rm -rf /var/www
      ln -fs /vagrant /var/www
    fi
- Commands
  - vagrant init - Create Vagrantfile
  - vagrant box add <boxName> - 建立一個 box ( 例如:  “cantos/7”)
  - vagrant up - 啟動 VM (若 box 不存在則重新下載，並執行 provision)
  - vagrant ssh - 進入VM 的命令列 
  - vagrant box remove <boxName>
  - VM 操作
    > vagrant reload --provision
    > vagrant halt
    > vagrant suspend
  - 全部刪除, 只要有 Vagrantfile, 透過 vagrant up 可以重新下載及 provision
    >vagrant destory

