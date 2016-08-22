# Android 開發

## 開發環境配置

*   下載 JDK, 4.4.2 開始使用 jdk7 開發

        *   JAVA_HOME=jdk7

*   下載 Android Development Tools, (ADT) ANDROID=adt

        *   ADT 是 Plugin for Eclipse, 目前內含一個 Eclipse (ADT Bundle)
    *   PATH=jdk7/bin;android/tools

*   Android Debug Bridge(ADB) 可以用來偵錯 exe, process
*   Android Virtual Device(AVD), 虛擬裝置

**SDK Manager 及 adt/sdk 底下的目錄**

*   tools - 版本無關的工具

        *   sqlite3
    *   adb

*   platform-tools - 與版本有關的 adb
*   build-tools - Eclipse 建置
*   source - Android SDK 原始碼
*   platform - 編譯好的 SDK

APK - zip 目錄結構

*   AndroidManifest.xml

**建立 Android 專案**

*   Appcompat_v7 - 用來向下相容的 lib，可以從 Library 裡把該 library 移除並自行解決向下相容的問題

**Change app package**

*   Refactoring java src package name
*   change AndroidManifest.xml

**ADB 命令列操作**

*   列出連線的 devices
*   > adb devices
*   刪除 App
*   > adb uninstall [com.trg.mobile.firstapp]
*   與 Eclpse 獨立的 log, 用這個方法可以判斷是否 Eclipse 的 Logcat 問題
*   >adb logcat

**ASOP (模擬器上的 dev tools)**

*   Package Browser - 可以瀏覧 App 的 package name, 利用 ADB 可以進行 uninstall

**Android Manifest (Editor on Eclipse)**

*   Manifest Tab

**Android Run Configuration**

**Eclipse Hotkeys**

*   Content Assist - alt + /
*   Block Move - alt + 上/下
*   Auto Format - ctrl + shift + F

**Eclipse DDMS Perspective**

*   File Explorer
*   LogCat

**Eclipse Navigate**

*   go to resource - abc_* (abc means Android Backward Compaitable)

**Project Explorer - Working Set**

## 開始開發
<ul><li>建立XML(View)

*   檔名的選擇規則

1.  全小寫，可加數字
2.  數字不可在最前面
3.  不要加符號

*   拉畫面時，虛線是預期的位置，實線是父類別的位置。
</ol>

## Android JNI

1.  下載 [](http://developer.android.com/tools/sdk/ndk/index.html)http://developer.android.com/tools/sdk/ndk/index.html[,](http://developer.android.com/tools/sdk/ndk/index.html安裝) 並安裝 JNI - /Development/android-ndk-r10c

*   static { System.loadLibrary("demolib");}
*   public native String getContent();

1.  Copy make file form HelloJNI

        1.  Samples/HelloJNI/jni 目錄有Android.mk 檔
    2.  調整 Android.mk

                1.  LOCAL_MODULE: demolib
        2.  com_uuu

*   下指令, 產生 header file (.h)
*   > **javah** -d ../jni -classpath ./classes:$ANDROID_HOME/platforms/android-19/android.jar com.example.myfirstjni.MainActivity

4. 

## Animation Lab

OSX: Problem to add an image resource?

## Tab Lab

1.  import Tab.zip into Eclipse
2.  Change the "run as" to run com.patristar.TabInit Activity
3.  Download "Action Bar Icon Pack" from Google Developer

        1.  copy dark/light image
    2.  rename to res/drawable-nodpi folder

4.  create new drawable-nodpi/tab_icon4.xml (copy from tab_icon3.xml)
5.  create Activity4 by copy src/Activity3.java
6.  Edit AndroidManifest.xml , Add Activity4 by copy Activity3
7.  Edit TabInit.java , add tab4 Intent

## Menu Lab

顯示不出來

## Dialog Lab

## UserPreference Lab1

執行程式, 儲存了之後可以在

DDMS FileExplorer
<ul style="list-style: none;"><li>data/data/package.../shared_perfs/main.xml</li></ul style="list-style: none;">

## UserPreference Lab2

Adapter View - User Runtime 產生的資料

List Activity

## SQLlite Lab

**sqlite 的指令**

1. 點開頭, enter 結尾

*   .dump
*   .schema
*   .tables

**執行 lab**

透過 DDMS 取得 android/data/data/com.uuu/database/db.sqlite

c:\>sqlite3 **db.sqlite**

sqlite>** .dump**

PRAGMA foreign_keys=OFF;

BEGIN TRANSACTION;

CREATE TABLE android_metadata (locale TEXT);

INSERT INTO "android_metadata" VALUES('zh_TW');

COMMIT;

sqlite>

**程式的架構:**

*   SQLiteHelper 放DDL (CREATE, ALTER ...)
*   Activity, Services 放 DML(INSERT, SELECT...)

**sqlitelab**

*   參考 exercise README file
*   onUpgrade()

        *   實務上會很複雜, 有 第一個 version 與現在要 upgrade 的 version

*   sqlite3 觀察 db.sqlite
*   BEGIN, COMMIT supported 

**ReceiverLab**

1.  AndroidManifest: Permission: New uses permission android.permission.RECEIVE_BOOT_COMPLETED
2.  new class BootInfoReceiver extends BroadcastReceiver

        1.  implement BrootInfoReceiver onReceive

3.  AndroidManifest applictions add Receiver (會自動找到 BootInfoReceiver)

        1.  exports, enable = true 存檔
    2.  在 BootInfoReceiver 增加 Intent Filter
    3.  Intent Filter 再增加 action, action 的name 選擇 android.intent.action.BOOT_COMPLETED

4.  該程式開始接收 system broadcast (可以重啟模擬器觀察)

WidgetLab

1.  new xml, linear layout, added drawable-nodpi 
2.

## GCMLab

1.  Import project from zip
2.  get API key, project id from [](http://code.google.com/apis/console)http://code.google.com/apis/console
3.  Login on google account on Emulator
4.  Open the C2DMDemo project, change the C2DMDemoActivity

        1.  registerIntent.putExtra("sender", "**projectId**");  **// 數字**

5.  LogCat (c2dm) and look for **registration_id (long)**

                        String data = URLEncoder.encode("registration_id", "UTF-8")

                                        + "="

                                        + URLEncoder.encode(

1.  使用認証代號作認証授權

                        conn.setRequestProperty("Authorization",

                                                        "key=AIzaSyD84Zk4advmi15w1y_lJj2d-h8aB3qqKR8");

## 其他參考資訊

*   ADT 下載 [](http://developer.android.com/sdk/index.html)http://developer.android.com/sdk/index.html
*   Android 版本市佔率 [](http://developer.android.com/about/dashboards/index.html)http://developer.android.com/about/dashboards/index.html
*   程式版控

        *   Bitbucket 類似 Github, 提供免費的 Private Repository
    *   [](https://about.gitlab.com)https://about.gitlab.com

*   Aptana Eclipse Plugin for HTML/Java Script 編輯
*   JNI 應用： 擴增實境 Vuforia(Qualcomm)
*   Art Resource [](http://www.fiverr.com)http://www.fiverr.com 很少的錢就有 logo
*   APK 很容易被上架，寫好的 APK 幾乎是送出去
*   sqlcipher for adroid (NDK) - 可以把 db 進行加密

        *   assets/zip
    *   /libs

                *   NDK Lib -> C/C++
        *   3rd jar -> Java

        *   sqlcipher 會把 SQLite OpenHelper 換為 sqlcipher 的版本

                *   要使用 sqlcipher 來查詢 db.sqlite

*   Content Provider 參考資料 [](http://developer.android.com/reference)http://developer.android.com/reference