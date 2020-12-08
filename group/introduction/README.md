# 开发前须知

#### 应用同步接口开发步骤
该开发步骤主要针对校内应用，应用需根据SID提供的群组对接API开发接口，实现群组同步。

**STEP 1**：获取APPID、APPSECRET，验证SID请求数据的合法性。验证方法参考：[群组推送安全验证](/group/develop/safety-verification.html)。

APPID、APPSECRET是锐捷和应用方约定（任一方提供时，另一方与其保持一致即可）的一组数据。

**STEP 2**：开发同步接口。

同步接口开发需实现9个接口，便于SID调用，接口分为两类：

1. [群组节点管理](/group/develop/node-management.html)

   创建群组节点：新建一个群组节点。

   更新群组节点：更新某个群组节点的信息。

   删除群组节点：删除某个群组节点。

   查询某个群组节点：查询某个群组节点及子节点信息。

2. [人员管理](/group/develop/personnel-management.html)

   创建成员：新建一个人员信息。

   更新成员：更新某个人员的信息。

   删除成员：删除某个人员信息。

   查询成员：查看某个人员的信息。

   获取群组节点下成员：查询某个群组节点下有哪些人员。

**STEP 3**：建立群组并推送群组数据。

1. [定义并发布一个群组](/group/procedure/define-group.html)。
2. [建立群组推送任务](/group/procedure/create-push-task.html)。
3. [推送群组数据](/group/procedure/push-task.html)。

**STEP 4**：测试并修改已编写的接口。