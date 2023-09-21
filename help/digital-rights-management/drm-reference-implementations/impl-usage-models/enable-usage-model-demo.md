---
title: 启用使用模型演示
description: 启用使用模型演示
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '62'
ht-degree: 0%

---

# 启用使用模型演示{#enable-the-usage-model-demo}

1. 指定自定义属性 `RI_UsageModelDemo=true` 在打包时。

   如果使用Media Packager命令行工具打包内容，请输入：

   ```
   java -jar AdobeMediaPackager.jar [<i>source_file</i>] [<i>dest_file</i>] -k RI_UsageModelDemo=true
   ```

>[!NOTE]
>
>如果您在打包时未激活可选演示模式，则许可证服务器会根据它处理的第一个有效DRM策略颁发许可证。
