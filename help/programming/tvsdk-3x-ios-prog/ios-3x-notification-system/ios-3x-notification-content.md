---
description: PTNotification对象提供有关播放器状态更改、警告和错误的信息。 停止播放视频的错误也会导致播放器状态发生变化。
title: 通知内容
exl-id: 62423718-b154-4105-82b2-f6e389105ec8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---

# 播放器状态、活动、错误和日志记录的通知 {#notifications-player-status-activity-errors-logging}

`PTNotification` 对象提供有关播放器状态更改、警告和错误的信息。 停止播放视频的错误也会导致播放器状态发生变化。

您的应用程序可以检索通知和状态信息。 您还可以使用通知信息创建用于诊断和验证的日志记录系统。

>[!NOTE]
>
>TVSDK还使用 *`notification`* 请参阅 `NSNotifications` ( `PTMediaPlayer` 通知) *`event`* 通知，发送用于提供有关播放器活动的信息。

TVSDK还存在问题 `PTMediaPlayerNewNotificationItemEntryNotification` 何时发出 `PTNotification`.

您可以实施事件侦听器来捕获和响应事件。 许多事件都提供 `PTNotification` 状态通知。

## 通知内容 {#notification-content}

`PTNotification` 提供与播放器状态相关的信息。

TVSDK提供了按时间顺序排列的 `PTNotification` 通知。 每个通知都包含以下信息：

* 时间戳
* 包含以下元素的诊断元数据：

   * `type`：信息、警告或错误。
   * `code`：通知的数值表示形式。
   * `name`：人类可读的通知描述，如SEEK_ERROR
   * `metadata`：包含有关通知的相关信息的键/值对。 例如，一个名为的键 `URL` 提供一个值，该值为与通知相关的URL。

   * `innerNotification`：对另一个的引用 `PTNotification` 直接影响此通知的对象。

您可以将此信息存储在本地，以供以后分析使用，也可以将其发送到远程服务器以进行日志记录和图形显示。

## 通知设置 {#notification-setup}

TVSDK会为基本通知设置播放器，但您必须为自定义通知完成相同的设置。

有两种实施 `PTNotification`：

* 倾听
* 将自定义通知添加到 `PTNotificationHistory`

为了收听通知，TVSDK将 `PTNotification` 类并将其附加到 `PTMediaPlayerItem`，该页面会附加到PTMediaPlayer实例。 只有一个 `PTNotificationHistory` 实例依据 `PTMediaPlayer`.

>[!IMPORTANT]
>
>如果要添加自定义项，则应用程序而非TVSDK必须执行这些步骤。

## 收听通知 {#listen-to-notifications}

有两种方式可以倾听 `PTNotification` 中的通知 `PTMediaPlayer`：

1. 手动检查 `PTNotificationHistory` 的 `PTMediaPlayerItem` 使用计时器并检查二者的区别：

   ```
   //Access to the PTMediaPlayerItem  
   PTMediaPlayerItem *item = self.player.currentItem; 
   PTNotificationHistory *notificationHistory = item.notificationHistory; 
   
   //Get the list of notification events from the notification History  
   NSArray *notifications = notificationHistory.notificationItems;
   ```

1. 使用已发布的 [NSNotification](https://developer.apple.com/library/mac/%23documentation/Cocoa/Reference/Foundation/Classes/NSNotification_Class/Reference/Reference.html) 的 `PTMediaPlayerPTMediaPlayerNewNotificationEntryAddedNotification`.
1. 注册至 `NSNotification` 通过使用 `PTMediaPlayer` 从中获取通知：

   ```
   //Register to the NSNotification 
   
   [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerNotification:)  
     name:PTMediaPlayerNewNotificationEntryAddedNotification object:self.player];
   ```

## 实施通知回调 {#implement-notification-callbacks}

您可以实施通知回调。

通过获取 `PTNotification` 从 `NSNotification` 用户信息并使用读取其值 `PTMediaPlayerNotificationKey`：

```
- (void) onMediaPlayerNotification:(NSNotification *) nsnotification { 
    PTNotification *notification = [nsnotification.userInfo objectForKey:PTMediaPlayerNotificationKey]; 
    NSLog(@"Notification: %@", notification); 
}
```

## 添加自定义通知 {#add-custom-notifications}

添加自定义通知：新建 `PTNotification` 并将其添加到 `PTNotificationHistory` 通过使用当前 `PTMediaPlayerItem`：

```
//Access to the PTMediaPlayerItem  
PTMediaPlayerItem *item = self.player.currentItem; 
PTNotificationHistory *notificationHistory = item.notificationHistory; 
 
//Create notification 
PTNotification* notification = [[PTNotification notificationWithType:PTNotificationTypeWarning code:99999 description:@"Custom notification description"]; 
 
//Add notification 
[notificationHistory addNotification:notification];
```
