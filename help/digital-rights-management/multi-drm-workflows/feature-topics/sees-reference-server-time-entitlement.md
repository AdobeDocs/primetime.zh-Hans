---
description: 与SEES合作，了解如何使用ExpressPlay启用基于时间的授权服务。
title: 参考服务基于时间的授权
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---


# 参考服务：基于时间的授权{#reference-service-time-based-entitlement}

与SEES合作，了解如何使用ExpressPlay启用基于时间的授权服务。

SEES从客户端接收授权请求（请参阅“公共API”部分）。 SEES服务器根据`contentID`查找CEK和IV，添加`expirationTime`，并将请求转发到ExpressPlay服务器。 最终的ExpressPlay令牌有时间限制。 请参阅下面的基于时间的授权序列图。![](assets/fees-time-based.png)

**表1:客户端发送的许可证参数**

| 查询参数 | 说明 | 必需 |
|---|---|---|
| `contentKey` | 内容加密密钥的16字节十六进制字符串表示形式 | 是 |
| `iv` | 内容加密IV的16字节十六进制字符串表示形式 | 是 |
| `rentalDuration` | 租金的持续时间（以秒为单位）（默认值= 0） | 否 |

**表2:由SEES Server添加的令牌限制参数**

<table id="table_E979FAD7A61A4832A46667301939FAEB">  
 <thead> 
  <tr> 
   <th class="entry"> 查询参数 </th> 
   <th class="entry"> 说明 </th> 
   <th class="entry"> 需要？ </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> expirationTime</span> </td> 
   <td>此令牌的过期时间。 此值必须是<a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" type="external"> RFC 3339</a>中“Z”区域指示符（“祖鲁时间”）日期/时间格式的字符串，或前面带“+”符号的整数。 RFC 3339的日期/时间示例为<span class="codeph"> 2006-04-14T12:01:10Z</span>。 <p>如果该值是RFC 3339日期/时间格式的字符串，则它表示令牌的绝对过期日期/时间。 如果值是前面有“+”符号的整数，则它被解释为从发出令牌后相对秒数（表示令牌有效）。 例如，<span class="codeph"> +60</span>指定一分钟。 令牌生存期的最大值（和默认值，如果未指定）为30天。 指定“+”符号时使用编码表单“%2B”。 </p> </td> 
   <td> 否 </td> 
  </tr> 
 </tbody> 
</table>

