---
description: 您可以自定义或覆盖广告行为。
seo-description: 您可以自定义或覆盖广告行为。
seo-title: 设置自定义播放
title: 设置自定义播放
uuid: 479ca1b0-6b3f-42fa-85e1-31d707da8730
translation-type: tm+mt
source-git-commit: a21a5fcc819a7bec58ad36e118d04f462ec3fd92
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---


# 设置自定义播放{#set-up-customized-playback}

您可以自定义或覆盖广告行为。

在自定义或覆盖广告行为之前，请先注册广告策略实例。
要自定义广告行为，请执行下列操作之一：

* 实现`AdPolicySelector`接口及其所有方法。

   如果需要覆盖&#x200B;**all**&#x200B;默认广告行为，则建议使用此选项。

* 扩展`DefaultAdPolicySelector`类并仅为那些需要自定义的行为提供实现。

   如果只需要覆盖默认行为的&#x200B;**某些**，则建议使用此选项。

对于这两个选项，请完成以下任务:

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
   >如果通过`MediaPlayerItemConfig`类为特定流注册了自定义内容工厂，则在取消分配`MediaPlayer`实例时将清除该工厂。 每次创建新的播放会话时，您的应用程序都必须注册它。