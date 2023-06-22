---
description: FairPlay许可证令牌界面提供生产和测试服务。
title: FairPlay许可证令牌请求/响应
exl-id: 7073a74b-d907-4d45-8550-4305655c33f5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '814'
ht-degree: 4%

---

# FairPlay许可证令牌请求和响应 {#fairplay-license-token-request-response}

FairPlay许可证令牌界面提供生产和测试服务。 此请求返回可兑换为FairPlay许可证的令牌。

**方法：GET、POST** （使用www-url编码的主体，其中包含这两种方法的参数）

**URL：**

* **生产：** `https://fp-gen.{prod_domain}/hms/fp/token`

* **测试：** `https://fp-gen.test.expressplay.com/hms/fp/token`

* **示例请求：**

```<xref href="https: pr-gen.test.expressplay.com="" hms="" pr="" token?customerAuthenticator="201722,1ad8eed133edf43cbcc185f0236828ae&kid=b366360da82e9c6e0b0984002a362cf2&contentKey=b366360da82e9c6e0b0984002a362cf2&rightsType=BuyToOwn&analogVideoOPL=0&compressedDigitalAudioOPL=0&compressedDigitalVideoOPL=0&uncompressedDigitalAudioOPL=0&uncompressedDigitalVideoOPL=0&quot; format=&quot;html&quot; scope=&quot;external&quot;">
  https://fp-gen.test.expressplay.com/hms/fp/token?customerAuthenticator= 
   <ExpressPlay customer authenticator identifier> 
   &kid=<CEKSID> 
   &contentKey=<CEK> 
   &rightsType=BuyToOwn 
   &analogVideoOPL=0 
   &compressedDigitalAudioOPL=0 
   &compressedDigitalVideoOPL=0 
   &uncompressedDigitalAudioOPL=0 
   &uncompressedDigitalVideoOPL=0
```

* **示例响应：**

   ```
   https://fp.service.expressplay.com:80/hms/fp/rights/?ExpressPlayToken=<base64-encoded ExpressPlay token>
   ```

**请求查询参数**

**表3：令牌查询参数**

