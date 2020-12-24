# APP内应用免认证接口
# OAuth2.0标准认证接口
> [获取code](#1)
>
> [通过code换取token](#2)
>
> [通过token换取用户信息](#3)


#### 一、获取code<a id=1></a>

> Sid请求APP获取code的接口
>

**请求⽅式：** GET（**HTTPS或HTTP**）

**请求地址：** https://xxx.com.cn/oauth/authorize

注：https方式类似。

**请求参数：**

```javascript
请求示例：
 https://xxx.com.cn/oauth/authorize?client_id=[AppKey]&redirect_uri=[urlEncode(应用回调地址)]&response_type=code&scope=base_api&state=xxx
```

**参数说明：**

| **参数** | **是否必须** | **说明**                               |
| -------- | ------------ | -------------------------------------- |
| client_id  | 是           | 应用唯一标识，即应用注册时获得的 App Key |
| redirect_uri  | 是           | 授权后重定向的回调链接地址，注意需使用 urlEncode 对链接进行处理 |
| response_type  | 是           | 返回类型，请填写 code 。 |
| scope  | 是           | 作用域，与注册时匹配。 base_api 可以访问基础API且支持静默模式不弹出授权提醒； all 可以使用所有高级API。通过开放平台创建的应用默认授予 base_api 作用域，可申请 all 权限；在微哨管理平台创建的应用同时授予 base_api 和 all 权限。 |
| state  | 是           | 重定向后会带上 state 参数。开发者可以用此参数验证请求有效性，或记录用户请求授权页前的位置。同时此参数可用于防止跨站请求伪造（CSRF）攻击 |

**返回结果：**
因为应用嵌入在APP内部，此时APP应该是登录状态，在一系列校验好，会重定向到redirect_uri并且带着code和state
```javascript
示例：
 https://redirect_uri?code=xxxxx&state=xxx
```

**参数说明：**

| **参数** | **说明**                                        |
| -------- | ----------------------------------------------- |
| code   | 下发的code |
| code   | 请求code时带的参数 |


#### 二、通过 code 换取网页授权 AccessToken<a id=2></a>


**请求⽅式：** POST（**HTTPS或HTTP**）

**请求地址：** http://{server}/oauth/token

注：https方式类似。

**请求参数：**

```javascript
示例：
grant_type=authorization_code&client_id=[AppKey]&client_secret=[AppSecret]&code=[code]&redirect_uri=[urlEncode(应用回调地址)]

```

**参数说明：**

| **参数** | **是否必须** | **说明**                  |
| -------- | ------------ | ------------------------- |
| grant_type   | 是           | 固定值 authorization_code。             |
| client_id  | 是           | 应用唯一标识，即应用注册时获得的 App Key。|
| client_secret   | 是           | 应用密钥，即应用注册时获得的 App Secret。             |
| code  | 是           | 授权票据，即第一步应用回调地址获得的 code 参数值 |
| redirect_uri   | 是           | 应用回调地址             |


**返回结果：**
```json
{
  "access_token": "fDanz0ydkCqVsgSoze7mrCnwJIsN0dL",
  "expires_in": "1209600",
  "scope": "base_api",
  "refresh_token": "HhbiRKzjVnKdvGfmuGjvh3Clm4AIMqV8",
  "token_type": "Bearer"
}
```

**参数说明：**

| **参数** | **说明**                                                     |
| -------- | ------------------------------------------------------------ |
| access_token | 下发的token |
| expires_in | 有效期 |
| scope | 作用域 |


#### 三、获取用户信息<a id=3></a>

> 获取用户信息。

**请求⽅式：** GET（**HTTPS或HTTP**）

**请求地址：** http://{server}/profile?access_token=[AccessToken]

注：https方式类似。


**返回结果：**
```json
{
  "name": "张三",
  "student_number": "zhangsan"
}
```

**参数说明：**

| **参数** | **说明**                                                     |
| -------- | ------------------------------------------------------------ |
| name | 姓名 |
| student_number | 学工号 |

