# Hybris WCMS 課程筆記

## Hybris Type System 開發 

Model Driven Development (數據建模-抽象的設計模型)

1.  只放 item.xml, model 的 defination 到版控系統

        1.  Collections(建議少用) vs Relations(儘量用這個)
    2.  Deployment Table (獨立建立一個表)

## Merchandise Project Overview

*   **merchandisecockpit **(後台)
*   **merchandisecore** ( implementation 有關的 cms 後台)

        *    - resources/merchandisecore/import/cockpits/cmscockpit/structure-view/TlwContentPageTemplate.vm

*   **merchandisefacades **與用戶相關的資料
*   **merchandiseinitialdata** 初始數據的程式

        *   resources/import/impex files

*   **merchandisestorefront **前端

        *   JSP - \web\webroot\WEB-INF\views\desktop\cms\*.jsp
    *   Controllers - web\src\de\hybris\merchandise\storefront\controllers\pages\TLWProductPageController.java

*    **merchandisefullfillment **與訂單相關的(訂單流程)

## 開發的第一階段-準備 Project Initial Data Process

SampleDataImportService - 每次按下 initialized 及 update時都會呼叫

 - InitialDataSystemSetup **extends SampleDataImportService** 

1.  Create Class Merchandise overide importContentCatalog
2.  建 impex (暫時先放空的)   

        1.  **ImpEx － **對Type System 進行資料的最底層的操作

3.   **initialdata-spring.xml **把剛剛寫的 InitialDataSystemSetup  bean 放到 spring xml
4.     alias="sampleDataImportService" 這樣就會取代原來的 defaultSampleDataImportService

4. 到 hmc 的 wcms UI 去查資料確認 PageTemplate/Velocity/Slot 是否正確.

## 第二階段 瞭解 WCMS Model

- 建議先從 Model 瞭解, 透過 Impex 來進行設計

**WCMS ImpEx 的資料結構**

*   調整 WCMS 的 Impex

        *   PageTemplate （.jsp)
    *   Slot (Template 上的)
    *   Component (實際的元件)
    *   Restrictions (權限)

*   建立 Velocity Template (for copit) (.vm file)
*   最後到 cmscockpit 新增頁面, 確認可以新增頁面, 及看到 .vm file Template
*   透過 Storefront 可以看到 設計出來的 JSP

## 第三階段 Create

透過 Impex 創建頁面

1.  ContentPage
2.  masterTempate
3.  label  ---> Controller Label
4.  defaultPage
5.  approvalStatus
6.  ContentSlot
7.  ContentSlotForPage

**建立 Controller (Programing)**

建立 Controller extends AbstractPageController (TLWProductPageController)

Label -> AbstractPageModel -> jsp (in the PageTemplate)

1. 取得 cmsPageService

@Resource(name = "cmsPageService")

private CMSPageService cmsPageService;

2. 與 CMS 的 controll 的 product_page (using label)

cmsPageService.getDefaultContentPage(PRODUCT_PAGE_LABEL); //

3. 按 AbstractPageController 的方式回傳頁面

storeCmsPageInModel(model, getPageForProduct());

return getViewForPage(model);

**建立 Paragraph Component by Impex (文字)**

CMSParagraphComponent

- name

- content

- cmsComponent(&componentRef) (引用之前定義的)

建立 JspIncludeComponent Component by Impex (JSP) 

**Update System**

修改 Controller/ ant all/ restart server

PS: impex 可以到 console ImpEx 的 Import Tools 試跑(其實也就真的執行了, 但只會更新 stage)

## 自建擴充 Component

**建立 RandomImageComponent**

[](https://wiki.hybris.com/display/R5T/Creating+New+CMS+Components)https://wiki.hybris.com/display/R5T/Creating+New+CMS+Components

建立自己的 Paragraph Component (獨立的 MVC model)

*   **extends ParagraphCompnent**

*   Model: ItemType
*   View: Component Slot - 要對應一個 jsp (JSP名稱要與 Component Code 完全對應)
*   Controller: Render - 可以看做 Component 的 Controller

PS:

1) Enum Type 在 Impex 要用 topic(code)

2) Text 要加上 Text[lang=en] 才會有作用

## Action (WCMS 元件的 Behavior)

Merchaindisestore 若要從頭, 可以從 core trail commerce II 的 optional

Action(也是一個特別的 Component)

1.  create action in items.xml (itemType 要 extends="SimpleCMSAction")
2.  設定 impex
3.  create view 要對應一個 jsp (JSP名稱要與 Component Code 完全對應)

        1.  JSP 裡 有一個 _url 變量
    2.  有一個 form 裡面的資料來自於
    3.  form 裡面的 變數 來自於 controller

*   ################################
*   PS: 調整了 item.xml 必需 update
*     1) Updating system
*     2) Localizing types
*   ################################

## Restriction (設計權限)

**建立Custom Restriction**

範例: 建立使用者權限 (只有某個人可以看到) CMSUserRestriction

1.  using ImpEx update CMSUserRestriction
2.  create item.xml MyCMSrestrition extends AbstractRestrition

        1.  PS: persistentce type = properteis (真正mapping 到資料庫的欄位)

                1.  persistentce type = dynamic (可從 properteis 計算出來)

3.  spring-bean.xml

        1.  create description bean implement
    2.  create evaluator bean implement

4.  create spring bean base on 2 and 1

## 訂單管理流程 OMM/OMS

在客人下了訂單之後的流程 

OMM - 基於 Hybris 的 workflow, 集成

 - 因為集成還有人類介入, 一定是 Async

 - 通常會變, 所以只提供接口及 Mock

 - 流程 (machandisefullfillmentprocess)

    1) 虛假訂單檢查 (fruad check)

        2) 物流 

OMS

 - 5.7 與 OMM 整合

 - 還與 MongoDB 整合

hybris 的 process 都儲存在 DB 裡, 可以透過 hmc 來查詢

## 促銷 vouchers

Vouchor

Promotion

工程師可以在 hmc 裡去進行設定, 若是 MK/MD 應該從 backoffice 進行

問題:

=====

1) cmscockpit 為什麼不能 live editor? Ans: 要加 Template

2) 版面的 approval 怎麼做?

3) 可以預定時間排程上版嗎? (Restriction)

4) 頁面的權限設定 Restrisrtion

5) 內建的 Component 介紹?

6) storefront 的 module 哪裡來? module gen?

6) template 介紹?

7) Export/ImpEx?