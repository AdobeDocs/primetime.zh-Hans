---
description: Widevine许可证令牌界面提供生产和测试服务。
title: Widevine许可证令牌请求/响应
exl-id: f8d71f63-7783-44f9-8b1b-4b5646dca339
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '858'
ht-degree: 5%

---

# Widevine许可证令牌请求/响应 {#widevine-license-token-request-response}

Widevine许可证令牌界面提供生产和测试服务。

此HTTP请求返回一个令牌，该令牌可兑换为Widevine许可证。

**方法：GET、POST** （使用www-url编码的主体，其中包含这两种方法的参数）

**URL：**

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

**表13：令牌查询参数**

<table id="table_ww1_hcs_pv">  
 <thead> 
  <tr> 
   <th class="entry"> <b>查询参数</b> </th> 
   <th class="entry"> <b>描述</b> </th> 
   <th class="entry"> <b>必需？</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <span class="codeph"> customerAuthenticator </span> </td> 
   <td> <p>这是您的客户API密钥，每个密钥分别用于生产和测试环境。 您可以在“ExpressPlay管理功能板”选项卡上找到它。 </p> </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> 错误格式 </span> </td> 
   <td> 可以 <span class="codeph"> html </span> 或 <span class="codeph"> json </span>. <p>如果 <span class="codeph"> html </span> （缺省）在响应的图元主体中提供任何错误的HTML表示形式。 如果 <span class="codeph"> json </span> 指定，则会返回JSON格式的结构化响应。 参见 <a href="https://www.expressplay.com/developer/restapi/#json-errors" format="html" scope="external"> JSON错误 </a> 了解详细信息。 </p> <p>响应的MIME类型为 <span class="codeph"> text/uri-list </span> 成功时， <span class="codeph"> text/html </span> 对象 <span class="codeph"> html </span> 错误格式，或 <span class="codeph"> application/json </span> 对象 <span class="codeph"> json </span> 错误格式。 </p> </td> 
   <td> 否 </td> 
  </tr> 
 </tbody> 
</table>

**表14：许可证查询参数**

| 查询参数 | 描述 | 必需？ |
|--- |--- |--- |
| `generalFlags` | 表示许可证标记的4字节十六进制字符串。 “0000”是唯一允许的值 | 否 |
| `kek` | 密钥加密密钥(KEK)。 密钥是使用密钥封装算法(AES Key Wrap，RFC3394)通过KEK加密存储的。 | 否 |
| `kid` | 内容加密密钥或字符串的16字节十六进制字符串表示形式 `^somestring'`. 字符串的长度，后跟 `^` 不能大于64个字符。 请查看下面的注释以查看示例。 | 是 |
| `ek` | 加密内容密钥的十六进制字符串表示形式。 | 否 |
| `contentKey` | 内容加密密钥的16字节十六进制字符串表示形式 | 是，除非 `kek` 和 `ek` 或 `kid` 提供 |
| `contentId` | 内容ID | 否 |
| `securityLevel` | 允许值为1-5。 <ul><li>1 = `SW_SECURE_CRYPTO`</li><li> 2 = `SW_SECURE_DECODE` </li><li> 3 = `HW_SECURE_CRYPTO` </li><li> 4 = `HW_SECURE_DECODE` </li><li> 5 = `HW_SECURE_ALL`</li></ul> | 是 |
| `hdcpOutputControl` | 允许的值为0、1、2。 <ul><li>0 = `HDCP_NONE` </li><li> 1 = `HDCP_V1` </li><li> 2 = `HDCP_V2`</li></ul> | 是 |
| `licenseDuration` * | 许可证的持续时间（秒）。 如果未提供，则表示对持续时间没有限制。 有关详细信息，请查看下面的注释。 | 否 |
| `wvExtension` | 包装extensionType和extensionPayload的简短形式，以逗号分隔的字符串。 请参阅下面的格式。 示例： `…&wvExtension=wudo,AAAAAA==&…` | 否，可使用任何数字 |

关于 `licenseDuration`： <ol><li> 播放将停止 `licenseDuration` 开始播放后的秒数。 </li><li> 要允许播放在任意时间内停止/恢复，请忽略 `licenseDuration` （默认为infinite）。 否则，请指定最终用户应能够享受流的时长。 </li></ol>

**表15：令牌限制查询参数**

