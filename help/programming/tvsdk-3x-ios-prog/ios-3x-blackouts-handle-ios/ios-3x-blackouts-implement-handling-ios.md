---
description: TVSDK提供了用于处理封锁期的API和示例代码。
title: 实施封锁处理
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---

# 实施封锁处理 {#implement-blackout-handling}

TVSDK提供了用于处理封锁期的API和示例代码。

要实施封锁处理并在封锁期间提供替代内容，请执行以下操作：

1. 设置应用程序以订阅实时流清单中的封锁标记。

   ```
   - (void) createMediaPlayer:(PTMediaPlayerItem *)item 
   { 
       [PTSDKConfig setSubscribedTags:[NSArray arrayWithObject:<INSERT-BLACKOUT-TAG>]]; 
       // For example:  
       // [PTSDKConfig setSubscribedTags:[NSArray arrayWithObject:@"#EXT-OATCLS-SCTE35"]]; 
   }
   ```

1. 添加通知侦听器 `PTTimedMetadataChangedNotification`.

   ```
   - (void)addobservers 
   { 
       [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerSubscribedTagIdentified:)  
         name:PTTimedMetadataChangedNotification object:self.player.currentItem]; 
   }
   ```

1. 实施侦听程序方法 `PTTimedMetadata` 前景中的对象。

   例如：

   ```
   - (void)onMediaPlayerSubscribedTagIdentified:(NSNotification *)notification 
   { 
       NSDictionary *userInfo = [notification userInfo]; 
       PTTimedMetadata *timedMetadata = [(PTTimedMetadata *)[userInfo objectForKey:PTTimedMetadataKey]  
         retain]; 
   
    if ([timedMetadata.name isEqualToString:<INSERT-BLACKOUT-TAG>]) 
       { 
        // handle tag. For example: store it in a dictionary keyed by time to be handled when  
        //   playback time = timedMetadata time. 
           NSNumber *timedMetadataStartTime =  
             [NSNumber numberWithInt:(int)CMTimeGetSeconds(timedMetadata.time)]; 
           [timedMetadataCollection setObject:timedMetadata forKey:timedMetadataStartTime]; 
       } 
   
       [timedMetadata release]; 
   }
   ```

1. 句柄 `TimedMetadata` 播放期间不断更新的对象。

   ```
   - (void)onMediaPlayerTimeChange:(NSNotification *)notification 
   { 
       @synchronized(self) 
       { 
           CMTimeRange seekableRange = self.player.seekableRange; 
           if (CMTIMERANGE_IS_VALID(seekableRange)) 
           { 
               _currentTime = (int) CMTimeGetSeconds(self.player.currentTime); 
               if (isnan(_currentTime)) 
               { 
                   _currentTime = 0; 
               } 
               [self handleCollectionAtTime:_currentTime]; 
           } 
       } 
   }
   ```

