# 利用 convert 轉圖 Thumbnail

*   **把資料合併到 curadb.cuwalk_members**

*   select m.user_id, m.email, c.email, c.memberImage from cuwalk.member c, curadb.members m where CONVERT(m.email USING utf8) = CONVERT(m.email USING utf8) into outfile '~/userimages.txt';

*   **建立目錄，放到對的目錄並更名**

*   mkdir  59 ; mv 1392177969.jpg   59/MyPic-59.jpg

*   **Convert 批次轉 Thumbnail (切中間最大張)**

*   convert    59/MyPic-59.jpg  -set option:distort:viewport "%[fx:min(w,h)]x%[fx:min(w,h)]+%[fx:max((w-h)/2,0)]+%[fx:max((h-w)/2,0)]"  -filter point -distort SRT 0  +repage -thumbnail 10000@   59/MyPic-59_100x100.jpg           
*

[](http://www.happycloud.com.tw/cuwalk/image/user/)http://www.happycloud.com.tw/cuwalk/image/user/

mkdir  63 ; mv 1389080324.jpg   63/MyPic-63.jpg

mkdir  65 ; mv 1388385448.jpg   65/MyPic-65.jpg

mkdir  66 ; mv 1388393370.jpg   66/MyPic-66.jpg

mkdir  67 ; mv 1389154307.jpg   67/MyPic-67.jpg

mkdir  68 ; mv 1388457236.jpg   68/MyPic-68.jpg

mkdir  71 ; mv 1388743727.jpg   71/MyPic-71.jpg

mkdir  72 ; mv 1388990104.jpg   72/MyPic-72.jpg

mkdir  73 ; mv 1389006469.jpg   73/MyPic-73.jpg

mkdir  74 ; mv 1389064877.jpg   74/MyPic-74.jpg

mkdir  76 ; mv 1390555070.jpg   76/MyPic-76.jpg

mkdir  10 ; mv 1389371616.jpg   10/MyPic-10.jpg

mkdir  79 ; mv 1389258676.jpg   79/MyPic-79.jpg

mkdir  80 ; mv 1389179489.jpg   80/MyPic-80.jpg

mkdir  81 ; mv 1392362264.jpg   81/MyPic-81.jpg

mkdir  84 ; mv 1389261558.jpg   84/MyPic-84.jpg

mkdir  85 ; mv 1389264492.jpg   85/MyPic-85.jpg

mkdir  86 ; mv 1389346453.jpg   86/MyPic-86.jpg

mkdir  87 ; mv 1389351948.jpg   87/MyPic-87.jpg

mkdir  17 ; mv 1392784297.jpg   17/MyPic-17.jpg

mkdir  97 ; mv 1389932350.jpg   97/MyPic-97.jpg

mkdir  98 ; mv 1389932968.jpg   98/MyPic-98.jpg

mkdir 106 ; mv 1390285563.jpg  106/MyPic-106.jpg

mkdir 108 ; mv 1390291170.jpg  108/MyPic-108.jpg

mkdir 109 ; mv 1390292341.jpg  109/MyPic-109.jpg

mkdir 110 ; mv 1390292954.jpg  110/MyPic-110.jpg

mkdir 112 ; mv 1390376642.jpg  112/MyPic-112.jpg

mkdir 113 ; mv 1390380500.jpg  113/MyPic-113.jpg

mkdir 114 ; mv 1390381615.jpg  114/MyPic-114.jpg

mkdir 117 ; mv 1392647313.jpg  117/MyPic-117.jpg

mkdir 122 ; mv 1390962792.jpg  122/MyPic-122.jpg

mkdir 126 ; mv 1391182920.jpg  126/MyPic-126.jpg

mkdir 127 ; mv 1392690063.jpg  127/MyPic-127.jpg

mkdir 128 ; mv 1391223235.jpg  128/MyPic-128.jpg

mkdir 129 ; mv 1391352554.jpg  129/MyPic-129.jpg

mkdir 132 ; mv 1392618381.jpg  132/MyPic-132.jpg

mkdir 134 ; mv 1392363190.jpg  134/MyPic-134.jpg

mkdir 136 ; mv 1392620678.jpg  136/MyPic-136.jpg

mkdir 138 ; mv 1393161172.jpg  138/MyPic-138.jpg

mkdir 139 ; mv 1393917145.jpg  139/MyPic-139.jpg