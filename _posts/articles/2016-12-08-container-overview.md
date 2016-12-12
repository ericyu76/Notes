---
layout: post
title: Container/Docker 相關整理
excerpt: "針對 Container/Docker 的概念整理"
categories: articles
tags: [cloud, container, docker]
comments: true
---

# Container 相關整理
## 什麼是 Container

我把它稱做"程式貨櫃",過去一百年貨櫃 (Container)
讓國際物流的效率很有效的提昇了，程式的佈署也有貨櫃的概念讓程式與程式間的整合更為標準化。 Container 由幾個重要的概念組合起來

1. Container 是一種把程式(服務)再封裝的單位, 讓系統間的組合為標準/容易彈性組合擴充
2. Container 與 Container之間的溝通, 透過設定的 ip/port 進行整合
3. 由於作業系統的特性，Container 目前都是使用 Linux 核心
4. 多個 Container 可以在同一個虛擬機(VM)上執行, 每個 Container 邏輯上都是一個獨立的作業系統(只執行服務程式)
5. Container 擁有自己的作業系統設定及網路配置, 透過 image 的方式儲存container 的 snapshot 在 registry
6. Container 比作業系統使用的資源更少，不論是開發測試環境或上線環境，都能更有效率的運用硬體資源

## 什麼是 Docker (與 DockerHub 不同)
1. Docker 是 Container 概念的實作
2. Docker 用來執行/管理 image 及 container，是 OpenSource，免費使用
3. Docker Image 是目前最常見的 Container image 封裝的一種格式, 幾乎只要談 Container 就是會提 Docker
4. Docker Registry 可以自建，用來儲存自製的 image
5. 透過 Dockerfile 的配置 script，可以讓服務的所有管理配置活動容易自動化(包含 os, storage, network 等等)

## 什麼是 DockerHub.com
1. DockerHub，是Docker的主要獲利模式，同時有免費及付費服務。讓大家可以很方便的從公有雲管理自己的 images.
2. 每個人都可以免費註冊帳號, 包含無限制的 Public Image 及 1 個 Private Image 免費使用。
3. 由於免費方案，DockerHub 上提供數量非常廣大的現成 Public Image 供大家免費使用
4. 大多 OpenSource 的軟體，自己也維護 Image在 DockerHub 上

## Container/Docker 的可能使用情境 
### 在實驗階段: 

若是使用 OpenSource 軟體，大多可以在網路上找到可用的 Image, 安裝的過程全部自動化

### 在開發階及測試階段: 

透過 script 的撰寫，可以快速搭建一整個測試環境

### 在上線環境的應用: 

容錯容量的管理可以因應需求自動化擴充及縮小，更有效的運用硬體資源
不被雲端服務的 Vendor 挷定(Iaas)，只要能執行 Docker的 VM，就能很快的把相同的服務建立起來

## 目前使用 Container/Docker 的挑戰
* 使用 Docker 指令操作作業系統及程式配置, 開發人員與 Infra 人員的技術能力需整合. 二種角色都需要熟悉 Docker