| 查询参数 | 描述 | 必需？ |
|--- |--- |--- |
| `expirationTime` | 此令牌的过期时间。 此值必须为中的字符串 [RFC 3339](https://www.ietf.org/rfc/rfc3339.txt) “Z”区域指示符中的日期/时间格式（“Zulu时间”），或以+符号开头的整数。 RFC 3339日期/时间的示例为2006-04-14T12:01:10Z。 <br> 如果值是中的字符串 [RFC 3339](https://www.ietf.org/rfc/rfc3339.txt) 日期/时间格式，则它表示令牌的绝对到期日期/时间。 如果该值是前面有+号的整数，则从颁发起该令牌将解释为有效的相对秒数。 例如， `+60` 指定一分钟。 <br> 最长和默认（如果未指定）令牌生命周期为30天。 | 否 |

**表16：关联查询参数**

| **查询参数** | **描述** | **必需？** |
|---|---|---|
| `cookie` | 令牌中携带并由令牌赎回服务器记录的任意字符串（最多32个字符）。 可用于关联兑换服务器上的日志条目和服务提供商服务器上的日志条目。 | 否 |

<!--<a id="section_6BFBD314C77C40C4B172ABBDD2D8D80E"></a>-->

**表17：HTTP响应**

| **HTTP状态代码** | **描述** | **内容类型** | **实体正文包含** |
|---|---|---|---|
| `200 OK` | 没有错误。 | `text/uri-list` | 许可证客户获取URL +令牌 |
| `400 Bad Request` | 参数无效 | `text/html` 或 `application/json` | 错误描述 |
| `401 Unauthorized` | 身份验证失败 | `text/html` 或 `application/json` | 错误描述 |
| `404 Not found` | 错误的URL | `text/html` 或 `application/json` | 错误描述 |
| `50x Server Error` | 服务器错误 | `text/html` 或 `application/json` | 错误描述 |

**表18：事件错误代码**

<table id="table_agj_gqx_pv">  
 <thead> 
  <tr> 
   <th class="entry"> 代码 </th> 
   <th class="entry"> 描述 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> -2002 </td> 
   <td> 令牌过期时间无效： &lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2003 </td> 
   <td> IP地址无效 </td> 
  </tr> 
  <tr> 
   <td> -2005 </td> 
   <td> 内容加密密钥无效： &lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2008 </td> 
   <td> 指定的输出控制标志无效： &lt;details&gt; </td> 
  </tr> 
  <tr> 
   <td> -2017 </td> 
   <td> 必须提供身份验证令牌 </td> 
  </tr> 
  <tr> 
   <td> -2018 </td> 
   <td> 身份验证令牌无效： &lt;details&gt; <p>注意：如果验证器错误或者使用生产验证器在*.test.expressplay.com上访问测试API时，可能会发生这种情况，反之亦然。 </p> <p importance="high">注意：测试SDK和高级测试工具(ATT)仅适用于 <span class="filepath"> *.test.expressplay.com </span>，而生产设备必须使用 <span class="filepath"> *.service.expressplay.com </span> </p>. </td> 
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
   <td> 缺少租用播放持续时间 </td> 
  </tr> 
  <tr> 
   <td> -2025 </td> 
   <td> 租借播放持续时间无效 </td> 
  </tr> 
  <tr> 
   <td> -2027 </td> 
   <td> 内容加密密钥长度必须为32个十六进制数字 </td> 
  </tr> 
  <tr> 
   <td> -2030 </td> 
   <td> ExpressPlay管理错误： &lt;details&gt; </td> 
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
   <td> 未指定对应的值 </td> 
  </tr> 
  <tr> 
   <td> -2036 </td> 
   <td> 扩展类型应为4个字符 </td> 
  </tr> 
  <tr> 
   <td> -2037 </td> 
   <td> 扩展有效负载应采用Base64编码 </td> 
  </tr> 
  <tr> 
   <td> -2040 </td> 
   <td> <span class="codeph"> OutputControlFlag </span> 必须为4个字节编码 </td> 
  </tr> 
  <tr> 
   <td> -3004 </td> 
   <td> 指定的错误格式无效： &lt;format&gt; </td> 
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
   <td> 缺失 <span class="filepath"> 小孩 </span> </td> 
  </tr> 
  <tr> 
   <td> -4019 </td> 
   <td> 无法从密钥存储服务获取内容密钥 </td> 
  </tr> 
  <tr> 
   <td> -4020 </td> 
   <td> <span class="codeph"> 小孩 </span> 长度必须为32个十六进制字符 </td> 
  </tr> 
  <tr> 
   <td> -4021 </td> 
   <td> <span class="codeph"> 小孩 </span> “^”后的长度必须为64个字符 </td> 
  </tr> 
  <tr> 
   <td> -4022 </td> 
   <td> 无效 <span class="codeph"> 小孩 </span> </td> 
  </tr> 
  <tr> 
   <td> -4024 </td> 
   <td> 加密密钥无效或 <span class="codeph"> kek </span> </td> 
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
   <td> 指定的租用持续时间无效 </td> 
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
   <td> 无效 <span class="codeph"> WVExtension </span> 指定的参数 </td> 
  </tr> 
  <tr> 
   <td> -7011 </td> 
   <td> Widevine选项已禁用 </td> 
  </tr> 
 </tbody> 
</table>