| 查询参数 | 描述 | 必需？ |
|--- |--- |--- |
| customerAuthenticator作为查询参数的客户验证器customerAuthenticator FairPlay | 这是您的客户API密钥，每个密钥分别用于生产和测试环境。 您可以在“ExpressPlay管理功能板”选项卡上找到它。 | 是 |
| 错误格式 | html或json。 如果html（默认）在响应的实体正文中提供了任何错误的HTML表示形式。 如果指定了json，则会返回JSON格式的结构化响应。 参见 [JSON错误](https://www.expressplay.com/developer/restapi/#json-errors) 了解详细信息。 响应的mime类型是text/uri-list （成功）、text/html (HTML错误格式)或application/json （JSON错误格式）。 | 否 |

**表4：许可证查询参数**

| **查询参数** | **描述** | **必需？** |
|---|---|---|
| `generalFlags` | 表示许可证标记的4字节十六进制字符串。 “0000”是唯一允许的值。 | 否 |
| `kek` | 密钥加密密钥(KEK)。 密钥是使用密钥封装算法(AES Key Wrap，RFC3394)通过KEK加密存储的。 如果 `kek` 是以下任一选项提供的： `kid` 或 `ek` 需要提供参数， *但不是两者都有*. | 否 |
| `kid` | 内容加密密钥或字符串的16字节十六进制字符串表示形式 `'^somestring'`. 字符串的长度，后跟 `'^'` 不能大于64个字符。 | 否 |
| `ek` | 加密内容密钥的十六进制字符串表示形式。 | 否 |
| `contentKey` | 内容加密密钥的16字节十六进制字符串表示形式 | 是，除非 `kek` 和 `ek` 或 `kid` 提供了。 |
| `iv` | 内容加密IV的16字节十六进制字符串表示形式 | 是 |
| `rentalDuration` | 租用的持续时间（以秒为单位，默认值 — 0） | 否 |
| `fpExtension` | 简短表单包装 `extensionType` 和 `extensionPayload`，以逗号分隔的字符串。 例如： [...] `&fpExtension=wudo,AAAAAA==&`[...] | 否，可使用任何数字 |

**表5：令牌限制查询参数**

<table id="table_ar3_lsx_pv">  
 <thead> 
  <tr> 
   <th class="entry"> <b>查询参数</b> </th> 
   <th class="entry"> <b>描述</b> </th> 
   <th class="entry"> <b>必需？</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <span class="codeph"> expirationTime </span> </td> 
   <td> 此令牌的过期时间。 此值必须是中的字符串 <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" scope="external"> RFC 3339 </a> “Z”区域指示符中的日期/时间格式（“Zulu时间”），或以“+”符号开头的整数。 RFC 3339日期/时间的示例为 <span class="codeph"> 2006-04-14T12:01:10Z </span>. <p>如果值是中的字符串 <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" scope="external"> RFC 3339 </a> 日期/时间格式，则它表示令牌的绝对到期日期/时间。 如果值是带有“+”号的整数，则从颁发开始，它将解释为令牌有效的相对秒数。 </p> 例如， <span class="codeph"> +60 </span> 指定一分钟。 最长和默认（如果未指定）令牌生命周期为30天。 </td> 
   <td> 否 </td> 
  </tr> 
 </tbody> 
</table>

**表6：关联查询参数**

| **查询参数** | **描述** | **必需？** |
|---|---|---|
| `cookie` | 一个长度不超过32个字符的任意字符串，在令牌中携带并由令牌赎回服务器记录。 这可用于将兑换服务器上的日志条目与服务提供商服务器上的日志条目相关联。 | 否 |

**响应**

**表7： HTTP响应**

| **HTTP状态代码** | **描述** | **内容类型** | **实体正文包含** |
|---|---|---|---|
| `200 OK` | 没有错误。 | `text/uri-list` | 许可证客户获取URL +令牌 |
| `400 Bad Request` | 参数无效 | `text/html` 或 `application/json` | 错误描述 |
| `401 Unauthorized` | 身份验证失败 | `text/html` 或 `application/json` | 错误描述 |
| `404 Not found` | 错误的URL | `text/html` 或 `application/json` | 错误描述 |
| `50x Server Error` | 服务器错误 | `text/html` 或 `application/json` | 错误描述 |

**表8：事件错误代码**

<table id="table_i2c_zsx_pv">  
 <thead> 
  <tr> 
   <th class="entry"> <b>代码</b> </th> 
   <th class="entry"> <b>描述</b> </th> 
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
   <td> 身份验证令牌无效： &lt;details&gt; <p>注意：如果验证器错误或在访问测试API时，可能会发生这种情况 <span class="filepath"> *.test.expressplay.com </span> 使用生产验证器，反之亦然。 </p> <p importance="high">注意：测试SDK和高级测试工具(ATT)仅适用于 <span class="filepath"> *.test.expressplay.com </span>，而生产设备必须使用 <span class="filepath"> *.service.expressplay.com </span>. </p> </td> 
  </tr> 
  <tr> 
   <td> -2019 </td> 
   <td> 可用令牌不足 </td> 
  </tr> 
  <tr> 
   <td> -2020 </td> 
   <td> 缺少权限类型 </td> 
  </tr> 
  <tr> 
   <td> -2021 </td> 
   <td> 权限类型无效 </td> 
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
   <td> 丢失的孩子 </td> 
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
   <td> <span class="codeph"> 小孩 </span> ^后必须为64个字符 </td> 
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
   <td> -6001 </td> 
   <td> 无效 <span class="codeph"> FPExtension </span> 指定的参数 </td> 
  </tr> 
  <tr> 
   <td> -6002 </td> 
   <td> FP令牌类型无效 </td> 
  </tr> 
  <tr> 
   <td> -6003 </td> 
   <td> 无效 <span class="codeph"> 四 </span> 指定的参数 </td> 
  </tr> 
  <tr> 
   <td> -6004 </td> 
   <td> 未能为FP生成CKC </td> 
  </tr> 
  <tr> 
   <td> -6005 </td> 
   <td> 指定的密钥数据无效 </td> 
  </tr> 
  <tr> 
   <td> -6006 </td> 
   <td> 服务未获得FairPlay支持的授权 </td> 
  </tr> 
  <tr> 
   <td> -6007 </td> 
   <td> 指定的租用持续时间无效 </td> 
  </tr> 
  <tr> 
   <td> -6008 </td> 
   <td> FairPlay不支持设备ID绑定 </td> 
  </tr> 
  <tr> 
   <td> -6009 </td> 
   <td> FairPlay选项已禁用 </td> 
  </tr> 
 </tbody> 
</table>
