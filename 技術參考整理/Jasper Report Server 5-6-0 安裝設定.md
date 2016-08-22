# Jasper Report Server 5.6.0 安裝設定

**為什麼要使用 Report Server**

*   把報表的需求與應用伺服器分開佈署, 達到分散資源的目的
*   把 Report 產生的邏輯與應用程式分開

**選擇 Jasper Report Server Community的理由**

*   免費 

        *   Community Report Server 執行過程中的 Run-time DB 不支援商業版的 DB, 例如: Oracle, 這裡採用 Mysql, 但產生報表的 DB 不在此限

*   有完整的 Rest API 可以進行整合
*   提供適度的 UI 可以直接用來當作 End User 的 Report Server
*   提供 Mobile App 可以產生報表

**安裝前備**

*   使用自備 Tomcat 7, 透過 buildmatic 進行設定, 經測試 Repository DB 使用 MySQL 可正常使用

        *   Tomcat Server: apache-tomcat-7.0.zip
    *   Jasper Report Server War Archive: jasperreportserver-5.6.0.war
    *   MySQL Server with root permission
    *   JDBC Driver: Ex: ojdbc6.jar (Oracle R11)

*           CATALINA_OPTS="-Xms1024M -Xmx2048M -XX:MaxPermSize=512M"

*   透過 catalina.sh 裡的 CATALINA_OPT 來設定...(最簡單的做法必需設定在run 之前) 

*   需自備 jdbc driver 安裝在 Tomcat 上面.

**Jasper Report Server 安裝(採 War Archive Install 的方式**

*   設定步驟(使用 Jasper Report Server 提供的 Omatic 方式安裝)

*   copy sample_conf/mysql_master.properties to default_master.properties

*           ./js-install-ce.sh

**開始執行測試**

*   啟動 Tomcat ( tomcat_folder/bin/startup.sh)
*   打開瀏覽器登入 [](http://172.17.120.137:8880/jasperserver/login.html)http://172.17.120.137:8880/jasperserver/login.html

## 中文字型

**執行 iReport.exe 製作字型檔案的 extension jar**

1.   使用Windows 的字型檔, Copy c:/Windows/Fonts/msjh.ttf 到 iReport Designer 的 Fonts 目錄 (要是 ttf 才行)
2.  在 designer 的 tools> setting > Fonts Tab 裡 Install Font 目錄的字型

1.  建議字型的名字不要取和系統字型類似, 可能會搞混
2.  從 Designer tools>setting>Fonts Tab 中匯出字型 jar 檔

**iReport Designer 字型設定**

若直接使用系統中文字型, 放到 server 會不能顯示, 要使用另外安裝的字型(橫線以上的)

  使用 extension jar

1.  iReport > 工具 > 選項 > iReport(Tab) > Classpath
2.  把 3chinesefont.jar (預先製作的中文字型 extension jar) 加進 classpath 即可看到三個字型 xxx(ttf)可以選擇(千萬不要選擇系統字型)

**Report Server 字型設定**

1.   將 3chinesefont.jar 檔放到 tomcat lib 目錄裡
2.   只要 class loader 讀得到都可以, 重新啟動 Tomcat 

## 透過 http 與 Jasper Report Server 進行溝通

**API:**

*   (Background) Execution Reports

*   (POST) [](http://172.17.120.84:8080/jasperserver/rest_v2/reportExecutions/)[http://172.17.120.84:8080/jasperserver/rest_v2/reportExecutions/](http://172.17.120.84:8080/jasperserver/rest_v2/reportExecutions/)
*    {
*       "reportUnitUri": "/reports/som/cbsku",
*       "async": "true",
*       "freshData": "false",
*       "saveDataSnapshot": "false",
*       "outputFormat": "pdf",
*       "interactive": "false",
*       "ignorePagination": "false",
*       "parameters": {
*         "reportParameter": [
*           {
*             "name": "skuNoStart",
*             "value": [
*               "199000"
*             ]
*           },
*           {
*             "name": "skuNoEnd",
*             "value": [
*               "200000"
*             ]
*           }
*         ]
*       }
*     }
*

*   (GET) [](http://172.17.120.84:8080/jasperserver/rest_v2/reportExecutions/33020942-38c5-42a7-98ce-dc528e07c711)http://172.17.120.84:8080/jasperserver/rest_v2/reportExecutions/33020942-38c5-42a7-98ce-dc528e07c711