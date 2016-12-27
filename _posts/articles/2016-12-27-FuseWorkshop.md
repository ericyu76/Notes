---
layout: post
title: Fuse Workshop Note
excerpt: "Fuse 的 workshop 紀錄"
categories: articles
tags: [fuse, esb]
comments: true
date: 2016-12-27T12:01:55+08:00
---

# Fuse Workshop

## Preparing

*   Copy Fuse Workshop folder

*   Start JBoss Developer Studio(Can't create Fuse project?)
*   Install New Software - SOA Enterprise

*   Open Shift 無法跑 fuse 因為機器太差

## Apache Camel

**Route Component Type**

同一個元件在不同角色時，URI parameter 的定義不一樣

角色包含

*   producer（箭頭接出）
*   processor (Routing Engine)
*   consumer（箭頭接入）

**Message Exchange**

*   訊息的單位
*   Message 包含 Header, Attachment(Body Content), Error Flag 
*   Exchange 包含From, To, Track ID: what is inside?

**URI Format**

*   component://host?parameter=value&
*

**Transformation**

*   Message Transformation - 資料格式的轉換
*   Data Transformation － 檔案格式的轉換

**Processor**

沒有現成的 Transform 元件，就可以客制, 有二種方式

*   Proessor - 可以處理信封(Exchange), 也可處理 Body(從 Exchange 取到 Message)
*   Bean － 只能處理 body, 但相對單純(可以利用這個方式把 business logic 放進來)

**Camel 注意事項:**

*   請使用 Blueprint, 不要再用 Spring DSL 及 Java DSL (未來 Comunity 版本不再支援)

**Enterprise Integration Pattens**

Asynchronized

Message Channel

WireTap - 老鼠尾

Camel 支援二種Transaction

jdbc Transaction/???

## Maven

Jar 檔的管理，透過 pom.xml 抓取

**Lab2**

jaxb.index(為了取代 jaxb 的行為)

**Lab3**

從 canvas 上面 add 第二條 route

從Outline 上面選二個 route

Canvas 上面線斷掉的話後面的東西會不見

Spilt 有bug要自己貼

**Lab4 使用 ActiveMQ**

**Beans Registry**

1.  Create Bean POJO
2.  Registed <bean> on camel route
3.  Referene bean in ben <route ref="ddd">

Bean Registry

*   可以透過 Fuse Integration Perspective 查看 route 的執行情況

![](https://hackpad-attachments.s3.amazonaws.com/hackpad.com_4V13OVmhmvT_p.236988_1427875233218_螢幕快照 2015-04-01 下午3.59.40.png)

## OSGi Container (Fuse Fabric)

Module 名字加上 version# 來區分相同的 jar

*   Java 會發生 classpath conflict 的問題，OSGi 不會

JVM 把所有的 class 都放在 memory. 但OSGi 不會互相看到.

Module 之間要設定 Export/Import 才能看到 (Depency 要另外設定)

Bundle 是要放進 OSGi 的單元 (.jar)

OSGi Service 指的是 Bundle 提供的服務(非指 WebServices)

包 bundle 時並不會幫我們把 pom.xml 裡的jar load 進來, 所以要自己設定，讓 karaf

*   bundle jar deploy 到 karaf

**Howtio**

OSGi －Runtime/Bundle

Wiki －－ 看GIT

**Deploy application using Studio Fuse Integration**

用拉的...

![](https://hackpad-attachments.s3.amazonaws.com/hackpad.com_4V13OVmhmvT_p.236988_1427877281686_螢幕快照 2015-04-01 下午4.34.12.png)

在 Windows 環境下，使用者需要是 Administrator 才能看到 process

## Fuse Fabric

正常 Production 情況下會需要多個 OSGi Container 進行 cluster

**啟動 Fabric**

*   在 Fuse Console 下執行   **fabric:create --wait-for-provisioning  重新 login 後，會看到 Howtio 多了 Fabric 的功能**

未來要進入到 container 查 camel 的狀態，就要透過 Profile 裡的 container 查狀態

**Term:**

Fabric Server -  佈署被管理的元件, 有 Git

Ensemble － 把 Fabric Server 連起來, 要至少三台Fabric Server

Container 

RDB-Registry Database, 

*   Runtime Registry

*   mvn:[repositoryUrl!]groupId/artifactId/[Version]
*   file:....foo-1.0.0.jar
*

Maven Proxy

*   Local Repo
*   Remote Repo

## Deply Bundle to Fabric

**一般：**

*   create profile

*   Create Container

*   Deploy profie to Container

**快速建立 Profile (透過 pom.xml裡增加設定Profile)：**

*   pom裡加一個 fabric8 plugin
*   增加 fabric8 properties (把需要的 feature, bundle 都設定好)
*   mvn goal** fabric8:deply**
*   到 Wiki 的 profile 確認, 並 create **New Container**

## Reference

Lab file: Fuseon-Lab.pdf

Blog - [](http://wei-meilin.blogspot.tw)http://wei-meilin.blogspot.tw

Slides - [](http://slides.com/weimeilin)http://slides.com/weimeilin

Trend: Micro Services
