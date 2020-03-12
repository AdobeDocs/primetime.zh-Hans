---
description: PTMediaPlayer接口封装媒体播放器对象的功能和行为。
seo-description: PTMediaPlayer接口封装媒体播放器对象的功能和行为。
seo-title: 设置PTMediaPlayer
title: 设置PTMediaPlayer
uuid: 78549406-7e33-4bca-a25e-1e433f6a75d7
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 设置PTMediaPlayer {#set-up-the-ptmediaplayer}

TVSDK提供用于创建高级视频播放器应用程序（您的Primetime播放器）的工具，您可以将其与其他Primetime组件集成。

使用平台的工具创建播放器并将其连接到TVSDK中的媒体播放器视图，该视图具有播放和管理视频的方法。 例如，TVSDK提供播放和暂停方法。 您可以在平台上创建用户界面按钮并设置按钮以调用这些TVSDK方法。

PTMediaPlayer接口封装媒体播放器对象的功能和行为。

要设置，请执行以下操 `PTMediaPlayer`作：

1. 从用户界面中获取媒体的URL，例如，在文本字段中。

   ```
   NSURL *url = [NSURL URLWithString:textFieldURL.text];
   ```

1. 创建 `PTMetadata`。

   假设您的方法 `createMetada` 准备元数据(请参 [阅广告](../ad-insertion/r-psdk-ios-1.4-advertising-requirements.md))。

   ```
   PTMetadata *metadata = [self createMetadata]
   ```

1. 使用 `PTMediaPlayerItem` 实例进行创 `PTMetadata` 建。

   ```
   PTMediaPlayerItem *item = [[[PTMediaPlayerItem alloc] 
          initWithUrl:url mediaId:yourMediaID metadata:metadata] autorelease];
   ```

1. 向TVSDK发送的通知添加观察者。

   ```
   [self addObservers]
   ```

1. 使用 `PTMediaPlayer` 您的新内容进行创 `PTMediaPlayerItem`建。

   ```
   PTMediaPlayer *player = [PTMediaPlayer playerWithMediaPlayerItem:item];
   ```

1. 设置播放器的属性。

   以下是一些可用属 `PTMediaPlayer` 性：

   ```
   player.autoPlay                    = YES;  
   player.closedCaptionDisplayEnabled = YES; 
   player.videoGravity                = PTMediaPlayerVideoGravityResizeAspect;  
   player.allowsAirPlayVideo          = YES;
   ```

1. 设置播放器的view属性。

   ```
   CGRect playerRect = self.adPlayerView.frame;  
   playerRect.origin = CGPointMake(0, 0); 
   playerRect.size = CGSizeMake(self.adPlayerView.frame.size.width,  
                                self.adPlayerView.frame.size.height); 
   
   [player.view setFrame:playerRect]; 
   [player.view setAutoresizingMask:  
         ( UIViewAutoresizingFlexibleWidth | UIViewAutoresizingFlexibleHeight )];
   ```

1. 在当前视图的子视图中添加播放器的视图。

   ```
   [self.adPlayerView  setAutoresizesSubviews:YES];  
   [self.adPlayerView addSubview:(UIView *)player.view];
   ```

1. 呼叫 `play` 以开始媒体播放。

   ```
   [player play];
   ```

