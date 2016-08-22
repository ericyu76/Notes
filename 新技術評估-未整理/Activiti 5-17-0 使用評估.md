# Activiti 5.17.0 使用評估

Activiti 是 jBPM 3/4 的延續, 所以 Activiti 的版號就從 5 開始. 相對於 jBPM5 來說, 較為 light weight, 且為 jBPM 3/4 的原作者所維護的.  jBPM5 對於之前已經瞭解 jbpm3/4 的使用者來說會很容易入門使用. 目前台灣似乎沒有代理廠進行企業級的支援.

## 安裝及設定

安裝過程很簡單, 預設使用內建的H2 Database,  可以讓大家快速針對功能的部分進行評估.

1.  事先準備

        1.  jdk 1.7 或以上

2.  Download activiti-5.17.0.zip
3.  Download apache-tomcat-7.0.59.zip
4.  Copy activiti war to tomcat webapps folders

        1.  activiti-explorer.war
    2.  activiti-rest.war

5.  Start Tomcat Server(Activiti Server)

*   >%tomcat%/bin/startup.sh

## Create Flow