# Camel Study 及實作

Prepare:

1. Get real wsdl file (將會拿來改為 proxy 的 wsdl)

步驟:

1. 調整 wsdl 的 address binding 為 ESB 的domain

2. 根據 wsdl 產生 class (As a Proxy WSDL)

        1) 改 POM.xml 的 wsdl  file

        2) 記住 wsdl 的 

                <wsdl:service name="XXX"> 

                <wsdl:port name="YYY">

        2) mvn compile

2. 調整 camel-context

        1) RealService --> 參考服務提供者的 WSDL get real service endpoint

        2) 設定  Proxy Service <cxf:cxfendpoint>

                  <cxf:cxfEndpoint id="acceptanceInstall"

                   address="[](http://localhost:1101/services/acceptanceInstall)http://localhost:1101/services/acceptanceInstall"

                   endpointName="s:acceptanceInstallSoap11"

                   serviceName="s:acceptanceInstallService"

                   wsdlURL="etc/acceptanceInstall.wsdl"

                   xmlns:s="[](http://localhost/so-webservice/acceptanceInstall)http://localhost/so-webservice/acceptanceInstall"/>

                1. id: 取個名字, 會用在 route 裡

                2. address: proxy 對外服務的 ip/port (endpoint) 加上 "?wsdl" 可以拿到 wsdl

                3. endpointName: proxy service wsdl 上的 endpointName, 即 YYY

                4. serviceName: proxy service wsdl 上的 service Name, 即 XXX

                5. wsdlURL: proxy service 的 wsdl 檔

                6. "xmlns:s": proxy wsdl 的 targetNamespace

Camel Questions:

1) 為什麼是 1101, 1102 port?

2) (Resolved) RealService 裡的 org.apache.camel.example.reportincident 這個 package 的 class 從哪裡來的? (是 POM 裡的 apache parrent 套件)

3) 目前包版的程式還未能獨立 rebuild 脫離 apache example

4) (Resolved)Step 1 產生的 service 是 proxy 還是 real? endpoint 要設什麼 port?  (是 proxy 的)

5) 把所有不同的 proxy service 放在一個 bundle 比較好, 還是全部分開建立 route 比較好?

<<Todo>>

MQ 整合 [](http://lowry-techie.blogspot.tw/2010/11/camel-integration-with-websphere-mq.html)http://lowry-techie.blogspot.tw/2010/11/camel-integration-with-websphere-mq.html

===========

MQ SIT IP: 172.17.120.51

username: truser

pw: Testrite

localhost login

os windows 2003

This pad text is synchronized as you type, so that everyone viewing this page sees the same text.  This allows you to collaborate seamlessly on documents!