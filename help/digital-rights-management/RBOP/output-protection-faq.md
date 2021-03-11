---
description: 有关使用基于分辨率的输出保护的常见问题。
title: RBOP常见问题解答
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---


# RBOP常见问题解答{#rbop-faq}

有关使用基于分辨率的输出保护的常见问题。

* **问：** *在定义像素约束的数字输出要求时，当我离开HDCP版本时，我会收到解析/格式化错误，但我没有任何HDCP要求。在这种情况下，我应如何配置数字输出要求？* **答：由** 于客户端当前不支持HDCP版本检查，Adobe建议将HDCP版本设置为 `1.0`。这将确保您的配置格式正确，并且在支持HDCP版本检查时，在语义上保持一致。 以下代码片断说明了使用此HDCP值的配置。

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

* **问：RBOP** *像素约束是离散的还是基于范围的？* **A.RBOP** 像素约束是基于的。如果存在多个像素约束，则每个像素计数定义所有小于或等于给定计数的像素计数的要求，或最大小于该值的像素计数。 简而言之，这些值将作为每个垂直像素计数的最大阈值应用。

   假设具有垂直分辨率240、480、600、720和1080的MBR流会通过以下RBOP设置传递到您的播放器。

   **RBOP策略设置：**

   * 720P — 需要HDCP
   * 480P — 无操作

   以下规则将应用于每个变体。

   **流：**

   * 240, 480:两者均为&lt;= 480;不需要OP，流将随HDCP一起加载或不存在HDCP。
   * 600, 720:两者均为&lt;= 720;回放需要HDCP
   * 1080:> 720;流是列出的块（返回错误），因为在上述规则中找不到它。


* **问：** 在我的某些Android设备上，我定义的像素计数限制未完全按定义应用。发生了什么？

   **回答：** 某些Android设备的报告帧大小比正常大小略高。要纠正这种情况，请将帧大小（`maxPixel`和`pixelCount`设置）向上调整20像素。 例如，从以下位置向上调整帧大小设置：

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

   to:

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

   对于所有`maxPixel`和`pixelCount`实例。

