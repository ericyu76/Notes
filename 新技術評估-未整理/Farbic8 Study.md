# Farbic8 Study

## 設定及執行

Fabric8 下載下來裡面就包含了 karaf 的核心及 fabric 的機制, 解開後執行 fabric8 就可以進入 port 8181 的 hawtio 界面進行設定.

(PS: JBoss Fuse 似乎就是 Fabric8)

**建立 Profile**

Profile 是一組設定的集合, 透過預先佈署及設定的 profile 可以讓 fabric 很容易的横向擴充

透過fabric8 提供的 quickstart 的文件說明, 就可以進行 profile 的mvn deploy. 執行完 deploy 後進入 hawtio 管理界面, 可以看到已經 deploy 的 profile. (內建已經有了一個 root 的 profile)

**建立 Container**

Container 就是執行工作的最小單位, 透過 Profile 產生的獨立 JVM instance. 建立好 Profile 之後, 就可以很容易透過 hawtio 界面或 command line 進行 container 的擴充.

hawtio 提供了很方便的使用者介面可以讓建立 container 簡單的建立: runtime > profiles > 

**專有名詞**

Fabric - 管理Container 的單位 <--不是很確定, 本身要做到容錯至少需有3台

## Developer Workflow

*   這個似乎把我想知道的整個開發流程定義好了, 要參考這個來做.(然後與 SOA 的 Service Governance 一起看)

[](http://www.christianposta.com/blog/?p=373)[http://www.christianposta.com/blog/?p=373](http://www.christianposta.com/blog/?p=373)

[](http://fabric8.io/gitbook/developer.html)[http://fabric8.io/gitbook/developer.html](http://fabric8.io/gitbook/developer.html)

*   建立 profile最快的方式(參考 [](http://www.christianposta.com/blog/?p=373))[http://www.christianposta.com/blog/?p=373](http://www.christianposta.com/blog/?p=373))

## 待處理

*   Web Services/Camel Route 如何放到 Profile裡? (參考建立 Profile 的方式)

*   Development Flow (與git 如何整合)
*   把 container 放在不同的 machine 裡進行 cluster 測試