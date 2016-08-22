# Wordpress 安裝/昇級筆記

**Installation**

1.  Download from wordpress chiness web
2.  Edit httpd.conf

*   CREATE DATABASE `wordpress` CHARACTER SET utf8 COLLATE utf8_general_ci;
*   CREATE USER 'wordpress'@'localhost' IDENTIFIED BY 'w0rdpr1ss';
*   GRANT ALL PRIVILEGES ON wordpress . * TO 'wordpress'@'localhost';
*   FLUSH **PRIVILEGES**;
*

**Configuration**

1.  Get wp-conf.php by visit [](https://localhost/wordpress)[https://localhost/wordpress](https://localhost/wordpress), write wp-conf.php to httpd wordpress folder
2.  Grant the **wp-content** folder wirte privilege for upload image file (好像怪怪的)
3.  Setup User/Pass
4.  要參考附件 Wordpress 之後必做的事

        1.  移除預設連結
    2.  修改 theme Footer
    3.  調整 about 頁面

5.  設定永久固定連結並調整 .htaccess

**手動昇級程序**

1.  下載最新版本的 wordpress
2.  備份 MySQL DB
3.  備份 wordpress 程式目錄，以下三個檔案是不能被新版取代的

        1.  wp-content 目錄(整個目錄)
    2.  wp-config.php
    3.  .htaccess

4.  解壓縮新版的 wordpress
5.  把步驟3的部分 copy 到新的 wordpress 目錄
6.  瀏覽器連結至 [](http://xxxx.xxx.xxx/wp-admin)http://[x](http://wordpress/wp-admin)x[x](http://xx/wp-admin)x[.](http://xxxx/wp-admin)x[x](http://xxxx.x/wp-admin)x[.](http://xxxx.xxx/wp-admin)x[x](http://xxxx.xxx.x/wp-admin)x/wp-admin 執行必要的資料庫昇級
7.  Done!

**Reference**

## Todo:

*   改了文章鏈結模式, 連結就變怪怪的,  要調整 .htaccess (from Wordpress 的文章設定)
*   About Me, About Site 設定
*   Archme 擋 comment spam 的設定(暫時取消, 付費服務)
*   Google Analystic 設定/Google 網站 index
*   Google 站長工具設定及觀察

*   Bing 站長工具設定及觀察