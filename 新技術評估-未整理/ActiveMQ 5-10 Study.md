# ActiveMQ 5.10 Study

1.  Windows 版與Linux 版本並不通用要分開下載及安裝

*   bin/activemq start

1.  管理界面

        1.  amq 的 default port 是 61616
    2.  Web 管理界面  [](http://localhost:8161/admin)http://localhost:8161/admin

2.  Demo 的範例在 example 目錄裡

執行的方式: 

*   C:\opt\apache-activemq-5.10.0>bin\activemq.bat start xbean:examples/conf/activemq-demo.xml

問題及Todo:

*   為什麼 hawtio 界面不能使用, 網路文章說 5.9 開始內建?
*   執行範例時, 為什麼會有 Camel, 與 camel 的關是什麼?

*   MQTT 到底是羽量級的資料傳輸格式.