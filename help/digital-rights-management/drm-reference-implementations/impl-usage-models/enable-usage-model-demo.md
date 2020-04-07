---
seo-title: 启用使用模型演示
title: 启用使用模型演示
uuid: 43930ebb-e936-4f48-990d-7ad19992e326
translation-type: tm+mt
source-git-commit: 6e949c2f88deef88f0d0ac95b18c006da1c89d2f

---


# 启用使用模型演示{#enable-the-usage-model-demo}

1. 在打包时指定 `RI_UsageModelDemo=true` 自定义属性。

   如果您使用Media Packager命令行工具打包内容，请输入：

   ```
   java -jar AdobeMediaPackager.jar [<i>source_file</i>] [<i>dest_file</i>] -k RI_UsageModelDemo=true
   ```

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>如果您在打包时未激活可选的演示模式，则许可证服务器会根据其处理的第一个有效DRM策略发布许可证。

