# 用户信息对外API

用户信息对外api描述SID向应用提供的标准接口，以便外部应用调用。标准接口如下：

>[根据学工号获取身份平台用户信息](#1)
>
>[用户同步](#2)
>
>[微哨在用接口-应用同步用户信息](#3)
>
>[微哨在用接口-根据学工号查询用户信息](#4)
>
>[微哨在用接口-增量同步用户](#5)
>
>[海大科探在用接口-增量同步用户](#6)
>
>[海大再用接口-分页获取标签下的用户](#7)



#### 一、根据学工号获取身份平台用户信息<a id=1></a>

> 根据学工号获取身份平台用户信息

**请求⽅式：** GET（**HTTPS或HTTP**）

**请求地址：** http://self.xxx.edu.cn/linkid/api/aggregate/user/public/userInfo/{userId}

**请求参数：**

```javascript
userId:  学工号
```

**参数说明：**

| **参数** | 类型   | **是否必须** | **说明**     |
| -------- | ------ | ------------ | ------------ |
| userId   | String | 是           | 用户的学工号 |

**返回结果：**

```javascript
{
    "code": 200,
    "message": "OK",
    "data": {
        "XH": "2220184875",
        "XM": "张4875",
        "IDCARD": "3454566531",
        "BJM": "0",
        "SZBH": "433898",
        "ZZMM": "共青团员",
        "KLMC": "理工类",
        "CSD": "湖北",
        "objectId": "5d1c52e1ee25e001c51a1da5",
        "XSDQZTM": "导入待生效",
        "CSRQ": "2000-09-01",
        "SFZJLX": "居民身份证",
        "XB": "女性",
        "SZDW": ["201000"],
        "MZ": "汉族",
        "LASTCHANGEPASSWORDTIME": "2019-07-02T16:00:00.000+0000"
    }
}

```

**参数说明：**

| **参数**               | 类型       | **说明**                             |
| ---------------------- | ---------- | ------------------------------------ |
| code                   | int        | 返回状态code                         |
| message                | String     | 返回状态消息                         |
| data                   | 自定义对象 | 返回值的自定义对象                   |
| XH                     | String     | 学号， 用户为学生时返回， 教工不返回 |
| GH                     | String     | 工号， 用户为教工时返回， 学生不返回 |
| XM                     | String     | 姓名                                 |
| SFLBDM                 | String     | 参照学校真实“标准”配置               |
| LASTCHANGEPASSWORDTIME | Double     | 上次修改密码时间                     |
| 更多返回信息           |            | 更多返回信息含义，请查看标准         |



#### 二、用户同步<a id=2></a>

> 当业务系统需要某个部门、班级的全部用户信息时，可以通过API同步身份平台的相关用户信息。

**请求⽅式：** POST（**HTTPS或HTTP**）

**请求地址：** http://self.xxx.edu.cn/linkid/api/aggregate/user/public/pageQueryUsers

**请求参数：**

```javascript
{
 "currentPage": 1,
 "pageSize": 10
}
```

**参数说明：**

| **参数**    | 类型 | **是否必须** | **说明**       |
| ----------- | ---- | ------------ | -------------- |
| currentPage | int  | 是           | 当前页         |
| pageSize    | int  | 是           | 每页返回记录数 |

**返回结果：**

```javascript
{
    "code": 200,
    "message": "OK",
    "data": {
               "userList": [{
                   "XH": "2220184875",
        		   "XM": "张4875",
                   "IDCARD": "3454566531",
                   "BJM": "0",
                   "SZBH": "433898",
                   "ZZMM": "共青团员",
                   "KLMC": "理工类",
                   "CSD": "湖北",
                   "objectId": "5d1c52e1ee25e001c51a1da5",
                   "XSDQZTM": "导入待生效",
                   "CSRQ": "2000-09-01",
                   "SFZJLX": "居民身份证",
                   "XB": "女性",
                   "SZDW": ["201000"],
                   "MZ": "汉族",
                   "LASTCHANGEPASSWORDTIME": "2019-07-02T16:00:00.000+0000"
                   }
        ],
        "currentPage": 1,
        "pageSize": 10,
        "aggregatePageSortDtos": null,
        "totalPages": 9,
        "totalAmount": 89
    }
}


```

**参数说明：**

| **参数**     | 类型       | **说明**                                                     |
| ------------ | ---------- | ------------------------------------------------------------ |
| code         | int        | 返回状态code                                                 |
| message      | String     | 返回状态消息                                                 |
| data         | 自定义对象 | 返回值的自定义对象                                           |
| currentPage  | int        | 当前页                                                       |
| pageSize     | int        | 每页返回记录数                                               |
| totalPages   | int        | 总页数                                                       |
| totalAmount  | int        | 总记录数                                                     |
| userList     | List       | 用户信息列表， 用户信息返回参考 [根据学工号获取身份平台用户信息接口](#1) |
| 更多返回信息 |            | 更多返回信息含义，请查看标准                                 |



#### 三、微哨在用接口-应用同步用户信息<a id=3></a>

> 微哨通过配置认证api返回的属性， 获取对应的用户信息。

**请求⽅式：** POST（**HTTPS或HTTP**）

**请求地址：** http://self.xxx.edu.cn/linkid/service/user/applicationconfig/userinfo

**请求参数：**

```javascript
{
    "usertype":"02",
    "currentPage":0,
    "pageSize":10
}
```

**参数说明：**

| **参数**    | 类型   | **是否必须** | **说明**                                                     |
| ----------- | ------ | ------------ | ------------------------------------------------------------ |
| currentPage | int    | 是           | 当前页                                                       |
| pageSize    | int    | 是           | 每页返回记录数                                               |
| usertype    | string | 是           | 人员类型， 默认：教职工01、本科生02、研究生03、临时人员05， 实际以学校现场配置位置 |

**返回结果：**

```javascript
{
    "code": 200,
    "message": "OK",
    "data": {
        "totalAmount": 1,
        "userPropertyNameValueDtos": [
            [
                {
                    "propertyValue": "女性",
                    "propertyName": "XB"
                },
                {
                    "propertyValue": "中国",
                    "propertyName": "GJ"
                },
                {
                    "propertyValue": "888888888888888888",
                    "propertyName": "IDCARD"
                },
                {
                    "propertyValue": "",
                    "propertyName": "SFZJYXQ"
                },
                {
                    "propertyValue": "1986-12-01",
                    "propertyName": "CSRQ"
                },
                {
                    "propertyValue": "叶雪雪",
                    "propertyName": "XM"
                },
                {
                    "propertyValue": "",
                    "propertyName": "XMPY"
                },
                {
                    "propertyValue": "",
                    "propertyName": "CYM"
                },
                {
                    "propertyValue": "中国共产党党员",
                    "propertyName": "ZZMM"
                },
                {
                    "propertyValue": "1567111106",
                    "propertyName": "XH"
                },
                {
                    "propertyValue": "02",
                    "propertyName": "SFLBDM"
                },
                {
                    "propertyValue": "汉族",
                    "propertyName": "MZ"
                },
                {
                    "propertyName": "EMAIL"
                }
            ]
        ]
    }
}

```

**参数说明：**

| **参数**                  | 类型       | **说明**                  |
| ------------------------- | ---------- | ------------------------- |
| code                      | int        | 返回状态code              |
| message                   | String     | 返回状态消息              |
| data                      | 自定义对象 | 返回值的自定义对象        |
| totalAmount               | int        | 总记录数                  |
| userPropertyNameValueDtos | List       | 用户信息列表              |
| propertyName              | string     | 用户属性名称              |
| propertyValue             | object     | 用户属性的值              |
| 更多用户属性              |            | 更多用户属性， 请查看标准 |



#### 四、微哨在用接口-根据学工号查询用户信息<a id=4></a>

> 微哨通过配置认证api返回的属性， 获取对应的用户信息。

**请求⽅式：** POST（**HTTPS或HTTP**）

**请求地址：** http://self.xxx.edu.cn/linkid/api/user/public/userinfo/bypropertynames

**请求参数：**

```javascript
{
    "propertyNames":[
        "GH",
        "XH"
    ],
    "value":"1"
}
```

**参数说明：**

| **参数**      | 类型   | **是否必须** | **说明**                                |
| ------------- | ------ | ------------ | --------------------------------------- |
| propertyNames | list   | 是           | 用户属性的名称， 根据学工号查询传GH和XH |
| value         | string | 是           | 用户属性的值， 学工号                   |

**返回结果：**

```javascript
{
    "code": 200,
    "message": "OK",
    "data": [
        {
            "propertyValue": "居民身份证",
            "propertyName": "SFZJLXM"
        },
        {
            "propertyValue": true,
            "propertyName": "ISINITIALPASSWORD"
        },
        {
            "propertyValue": "男性",
            "propertyName": "XB"
        },
        {
            "propertyValue": "中国",
            "propertyName": "GJ"
        },
        {
            "propertyValue": "true",
            "propertyName": "ZHZT"
        },
        {
            "propertyValue": "511623199802265719",
            "propertyName": "IDCARD"
        },
        {
            "propertyValue": "",
            "propertyName": "SFZJYXQ"
        },
        {
            "propertyValue": "1",
            "propertyName": "GH"
        },
        {
            "propertyValue": "在职",
            "propertyName": "JZGZT"
        },
        {
            "propertyValue": "2020-09-15",
            "propertyName": "CSRQ"
        },
        {
            "propertyValue": "xs教职工测试14",
            "propertyName": "XM"
        },
        {
            "propertyValue": "",
            "propertyName": "XMPY"
        },
        {
            "propertyValue": "",
            "propertyName": "CYM"
        },
        {
            "propertyValue": "群众",
            "propertyName": "ZZMM"
        },
        {
            "propertyValue": "",
            "propertyName": "DZXX"
        },
        {
            "propertyValue": "",
            "propertyName": "DH"
        },
        {
            "propertyName": "YDDH"
        },
        {
            "propertyValue": "",
            "propertyName": "CSD"
        },
        {
            "propertyValue": "01",
            "propertyName": "SFLBDM"
        },
        {
            "propertyValue": "2020-10-21T16:00:00.000+0000",
            "propertyName": "LASTCHANGEPASSWORDTIME"
        },
        {
            "propertyValue": "汉族",
            "propertyName": "MZ"
        },
        {
            "propertyName": "EMAIL"
        },
        {
            "propertyValue": [
                "RJXZZZ"
            ],
            "propertyName": "SZDW"
        },
        {
            "propertyValue": "5f91215e74b038000764975d",
            "propertyName": "objectId"
        }
    ]
}

```

**参数说明：**

| **参数**      | 类型       | **说明**                  |
| ------------- | ---------- | ------------------------- |
| code          | int        | 返回状态code              |
| message       | String     | 返回状态消息              |
| data          | 自定义对象 | 返回值的自定义对象        |
| propertyName  | string     | 用户属性名称              |
| propertyValue | object     | 用户属性的值              |
| 更多用户属性  |            | 更多用户属性， 请查看标准 |



#### 五、微哨在用接口-增量同步用户<a id=5></a>

> 微哨增量从SourceId同步用户。

**请求⽅式：** POST（**HTTPS或HTTP**）

**请求地址：** http://self.xxx.edu.cn/linkid/api/user/dataSource/public/pageQuery/time

**请求参数：**

```javascript
{
    "current":1,
    "size":"1",
    "startTime":"2010-01-01 00:00:00",
    "endTime":""
}
```

**参数说明：**

| **参数**  | 类型   | **是否必须** | **说明**                                                     |
| --------- | ------ | ------------ | ------------------------------------------------------------ |
| current   | list   | 是           | 用户属性的名称                                               |
| value     | string | 是           | 用户属性的值                                                 |
| startTime | string | 是           | 查询这个时间之后有更新的用户数据,   格式："yyyy-MM-dd hh:mm:ss" |
| endTime   | string | 否           | 查询这个时间之前有更新的用户数据，格式："yyyy-MM-dd hh:mm:ss" |

**返回结果：**

```javascript
{
    "code": 200,
    "message": "OK",
    "data": {
        "total": 100,
        "users": [
            {
                "GH": "R00166",
                "updatedTime": 1604913327223,
                "SFLBDM": "01",
                "szdwAndGwmc": [
                    {
                        "szdw": "R5f91269d45fc080006eab46b",
                        "gwmc": null,
                        "type": null,
                        "szdwSource": "RG_SourceID"
                    }
                ],
                "isDeleted": false,
                "XM": "xs教职工测试14",
                "LABEL": [],
                "EMAIL": null,
                "SZDW": [
                    "R5f91269d45fc080006eab46b"
                ]
            }
        ]
    }
}

```

**参数说明：**

| **参数**     | 类型       | **说明**                      |
| ------------ | ---------- | ----------------------------- |
| code         | int        | 返回状态code                  |
| message      | String     | 返回状态消息                  |
| data         | 自定义对象 | 返回值的自定义对象            |
| total        | int        | 总数                          |
| GH           | string     | 用户属性名称                  |
| SFLBDM       | string     | 人员类型代码                  |
| XM           | string     | 姓名                          |
| SZDW         | list       | 所在单位代码， 一个人有多部门 |
| szdwAndGwmc  | list       | 用户三元组数据                |
| 更多用户属性 |            | 更多用户属性， 请查看标准     |



#### 六、海大科探在用接口-增量同步用户<a id=6></a>

> 科探增量从SourceId同步用户， 全部用户查询不分页， 根据时间戳增量获取

**请求⽅式：** GET（**HTTPS或HTTP**）

**请求地址：** http://self.xxx.edu.cn/linkid/api/aggregate/keTan/public/findUsersByDate?timestamp=1605150501700

**请求参数：**

```javascript
timestamp， 时间戳， 示例：1605150501700
```

**参数说明：**

| **参数**  | 类型 | **是否必须** | **说明**                     |
| --------- | ---- | ------------ | ---------------------------- |
| timestamp | long | 是           | 时间戳， 示例：1605150501700 |

**返回结果：**

```javascript
{
    "errno": 0,
    "error": null,
    "entities": [
        {
            "account": "031230",
            "name": "yangtao",
            "email": "null",
            "phone": "null",
            "timestamp": 1605150501720,
            "disabled": false
        }
    ],
    "total": 1
}

```

**参数说明：**

| **参数**  | 类型       | **说明**                  |
| --------- | ---------- | ------------------------- |
| errno     | int        | 返回状态，0 成功， 1 失败 |
| error     | String     | 返回状态消息              |
| entities  | 自定义对象 | 返回值的自定义对象        |
| total     | int        | 总数                      |
| account   | string     | 学工号                    |
| name      | string     | 姓名                      |
| email     | string     | 邮箱                      |
| phone     | string     | 手机号                    |
| timestamp | long       | 时间戳                    |
| disabled  | boolean    | 用户是否废弃              |



#### 七、海大再用接口-分页获取标签下的用户<a id=7></a>

> 海大获取标签下用户信息

**请求⽅式：** GET（**HTTPS或HTTP**）

**请求地址：** http://self.xxx.edu.cn/linkid/api/user/public/pageQueryUsersByLabelId

**请求参数：**

```javascript
示例：https://idself26.rghall.com.cn/linkid/api/user/public/pageQueryUsersByLabelId?number=1&size=10&labelId=5f57697b437baa0006942c68
```

**参数说明：**

| **参数** | 类型   | **是否必须** | **说明**                                                     |
| -------- | ------ | ------------ | ------------------------------------------------------------ |
| number   | list   | 是           | 当前请求页                                                   |
| size     | string | 是           | 每页返回值                                                   |
| labelId  | string | 否           | 查询这个时间之前有更新的用户数据，格式："yyyy-MM-dd hh:mm:ss" |

**返回结果：**

```javascript
{
    "code": 200,
    "message": "OK",
    "data": {
        "totalElements": 20,
        "totalPages": 20,
        "currentPage": 1,
        "pageSize": 1,
        "content": [
            {
                "SFZJYXQ": "",
                "DH": "",
                "IDCARD": "330202199504081118",
                "ZZMM": "中国共产党党员",
                "EMAIL": null,
                "JZGZT": "在职",
                "szdwAndGwmc": [
                    {
                        "szdw": "R5fa3bca7d71c090006a9f6f7",
                        "gwmc": null,
                        "type": null,
                        "szdwSource": "RG_SourceID"
                    },
                    {
                        "szdw": "R5fab5d6c5951ed000666a80a",
                        "gwmc": null,
                        "type": "rule",
                        "szdwSource": "RG_SourceID"
                    },
                    {
                        "szdw": "R5fab5dc65951ed000666a810",
                        "gwmc": null,
                        "type": "rule",
                        "szdwSource": "RG_SourceID"
                    },
                    {
                        "szdw": "R5fab5e395951ed000666a817",
                        "gwmc": null,
                        "type": "rule",
                        "szdwSource": "RG_SourceID"
                    },
                    {
                        "szdw": "R5fab5e8e5951ed000666a81a",
                        "gwmc": null,
                        "type": "rule",
                        "szdwSource": "RG_SourceID"
                    },
                    {
                        "szdw": "R5fab5f2e5951ed000666a821",
                        "gwmc": null,
                        "type": "rule",
                        "szdwSource": "RG_SourceID"
                    }
                ],
                "isDeleted": false,
                "CSD": "",
                "CYM": "",
                "XMPY": "",
                "LABEL": [
                    "5f57697b437baa0006942c68"
                ],
                "SZDW": [
                    "R5fa3bca7d71c090006a9f6f7",
                    "R5fab5d6c5951ed000666a80a",
                    "R5fab5dc65951ed000666a810",
                    "R5fab5e395951ed000666a817",
                    "R5fab5e8e5951ed000666a81a",
                    "R5fab5f2e5951ed000666a821"
                ],
                "GH": "1987121",
                "GJ": "中国",
                "YDDH": "11111111111",
                "XB": "女性",
                "MZ": "汉族",
                "CSRQ": null,
                "SFZJLXM": "居民身份证",
                "SFLBDM": "01",
                "XM": "许晴",
                "DZXX": "",
                "TEL": "13603537730",
                "LASTCHANGEPASSWORDTIME": "2020-09-07T16:00:00.000+0000",
                "SFLBMC": "教职工"
            }
        ]
    }
}

```

**参数说明：**

| **参数**      | 类型       | **说明**                      |
| ------------- | ---------- | ----------------------------- |
| code          | int        | 返回状态code                  |
| message       | String     | 返回状态消息                  |
| data          | 自定义对象 | 返回值的自定义对象            |
| totalElements | int        | 总数                          |
| totalPages    | int        | 总页数                        |
| currentPage   | int        | 当前页                        |
| pageSize      | int        | 每页返回数据                  |
| content       | list       | 用户列表                      |
| GH            | string     | 用户属性名称                  |
| SFLBDM        | string     | 人员类型代码                  |
| XM            | string     | 姓名                          |
| SZDW          | list       | 所在单位代码， 一个人有多部门 |
| szdwAndGwmc   | list       | 用户三元组数据                |
| LABEL         | list       | 用户身上的标签id列表          |
| 更多用户属性  |            | 更多用户属性， 请查看标准     |