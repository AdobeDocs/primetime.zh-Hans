---
description: 浏览器TVSDK库的通知部分允许您创建可用于诊断和验证目的的日志记录和调试系统。
title: 通知系统
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# 通知系统 {#notification-system}

浏览器TVSDK库的通知部分允许您创建可用于诊断和验证目的的日志记录和调试系统。

<!--<a id="section_EC5DBE8DDA434B70A01FA2F3EF4618BD"></a>-->

浏览器TVSDK具有 *不可丢弃* 其API的政策。 大多数方法会返回 `PSDKErrorCode` 指示方法是否已成功执行的值。 要获取所有可能的完整列表，请执行以下操作 `PSDKErrorCode` 值，请参阅浏览器TVSDK API引用。

通过特定事件通知异步错误。

浏览器TVSDK调度 `MediaPlayer` 事件，用于提供有关播放器活动的信息。 您必须实施事件侦听器来捕获和响应这些事件。

>[!TIP]
>
>关键事件和信息记录在Web浏览器控制台上。

## 收听通知 {#section_06B96633433D497E842FB7ADD5F2C7DA}

您可以监听通知，并将您自己的通知添加到通知历史记录中。 浏览器TVSDK通知系统的核心是 `Notification` 类，表示独立通知。

要设置应用程序以侦听通知，请执行以下操作：

1. 使用MediaPlayer实例监听MediaPlayer状态更改。

   ```js
   player.addEventListener( 
         AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange);
   ```

1. 实施回调。

   回调将接收 `AdobePSDK.MediaPlayerStatusChangeEvent`，浏览器TVSDK会将此事件对象传递到包含新播放器状态的回调。
1. 您的应用程序可以使用侦听由浏览器TVSDK调度的其他事件。 `MediaPlayer` 实例。
