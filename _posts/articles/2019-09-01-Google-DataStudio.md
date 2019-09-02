---
layout: post
title: Google Data Studio 及 Google BigQuery
excerpt: "心得及重點摘要"
categories: articles
tags: [Google, Firebase Analytics, Data Studio, BigQuery]
comments: true
---

# Google Data Studio 及 Google BigQuery

## Report Like a Boss Using Google Data Studio 
[影片連結](https://www.youtube.com/watch?v=C1w-yuTDUeM)

### 重點摘要:
1. 使用 Google Data Studio 可以直接利用內建的 connectior 來連結各種 Data Source. Data Source 目前主要以 Google 上的服務為主. 這個範例用的是 Google Analytics, 試了一下Firebase Analytics 的 Event 也都能夠作為 Data Source.
2. Data Studio 用在產生即時的報表，而不用再每個晚上跑日報或週報，利用篩選器的功能，也能很容易讓老闆在各種不同維度的資料自由決定。
3. 說明建立報表日期篩選器，圖表選項篩選器
4. 圖表可以建立分享連結，也能讓其他人協作編輯
5. Data Studio Gallery 提供很多已經完成的報表讓大家參考學習

### 個人心得
Data Studio 是一個簡單的工具，幾乎不太需要太多專業的知識。自己試著從 Firebase Analytics 裡的 BigQuery Event 去拉資料，發現的確很容易製作圖表。但因為 Firebase Event 的資料結構過於複雜，尤其加上還有自訂 Event Param, 所以可能還需要針對 BigQuery 資料做一些整理, 否則製作 Data Studio 的報表複雜，而且資料速度有點慢。


## BigQuery for Analytics (Firebase Dev Summit 2017)
[影片連結](https://www.youtube.com/watch?v=pxNrkjBeHpw&t=906s)

重點摘要:
1. 這個 Session 利用 BigQuery 存取 Firebase Analytics 上的資料做為範例
2. BigQuery 上的 Table 資料結構並不是 2 維的，裡面有樹狀的結構

### UNNEST
利用 UNNEST 指令可以先把 Array 的資料 de-normalized 為多筆，然後再透過 UNNEST 的欄位進行篩選及檢視。

例子1: 把 Event_params 展開再進行篩選
```sql
SELECT eventkey
FROM `testrite-loyaltyapp.analytics_179803436.events_20190831`
CROSS JOIN UNNEST (event_params) AS eventkey
WHERE event_name = 'add_to_cart'
AND eventkey.key = 'item_name'
LIMIT 20
```
例子2: user properties 再展開
```sql
SELECT userprop.value.string_value as memberId, eventkey.value.string_value as itemname
FROM `testrite-loyaltyapp.analytics_179803436.events_20190830`,
UNNEST (event_params) AS eventkey,
UNNEST (user_properties) AS userprop
WHERE event_name = 'add_to_cart' AND userprop.key = 'user_id'
AND eventkey.key = 'item_name'
LIMIT 20
```
### SubQuery
就像一般的 DB 能做的，BigQuery 也能 SubQuery, 用法都一樣。這邊用了 CORR 這個函數來計算剛剛例子裡的相關係數。

### SELECT FROM UNNES
把 Table 直式的資料轉成橫式。
```sql
SELECT 
(select value.string_value from unnest (event_params) where key ='item_id') as sku,
(select value.string_value from unnest (event_params) where key ='item_name') as itemName,
(select value.double_value from unnest (event_params) where key ='quantity') as quantity,
(select value.double_value from unnest (event_params) where key ='price') as price
FROM `testrite-loyaltyapp.analytics_179803436.events_20190830`,
UNNEST (event_params) AS eventkey
WHERE event_name = 'add_to_cart'
LIMIT 20
```

