---
layout: post
title: Docker 實際建置
excerpt: "透過這個實作, 來完成真正的 Docker 環境, 並儘量優化為一個未來建置 Docker 的最佳範例"
categories: articles
tags: [docker, microservices, container]
comments: true
---

# Docker 實際建置


# 啟動 Mongodb Container (Docker)
- 建立 docker container

```bash
    > docker pull mongo/latest
```

- 啟動 container (my-mongo), 並讓 27017 container port 對應到 docker host 的 port
-  -v /vagrant/dockers/mongodb/data:/data/db , 永久保留 mongodb 的db files 到 /vagrant/dockers 目錄裡

```bash
    > docker run -idt --name my-mongo -p 27017:27017 -v /vagrant/dockers/mongodb/data:/data/db mongo:latest mongod
```

- 啟動時若設定了 volumn 的對應， 透過 docker logs 會看到 /data/db 的 permission error 

解決:
```bash
    > chcon -Rt svirt_sandbox_file_t /my/own/datadir
```

# Java Spring boot Application Docker 化
## 說明
- 依SpringBoot 官方說明文件進行建置
  https://spring.io/guides/gs/spring-boot-docker/
- 每次開發完成都透過 mvn 把程式 build 一個 image，後面要佈署的系統只要拉 image 即可
## 作法摘要
  - 透過 spring-boot 把 spring 應用包成一個 jar 檔 (spring-boot 要 1.5.2.RELEASE 可以成功)

  ```bash
    > mvn package
  ```

  - 每次mvn rebuild 都會產生一個 docker image
  - 把 Dockerfile 放在 /src/main/docker，透過 docker file 來自動佈署 rebuild 完成的 Jar 檔

```bash
    FROM frolvlad/alpine-oraclejdk8:slim
    VOLUME /tmp
    ADD itmobileserver-1.0.0-SNAPSHOT.jar app.jar
    RUN sh -c 'touch /app.jar'
    ENV JAVA_OPTS=""
    ENTRYPOINT [ "sh", "-c", "java $JAVA_OPTS -Djava.security.egd=file:/dev/./urandom -jar /app.jar" ]
```

  - 產生 docker image

  ```bash
    > mvn docker:build
    > docker images  // can found your new images
  ```
  - 產生 docker image 後 push 到 registry(沒成功過, 都自己 docker push)
  ```bash
    > mvn docker:build -DpushImage
  ```
  -  執行 docker container (my-java)
  ```bash
    > docker run -p 8080:8080 --name my-java -d  ericyu76/itmobileserver
  ```
# AP Server 與 DB Server 的連結

參考資料: https://g00glen00b.be/docker-spring-boot/

## Docker link
- 透過 docker link 來連結，可以讓 container 拿到對應的網路環境變數
    
```bash
    > docker run -p 8080:8080 --name my-java --link my-mongo -d  ericyu76/itmobileserver
    > docker exec -it my-java env
    LATEST_PORT=tcp://172.17.0.2:27017
    LATEST_PORT_27017_TCP=tcp://172.17.0.2:27017
    LATEST_PORT_27017_TCP_ADDR=172.17.0.2
    LATEST_PORT_27017_TCP_PORT=27017
    LATEST_PORT_27017_TCP_PROTO=tcp
    LATEST_NAME=/my-java/latest
    LATEST_ENV_GOSU_VERSION=1.7
    LATEST_ENV_GPG_KEYS=0C49F3730359A14518585931BC711F9BA15703C6
    LATEST_ENV_MONGO_MAJOR=3.4
    LATEST_ENV_MONGO_VERSION=3.4.4
    LATEST_ENV_MONGO_PACKAGE=mongodb-org
```

Java程式如何使用到 container 的環境變數?
1. Docker RUN  時指定參數
     ```bash
     > java -DMONGO_DB_URL=$MONGODB_PORT_27017_TCP_ADDR:$MONGODB_PORT_27017_TCP_PORT
     ```
2. Java Code/Properties
    ```bash
    # in java code
    System.getProperty("MONGO_DB_URL");
    # in properties
    mongodb.url=${MONGO_DB_URL}
    ```
3. /etc/hosts 會自己增加一條
    ```bash
    172.17.0.2      mongodb 86bc30c8c4ef my-mongo
    ```
4. 使用 docker network
   1. 先建立一個網路 bridge 取名為 testnet
        ```bash
          > docker network create -d bridge --subnet 192.168.88.0/24 testnet
        ```
   2.  啟動 container 時指定網路
        ```bash
        > docker run -d --network testnet --name myapp1 <image>
        > docker run -d --network testnet --name myapp2 <image>
        ```
   3. 或者將網路連結到不同的 container
        ```bash
        > docker network connect testnet myapp1
        > docker network connect testnet myapp2
        ```
使用 docker network 後，在同個網段的 container 透過 docker 內建的 DNS, 可以使用 myapp1 這樣的名稱直接連上(應避免使用 ip)

## 在不同的機器上要怎麼做呢？

