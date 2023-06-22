---
description: 您可以自定义或覆盖广告行为。
title: 设置自定义播放
exl-id: 28c28589-9e94-40de-b921-1bffc0392c29
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# 设置自定义播放{#set-up-customized-playback}

您可以自定义或覆盖广告行为。

在自定义或覆盖广告行为之前，请先使用注册广告策略实例。
要自定义广告行为，请执行以下操作之一：

* 实施 `AdPolicySelector` 接口及其所有方法。

   如果需要覆盖，建议使用此选项 **所有** 默认广告行为。

* 扩展 `DefaultAdPolicySelector` 类，并仅为那些需要自定义的行为提供实现。

   如果您只需要覆盖，则建议使用此选项 **部分** 缺省行为的URL值。

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

1. 在广告工作流中注册TVSDK使用的新内容工厂。

   ```
   PSDKConfig.advertisingFactory = new CustomContentFactory();
   ```

   >[!TIP]
   >
   >如果自定义内容工厂注册了特定流，则通过 `MediaPlayerItemConfig` 类时，它将在 `MediaPlayer` 实例已取消分配。 您的应用程序必须在每次创建新播放会话时注册它。
