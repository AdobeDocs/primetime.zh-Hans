---
description: 您的应用程序必须在适当的时间使用适当的PTTimedMetadata对象。
title: 在调度时存储定时元数据对象
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 0%

---


# 在调度定时元数据对象时存储这些对象{#store-timed-metadata-objects-as-they-are-dispatched}

您的应用程序必须在适当的时间使用适当的PTTimedMetadata对象。

在内容分析（在播放前发生）期间，TVSDK识别订阅的标记并通知您的应用程序这些标记。 与每个`PTTimedMetadata`关联的时间是播放时间线上的绝对时间。

您的应用程序必须完成以下任务:

1. 跟踪当前播放时间。
1. 将当前播放时间与调度的`PTTimedMetadata`对象匹配。

1. 使用`PTTimedMetadata`，其中开始时间等于当前播放时间。

   >[!NOTE]
   >
   >下面的代码假设一次只有一个`PTTimedMetadata`实例。 如果有多个实例，应用程序必须将它们正确保存在词典中。 一种方法是在给定时间创建一个数组，并将所有实例存储在该数组中。

   下面的示例说明如何将`PTTimedMetadata`对象保存在按每个`timedMetadata`的开始时间键入的`NSMutableDictionary (timedMetadataCollection)`中。

   ```
   NSMutableDictionary *timedMetadataCollection; 
   
   - (void)onMediaPlayerSubscribedTagIdentified:(NSNotification *)notification 
   { 
       if (!timedMetadataCollection) 
       { 
           timedMetadataCollection = [[NSMutableDictionary alloc] init]; 
       } 
       NSDictionary *userInfo = [notification userInfo]; 
       PTTimedMetadata *timedMetadata = [(PTTimedMetadata *)[userInfo objectForKey:PTTimedMetadataKey] retain]; 
       if ([timedMetadata.name  isEqualToString: @"#EXT-OATCLS-SCTE35"]) 
       { 
            NSLog(@"Adding timedMetadata %@ to timedMetadataCollection with time                      
                    %f",timedMetadata.name,CMTimeGetSeconds(timedMetadata.time)); 
   
           NSNumber *timedMetadataStartTime = [NSNumber numberWithInt:(int)CMTimeGetSeconds(timedMetadata.time)]; 
           [timedMetadataCollection setObject:timedMetadata forKey:timedMetadataStartTime]; 
       } 
       [timedMetadata release]; 
   }
   ```

## 解析Nielsen ID3标签{#example_3B51E9D4AF2449FAA8E804206F873ECF}

要提取ID3标记以进行分析，请在`onMediaPlayerSubscribedTagIdentified`方法上使用以下内容：

```
(void)onMediaPlayerSubscribedTagIdentified:(NSNotification *)notification 
{ 
NSDictionary *userInfo = [notification userInfo]; 
PTTimedMetadata *timedMetadata = (PTTimedMetadata *)[userInfo objectForKey:PTTimedMetadataKey]; 
if (timedMetadata.type == PTTimedMetadataTypeID3) 
Unknown macro: { PTMetadata *metadata = (PTMetadata *)timedMetadata; NSString * nstr = [[NSString alloc] initWithFormat} 
 
}
```

解析ID3标记后，使用以下方法提取特定于Nielsen的元数据：

```
    (NSString *)parseNielsenUrlFromID3Tag:(NSString *)str 
    { 
    /* ID3 tag <AVMetadataItem: 0x15e58e60, identifier=id3/PRIV, keySpace=org.id3, key class = __NSCFString, key=PRIV, commonKey=(null), extendedLanguageTag=(null), dataType=(null), time= {110265598/4410000 = 25.004} 
 
    , duration= 
    {INVALID} 
 
    , startDate=(null), extras= 
    { info = "www.nielsen.com/X100zdCIGeIlgZnkYj6UvQ==/pI-X5FFk07770SXf2ZbI6g==/CE0C6​1TsDo0jIrNn9N2yTPe6nVG3dHZHfgS52fJeQjf9fJCga9tj4OW4NXPZ9fI1mx0gfYUPBXnjqolHemZPtn_FCoNg​8Dqw8-Auruf15fU04pJfXTTN0IgZ4iWBmeRiPpS9X100zdCIGeIlgZnkYj6UvVjmPIdY5jyRQTA=/00000/21778/00"; } 
 
    , value length=1> 
    */ 
 
NSString *nielsenStr = nil; 
for (NSString *keyValuePairString in [str componentsSeparatedByString:@", "]) 
{ 
if([keyValuePairString rangeOfString:@"nielsen.com"].location != NSNotFound) 
{ // Nielsen NSRange start = [keyValuePairString rangeOfString:@"\""]; NSRange end = [keyValuePairString rangeOfString:@"\";"]; nielsenStr = [keyValuePairString substringWithRange:NSMakeRange(start.location + 1, end.location-start.location)]; } 
 
} 
return nielsenStr; 
}
```
