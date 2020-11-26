# 开发前须知

>[CAS认证对接](#1)
>
>[OAuth认证对接](#2)

## CAS认证对接<a id=1></a>

应用进行SID认证需先进行以下操作：

#### 一、在SID中注册、配置应用。

应用注册和配置请参考：[CAS认证对接](/quick-get-start/general-application-docking.html)。

#### 二、在应用中配置CAS client

1、配置maven环境依赖。

```Java
<dependency>
    <groupId>org.jasig.cas.client</groupId>
    <artifactId>cas-client-core</artifactId>
    <version>3.5.0</version>
</dependency>
```

也可从https://mvnrepository.com/artifact/org.jasig.cas.client/cas-client-core地址下载。

2、配置应用程序部署描述文件 (web.xml)

**注：下文内{server}表示sso地址。**

（1）必备配置。设置serverName、监听类。serverName为登陆成功或者退出成功的回调地址。

```xml
<context-param>
    <param-name>serverName</param-name>
    <param-value>http://localhost:8080</param-value>
</context-param>
<listener>
    <listener-class>
    	org.jasig.cas.client.session.SingleSignOutHttpSessionListener
    </listener-class>
</listener>
```

（2）配置AuthenticationFilter。

>AuthenticationFilter的作用是用于拦截SSO登陆请求的，当你提交的request符合SSO登陆规则，CAS client会通过这个filter将登陆请求转向到CAS server的登陆界面。因为这是第一步，所以它要在最上面。

```
<filter>
    <filter-name>CAS Authentication Filter</filter-name>
    <filter-class>
    	org.jasig.cas.client.authentication.AuthenticationFilter
    </filter-class>
    <init-param>
    <!--平台登录路径-->
        <param-name>casServerLoginUrl</param-name>
        <param-value>{server}/login</param-value>
    </init-param>
</filter>
<filter-mapping>
    <filter-name>CAS Authentication Filter</filter-name>
    <url-pattern>/*</url-pattern><!—拦截路径-->
</filter-mapping>
```

（3）配置TicketValidationFilter。

>用于拦截登陆返回的跳转请求的。当CAS server确认登陆用户名密码后，会返回一个server ticket，这个ticket会由应用服务器上的CAS client再送回CAS server进行验证，用于防止仿冒攻击的。

```
<filter>
    <filter-name>CAS Validation Filter</filter-name>
    <filter-class>
    	org.jasig.cas.client.validation.Cas30ProxyReceivingTicketValidationFilter
    </filter-class>
    <init-param>
    <!--平台验证路径-->
        <param-name>casServerUrlPrefix</param-name>
        <param-value>{server}/p3</param-value>
    </init-param>
    <init-param>
        <!--验证后是否重定向-->
        <param-name>redirectAfterValidation</param-name>
        <param-value>true</param-value>
    </init-param>
    <init-param>
        <!--服务器与客户端的误差时间-->
        <param-name>tolerance</param-name>
        <param-value>5000</param-value>
    </init-param>
</filter>
    <filter-mapping>
        <filter-name>CAS Validation Filter</filter-name>
        <url-pattern>/*</url-pattern><!--拦截路径-->
</filter-mapping>
```

注：

org.jasig.cas.client.validation.Cas30ProxyReceivingTicketValidationFilter为CAS3.0协议，CAS2.0协议请配置org.jasig.cas.client.validation.Cas20ProxyReceivingTicketValidationFilter，同时配置：casServerUrlPrefix为{server}。

（4）配置HttpServletRequestWrapperFilter。

>目的是将CAS server返回的信息封装到Http request里面，这样客户端就可以用request.getRemoteUser()来获取用户名等信息了。

```
<filter>
    <filter-name>
    	CAS HttpServletRequest Wrapper Filter
    </filter-name>
    <filter-class>
    	org.jasig.cas.client.util.HttpServletRequestWrapperFilter
    </filter-class>
</filter>
<filter-mapping>
    <filter-name>
    	CAS HttpServletRequest Wrapper Filter
    </filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>
```

（5）配置AssertionThreadLocalFilter。

>是用于前端程序（通常是前端脚本程序）访问，因为这个时候无法通过request来获取信息。

```
<filter>
    <filter-name>
    	CAS Assertion Thread Local Filter
    </filter-name>
    <filter-class>
    	org.jasig.cas.client.util.AssertionThreadLocalFilter
    </filter-class>
</filter>
<filter-mapping>
    <filter-name>
    	CAS Assertion Thread Local Filter
    </filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>
```

（6）配置SingleSignOutFilter。

>用于拦截登出路径，清除登录信息。

```
<filter>
    <filter-name>
    	CAS Single Sign Out Filter
    </filter-name>
    <filter-class>
    	org.jasig.cas.client.session.SingleSignOutFilter
    </filter-class>
</filter>
<filter-mapping>
    <filter-name>
    	CAS Single Sign Out Filter
    </filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>
```

#### 三、获取登陆用户名和用户信息示例

```
//在应用程序中获取用户信息
AttributePrincipal principal = (AttributePrincipal)request.getUserPrincipal();
String username = principal.getName();

//获取用户属性的示例代码如下：
Map attributes = principal.getAttributes(); 
String email=attributes.get("age");   //获取需要的属性，key填属性名即可
```

#### 四、SID认证对外接口

SID认证对外接口（CAS）请参考认证模块【CAS认证接口】。



## OAuth认证对接<a id=2></a>

针对OAuth认证对接，进行SID认证前，应用需先在SID中注册、配置应用，应用注册和配置请参考：[OAuth认证对接](/quick-get-start/general-application-docking.html)。

SID认证对外接口（OAuth2.0）请参考认证模块【OAuth认证接口】。

