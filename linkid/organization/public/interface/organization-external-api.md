# 组织信息对外API

组织信息对外api描述SID向应用提供的标准接口，以便外部应用调用。标准接口如下：

>[根据组织id获取所有部门id](#1)
>
>[根据部门id查询部门详细信息](#2)



#### 一、根据组织id获取所有部门id<a id=1></a>

> 当业务系统要同步身份平台的部门信息时， 需要根据组织查询所有部门id
>

**请求⽅式：** POST（**HTTPS或HTTP**）

**请求地址：** http://self.xxx.edu.cn/linkid/api/organization/public/findAllSonOrganizationIds

**请求参数：**

```javascript
["RJXZZZ"]
```

**参数说明：**

| **参数**     | 类型 | **是否必须** | **说明** |
| ------------ | ---- | ------------ | -------- |
| request body | 列表 | 是           | 组织id   |

**返回结果：**

```javascript
{
    "code": 200,
    "message": "OK",
    "data": [
        "RJXZZZ",
        "R5f91237eef72960006ea0d2d"
    ]
}

```

**参数说明：**

| **参数** | 类型       | **说明**           |
| -------- | ---------- | ------------------ |
| code     | int        | 返回状态code       |
| message  | String     | 返回状态消息       |
| data     | 自定义对象 | 返回值为部门id列表 |



#### 二、根据部门id查询部门详细信息<a id=2></a>

> 当业务系统要同步身份平台的部门信息时， 需要根据组织查询所有部门id,  然后根据部门id查询部门详细信息

**请求⽅式：** GET（**HTTPS或HTTP**）

**请求地址：** http://self.xxx.edu.cn/linkid/api/organization/public/findById/{id}

**请求参数：**

```javascript
请求示例：
https://self.xxx.edu.cn/linkid/api/organization/public/findById/R5f91237eef72960006ea0d2d
```

**参数说明：**

| **参数** | 类型   | **是否必须** | **说明** |
| -------- | ------ | ------------ | -------- |
| id       | string | 是           | 部门id   |

**返回结果：**

```javascript
{
    "code": 200,
    "message": "OK",
    "data": {
        "id": "R5f91237eef72960006ea0d2d",
        "code": "a",
        "desc": null,
        "name": "a",
        "parent": "RJXZZZ",
        "category": "未分类部门",
        "createUser": null,
        "address": null,
        "tel": null,
        "official": true,
        "version": null,
        "isDeleted": false,
        "updatedTime": "2020-10-22T06:15:26.598+0000",
        "organizationIndex": 1
    }
}

```

**参数说明：**

| **参数**          | 类型       | **说明**                    |
| ----------------- | ---------- | --------------------------- |
| code              | int        | 返回状态code                |
| message           | String     | 返回状态消息                |
| data              | 自定义对象 | 返回值为部门id列表          |
| id                | string     | 部门id                      |
| code              | string     | 部门编码                    |
| desc              | string     | 部门描述                    |
| name              | string     | 部门名称                    |
| parent            | string     | 父部门id                    |
| category          | string     | 部门分类                    |
| createUser        | string     | 创建人                      |
| address           | string     | 部门地址                    |
| tel               | string     | 部门电话                    |
| official          | boolean    | 是否正式部门                |
| version           | string     | 数据版本， 增量采集数据使用 |
| isDeleted         | boolean    | 部门是否删除                |
| updatedTime       | string     | 部门更新时间                |
| organizationIndex | int        | 部门排序                    |
