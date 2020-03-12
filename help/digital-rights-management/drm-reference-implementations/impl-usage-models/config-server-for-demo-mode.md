---
description: 'null'
seo-description: 'null'
seo-title: 配置使用模型演示模式
title: 配置使用模型演示模式
uuid: f818c7fc-e88f-4fa4-926e-08a1337b28d3
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 配置使用模型演示模式{#configure-usage-model-demo-mode}

在参考实施服务器为使用模型演示发放许可证之前，您必须配置服务器以指定为四个使用模型中的每一个模型生成许可证的方式。 这意味着您需要为每个使用模型指定DRM策略。 参考实施在目录中包含以下DRM策 [!DNL Reference Implementation/Server/Reference Implementation Server/resources/] 略示例：

* `dto-policy.pol` -（下载到自有）
* `vod-policy.pol` -（租赁／视频点播）
* `sub-policy.pol` -（订阅）
* `ad-policy.pol` -（广告资助）

>[!NOTE]
>
>您可以将这些示例策略替换为您自己的DRM策略。

1. 在中设置这 [!DNL flashaccess-refimpl.properties] 些属性，以指定您计划应用到每个使用模型的DRM策略：

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

1. 将示例策略文件复制到您在中的属性中指定的 `config.resourcesDirectory` 目录中 [!DNL flashaccess-refimpl.properties]。
