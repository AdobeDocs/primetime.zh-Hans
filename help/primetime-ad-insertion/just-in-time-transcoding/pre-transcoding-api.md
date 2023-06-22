---
title: 预转码API
description: 您可以使用及时重新打包API提前对广告创意进行转码，以便在需要时提供内容兼容版本，从而消除与即时(JIT)重新打包相关的2到4分钟延迟。
exl-id: d45668e0-ec8a-4e5a-a56b-cffff27561f2
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 0%

---

# 预转码和重新打包API {#pre-transcoding-api}

PrimetimeAd Insertion为提前知道创意URL的情况（例如大型直销活动）提供了一个预转码API。  这消除了与即时的转码相关的2-4分钟的延迟。

## HTTP请求 {#section_F616F5722F0B4AB7939EE2ECBEDDB297}

向指定的URL发送HTTPPOST命令，以告知CRS您希望对哪些广告创意进行转码以及您希望它使用哪些选项。 响应代码报告成功或失败以及其他信息。

此请求需要用户名和密码。 您可以从Adobe技术客户经理处获取这些信息。 如果您需要有关身份验证的信息，请联系您的Adobe Primetime启用代表。

要向CRS提交转码请求，请发送HTTP消息，如下所示：

* **URL -** [https://id3.auditude.com/repackage](https://id3.auditude.com/repackage)

* **方法 —** `POST`

* **身份验证 —** `Digest`

* **页眉 —** `Content-Type: text/xml`

* **正文 —** XML，如下例所示：

   ```xml
   <RepackageList>
       <Repackage>
           <AdSystem>Auditude</AdSystem>
           <AdID>AUD1</AdID>
           <CreativeID>AUD-CR1</CreativeID>
           <CreativeURL>https://cdn.auditude.com/assets/ip/starbucks2.mp4</CreativeURL>
           <Zone>3</Zone>
       </Repackage>
       <Repackage>
           <AdSystem>Auditude</AdSystem>
           <AdID>AUD2</AdID>
           <CreativeID>AUD-CR1</CreativeID>
           <CreativeURL>https://cdn.auditude.com/assets/ip/starbucks2.mp4</CreativeURL>
           <Format>id3 targetdur=5</Format>
           <Zone>3</Zone>
       </Repackage>
   </RepackageList>
   ```

此 `RepackageList` 正文中的块可以包含1到300 `Repackage` 块。 如果 `Repackage` 正文中的块数超过300，则HTTP请求将失败，并出现以下错误：

```
<codeph>
 HTTP 413 Request Entity Too Large: Validation fail: Too many
     requests. Max limit is 300
</codeph>.
```


中的必需和可选参数 `Repackage` 块如下所示：

* **`AdSystem`** （必需） — 源广告服务器，例如， `Auditude`， `FreeWheel`， `Apad.tv`. 这是一个与VAST元素对应的字符串值 `AdSystem`.

* **`AdId`** （必需） — 这是请求中指定的第三方广告服务器的标识符。 它对应于 `id` 的属性 `Ad` VAST响应中的元素。

* **`CreativeURL`** （必需） — 要转码的广告创意的位置(URI)。 这对应于VAST `MediaFile` 元素。

* `CreativeID` （可选） — 要作为广告体验的一部分包含的广告创意的标识符。
* **`Zone`** （必需） — 帐户的区域ID（从技术客户经理处获取）。 这是一个与Auditude平台对应的数值 `publisher_site_id` 设置。

* **`Format`** （可选） — 用于控制CRS如何对广告创意进行转码的参数：

   * `clientside`  — 生成与TVSDK用于与CDN通信的URL兼容的输出。
   >[!IMPORTANT]
   >
   >如果您希望重新打包的广告与客户端Ad Insertion兼容，则必须提供此参数。 如果不提供此功能，则重新打包的广告将仅与服务器端Ad Insertion兼容。

   * `hls`  — 生成与HLS兼容的转码广告创意。
   * `dash`  — 生成与DASH兼容的转码广告创意。
   * `id3`  — 将ID3定时元数据标记插入到转码的广告创意中。
   * `targetdur`  — 转码广告创意的区段持续时间（秒）。 默认为 `targetdur=4`. 此值应与清单中指定的值对应 `<s>` 在目标持续时间标记中： `#EXT-X-TARGETDURATION:<s>`.

   >[!NOTE]
   >
   >与DASH兼容的资源与Adobe Primetime广告插入不兼容。

>[!IMPORTANT]
>
>要确保最流畅的播放，请设置 `targetdur` 以匹配内容区块持续时间。

## HTTP响应 {#section_B30D27E4A6AC4AAD9E758162EFF7D963}

CRS使用以下状态代码之一来响应请求：

* **HTTP 202**  — 已接受（正文为空）。 这表示成功。 CRS会将转码广告上传到CDN服务器。
* **HTTP 400**  — 错误请求。 已发布的XML无效。
* **HTTP 500**  — 内部服务器错误。 服务器遇到内部问题（例如，服务器无法连接到数据库）。

## 为SSAI或CSAI预转码资产 {#section_098888BB74FD4DC1AD0BD507B2A48318}

使用重新打包API，您可以对将来的SSAI或CSAI事件进行预编码。 如果资源将来要与SSAI一起使用，请确保POST调用中的所有参数都是唯一的。 参数为：AdSystem、AdId、CreativeURL、Zone、Format。 该组参数中的任何差异都会导致SSAI产生新的转码请求。

对于将来与CSAI一起使用的资产，资产的唯一性取决于Zone和CreativeURL。 AdSystem和AdId不会生成不同的转码资产，并且这些资产可供客户端使用。
