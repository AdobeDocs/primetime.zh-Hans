---
description: PTMediaPlayer界面封装媒体播放器对象的功能和行为。
title: 设置PTMediaPlayer
exl-id: 6d16bfd2-8d1d-4261-b343-c2e999c4d28b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---

# 设置PTMediaPlayer {#set-up-the-ptmediaplayer}

TVSDK提供了用于创建高级视频播放器应用程序（您的Primetime播放器）的工具，您可以将其与其他Primetime组件集成。

使用您平台的工具来创建播放器，并将其连接到TVSDK中的媒体播放器视图，该视图提供了播放和管理视频的方法。 例如，TVSDK提供播放和暂停方法。 您可以在平台上创建用户界面按钮，并设置这些按钮以调用这些TVSDK方法。

PTMediaPlayer界面封装媒体播放器对象的功能和行为。

要设置您的 `PTMediaPlayer`：

1. 从用户界面获取媒体的URL，例如，在文本字段中。

   ```
   NSURL *url = [NSURL URLWithString:textFieldURL.text];
   ```

1. 创建 `PTMetadata`.

   假定您的方法 `createMetada` 准备元数据(请参阅 [广告](../../ios-3x-advertising/ios-3x-advertising-requirements.md))。

   ```
   PTMetadata *metadata = [self createMetadata]
   ```

1. 创建 `PTMediaPlayerItem` 通过使用 `PTMetadata` 实例。

   ```
   PTMediaPlayerItem *item = [[[PTMediaPlayerItem alloc] 
          initWithUrl:url mediaId:yourMediaID metadata:metadata] autorelease];
   ```

1. 将观察者添加到TVSDK调度的通知。

   ```
   [self addObservers]
   ```

1. 创建 `PTMediaPlayer` 使用新的 `PTMediaPlayerItem`.

   ```
   PTMediaPlayer *player = [PTMediaPlayer playerWithMediaPlayerItem:item];
   ```

1. 在播放器上设置属性。

   以下是一些可用的 `PTMediaPlayer` 属性：

   ```
   player.autoPlay                    = YES;  
   player.closedCaptionDisplayEnabled = YES; 
   player.videoGravity                = PTMediaPlayerVideoGravityResizeAspect;  
   player.allowsAirPlayVideo          = YES;
   ```

1. 设置播放器的视图属性。

   ```
   CGRect playerRect = self.adPlayerView.frame;  
   playerRect.origin = CGPointMake(0, 0); 
   playerRect.size = CGSizeMake(self.adPlayerView.frame.size.width,  
                                self.adPlayerView.frame.size.height); 
   
   [player.view setFrame:playerRect]; 
   [player.view setAutoresizingMask:  
         ( UIViewAutoresizingFlexibleWidth | UIViewAutoresizingFlexibleHeight )];
   ```

1. 在当前视图的子视图中添加播放器视图。

   ```
   [self.adPlayerView  setAutoresizesSubviews:YES];  
   [self.adPlayerView addSubview:(UIView *)player.view];
   ```

1. 调用 `play` 以开始媒体播放。

   ```
   [player play];
   ```
