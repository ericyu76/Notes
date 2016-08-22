# ServiceMix 5 Study

SMX Question:

*           1. 安裝在 Linux 的 service 5.1.1 怎麼很多基本的 camel 元件都沒有?  要手動裝.

*           2. port 的管理如何做? (目前只能自己指定, 是不是不同的服務都可以指定在同一個 port?)

           [](http://192.168.2.93:1101/services/acceptanceInstall?wsdl)http://192.168.2.93:1101/services/acceptanceInstall?wsdl

        3. 佈署 jar 檔時, 有一些錯誤, 但未進行處理還可以進行

1. Basic Operation

*   Running at Foreground

        *   Start: bin/servicemix
    *   Stop Server: ctrl-D

*   Running at Background

        *   Start: $ **bin/start**
    *   Stop Server: karaf@root> **osgi:shutdown**

*   List features: features:list
*   List osgi: osgi:list
*   "log following": log:tail
*   "Display latest log": log:display

2. web console/hawtio

         features:install webconsole

  **   URL   **[](http://localhost:8181/system/console)**http://localhost:8181/system/console****  id/pw: karaf/karaf**

        install howtio

        smx> features:addurl mvn:io.hawt/hawtio-karaf/1.4.19/xml/features

    smx>features:install hawtio

** URL    **[](http://localhost:8181/hawtio)**http://[l](http://8181:/hawtio)o[c](http://lo8181:/hawtio)a[l](http://loca8181:/hawtio)h[o](http://localh8181:/hawtio)s[t](http://localhos8181:/hawtio):8181/hawtio**** id/pw: karaf/karaf**

3. remote console (by ssh)

        ssh karaf@172.17.120.84 -p 8101

4. deploy camel example

  -- copy jar file to %servicemix%/deploy

  -- features:install camel-http