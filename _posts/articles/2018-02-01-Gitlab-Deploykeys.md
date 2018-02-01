---
layout: post
title: Gitlab Deploy Key 的設定
excerpt: "在佈署系統時, 會有需要取得 git repository source code, 但在不同的佈署人員之間去執行 git pull 會需要在不同帳號間切換，是很麻煩的事。加上若有 CI 自動化的需求時，也不能使用特定人員的帳號及密碼。"
categories: articles
tags: [gitlab, git]
comments: true
---

# Gitlab Deploy Key 的設定

在佈署系統時, 會有需要取得 git repository source code, 但在不同的佈署人員之間去執行 git pull 會需要在不同帳號間切換，是很麻煩的事。加上若有 CI 自動化的需求時，也不能使用特定人員的帳號及密碼。

使用 deploy key 來配置這個佈署的角色，它不需要密碼即可進行 git pull。因為不需要密碼，又需要在安全性的考量下，必需在 gitlab 的 repository 上去配置一個 ssh key 來信任欲進行佈署的機器。 每一部機器都要配置一個 deploy key。

# 建立 Deploy key 的步驟

1. 在被信任的機器上建立 id_rsa.pub，先登入要執行 git pull 的機器
```bash
   > ssh-keygen -t rsa -C "user@yourcompany.com" -b 4096
   Generating public/private rsa key pair.
   Enter file in which to save the key (/home/admin/.ssh/id_rsa):  <直接按 Enter 儲存於提示的路徑>
   Enter passphrase (empty for no passphrase): <直接按 Enter 可以不設定密碼>
   Enter same passphrase again:
   Your identification has been saved in /home/admin/.ssh/id_rsa.
   Your public key has been saved in /home/admin/.ssh/id_rsa.pub.
   The key fingerprint is:
   5b:92:72:4e:5d:c5:66:ce:74:cc:d6:c7:0a:9b:68:38 user@yourcompany.com
   The key's randomart image is:
   +--[ RSA 4096]----+
   |             ..+.|
   |            ..= O|
   |         . ..X +.|
   |        Eoo.o +  |
   |      . Soo      |
   |       = +       |
   |        o        |
   |                 |
   |                 |
   +-----------------+
```

2. 在 gitlab 上面的 repositoy 建立 deploy key
   1. 在 gitlab 的 repository 裡找到 deploy keys 的設定頁面
   2. 為 deploy key 取一個 title 來辨識任信的機器
   3. 取得 id_rsa.pub 的內容後，將該內容貼到 key 這個欄位裡
   4. 按下新增即可

3. 調整 deploy machine (要執行 git pull/git clone 的機器)上的配置
   1. git clone 使用 ssh 的 URL (eg: git@**yourdomain**:**owner/yourRepository.git**) 進行 clone 就可以了
   2. 若原來的專案已經存在，可以透過調整 .git/config 裡的 remote origin url 來調整

# 參考資料:
   * https://docs.gitlab.com/ce/ssh/README.html