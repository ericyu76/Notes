# Gitlab 安裝及設定

1.  下載 gitlab commnuity Edition(for Centos)

1.  使用 root 帳號登入，執行安裝

## 權限設計及 LDAP 整合

*   讓使用者不能自行建立專案 (擔心硬碟空間不足)
*   使用者不能隨意自行建立帳號

        *   設定使用者自建專案數為 0

*   先建立 Group 再到 Group 裡建立專案(專案就不會建立在某個人身上了)

        *   由 Admin 建立專案

                *   先選擇專案 Owner 的 Group
        *   建立專案為 private

*   >ldapsearch -h ad0.testritegroup.com -p 389 -b 'CN=zAccount,DC=testritegroup,DC=com' -D 'T2427@testritegroup.com' -x -W
*

*   main: # 'main' is the GitLab 'provider ID' of this LDAP server
*        label: 'LDAP'
*        host: '**ad0.testritegroup.com**'
*        port: 389
*        uid: '**sAMAccountName**'
*        method: 'plain' # "tls" or "ssl" or "plain"
*        bind_dn: '**T2427@testritegroup.com**' # 需要一個查詢 LDAP 的帳號
*        password: '******' # 查詢帳號的密碼
*        active_directory: true
*        allow_username_or_email_login: true
*        base: '**DC=testritegroup,DC=com**'
*        attributes:
*          username: [ 'sAMAccountName']
*          

##  從SVN 移轉舊資料
### 使用 bitbucket 提供的工具 svn-migration-scripts.jar 及方法 https://www.atlassian.com/git/tutorials/migrating-overview/
### Migration 步驟
### 確認環境及準備  
		> java -jar ./svn-migration-scripts.jar verify
### 調整 svn 可以被匯出
#### 啓動 http
#### 調整 http.conf 加入 directory 的部分
### 把作者資料倒出來 (git 需要 email, svn 卻沒有) 
		java -jar ./svn-migration-scripts.jar authors http://tgtpe-admvcs.testritegroup.com/svn/tlw/hht gitexport gitexport > authors.txt

### 調整 authors.txt
### convert 
		> git svn clone --stdlayout --authors-file=authors.txt <svn repo url> <local git repos>
### push to git server  
		> git remote add origin http://T2427@git.testritegroup.com/bs4/tlw-hht.git



## 待辦

*   換 Logo

*   取消建立專案的權限(集中建立)

*   hook 實驗 by Project
*   申請 gitlab domain name

*   調整 email 內的連結
