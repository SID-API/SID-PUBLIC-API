# 获取JWT

## 说明

获取Json web token（JWT）和access_token类似，是获取凭证的另一种方式。是调用SourceID业务接口的第一步，相当于创建了一个登录凭证，相关业务API接口都需要依赖于JWT来鉴权调用者身份。因此开发者，在使用业务接口前，要明确JWT的颁发来源，使用正确的JWT。

## 获取token

  **请求方式：** POST（**HTTPS或HTTP**)

  **请求地址：**{domain}/oauth2.0/jwt

  **请求参数包：**

```
{
	"username":xxx,
	"password":xxx
}
```

  **请求参数说明：**

| **参数** | **必须** | **说明**                |
| -------- | -------- | ----------------------- |
| username | 是       | 应用唯一标识，对应appid |
| password | 是       | 应用秘钥，对应security  |


  **返回结果：**

  ```json
  {
      "token": "xxx",
      "expires_in": xxx
  }
  ```

  **参数说明：**

| **参数**   | **说明**   |
| ---------- | ---------- |
| token      | 访问令牌   |
| expires_in | 令牌有效期 |