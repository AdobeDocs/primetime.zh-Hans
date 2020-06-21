---
description: 有关使用基于分辨率的输出保护的常见问题。
seo-description: 有关使用基于分辨率的输出保护的常见问题。
seo-title: RBOP常见问题解答
title: RBOP常见问题解答
uuid: 7dcd337c-369a-474c-8768-409c48b5cee5
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%

---


# RBOP常见问题解答 {#rbop-faq}

有关使用基于分辨率的输出保护的常见问题。

* **问：** 定 *义像素约束的数字输出要求时，我在将HDCP版本保留为不存在时会收到解析／格式错误，但我没有任何HDCP要求。 在这种情况下，我应如何配置数字输出要求？* **答：** 由于客户端当前不支持HDCP版本检查，Adobe建议将HDCP版本设置为 `1.0`。 这将确保您的配置格式正确，并且在将来支持HDCP版本检查时在语义上保持一致。 以下代码片断说明了使用此HDCP值的配置。

   ```
   { "pixelConstraints":  
     [  
       { "pixelCount": 720, "digital":  
         [  
           {  
             "output": "REQUIRED", "hdcp": {"major": 1, "minor": 0}  
           }  
         ]  
       }  
     ]  
   }
   ```

* **问：RBOP** 像 *素约束是离散的还是基于范围的？* **A.** RBOP像素约束是基于范围的。 如果存在多个像素约束，则每个像素计数定义小于或等于给定计数的所有像素计数的要求，或者最大小于该值的计数。 简而言之，这些值将作为每个垂直像素计数的最大阈值应用。

   假设垂直分辨率为240、480、600、720和1080的MBR流会通过以下RBOP设置传递到您的播放器。

   **RBOP策略设置：**

   * 720P —— 需要HDCP
   * 480P —— 无OP
   以下规则将应用于每个变体。

   **流：**

   * 240, 480: 都&lt;= 480; 无需OP，流将在HDCP存在或没有HDCP的情况下加载。
   * 600, 720: 都&lt;= 720; 回放需要HDCP
   * 1080: > 720; 流是列出的块（返回错误），因为在上述规则中找不到它。


* **问** ：在我的某些Android设备上，我定义的像素计数限制并未完全按定义应用。 发生什么了？

   **答：** 某些Android设备的报告帧大小比正常大小略高。 要纠正这种情况，请将帧大小(和 `maxPixel` 设置) `pixelCount` 向上调整20像素。 例如，从以下位置向上调整帧大小设置：

   ```
   { 
       "maxPixel":  
   
<b>800</b>,&quot;pixelConstraints&quot;: [{ &quot;pixelCount&quot;:\
<b>532</b>,“数字”: [{&quot;output&quot;: “必需”、“hdcp”:{“主要”: 1,&quot;minor&quot;: 0}}],“模拟”: {&quot;output&quot;: &quot;必需&quot;}},...

```
to: 
```
{&quot;maxPixel&quot;:\
<b>820</b>,&quot;pixelConstraints&quot;: [{ &quot;pixelCount&quot;:\
<b>552</b>,“数字”: [{&quot;output&quot;: “必需”、“hdcp”:{“主要”: 1,&quot;minor&quot;: 0}}],“模拟”: {&quot;output&quot;: &quot;必需&quot;}},...

```
throughout, for all instances of `maxPixel` and `pixelCount`.

