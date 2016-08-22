# MongoDB with Restheart

安裝及設定

*   mongod --dbpath ~/data/db

可以利用 restheart 來做為 MongoDB 的 REST 服務

## Restheart

1.  JDK 8 Required
2.  start command

        1.  java -server -jar restheart.jar

3.  API Workthrough (using curl)

*   Create Database
**   curl -X PUT  -H "Content-Type:application/json" \
*    "[](http://localhost:8080/myfirstdb)http://localhost:8080/myfirstdb desc='this is my first db'"
**   Create Collections
**    curl -X PUT  -H "Content-Type:application/json" \
*    "[](http://localhost:8080/myfirstdb/assets)http://localhost:8080/myfirstdb/assets desc='Application Asset'"
**   Create data
*    curl -X POST  -H "Content-Type:application/json" \
*    "[](http://localhost:8080/myfirstdb/assets)http://localhost:8080/myfirstdb/assets name='OMS' systemOwner='Eric Yu'"
**    curl -X POST  -H "Content-Type:application/json" \
*    "[](http://localhost:8080/myfirstdb/assets)http://localhost:8080/myfirstdb/assets name='SOM' systemOwner='Pogi Lin'"
**    Get All Data
*     curl -X GET  -H "Content-Type:application/json" \
*    "[](http://localhost:8080/myfirstdb/assets)http://localhost:8080/myfirstdb/assets"
*

## Reference

1.  MongoDB Manual - [](http://docs.mongodb.org/manual/)http://docs.mongodb.org/manual/