---
description: PlayReady许可证令牌界面提供生产和测试服务。
title: PlayReady许可证令牌请求/响应
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 4%

---


# PlayReady许可证令牌请求/响应{#playready-license-token-request-response}

PlayReady许可证令牌界面提供生产和测试服务。

此HTTP请求返回可兑换为PlayReady许可证的令牌。

**方法：GET, POST** （带有www-url编码的正文，其中包含两种方法的参数）

**URL:**

* **生产：** `https://pr-gen.{prod_domain}/hms/pr/token`

* **测试：** ` [https://pr-gen.test.expressplay.com/hms/pr/token](https://pr-gen.test.expressplay.com/hms/pr/token)`

* **示例请求：**

   ```
   <xref href="https: pr-gen.test.expressplay.com="" hms="" pr="" token?customerAuthenticator="201722,1ad8eed133edf43cbcc185f0236828ae&kid=b366360da82e9c6e0b0984002a362cf2&contentKey=b366360da82e9c6e0b0984002a362cf2&rightsType=BuyToOwn&analogVideoOPL=0&compressedDigitalAudioOPL=0&compressedDigitalVideoOPL=0&uncompressedDigitalAudioOPL=0&uncompressedDigitalVideoOPL=0&quot; format=&quot;html&quot; scope=&quot;external&quot;">
   https://pr-gen.test.expressplay.com/hms/pr/token?customerAuthenticator=
    <ExpressPlay customer authenticator identifier>
    &kid=<CEKSID>
    &contentKey=<CEK>
    &rightsType=BuyToOwn
    &analogVideoOPL=0
    &compressedDigitalAudioOPL=0
    &compressedDigitalVideoOPL=0
    &uncompressedDigitalAudioOPL=0
    &uncompressedDigitalVideoOPL=0
   </xref href="https:>
   ```

* **示例响应：**

   ```
   {"licenseAcquisitionUrl":"https://expressplay-licensing.axprod.net/LicensingService.ashx",
               "token":"<base64-encoded ExpressPlay token>"}
   ```

## 请求查询参数{#section_26F8856641A64A46A3290DBE61ACFAD2}

**表9:令牌查询参数**

<table id="table_zxg_dyr_pv">  
 <thead> 
  <tr> 
   <th class="entry"><b>查询参数</b> </th> 
   <th class="entry"><b>说明</b> </th> 
   <th class="entry"><b>需要？</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> customerAuthenticator</span> </td> 
   <td> <p>这是您的客户API密钥，每个密钥针对您的生产和测试环境。 您可以在ExpressPlay管理仪表板选项卡上找到此选项。 </p> </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> errorFormat</span> </td> 
   <td><span class="codeph"> html</span>或<span class="codeph"> json</span>。 如果<span class="codeph"> html</span>（默认）在响应的实体中提供任何错误的HTML表示形式。 <p>如果指定<span class="codeph"> json</span>，则返回JSON格式的结构化响应。 有关详细信息，请参阅<a href="https://www.expressplay.com/developer/restapi/#json-errors" format="html" scope="external"> JSON错误</a>。 </p> <p>响应的MIME类型为：成功时<span class="codeph"> text/uri-列表</span>,HTML错误格式为<span class="codeph"> text/html</span>,JSON错误格式为<span class="codeph"> application/json</span>。 </p> </td> 
   <td> 否 </td> 
  </tr> 
 </tbody> 
</table>

**表10:许可证查询参数**

<table id="table_f1l_fyr_pv">  
 <thead> 
  <tr> 
   <th class="entry"><b>查询参数</b> </th> 
   <th class="entry"><b>说明</b> </th> 
   <th class="entry"><b>需要？</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> generalFlags</span> </td> 
   <td>表示许可证标志的4字节十六进制字符串。 对于永久许可证，必须将其设置为“00000001”。 <p>注意：租赁许可证(<span class="codeph"> rightsType=Rental</span>)必须是永久的。 </p> </td> 
   <td> 否 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 科索沃</span> </td> 
   <td> 密钥加密密钥(KEK)。 密钥使用密钥封装算法（AES密钥封装，RFC3394）通过KEK进行加密存储。 </td> 
   <td> 否 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 小孩</span> </td> 
   <td>内容加密密钥的16字节十六进制字符串表示形式或字符串<span class="codeph"> ^somestring'</span>。 字符串后跟“^”的长度不能大于64个字符。 </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 克</span> </td> 
   <td> 加密内容密钥的十六进制字符串表示形式。 </td> 
   <td> 否 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> contentKey</span> </td> 
   <td> 内容加密密钥的16字节十六进制字符串表示形式 </td> 
   <td>是，除非提供<span class="codeph"> kek</span>和<span class="codeph"> ek</span>或<span class="codeph"> kid</span> </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> rightsType</span> </td> 
   <td>指定权限类型。 必须为<span class="codeph"> BuyToOwn</span>或<span class="codeph"> Rental</span>。 </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> rental.periodEndTime</span> </td> 
   <td>租赁结束日期。 此值必须采用“Z”区域指示符（“祖鲁时间”）格式的“RFC 3339”_日期/时间格式，或前面有“+”符号的整数。 <p>如果值为<a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" scope="external"> RFC 3339</a>日期/时间格式，则表示许可证的绝对过期日期/时间。 RFC 3339的日期/时间示例为2006-04-14T12:01:10Z。 </p> <p> 如果值是前面有“+”符号的整数，则它被视为从发出令牌时起的相对秒数。 此时后无法播放内容。 仅当<span class="codeph"> rightsType</span>为<span class="codeph"> Rental</span>时有效。 </p> </td> 
   <td>是，当<span class="codeph"> rightsType</span>为<span class="codeph"> Rental</span>时。 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> rental.playDuration</span> </td> 
   <td>开始播放后，内容可以播放的时间（以秒为单位）。 仅当<span class="codeph"> rightsType</span>为Rental时有效。 </td> 
   <td> 否 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> analogVideoOPL</span> </td> 
   <td> 指示模拟视频的输出保护级别的整数值。 有效范围0-999。 </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> compressedDigitalAudioOPL</span> </td> 
   <td> 指示压缩数字音频的输出保护级别的整数值。 有效范围0-999。 </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> compressedDigitalVideoOPL</span> </td> 
   <td> 用于指示压缩数字视频的输出保护级别的整数值。 有效范围0-999。 </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> uncompressedDigitalAudioOPL</span> </td> 
   <td> 指示未压缩数字音频的输出保护级别的整数值。 有效范围0-999。 </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> uncompressedDigitalVideoOPL</span> </td> 
   <td> 指示未压缩数字视频的输出保护级别的整数值。 有效范围0-999。 </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> unknownOutputBehavior</span> </td> 
   <td>输出未知时的必需行为。 允许的值：<span class="codeph">允许</span>、<span class="codeph">禁止</span>或<span class="codeph"> SDOnly</span> </td> 
   <td> 否 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> outputControlFlags</span> </td> 
   <td> 一个4字节的十六进制值，用于指示其他输出控制选项的标记 </td> 
   <td> 否 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> extensionType</span> </td> 
   <td>表示扩展的32位标识符的任意4字母字。 每个字母的8位ASCII码是标识符的相应8位字节部分。 例如，将写入标识符值0x61626364（十六进制），因为“a”的ASCII代码为0x61等。<span class="codeph"></span> </td> 
   <td> 否 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> extensionPayload</span> </td> 
   <td> 扩展的base64编码字符串。 </td> 
   <td>是，当指定<span class="codeph"> extensionType</span>时。 </td> 
  </tr> 
 </tbody> 
