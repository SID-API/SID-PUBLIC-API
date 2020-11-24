# 海大在使用的其他API

海大目前还在使用的api， 未标准对外接口如下：

>[查询所有对接的应用](#1)
>
>[查询用户的入口授权](#2)
>
>[重置用户密码](#3)



#### 一、查询所有对接的应用<a id=1></a>

> 海大门户应用获取已对接的应用列表， 展示应用相关信息
>

**请求⽅式：** GET（**HTTPS或HTTP**）

**请求地址：** http://self.xxx.edu.cn/linkid/api/aggregate/app/public/find/clientId/name/all

**请求参数：**

```javascript
请求示例：
https://self.xxx.edu.cn/linkid/api/aggregate/app/public/find/clientId/name/all
```

**返回结果：**

```javascript
{
    "code": 200,
    "message": "OK",
    "data": [
        {
            "clientId": "OC4wNS4wNS4wNy4wMC4wMy4wMS4wMS4w",
            "name": "智慧身份源系统",
            "url": "http://id.ruijie.com.cn",
            "describe": "智慧身份源系统",
            "isDeleted": false
        },
        {
            "clientId": "11111111111111",
            "name": "11111111111111111",
            "url": "http://www.1111111.com",
            "describe": "11111111111111111111111",
            "isDeleted": false
        }
    ]
}
```

**参数说明：**

| **参数**  | 类型       | **说明**                                   |
| --------- | ---------- | ------------------------------------------ |
| code      | int        | 返回状态code                               |
| message   | String     | 返回状态消息                               |
| data      | 自定义对象 | 自定义对象                                 |
| clientId  | string     | 应用的clientId                             |
| name      | string     | 应用名称                                   |
| url       | string     | 应用url                                    |
| describe  | string     | 应用描述                                   |
| isDeleted | boolean    | 是否已删除， true：已删除， false： 未删除 |



#### 二、查询用户有入口授权的应用<a id=2></a>

> 海大查询用户的有入口授权的应用

**请求⽅式：** GET（**HTTPS或HTTP**）

**请求地址：** http://self.xxx.edu.cn/linkid/remote/permission/entrance/public/find/entancePermissions/{userId}

**请求参数：**

```javascript
请求示例：
https://self.xxx.edu.cn/linkid/linkid/remote/permission/entrance/public/find/entancePermissions/admin
```

**返回结果：**

```javascript
{
    "code": 200,
    "message": "OK",
    "data": [
        {
            "clientId": "OC4wNS4wNS4wNy4wMC4wMy4wMS4wMS4w",
            "name": "智慧身份源系统",
            "url": "http://id.ruijie.com.cn",
            "describe": "智慧身份源系统",
            "isDeleted": null
        },
        {
            "clientId": "11111111111111",
            "name": "11111111111111111",
            "url": "http://www.1111111.com",
            "describe": "11111111111111111111111",
            "isDeleted": null
        }
    ]
}

```

**参数说明：**

| **参数**  | 类型       | **说明**       |
| --------- | ---------- | -------------- |
| code      | int        | 返回状态code   |
| message   | String     | 返回状态消息   |
| data      | 自定义对象 | 自定义对象     |
| clientId  | string     | 应用的clientId |
| name      | string     | 应用名称       |
| url       | string     | 应用url        |
| describe  | string     | 应用描述       |
| isDeleted | null       | 无用字段       |



#### 三、重置用户密码<a id=3></a>

> 查询用户在某个应用匹配的应用角色

**请求⽅式：** POST（**HTTPS或HTTP**）

**请求地址：** http://self.xxx.edu.cn/linkid/public/api/user/password/reset

**请求参数：**

```javascript
{
    "propertyNames":[
        "XH",
        "GH"
    ],
    "value":"admin",
    "newPassword":"111111",
    "forceChangePasswordNextLogin":true,
    "source":"a"
}
```

**参数说明：**

| **参数**                     | 类型    | **是否必须** | **说明**                 |
| ---------------------------- | ------- | ------------ | ------------------------ |
| propertyNames                | list    | 是           | 用户名标准对应的字段     |
| value                        | string  | 是           | 用户名                   |
| newPassword                  | string  | 是           | 新密码                   |
| forceChangePasswordNextLogin | boolean | 是           | 是否强制下次登录修改密码 |
| source                       | string  | 是           | 修改密码调用来源         |

**返回结果：**

```javascript
{
  "code": 200,
  "message": "OK",
  "data": true
}

```

**参数说明：**

| **参数** | 类型    | **说明**     |
| -------- | ------- | ------------ |
| code     | int     | 返回状态code |
| message  | String  | 返回状态消息 |
| data     | boolean | 重置密码结果 |

#### 
