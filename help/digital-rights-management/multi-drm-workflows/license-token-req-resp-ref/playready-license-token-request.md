---
description: PlayReady许可证令牌界面提供生产和测试服务。
title: PlayReady许可证令牌请求/响应
exl-id: 12f925f7-336b-42b2-95a9-e806801bab8c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 4%

---

# PlayReady许可证令牌请求/响应 {#playready-license-token-request-response}

PlayReady许可证令牌界面提供生产和测试服务。

此HTTP请求返回可为PlayReady许可证兑换的令牌。

**方法：GET、POST** （使用www-url编码的主体，其中包含这两种方法的参数）

**URL：**

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

## 请求查询参数 {#section_26F8856641A64A46A3290DBE61ACFAD2}

**表9：令牌查询参数**

<table id="table_zxg_dyr_pv">  
 <thead> 
  <tr> 
   <th class="entry"><b>查询参数</b> </th> 
   <th class="entry"><b>描述</b> </th> 
   <th class="entry"><b>必需？</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> customerAuthenticator</span> </td> 
   <td> <p>这是您的客户API密钥，每个密钥分别用于生产和测试环境。 您可以在“ExpressPlay管理功能板”选项卡上找到它。 </p> </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 错误格式</span> </td> 
   <td>可以 <span class="codeph"> html</span> 或 <span class="codeph"> json</span>. 如果 <span class="codeph"> html</span> （缺省）在响应的图元主体中提供任何错误的HTML表示形式。 <p>如果 <span class="codeph"> json</span> 指定，则会返回JSON格式的结构化响应。 参见 <a href="https://www.expressplay.com/developer/restapi/#json-errors" format="html" scope="external"> JSON错误</a> 了解详细信息。 </p> <p>响应的MIME类型为 <span class="codeph"> text/uri-list</span> 成功时， <span class="codeph"> text/html</span> (对于HTML错误格式)，或 <span class="codeph"> application/json</span> （对于JSON错误格式）。 </p> </td> 
   <td> 否 </td> 
  </tr> 
 </tbody> 
</table>

**表10：许可证查询参数**

<table id="table_f1l_fyr_pv">  
 <thead> 
  <tr> 
   <th class="entry"><b>查询参数</b> </th> 
   <th class="entry"><b>描述</b> </th> 
   <th class="entry"><b>必需？</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> generalFlags</span> </td> 
   <td>表示许可证标记的4字节十六进制字符串。 永久许可证必须将其设置为“00000001”。 <p>注意：租赁许可证(<span class="codeph"> rightsType=租赁</span>)必须是永久性的。 </p> </td> 
   <td> 否 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> kek</span> </td> 
   <td> 密钥加密密钥(KEK)。 密钥是使用密钥封装算法(AES Key Wrap，RFC3394)通过KEK加密存储的。 </td> 
   <td> 否 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 小孩</span> </td> 
   <td>内容加密密钥或字符串的16字节十六进制字符串表示形式 <span class="codeph"> ^somestring'</span>. “^”后跟字符串的长度不能超过64个字符。 </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> ek</span> </td> 
   <td> 加密内容密钥的十六进制字符串表示形式。 </td> 
   <td> 否 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> contentkey</span> </td> 
   <td> 内容加密密钥的16字节十六进制字符串表示形式 </td> 
   <td>是，除非 <span class="codeph"> kek</span> 和 <span class="codeph"> ek</span> 或 <span class="codeph"> 小孩</span> 提供 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> righttype</span> </td> 
   <td>指定权限的种类。 必须是 <span class="codeph"> BuyTown</span> 或 <span class="codeph"> 租金</span>. </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> rental.periodEndTime</span> </td> 
   <td>租赁结束日期。 此值必须采用“RFC 3339”的“Z”区域指示符（“Zulu时间”）格式的日期/时间格式，或采用“+”符号前面的整数。 <p>如果值是 <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" scope="external"> RFC 3339</a> 日期/时间格式，则它表示许可证的绝对到期日期/时间。 RFC 3339日期/时间的示例为2006-04-14T12:01:10Z。 </p> <p> 如果该值是带有“+”号的整数，则会将其视为从颁发令牌开始算起的相对秒数。 内容在此时间后无法播放。 仅在以下情况下有效 <span class="codeph"> righttype</span> 是 <span class="codeph"> 租金</span>. </p> </td> 
   <td>是，当 <span class="codeph"> righttype</span> 是 <span class="codeph"> 租金</span>. </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> rental.playDuration</span> </td> 
   <td>开始播放后可以播放内容的时间（以秒为单位）。 仅在以下情况下有效 <span class="codeph"> righttype</span> 是租赁。 </td> 
   <td> 否 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> analogVideoOPL</span> </td> 
   <td> 表示模拟视频的输出保护级别的整数值。 有效范围为0-999。 </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> compressedDigitalAudioOPL</span> </td> 
   <td> 表示压缩数字音频的输出保护级别的整数值。 有效范围为0-999。 </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> compressedDigitalVideoOPL</span> </td> 
   <td> 表示压缩数字视频的输出保护级别的整数值。 有效范围为0-999。 </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 未压缩的DigitalAudioOPL</span> </td> 
   <td> 表示未压缩数字音频的输出保护级别的整数值。 有效范围为0-999。 </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 未压缩的DigitalVideoOPL</span> </td> 
   <td> 表示未压缩数字视频的输出保护级别的整数值。 有效范围为0-999。 </td> 
   <td> 是 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> unknownOutputBehavior</span> </td> 
   <td>输出未知时的必需行为。 允许的值： <span class="codeph"> 允许</span>， <span class="codeph"> 不允许</span> 或 <span class="codeph"> SDOnly</span> </td> 
   <td> 否 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> outputControlFlags</span> </td> 
   <td> 一个4字节的十六进制值，用于指示其他输出控制选项的标志 </td> 
   <td> 否 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> extensiontype</span> </td> 
   <td>表示扩展的32位标识符的任意4字母单词。 每个字母的8位ASCII代码都是标识符对应的8位字节部分。 例如，标识符值0x61626364 （十六进制）将被写入'<span class="codeph"> abcd</span>'，因为'a'的ASCII代码为0x61，以此类推。 </td> 
   <td> 否 </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> extensionPayload</span> </td> 
   <td> 扩展的base64编码字符串。 </td> 
   <td>是，当 <span class="codeph"> extensiontype</span> 已指定。 </td> 
  </tr> 
 </tbody> 
