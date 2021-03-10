---
title: 启用使用模型演示
description: 启用使用模型演示
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '62'
ht-degree: 0%

---


# 启用使用模型demo{#enable-the-usage-model-demo}

1. 在打包时指定自定义属性`RI_UsageModelDemo=true`。

   如果要使用Media Packager命令行工具打包内容，请输入：

   ```
   java -jar AdobeMediaPackager.jar [<i>source_file</i>] [<i>dest_file</i>] -k RI_UsageModelDemo=true
   ```

>[!NOTE]
>
>如果您在打包时未激活可选演示模式，则许可证服务器会根据其处理的第一个有效DRM策略发布许可证。

