---
description: 本节介绍一个说明配置概念和形式的示例配置。
seo-description: 本节介绍一个说明配置概念和形式的示例配置。
seo-title: 示例RBOP配置
title: 示例RBOP配置
uuid: fa5ead93-36c5-4ad1-947b-c4f1f2632d9b
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---


# 示例RBOP配置{#sample-rbop-configuration}

本节介绍一个说明配置概念和形式的示例配置。

以下JSON配置示例定义了一个像素输出策略，它指定以下内容：

* 将视频解密限制为1080或更低分辨率
* 对第720和480号决议施加具体限制：

   * 对于720号决议：需要HDCP进行数字输出；需要&#x200B;*复制生成管理系统——模拟*(CGMS-A)保护以进行模拟输出。
   * 480号决议：需要HDCP进行数字输出；不需要模拟保护

```
{ 
  "pixelConstraints":  
    [ 
      { 
        "pixelCount": 720, 
        "digital": 
          [ 
            {"output": "REQUIRED", "hdcp": {"major": 1, "minor": 0}} 
          ], 
        "analog": {"output": "REQUIRED_CGMSA"} 
      }, 
      { 
        "pixelCount": 480, 
        "digital":  
          [ 
            {"output": "REQUIRED", "hdcp": {"major": 1, "minor": 0}} 
          ], 
        "analog": {"output": "NO_PROTECTION"} 
      } 
    ], 
  "maxPixel": 1080 
}
```

请注意上述示例配置的以下信息：

* `pixelCount`规范在JSON结构中的`pixelConstraints`部分下一级。

* 在每个像素计数规范中，为数字和模拟输出指定输出保护。
* 在数字输出规范中，指定了HDCP版本，但客户端当前不支持HDCP版本控制。 有关更多信息，请参阅常见问题解答。

