# 群组推送安全验证

SID调用应用接口时，应用需要验证请求的合法性。其中，涉及到的术语、验证原理、验证步骤如下：

**术语**

|  **术语**   |                           **介绍**                           |
| :---------: | :----------------------------------------------------------: |
|    APPID    |             应用的唯一标识。SID与应用约定的数据              |
| APPSECURITY |               应用的密钥。SID与应用约定的数据                |
|  Timestamp  | 时间戳（北京时间毫秒数）。SID调用API时生成的时间戳，附带在SID请求数据中 |
|  Signature  | MD5签名。由（APPID+APPSECURITY+Timestamp)字符串经过MD5后生成。附带在SID请求数据中 |

**验证原理**

SID在调⽤应用接口时，会携带**Signature**和**Timestamp**。Signature是SID获取到的APPID、APPSECURITY，以及Timestamp三个值通过MD5后形成的。应⽤在接收到SID调用请求时，会通过相同的⽅式（应用将自身的APPID、APPSECURITY和接收到的Timestamp进行MD5形成一个MD5值，并与请求中的Signature匹配）验证请求是否合法。

**验证步骤**

1. 获取SID请求数据中的Signature、Timestamp。

2. 将APPID、APPSECURITY与SID请求数据中的Timestamp进行MD5加密，形成MD5值。

   MD5值形成过程如下：

   APPID = 12345, 

   APPSECURITY=derfs, 

   Timestamp=1589102903474 , 

   即12345derfs1589102903474通过md5加密后形成32位⼩写签名。

   ```
   md5 -s 12345derfs1589102903474
   # MD5 ("12345derfs1589102903474") = 0e5d920d35e426875dba18f1a0e694a3
   ```

3. 将第二步中的MD5值与SID请求数据中的Signature进行比较，相同，则SID请求合法，否则，请求不合法。

