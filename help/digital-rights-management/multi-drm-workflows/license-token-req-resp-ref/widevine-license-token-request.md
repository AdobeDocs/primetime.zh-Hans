---
description: Widevine许可证令牌界面提供生产和测试服务。
seo-description: Widevine许可证令牌界面提供生产和测试服务。
seo-title: Widevine许可证令牌请求／响应
title: Widevine许可证令牌请求／响应
uuid: a3522422-7075-49a7-bc55-137ef84ee430
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c

---


# Widevine许可证令牌请求／响应 {#widevine-license-token-request-response}

Widevine许可证令牌界面提供生产和测试服务。

此HTTP请求返回可兑换为Widevine许可证的令牌。

**方法：GET, POST** （带有www-url编码的正文，其中包含两种方法的参数）

**URL:**

* **生产：** `https://wv-gen.{prod_domain}/hms/wv/token`

* **测试：** ` [https://wv-gen.test.expressplay.com/hms/wv/token](https://wv-gen.test.expressplay.com/hms/wv/token)`

* **示例请求：**

   ```
   https://wv-gen.service.expressplay.com/hms/wv/token?customerAuthenticator= 
   <ExpressPlay customer authenticator identifier>
   ```

* **示例响应：**

   ```
   https://wv.service.expressplay.com/hms/wv/rights/?ExpressPlayToken=<base64-encoded ExpressPlay token>
   ```

<!--<a id="section_1E22012EE4B94BB2974D3B16DE8812D9"></a>-->

**表13:令牌查询参数**

<table id="table_ww1_hcs_pv">  
 <thead> 
  <tr> 
   <th class="entry"> <b>查询参数</b> </th> 
   <th class="entry"> <b>说明</b> </th> 
   <th class="entry"> <b>必需？</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <span class="codeph"> customerAuthenticator </span> </td> 
   <td> <p>这是您的客户API密钥，每个密钥对应于您的生产和测试环境。 您可以在ExpressPlay的“管理控制板”选项卡上找到该选项卡。 </p> </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> errorFormat </span> </td> 
   <td> html <span class="codeph"> 或 </span> json <span class="codeph"></span>。 <p>如果 <span class="codeph"> HTML </span> （默认）在响应的实体主体中提供了任何错误的HTML表示形式。 如果 <span class="codeph"> 指 </span> 定了json，则返回JSON格式的结构化响应。 有关详 <a href="https://www.expressplay.com/developer/restapi/#json-errors" format="html" scope="external"> 细信息，请参 </a> 阅JSON错误。 </p> <p>响应的MIME类型为：成功时为 <span class="codeph"> text/uri-list，对于html错误格式，为text/uri-list，或者为text/uri-list, </span> 则为html <span class="codeph"> error格式，或为json应用程序 </span><span class="codeph"></span><span class="codeph"></span><span class="codeph"></span> /json错误格式。 </p> </td> 
   <td> 否 </td> 
  </tr> 
 </tbody> 
</table>

**表14:许可证查询参数**

| 查询参数 | 说明 | 必需？ |
|--- |--- |--- |
| `generalFlags` | 表示许可证标志的4字节十六进制字符串。 “0000”是唯一允许的值 | 否 |
| `kek` | 密钥加密密钥(KEK)。 密钥使用密钥封装算法（AES密钥封装，RFC3394）通过KEK进行加密存储。 | 否 |
| `kid` | 内容加密密钥或字符串的16字节十六进制字符串表示形式 `^somestring'`。 字符串后跟的长 `^` 度不能大于64个字符。 有关示例，请查看下面的备注。 | 是 |
| `ek` | 加密内容密钥的十六进制字符串表示形式。 | 否 |
| `contentKey` | 内容加密密钥的16字节十六进制字符串表示形式 | 是，除非 `kek` 提供 `ek` 或 `kid` 提供 |
| `contentId` | 内容ID | 否 |
| `securityLevel` | 允许的值为1-5。 <ul><li>1 = `SW_SECURE_CRYPTO`</li><li> 2 = `SW_SECURE_DECODE` </li><li> 3 = `HW_SECURE_CRYPTO` </li><li> 4 = `HW_SECURE_DECODE` </li><li> 5 = `HW_SECURE_ALL`</li></ul> | 是 |
| `hdcpOutputControl` | 允许的值为0、1、2。 <ul><li>0 = `HDCP_NONE` </li><li> 1 = `HDCP_V1` </li><li> 2 = `HDCP_V2`</li></ul> | 是 |
| `licenseDuration` * | 许可证的持续时间（以秒为单位）。 如果未提供，则表示对持续时间没有限制。 有关详细信息，请查看以下说明。 | 否 |
| `wvExtension` | 以逗号分隔的字符串形式包含extensionType和extensionPayload的简短表单。 请参阅下面的格式。 示例： `…&wvExtension=wudo,AAAAAA==&…` | 否，可以使用任何数字 |

