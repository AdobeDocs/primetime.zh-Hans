---
description: PTNotification对象提供有关播放器状态、警告和错误更改的信息。 停止播放视频的错误还会导致播放器的状态发生变化。
title: 播放器状态、活动、错误和日志的通知
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---


# 播放器状态、活动、错误和日志记录{#notifications-for-player-status-activity-errors-and-logs-overview}的通知

PTNotification对象提供有关播放器状态、警告和错误更改的信息。 停止播放视频的错误还会导致播放器的状态发生变化。

应用程序可以检索通知和状态信息。 您还可以使用通知信息为诊断和验证创建日志记录系统。

>[!IMPORTANT]
>
>TVSDK还使用&#x200B;*`notification`*&#x200B;引用`NSNotifications`（`PTMediaPlayer`通知）*`event`*&#x200B;通知，分派用于提供有关播放器活动的信息。

TVSDK在发出`PTNotification`时也会发出`PTMediaPlayerNewNotificationItemEntryNotification`问题。

您实现事件监听器以捕获和响应事件。 许多事件提供`PTNotification`状态通知。

## 通知内容{#notification-content}

PTNotification提供与播放器状态相关的信息。

TVSDK提供`PTNotification`通知的时间列表。 每个通知都包含以下信息：

* 时间戳
* 包含以下元素的诊断元数据：

   * `type`:信息、警告或错误。
   * `code`:通知的数字表示。
   * `name`:通知的用户可读描述，如SEEK_ERROR
   * `metadata`:包含有关通知的相关信息的键/值对。例如，名为`URL`的键提供一个值，该值是与通知相关的URL。

   * `innerNotification`:直接影响此 `PTNotification` 通知的对象的引用。

您可以将此信息存储在本地以备以后分析，或将其发送到远程服务器以进行记录和图形表示。

## 通知设置{#notification-setup}

TVSDK为基本通知设置播放器，但您必须完成自定义通知的相同设置。

`PTNotification`有两个实现：

* 听
* 向`PTNotificationHistory`添加自定义通知

要侦听通知，TVSDK将`PTNotification`类实例化并将其附加到附加到PTMediaPlayer实例的`PTMediaPlayerItem`实例。 每个`PTMediaPlayer`只有一个`PTNotificationHistory`实例。

>[!IMPORTANT]
>
>如果添加自定义项，则您的应用程序（而非TVSDK）必须执行这些步骤。

## 侦听通知{#listen-to-notifications}

在`PTMediaPlayer`中，有两种方法可以侦听`PTNotification`通知：

1. 使用计时器手动检查`PTMediaPlayerItem`的`PTNotificationHistory`并检查区别：

   ```
   //Access to the PTMediaPlayerItem  
   PTMediaPlayerItem *item = self.player.currentItem; 
   PTNotificationHistory *notificationHistory = item.notificationHistory; 
   
   //Get the list of notification events from the notification History  
   NSArray *notifications = notificationHistory.notificationItems;
   ```

1. 使用`PTMediaPlayerPTMediaPlayerNewNotificationEntryAddedNotification`的已发布[NSNotification](https://developer.apple.com/library/mac/%23documentation/Cocoa/Reference/Foundation/Classes/NSNotification_Class/Reference/Reference.html)。
1. 使用要从中获取通知的`PTMediaPlayer`实例注册到`NSNotification`:

   ```
   //Register to the NSNotification 
   
   [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerNotification:)  
     name:PTMediaPlayerNewNotificationEntryAddedNotification object:self.player];
   ```

## 实现通知回调{#implement-notification-callbacks}

您可以实施通知回调。

1. 通过从`NSNotification`用户信息获取`PTNotification`并使用`PTMediaPlayerNotificationKey`读取其值，实现通知回调：

   ```
   - (void) onMediaPlayerNotification:(NSNotification *) nsnotification { 
       PTNotification *notification = [nsnotification.userInfo objectForKey:PTMediaPlayerNotificationKey]; 
       NSLog(@"Notification: %@", notification); 
   }
   ```

## 添加自定义通知{#add-custom-notifications}

要添加自定义通知：
新建一个`PTNotification`，并使用当前`PTMediaPlayerItem`将其添加到`PTNotificationHistory`:

```
//Access to the PTMediaPlayerItem  
PTMediaPlayerItem *item = self.player.currentItem; 
PTNotificationHistory *notificationHistory = item.notificationHistory; 
 
//Create notification 
PTNotification* notification = [[PTNotification notificationWithType:PTNotificationTypeWarning code:99999 description:@"Custom notification description"]; 
 
//Add notification 
[notificationHistory addNotification:notification];
```
