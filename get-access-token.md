# 获取access_token

## 说明

获取access_token是调用SourceID业务接口的第一步，相当于创建了一个登录凭证，相关业务API接口都需要依赖于access_token来鉴权调用者身份。因此开发者，在使用业务接口前，要明确access_token的颁发来源，使用正确的access_token。

## 获取token

  **请求方式：** GET（**HTTPS或HTTP**)

  **请求地址：**http://xxx.cdu.edu.cn/oauth2.0/accessToken?grant_type=client_credentials&client_id=xxx&client_secret=xxx

  **请求参数包：**

  无

  **请求参数说明：**

| **参数**      | **必须** | **说明**                                 |
| ------------- | -------- | ---------------------------------------- |
| grant_type    | 是       | 客户端模式，这里固定为client_credentials |
| client_id     | 是       | 应用账号                                 |
| client_secret | 是       | 应用密钥                                 |
| scope         | 否       | 权限列表，以空格分隔，空为默认           |


  **返回结果：**

  ```json
  {
      "access_token": "AT-1-IWyhZhU1hKKvWPddAJpdHRN2ECu08Ypo",
      "token_type": "bearer",
      "expires_in": 28800,
      "refresh_token": "RT-1-cvHg23sAYRfu-1h8e57U9PSGK1qyL-mW"
  }
  ```

  **参数说明：**

| **参数**      | **说明**   |
| ------------- | ---------- |
| access_token  | 访问令牌   |
| token_type    | 令牌类型   |
| expires_in    | 令牌有效期 |
| refresh_token | 令牌有效期 |