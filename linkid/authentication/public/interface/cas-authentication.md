# CAS认证接口
> [用户认证](#1)
>
> [请求验证ticket](#2)
>
> [cas登出](#3)


#### 一、用户认证<a id=1></a>

> 应用向SID认证服务器请求认证，SID返回认证页面。
>

**请求⽅式：** GET（**HTTPS或HTTP**）

**请求地址：** http://{server}/login

注：https方式类似。

**请求参数：**

```javascript
请求示例：
http://ljw.sso.rghall.com.cn/login?service=http://192.168.54.63:8080/user/index
```

**参数说明：**

| **参数** | **是否必须** | **说明**                               |
| -------- | ------------ | -------------------------------------- |
| service  | 是           | SID要跳转的地址，即SID下发ticket的地址 |

**返回结果：**

```
返回ticket，示例为：
http://192.168.54.63:8080/user/index?ticket=ST-368-gChqIqVuq9j83YCG9dw4sh1KDaMrg-sso-fddcfb8db-z9ng2
```

**参数说明：**

| **参数** | **说明**                                        |
| -------- | ----------------------------------------------- |
| ticket   | 票据。ticket参数在service指向的url里，由SID下发 |



#### 二、请求验证ticket<a id=2></a>

> 应用携带SID下发的ticket，请求SID验证ticket的有效性，SID验证成功后返回用户信息。

**1、CAS3.0协议请求验证ticket**

**请求⽅式：** GET（**HTTPS或HTTP**）

**请求地址：** http://{server}/p3/serviceValidate

注：https方式类似。

**请求参数：**

```javascript
请求示例：
http://ljw.sso.rghall.com.cn/p3/serviceValidate?ticket=ST-368-gChqIqVuq9j83YCG9dw4sh1KDaMrg-sso-fddcfb8db-z9ng2&service=http://192.168.54.63:8080/user/index
```

**参数说明：**

| **参数** | **是否必须** | **说明**                  |
| -------- | ------------ | ------------------------- |
| ticket   | 是           | SID下发的票据             |
| service  | 是           | 和用户验证中的service相同 |

**返回结果：**

SID返回xml格式的用户信息，如下图：

![tempLogin](cas-authentication.assets/tempLogin.png)

**参数说明：**

| **参数** | **说明**                                                     |
| -------- | ------------------------------------------------------------ |
| 用户信息 | 用户信息为xml格式，包括用户登录名。返回的用户属性可在SID中配置。 |

**2、CAS2.0协议请求验证ticket。**

**请求⽅式：** GET（**HTTPS或HTTP**）

**请求地址：** http://{server}/serviceValidate

注：https方式类似。

**请求参数：**

```javascript
请求示例：
http://ljw.sso.rghall.com.cn/serviceValidate?ticket=ST-368-gChqIqVuq9j83YCG9dw4sh1KDaMrg-sso-fddcfb8db-z9ng2&service=http://192.168.54.63:8080/user/index
```

**参数说明：**

| **参数** | **是否必须** | **说明**                  |
| -------- | ------------ | ------------------------- |
| ticket   | 是           | SID下发的票据             |
| service  | 是           | 和用户验证中的service相同 |

**返回结果：**

SID返回xml格式的用户信息，如下图：

![image-20201125105229012](cas-authentication.assets/image-20201125105229012.png)

**参数说明：**

| **参数** | **说明**                                                     |
| -------- | ------------------------------------------------------------ |
| 用户信息 | 用户信息为xml格式，包括用户登录名。返回的用户属性可在SID中配置。 |

#### 三、cas登出<a id=3></a>

> CAS登出。

**请求⽅式：** GET（**HTTPS或HTTP**）

**请求地址：** http://{server}/logout

注：https方式类似。