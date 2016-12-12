---
layout: post
title: 利用 jHipster建立Java Web Application系統
categories: articles
tags: [java, spring, jhipster]
comments: true
date: 2015-08-30T18:00:35+08:00
---

## 什麼是 jHipster?

jHispter 是一個自動化的 script , 讓開發者快速建立Java Web Application 的先進 Framework 集合。這裡有 Framework 集合的[官方說明](http://jhipster.github.io/presentation/)

看完Framework說明後，假若這些 framework 也符合開發者的需求，就可以再看一下 [jHispter Video (約20分鐘)](https://jhipster.github.io/video_tutorial.html)

20分鐘影片內容包含:

*   建立一個新的系統 bookstore
*   查看資料
*   API管理及測試
*   Development 環境與 Production 環境的比較
*   系統監控
*   佈署到 cloud 服務自動化

相信大約三十分鐘的時間，大概就知道 jhipster帶來的好處了。

**幾個比較重要的 Framework**

*   AngularJS as FrontEnd
    *   html5/css3
* Spring 4 MVC
* Spring 4 Security
* Spring 4 JPA


**優點:**

1.  容易佈署到 Cloud 服務
2.  適合已經熟悉 Java/spring framework 的使用者
3.  提供完整的後台 (Entity管理, API 管理)

**測試重點：**

*   要建立一個包含了 Spring Security, Oauth2 的 Java Backend 能有多快
*   Persistent Framework 的支援程度? 企業環境使用的是 Oracle

## 開始試用

**安裝(前面要安裝 node.js 就省略)**


```bash
   > npm -g install yo
   > npm -g install generator-jhipster
```

**基礎設定**

```bash
   > mkdir application-folder
   > cd application-folder
   >  yo jhispter
```

14 個基礎設定，我選擇了: Java 7, MySQL, Hibernate-2nd Level enable

**DB 設定/調整**

*   Production: src/main/resources/config/application-prod.yml
*   Development: src/main/resources/config/application-prod.yml

*    如何設定為 Oracle?

**啟動 Server，檢視結果**

``` bash
> export JAVA_HOME=$(/usr/libexec/java_home)
> mvn spring-boot:run
```

打開 browser 連到 localhost:8080 可看到建立出來的程式結果，也可以利用 grunt serve 的 live reload 更即時的看到 UI 設計的變化，這個在 RWD 的 UI 設計時是相當方便的.

**新增 Entity (DataModel 及 Relation 要先想好，Generator不容易回頭)**

``` bash
> yo jhipster:entity [entityName]
> mvn test
```

萬一做錯，不容易回頭，利用 git/svn 版控工具進行回復是一個最快的方式，否則就有很多檔案要刪。參考連結裡有一個網址說明如何手動回復。

**新增 Service(應用在單一 Entity 以外的業務邏輯)**

*   新增 service，並在新增的 service 裡能使用  mybatis DAO

```bash
> yo jhipster:service orderManager
```

產生了 Services 之後，加上 @RoleAllowed @Timed @RestController @RequestMapping...等等即可，未測試完成.

**Security 設定**

*   如何保護Enitity/Service及設定權限？

```bash
$ curl [](http://localhost:8080/api/login?username=admin\)http://localhost:8080/api/login?username=admin\
&password=admin\
&grant_type=\
&scope=read%20write\
&client_secret=mySecretOAuthSecret&\
client_id=myApp
```

**Java IDE 開發環境**

因為熟悉使用 Eclipse, 使用 Eclipse 的 Import from Maven Project 把 application-folder 的目錄整個匯入(不知道怎麼啟動 spring-boot)

**已知問題:**

**潛在可能的問題**

*   需要完整瞭解整個 full stack 不容易
*   jHispter 整個專案會不會消失, 消失的話，整個專案的維護是否會困難？

**總結**

可以把 jHispter 產生出來的 Application 當作 RESTful 的 server

*   已經產生基本的 spring security/oauth2 implement
*   對於hibernate 不是很熟, 要用 hibernate 去製作複雜的 db 服務不容易，但簡單的基本資料查詢沒有什麼問題
*   要進一步瞭瞭 Service generator 的能力到什麼地步

## 參考資料

*   jHispter 全部的 Framework 說明投影片,用鍵盤的上下左右鍵控制 [](http://jhipster.github.io/presentation/)[http://jhipster.github.io/presentation/](http://jhipster.github.io/presentation/)
*   jHispter Video: [](https://jhipster.github.io/video_tutorial.html)https://jhipster.github.io/video_tutorial.html
*   Entity 做錯回復的說明: [](http://stackoverflow.com/questions/28226336/how-to-delete-an-entity-after-creating-it-using-jhipster)http://stackoverflow.com/questions/28226336/how-to-delete-an-entity-after-creating-it-using-jhipster