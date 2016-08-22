# Spring Security OAuth2 Study

**解決如何讓 Client 呼叫 API 的權限管理問題 (相對於 Session, 採用 Token)**

*   User Token (自已使用的 token, 提供使用者帳號及密碼)
*   Client Token(自己授權 Client 可以使用的 Token)

**包含 User Approval 的取得 token 流程**

![](https://hackpad-attachments.s3.amazonaws.com/hackpad.com_c7RXuQJbR0Q_p.236988_1435141208174_undefined)

**Auth Server - Spring Servlet Path**

**/authorize 要求 User 認證**

/authorize?client_id={client_id}&redirect_uri={redirect_uri}&response_type={response_type}&scope={scope}

**/token client 向 Auth Server 要 token**

## Test Case 的執行

**Vanilla (最簡單的範例)**

curl -H "Accept: application/json" **my-client-with-secret**:secret@localhost:8080/oauth/token -d grant_type=client_credentials

**Get Test:**

curl -H "Authorization: Bearer 6ac22bbe-eaa6-4f06-9b5b-870575104189" localhost:8080/

**POST Test:**

curl -H "Authorization: Bearer 6ac22bbe-eaa6-4f06-9b5b-870575104189" --data {name:"Eric"} localhost:8080/

**問題:**

1.  **my-client-with-secret 是什麼?**
2.  為什麼不能控制 read/write 的權限

## Resource

*   完整說明的投影片

        *   [](https://speakerdeck.com/dsyer/data-modelling-and-identity-management-with-oauth2)https://speakerdeck.com/dsyer/data-modelling-and-identity-management-with-oauth2