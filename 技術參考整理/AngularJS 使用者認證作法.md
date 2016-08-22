# AngularJS 使用者認證作法

**應用在 Ionic 的文章**

[](http://devdactic.com/user-auth-angularjs-ionic/)http://devdactic.com/user-auth-angularjs-ionic/

**要點:**

*   建立 AuthService 在 services.js, 提供與認證相關的服務

        *   login() 到 Server 進行認證, 取得 token, 儲存 token
    *   logout()
    *   useCredentials

                *   $http.defaults.headers.common['X-Auth-Token'] = token;

*   挷在 body 的 controller 可以接收到所有的 broadcast event. 透過這個 Event 來提示使用者是否權限不足, 或認證有誤
*   services 裡 return q$() 可以讓 promise 的語法很清楚

        *   var login = function(username, pw){ return $q();}
    *   AuthService.login(username, pw).then()...

**延伸**

*   **AngularJS 的認證應用**

[](https://medium.com/opinionated-angularjs/techniques-for-authentication-in-angularjs-applications-7bbf0346acec)[https://medium.com/opinionated-angularjs/techniques-for-authentication-in-angularjs-applications-7bbf0346acec](https://medium.com/opinionated-angularjs/techniques-for-authentication-in-angularjs-applications-7bbf0346acec)