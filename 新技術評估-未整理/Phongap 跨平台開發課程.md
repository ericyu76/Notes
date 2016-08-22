# Phongap 跨平台開發課程

## 跨平台架構開發的 Overview

*   各個作業系統的特性 (android, iOS xcode)
*   xcode/android 在開發過程的注意事項

        *   iOS 需要 developer 才能在手機上跑，需要 osx 的硬體 ＄
    *   android 比較不需要高的成本
    *   android/ios Emulator 的debug mode

                *   Android/iOS 看 layout
        *   Chrome 進行 java script 的除錯

*   跨平台技術的挑戰-就是很多技術的匯整

        *   CSS3/HTML5

*   WebView的概念-不需要 web server 的技術(html on local)
*   Group IT 在Hybrid 的環境的想法

## 開發環境的準備

**Android 的開發環境**

*   下載 Eclipse Juno 以上
*   安裝 Eclipse Plugin (Developer Tools)

        *   Eclipse -> Window -> Install New Software
    *   Work with "[](https://dl-ssl.google.com/android/eclipse/)[https://dl-ssl.google.com/android/eclipse/](https://dl-ssl.google.com/android/eclipse/)"

*   下載 SDK 並安裝, 若要安裝 Android 的 SDK 需要大約六個小時，除非有特定的平台。
*   需要準備手機，決定開發環境
*   java asm.jar

*

**JQuery Mobile**

*   需要 JQuery 及 jQuery Mobile 的 js
*   利用手機在 JQuery Mobile 上面看 demo
*   [](http://goo.gl/z3imAB)http://goo.gl/z3imAB 下載程式
*   Aptana - 免費的 html 編輯器
*   建議使用 Chrome
*   準備 localhost 的 WebServer (Cordova 有附)

**PhoneGap/Cordova**

*   要先安裝 node.js/npm
*   > npm install cordova

## 課程硬體需求

**共用設備：**

*   Wifi AP
*   Web Server

**個人設備：**
<undefined><li>**硬體**</li></li>
<li>Notebook</li>

*   能夠有一個 web server
*   Android 模擬器效能差，最好有一台 Android
*   Macbook 使用 iOS Emulator
</li>
<li>Android 手機</li>
<li>**軟體**</li></li>
<li>Eclipse/ Android SDK</li></li>
<li>對應自己手機的 SDK版本</li></li>
<li>Node.js</li></li>
<li>npm -install cordova</li></undefined>

## jQueryMobile

使用 jQueryMobile 最基本的需求

**   <!doctype html>
*   <html>
*   <head>
*   <meta charset="UTF-8">
*   <title>Pages</title>
*   <meta name="viewport" content="width=device-width, initial-scale=1"> 
*   <link rel="stylesheet" href="[](http://code.jquery.com/mobile/1.4.4/jquery.mobile-1.4.4.min.css)http://code.jquery.com/mobile/1.4.4/jquery.mobile-1.4.4.min.css" />
*   <script src="[](http://code.jquery.com/jquery-1.11.1.min.js)http://code.jquery.com/jquery-1.11.1.min.js"></script>
*   <script src="[](http://code.jquery.com/mobile/1.4.4/jquery.mobile-1.4.4.min.js)http://code.jquery.com/mobile/1.4.4/jquery.mobile-1.4.4.min.js"></script>
*   </head>
*   <body>
*           <div data-role="page">
*           <div data-role="header">
*                   <h1>JQuery Mobile</h1>
*           </div>
*           <div data-role="content">
*                   <h1>Content</h1>
*                   <p>Hello World!</p>
*                   <a href="#">Custom Download</a>
*           </div>
*           <div data-role="header">
*                   <h1>JQuery Mobile</h1>
*           </div>
*           </div>
*   </body>
*   </html>

## 目標：開發一個自己的 APP在自己的手機上執行

For Android Only

Question:

1.  Android 如何看到 Java Script 的 console.log?
2.  Android Screen Monitor 如何做？

## 執行Phonegap 範例程式

下載 [](http://goo.gl/IPbrNa)[http://goo.gl/IPbrNa](http://goo.gl/IPbrNa)  --Phonegap Template

1.  建立 Cordova 專案

*   > cordova create [目錄名] [App Bundle 名] [App名稱]

1.  複製上課的Lab 程式至 www 目錄

*   > cp -R ~/PhoneGap_Template/Notification/* .

1.  新增手機的平台, platforms 可以是 : ios, android,....

*   > cordova platform add [platforms]

1.  新增該 Lab 的 Plugin Name, eg: org.apache.cordova.**device-motion**

*   > cordova plugin add [plugin name]

*   cordova prepare [platforms]

1.  在手機上執行程式: 調整Android 專案的 SDK 符合自己的手機

**Lab 0: HelloWorld**

*   Development Lifecycle

**Lab 1:  Notification Lab App**

*   org.apache.cordova.**dialogs**
*   org.apache.cordova.**device**
*   org.apache.cordova.**vibration**

**Lab 2 Event Lab App**

*   org.apache.cordova.**battery-status**
*   org.apache.cordova.**network-information**

**Lab 3 Geolocation**

*   org.apache.cordova.**geolocation**

**Lab 4 Compass**

*   org.apache.cordova.**device-orientation**

**Lab 5 Accelerometer**

*   org.apache.cordova.**device-motion**

**Lab 6 Camera**

*   org.apache.cordova.**device-motion**

**Lab 7 Capture**

*   org.apache.cordova.**file**
*   org.apache.cordova.**media-capture**

**Lab 8 Media**

*   org.apache.cordova.**device**
*   org.apache.cordova.**file**
*   org.apache.cordova.**media**

**Lab 9 WebService**

**Lab 10 Storage (DB)**

## Android Java Script Debug

因為 JavaScript 使用 console.log() 進行 debug, 要如何看到 log?

1.  先建立好 Andorid 的開發環境

        1.  安裝 Android USB Driver
    2.  安裝 Eclipse
    3.  下載 Android SDK，執行 Android , 啟動 android sdk manager, 選擇與自己手機版本相符的 SDK
    4.  手機要打開開發人員模式
    5.  安裝 Eclipse Plugin

2.  建立好 Phonegap Android 專案
3.  Eclipse > Windows > Show View > 新增 Android 的 LogCat
4.  設定 LogCat 的filter 來看到自己想看的訊息