---
layout: post
title: AR Wikitude On Cordova/PhoneGap 試用
excerpt: "試用 wikitude 的紀錄"
categories: articles
tags: [ar, wikitude, cordova, phonegap]
comments: true
date: 2016-08-28T19:10:55+08:00
---

# AR擴增實境應用 on Cordova

Reference:

[](http://www.upsidelearning.com/blog/index.php/2010/04/30/tools-for-developing-augmented-reality-applications/)http://www.upsidelearning.com/blog/index.php/2010/04/30/tools-for-developing-augmented-reality-applications/

**實作及體驗**

Wikitude 的 Phonegap/Cordova [plugin 說明](http://www.wikitude.com/developer/documentation/phonegap)http://www.wikitude.com/developer/documentation/phonegap

1.  安裝 sample project
2.  安裝 plugin 

```bash
        $ cordova plugin add https://github.com/Wikitude/wikitude-cordova-plugin.git
```

3.  取得 License, [](http://www.wikitude.com/developer/licenses)http://www.wikitude.com/developer/licenses，修改至 .js 裡的 key
4.  rebuild iOS 時，要注意不能開啟  bitcode (ios9)
5.  在執行及感受這個 sample app 的過程需要下載一些圖片： 從這裡

[](http://www.wikitude.com/external/doc/documentation/latest/phonegap/images/wikitude_sample_app_target_images.zip)[http://www.wikitude.com/external/doc/documentation/latest/phonegap/images/wikitude_sample_app_target_images.zip](http://www.wikitude.com/external/doc/documentation/latest/phonegap/images/wikitude_sample_app_target_images.zip)

*   Android 可以從這個網址下載 ( [](http://service.testritegroup.com/apps/appbin/ar-sample.apk)[http://service.testritegroup.com/apps/appbin/ar-sample.apk](http://service.testritegroup.com/apps/appbin/ar-sample.apk) )