# 三元组对外API

三元组对外api描述SID向应用提供的标准接口，以便外部应用调用。标准接口如下：

>[增量获取组织信息](#1)
>
>[增量获取岗位信息](#2)
>
>[增量获取用户信息](#3)
>
>[增量获取三元组关系](#4)



#### 一、增量获取组织信息<a id=1></a>

> 当业务系统需要在SourceId， 增量获取组织信息
>

**请求⽅式：** GET（**HTTPS或HTTP**）

**请求地址：** http://self.xxx.edu.cn/linkid/api/aggregate/keTan/public/findOrganizationsByDate?timestamp={timestamp}

注：https方式类似。

**请求参数：**

```javascript
 http://ljw.sso.rghall.com.cn/linkid/api/aggregate/keTan/public/findOrganizationsByDate?timestamp=1601000903868
```

**参数说明：**

| **参数**  | 类型 | **是否必须** | **说明** |
| --------- | ---- | ------------ | -------- |
| timestamp | long | 是           | 时间戳   |

**返回结果：**

```javascript
//有数据
{
    "errno": 0,
    "error": null,
    "entities": [
        {
            "organizeId": "a",
            "organizeName": "a",
            "parentOrganizeId": "RJXZZZ",
            "independent": false,
            "timestamp": 1603347326598,
            "disabled": false
        },
        {
            "organizeId": "aaaaa",
            "organizeName": "aaa",
            "parentOrganizeId": "",
            "independent": true,
            "timestamp": 1604302576033,
            "disabled": true
        },
        {
            "organizeId": "bbb",
            "organizeName": "bbb",
            "parentOrganizeId": "",
            "independent": true,
            "timestamp": 1604302581061,
            "disabled": true
        }
    ],
    "total": 3
}

//无数据
{
    "errno": 1,
    "error": "没有需要同步的组织数据",
    "entities": null,
    "total": 0
}
```

**参数说明：**

| **参数**         | 类型       | **说明**                        |
| ---------------- | ---------- | ------------------------------- |
| errno            | int        | 返回状态, 0 成功， 1  失败      |
| error            | String     | 返回状态消息                    |
| entities         | 自定义对象 | 自定义对象                      |
| total            | int        | 总记录数                        |
| organizeId       | string     | 部门id                          |
| organizeName     | string     | 部门名称                        |
| parentOrganizeId | string     | 父部门id                        |
| independent      | boolean    | 是否独立，true 没有父部门       |
| disabled         | boolean    | 是否有效，true 有效， false无效 |
| timestamp        | long       | 时间戳                          |



#### 二、增量获取岗位信息<a id=2></a>

> 业务系统调用接口， 增量获取岗位信息

**请求⽅式：** GET（**HTTPS或HTTP**）

**请求地址：** http://self.xxx.edu.cn/linkid/api/aggregate/keTan/public/findPostsByDate?timestamp={timestamp}

注：https方式类似。

**请求参数：**

```javascript
请求示例：
http://ljw.sso.rghall.com.cn/linkid/api/aggregate/keTan/public/findPostsByDate?timestamp=1601000903868
```

**参数说明：**

| **参数**  | 类型 | **是否必须** | **说明** |
| --------- | ---- | ------------ | -------- |
| timestamp | long | 是           | 时间戳   |

**返回结果：**

```javascript
{
    "errno": 0,
    "error": null,
    "entities": [
        {
            "postCode": "88",
            "postName": "测试",
            "formal": false,
            "timestamp": 1603260786072,
            "disabled": false
        },
        {
            "postCode": "61",
            "postName": "在校生",
            "formal": false,
            "timestamp": 1604646910939,
            "disabled": false
        },
        {
            "postCode": "62",
            "postName": "校友",
            "formal": false,
            "timestamp": 1604646926142,
            "disabled": false
        },
        {
            "postCode": "aaa",
            "postName": "aaaa",
            "formal": false,
            "timestamp": 1605099529978,
            "disabled": false
        }
    ],
    "total": 4
}
```

**参数说明：**

| **参数**  | 类型       | **说明**                          |
| --------- | ---------- | --------------------------------- |
| errno     | int        | 返回状态, 0 成功， 1  失败        |
| error     | String     | 返回状态消息                      |
| entities  | 自定义对象 | 返回值为部门id列表                |
| postCode  | string     | 岗位编码                          |
| postName  | string     | 岗位名称                          |
| formal    | boolean    | 是否正式岗位， true 是， false 否 |
| timestamp | long       | 时间戳                            |
| disabled  | boolean    | 是否有效， true有效， false无效   |



#### 三、增量获取用户信息<a id=3></a>

> 查询用户在某个应用匹配的应用角色

**请求⽅式：** GET（**HTTPS或HTTP**）

**请求地址：** http://self.xxx.edu.cn/linkid/api/aggregate/keTan/public/findUsersByDate?timestamp={timestamp}

注：https方式类似。

**请求参数：**

```javascript
示例： http://ljw.sso.rghall.com.cn/linkid/api/aggregate/keTan/public/findUsersByDate?timestamp=1601000903868
```

**参数说明：**

| **参数**  | 类型 | **是否必须** | **说明** |
| --------- | ---- | ------------ | -------- |
| timestamp | long | 是           | 时间戳   |

**返回结果：**

```javascript
{
    "errno": 0,
    "error": null,
    "entities": [
        {
            "account": "00000002",
            "name": "gzx123",
            "email": "null",
            "phone": "13305902541",
            "timestamp": 1601458338487,
            "disabled": true
        },
        {
            "account": "1987121",
            "name": "郭知",
            "email": "null",
            "phone": "13305902541",
            "timestamp": 1602666383817,
            "disabled": true
        }
    ],
    "total": 2
}
```

**参数说明：**

| **参数**  | 类型       | **说明**                        |
| --------- | ---------- | ------------------------------- |
| errno     | int        | 返回状态, 0 成功， 1  失败      |
| error     | String     | 返回状态消息                    |
| entities  | 自定义对象 | 返回值为部门id列表              |
| account   | string     | 学工号                          |
| name      | string     | 姓名                            |
| email     | string     | 邮箱                            |
| phone     | string     | 手机号                          |
| timestamp | long       | 时间戳                          |
| disabled  | boolean    | 是否有效， true有效， false无效 |



#### 四、增量获取三元组关系接口<a id=4></a>

> 查询用户在某个应用匹配的应用角色

**请求⽅式：** GET（**HTTPS或HTTP**）

**请求地址：** http://self.xxx.edu.cn/linkid/api/aggregate/keTan/public/findUserOrganizationPost?timestamp={timestamp}

注：https方式类似。

**请求参数：**

```javascript
示例： http://ljw.sso.rghall.com.cn/linkid/api/aggregate/keTan/public/findUserOrganizationPost?timestamp=1601000903868
```

**参数说明：**

| **参数**  | 类型 | **是否必须** | **说明** |
| --------- | ---- | ------------ | -------- |
| timestamp | long | 是           | 时间戳   |

**返回结果：**

```javascript
{
    "errno": 0,
    "error": null,
    "entities": [
        {
            "account": "vincent",
            "postCode": "10",
            "deptCode": null,
            "userCode": null,
            "timestamp": 1601458338487,
            "disabled": true
        },
        {
            "account": "vincent",
            "postCode": "10",
            "deptCode": null,
            "userCode": null,
            "timestamp": 1602666383817,
            "disabled": true
        }
    ],
    "total": 2
}
```

**参数说明：**

| **参数**  | 类型       | **说明**                        |
| --------- | ---------- | ------------------------------- |
| errno     | int        | 返回状态, 0 成功， 1  失败      |
| error     | String     | 返回状态消息                    |
| entities  | 自定义对象 | 返回值为部门id列表              |
| account   | string     | 学工号                          |
| postCode  | string     | 岗位编码                        |
| deptCode  | string     | 编码编码                        |
| userCode  | 废弃       | 废弃                            |
| timestamp | long       | 时间戳                          |
| disabled  | boolean    | 是否有效， true有效， false无效 |