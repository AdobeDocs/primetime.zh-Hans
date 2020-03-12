---
description: 本节介绍一个说明配置概念和形式的示例配置。
seo-description: 本节介绍一个说明配置概念和形式的示例配置。
seo-title: 示例RBOP配置
title: 示例RBOP配置
uuid: fa5ead93-36c5-4ad1-947b-c4f1f2632d9b
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# 示例RBOP配置 {#sample-rbop-configuration}

本节介绍一个说明配置概念和形式的示例配置。

以下JSON配置示例定义了一个像素输出策略，该策略指定以下内容：

* 将视频解密限制为1080或更低分辨率
* 对第720和480号决议施加具体限制：

   * 对于720号决议：需要HDCP进行数字输出；需要 *复制生成管理系统——模拟* (CGMS-A)保护以实现模拟输出。
   * 对于480号决议：需要HDCP进行数字输出；不需要模拟保护

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

请注意上述示例配置的以下相关信息：

* 在 `pixelCount` JSON结构中，规范在部分中向下一级 `pixelConstraints` 。

* 在每个像素计数规范中，为数字和模拟输出指定输出保护。
* 在数字输出规范中，指定了HDCP版本，但客户端当前不支持HDCP版本控制。 有关详细信息，请参阅常见问题解答。

