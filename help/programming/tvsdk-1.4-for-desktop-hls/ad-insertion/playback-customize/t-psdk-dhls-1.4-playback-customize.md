---
description: 您可以自定义或覆盖广告行为。
seo-description: 您可以自定义或覆盖广告行为。
seo-title: 设置自定义播放
title: 设置自定义播放
uuid: 479ca1b0-6b3f-42fa-85e1-31d707da8730
translation-type: tm+mt
source-git-commit: a21a5fcc819a7bec58ad36e118d04f462ec3fd92

---


# 设置自定义播放{#set-up-customized-playback}

您可以自定义或覆盖广告行为。

在自定义或覆盖广告行为之前，请先注册广告策略实例。
要自定义广告行为，请执行以下操作之一：

* 实现接 `AdPolicySelector` 口及其所有方法。

   如果您需要覆盖所有默认广告 **行为** ，则建议使用此选项。

* 扩展类 `DefaultAdPolicySelector` 并仅为那些需要自定义的行为提供实现。

   如果只需覆盖部分默认行 **为** ，建议使用此选项。

对于这两个选项，请完成以下任务：

1. 实施您自己的自定义广告策略选择器。

   ```
   public class CustomAdPolicySelector implements AdPolicySelector { 
       // your own customization here 
   }
   ```

1. 扩展内容工厂以使用自定义广告策略选择器。

   ```
   public class CustomContentFactory extends DefaultContentFactory { 
       /** 
        * @inheritDoc 
        */ 
       override protected function doRetrieveAdPolicySelector(item:MediaPlayerItem):AdPolicySelector { 
           return new CustomAdPolicySelector(item); 
       } 
   }
   ```

   ```
   psdkutils::PSDKSharedPointer<psdk::ContentFactory> factory; 
   psdkFactory->createDefaultContentFactory(&factory); 
   psdkutils::PSDKSharedPointer<psdk::AdPolicySelector> defaultAdPolicySelector; 
   factory->retrieveAdPolicySelector(item, &defaultAdPolicySelector);
   ```

1. 注册TVSDK在广告工作流程中使用的新内容工厂。

   ```
   PSDKConfig.advertisingFactory = new CustomContentFactory();
   ```

   >[!TIP]
   >
   >如果自定义内容工厂已通过类为特定流注册， `MediaPlayerItemConfig` 则在取消分配实例时将清 `MediaPlayer` 除它。 每次创建新的播放会话时，您的应用程序都必须注册它。