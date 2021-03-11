---
description: 您可以使用CRS重新打包API提前对非HLS广告创意进行转码，因此在需要运行HLS版本时可用，从而消除了与即时(JIT)重新打包相关的2-4分钟延迟。
title: 重新打包API
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 0%

---


# 重新打包API {#repackaging-api}

您可以使用CRS重新打包API提前对非HLS广告创意进行转码，因此在需要运行HLS版本时可用，从而消除了与即时(JIT)重新打包相关的2-4分钟延迟。

## HTTP请求{#section_F616F5722F0B4AB7939EE2ECBEDDB297}

将HTTPPOST命令发送到指定的URL，以告知CRS要转码的广告创意以及希望它使用的选项。 响应代码报告成功或失败以及其他信息。

此请求需要用户名和密码。 您可以从您的Adobe技术客户经理处获得这些。 如果您需要有关身份验证的信息，请与Adobe Primetime Enablement代表联系。

要向CRS提交转码请求，请按如下方式发送HTTP消息：

* **URL -** [https://id3.auditude.com/repackage](https://id3.auditude.com/repackage)

* **方法 —** `POST`

* **身份验证 —** `Digest`

* **标题 —** `Content-Type: text/xml`

* **Body -** XML，如下例所示：

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

Body中的`RepackageList`块可以包含1到300个`Repackage`块。 如果正文中`Repackage`块的数量超过300，则HTTP请求将失败，并出现以下错误：

```
<codeph>
 HTTP 413 Request Entity Too Large: Validation fail: Too many
     requests. Max limit is 300
</codeph>.
```


`Repackage`块中的必需和可选参数如下所示：

* **`AdSystem`** （必需） — 源广告服务器，例如 `Auditude`, `FreeWheel`、 `Apad.tv`。这是与VAST元素`AdSystem`对应的字符串值。

* **`AdId`** （必需） — 这是请求中指定的第三方广告服务器的标识符。它对应于VAST响应中`Ad`元素的`id`属性。

* **`CreativeURL`** （必需） — 要转码的广告创意的位置(URI)。这对应于VAST `MediaFile`元素。

* `CreativeID` （可选） — 要作为广告体验的一部分包含的广告创意的标识符。
* **`Zone`** （必需） — 您帐户的区域ID（从您的技术客户经理处获取）。这是与Auditude平台`publisher_site_id`设置相对应的数值。

* **`Format`** （可选） — 控制CRS如何转码广告创意的参数：

   * `clientside`  — 生成与TVSDK用来与CDN通信的URL兼容的输出。
   >[!IMPORTANT]
   >
   >如果希望重新打包的广告与客户端Ad Insertion兼容，则必须提供此参数。 如果您不提供，则重新打包的广告将仅与服务器端Ad Insertion兼容。

   * `hls`  — 生成与HLS兼容的转码广告创意。
   * `dash`  — 生成与DASH兼容的转码广告创意。
   * `id3`  — 将ID3定时元数据标记插入转码广告创意。
   * `targetdur`  — 转码广告创意的细分持续时间（以秒为单位）。默认值为`targetdur=4`。 此值应与目标持续时间标签中清单中为`<s>`指定的值相对应：`#EXT-X-TARGETDURATION:<s>`。

   >[!NOTE]
   >
   >与DASH兼容的资源与Adobe Primetime广告插入不兼容。

>[!IMPORTANT]
>
>要确保播放最顺畅，请设置`targetdur`以匹配内容块持续时间。

## HTTP响应{#section_B30D27E4A6AC4AAD9E758162EFF7D963}

CRS使用以下状态代码之一响应请求：

* **HTTP 202**  — 已接受（正文为空）。这表示成功。 CRS将转码广告上传到CDN服务器。
* **HTTP 400**  — 错误请求。发布的XML无效。
* **HTTP 500**  — 内部服务器错误。服务器遇到内部问题（例如，服务器无法连接到数据库）。

## 为SSAI或CSAI {#section_098888BB74FD4DC1AD0BD507B2A48318}预转码资源

使用重新打包API，您可以预转码将来的SSAI或CSAI事件。 如果资产打算在将来与SSAI一起使用，请确保POST调用中的所有参数都是唯一的。 参数有：AdSystem、AdId、CreativeURL、区域、格式。 此参数集中的任何差异都会导致对SSAI的新转码请求。

对于将来与CSAI一起使用的资产，资产的唯一性取决于Zone和CreativeURL。 AdSystem和AdId不会导致不同的转码资产，这些资产对客户端可用。
