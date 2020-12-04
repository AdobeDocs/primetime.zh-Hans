---
seo-title: 启用使用模型演示
title: 启用使用模型演示
uuid: 43930ebb-e936-4f48-990d-7ad19992e326
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '62'
ht-degree: 0%

---


# 启用使用模型demo{#enable-the-usage-model-demo}

1. 在打包时指定自定义属性`RI_UsageModelDemo=true`。

   如果您使用Media Packager命令行工具打包内容，请输入：

   ```
   java -jar AdobeMediaPackager.jar [<i>source_file</i>] [<i>dest_file</i>] -k RI_UsageModelDemo=true
   ```

>[!NOTE]
>
>如果打包时不激活可选演示模式，则许可证服务器将根据其处理的第一个有效DRM策略发布许可证。

