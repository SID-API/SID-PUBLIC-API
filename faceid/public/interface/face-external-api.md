# 人脸对外接口

该部分描述SID应向应用提供的标准接口，以便外部应用调用。标准接口如下：

>[1:1 认证](#1)
>
>[1:N 认证](#2)
>
>[增量同步照片](#3)
>
>[增量同步特征值](#4)
>
>[通过用户id和照片类型查询照片](#5)
>
>[检查照片质量](#6)
>
>[通过用户id list查询用户照片](#7)
>
>[上传照片](#8)

#### 一、1:1 认证接口（特征值或照片）<a id=1 ></a>

> 应用上传一张照片或特征值与 SID中保存的底库照片或特征值进行比对。

**请求⽅式：** POST（**HTTPS或HTTP**）

**请求地址：** http://{server}/faceid/public/auth/compare/userId

**请求参数：**

```
{
    "featureB":"xTKzP.....ACAPw==",
    "imageB":{
    	"image":"/9j/4AAQSkZJRgAB......OMCuquxOVH//2Q==",
    	"ext":"jpg"
    },
    "userId" : "testface"
}
```

**参数说明：**

| **参数** | 类型       | **是否必须** | **说明**     |
| -------- | ---------- | ------------ | ------------ |
| featureB | String     | 是           | 照片的特征值 |
| imageB   | 自定义对象 | 是           | 照片对象     |
| userId   | String     | 是           | 用户的学工号 |
| image    | String     | 是           | 照片的base64 |
| ext      | String     | 是           | 照片后缀     |

**返回结果：**

```
{
    "code": 200,
    "message": "OK",
    "data": {
        "userId": "testface",
        "image": "/group1/M00/00/09/rBEITl-XwYCAD1-MAAHfytyTzvE998.jpg",
        "score": 0.9973,
        "appScore": 0.63,
        "hasPass": true,
        "hasPermission": null
    }
}
```

**参数说明：**

| **参数** | 类型       | **说明**               |
| -------- | ---------- | ---------------------- |
| code     | int        | 返回状态code           |
| message  | String     | 返回状态消息           |
| data     | 自定义对象 | 返回值的自定义对象     |
| userId   | String     | 用户学工号             |
| image    | String     | 照片对应的存储存储路径 |
| score    | Double     | 相似值                 |
| appScore | Double     | 厂商相似值标准         |
| hasPass  | Boolean    | 照片是否通过           |



#### 二、1:N 认证接口（特征值或照片）<a id=2 ></a>

> 应用上传一张照片，返回与这张照片相似度最高的用户信息，进行1:N 认证。

**请求⽅式：** POST（**HTTPS或HTTP**）

**请求地址：** http://{server}/faceid/public/auth/search

**请求参数：**

```
{
  "feature":"xTKzPP6I4......AACAPw==",
  "file":{
    	"image":"/9j/4AAQSkZJRgAB......OMCuquxOVH//2Q==",
    	"ext":"jpg"
    }
}
```

**参数说明：**

| **参数** | 类型   | **是否必须**       | **说明**     |
| -------- | ------ | ------------------ | ------------ |
| feature  | String | 与 image 任选一个  | 照片的特征值 |
| image    | String | 与 feature任选一个 | 照片的base64 |
| ext      | String | 与image一致        | 照片的后缀   |

**返回结果：**

```
{
    "code": 200,
    "message": "OK",
    "data": {
        "userId": "testface",
        "image": "/group1/M00/00/09/rBEITl-XwYCAD1-MAAHfytyTzvE998.jpg",
        "score": 0.9973356
    }
}
```

**参数说明：**

| **参数** | 类型       | **说明**           |
| -------- | ---------- | ------------------ |
| code     | int        | 返回状态code       |
| message  | String     | 返回状态消息       |
| data     | 自定义对象 | 返回值的自定义对象 |
| userId   | String     | 用户学工号         |
| image    | String     | 照片对应的存储路径 |
| score    | Double     | 相似值             |




#### 三、增量同步照片接口（水印或不加水印）<a id=3 ></a>

> 应用根据时间戳增量同步特征值接口。

**请求⽅式：** POST（**HTTPS或HTTP**）

**请求地址：** http://{server}/faceid/public/face/findIncreaseUserFaceImage

**请求参数：**

```
{
    "currentPage":1,
    "timeStamp":2,
    "pageSize":20，
    "types":["100"]
}
```

**参数说明：**

| **参数**    | 类型         | **是否必须** | **说明**                                              |
| ----------- | ------------ | ------------ | ----------------------------------------------------- |
| currentPage | int          | 是           | 分页页码                                              |
| pageSize    | int          | 是           | 分页每页大小                                          |
| timeStamp   | long         | 是           | 应用上次同步照片的时间。SID从该时间戳以后开始同步照片 |
| types       | List<String> | 是           | 照片类型code                                          |

**返回结果：**

```
{
    "code": 200,
    "message": "OK",
    "data": {
        "pageSize": 10,
        "pageNum": 1,
        "totalAmount": 3,
        "results": [
            {
                "userId": "james",
                "faceId": "5f70993cecf37300063840c2",
                "imageUrl": "/group1/M00/00/05/rBEITl9wmT2AGYY7AADBdIqeHWk671.jpg",
                "timeStamp": 1603768753929,
                "face": [
                    {
                        "type": "100",
                        "image": "/9j/4AAQS......RghD83GR//Z",
                        "fileName": "rBEITl9wmT2AGYY7AADBdIqeHWk671.jpg",
                        "updateTime": 1601214816398
                    }
                ],
                "deleted": false
            },
            {
                "userId": "5f86c39d9d72dd0006678544",
                "faceId": "5f86c3dfebd1ae000631fa04",
                "imageUrl": "/group1/M00/00/07/rBEITl-Gw-CALhSGAAFlVfs2oiA611.jpg",
                "timeStamp": 1603768052435,
                "face": [
                    {
                        "type": "100",
                        "image": "/9j/4AAQSkZJRgAB......OMCuquxOVH//2Q==",
                        "fileName": "rBEITl-Gw-CALhSGAAFlVfs2oiA611.jpg",
                        "updateTime": 1607937942726
                    }
                ],
                "deleted": true
            }
        ]
    }
}
```

**参数说明：**

| **参数**                | 类型       | **说明**                                     |
| ----------------------- | ---------- | -------------------------------------------- |
| code                    | int        | 返回状态code                                 |
| message                 | String     | 返回状态消息                                 |
| data                    | 自定义对象 | 返回值的自定义对象                           |
| pageSize                | int        | 分页每页长度                                 |
| pageNum                 | int        | 分页页码                                     |
| totalAmount             | int        | 需要同步照片的人员总数                       |
| results.userId          | String     | 学工号                                       |
| results.faceId          | String     | 用户id                                       |
| results.imageUrl        | String     | 回显照片的存储路径                           |
| results.timeStamp       | long       | 照片变动时间戳（毫秒）                       |
| results.deleted         | boolean    | 照片是否被删除。 true=删除，false=新增或修改 |
| results.face.type       | String     | 照片类型code                                 |
| results.face.image      | String     | 照片base64                                   |
| results.face.fileName   | String     | 照片名称                                     |
| results.face.updateTime | long       | 照片上传时间                                 |

注：照片类型code： 底库照片=100 （支持字符串 01），生活照=201，职业照=202。



#### 四、增量同步特征值接口<a id=4 ></a>

> 增量同步特征值接口。

**请求⽅式：**  POST（**HTTPS或HTTP**）

**请求地址：**  http://{server}/faceid/public/face/findIncreaseUserFace

**请求参数：**

```
{
    "currentPage":1,
    "pageSize":100,
    "timeStamp":0
}
```

**参数说明：**

| **参数**    | 类型 | **是否必须** | **说明**                                              |
| ----------- | ---- | ------------ | ----------------------------------------------------- |
| currentPage | int  | 是           | 分页页码                                              |
| pageSize    | int  | 是           | 分页每页大小                                          |
| timeStamp   | long | 是           | 应用上次同步照片的时间。SID从该时间戳以后开始同步照片 |

**返回结果：**

```
{
    "code": 200,
    "message": "OK",
    "data": {
        "pageSize": 100,
        "pageNum": 1,
        "totalAmount": 1,
        "orders": null,
        "results": [
            {
                "userId": "testface",
                "imageUrl": "/group1/M00/00/09/rBEITl-XkxaAIRZjAAFRPYtJz1g042.jpg",
                "timeStamp": 1603769154390,
                "images": [
                    {
                        "feature": "1utfPYb5ur2ADCg97r......ACAPw==",
                        "type": "100",
                        "updateTime": 1603769129918
                    }
                ],
                "deleted": false
            }
        ]
    }
}
```

**参数说明：**

| **参数**                  | 类型       | **说明**                                    |
| ------------------------- | ---------- | ------------------------------------------- |
| code                      | int        | 返回状态code                                |
| message                   | String     | 返回状态消息                                |
| data                      | 自定义对象 | 返回值的自定义对象                          |
| pageSize                  | int        | 分页每页长度                                |
| pageNum                   | int        | 分页页码                                    |
| totalAmount               | int        | 照片总数                                    |
| results.userId            | String     | 学工号                                      |
| results.imageUrl          | String     | 回显照片的存储路径                          |
| results.timeStamp         | long       | 照片变动时间戳（毫秒）                      |
| results.deleted           | boolean    | 照片是否被删除。true=删除，false=新增或修改 |
| results.images.type       | String     | 照片类型code                                |
| results.images.feature    | String     | 照片特征值                                  |
| results.images.updateTime | long       | 照片特征值计算时间                          |

注：照片类型code： 底库照片=100，生活照=201，职业照=202。



#### 五、通过用户id和照片类型查询照片<a id=5 ></a>

##### 1、返回照片路径

> 通过用户id和照片类型查询照片返回照片路径。

**请求⽅式：** POST（**HTTPS或HTTP**）

**请求地址：** http://{server}/faceid/public/face/searchFaceByUserIdAndType

**请求参数：**

```
{
    "userId" : "testface",
    "type":100
}
```

**参数说明：**

| **参数** | 类型   | **是否必须** | **说明**     |
| -------- | ------ | ------------ | ------------ |
| userId   | String | 是           | 学工号       |
| type     | int    | 是           | 照片分类code |

**返回结果：**

```
{
    "code": 200,
    "message": "OK",
    "data": {
        "userId": "testface",
        "path": "/group1/M00/00/09/rBEITl-XwYCAD1-MAAHfytyTzvE998.jpg"
    }
}
```

**参数说明：**

| **参数** | 类型       | **说明**           |
| -------- | ---------- | ------------------ |
| code     | int        | 返回状态code       |
| message  | String     | 返回状态消息       |
| data     | 自定义对象 | 返回值的自定义对象 |
| userId   | String     | 学工号             |
| path     | String     | 照片在存储上的路径 |

注：照片类型code： 底库照片=100，生活照=201，职业照=202。

##### 2、返回照片base64

> 通过用户id和照片类型查询照片返回照片的base64。

**请求⽅式：** POST（**HTTPS或HTTP**）

**请求地址：** http://{server}/faceid/public/face/searchFaceByUserIdAndTypeImage

**请求参数：**

```
{
    "userId" : "testface",
    "type":100
}
```

**参数说明：**

| **参数** | 类型   | **是否必须** | **说明**     |
| -------- | ------ | ------------ | ------------ |
| userId   | String | 是           | 学工号       |
| type     | String | 是           | 照片分类code |

**返回结果：**

```
{
    "code": 200,
    "message": "OK",
    "data": {
        "userId": "testface",
        "path": "/group1/M00/00/09/rBEITl-XwYCAD1-MAAHfytyTzvE998.jpg",
        "image": "/9j/4AAQ.....YbGf/Z"
    }
}
```

**参数说明：**

| **参数** | 类型       | **说明**           |
| -------- | ---------- | ------------------ |
| code     | int        | 返回状态code       |
| message  | String     | 返回状态消息       |
| data     | 自定义对象 | 返回值的自定义对象 |
| userId   | String     | 学工号             |
| path     | String     | 照片在存储上的路径 |
| image    | String     | 照片base64         |

注：照片类型code： 底库照片=100，生活照=201，职业照=202。



#### 六、检查照片质量<a id=6 ></a>

> 检查照片质量。

**请求⽅式：** POST（**HTTPS或HTTP**）

**请求地址：** http://{server}/faceid/public/face/quality

**请求参数：**

```
{
    "file" : {
        "image":"/9j/4AAQ......EQBERAf/Z",
        "ext":"jpg"
    }
}
```

**参数说明：**

| **参数**   | 类型   | **是否必须** | **说明**   |
| ---------- | ------ | ------------ | ---------- |
| file.image | String | 是           | 照片base64 |
| file.ext   | String | 是           | 照片后缀   |

**返回结果：**

```
{
    "code": 200,
    "message": "OK",
    "data": {
        "qualityScores": "0.7168,0.5429,0.0000,0.0002,0.9148,0.5352,0.0008,0.9664,0.0000,0.0000,0.0000,0.0000,0.0000,0.0000,0.0000,0.0000,-1.3611,4.4754,-2.4668,137.0000,327.0000,284.0000,284.0000,1.0000,0.9830,0.8736,0.0000,0.0000,0.0000,0.0000,4c0c864175cc13c0526e021f798fa3cf",
        "scores": [
            0.63,
            0.51,
            0.0
        ],
        "scoresInfo": [
            {
                "position": 1,
                "explain": "总分"
            },
            {
                "position": 2,
                "explain": "光照分"
            },
            {
                "position": 3,
                "explain": "口罩分"
            }
        ],
        "manufactureName": "云从",
        "isQualified": true,
        "unqualifiedReason": ""
    }
}
```

**参数说明：**

| **参数**          | 类型             | **说明**                 |
| ----------------- | ---------------- | ------------------------ |
| code              | int              | 返回状态code             |
| message           | String           | 返回状态消息             |
| data              | 自定义对象       | 返回值的自定义对象       |
| qualityScores     | String           | 照片质量分               |
| scores            | List<String>     | 照片质量分合格标准       |
| scoresInfo        | List<自定义对象> | 表明每个位置的质量分含义 |
| manufactureName   | String           | 厂商名称                 |
| isQualified       | boolean          | 照片是否符合标准         |
| unqualifiedReason | String           | 不符合标准的原因         |

注：qualityScores 字符串中的各类分数是根据 “,”(逗号)隔开的。计算总分是否合格的方法如下：

根据 scoresInfo获取总分的位置(position)为 1。然后在质量分（qualityScores）中获取第一位分数为 0.7168，在 合格标准中（scores） 获取总分标准为 0.63。因为 0.7168 >  0.63， 所以质量合格。



#### 七、通过用户id list查询用户照片<a id=7 ></a>

> 通过用户id list查询用户照片。当用户（userIds） 长度超过10个时，取前10个用户的学工号返回

**请求⽅式：** POST（**HTTPS或HTTP**）

**请求地址：** http://{server}/faceid/public/face/findAllImageBase64ByUserIds

**请求参数：**

```
{
	"userIds": ["testface"],
	"types": ["100"]
}
```

**参数说明：**

| **参数** | 类型         | **是否必须** | **说明**     |
| -------- | ------------ | ------------ | ------------ |
| userIds  | List<String> | 是           | 学工号       |
| types    | List<String> | 是           | 照片分类code |

**返回结果：**

```
{
    "code": 200,
    "message": "OK",
    "data": [
        {
            "userId": "testface",
            "imageUrl": "/group1/M00/00/09/rBEITl-XwYCAD1-MAAHfytyTzvE998.jpg",
            "userFaceFileDtos": [
                {
                    "type": "100",
                    "image": "/9j/4AAYXk...../2OEQdm5gYbGf/Z",
                    "fileName": "rBEITl-XwYCAD1-MAAHfytyTzvE998.jpg",
                    "timeStamp": 0
                }
            ]
        }
    ]
}
```

**参数说明：**

| **参数**                   | 类型       | **说明**               |
| -------------------------- | ---------- | ---------------------- |
| code                       | int        | 返回状态code           |
| message                    | String     | 返回状态消息           |
| data                       | 自定义对象 | 返回值的自定义对象     |
| userId                     | String     | 学工号                 |
| imageUrl                   | String     | 回显照片的存储路径     |
| userFaceFileDtos.type      | String     | 照片类型               |
| userFaceFileDtos.timeStamp | long       | 照片变动时间戳（毫秒） |
| image                      | String     | 照片base64             |

注：照片类型code： 底库照片=100，生活照=201，职业照=202。



#### 八、上传照片（通过类型+用户id）<a id=8 ></a>

> 上传照片（通过类型+用户id）。

**请求⽅式：** POST（**HTTPS或HTTP**）

**请求地址：** http://{server}/faceid/public/face/image

**请求参数：**

```
{
    "ext":"jpg",
    "type":100,
    "userId":"2009082",
    "image":"/9j/4AAQS....Gf/Z"
}
```

**参数说明：**

| **参数** | 类型   | **是否必须** | **说明**       |
| -------- | ------ | ------------ | -------------- |
| userId   | String | 是           | 学工号         |
| type     | String | 是           | 照片分类code   |
| ext      | String | 是           | 照片后缀       |
| image    | String | 是           | 照片base64编码 |

**返回结果：**

```
{
    "code": 200,
    "message": "OK",
    "data": {
        "userId": "2009082",
        "path": "/group1/M00/00/18/rBEITl-iGcOAd-uEAAHfytyTzvE908.jpg"
    }
}
```

**参数说明：**

| **参数** | 类型       | **说明**           |
| -------- | ---------- | ------------------ |
| code     | int        | 返回状态code       |
| message  | String     | 返回状态消息       |
| data     | 自定义对象 | 返回值的自定义对象 |
| userId   | String     | 学工号             |
| path     | String     | 上传照片的存储路径 |

注：照片类型code： 底库照片=100，生活照=201，职业照=202。