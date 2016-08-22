# Overlord S-RAMP, DTGov

**1. S-RAMP (SOA Repository Artifact and Model Protocol)**

1.  功能及用途

        1.  JBoss 實作 OASIS 的 S-RAMP 標準 ([](https://www.oasis-open.org/committees/s-ramp/))https://www.oasis-open.org/committees/s-ramp/) , 用來分享 SOA Repository 的資訊
    2.  Artifact 管理 (任何有關服務文件的管理), 包含 Artifact 的屬性, 分類, 關係
    3.  分類管理(類似 Hierarchy)

2.  使用者介面 [](http://172.17.120.84:8080/s-ramp-ui/)http://172.17.120.84:8080/s-ramp-ui/
3.  透過 demos 目錄下, 執行下列指令可以瞭解如何用 Java 程式透過 S-RAMP 提供的 REST API 進行 Artifacts 管理

*   mvn -Pdemo -Dsramp.auth.username=admin -Dsramp.auth.password=admin -Dsramp.endpoint=[](http://172.17.120.84:8080/s-ramp-server)http://172.17.120.84:8080/s-ramp-server clean test 

## S-RAMP 工具名詞解釋 

*   **Classfier **- 分類, 類似 Tag(#) 的方式, Tag 之間沒有關係
*   **Ontologies ([知識本體](http://www.gss.com.tw/index.php/focus/eis/79-eis40/525-ontology)) **

        *   有 Hierarchy 的Tags
    *   利用OWL Lite format , 可以參考 DEMO Ontologies 

*   **Artifacts **(人造物) - 人類看得懂的東西(非給機器看的)

## Follow Up

*   定義 SOA Repository 的概念(介紹 S-RAMP)

*   定義 Ontologies, 建立 **testritegroup.soa.owl.xml**

**2. DTGov**

1.  功能及用途

        1.  Artifact 管理 (任何有關服務文件的管理), 包含 Artifact 的屬性, 分類, 關係
    2.  分類管理(類似 Hierarchy)

2.  使用者介面 [](http://172.17.120.84:8080/s-ramp-ui/)http://172.17.120.84:8080/s-ramp-ui/

** 3.安裝**

*   下載 overload-1.0.0.Final.zip 包含了 DTGov 及 S-RAMP 二個元件
*   若選擇使用 tomcat , ant 會自己下載一份 Tomcat 7 , Ant 版本要用最新的

*   ant deploy-tomcat