---
layout: post
title: Docker 學習筆記
excerpt: "整理試用 Docker 的紀錄"
categories: articles
tags: [docker, technical]
comments: true
date: 2016-10-15T12:39:55+08:00
---
# Docker 學習筆記

希望透過 docker 的技術能夠將開發環境的 template 建立起來，未來若要在本地或雲端建置系統，就可以非常快速的把環境建立起來。

## 安裝 Host Server

Host Server 是用來執行 Docker 的 Server, 需要從 OS 層次開始安裝。這邊使用 centos7 的 x86-64 的最小安裝 iso 檔案進行安裝。

*  選擇 CentOS 7 的原因
> * 接近 Redhat Enterprise OS

*  Docker 官方建議採用 kernel 3.1 以上

## Install Docker CentOS 7 為例

*  將  yum db update 到最新

> ```sh
> sudo yum update
```

*  設定 docker Repository, 可以使用 yum 安裝 docker

使用 root 新增一個文字檔 "**/etc/yum.repos.d/docker.repo**", 內容為

> ```ini
   [dockerrepo]
   name=Docker Repository
   baseurl=[](https://yum.dockerproject.org/repo/main/centos/$releasever/)https://yum.dockerproject.org/repo/main/centos/$releasever/
   enabled=1
   gpgcheck=1
   gpgkey=[](https://yum.dockerproject.org/gpg)https://yum.dockerproject.org/gpg
```

* 安裝 docker

>```sh
     > sudo yum install docker-engine
```

* 啟動 Docker, 設定未來開機後都自己啟動 docker

> ```sh
     > sudo service docker start
     > sudo chkconfig docker on
```

* 測試 docker

> ```sh
    > docker run hello-world
```

* 因為用 root 來執行 docker 有危險，所以要另外建立一個 Group 叫 docker 把 user "ericyu" 加進去，之後 ericyu 執行 docker 就不需要 root/sudo.

> ```sh
	> sudo usermod -aG docker ericyu
```

## Docker 指令

1.  docker **search** - 搜尋網路上的 docker images
2.  docker **pull** - 從網路上下載 docker images
3.  docker **rm** - 移除本地的 docker images
4.  docker **images** - 列出已經 pull 回來的 images
5.  docker **run** - 執行 docker images

   **-i** interactive

   **-t** terminal

   **-d** daemon (變為 daemon, 背景執行)

   **-P** AutoPort Mapping  (把 container 的 port 與 host 的 port mapping 一起)

1.  docker **exec** -i -t [container] **/bin/bash**  (進行已經運行的 container shell)
2.  docker **logs** -f 可以打出 container 的 stdout 訊息

## Docker image 的操作

從 docker hub或 registry 下載下來的image, 我們會會進行配置或調整。當我們進行完這些調整想要把這些設定儲存下來的話，就需要瞭解對 image 的操作。 images 的管理有二種做法搭配:

1.  把所有的的變更儲存在新的 image 並進行儲存(commit/push)，供之後取用。
2.  透過 Dockerfile 來把 pull 下來的 image 進行特別的配置。

**操作:**

```sh
  > docker run -i -t [dockerImage] /bin/bash
  root@xxxx> do some changes
```

*  透過 Dockerfile 進行額的配置，透過 Dockerfile 的 script 建立

*   儲存變更 image

```sh
   >docker commit -a "Eric Yu" -m "some change messsage"
```

*  上傳 image 到 Docker Hub

```sh
      >docker tag (給目前的 image 給版號)
      >docker push ericyu/centos:v2
```

## Docker Network  操作

之前在建立 Docker 時，就可以使用網路存取 docker 裡的服務。因為 docker defualt 是使用 bridge 為預設的網路設定型態，然後透過 -P 來自動對應 port。若我們有自定義的需求時就要自己建立自己的網路配置。

**操作:**

*  瞭解目前的網路

```sh
   > docker network ls
```

*  建立網路自己的網路 (叫 my-bridge-network)

```sh
   > docker network create -d bridge my-bridge-network
```

*  啟動 Server 將 Server 加入自己的網路

```sh
   > docker run -d --net=my-bridge-network --name db training/postgres
```

## Docker Storage

Storage 是用來把資料儲存下來, 或者有分享的需求時使用。可以透過 docker inspect container 來看mount(掛載)的資訊。Mount volume 有二種方式:

* 直接掛載本機目錄
* 掛載 docker datastore

```sh
  > docker run -i -t --name web -v /src/webapp:/opt/webapp ericyu76/httpd /bin/bash
```

```sh
  > docker run -i -t -v /opt --name datastore ericyu76/http /bin/bash
```

```sh
  > docker run -i -t --volumes-from datastore --name httpd ericyu76/httpd /bin/bash
```