---
description: FairPlay许可证令牌接口提供生产和测试服务。
seo-description: FairPlay许可证令牌接口提供生产和测试服务。
seo-title: FairPlay许可证令牌请求／响应
title: FairPlay许可证令牌请求／响应
uuid: 10d4a760-8895-4fb3-8288-1c3a640df587
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 4%

---


# FairPlay许可证令牌请求和响应{#fairplay-license-token-request-response}

FairPlay许可证令牌接口提供生产和测试服务。 此请求返回可兑换为FairPlay许可证的令牌。

**方法：GET** 、POST（带有包含两种方法参数的ww-url编码的正文）

**URL:**

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

**表3:令牌查询参数**

| 查询参数 | 说明 | 必需？ |
|--- |--- |--- |
| 作为查询参数的客户身份验证器客户身份验证器FairPlay | 这是您的客户API密钥，每个密钥针对您的生产和测试环境。 您可以在ExpressPlay管理员仪表板选项卡上找到此选项。 | 是 |
| errorFormat | html或json。 如果html（默认）在响应的实体正文中提供任何错误的HTML表示形式。 如果指定json，则返回JSON格式的结构化响应。 有关详细信息，请参阅[JSON错误](https://www.expressplay.com/developer/restapi/#json-errors)。 响应的mime类型为：成功时为text/uri-列表,HTML错误格式为text/html,JSON错误格式为application/json。 | 否 |

**表4:许可查询参数**

| **查询参数** | **说明** | **必需？** |
|---|---|---|
| `generalFlags` | 表示许可证标志的4字节十六进制字符串。 “0000”是唯一允许的值。 | 否 |
| `kek` | 密钥加密密钥(KEK)。 密钥使用密钥打包算法（AES密钥包，RFC3394）通过KEK进行加密存储。 如果提供`kek`，则需要提供`kid`或`ek`参数之一，*但不同时提供*&#x200B;参数。 | 否 |
| `kid` | 内容加密密钥的16字节十六进制字符串表示形式或字符串`'^somestring'`。 字符串后跟`'^'`的长度不能大于64个字符。 | 否 |
| `ek` | 加密内容密钥的十六进制字符串表示形式。 | 否 |
| `contentKey` | 内容加密密钥的16字节十六进制字符串表示形式 | 是，除非提供`kek`和`ek`或`kid`。 |
| `iv` | 内容加密IV的16字节十六进制字符串表示法 | 是 |
| `rentalDuration` | 租金的持续时间（以秒为单位）（默认- 0） | 否 |
| `fpExtension` | 以逗号分隔的字符串形式包括`extensionType`和`extensionPayload`的简短表单。 例如：[..] `&fpExtension=wudo,AAAAAA==&`[..] | 否，可以使用任何数字 |

**表5:令牌限制查询参数**

<table id="table_ar3_lsx_pv">  
 <thead> 
  <tr> 
   <th class="entry"> <b>查询参数</b> </th> 
   <th class="entry"> <b>说明</b> </th> 
   <th class="entry"> <b>必需？</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <span class="codeph"> expirationTime  </span> </td> 
   <td> 此令牌的过期时间。 此值必须是<a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" scope="external"> RFC 3339 </a>日期／时间格式中的字符串（“祖鲁时间”），或前面有“+”符号的整数。 RFC 3339日期／时间的示例为<span class="codeph"> 2006-04-14T12:01:10Z </span>。 <p>如果该值是<a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" scope="external"> RFC 3339 </a>日期／时间格式的字符串，则它表示令牌的绝对过期日期／时间。 如果值是前面有“+”符号的整数，则它被解释为从发出开始的相对秒数，表示令牌有效。 </p> 例如，<span class="codeph"> +60 </span>指定一分钟。 最大和默认（如果未指定）令牌生命周期为30天。 </td> 
   <td> 否 </td> 
  </tr> 
 </tbody> 
</table>

**表6:相关查询参数**

| **查询参数** | **说明** | **必需？** |
|---|---|---|
| `cookie` | 任意字符串，长度不超过32个字符，包含在令牌中并由令牌兑换服务器记录。 这可用于关联在兑换服务器上和服务提供商服务器上的日志条目。 | 否 |

**响应**

**表7:HTTP响应**

| **HTTP状态代码** | **说明** | **内容类型** | **实体正文包含** |
|---|---|---|---|
| `200 OK` | 无错误。 | `text/uri-list` | 许可证获取URL +令牌 |
| `400 Bad Request` | 无效标记 | `text/html` 或  `application/json` | 错误描述 |
| `401 Unauthorized` | 身份验证失败 | `text/html` 或  `application/json` | 错误描述 |
| `404 Not found` | 错误的URL | `text/html` 或  `application/json` | 错误描述 |
| `50x Server Error` | 服务器错误 | `text/html` 或  `application/json` | 错误描述 |

**表8:事件错误代码**

<table id="table_i2c_zsx_pv">  
 <thead> 
  <tr> 
   <th class="entry"> <b>代码</b> </th> 
   <th class="entry"> <b>说明</b> </th> 
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
   <td> 身份验证令牌无效：&lt;详细信息&gt; <p>注意： 如果验证器错误，或者使用生产验证器访问<span class="filepath"> *.test.expressplay.com </span>上的测试API时，也会发生这种情况，反之亦然。 </p> <p importance="high">注意： 测试SDK和高级测试工具(ATT)只能用于<span class="filepath"> *.test.expressplay.com </span>，而生产设备必须使用<span class="filepath"> *.service.expressplay.com </span>。 </p> </td> 
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
   <td> 缺少租赁播放持续时间 </td> 
  </tr> 
  <tr> 
   <td> -2025 </td> 
   <td> 租赁播放持续时间无效 </td> 
  </tr> 
  <tr> 
   <td> -2027 </td> 
   <td> 内容加密密钥必须长32个十六进制数字 </td> 
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
   <td> 扩展名类型应为4个字符 </td> 
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
   <td> 《失踪的孩子》 </td> 
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
   <td> <span class="codeph"> ^ </span> 之后长度必须是64个字符 </td> 
  </tr> 
  <tr> 
   <td> -4022 </td> 
   <td> 无效的<span class="codeph">子项</span> </td> 
  </tr> 
  <tr> 
   <td> -4024 </td> 
   <td> 加密密钥或<span class="codeph"> kek </span>无效 </td> 
  </tr> 
  <tr> 
   <td> -5003 </td> 
   <td> 常规标志无效 </td> 
  </tr> 
  <tr> 
   <td> -6001 </td> 
   <td> 指定的<span class="codeph"> FPExtension </span>参数无效 </td> 
  </tr> 
  <tr> 
   <td> -6002 </td> 
   <td> FP令牌类型无效 </td> 
  </tr> 
  <tr> 
   <td> -6003 </td> 
   <td> 指定的<span class="codeph"> iv </span>参数无效 </td> 
  </tr> 
  <tr> 
   <td> -6004 </td> 
   <td> 无法为FP生成CKC </td> 
  </tr> 
  <tr> 
   <td> -6005 </td> 
   <td> 指定的密钥数据无效 </td> 
  </tr> 
  <tr> 
   <td> -6006 </td> 
   <td> 未获得FairPlay支持授权的服务 </td> 
  </tr> 
  <tr> 
   <td> -6007 </td> 
   <td> 指定的租赁持续时间无效 </td> 
  </tr> 
  <tr> 
   <td> -6008 </td> 
   <td> FairPlay不支持设备ID绑定 </td> 
  </tr> 
  <tr> 
   <td> -6009 </td> 
   <td> 禁用了FairPlay选项 </td> 
  </tr> 
 </tbody> 
</table>