1. 添加 `PTTimedMetadata` 处理程序切换到替代内容并返回主内容，如 `PTTimedMetadata` 对象及其播放时间。

   ```
   - (void)handleCollectionAtTime:(int)currentTime 
   { 
       NSArray *allKeys = nil; 
       NSMutableArray * timedMetadatasToDelete = [[[NSMutableArray alloc]init]autorelease]; 
   
       if (!_inBlackout && timedMetadataCollection) 
       { 
           allKeys = [timedMetadataCollection allKeys]; 
           int count = [allKeys count]; 
           for (int i=count-1; i>-1; i--) 
           { 
               NSNumber *currTimedMetadataTime = allKeys[i]; 
               PTTimedMetadata *currTimedMetadata =  
                 [timedMetadataCollection objectForKey:currTimedMetadataTime]; 
   
               if (currentTime == [currTimedMetadataTime integerValue] &&  
                                  currTimedMetadata.name == <INSERT-BLACKOUT-TAG> &&  
                                  [self isBlackoutStart: currTimedMetadata]) 
               { 
                                   PTAdMetadata *newItemAdMetadata =  
                                     [self createAlternateMediaMetadata];            
   
               // 1. Turn off preroll on the alternate media item. 
                   newItemAdMetadata.enableLivePreroll = NO; 
   
                               PTMediaPlayerItem *newItem =  
                                 [[PTMediaPlayerItem alloc]initWithUrl: 
                                   <INSERT-ALTERNATE-STREAM-URL mediaId:<INSERT-ALTERNATE-STREAM- 
                                    MEDIA-ID> metadata:newItemAdMetadata];
   
              // 2. Register the current (original playback item) in background. 
                   [self.player registerCurrentItemAsBackgroundItem]; 
   
              // 3. Replace the current playback item with the alternate stream. 
                    [self.player replaceCurrentItemWithPlayerItem:newItem]; 
   
              // 4. Reset observers. 
                   [self removeObservers]; 
                   [self addobservers]; 
   
              // 5. Register listener on the subscribed tags in background item. 
                   [[NSNotificationCenter defaultCenter] addObserver:self  
                      selector:@selector(onSubscribedTagInBackground:)  
                       name:PTTimedMetadataChangedInBackgroundNotification  
                         object:self.player.currentItem]; 
   
              // 6. Register listener on the error in background item. 
                            [[NSNotificationCenter defaultCenter]  
                               addObserver:self selector:@selector(onBackgroundManifestError:)  
                               name:PTBackgroundManifestErrorNotification   
                                 object:self.player.currentItem]; 
   
              // 7. Resume playback 
                        [self.player play]; 
   
                       // 8. Set boolean to true to handle blackout end. 
                     _inBlackout = YES; 
                     break; 
               } 
           } 
       } 
       else if (_inBlackout && backgroundTimedMetadataCollection) 
       { 
           allKeys = [backgroundTimedMetadataCollection allKeys]; 
           int count = [allKeys count]; 
           for (int i=count-1; i>-1; i--) 
           { 
               NSNumber *currTimedMetadataTime = allKeys[i]; 
               PTTimedMetadata *currTimedMetadata =  
                 [backgroundTimedMetadataCollection objectForKey:allKeys[i]]; 
   
               if (currentTime == ([currTimedMetadataTime integerValue] &&  
                 currTimedMetadata.name == <INSERT-BLACKOUT-TAG>  &&  
                 [self isBlackoutEnd:currTimedMetadata] ) 
               {      
                                  // 1. Come out of blackout. Unregister background item. 
                              [self.player unregisterCurrenBackgroundItem]; 
   
                       PTMetadata *metadata = [self createMetadata]; 
                       PTAdMetadata *adMetadata =  
                         (PTAdMetadata *)[currMetadata metadataForKey:PTAdResolvingMetadataKey]; 
                             adMetadata.enableLivePreroll = NO; 
   
                               PTMediaPlayerItem *item =  
                                 [[[PTMediaPlayerItem alloc] initWithUrl:<INSERT-ORIGINAL-URL>  
                                   mediaId:<INSERT-ORIGINAL-MEDIAID> metadata:metadata autorelease]; 
   
                                   // 2. Switch back to original item. 
                       [self.player replaceCurrentItemWithPlayerItem:item]; 
                       self.player.autoPlay = YES; 
                       [self removeObservers]; 
   
                       // 3. Remove background item listener. 
                       [[NSNotificationCenter defaultCenter] removeObserver:self  
                          name:PTTimedMetadataChangedInBackgroundNotification  
                       object:self.player.currentItem]; 
   
                                  [[NSNotificationCenter defaultCenter] removeObserver:self  
                                     name:PTBackgroundManifestErrorNotification 
                       object:self.player.currentItem]; 
                       [self addobservers]; 
                       [self.player play]; 
   
                               // 4. Update boolean to correctly maintain the current state. 
                       _inBlackout = NO; 
                       break; 
               } 
           } 
       } 
   }
   ```

1. 实施侦听程序方法 `PTTimedMetadata` 背景中的对象。

   ```
   - (void)onSubscribedTagInBackground:(NSNotification *)notification 
   { 
       NSDictionary *userInfo = [notification userInfo]; 
       PTTimedMetadata *timedMetadata = [(PTTimedMetadata *) 
         [userInfo objectForKey:PTTimedMetadataKey] retain]; 
   
       if ([timedMetadata.name isEqualToString:<INSERT-BLACKOUT-TAG>]) 
       { 
           NSNumber *timedMetadataStartTime =  
             [NSNumber numberWithInt:(int)CMTimeGetSeconds(timedMetadata.time)]; 
           [backgroundTimedMetadataCollection  
              setObject:timedMetadata forKey:timedMetadataStartTime]; 
       } 
   
       [timedMetadata release]; 
   }
   ```

1. 为后台错误实施侦听程序方法。

   ```
   - (void) onBackgroundManifestError:(NSNotification *)notification 
   { 
       NSLog (@"onBackgroundManifestError"); 
   }
   ```

1. 如果封锁范围位于播放流的DVR上，请更新不可搜索的范围。

   ```
   // This sample assumes that blackoutStartTimedMetadata is the PTTimedMetadata  
   // object that indicated "blackout start", and assuming blackoutEndTimedMetadata is the  
   // PTTimedMetadataObject that indicated "blackout end". Since in this case they are both  
   // in DVR, both are notified to the application before playback starts. This is the right  
   // time for the application to set this range in DVR as non-seekable range. 
   
   CMTime ignoreRangeStart = blackoutStartTimedMetadata.time; 
   CMTime ignoreRangeDuration = CMTimeMakeWithSeconds(CMTimeMakeWithSeconds  
     (CMTimeGetSeconds(blackoutEndTimedMetadata.time) -   
        CMTimeGetSeconds(blackoutStartTimedMetadata.time)),  
          blackoutEndTimedMetadata.time.timescale); 
   
   CMTimeRange ignoreRange = CMTimeRangeMake(ignoreRangeStart, ignoreRangeDuration); 
   NSArray *ignoreRangeArray = [NSArray arrayWithObject:[NSValue valueWithCMTimeRange:ignoreRange]]; 
   PTBlackoutMetadata *blackoutMetadata =  
     [[PTBlackoutMetadata alloc]initWithNonSeekableRanges:ignoreRangeArray]; 
   PTMetadata *currMetadata = self.item.metadata; 
   
   if (currMetadata) 
   { 
       [currMetadata setMetadata:blackoutMetadata forKey:PTBlackoutMetadataKey] 
   }
   ```
