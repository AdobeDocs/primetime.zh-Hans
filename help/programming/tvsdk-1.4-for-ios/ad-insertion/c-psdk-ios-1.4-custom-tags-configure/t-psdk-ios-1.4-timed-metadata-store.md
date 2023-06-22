---
description: 您的应用程序必须在适当的时间使用适当的PTTimedMetadata对象。
title: 在调度定时元数据对象时存储这些对象
exl-id: 43bc2b47-b947-4af1-bba8-6f2063c7b60c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 0%

---

# 在调度定时元数据对象时存储这些对象 {#store-timed-metadata-objects-as-they-are-dispatched}

您的应用程序必须在适当的时间使用适当的PTTimedMetadata对象。

在播放之前进行的内容解析期间，TVSDK会识别订阅的标记并通知您的应用程序这些标记。 与每个报表包关联的 `PTTimedMetadata` 是播放时间轴上的绝对时间。

您的应用程序必须完成以下任务：

1. 跟踪当前播放时间。
1. 将当前播放时间与调度的播放时间相匹配 `PTTimedMetadata` 对象。

1. 使用 `PTTimedMetadata` 其中，开始时间等于当前播放时间。

   >[!NOTE]
   >
   >以下代码假定只有一个 `PTTimedMetadata` 每次实例。 如果有多个实例，应用程序必须将其适当保存到词典中。 一种方法是在给定的时间创建一个数组，然后存储该数组中的所有实例。

   以下示例说明如何保存 `PTTimedMetadata` 中的对象 `NSMutableDictionary (timedMetadataCollection)` 按每个的开始时间键值 `timedMetadata`.

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

## 解析Nielsen ID3标记 {#example_3B51E9D4AF2449FAA8E804206F873ECF}

要提取ID3标记以进行解析，请在 `onMediaPlayerSubscribedTagIdentified` 方法：

```
(void)onMediaPlayerSubscribedTagIdentified:(NSNotification *)notification 
{ 
NSDictionary *userInfo = [notification userInfo]; 
PTTimedMetadata *timedMetadata = (PTTimedMetadata *)[userInfo objectForKey:PTTimedMetadataKey]; 
if (timedMetadata.type == PTTimedMetadataTypeID3) 
Unknown macro: { PTMetadata *metadata = (PTMetadata *)timedMetadata; NSString * nstr = [[NSString alloc] initWithFormat} 
 
}
```

解析ID3标记后，使用以下内容提取特定于Nielsen的元数据：

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
