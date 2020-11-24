# 标签对外API

标签信息对外api描述SID向应用提供的标准接口，以便外部应用调用。标准接口如下：

>[查询所有标签分类](#1)
>
>[通过身份标签分类查询身份标签列表](#2)
>
>[分页获取标签下的用户](#3)



#### 一、查询所有标签分类<a id=1></a>

> 当业务系统要同步身份平台的标签信息是， 需要先获取所有的标签分类， 然后根据分类id去获取所有标签
>

**请求⽅式：** POST（**HTTPS或HTTP**）

**请求地址：** http://self.xxx.edu.cn/linkid/api/aggregate/label/public/find/label/type

**请求参数：**

```javascript
{
	"isAcquiredParents": true,
	"hasDefaultNode": false,
}
```

**参数说明：**

| **参数**          | 类型    | **是否必须** | **说明**                                                     |
| ----------------- | ------- | ------------ | ------------------------------------------------------------ |
| isAcquiredParents | boolean | 是           | 表示当前接⼝是标签分类获取上级分类，当前该功能要求只展示第⼀层分类，且 第⼀个元素⽂案展示为-，如果不是就展示所有有权限看到的分类树 |
| hasDefaultNode    | boolean | 是           | 表示是否在节点树最后加上默认分类节点                         |

**返回结果：**

```javascript
{
	code: 200,
	data: [{ // 分情况展示 
		key: '-',
		title: '-'
	}, {
		key: 1,
		title: 分类1
	}， {
		key: 2,
		title：‘ 分类2’,
		children: [{
			key: 3,
			title: '分类2.1'
		}]
	}, {
		// 分情况展示 
		key: 5,
		title: '默认分类'
	}]
}


```

**参数说明：**

| **参数** | 类型       | **说明**           |
| -------- | ---------- | ------------------ |
| code     | int        | 返回状态code       |
| message  | String     | 返回状态消息       |
| data     | 自定义对象 | 返回值为部门id列表 |
| key      | string     | 标签分类id         |
| title    | string     | 标签分类名称       |



#### 二、通过身份标签分类查询身份标签列表<a id=2></a>

> 当业务系统要同步身份平台的标签信息是， 需要先获取所有的标签分类， 然后根据分类id去获取所有标签

**请求⽅式：** GET（**HTTPS或HTTP**）

**请求地址：** http://self.xxx.edu.cn/linkid/api/aggregate/label/public/find/by/typeId/{标 签分类id}

**请求参数：**

```javascript
请求示例：
https://self.xxx.edu.cn/linkid/api/aggregate/label/public/find/by/typeId/5f91237eef72960006ea0d2d
```

**参数说明：**

| **参数** | 类型   | **是否必须** | **说明**   |
| -------- | ------ | ------------ | ---------- |
| typeId   | string | 是           | 标签分类id |

**返回结果：**

```javascript
{
	"code": 200,
	"message": "OK",
	"data": [{
		"id": "5dfcbc94432aa42fecac5907",
		"name": "xcv",
		"describe": null,
		"applicationId": null,
		"createUser": "5c7776dfedd9a9952b3b44c2",
		"organizationId": "R5dc275fddc04fa681a724671",
		"organizationName": "XXXX",
		"createTime": "2019.12.20 20:20",
		"suppleList": ["5afc83b4a32ab41ad8ef8411", "5afc83b4a32ab41ad8ef8412"],
		"labelTypeId": "5df986b4432aa40dd8ee88de",
		"showStatus": "public",
		"public": true
	}]
}


```

**参数说明：**

| **参数**         | 类型       | **说明**                                  |
| ---------------- | ---------- | ----------------------------------------- |
| code             | int        | 返回状态code                              |
| message          | String     | 返回状态消息                              |
| data             | 自定义对象 | 返回值为部门id列表                        |
| id               | string     | 标签id                                    |
| name             | string     | 标签名称                                  |
| describe         | string     | 标签描述                                  |
| createUser       | string     | 标签维护人                                |
| organizationId   | string     | 标签所属部门id                            |
| organizationName | string     | 标签所属部门名称                          |
| suppleList       | string     | 标签补充名单， 人员objectId列表           |
| createTime       | string     | 标签创建时间                              |
| labelTypeId      | boolean    | 标签所属分类id                            |
| showStatus       | string     | 标签是否公开展示， “public” 公开， 其他否 |
| public           | boolean    | 标签是否公开展示， true 公开， 其他否     |



#### 三、分页获取标签下的用户<a id=3></a>

> 分页获取标签下用户信息

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