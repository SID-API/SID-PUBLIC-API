# 单点对接

SID向应用提供CAS和OAuth2.0两种单点登录认证方式：

#### CAS单点对接说明

- 应用通过调用[CAS认证接口](/linkid/authentication/public/interface/cas-authentication.html)，实现与SID的单点对接。
- 从结构上看，CAS 包含两个部分： CAS Server 和 CAS Client。CAS Server 需要独立部署，主要负责对用户的认证工作；CAS Client 负责处理对客户端受保护资源的访问请求，需要登录时，重定向到 CAS Server。**应用和SID的角色分别对应CAS Client、CAS Server**，因此，应用需实现CAS Client功能以对接SID（CAS Server）。

#### OAuth2.0单点对接说明

OAuth协议是一种安全协议，允许用户授权第三方应用访问其储存在“其他服务提供者”上的信息，而不需要将用户名和密码提供给第三方应用或分享用户数据的所有内容。

OAuth2.0协议描述了4种客户端应用程序获取访问令牌（代表用户对客户端访问其数据权限的许可）的模式，各种模式的应用场景如下：

- authorization code：授权码模式

  功能最完整、流程最严密的授权模式，通常使用在公网的开放平台中。适用于有自己的服务器的应用，授权码是一个一次性临时凭证，用来换取 `access_token` 和 `refresh_token`。一旦换取成功，`code` 立即作废，不能再使用第二次。

- resource owner password credentials：密码模式

  一般在内部系统中使用，调用者以用户为单位。用户向客户端提供自己的用户名和密码，向“其他服务提供者”换取 `access_token` 。

- client credentials：客户端模式

  一般在内部系统之间的API调用，两个平台之间调用，调用者以平台为单位。如第三方，或者调用者是一个后端模块，没有用户界面时，可以使用客户端模式。鉴权服务器直接对客户端进行身份验证，验证通过后，返回 token。

- implicit：简化模式

  适用于纯静态页面应用。该模式下，`access_token` 容易泄露且不可刷新。

SID提供了授权码模式、密码模式、客户端模式接口与应用进行单点对接，接口详见：[OAuth2.0认证接口](/linkid/authentication/public/interface/oauth-authentication.html)。