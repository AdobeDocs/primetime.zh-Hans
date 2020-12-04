---
description: 本节概述与输出保护相关的配置、选项和含义。
seo-description: 本节概述与输出保护相关的配置、选项和含义。
seo-title: RBOP概念
title: RBOP概念
uuid: fc19c3c9-39a1-4b62-b763-101e5454a01f
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---


# RBOP概念{#rbop-concepts}

本节概述与输出保护相关的配置、选项和含义。

在分层JSON结构中指定基于分辨率的输出保护要求。 *输出要求基于像素。*

在JSON规范的最高级别，您可以为指定分辨率定义最大像素分辨率和像素约束：

* `maxPixel` -最大像素分辨率定义解密所用的最大分辨率。
* `pixelConstraints` -像素约束定义必须针对指定分辨率强制执行的输出要求。

将输出要求与特定像素约束相关联。 可以与给定像素约束关联的要求类型包括数字、模拟和无线(OTA)连接限制。

**数字输出**

数字输出要求可以指定限制选项，如“需要数字输出保护”或“不允许播放”。 输出要求还可以指定限制较少的选项，如“不应应用保护”或“如果可用，应使用数字保护”。

**模拟输出**

模拟输出连接比数字输出更简单；它们由单一输出要求组成。
