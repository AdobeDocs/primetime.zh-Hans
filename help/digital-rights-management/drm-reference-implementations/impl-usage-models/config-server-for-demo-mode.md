---
title: 配置使用模型演示模式
description: 配置使用模型演示模式
copied-description: true
exl-id: 593acfbd-fd37-4bab-ac8e-5cb62963fac4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# 配置使用模型演示模式{#configure-usage-model-demo-mode}

在参考实施服务器可以颁发使用模式演示的许可证之前，您必须配置服务器以指定如何为四种使用模式中的每种模式生成许可证。 这意味着您需要为每个使用模型指定DRM策略。 参考实施包括以下示例DRM策略 [!DNL Reference Implementation/Server/Reference Implementation Server/resources/] 目录：

* `dto-policy.pol`  — （下载到拥有）
* `vod-policy.pol` - （租赁/视频点播）
* `sub-policy.pol`  — （订阅）
* `ad-policy.pol` - （广告资助）

>[!NOTE]
>
>您可以使用自己的DRM策略来替换这些示例策略。

1. 在中设置这些属性 [!DNL flashaccess-refimpl.properties] 要指定计划应用于每个使用模型的DRM策略，请执行以下操作：

   ```
   # DRM Policy file name for Download To Own usage 
   RefImpl.UsageModelDemo.Policy.DTO=dto-policy.pol 
   # DRM Policy file name for Rental usage 
   RefImpl.UsageModelDemo.Policy.VOD=vod-policy.pol 
   # DRM Policy file name for Subscription usage 
   RefImpl.UsageModelDemo.Policy.Subscribe=sub-policy.pol 
   # DRM Policy file name for Ad Supported (free) usage 
   RefImpl.UsageModelDemo.Policy.Free=ad-policy.pol
   ```

1. 将示例策略文件复制到您在 `config.resourcesDirectory` 中的属性 [!DNL flashaccess-refimpl.properties].
