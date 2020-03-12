---
description: 与SEES合作，了解如何使用ExpressPlay启用基于时间的授权服务。
seo-description: 与SEES合作，了解如何使用ExpressPlay启用基于时间的授权服务。
seo-title: 参考服务基于时间的授权
title: 参考服务基于时间的授权
uuid: dd937299-a271-49a9-9b26-eec16f1484df
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c

---


# 参考服务：基于时间的授权 {#reference-service-time-based-entitlement}

与SEES合作，了解如何使用ExpressPlay启用基于时间的授权服务。

SEES从客户端接收授权请求（请参阅公共API部分）。 SEES服务器基于查找、添加请求 `contentID`并将请求转 `expirationTime`发到ExpressPlay服务器。 最终的ExpressPlay令牌有时间限制。 请参阅下面的基于时间的授权序列图。 ![](assets/fees-time-based.png)

**表1:客户端发送的许可证参数**

| 查询参数 | 说明 | 必需 |
|---|---|---|
| `contentKey` | 内容加密密钥的16字节十六进制字符串表示形式 | 是 |
| `iv` | 内容加密IV的16字节十六进制字符串表示形式 | 是 |
| `rentalDuration` | 租金的持续时间（以秒为单位）（默认值= 0） | 否 |

**表2:SEES Server添加的令牌限制参数**

<table id="table_E979FAD7A61A4832A46667301939FAEB">  
 <thead> 
  <tr> 
   <th class="entry"> 查询参数 </th> 
   <th class="entry"> 说明 </th> 
   <th class="entry"> 必需？ </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> expirationTime</span> </td> 
   <td>此令牌的过期时间。 此值必须是 <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" type="external"> RFC 3339</a> 、“Z”区域指示符（“祖鲁时间”）中的日期／时间格式字符串，或前面有“+”符号的整数。 RFC 3339的日期／时间示例为 <span class="codeph"> 2006-04-14T12:01:10Z</span>。 <p>如果该值是RFC 3339日期／时间格式的字符串，则它表示令牌的绝对过期日期／时间。 如果值是前面有“+”符号的整数，则它被解释为从发出令牌后的相对秒数（表示令牌有效）。 例如， <span class="codeph"> +60</span> 指定一分钟。 令牌的最大期限（和默认期限，如果未指定）为30天。 指定“+”符号时，请使用编码表单“%2B”。 </p> </td> 
   <td> 否 </td> 
  </tr> 
 </tbody> 
</table>

