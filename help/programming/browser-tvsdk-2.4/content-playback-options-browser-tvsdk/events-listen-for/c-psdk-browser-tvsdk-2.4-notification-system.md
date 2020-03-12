---
description: 浏览器TVSDK库的通知部分允许您创建可用于诊断和验证目的的记录和调试系统。
seo-description: 浏览器TVSDK库的通知部分允许您创建可用于诊断和验证目的的记录和调试系统。
seo-title: 通知系统
title: 通知系统
uuid: 69c4ff1d-3167-413b-ab49-942a5ddc34d7
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 通知系统 {#notification-system}

浏览器TVSDK库的通知部分允许您创建可用于诊断和验证目的的记录和调试系统。

<!--<a id="section_EC5DBE8DDA434B70A01FA2F3EF4618BD"></a>-->

浏览器TVSDK的API *有* “无抛出”策略。 大多数方法都会返 `PSDKErrorCode` 回一个值来指示该方法是否成功执行。 有关所有可能值的完整列 `PSDKErrorCode` 表，请参阅浏览器TVSDK API参考。

通过特定事件通知异步错误。

浏览器TVSDK调度 `MediaPlayer` 事件以提供有关播放器活动的信息。 必须实现事件监听器才能捕获这些事件并对其做出响应。

>[!TIP]
>
>关键事件和信息会记录在Web浏览器控制台上。

## 侦听通知 {#section_06B96633433D497E842FB7ADD5F2C7DA}

您可以侦听通知并将您自己的通知添加到通知历史记录。 浏览器TVSDK通知系统的核心是类， `Notification` 它表示一个独立通知。

要设置应用程序以监听通知，请执行以下操作：

1. 使用MediaPlayer实例侦听MediaPlayer状态更改。

   ```js
   player.addEventListener( 
         AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange);
   ```

1. 实现回调。

   回调接收该事件的一个实 `AdobePSDK.MediaPlayerStatusChangeEvent`例，而Browser TVSDK将此事件对象传递给包含新播放器状态的回调。
1. 您的应用程序可以使用该实例侦听由浏览器TVSDK调度的其他 `MediaPlayer` 事件。

