# 开发前须知

>[角色接口规范说明](#1)
>
>[角色接口调用授权](#2)
>
>[创建应用角色](#3)
>
>[标签数据授权](#4)
>
>[用户数据授权](#5)



#### 角色接口规范说明：<div id=1></div>

1. 各类数据内容返回， 属性名为驼峰式， 以文档示例为准

2. 分页接口， 分页参数属性是驼峰式， 以文档示例为准

   

#### 角色接口调用授权：<div id=2></div>

* [获取accessToken](../../../get-access-token.md)
* 设置请求头 Authorization: Bearer {access_token}

![image-20201111115147461.png](README.assets/image-20201111115147460.png)



#### 创建应用角色<div id=3></div>

##### 1、编辑应用

![image-20201117114847707](README.assets/image-20201117114847707.png)

##### 2、配置应用角色

![image-20201117114946687](README.assets/image-20201117114946687.png)

##### 3、新增角色

![image-20201117115034306](README.assets/image-20201117115034306.png)

![image-20201117115145681](README.assets/image-20201117115145681.png)



##### 4、进行角色映射

![image-20201117115202060](README.assets/image-20201117115202060.png)

![image-20201117115218756](README.assets/image-20201117115218756.png)

![image-20201117115235012](README.assets/image-20201117115235012.png)



![image-20201117115256632](README.assets/image-20201117115256632.png)



#### 标签数据授权<div id=4></div>

[标签数据授权](../../label/introduction/README.md)

#### 用户数据授权<div id=5></div>

[用户数据授权](../../user/introduction/README.md)