---
layout: post
title: 微服務讀書筆記
excerpt: "Oreilly 建構微服務一書整理的讀書筆記"
categories: articles
tags: [microservices, docker, container, elk]
comments: true
---

# 建構微服務

# 架構師的責任
  - 與非技術人員 align 公司願景及策略
  - 與交付團隊接觸
  - 理解現實限制，結合務實作法
  - 建立標準
    - 監控 metrics, graphite
    - 介面
    - 安全
  - 中央治理 goverance
    - 溝通技術願景
    - 參與交付團隊建模
    - 儘可能的說清楚論述，以小組意見為主，小組是最終負責的人
  
![](https://d2mxuefqeaa7sj.cloudfront.net/s_91654CA379A5A250EF14AC1124F5D1101958B98C738344C1B7BA69B095F0328A_1496113359907_file.jpeg)

# 微服務的設計 - 拆分單體系統

在進行單體系統拆解前要先

1. 確實瞭解系統在做什麼
2. 辨識邊界服務(界面)
3. 從小的部分慢慢調整
## 服務候選人
- 上下文邊界「庫存品項」- 為最好的服務候選人
![](https://d2mxuefqeaa7sj.cloudfront.net/s_91654CA379A5A250EF14AC1124F5D1101958B98C738344C1B7BA69B095F0328A_1496115749386_file.jpeg)

- 不是資料分享的角度(貧血的 crud)，而是提供什麼功能
- 第二選項-技術邊界
  - 地理位置
  - 技術？
![](https://d2mxuefqeaa7sj.cloudfront.net/s_91654CA379A5A250EF14AC1124F5D1101958B98C738344C1B7BA69B095F0328A_1496116224618_file.jpeg)

## 服務與組織
  - Conway 定律 - 組織影響系統架構
  - 讓服務可由單一組織負全責，有高度的決策權力，才有朝向敏捷發展的動機
  - 讓組織設計與系統服務設計相同


![Squad 是系統維運的組織, LOB 是 Line of Business](https://d2mxuefqeaa7sj.cloudfront.net/s_91654CA379A5A250EF14AC1124F5D1101958B98C738344C1B7BA69B095F0328A_1498275201286_file.jpeg)

# 微服務的技術及佈署
## VM Image
![](https://d2mxuefqeaa7sj.cloudfront.net/s_91654CA379A5A250EF14AC1124F5D1101958B98C738344C1B7BA69B095F0328A_1498277184254_file.jpeg)

## Container
  比 VM 更輕一級的虛擬化
![](https://d2mxuefqeaa7sj.cloudfront.net/s_91654CA379A5A250EF14AC1124F5D1101958B98C738344C1B7BA69B095F0328A_1498277290325_file.jpeg)

  Docker
  LXC
  CloudFoundary
## PaaS 服務
  AWS - EC2, ECS
  Her
## 整合
  REST
  SOAP
## 斷路器

大規模的服務需要設計斷路器，避免問題蔓延

![](https://d2mxuefqeaa7sj.cloudfront.net/s_91654CA379A5A250EF14AC1124F5D1101958B98C738344C1B7BA69B095F0328A_1498275525694_file.jpeg)



# 微服務的安全

HTTPS Authentication - 最簡單的認證且技術上充分支援, 必須以 https 為前提
SSO Gateway 集中管理 

  - SAML
  - OAuth2 - OpenID Connect
![](https://d2mxuefqeaa7sj.cloudfront.net/s_91654CA379A5A250EF14AC1124F5D1101958B98C738344C1B7BA69B095F0328A_1498272868925_file.jpeg)

![Api Gateway及網頁存取的整體架構](https://d2mxuefqeaa7sj.cloudfront.net/s_91654CA379A5A250EF14AC1124F5D1101958B98C738344C1B7BA69B095F0328A_1498273404430_file.jpeg)

# 微服務的日誌及監控服務

要先考慮觀眾的需求再進行設計

## ELK 工具
1. Logstash - 解析及捕抓日誌
2. ElasticSearch - 全文檢索
3. Kibana 查看日誌
![](https://d2mxuefqeaa7sj.cloudfront.net/s_91654CA379A5A250EF14AC1124F5D1101958B98C738344C1B7BA69B095F0328A_1498276635077_file.jpeg)

## 監控工具
  Nagios (CPU, MEM)
  Metrics(JVM)
  Application Layer Statics
## 相關性 ID
  要設計一個 co-relation ID 可以辨識在不同服務裡同一筆的交易



