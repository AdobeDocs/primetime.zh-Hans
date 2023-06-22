---
description: 与SEE合作，了解如何使用ExpressPlay启用基于时间的授权服务。
title: 参考服务基于时间的授权
exl-id: a37b0e71-ba7b-4f03-9866-5e8b062e0b7d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# 参考服务：基于时间的授权 {#reference-service-time-based-entitlement}

与SEE合作，了解如何使用ExpressPlay启用基于时间的授权服务。

SEE从客户端接收授权请求（请参阅公共API部分）。 SES服务器查找CEK和IV，根据 `contentID`，添加 `expirationTime`，并将请求转发到ExpressPlay服务器。 最终的ExpressPlay令牌具有时间限制。 请参阅下面的基于时间的权利序列图。 ![](assets/fees-time-based.png)

**表1：客户端发送的许可证参数**

| 查询参数 | 描述 | 必需 |
|---|---|---|
| `contentKey` | 内容加密密钥的16字节十六进制字符串表示形式 | 是 |
| `iv` | 内容加密IV的16字节十六进制字符串表示形式 | 是 |
| `rentalDuration` | 租用的持续时间（以秒为单位，默认值= 0） | 否 |

**表2：由SEES服务器添加的令牌限制参数**

<table id="table_E979FAD7A61A4832A46667301939FAEB">  
 <thead> 
  <tr> 
   <th class="entry"> 查询参数 </th> 
   <th class="entry"> 描述 </th> 
   <th class="entry"> 必需？ </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> expirationTime</span> </td> 
   <td>此令牌的过期时间。 此值必须是中的字符串 <a href="https://www.ietf.org/rfc/rfc3339.txt" format="html" type="external"> RFC 3339</a> “Z”区域指示符中的日期/时间格式（“Zulu时间”），或以“+”符号开头的整数。 RFC 3339日期/时间的示例为 <span class="codeph"> 2006-04-14T12:01:10Z</span>. <p>如果值是RFC 3339日期/时间格式的字符串，则它表示令牌的绝对过期日期/时间。 如果该值是带有“+”号的整数，则它将被解释为从颁发起令牌有效的相对秒数。 例如， <span class="codeph"> +60</span> 指定一分钟。 最长令牌生命周期（如果未指定，则默认为30天）。 指定“+”符号时使用编码形式“%2B”。 </p> </td> 
   <td> 否 </td> 
  </tr> 
 </tbody> 
</table>