</table>

## 响应{#section_0079C31B4AF14DBBB6277CF251FB90E3}

**表11:HTTP响应**

| **HTTP状态代码** | **说明** | **内容类型** | **实体正文包含** |
|---|---|---|---|
| `200 OK` | 无错误。 | `text/uri-list` | 许可证获取URL和令牌 |
| `400 Bad Request` | 无效的图 | `text/html` 或  `application/json` | 错误描述 |
| `401 Unauthorized` | 身份验证失败 | `text/html` 或  `application/json` | 错误描述 |
| `404 Not found` | 错误的URL | `text/html` 或  `application/json` | 错误描述 |
| `50x Server Error` | 服务器错误 | `text/html` 或  `application/json` | 错误描述 |

**表12:事件错误代码**

<table id="table_lqb_ycs_pv">  
 <thead> 
  <tr> 
   <th class="entry"><b>代码</b> </th> 
   <th class="entry"><b>说明</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> -2002 </td> 
   <td> 令牌过期时间无效：&lt;详细信息&gt; </td> 
  </tr> 
  <tr> 
   <td> -2003 </td> 
   <td> 无效的IP地址 </td> 
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
   <td>身份验证令牌无效：&lt;详细信息&gt; <p>注意： 如果验证器错误，或使用生产验证器访问*.test.expressplay.com上的测试API时，则会发生这种情况，反之亦然。 </p> <p importance="high">注意：测试SDK和高级测试工具(ATT)只能与<span class="filepath"> *.test.expressplay.com</span>一起使用，而生产设备必须使用<span class="filepath"> *.service.expressplay.com</span>。 </p> </td> 
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
   <td> 内容加密密钥必须长32位十六进制数字 </td> 
  </tr> 
  <tr> 
   <td> -2030 </td> 
   <td> ExpressPlay管理错误：&lt;详细信息&gt; </td> 
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
   <td> 未指定相应值 </td> 
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
   <td><span class="codeph"> </span> OutputControlFlag必须编码4个字节 </td> 
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
   <td> -4018 </td> 
   <td>缺少<span class="codeph">子项</span> </td> 
  </tr> 
  <tr> 
   <td> -4019 </td> 
   <td> 无法从密钥存储服务获取内容密钥 </td> 
  </tr> 
  <tr> 
   <td> -4020 </td> 
   <td><span class="codeph"> 基</span> 德长度必须为32个十六进制字符 </td> 
  </tr> 
  <tr> 
   <td> -4021 </td> 
   <td><span class="codeph"> 在</span> ^之后长度必须为64个字符 </td> 
  </tr> 
  <tr> 
   <td> -4022 </td> 
   <td>无效的<span class="codeph">子项</span> </td> 
  </tr> 
  <tr> 
   <td> -4024 </td> 
   <td>加密的<span class="codeph">密钥</span>或kek无效 </td> 
  </tr> 
  <tr> 
   <td> -5001 </td> 
   <td> 未知输出类型错误无效 </td> 
  </tr> 
  <tr> 
   <td> -5002 </td> 
   <td> 此服务禁用了PlayReady选项 </td> 
  </tr> 
  <tr> 
   <td> -5003 </td> 
   <td> 常规标志无效 </td> 
  </tr> 
  <tr> 
   <td> -5004 </td> 
   <td> 设备ID必须长32个十六进制字符 </td> 
  </tr> 
  <tr> 
   <td> -5005 </td> 
   <td> 设备ID无效 </td> 
  </tr> 
  <tr> 
   <td> -5006 </td> 
   <td> 缺少OPL值 </td> 
  </tr> 
  <tr> 
   <td> -5007 </td> 
   <td>只能指定<span class="codeph"> kek</span>或<span class="codeph"> contentKey</span>中的一个 </td> 
  </tr> 
 </tbody> 
</table>
