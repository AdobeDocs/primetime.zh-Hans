---
description: 本节介绍一个示例配置，该配置说明了配置的概念和形式。
title: 示例RBOP配置
exl-id: 0f40be83-9c7f-482b-ac42-9aa4e3f46f58
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 0%

---

# 示例RBOP配置 {#sample-rbop-configuration}

本节介绍一个示例配置，该配置说明了配置的概念和形式。

以下示例JSON配置定义了一个指定以下内容的像素输出策略：

* 将视频解密限制为1080或以下分辨率
* 对720和480号决议施加具体限制：

   * 对于720分辨率：需要HDCP进行数字输出；需要 *拷贝生成管理系统 — 模拟* (CGMS-A)对模拟输出的保护。
   * 对于480分辨率：数字输出需要HDCP；模拟不需要保护

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

请注意以下关于上述示例配置的说明：

* 此 `pixelCount` 规范在JSON结构中的下一级，位于 `pixelConstraints` 部分。

* 在每个像素计数规范内，为数字和模拟输出指定输出保护。
* 在数字输出规范中，指定了HDCP版本，尽管客户端当前不支持HDCP版本控制。 有关更多信息，请参阅常见问题解答。
