---
description: PTNotification对象提供有关播放器状态、警告和错误更改的信息。 停止播放视频的错误也会导致播放器的状态发生变化。
seo-description: PTNotification对象提供有关播放器状态、警告和错误更改的信息。 停止播放视频的错误也会导致播放器的状态发生变化。
seo-title: 播放器状态、活动、错误和日志的通知
title: 播放器状态、活动、错误和日志的通知
uuid: 59716a66-3736-4076-8011-8104bfe3a83a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 播放器状态、活动、错误和记录的通知 {#notifications-for-player-status-activity-errors-and-logs-overview}

PTNotification对象提供有关播放器状态、警告和错误更改的信息。 停止播放视频的错误也会导致播放器的状态发生变化。

应用程序可以检索通知和状态信息。 您还可以使用通知信息创建用于诊断和验证的日志记录系统。

>[!IMPORTANT]
>
>TVSDK还使用 *`notification`* 引用（通知） `NSNotifications` 通 `PTMediaPlayer`*`event`* 知，通知被调度来提供有关播放器活动的信息。

TVSDK在出现问题 `PTMediaPlayerNewNotificationItemEntryNotification` 时也会出现问题 `PTNotification`。

您实现事件监听器以捕获事件并对其做出响应。 许多活动都提 `PTNotification` 供状态通知。

## 通知内容 {#notification-content}

PTNotification提供与播放器状态相关的信息。

TVSDK提供通知的时间顺序 `PTNotification` 列表。 每个通知都包含以下信息：

* 时间戳
* 包含以下元素的诊断元数据：

   * `type`:信息、警告或错误。
   * `code`:通知的数字表示。
   * `name`:通知的可读描述，如SEEK_ERROR
   * `metadata`:包含有关通知的相关信息的键／值对。 例如，名为的键 `URL` 提供一个值，该值是与通知相关的URL。

   * `innerNotification`:对直接影响此通 `PTNotification` 知的其他对象的引用。

您可以将此信息存储在本地以供以后分析，或将其发送到远程服务器进行记录和图形表示。

## 通知设置 {#notification-setup}

TVSDK为基本通知设置播放器，但您必须为自定义通知完成相同设置。

有两种实现方 `PTNotification`式：

* 聆听
* 要向 `PTNotificationHistory`

要侦听通知，TVSDK将 `PTNotification` 类实例化并将其附加到PTMediaPlayer实例 `PTMediaPlayerItem`中的实例。 每个实例只 `PTNotificationHistory` 有一个 `PTMediaPlayer`。

>[!IMPORTANT]
>
>如果添加自定义，则您的应用程序（而非TVSDK）必须执行这些步骤。

## 侦听通知 {#listen-to-notifications}

有两种方式可以在中侦听 `PTNotification` 通知 `PTMediaPlayer`:

1. 使用计时 `PTNotificationHistory` 器手动 `PTMediaPlayerItem` 检查其中的项并检查差异：

   ```
   //Access to the PTMediaPlayerItem  
   PTMediaPlayerItem *item = self.player.currentItem; 
   PTNotificationHistory *notificationHistory = item.notificationHistory; 
   
   //Get the list of notification events from the notification History  
   NSArray *notifications = notificationHistory.notificationItems;
   ```

1. 使用发布 [的](https://developer.apple.com/library/mac/%23documentation/Cocoa/Reference/Foundation/Classes/NSNotification_Class/Reference/Reference.html) NSN通知 `PTMediaPlayerPTMediaPlayerNewNotificationEntryAddedNotification`。
1. 使用要 `NSNotification` 从中获取通知 `PTMediaPlayer` 的实例注册到：

   ```
   //Register to the NSNotification 
   
   [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerNotification:)  
     name:PTMediaPlayerNewNotificationEntryAddedNotification object:self.player];
   ```

## 实现通知回呼 {#implement-notification-callbacks}

您可以实现通知回调。

1. 通过从用户信息中获取通知 `PTNotification` 并使用 `NSNotification` 以下方法读取通知回调值 `PTMediaPlayerNotificationKey`:

   ```
   - (void) onMediaPlayerNotification:(NSNotification *) nsnotification { 
       PTNotification *notification = [nsnotification.userInfo objectForKey:PTMediaPlayerNotificationKey]; 
       NSLog(@"Notification: %@", notification); 
   }
   ```

## 添加自定义通知 {#add-custom-notifications}

添加自定义通知：新建一 `PTNotification` 个，然后使用当 `PTNotificationHistory` 前版本将其添加到 `PTMediaPlayerItem`:

```
//Access to the PTMediaPlayerItem  
PTMediaPlayerItem *item = self.player.currentItem; 
PTNotificationHistory *notificationHistory = item.notificationHistory; 
 
//Create notification 
PTNotification* notification = [[PTNotification notificationWithType:PTNotificationTypeWarning code:99999 description:@"Custom notification description"]; 
 
//Add notification 
[notificationHistory addNotification:notification];
```
