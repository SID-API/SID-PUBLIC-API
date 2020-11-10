# 用户密码修改对外API

用户密码相关对外的api，描述SID向应用提供的标准接口，以便外部应用调用。标准接口如下：


#### 一、密码相关接口

##### 1、修改密码接口

**请求⽅式：** POST（**HTTPS或HTTP**）

**请求地址：** 

http://{server}/linkid/api/public/password/change

**请求参数：**

```
{
    "idCard": "",
    "newPasswd": "12345aA!",
    "oldPasswd": "12345aA!1",
    "xgh": "20202021"
}
```

**参数说明：**

| **参数**  | 类型   | **是否必须**       | **说明**                     |
| --------- | ------ | ------------------ | ---------------------------- |
| idCard    | String | 与 xgh 任选一个    | 身份证号 |
| newPasswd | String | 是                 | 新密码                       |
| oldPasswd | String | 是                 | 下次登录是否开启强制修改密码 |
| xgh       | String | 与 idCard 任选一个 | 学工号                       |

**返回结果：**

```
{
    "code": 200,
    "message": "OK",
    "data": true
}
```

##### 2、重置密码

**请求⽅式：** POST（**HTTPS或HTTP**）

**请求地址：** 

http://{server}/linkid/api/public/password/reset

**请求参数：**

```
{
     "xgh":"20202021",
     "idCard":"12345aA!",
     "passwd":"18547212068"
}
```

**参数说明：**

| **参数** | 类型   | **是否必须**       | **说明**                     |
| -------- | ------ | ------------------ | ---------------------------- |
| xgh      | string | 与 idCard 任选一个 | 学工号 |
| idCard   | string | 与 xgh 任选一个    | 新密码                       |
| passwd   | string | 是                 | 是否重置为初始密码           |

**返回结果：**

```
{
    "code": 200,
    "message": "OK",
    "data": true
}
```

##### 3、重置为初始密码


**请求⽅式：** POST（**HTTPS或HTTP**）

**请求地址：** 

​	http://{server}/linkid/api/public/password/reset/initial

**请求参数：**


```
{
     "xgh":"20202021",
     "idCard":"12345aA!",
     "passwd":"18547212068"
}
```

**参数说明：**

| **参数** | 类型   | **是否必须**       | **说明**                     |
| -------- | ------ | ------------------ | ---------------------------- |
| xgh      | string | 与 idCard 任选一个 | 学工号 |
| idCard   | string | 与 xgh 任选一个    | 新密码                       |
| passwd   | string | 是                 | 是否重置为初始密码           |

**返回结果：**

```json
{
    "code": 200,
    "message": "OK",
    "data": true
}
```


#### 二、用户名密码认证接口

##### 1、第三方开放登录接口

**请求⽅式：** POST（**HTTPS或HTTP**）

**请求地址：** http://{server}/linkid/api/user/third/login

**请求参数：**

```json
{
  "password": "MTIzNDVhQSE=", //用户密码要用Base64加密
  "userId": "20202021"
}
```

**参数说明：**

| **参数** | 类型   | **是否必须** | **说明** |
| -------- | ------ | ------------ | -------- |
| password | String | 是           | 密码要用Base64加密     |
| userId   | String | 是           | 学工号   |

**返回结果：**

```
{
  "code": 200,
  "message": "OK",
  "data": [
    {
      "propertyValue": "居民身份证",
      "propertyName": "SFZJLXM"
    },
    {
      "propertyValue": "中国",
      "propertyName": "GJ"
    },
    {
      "propertyValue": "",
      "propertyName": "BCH"
    },
    {
      "propertyValue": "20202021",
      "propertyName": "GH"
    }
    ........
  ]
}
```

**返回参数说明：**

| **参数** | 类型   | **说明**     |
| -------- | ------ | ------------ |
| XH       | String | 姓名         |
| XM       | String | 返回状态消息 |

注：更多返回参数信息，请参考标准。

##### 2、验证用户名密码是否正确

**请求⽅式：** POST（**HTTPS或HTTP**）

**请求地址：** http://{server}/linkid/api/user/public/login

**请求参数：**

```json
{
   "password": "12345aA7",
    "propertyNames": [
      "GH","XH"
    ],
    "value": "20202021"
}
```

**参数说明：**

| **参数**      | 类型   | **是否必须** | **说明**                 |
| ------------- | ------ | ------------ | ------------------------ |
| password      | String | 是           | 密码                     |
| propertyNames | list   | 是           | 根据学工号登录时的固定格 |
| value         | String | 是           | 学工号                   |

**返回结果：**

```json
{
  "code": 200,
  "message": "OK",
  "data": [
    {
      "propertyValue": "居民身份证",
      "propertyName": "SFZJLXM"
    },
    {
      "propertyValue": "中国",
      "propertyName": "GJ"
    },
    {
      "propertyValue": "",
      "propertyName": "BCH"
    },
    {
      "propertyValue": "20202021",
      "propertyName": "GH"
    },
    {
      "propertyValue": "1931-12-03",
      "propertyName": "CSRQ"
    },
    .......
  ]
}
```

**返回参数说明：**

| **参数** | 类型   | **说明**     |
| -------- | ------ | ------------ |
| XH       | String | 姓名         |
| XM       | String | 返回状态消息 |

注：更多返回参数信息，请参考标准。