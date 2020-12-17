

# 海大在用接口对外API

海大在用接口对外API描述SID向应用提供的标准接口，以便外部应用调用。标准接口如下：

>[海大科探在用接口-增量同步用户](#6)
>
>[海大在用接口-分页获取标签下的用户](#7)
>
>[海大微信绑定接口-添加用户在SID中的微信绑定](#8)
>
>[海大微信解绑接口-解除用户在SID中的微信绑定](#9)



#### 一、海大科探在用接口-增量同步用户<a id=6></a>

> 科探增量从SourceId同步用户， 全部用户查询不分页， 根据时间戳增量获取

**请求⽅式：** GET（**HTTPS或HTTP**）

**请求地址：** http://self.xxx.edu.cn/linkid/api/aggregate/keTan/public/findUsersByDate?timestamp=xxx

注：https方式类似。

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



#### 二、海大在用接口-分页获取标签下的用户<a id=7></a>

> 海大获取标签下用户信息

**请求⽅式：** GET（**HTTPS或HTTP**）

**请求地址：** http://self.xxx.edu.cn/linkid/api/user/public/pageQueryUsersByLabelId

注：https方式类似。

**请求参数：**

```javascript
示例：
https://idself26.rghall.com.cn/linkid/api/user/public/pageQueryUsersByLabelId?number=1&size=10&labelId=5f57697b437baa0006942c68
```

**参数说明：**

| **参数** | 类型   | **是否必须** | **说明**   |
| -------- | ------ | ------------ | ---------- |
| number   | list   | 是           | 当前请求页 |
| size     | string | 是           | 每页返回值 |
| labelId  | string | 否           | 标签id     |

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

#### 三、海大微信绑定接口-添加用户在SID中的微信绑定<a id=8></a>

> 海大添加用户的微信绑定

**请求⽅式：** POST（**HTTPS或HTTP**）

**请求地址：** http://self.xxx.edu.cn/linkid/api/public/wechat/weChatBindFromApplets

注：https方式类似。

**参数说明：**

| **参数**   | 类型   | **是否必须** | **说明**                                                     |
| ---------- | ------ | ------------ | ------------------------------------------------------------ |
| userId     | String | 是           | 用户学工号                                                   |
| unionId    | String | 否           | 用户统一标识。<br>针对一个微信开放平台帐号下的应用，同一用户的 unionid 唯一 |
| openid     | String | 否           | 普通用户标识，对该公众帐号唯一                               |
| fromSource | String | 否           | 认证来源， 默认为应用的clientid                              |

**备注**：微信绑定的功能需要至少提供```userId, unionId```或者```userId, openid, fromSource```才能完成绑定。

**返回结果：**

```javascript
{
    "code": 200,
    "message": "OK",
    "data": true
}
```

**参数说明：**

| **参数** | 类型    | **说明**                        |
| -------- | ------- | ------------------------------- |
| code     | int     | 返回状态code                    |
| message  | String  | 返回状态消息                    |
| data     | boolean | 绑定成功返回true，失败返回false |

#### 四、海大微信解绑-解除用户在SID中的微信绑定<a id=9></a>

> 海大解除用户的微信绑定

**请求⽅式：** POST（**HTTPS或HTTP**）

**请求地址：** http://self.xxx.edu.cn/linkid/api/public/wechat/weChatUnbindFromApplets

注：https方式类似。

**参数说明：**

| **参数**   | 类型   | **是否必须** | **说明**                                                     |
| ---------- | ------ | ------------ | ------------------------------------------------------------ |
| userId     | String | 是           | 用户学工号                                                   |
| unionId    | String | 否           | 用户统一标识。<br>针对一个微信开放平台帐号下的应用，同一用户的 unionid 唯一 |
| openid     | String | 否           | 普通用户标识，对该公众帐号唯一                               |
| fromSource | String | 否           | 认证来源， 默认为应用的clientid                              |

**备注**：微信解绑的功能需要至少提供```userId, unionId```或者```userId, openid, fromSource```才能完成解绑。

**返回结果：**

```javascript
{
    "code": 200,
    "message": "OK",
    "data": true
}
```

**参数说明：**

| **参数** | 类型    | **说明**                        |
| -------- | ------- | ------------------------------- |
| code     | int     | 返回状态code                    |
| message  | String  | 返回状态消息                    |
| data     | boolean | 解绑成功返回true，失败返回false |