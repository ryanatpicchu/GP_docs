# GP API Documentation
## NOTICES

  * 
  * 

## URL

  * API : url will provide late


## Table of Contents

1. [Auth](#auth)
1. [Exchange](#exchange)


### Auth

認證使用者以取得access token

* **URL**

  * /auth

* **Method:**

  `POST`
  
* **Request:**

  * **JSON Body** 
 
   {"timestamp":1503383341514, "partnerId":"iparking", "partnerIp":"223.27.48.212", "userId":"886936630795"}
   
  * **HASH** 
 
 ```
$message = '{"timestamp":1503383341514, "partnerId":"iparking", "partnerIp":"223.27.48.212", "userId":"886936630795"}';

$secret_key = '<WILL PROVIDE LATER>';

hash_hmac('SHA256',  $message, $secret_key)
  
  ```
 
 
  * **JSON Content:**

    | Field           | Required | Type     | Description                                                      |
    |:----------------|:---------|:---------|:-----------------------------------------------------------------|
    | timestamp       | Yes      | Long     | 發出請求的時間戳，以毫秒為單位的 Epoch time(UTC milliseconds since 1/1/1970) |
    | partnerId       | Yes      | String   | iparking / gogogaie |
    | partnerIp       | Yes      | String   | iparking / gogogaie 發出需求的主機IP 位址 (IPv4 或 IPv6) |
    | userId          | Yes      | String   | iParking 用戶識別碼，暫定是手機號碼 |

* **Success Response:**

  * **Content:**

    | Field           | Required | Type     | Description                                                      |
    |:----------------|:---------|:---------|:-----------------------------------------------------------------|
    | status          | Yes      | String   | 信息回應狀態說明，如果成功會回傳 "success";如果有其他錯誤，會回傳特定的錯誤信息 |
    | statusCode      | Yes      | Int      | <WILL PROVIDE LATER>                                             |
    | accessToken     | Yes      | String   | access token 用於其它api 呼叫 |
    | expiredTime     | Yes      | Long     | token 過期的時間戳，以毫秒為單位的 Epoch time(UTC milliseconds since 1/1/1970) |     


* **Sample Call:**

  ```
  /auth?hash=663187fac4edbcdff62ea239deacc34719305749201267929e
  
  ```
 
### Exchange

用酷幣或記錄於iParking 的"中心化"GP 交換crypto GP。交換成功後，iParking 頁面上的GP 數量會消失，GP數量會在GP App 裡顯示

* **URL**

  * /exchange

* **Method:**

  `POST`
  
* **Request:**

  * **JSON Body** 

  	{"timestamp":1503383341514, "partnerId":"iparking", "partnerIp":"223.27.48.212", "userId":"886936630795", "accessToken":"375e3e418a45494c92bf1e6ec2f7460e", "currency":"酷幣", "tokenAmount":10}
 
 
  * **JSON Content:**

    | Field           | Required | Type     | Description                                                      |
    |:----------------|:---------|:---------|:-----------------------------------------------------------------|
    | timestamp       | Yes      | Long     | 發出請求的時間戳，以毫秒為單位的 Epoch time(UTC milliseconds since 1/1/1970) |
    | partnerId       | Yes      | String   | iparking / gogogaie |
    | partnerIp       | Yes      | String   | iparking / gogogaie 發出需求的主機IP 位址 (IPv4 或 IPv6) |
    | userId          | Yes      | String   | iParking 用戶識別碼，暫定是手機號碼 |
    | accessToken     | Yes      | String   | API識別碼 |
    | currency        | Yes      | String   | GP / 酷幣 |
    | tokenAmount     | Yes      | Int      | GP / 酷幣數量 |
  

* **Success Response:**

  * **Content:**

    | Field           | Required | Type     | Description                                                      |
    |:----------------|:---------|:---------|:-----------------------------------------------------------------|
    | status          | Yes      | String   | 信息回應狀態說明，如果成功會回傳 "success";如果有其他錯誤，會回傳特定的錯誤信息 |
    | statusCode      | Yes      | Int      | <WILL PROVIDE LATER>                                             |
    | exchangedTokenAmount     | Yes      | Int | 兌換之相對應的GP數量 |
    | currency        | Yes      | String   | GP |

* **Sample Call:**

  ```
  /exchange?hash=663187fac4edbcdff62ea239deacc34719305749201267929e
  
  ```