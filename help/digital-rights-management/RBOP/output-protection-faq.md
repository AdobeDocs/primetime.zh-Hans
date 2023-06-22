---
description: 有关使用基于分辨率的输出保护的常见问题解答。
title: rbop常见问题解答
exl-id: 16b95db4-43a9-4458-b7f4-94033a36542e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# rbop常见问题解答 {#rbop-faq}

有关使用基于分辨率的输出保护的常见问题解答。

* **问：** *为像素限制定义数字输出要求时，当我将HDCP版本保留在外时会收到解析/格式错误，但是我没有任何HDCP要求。 在这种情况下，我应如何配置数字输出要求？* **答：** 由于客户端当前不支持HDCP版本检查，因此Adobe建议将HDCP版本设置为 `1.0`. 这将确保配置格式正确，并且将来支持HDCP版本检查时在语义上保持一致。 以下代码片段说明了具有此HDCP值的配置。

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

* **问：** *RBOP像素约束是离散的还是基于范围的？* **答：** RBOP像素约束是基于范围的。 每个像素计数定义小于或等于给定计数的所有像素计数的需求，如果存在多个像素约束，则最大像素计数小于该值。 简而言之，这些值将用作每个垂直像素计数的最大阈值。

   假设使用以下RBOP设置向播放器传递垂直分辨率为240、480、600、720和1080的MBR流。

   **RBOP策略设置：**

   * 720P — 需要HDCP
   * 480P — 无操作

   以下规则将应用于每个变体。

   **流：**

   * 240， 480：两者都小于= 480；不需要OP，并且无论是否存在HDCP，都将加载流。
   * 600、720：两者都小于= 720；播放时需要HDCP
   * 1080： > 720；流被列入阻止列表（返回错误），因为在上面的规则中未找到它。


* **问：** 在我的一些Android设备上，我定义的像素计数限制没有完全按照定义应用。 发生什么事了？

   **答：** 某些Android设备报告的帧大小略高于正常大小。 要解决这种情况，请调整帧大小( `maxPixel` 和 `pixelCount` settings)增加20像素。 例如，从以下位置向上调整帧大小设置：

   ```
   { 
       "maxPixel": 800, 
       "pixelConstraints": [ 
           { "pixelCount": 532, 
             "digital": [{"output": "REQUIRED", "hdcp":{"major": 1,"minor": 0}}], 
             "analog": {"output": "REQUIRED"} 
           }, 
   ... 
   ```

   至：

   ```
   { 
       "maxPixel": 820, 
       "pixelConstraints": [ 
           { "pixelCount": 552, 
             "digital": [{"output": "REQUIRED", "hdcp":{"major": 1,"minor": 0}}], 
             "analog": {"output": "REQUIRED"} 
           }, 
   ... 
   ```

   在整个，对于所有实例 `maxPixel` 和 `pixelCount`.
