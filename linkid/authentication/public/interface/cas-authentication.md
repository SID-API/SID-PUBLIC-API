# CAS认证接口

>[用户认证](#1)
>
>[请求验证ticket(CAS3.0)](#2)
>
>[单点登出](#3)

#### 一、用户认证<a id=1></a>

> 应用向SID认证服务器请求认证。
>

**请求⽅式：** GET（**HTTPS或HTTP**）

**请求地址：** http://ljw.sso.rghall.com.cn/login

**请求参数：**

```javascript
请求示例：
http://ljw.sso.rghall.com.cn/login?service=xxx
```

**参数说明：**

| **参数** | **是否必须** | **说明**                               |
| -------- | ------------ | -------------------------------------- |
| service  | 是           | SID要跳转的地址，即SID下发ticket的地址 |

**返回结果：**

无

**参数说明：**

| **参数** | **说明**                                        |
| -------- | ----------------------------------------------- |
| ticket   | 票据。ticket参数在service指向的url里，由SID下发 |



#### 二、请求验证ticket(CAS3.0)<a id=2></a>

> 应用携带SID下发的ticket，请求SID验证ticket的有效性，SID验证成功后返回用户信息。

**请求⽅式：** GET（**HTTPS或HTTP**）

**请求地址：** http://ljw.sso.rghall.com.cn/p3/serviceValidate

**请求参数：**

```javascript
请求示例：
http://ljw.sso.rghall.com.cn/p3/serviceValidate?ticket=xxx&service=xxx
```

**参数说明：**

| **参数** | **是否必须** | **说明**                  |
| -------- | ------------ | ------------------------- |
| ticket   | 是           | SID下发的票据             |
| service  | 是           | 和用户验证中的service相同 |

**返回结果：**

SID返回xml格式的用户信息，如下图：

![tempLogin](cas-authentication.assets/tempLogin.png)

**参数说明：**

| **参数** | **说明**                                                     |
| -------- | ------------------------------------------------------------ |
| 用户信息 | 用户信息为xml格式，包括用户登录名。返回的用户属性可在SID中配置。 |



#### 三、单点登出<a id=3></a>

> 单点登出地址。登陆类型为后端登出，即当TGT超时时，或者用户通过链接访问cas登出地址时，cas服务器直接给应用服务器发送登出请求，以达到登出效果。

**请求⽅式：** GET（**HTTPS或HTTP**）

**请求地址：** http://ljw.sso.rghall.com.cn/logout