---
description: 您可以根据默认解析器实现您自己的内容解析器。
seo-description: 您可以根据默认解析器实现您自己的内容解析器。
seo-title: 实现自定义内容解析程序
title: 实现自定义内容解析程序
uuid: 88627fdc-3b68-4a9f-847e-a490ea8e3034
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 实现自定义内容解析程序 {#implement-a-custom-content-resolver}

您可以根据默认解析器实现您自己的内容解析器。

当TVSDK检测到新机会时，它会重新访问注册的内容解析器，寻找能够解决该机会的内容解析器。 选择返回true的第一个用于解决该机会。 如果没有内容解析程序功能，则跳过该机会。 由于内容解析过程通常是异步的，因此内容解析程序负责在进程完成时通知。

1. 创建自定义 `AdvertisingFactory` 实例并覆盖 `createContentResolver`。

   例如：

   ```java
   new AdvertisingFactory() { 
       ... 
       @Override 
       public ContentResolver createContentResolver(MediaPlayerItem item) { 
           Metadata metadata = _mediaPlayer.getCurrentItem().getResource().getMetadata(); 
           if (metadata != null) { 
               if (metadata.containsKey(DefaultMetadataKeys.AUDITUDE_METADATA_KEY.getValue())) { 
                   return new AuditudeResolver(getActivity().getApplicationContext()); 
               } else if (metadata.containsKey(DefaultMetadataKeys.JSON_METADATA_KEY.getValue())) { 
                   return new MetadataResolver(); 
               } else if (metadata.containsKey(DefaultMetadataKeys.TIME_RANGES_METADATA_KEY.getValue())) { 
                   return new CustomAdMarkersContentResolver(); 
               } else if (metadata.containsKey(CustomAdResolver.CUSTOM_METADATA_KEY)) { 
                   return new CustomAdResolver(); 
               } 
           } 
           return null; 
       } 
       ... 
   }
   ```

1. 将广告客户端工厂注册到 `MediaPlayer`。

   例如：

   ```java
   // register the custom advertising factory with media player 
   advertisingFactory = createCustomAdvertisingFactory(); 
   mediaPlayer.registerAdClientFactory(advertisingFactory);
   ```

1. 将对象 `AdvertisingMetadata` 传递给TVSDK，如下所示：
   1. 创建对 `AdvertisingMetadata` 象和对 `MetadataNode` 象。
   1. 将对象 `AdvertisingMetadata` 保存到 `MetadataNode`。

   ```java
   MetadataNode result = new MetadataNode(); 
   result.setNode(DefaultMetadataKeys.ADVERTISING_METADATA.getValue(),  
                  advertisingMetadata);
   ```

1. 创建扩展该类的自定义广告解析 `ContentResolver` 程序类。
   1. 在自定义广告解析程序中，覆盖此受保护的函数：

      ```java
      void doResolveAds(Metadata metadata,  
                        PlacementOpportunity placementOpportunity)
      ```

      元数据包含您的 `AdvertisingMetada`内容。 将其用于以下矢量 `TimelineOperation` 生成。

   1. 为每个职位安排机会创建一个 `Vector<TimelineOperation>`。

      矢量可为空，但不能为null。

      此示例提 `TimelineOperation` 供了以下结构 `AdBreakPlacement`:

      ```java
      AdBreakPlacement(AdBreak.createAdBreak( 
                                ads,       // Vector<Ad> 
                                time,      // Ad Break start time. Note: local time on the timeline 
                                duration,  // Ad Break duration 
                                tag()      // An arbitrary string value that can be attached to  
                                           // the AdBreak object. 
                               ), placementInformation  // Retrieved from PlacementOpportunity 
      )
      ```

   1. 解析广告后，调用以下函数之一：

      * 如果广告解析成功： `notifyResolveComplete(Vector<TimelineOperation> proposals)`
      * 如果广告解决失败： `notifyResolveError(Error error)`
      例如，如果失败：

      ```java
      Metadata metadata = new MetadataNode(); 
      metadata.setValue("NATIVE_ERROR_CODE", exception.getCause().toString()); 
      error.setMetadata(metadata);
      ```


<!--<a id="example_4F0D7692A92E480A835D6FDBEDBE75E7"></a>-->

此示例自定义广告解析程序向广告服务器发出HTTP请求并接收JSON响应。

```java
public class CustomAdResolver extends ContentResolver { 
    ... 
    @Override 
    protected void doResolveAds(Metadata metadata, PlacementOpportunity placementOpportunity) { 
        ... 
        if (resolveSuccess == true) { 
            notifyResolveComplete(Vector<TimelineOperation> proposals); 
        } 
        else { 
            notifyResolveError(Error error); 
        } 
    } 
    ... 
}
```

实时流的JSON和服务器响应示例：

```
{     
    "response": { 
        "breaks": [ { 
            "start": 0, 
            "ads": [ { 
                "id": 1001, 
                "primary_asset": { 
                    "url": "https://venkat-test.s3.amazonaws.com/ads/geico/playlist.m3u8", 
                    "duration": 30000, 
                    "id": "asset1", 
                    "resource_type": "" 
                }, 
                "companion_assets": { 
                } 
            } 
        ] }, 
        { 
            "start": -1, 
            "ads": [ { 
                "id": 1003, 
                "primary_asset": { 
                    "url": "https://venkat-test.s3.amazonaws.com/ads/priceline/playlist.m3u8", 
                    "duration": 30000, 
                    "id": "asset3", 
                    "resource_type": "" 
                }, 
                "companion_assets": { 
                } 
            } ] 
        } ] 
    } 
} 
```

VOD的JSON和服务器响应示例：

```
{     
    "response": { 
        "breaks": [ { 
            "start": 0, 
            "ads": [ { 
                "id": 1001, 
                "primary_asset": { 
                    "url": "https://venkat-test.s3.amazonaws.com/ads/geico/playlist.m3u8", 
                    "duration": 30000, 
                    "id": "asset1", 
                    "resource_type": "" 
                }, 
                "companion_assets": {  
                } 
            }, 
            { 
                "id": 1002, 
                "primary_asset": { 
                    "url": "https://venkat-test.s3.amazonaws.com/ads/crescent/playlist.m3u8", 
                    "duration": 15000, 
                    "id": "asset2", 
                    "resource_type": "" 
                }, 
                "companion_assets": { 
                } 
            } ] 
        }, 
        { 
            "start": 50000, 
            "ads": [ { 
                "id": 1003, 
                "primary_asset": { 
                    "url": "https://venkat-test.s3.amazonaws.com/ads/priceline/playlist.m3u8", 
                    "duration": 30000, 
                    "id": "asset3", 
                    "resource_type": "" 
                }, 
                "companion_assets": { 
                } 
            } ] 
        }, 
        { 
            "start": 100000000, 
            "ads": [ { 
                "id": 1004, 
                "primary_asset": { 
                    "url": "https://venkat-test.s3.amazonaws.com/ads/camry/playlist.m3u8", 
                    "duration": 15000, 
                    "id": "asset4", 
                    "resource_type": "" 
                }, 
                "companion_assets": { 
                } 
            } ] 
        } ] 
    } 
} 
```

