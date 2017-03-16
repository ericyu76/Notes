---
layout: post
title: Gitlab 安裝及設定
excerpt: "Gitlab 與 LDAP 整合及配置"
categories: articles
tags: [git, gitlab, technical, ldap]
comments: true
date: 2016-10-22T14:00:55+08:00
---
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

```bash
ldapsearch -h ad0.companyname.com -p 389 -b 'CN=zAccount,DC=companyname,DC=com' -D 'eric.yu@companyname.com' -x -W
```

```yaml
  main: # 'main' is the GitLab 'provider ID' of this LDAP server
       label: 'LDAP'
       host: '**ad0.companyname.com**'
       port: 389
       uid: '**sAMAccountName**'
       method: 'plain' # "tls" or "ssl" or "plain"
       bind_dn: '**eric.yu@companyname.com**' # 需要一個查詢 LDAP 的帳號
       password: '******' # 查詢帳號的密碼
       active_directory: true
       allow_username_or_email_login: true
       base: '**DC=companyname,DC=com**'
       attributes:
         username: [ 'sAMAccountName']
```         

##  從SVN 移轉舊資料
### 使用 bitbucket 提供的工具 svn-migration-scripts.jar 及方法 https://www.atlassian.com/git/tutorials/migrating-overview/
### Migration 步驟
### 確認環境及準備  
		> java -jar ./svn-migration-scripts.jar verify
### 調整 svn 可以被匯出
#### 啓動 http
#### 調整 http.conf 加入 directory 的部分
### 把作者資料倒出來 (git 需要 email, svn 卻沒有) 
		java -jar ./svn-migration-scripts.jar authors http://www.xxx.com/svn/repo gitexport gitexport > authors.txt

### 調整 authors.txt
### convert 
		> git svn clone --stdlayout --authors-file=authors.txt <svn repo url> <local git repos>
### push to git server  
		> git remote add origin http://eric.yu@git.xxx.com/xxx/xxx-hht.git


## 設定 https

### 幾個要點
- 調整 /etc/gitlab/gitlab.rb 檔案如下面的檔案
- 執行 gitlab-ctl reconfigure

```ruby
external_url 'https://git.example.com'  #要把 http 改為 https 整個才會生效

gitlab_rails['gitlab_https'] = true
gitlab_rails['gitlab_port'] = 443

nginx['enable'] = true
nginx['redirect_http_to_https'] = ture
nginx['ssl_certificate'] = "/etc/gitlab/ssl/git.pem" #申請的 SSL Certificate
nginx['ssl_certificate_key'] = "/etc/gitlab/ssl/server.key"
```

## 備份
有二份內容要備份

1. Configuration, gitlab 的設定檔及一些密鑰
2. Application Data, postgres db 及 git bare 資訊

- Configuration, 檔案內容都在 /etc/gitlab 裡, 
```bash
umask 0077; tar -cf /var/opt/gitlab/backups/$(date "+etc-gitlab-%s.tar") -C / etc/gitlab
```
- Application Data 
    1. 設定備份的路徑可以是 mount 遠端的目錄 (/etc/gitlab/gitlab.rb)
       
       ```ini
       gitlab_rails['backup_path'] = /var/opt/gitlab/backups
       ```
    2. 調整保存的日期，單位為秒 172800 為 2 天
       
       ```ini
       gitlab_rails['backup_keep_time'] = 172800
       ```
    3. 設定 cron


## 待辦

*   換 Logo

*   取消建立專案的權限(集中建立)

*   hook 實驗 by Project
*   申請 gitlab domain name

*   調整 email 內的連結
