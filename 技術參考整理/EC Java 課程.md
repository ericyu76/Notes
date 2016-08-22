# EC Java 課程

## 課程大網

1. Basic Java (I) (java.lang)

*   Install Java SDK
*   Install Eclipse
*   Eclipse Debug
*   OO Basic
*   JavaBean

2. Basic Java(II) (java.util, java.io)ju

*   Exception
*   Collection/List/Map
*   Properties/Map
*   I/O
*   Calendar

3. Basic Java (III)

*   JDBC
*   JDBC Transaction

*   DAO Framework(Hibernate/SQLMap)

 4. Java Web Application

*   Tomcat
*   Java Web Servlet/JSP
*   Spring Framework
*   Spring MVC

5. Basic Java (IV)

*   logs ([](https://wiki.base22.com/display/btg/How+to+setup+SLF4J+and+LOGBack+in+a+web+app+-+fast))https://wiki.base22.com/display/btg/How+to+setup+SLF4J+and+LOGBack+in+a+web+app+-+fast)

*   Build tool - Ant/Maven
*   XML JAXB
*   WebServices SOAP
*   JSon

6. Java Web Framework

*   Hibernate

7. Jasper Report/Report Server

*   Understand Report Concept
*   Create Report

** **

## EC Java 第九次上課

  **UML Class Diagram**

*   Generalization
*   Realization
*   Association/Aggregation
*   Dependency
*   Stereotype

 參考資料 : [](http://puremonkey2010.blogspot.tw/2010/10/oo-uml.html)http://puremonkey2010.blogspot.tw/2010/10/oo-uml.html 

 **Spring Core **

[](http://docs.spring.io/spring/docs/current/spring-framework-reference/html/beans.html)[http://docs.spring.io/spring/docs/current/spring-framework-reference/html/beans.html](http://docs.spring.io/spring/docs/current/spring-framework-reference/html/beans.html)

*   <**bean** class="de.hybris.platform.order.OrderService">
*       <**property** name="stockService">
*           <**bean** class="de.hybris.platform.stock.StockService"/>
*       </**property**> 
*   </**bean**>
*

今天進行的內容:

1.  透過 Java Code 讀取 ApplicationContext.xml 來啟動 Spring Container
2.  透過 <bean id="..." class="com.testritegroup...."> 來 create services
3.  透過 <property> 來設定 bean 的 initial data
4.  透過 <property ref="..."> 來 reference 不同的 bean
5.  透過 <context:annotation-config/>  並在 Java code 的 Annotation(@Autowired) 來設定 reference
6.  透過 <context:component-scan base-package="com.testritegroup.learning" /> 加上 @Component來設定 bean

**JUnit**

1.  使用 JUnit 的優點 (主要是 Eric 的看法, 其他人也可以添加自己的想法)

        1.  相較於使用 main 來測試, 可以累積更多的 TestCase
    2.  可以把 Test Code 與 Production Code 分開
    3.  有容易閱讀的報告易於發現錯誤
    4.  Rebuild 時自動執行

*   **ANT**

- [](http://www.tutorialspoint.com/ant/)[http://www.tutorialspoint.com/ant/](http://www.tutorialspoint.com/ant/)

*   Spring DAO (要確認一下 Hybris 的 DTO 怎麼用???)

 [](http://www.petrikainulainen.net/spring-data-jpa-tutorial/)[http://www.petrikainulainen.net/spring-data-jpa-tutorial/](http://www.petrikainulainen.net/spring-data-jpa-tutorial/)

*    Spring Transaction

## EC Java 第八次上課

*    **Spring MVC RESTful Design**

[](http://howtodoinjava.com/2015/02/20/spring-rest-hello-world-json-example/)http://howtodoinjava.com/2015/02/20/spring-rest-hello-world-json-example/

<beans xmlns="[](http://www.springframework.org/schema/beans)http://www.springframework.org/schema/beans"

        xmlns:context="[](http://www.springframework.org/schema/context)http://www.springframework.org/schema/context"

        xmlns:xsi="[](http://www.w3.org/2001/XMLSchema-instance)http://www.w3.org/2001/XMLSchema-instance"

        xmlns:mvc="[](http://www.springframework.org/schema/mvc)http://www.springframework.org/schema/mvc"

        xsi:schemaLocation="

[](http://www.springframework.org/schema/beans)http://www.springframework.org/schema/beans

[](http://www.springframework.org/schema/beans/spring-beans-3.0.xsd)http://www.springframework.org/schema/beans/spring-beans-3.0.xsd

[](http://www.springframework.org/schema/context)http://www.springframework.org/schema/context

[](http://www.springframework.org/schema/context/spring-context-3.0.xsd)http://www.springframework.org/schema/context/spring-context-3.0.xsd

[](http://www.springframework.org/schema/mvc)http://www.springframework.org/schema/mvc [](http://www.springframework.org/schema/mvc/spring-mvc-4.0.xsd)http://www.springframework.org/schema/mvc/spring-mvc-4.0.xsd">

        <context:component-scan base-package="com.testritegroup.learning" />

         <mvc:annotation-driven />

        <bean

                class="org.springframework.web.servlet.view.InternalResourceViewResolver">

                <property name="prefix">

                        <value>/WEB-INF/views/</value>

                </property>

                <property name="suffix">

                        <value>.jsp</value>

                </property>

        </bean>

</beans>

 DAO (Data Access Object)

## EC Java 第七次上課

*   **Spring Core **

[](http://docs.spring.io/spring/docs/current/spring-framework-reference/html/beans.html)http://docs.spring.io/spring/docs/current/spring-framework-reference/html/beans.html (補充)

*    

*   **Spring MVC(Model View Controller)**

[](http://www.programcreek.com/2014/02/spring-mvc-helloworld-using-maven-in-eclipse/)http://www.programcreek.com/2014/02/spring-mvc-helloworld-using-maven-in-eclipse/ (Maven)

mvn archetype:generate -DgroupId=com.testritegroup.learning -DartifactId=mymvnproject -DarchetypeArtifactId=**maven-archetype-webapp** -DinteractiveMode=false

*   **Spring MVC + JSTL**

[](http://www.mkyong.com/spring-mvc/spring-mvc-and-list-example/)http://www.mkyong.com/spring-mvc/spring-mvc-and-list-example/

JSTL (Java Standard Tag Library)

1.  pom 加上 JSTL depency

*                    <dependency>
*                           <groupId>jstl</groupId>
*                           <artifactId>jstl</artifactId>
*                           <version>1.2</version>
*                   </dependency>

1.  jsp 要宣告 tag library

*   <%@taglib prefix="c" uri="[](http://java.sun.com/jsp/jstl/core)[http://java.sun.com/jsp/jstl/core](http://java.sun.com/jsp/jstl/core)"%>
*   <%@taglib prefix="fmt" uri="[](http://java.sun.com/jsp/jstl/fmt)[http://java.sun.com/jsp/jstl/fmt](http://java.sun.com/jsp/jstl/fmt)"%>

1.  Jsp 裡使用 <c:forEach>

*   <c:forEach  var="item" items="${items}">
*                   <li>${item.sku}: ${item.name} : ${item.price}"</li>
*           </c:forEach>

※ 改變 eclipse new jsp file 的 default charset:

[](http://veerasundar.com/blog/2010/12/changing-eclipse-default-encoding-to-utf-8-for-jsp-files/)http://veerasundar.com/blog/2010/12/changing-eclipse-default-encoding-to-utf-8-for-jsp-files/

## EC Java 第六次上課

 **Web**

Tomcat - Create a Servlet in Eclipse

[](http://tomcat.apache.org/download-70.cgi)http://tomcat.apache.org/download-70.cgi 

jar = java archive

war = web java archive

war  (web java archive)

index.html

xxx.html

...

...

WEB-INF

     classes  <== 自己寫的程式

     lib           <== jar檔存放的位置

     web.xml <== Deployment Description 簡稱DD (war 檔的設定) 給WEB SERVICE ,TOMCAT看的設定

 JavaBean

**Maven**

[](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html)https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html

建立 Maven 專案

*   > mvn archetype:generate -DgroupId=com.testritegroup.learning -DartifactId=mymvnproject -DarchetypeArtifactId=**maven-archetype-quickstart** -DinteractiveMode=false
**   <dependency>
*           <groupId>ch.qos.logback</groupId>
*           <artifactId>logback-classic</artifactId>
*           <version>1.1.3</version>
*   </dependency>
*

**Maven 編譯**

>mvn compile 

**Maven 產生 jar 到 target 目錄**

>mvn package

**把已經編譯的資料清除, 回復到只有 source code 的狀態**

>mvn clean

**Logback 的設定**

*   <?xml version="1.0" encoding="UTF-8"?>
*   <configuration>
*     <appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
*       <layout class="ch.qos.logback.classic.PatternLayout">
*         <Pattern>%d{HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n</Pattern>
*       </layout>
*     </appender>
*     <logger name="com.base22" level="TRACE"/>
*     <root level="debug">
*       <appender-ref ref="STDOUT" />
*     </root>
*   </configuration>

## EC Java 第五次上課

*    Install mysql at local or remote
*   Setup Eclipse SQL Explorer/ JDBC Driver

*   JDBC Basic/ CRUD

*   PreparedStatement pstmt = conn.prepareStatement("insert into my_course (ID, NAME, START_DATE)  values (?,?,?)");
**   pstmt.setInt(0, 100);
*   pstmt.setString(1, "Basic Java 5th");
*   pstmt.setDate(2, new Date(System.currentTimeMillis()));
**   int effectRow = pstmt.executeUpdate();
**   System.out.println("Inserted "+ effectRow +" Rows");

*   DB Transaction
*   Connection Pool 的概念

MySQL : 

*   inno DB(5.5之後default) : 這個才有Transaction
*   MyISAM(5.5之前default)

在建立MySQL連線時這樣可以指定連線時的編碼：

*   conn = DriverManager.getConnection("jdbc:mysql://172.17.120.114:3306/John?useUnicode=true&characterEncoding=utf-8", "jscat", "ecJavaLearning");

儲存時間到SQL時可以用Timestamp

*   pstmt.setTimestamp(2, new Timestamp(in.getCreatedate().getTime()));

JAVA 透過 JDBC 取得 MYSQL LAST INSERT ID 的方法參考：

[](http://stackoverflow.com/questions/1915166/how-to-get-the-insert-id-in-jdbc)http://stackoverflow.com/questions/1915166/how-to-get-the-insert-id-in-jdbc

*   pstmt = conn.prepareStatement("INSERT的SQL語法", **_Statement.RETURN_GENERATED_KEYS_**);
*   try (ResultSet generatedKeys = **_statement.getGeneratedKeys()_**) {
*       if (generatedKeys.next()) {
*           user.setId(generatedKeys.getLong(1));
*       }
*       else {
*           throw new SQLException("Creating user failed, no ID obtained.");
*       }
*   }

*   **Oracle 產生 id**
*   create sequence ORDER_SEQ interval 1 to 9999999999 inc by 1;
*   1. insert into ORDER values (ORDER_SEQ.next_val, ...)
*   2. select * from ORDER_SEQ.next_val;
*       insert into Order values ( value,...) 
*       

[](http://abu.tw/2008/06/oracle-autoincrement.html)http://abu.tw/2008/06/oracle-autoincrement.html

## EC Java 第四次上課

ShoppingCartCalc - **Domain Model** 與 **Transaction Script** 的設計概念的不同

ArgoUML ([](http://argouml.tigris.org/))http://argouml.tigris.org/) - Open Source 的 UML 工具

**Properties**

利用 ResourceBundle 來讀取 properteis

Configuration.properties, 設計 properties 要注意幾個優良的原則:

*   要寫註解, 註解要說明單位
*   能夠補充設定的例子
*   透過 Singleton 可以讓取得 properties 可以集中管理/一致

java 下面目錄符號使用 /

*   其實, Java 的目錄分隔符號, 可以依照不同作業系統使用 / 或 \, 建議使用 /, 可以通用於不同的作業系統.

**ReadFile to String**

[](http://stackoverflow.com/questions/16027229/reading-from-a-text-file-and-storing-in-a-string)http://stackoverflow.com/questions/16027229/reading-from-a-text-file-and-storing-in-a-string

如果要讀入 big5 的檔案格式要改用 InputStreamReader, 方可指定 charset

[](http://seke-blog.blogspot.tw/2008/12/how-to-read-big5-file-in-java.html)http://seke-blog.blogspot.tw/2008/12/how-to-read-big5-file-in-java.html

使用 InputStream 可以指定 encoding (MS950, UTF-8)

**Write String to a TextFile**

[](http://www.mkyong.com/java/how-to-write-utf-8-encoded-data-into-a-file-java/)http://www.mkyong.com/java/how-to-write-utf-8-encoded-data-into-a-file-java/

**Java 的時間系統**

*   java.util.Date - 目前是用來裝 Date 格式的物件, 在不同的程式間傳遞 Date 物件

        *   new Date() - 取得目前的時間, 精細度至 milli-second

*   java.util.Calendar - 用來進行日期計算/比較的物件
*   java.text.SimpleDateFormat - 字串與 Date 之間的互相轉換

        *   parse() - String 轉換為 Date
    *   format() - Date 轉換為 String

**作業**

延續上次的作業

1.  列印發票資料到文字檔 (用 MS950 編碼)
2.  列印發票要加印日期及時間 例如: 2015/09/03 12:30
3.  編碼利用 Properties 設定
4.  Feedback [](http://goo.gl/forms/NkzGuP7Wd3)[http://goo.gl/forms/NkzGuP7Wd3](http://goo.gl/forms/NkzGuP7Wd3)

## EC Java 第三次上課

變數範圍 Scope (Class member 變數, Method 變數, static 變數)

final 變數不能改

//public final int bornCount = 205;

public static final int = STUDENT_GENDER

**Exception**

*   RuntimeException (執行程式才會出現, java.lang.RuntimeException)
*   CheckedException (寫程式時就會出現, java.lang.Exception)

        *   由開發人員解決

*   使用 RuntimeExecption 的差別在於 function 不用加 throws ECException, 程式裡不用加 try catch 它也會將錯誤拋出來

**List (Interface)**

*   與 Array 的差異在於一開始不用知道大小, 一個一個加上去

**Map (Interface)**

*   這種資料結構可以用 Key 可以快速找到 Object

*   Grouping Data Map<Key, ArrayList<Object>>

**Collection(Interface)**

*   為 List 的父類別
*   使用 Iterator 的方式取得資料

有加static的變數不用new也不需要預先宣告

*   有個組促的 interface 可以拿來秀一下, 裡面有用到 HashMap

**memo : **

Public class Student {

   String name = "Eric";

        String getName(String name){

                return name; //這裡的name是指帶入getName的值(args)

                return this->name; //這裡的name是指Eric(抓class本身)

        }

}

**List**

HashMap foreach 的用法:

ref: [](http://stackoverflow.com/questions/4234985/how-to-for-each-the-hashmap)http://stackoverflow.com/questions/4234985/how-to-for-each-the-hashmap

以上課的案例來看:

                for(Entry<String, Student> entry : studentsMap.entrySet()) {

                    String key = entry.getKey();

                    Student  student1 = entry.getValue();

                    System.out.println("key:" + key + " age:" + student1.getAge());

                }

## EC Java 第二次上課

**語言基礎**
<undefined><li>**型別(Type)初值**</li></undefined>

byte short int **0**

long **0L**

float **0.0f**

double **0.0d**

char **'\u0000'**

boolean **false**

所有參考型別  **null**

**int vs Integer (先佔式型別 vs Class)**

*   int 是沒有 method
*   Integer 可以 serializable (序列化-- 表示可以用來進行傳輸或儲存)
*   Integer 有很多方法(method)

int  : 固定小寫的型別 / c寫的 / 沒有方法

Integer : 擁有很多方法 / 可以serializable

long : 64bit

[BigDecimal](http://docs.oracle.com/javase/7/docs/api/java/math/BigDecimal.html) : 可以存很長 小數點也可以處理

String : 底層是char , 唯一個的class卻沒有new

String的相等不能用 == 要用 equals

String age1 = new String("Eric"); 

String age1 = new String("Eric");

age1 == age2..........x

age1.equals(age2) ....ok

java在運行中都是用unicode

Eclipse 多行註解 - Ctrl + /

Eclipse 程式自動排版 - Ctrl + Shift + f

Eclipse 產生javaDoc

*   Project -> generiate JavaDoc  
*   config:  要選 C:\Program Files\Java\jdk1.7.0_45\bin\javadoc.exe

**Java API Doc**

產生自己程式的 Java Doc (很奇怪 Java 8 沒有 java doc)

[](http://eric1300460.pixnet.net/blog/post/30380556)[http://eric1300460.pixnet.net/blog/post/30380556](http://eric1300460.pixnet.net/blog/post/30380556)

Java SDK 的 Java Doc

[](http://docs.oracle.com/javase/7/docs/api/)[http://docs.oracle.com/javase/7/docs/api/](http://docs.oracle.com/javase/7/docs/api/)

**OO Basics**
<undefined><li>**繼承**</li></undefined>

*   extends 可以得到 parent 所有的 attribute 及 method
*   constructor 也被繼承, 若有 constructor 要使用 super 建構

        *   super 可以 呼叫父類別的 method

*   method 可以 overwrite

*
<undefined><li>**多型**</li></undefined>

*   interface - 只能定義Input、Output 不用實作 (method 要宣告 abstract, 不需要 implement code)

*   **Product **product = new **Furniture**();

*    java.lang(基本) 不用 import;
*    java.util
*            Collection..
*            Map
*            List
<undefined><li>**封裝**</li></undefined>

*   jar
*   [](http://logging.apache.org/log4j/1.2/download.html)http://logging.apache.org/log4j/1.2/download.html

## EC Java 第一次上課

*   Java SE/Java EE
*   Java Command Line: java, javac
*   Main Program(Hello World)
*   public static void main(String args[])

*   [scope-定義 method 可以被使用的 package 範圍]
*   [static - method 是否需要 initializing ]
*   [void -  回傳值]
*   [args[] - command argument]

*   Java Package
*   Eclipse, Install, New Project, 介紹開發環境
*   Eclipse Debug

Object vs Class

*   Class - 定義好的型別

*   Object - instance

建構子與方法的差異:

*   方法有回傳值
*   建構子的名稱跟class一樣

## 參考資料

*   [](https://docs.oracle.com/javase/tutorial/)[https://docs.oracle.com/javase/tutorial/](https://docs.oracle.com/javase/tutorial/)

## 作業

1.  第一週  [](http://goo.gl/forms/NkzGuP7Wd3)[http://goo.gl/forms/NkzGuP7Wd3](http://goo.gl/forms/NkzGuP7Wd3)
2.  第二週  [](http://goo.gl/forms/NkzGuP7Wd3)[http://goo.gl/forms/NkzGuP7Wd3](http://goo.gl/forms/NkzGuP7Wd3)

## 備註

*   [](https://logging.apache.org/log4php/)[https://logging.apache.org/log4php/](https://logging.apache.org/log4php/)