</table>

## 响应 {#section_0079C31B4AF14DBBB6277CF251FB90E3}

**表11： HTTP响应**

| **HTTP状态代码** | **描述** | **内容类型** | **实体正文包含** |
|---|---|---|---|
| `200 OK` | 没有错误。 | `text/uri-list` | 许可证客户获取url和令牌 |
| `400 Bad Request` | 参数无效 | `text/html` 或 `application/json` | 错误描述 |
| `401 Unauthorized` | 身份验证失败 | `text/html` 或 `application/json` | 错误描述 |
| `404 Not found` | 错误的URL | `text/html` 或 `application/json` | 错误描述 |
| `50x Server Error` | 服务器错误 | `text/html` 或 `application/json` | 错误描述 |

**表12：事件错误代码**

<table id="table_lqb_ycs_pv">  
 <thead> 
  <tr> 
   <th class="entry"><b>代码</b> </th> 
   <th class="entry"><b>描述</b> </th> 
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
   <td>身份验证令牌无效： &lt;details&gt; <p>注意：如果验证器错误或者使用生产验证器在*.test.expressplay.com上访问测试API时，可能会发生这种情况，反之亦然。 </p> <p importance="high">注意：测试SDK和高级测试工具(ATT)仅适用于 <span class="filepath"> *.test.expressplay.com</span>，而生产设备必须使用 <span class="filepath"> *.service.expressplay.com</span>. </p> </td> 
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
   <td><span class="codeph"> OutputControlFlag</span> 必须为4个字节编码 </td> 
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
   <td> -4018 </td> 
   <td>缺失 <span class="codeph"> 小孩</span> </td> 
  </tr> 
  <tr> 
   <td> -4019 </td> 
   <td> 无法从密钥存储服务获取内容密钥 </td> 
  </tr> 
  <tr> 
   <td> -4020 </td> 
   <td><span class="codeph"> 小孩</span> 长度必须为32个十六进制字符 </td> 
  </tr> 
  <tr> 
   <td> -4021 </td> 
   <td><span class="codeph"> 小孩</span> ^后必须为64个字符 </td> 
  </tr> 
  <tr> 
   <td> -4022 </td> 
   <td>无效 <span class="codeph"> 小孩</span> </td> 
  </tr> 
  <tr> 
   <td> -4024 </td> 
   <td>加密无效 <span class="codeph"> 键</span> 或kek </td> 
  </tr> 
  <tr> 
   <td> -5001 </td> 
   <td> 无效的未知输出类型错误 </td> 
  </tr> 
  <tr> 
   <td> -5002 </td> 
   <td> 已为此服务禁用PlayReady选项 </td> 
  </tr> 
  <tr> 
   <td> -5003 </td> 
   <td> 常规标志无效 </td> 
  </tr> 
  <tr> 
   <td> -5004 </td> 
   <td> 设备ID长度必须为32个十六进制字符 </td> 
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
   <td>只有一个 <span class="codeph"> kek</span> 或 <span class="codeph"> contentkey</span> 可以指定 </td> 
  </tr> 
 </tbody> 
</table>
