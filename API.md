# GP API Documentation
## NOTICES

  * 當酷幣要兌換成GP，或是遊戲勝利結算後匯出GP，GP 會直接上鏈，記錄於區塊鏈

## URL

  * API : url will provide later

## Table of Contents

1. [Auth](#auth)
1. [Exchange](#exchange)
1. [Balance](#balance)
1. [Status](#status)


### Auth

認證使用者以取得access token

* **URL**

  * /auth

* **Method:**

  `POST`
  
* **Request:**

  * **JSON Body** 
 
   {"timestamp":1503383341514, "partnerId":"iparking", "userId":"66668888", "userType":"business"}
   
  * **HASH** 
 
 ```
$message = '{"timestamp":1503383341514, "partnerId":"iparking", "userId":"66668888", "userType":"business"}';

$secret_key = '<WILL PROVIDE LATER>';

hash_hmac('SHA256',  $message, $secret_key)
  
  ```
 
 
  * **JSON Content:**

    | Field           | Required | Type     | Description                                                      |
    |:----------------|:---------|:---------|:-----------------------------------------------------------------|
    | timestamp       | Yes      | Long     | 發出請求的時間戳，以毫秒為單位的 Epoch time(UTC milliseconds since 1/1/1970) |
    | partnerId       | Yes      | String   | iparking / gogogaie |
    | userId          | Yes      | String   | iParking 用戶識別碼，一般用戶是手機號碼，企業用戶為統編 |
    | userType        | Yes      | String   | 用戶類別：business/normal |

* **Success Response:**

  * **Content:**

    | Field           | Required | Type     | Description                                                      |
    |:----------------|:---------|:---------|:-----------------------------------------------------------------|
    | status          | Yes      | String   | 信息回應狀態說明，如果成功會回傳 "success";如果有其他錯誤，會回傳特定的錯誤信息 |
    | statusCode      | Yes      | Int      | 0:成功，1:失敗 |
    | accessToken     | Yes      | String   | access token 用於其它api 呼叫 |
    | expiredTime     | Yes      | Long     | token 過期的時間戳，以毫秒為單位的 Epoch time(UTC milliseconds since 1/1/1970) |     


* **Sample Call:**

  ```
  /auth?hash=663187fac4edbcdff62ea239deacc34719305749201267929e
  
  ```
 
### Exchange

用酷幣交換crypto GP。交換成功後，iParking 頁面上的GP 數量會增加

* **URL**

  * /exchange

* **Method:**

  `POST`
  
* **Request:**

  * **JSON Body** 

  	{"timestamp":1503383341514, "partnerId":"iparking", "userId":"66668888", "accessToken":"375e3e418a45494c92bf1e6ec2f7460e", "currency":"GCoin", "tokenAmount":10}
 
 
  * **JSON Content:**

    | Field           | Required | Type     | Description                                                      |
    |:----------------|:---------|:---------|:-----------------------------------------------------------------|
    | timestamp       | Yes      | Long     | 發出請求的時間戳，以毫秒為單位的 Epoch time(UTC milliseconds since 1/1/1970) |
    | partnerId       | Yes      | String   | iparking / gogogaie |
    | userId          | Yes      | String   | iParking 用戶識別碼，一般用戶是手機號碼，企業用戶為統編 |
    | userType        | Yes      | String   | 用戶類別：business/normal |
    | accessToken     | Yes      | String   | API識別碼 |
    | currency        | Yes      | String   | GCoin （酷幣）|
    | tokenAmount     | Yes      | Int      | 欲兌換之GCoin (酷幣) 數量 |
  

* **Success Response:**

  * **Content:**

    | Field           | Required | Type     | Description                                                      |
    |:----------------|:---------|:---------|:-----------------------------------------------------------------|
    | status          | Yes      | String   | 信息回應狀態說明，如果成功會回傳 "success";如果有其他錯誤，會回傳特定的錯誤信息 |
    | statusCode      | Yes      | Int      |  |
    | exchangedTokenAmount     | Yes      | Int | 兌換之相對應的GP數量 |
    | currency        | Yes      | String   | GP |
    | transactionID   | Yes      | Int   |  |

* **Sample Call:**

  ```
  /exchange?hash=663187fac4edbcdff62ea239deacc34719305749201267929e
  
  ```


### Balance

顯示目前用戶錢包的GP數量

* **URL**

  * /balance

* **Method:**

  `POST`
  
* **Request:**

  * **JSON Body** 

    {"timestamp":1503383341514, "partnerId":"iparking", "userId":"886936630795", "accessToken":"375e3e418a45494c92bf1e6ec2f7460e"}
 
 
  * **JSON Content:**

    | Field           | Required | Type     | Description                                                      |
    |:----------------|:---------|:---------|:-----------------------------------------------------------------|
    | timestamp       | Yes      | Long     | 發出請求的時間戳，以毫秒為單位的 Epoch time(UTC milliseconds since 1/1/1970) |
    | partnerId       | Yes      | String   | iparking / gogogaie |
    | userId          | Yes      | String   | iParking 用戶識別碼，暫定是手機號碼 |
    | accessToken     | Yes      | String   | API識別碼 |
    

* **Success Response:**

  * **Content:**

    | Field           | Required | Type     | Description                                                      |
    |:----------------|:---------|:---------|:-----------------------------------------------------------------|
    | status          | Yes      | String   | 信息回應狀態說明，如果成功會回傳 "success";如果有其他錯誤，會回傳特定的錯誤信息 |
    | statusCode      | Yes      | Int      |  |
    | amount          | Yes      | Int | GP數量 |

* **Sample Call:**

  ```
  /balance?hash=663187fac4edbcdff62ea239deacc34719305749201267929e
  
  ```

### Status

查詢交易狀態

* **URL**

  * /status

* **Method:**

  `POST`
  
* **Request:**

  * **JSON Body** 

    {"timestamp":1503383341514, "partnerId":"iparking", "userId":"886936630795", "txId":"2", "accessToken":"375e3e418a45494c92bf1e6ec2f7460e"}
 
 
  * **JSON Content:**

    | Field           | Required | Type     | Description                                                      |
    |:----------------|:---------|:---------|:-----------------------------------------------------------------|
    | timestamp       | Yes      | Long     | 發出請求的時間戳，以毫秒為單位的 Epoch time(UTC milliseconds since 1/1/1970) |
    | partnerId       | Yes      | String   | iparking / gogogaie |
    | userId          | Yes      | String   | iParking 用戶識別碼，暫定是手機號碼 |
    | txId            | Yes      | String   | 用以查詢交易狀態的唯一值。於exchange 時獲取 |
    | accessToken     | Yes      | String   | API識別碼 |
    

* **Success Response:**

  * **Content:**

    | Field           | Required | Type     | Description                                                      |
    |:----------------|:---------|:---------|:-----------------------------------------------------------------|
    | status          | Yes      | String   | 信息回應狀態說明，如果成功會回傳 "success";如果有其他錯誤，會回傳特定的錯誤信息 |
    | statusCode      | Yes      | Int      |  |
    | txStatus        | Yes      | String   | pending / procesing / success /  |

* **Sample Call:**

  ```
  /status?hash=663187fac4edbcdff62ea239deacc34719305749201267929e
  
  ```