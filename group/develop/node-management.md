# 群组节点管理
>[查询某个群组节点](#link1)
>
>[创建群组节点](#link2)
>
>[更新群组节点](#link3)
>
>[删除群组节点](#link4)

应用端开发人员需实现群组节点管理相关接口，与SID进行节点同步。

#### 查询某个群组节点<div id=link1></div>

>查询某个群组节点及对应子节点信息。
>
>SID调用“创建群组节点”、“更新群组节点”、“删除群组节点”等接口时，会先调用该接口，执行查询操作，提高群组推送的容错性。

**请求⽅式：**POST（HTTPS或HTTP）

**请求地址：**http://{server}/app/department/get

**请求头:**

header: Signature (通过MD5获取到的签名值)

header: Timestamp（当前时间戳）

**请求参数：**

```
{
    "id": "xxxxx",
    "isNeedChildren": false
}
```

**参数说明：**

| **参数**       | **是否必须** | **说明**                                         |
| -------------- | ------------ | ------------------------------------------------ |
| id             | 是           | 节点id                                           |
| isNeedChildren | 是           | 是否需要获取当前节点下的⼦节点:true-是，false-否 |

**返回结果：**

```
{
    "errcode": 200,
    "errmsg": "ok",
    "department": [
    {
        "id": "xxxxx",
        "name": "锐捷⽹络",
        "code": "xxx",
        "parentid": "xxxxxx",
        "order": 1
    },
    {
        "id": "xxxxx",
        "name": "身份产品管理事业部",
        "code": "xxx",
        "parentid": "xxxxxx",
        "order": 1
    }
   ]
}
```

**参数说明：**

| **参数**   | **说明**               |
| ---------- | ---------------------- |
| errcode    | 返回码，成功为200      |
| errmsg     | 对返回码的文本描述内容 |
| department | 节点信息列表           |
| id         | 节点id                 |
| name       | 节点名称               |
| code       | 节点code               |
| parentid   | 节点⽗亲id             |
| order      | 节点顺序               |



#### 创建群组节点<div id=link2></div>

>新建一个群组节点。

**请求⽅式：**POST（HTTPS或HTTP）

**请求地址：**http://{server}/app/department/create

**请求头:**

header: Signature (通过MD5获取到的签名值)

header: Timestamp（当前时间戳）

**请求参数：**

```
{
    "name": "锐捷⽹络",
    "parentid": "xxxxxx",
    "code": "1234",
    "order": 1,
    "id": "xxxxx"
}
```

**参数说明：**

| **参数** | **是否必须** | **说明**     |
| -------- | ------------ | ------------ |
| name     | 是           | 节点名称     |
| parentid | 是           | 节点⽗亲id   |
| code     | 是           | 节点code     |
| order    | 否           | 同层节点顺序 |
| id       | 是           | 节点 id      |

**返回结果：**

```
{
    "errcode": 200,
    "errmsg": "created",
    "id": "xxxxx"
}
```

**参数说明：**

| **参数** | **说明**               |
| -------- | ---------------------- |
| errcode  | 返回码，成功为200      |
| errmsg   | 对返回码的文本描述内容 |
| id       | 节点id                 |



#### 更新群组节点<div id=link3></div>

>更新某个群组节点的信息。
>

**请求⽅式：**POST（HTTPS或HTTP）

**请求地址：**http://{server}/app/department/update

**请求头:**

header: Signature (通过MD5获取到的签名值)

header: Timestamp（当前时间戳）

**请求参数：**

```
{
    "id": "xxxxx",
    "name": "锐捷⽹络",
    "code": "1234",
    "parentid": "xxxxxx",
    "order": 1
}
```

**参数说明：**

| **参数** | **是否必须** | **说明**   |
| -------- | ------------ | ---------- |
| id       | 是           | 节点 id    |
| name     | 是           | 节点名称   |
| code     | 是           | 节点code   |
| parentid | 是           | 节点⽗亲id |
| order    | 是           | 节点顺序   |

**返回结果：**

```
{
    "errcode": 200,
	"errmsg": "updated"
}
```

**参数说明：**

| **参数** | **说明**               |
| -------- | ---------------------- |
| errcode  | 返回码，成功为200      |
| errmsg   | 对返回码的文本描述内容 |



#### 删除群组节点<div id=link4></div>

>删除某个群组节点。

**请求⽅式：**GET（HTTPS或HTTP）

**请求地址：**http://{server}/app/department/delete/{id}

**请求头:**

header: Signature (通过MD5获取到的签名值)

header: Timestamp（当前时间戳）

**参数说明：**

| **参数** | **是否必须** | **说明**   |
| -------- | ------------ | ---------- |
| id       | 是           | 节点 id    |

**返回结果：**

```
{
    "errcode": 200,
	"errmsg": "deleted"
}
```

**参数说明：**

| **参数** | **说明**               |
| -------- | ---------------------- |
| errcode  | 返回码，成功为200      |
| errmsg   | 对返回码的文本描述内容 |
