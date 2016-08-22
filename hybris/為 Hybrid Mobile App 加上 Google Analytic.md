# 為 Hybrid Mobile App 加上 Google Analytic

## 說明

Google 提供的 Analytic 功能比 iTune Connect及Google Play Console 更多功能. 原來 Google 也有提供 Analytic 給 Mobile App. iOS App 也可以使用. 

## Hybrid App

Hybrid App 主要還是以 HTML5 與 JavaScript 為主要的開發技術, 為了維持單一的JavaScript 為程式的主體, 我們必需找一個可以同時支援 android/ios 的 plugin.

於是 Github 上找到了  [danwilson](https://github.com/danwilson)/**[google-analytics-plugin](https://github.com/danwilson/google-analytics-plugin)**

## Step

1.  到 Google Analytic 建立一個行動 APP 並取得追蹤碼 UA-12345678-9
2.  在 Cordova 專案增加 plug-in

*   cordova plugin add [](https://github.com/danwilson/google-analytics-plugin.git)https://github.com/danwilson/google-analytics-plugin.git
*

1.  在  onDeviceReady 加上

*   window.analytics.startTrackerWithId('UA-XXXX-YY')
*

## Reference

*   Cordova Plugin- [](https://github.com/danwilson/google-analytics-plugin)[https://github.com/danwilson/google-analytics-plugin](https://github.com/danwilson/google-analytics-plugin)
*   Google 官方文件

        *   Android - [](https://developers.google.com/analytics/devguides/collection/android/v4/)https://developers.google.com/analytics/devguides/collection/android/v4/
    *   iOS - [](https://developers.google.com/analytics/devguides/collection/ios/v3/)https://developers.google.com/analytics/devguides/collection/ios/v3/

*   Google Analytic官方網站 - [](https://www.google.com/analytics)https://www.google.com/analytics