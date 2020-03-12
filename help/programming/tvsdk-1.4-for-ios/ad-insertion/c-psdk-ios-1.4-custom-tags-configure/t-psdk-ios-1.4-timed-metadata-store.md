---
description: 您的应用程序必须在适当的时间使用相应的PTTimedMetadata对象。
seo-description: 您的应用程序必须在适当的时间使用相应的PTTimedMetadata对象。
seo-title: 在调度定时元数据对象时存储这些对象
title: 在调度定时元数据对象时存储这些对象
uuid: d26ed49e-fb29-4765-86e9-9ebbe5fa0a2b
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 在调度定时元数据对象时存储这些对象 {#store-timed-metadata-objects-as-they-are-dispatched}

您的应用程序必须在适当的时间使用相应的PTTimedMetadata对象。

在内容分析（在播放前发生）期间，TVSDK会识别订阅的标记并通知您的应用程序这些标记。 与每个时间关联的时间 `PTTimedMetadata` 是播放时间线上的绝对时间。

应用程序必须完成以下任务：

1. 跟踪当前播放时间。
1. 将当前播放时间与调度的对象匹 `PTTimedMetadata` 配。

1. 使用 `PTTimedMetadata` 开始时间等于当前播放时间的位置。

   >[!NOTE]
   >
   >以下代码假定一次只 `PTTimedMetadata` 有一个实例。 如果有多个实例，则应用程序必须将它们正确保存在词典中。 一种方法是在给定时间创建一个数组，并将所有实例存储在该数组中。

   以下示例显示如何按每 `PTTimedMetadata` 个对象的开 `NSMutableDictionary (timedMetadataCollection)` 始时间将对象保存在键中 `timedMetadata`。

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

要提取ID3标记以进行分析，请在方法上使用以 `onMediaPlayerSubscribedTagIdentified` 下内容：

```
(void)onMediaPlayerSubscribedTagIdentified:(NSNotification *)notification 
{ 
NSDictionary *userInfo = [notification userInfo]; 
PTTimedMetadata *timedMetadata = (PTTimedMetadata *)[userInfo objectForKey:PTTimedMetadataKey]; 
if (timedMetadata.type == PTTimedMetadataTypeID3) 
Unknown macro: { PTMetadata *metadata = (PTMetadata *)timedMetadata; NSString * nstr = [[NSString alloc] initWithFormat} 
 
}
```

在解析ID3标记后，使用以下代码提取特定于Nielsen的元数据：

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

