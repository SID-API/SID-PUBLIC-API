# 成员管理
>[查询成员](#link1)
>
>[创建成员](#link2)
>
>[更新成员](#link3)
>
>[删除成员](#link4)
>
>[获取群组节点下成员](#link5)

应用端开发人员需实现成员管理相关接口，与SID进行人员同步。

#### 查询成员<div id=link1></div>

>查询某个人员信息。
>SID调用“创建成员”、“更新成员”、“删除成员”等接口时，会先调用该接口，执行查询操作，提高群组推送的容错性。

**请求⽅式：**GET（HTTPS或HTTP）

**请求地址：**http://{server}/app/user/get/{id}

注：https方式类似。

**请求头:**

header: Signature (通过MD5获取到的签名值)

header: Timestamp（当前时间戳）

**参数说明：**

| **参数**       | **是否必须** | **说明**    |
| -------------- | ------------ | --------------|
| id             | 是           | 学号或工号 |

**返回结果：**

```
{
    "errcode":200,
    "errmsg":"ok",
    "userInfo":{
        "userId": "YT001",
        "name": "xxx",
        "xb": "1",
        "tel": "18732990023",
        "sflbdm":"01",
        "departments":["xxxx1","xxxx2"],
        "department":["xxxx1","xxxx2"]
    }
}
```

**参数说明：**

| **参数**    | 是否必须 | **说明**                    |
| ----------- | -------- | --------------------------- |
| errcode     | 是       | 返回码，成功为200           |
| errmsg      | 是       | 对返回码的文本描述内容      |
| userInfo    | 是       | 用户信息                    |
| userId      | 是       | 学号或⼯号                  |
| name        | 是       | 用户姓名                    |
| xb          | 否       | 用户性别:1-⼥，2-男，3-不知 |
| tel         | 否       | ⽤户绑定手机号              |
| sflbdm      | 是       | ⽤户身份类别代码            |
| departments | 是       | ⽤户所属部⻔ID列表          |
| department | 是       | ⽤户所属部⻔Code列表          |


#### 创建成员<div id=link2></div>

>新建一个人员信息。

**请求⽅式：**POST（HTTPS或HTTP）

**请求地址：**http://{server}/app/user/create

注：https方式类似。

**请求头:**

header: Signature (通过MD5获取到的签名值)

header: Timestamp（当前时间戳）

**请求参数：**说明：在SID中可以配置用户同步信息，即要与应用同步哪些用户属性。

```
{
    "userId": "YT001",
    "name": "xxx",
    "xb": "1",
    "tel": "18732990023",
    "sflbdm":"01",
    "departments":["xxxx1","xxxx2"],
     "department":["xxxx1","xxxx2"]
}
```

**参数说明：**

| **参数** | **是否必须** | **说明**     |
| -------- | ------------ | ------------ |
| userId      | 是       | 学号或⼯号                  |
| name        | 是       | 用户姓名                    |
| xb          | 否       | 用户性别:1-⼥，2-男，3-不知 |
| tel         | 否       | ⽤户绑定手机号              |
| sflbdm      | 是       | ⽤户身份类别代码            |
| departments | 是       | ⽤户所属部⻔ID列表          |
| department | 是       | ⽤户所属部⻔Code列表          |
**返回结果：**

```
{
    "errcode": 200,
    "errmsg": "created"
}
```

**参数说明：**

| **参数** | **说明**               |
| -------- | ---------------------- |
| errcode  | 返回码，成功为200      |
| errmsg   | 对返回码的文本描述内容 |



#### 更新成员<div id=link3></div>

>更新某个人员的信息。

**请求⽅式：**POST（HTTPS或HTTP）

**请求地址：**http://{server}/app/user/update

注：https方式类似。

**请求头:**

header: Signature (通过MD5获取到的签名值)

header: Timestamp（当前时间戳）

**请求参数：**说明：在SID中可以配置用户同步信息，即要与应用同步哪些用户属性。

```
{
    "userId": "YT001",
    "name": "xxx",
    "xb": "1",
    "tel": "18732990023",
    "sflbdm":"01",
    "departments":["xxxx1","xxxx2"],
    "department":["xxxx1","xxxx2"],
}
```

**参数说明：**

| **参数** | **是否必须** | **说明**   |
| -------- | ------------ | ---------- |
| userId      | 是       | 学号或⼯号                  |
| name        | 是       | 用户姓名                    |
| xb          | 否       | 用户性别:1-⼥，2-男，3-不知 |
| tel         | 否       | ⽤户绑定手机号              |
| sflbdm      | 是       | ⽤户身份类别代码            |
| departments | 是       | ⽤户所属部⻔ID列表          |
| department | 是       | ⽤户所属部⻔Code列表          |
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



#### 删除成员<div id=link4></div>

>删除某个人员信息。

**请求⽅式：**GET（HTTPS或HTTP）

**请求地址：**http://{server}/app/user/delete/{id}

注：https方式类似。

**请求头:**

header: Signature (通过MD5获取到的签名值)

header: Timestamp（当前时间戳）

**参数说明：**

| **参数** | **是否必须** | **说明**   |
| -------- | ------------ | ---------- |
| id       | 是           | 学号或工号 |

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



#### 获取群组节点下成员<div id=link5></div>

>查询某个群组节点下有哪些人员。

**请求⽅式：**GET（HTTPS或HTTP）

**请求地址：**http://{server}/app/user/simplelist/{departmentId}

注：https方式类似。

**请求头:**

header: Signature (通过MD5获取到的签名值)

header: Timestamp（当前时间戳）

**参数说明：**

| **参数**     | **是否必须** | **说明** |
| ------------ | ------------ | -------- |
| departmentId | 是           | 部门id   |

**返回结果：**

```
{
    "errcode":200,
    "errmsg":"ok",
    "userlist": [
        {
            "userId": "YT001",
            "name": "xxx",
            "xb": "1",
            "tel": "18732990023",
            "sflbdm":"01",
            "departments":["xxxx1","xxxx2"],
            "department":["xxxx1","xxxx2"]
        }
     ]
}
```

**参数说明：**

| **参数**    | 是否必须 | **说明**                    |
| ----------- | -------- | --------------------------- |
| errcode     | 是       | 返回码，成功为200           |
| errmsg      | 是       | 对返回码的文本描述内容      |
| userlist    | 是       | ⽤户信息列表                |
| userId      | 是       | 学号或⼯号                  |
| name        | 是       | 用户姓名                    |
| xb          | 否       | 用户性别:1-⼥，2-男，3-不知 |
| tel         | 否       | ⽤户绑定手机号              |
| sflbdm      | 是       | ⽤户身份类别代码            |
| departments | 是       | ⽤户所属部⻔ID列表          |
| department | 是       | ⽤户所属部⻔Code列表          |