关于 `licenseDuration`: <ol><li> 播放将在播 `licenseDuration` 放开始数秒后停止。 </li><li> 要允许在不限时间内停止／恢复播放，请忽略( `licenseDuration` 默认为无限)。 否则，指定最终用户可以享受流的时间。 </li></ol>

**表15:令牌限制查询参数**

| 查询参数 | 说明 | 必需？ |
|--- |--- |--- |
| `expirationTime` | 此令牌的过期时间。 此值必须以“Z”区域指示符（“祖鲁时间”）的 [RFC 3339](https://www.ietf.org/rfc/rfc3339.txt) date/time格式输入字符串，或前面加+符号的整数。 RFC 3339的日期／时间示例为2006-04-14T12:01:10Z。 <br> 如果该值是 [RFC 3339](https://www.ietf.org/rfc/rfc3339.txt) date/time格式中的字符串，则它表示令牌的绝对过期日期／时间。 如果值是前面有+符号的整数，则它被解释为从发出开始的相对秒数，表示令牌有效。 例如，指定 `+60` 一分钟。 <br> 最大和默认（如果未指定）令牌生命周期为30天。 | 否 |

**表16:关联查询参数**

| **查询参数** | **说明** | **必需？** |
|---|---|---|
| `cookie` | 在令牌中长达32个字符的任意字符串，由令牌兑换服务器记录。 可用于关联赎回服务器上的日志条目和服务提供商服务器上的日志条目。 | 否 |

<!--<a id="section_6BFBD314C77C40C4B172ABBDD2D8D80E"></a>-->

**表17:HTTP响应**

| **HTTP状态代码** | **说明** | **内容类型** | **实体正文包含** |
|---|---|---|---|
| `200 OK` | 无错误。 | `text/uri-list` | 许可证获取URL +令牌 |
| `400 Bad Request` | 无效图标 | `text/html` os `application/json` | 错误说明 |
| `401 Unauthorized` | 身份验证失败 | `text/html` os `application/json` | 错误说明 |
| `404 Not found` | 错误的URL | `text/html` os `application/json` | 错误说明 |
| `50x Server Error` | 服务器错误 | `text/html` os `application/json` | 错误说明 |

**表18:事件错误代码**

<table id="table_agj_gqx_pv">  
 <thead> 
  <tr> 
   <th class="entry"> 代码 </th> 
   <th class="entry"> 说明 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> -2002 </td> 
   <td> 令牌到期时间无效：&lt;详细信息&gt; </td> 
  </tr> 
  <tr> 
   <td> -2003 </td> 
   <td> IP地址无效 </td> 
  </tr> 
  <tr> 
   <td> -2005 </td> 
   <td> 内容加密密钥无效：&lt;详细信息&gt; </td> 
  </tr> 
  <tr> 
   <td> -2008 </td> 
   <td> 指定的输出控制标志无效：&lt;详细信息&gt; </td> 
  </tr> 
  <tr> 
   <td> -2017 </td> 
   <td> 必须提供身份验证令牌 </td> 
  </tr> 
  <tr> 
   <td> -2018 </td> 
   <td> 身份验证令牌无效：&lt;详细信息&gt; <p>注意： 如果身份验证器错误，或使用生产身份验证器访问*.test.expressplay.com上的测试API时，可能会发生这种情况，反之亦然。 </p> <p importance="high">注意： 测试SDK和高级测试工具(ATT)只能与 <span class="filepath"> *.test.expressplay.com一起使用 </span>，而生产设备必须使用 <span class="filepath"> *.service.expressplay.com </span> </p>. </td> 
  </tr> 
  <tr> 
   <td> -2019 </td> 
   <td> 可用令牌不足 </td> 
  </tr> 
  <tr> 
   <td> -2022 </td> 
   <td> 缺少租赁期结束时间 </td> 
  </tr> 
  <tr> 
   <td> -2023 </td> 
   <td> 缺少租赁播放持续时间 </td> 
  </tr> 
  <tr> 
   <td> -2025 </td> 
   <td> 租赁播放持续时间无效 </td> 
  </tr> 
  <tr> 
   <td> -2027 </td> 
   <td> 内容加密密钥的长度必须为32个十六进制数字 </td> 
  </tr> 
  <tr> 
   <td> -2030 </td> 
   <td> ExpressPlay管理员错误：&lt;详细信息&gt; </td> 
  </tr> 
  <tr> 
   <td> -2031 </td> 
   <td> 服务帐户已禁用 </td> 
  </tr> 
  <tr> 
   <td> -2033 </td> 
   <td> Cookie无效 </td> 
  </tr> 
  <tr> 
   <td> -2034 </td> 
   <td> 输出控件无效，值超出指定范围 </td> 
  </tr> 
  <tr> 
   <td> -2035 </td> 
   <td> 未指定相应的值 </td> 
  </tr> 
  <tr> 
   <td> -2036 </td> 
   <td> 扩展类型应为4个字符 </td> 
  </tr> 
  <tr> 
   <td> -2037 </td> 
   <td> 扩展有效负荷应采用Base64编码 </td> 
  </tr> 
  <tr> 
   <td> -2040 </td> 
   <td> <span class="codeph"> OutputControlFlag必 </span> 须编码4个字节 </td> 
  </tr> 
  <tr> 
   <td> -3004 </td> 
   <td> 指定的错误格式无效：&lt;format&gt; </td> 
  </tr> 
  <tr> 
   <td> -4001 </td> 
   <td> 无法验证设备 </td> 
  </tr> 
  <tr> 
   <td> -4010 </td> 
   <td> 令牌无效 </td> 
  </tr> 
  <tr> 
   <td> -4018 </td> 
   <td> 失踪的 <span class="filepath"> 孩子 </span> </td> 
  </tr> 
  <tr> 
   <td> -4019 </td> 
   <td> 无法从密钥存储服务获取内容密钥 </td> 
  </tr> 
  <tr> 
   <td> -4020 </td> 
   <td> <span class="codeph"> 孩子 </span> 长度必须为32个十六进制字符 </td> 
  </tr> 
  <tr> 
   <td> -4021 </td> 
   <td> <span class="codeph"> 孩 </span> 子必须在'^'后长64个字符 </td> 
  </tr> 
  <tr> 
   <td> -4022 </td> 
   <td> 无效子 <span class="codeph"> 数 </span> </td> 
  </tr> 
  <tr> 
   <td> -4024 </td> 
   <td> 加密密钥或Kek无 <span class="codeph"> 效 </span> </td> 
  </tr> 
  <tr> 
   <td> -5003 </td> 
   <td> 常规标志无效 </td> 
  </tr> 
  <tr> 
   <td> -6005 </td> 
   <td> 指定的密钥数据无效 </td> 
  </tr> 
  <tr> 
   <td> -6007 </td> 
   <td> 指定的租赁持续时间无效 </td> 
  </tr> 
  <tr> 
   <td> -7002 </td> 
   <td> Widevine不支持设备ID绑定 </td> 
  </tr> 
  <tr> 
   <td> -7003 </td> 
   <td> 缺少安全级别值 </td> 
  </tr> 
  <tr> 
   <td> -7004 </td> 
   <td> 安全级别值无效 </td> 
  </tr> 
  <tr> 
   <td> -7006 </td> 
   <td> 缺少HDCP输出控制值 </td> 
  </tr> 
  <tr> 
   <td> -7007 </td> 
   <td> 指定的许可证持续时间无效 </td> 
  </tr> 
  <tr> 
   <td> -7008 </td> 
   <td> 无法生成Widevine许可证 </td> 
  </tr> 
  <tr> 
   <td> -7009 </td> 
   <td> 指定的 <span class="codeph"> WVExtension参 </span> 数无效 </td> 
  </tr> 
  <tr> 
   <td> -7011 </td> 
   <td> 禁用了Widevine选项 </td> 
  </tr> 
 </tbody> 
</table>