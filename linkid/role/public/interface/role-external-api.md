# 角色对外API

角色对外api描述SID向应用提供的标准接口，以便外部应用调用。标准接口如下：

>[创建应用角色接口](#1)
>
>[查询应用生成的角色](#2)
>
>[查询用户在某个应用匹配的应用角色](#3)
>
>[查询用户在所有应用匹配的应用角色](#4)



#### 一、创建应用角色接口<a id=1></a>

> 当业务系统需要在SourceId创建应用角色时调用
>

**请求⽅式：** POST（**HTTPS或HTTP**）

**请求地址：** http://self.xxx.edu.cn/linkid/public/api/aggregate/app/remote/role/create

**请求参数：**

```javascript
{
  "roleName":"应用生成的角色名称", 
  "roleCode":"应用生成的角色编号", 
  "roleDescriber":"应用生成的角色的描述" 
}
```

**参数说明：**

| **参数**      | 类型   | **是否必须** | **说明**             |
| ------------- | ------ | ------------ | -------------------- |
| roleName      | string | 是           | 应用生成的角色名称   |
| roleCode      | string | 是           | 应用生成的角色编号   |
| roleDescriber | string | 否           | 应用生成的角色的描述 |

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
| data     | boolean | 保存结果     |



#### 二、查询应用生成的角色<a id=2></a>

> 业务系统调用接口， 查询应用系统关联的角色

**请求⽅式：** GET（**HTTPS或HTTP**）

**请求地址：** http://self.xxx.edu.cn/linkid/public/api/aggregate/app/remote/role/find

**请求参数：**

```javascript
请求示例：
https://self.xxx.edu.cn/linkid/api/aggregate/app/remote/role/find
```

**返回结果：**

```javascript
{
  "code": 200,
  "message": "OK",
  "data": [
    {
      "id": "应用角色ID",
      "appId": "应用系统的ID",
      "roleName": "应用角色名称",
      "roleCode": "应用角色编号",
      "roleDescriber": "应用角色描述"
    }
  ]
}


```

**参数说明：**

| **参数**      | 类型       | **说明**           |
| ------------- | ---------- | ------------------ |
| code          | int        | 返回状态code       |
| message       | String     | 返回状态消息       |
| data          | 自定义对象 | 返回值为部门id列表 |
| id            | string     | 应用角色ID         |
| appId         | string     | 应用系统的ID       |
| roleName      | string     | 应用角色名称       |
| roleCode      | string     | 应用角色编号       |
| roleDescriber | string     | 应用角色描述       |



#### 三、查询用户在某个应用匹配的应用角色<a id=3></a>

> 查询用户在某个应用匹配的应用角色

**请求⽅式：** GET（**HTTPS或HTTP**）

**请求地址：** http://self.xxx.edu.cn/linkid/api/public/aggregate/app/remote/role/find/user/{userId}

**请求参数：**

```javascript
示例：http://self.xxx.edu.cn/linkid/api/aggregate/app/remote/role/find/user/12345
```

**参数说明：**

| **参数** | 类型   | **是否必须** | **说明** |
| -------- | ------ | ------------ | -------- |
| userId   | string | 是           | 学工号   |

**返回结果：**

```javascript
{
  "code": 200,
  "message": "OK",
  "data": [
    {
      "id": "应用角色ID",
      "appId": "应用系统的ID",
      "roleName": "应用角色名称",
      "roleCode": "应用角色编号",
      "roleDescriber": "应用角色描述"
    }
  ]
}

```

**参数说明：**

| **参数**      | 类型       | **说明**           |
| ------------- | ---------- | ------------------ |
| code          | int        | 返回状态code       |
| message       | String     | 返回状态消息       |
| data          | 自定义对象 | 返回值为部门id列表 |
| id            | string     | 应用角色ID         |
| appId         | string     | 应用系统的ID       |
| roleName      | string     | 应用角色名称       |
| roleCode      | string     | 应用角色编号       |
| roleDescriber | string     | 应用角色描述       |

#### 四、查询用户在所有应用匹配的应用角色<a id=4></a>

> 查询用户在某个应用匹配的应用角色

**请求⽅式：** GET（**HTTPS或HTTP**）

**请求地址：** http://self.xxx.edu.cn/linkid/api/aggregate/app/remote/public/role/find/user/{userId}

**请求参数：**

```javascript
示例： http://self.xxx.edu.cn//linkid/api/aggregate/app/remote/public/role/find/user/12345
```

**参数说明：**

| **参数** | 类型   | **是否必须** | **说明** |
| -------- | ------ | ------------ | -------- |
| userId   | string | 是           | 学工号   |

**返回结果：**

```javascript
{
  "code": 200,
  "message": "OK",
  "data": [
    {
      "id": "应用角色ID",
      "appId": "应用系统的ID",
      "roleName": "应用角色名称",
      "roleCode": "应用角色编号",
      "roleDescriber": "应用角色描述"
    }
  ]
}

```

**参数说明：**

| **参数**      | 类型       | **说明**           |
| ------------- | ---------- | ------------------ |
| code          | int        | 返回状态code       |
| message       | String     | 返回状态消息       |
| data          | 自定义对象 | 返回值为部门id列表 |
| id            | string     | 应用角色ID         |
| appId         | string     | 应用系统的ID       |
| roleName      | string     | 应用角色名称       |
| roleCode      | string     | 应用角色编号       |
| roleDescriber | string     | 应用角色描述       |