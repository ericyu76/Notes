---
layout: post
title: Cloud Foundry
excerpt: "Cloud Foundry 的初步瞭解及認識"
categories: articles
tags: [cloudfoundry, paas, container]
comments: true
date: 2015-10-01T21:01:55+08:00
---
# Cloud Foundry

## 簡介

*   是一個 Open Source Project 給想要使用PaaS雲端服務的使用者
*   Cloud Foundry 上面佈署的程式可以選擇佈署在 Amazon, Hekero, Pivot 或其他. 當然也包括企業內部的雲端服務
*   因為雲端服務有容易延展，易於管理的特性，因此開發設計時需符合 12 Factor 的設計準則
*   透過 Cloud Foundry CLI 進行程式的佈署，使用 manifest.yml 來描述服務間的關係，也利用 manifest.yml 來進行自動化佈署
*   背後架構有 Container 的概念，未來會支援 Docker

## 12 Factor 重點整理

1.  版控一致性，一個 command就要能 rebuild出完整的服務
2.  程式的元件 depency 要明確宣告
3.  環境配置要集中，並且最小化到少數的 file
4.  外部服務都要使用 URI, 不能假設服務都在同一台機器(包含 File System)
5.  避免 Session Replication, 應用要以 stateless 設計 (??)

## Reference

*   PaaS 12 Factor－[](http://12factor.net)http://12factor.net
*   Pivotal Cloud Foundry Service - [](http://pivotal.io/platform-as-a-service/pivotal-cloud-foundry)http://pivotal.io/platform-as-a-service/pivotal-cloud-foundry