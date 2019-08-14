---
layout: post
title: 剖析 Google 分析的現況
excerpt: "此篇是參考原文文章的個人重點摘要"
categories: articles
tags: [Google, Firebase Analytics, FA, GA]
comments: true
---
# 剖析 Google 分析的現況

此篇是參考原文文章的個人重點摘要 https://proandroiddev.com/anatomy-of-analytics-from-google-e107fff107ab

## Google Analytics (GA) 與 Google Analytics for Firebase (即為 Firebase Analytics -FA)
   * GA 與 FA 是二種完全不同的分析方式:
      * GA Event 是在 Event hierarchical 結構下的一個值
      * FA 是一個 Event 裡包含了多個值
   * GA 工具目前還不會不會消失，使用GA的人晚上可以安心的睡，但世界一直在變...
   * 二個工具之很很難相容

## GA vs FA Event, 資料結構完全不同
* GA 的 Event (category → action → label → value)
```java
// roundsSurvived
mTracker = googleAnalytics.newTracker(R.xml.tracker_global_config);
HitBuilders.EventBuilder builder = new HitBuilders.EventBuilder()
        .setCategory("gameOver")
        .setAction("roundsSurvived")
        .setLabel("")
        .setValue(gameStats.getRoundsSurvived());
mTracker.send(builder.build());
```

* FA 的 Event
```java
final Bundle params = new Bundle();
params.putLong("totalScore", gameStats.getTotalScore());
params.putLong("enemiesBeaten", gameStats.getEnemiesBeaten());
params.putLong("roundsSurvived", gameStats.getRoundSurvived());
mFirebaseAnalytics.logEvent("game_over", params);
```

## FA 管理者介面與 GA的差異
   1. FA 的 Dashboard 是從[內建的 Event](https://support.google.com/firebase/answer/6317485) 呈現的
   2. FA 的 Event
       * FA 支援最多 500 種 Event (內建的 Event 也算在內), event 的數量無限制
       * 每一個 Event 可以有 25 個 parameter
       * 只有內建的 Event 會出現，自定的 Event 都完全不會出現
       * Console Event 報表裡, 找不到自定 Parameter 資料... 
       * Event 報表只有 event 的數量及 event 的 user count
   3. GA 的資料有 Sampling, 但 FA 沒有，全數都紀錄, 就像 GA 360, 但不需要付那麼多費用
   4. I/O 2017 之後，FA 可以自定 Event/Parameter 報表，它資料料是從設定後開始累積，而不是既有資料呈現
   5. FA 若想要進一步分析資料，就要靠 BigQuery

## BigQuery
   1. FA 昇級為 Premium 帳號可以使用 BigQuery
   2. BigQuery 不像 FA/GA 很快就能學會操作, 需要較多時間學習，有熟悉這技術的人可以幫公司或組織找到問題的答案
   3. 參考資料
      * [Google 介紹影片](https://www.youtube.com/watch?v=Ki_F6VCOtXU)
      * [Using BigQuery and Firebase Analytics to understand your mobile app](https://cloud.google.com/blog/products/gcp/using-bigquery-and-firebase-analytics-to-understand-your-mobile-app)
      * [官方文件](https://cloud.google.com/bigquery/docs/)
      * [整本書](https://www.wiley.com/en-gb/Google+BigQuery+Analytics-p-9781118824825)
   4. [DataStudio](https://datastudio.google.com/navigation/reporting) 是 BigQuery 分析的很好視覺工具

## FA User Properties
   * User Properties 也稱做 Sticky Params 因為它們會添加到每個 Event, 即使用重新啟動 application, 都會持續存在。
   * 首先必須配置該 properties 在 console 裡, [預設的 user properties](https://support.google.com/firebase/answer/6317486?hl=en&ref_topic=6317484) 不需額外再配置(例如: age, device, gender...)
   * 除了預設的 user properties 之外，可以再增加最多 25 個 properties.
   * 有了 User Properteis 之後，可以在 Event 報表裡依照 user properties 進行 Filter 的配置
   * FA 的 setUserProperties() =  GA setCustomDimension(…)and setCustomMetric(…), 唯一不同的是，FA 不需要為每一個 event 進行配置
   * 



   * 愛家卡為什麼沒有 User Id User ID 在什麼地方?


## 如何同時使用二種 Analytics
文中是直接使用 [參考文章](https://firebase.googleblog.com/2017/02/how-do-i-add-firebase-analytics-to-app.html?m=1).
   1. 直接安裝二種 Analytics 的工具
   2. 使用 GTM 進行整合, 透過 FA 的 Event 直接在 Tag Manager 進行配置, 轉送到其他的 analytics 工具裡. [Google這邊有篇文章](https://developers.google.com/tag-manager/android/v5/)說明這個細節。
   3. 使用 BigQuery。但 GA 要把資料匯入 BigQuery 需要GA 360 版本。


## FA 配置
皆為技術性App工作細節
   1. 程式 dev/sit/prod 的配置方式
   2. 程式 debug 的 suffix packageId 配置方式
   3. FA 的開啟及關閉 function, setAnalyticsCollectionEnabled(true), 用在我們得到使用者允許才蒐集的情況


## FA 的 Session
   * FA 的 Session 指的是一段時間，App 跑在前景在 MinimumSessionDuration 以上就算啟動一個 session, 若 App 被系統暫停或停止，但在 SessionTimeoutDuration又啟動，那仍然在同一個 Session, 否則啟動另一個 Session
   * FA Api: 
      * setMinimumSessionDuration (long milliseconds); // default 10 sec
      * setSessionTimeoutDuration (long milliseconds); // default 30 min
   
## FA 的其他功能
   * Audience 受眾: 可以配置行為條件(Event/User Properteis...)建立分群
   * Funnels

## 結論
### FA 優點
   1. 目前 Google 很專注積極開發及優化的專案
   2. FA + BigQuery, 尤其是團隊內有很利害的 BigQuery 專案的時候
   3. 極簡。 Console 裡的資訊全是 Event
   4. 與其他 firebase 專案整合。尤其已經使用 firebase 的其他服務者。

### FA 缺點
   1. Console 功能仍不足
   2. Console 資訊分散不易聚焦 




