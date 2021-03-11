---
description: PTMediaPlayer接口封装媒体播放器对象的功能和行为。
title: 设置PTMediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---


# 设置PTMediaPlayer {#set-up-the-ptmediaplayer}

TVSDK提供用于创建高级视频播放器应用程序（您的Primetime播放器）的工具，您可以将该应用程序与其他Primetime组件集成。

使用您平台的工具创建播放器并将其连接到TVSDK中的媒体播放器视图,TVSDK中有播放和管理视频的方法。 例如，TVSDK提供播放和暂停方法。 您可以在平台上创建用户界面按钮并设置按钮以调用这些TVSDK方法。

PTMediaPlayer接口封装媒体播放器对象的功能和行为。

设置`PTMediaPlayer`:

1. 从用户界面（例如，在文本字段中）获取媒体的URL。

   ```
   NSURL *url = [NSURL URLWithString:textFieldURL.text];
   ```

1. 创建`PTMetadata`。

   假设您的方法`createMetada`准备元数据（请参阅[Advertising](../ad-insertion/r-psdk-ios-1.4-advertising-requirements.md)）。

   ```
   PTMetadata *metadata = [self createMetadata]
   ```

1. 使用`PTMetadata`实例创建`PTMediaPlayerItem`。

   ```
   PTMediaPlayerItem *item = [[[PTMediaPlayerItem alloc] 
          initWithUrl:url mediaId:yourMediaID metadata:metadata] autorelease];
   ```

1. 向TVSDK发送的通知添加观察器。

   ```
   [self addObservers]
   ```

1. 使用新`PTMediaPlayerItem`创建`PTMediaPlayer`。

   ```
   PTMediaPlayer *player = [PTMediaPlayer playerWithMediaPlayerItem:item];
   ```

1. 设置播放器的属性。

   以下是一些可用的`PTMediaPlayer`属性：

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

1. 在当前视图的子视图中添加播放器的视图。

   ```
   [self.adPlayerView  setAutoresizesSubviews:YES];  
   [self.adPlayerView addSubview:(UIView *)player.view];
   ```

1. 调用`play`以播放开始媒体。

   ```
   [player play];
   ```

