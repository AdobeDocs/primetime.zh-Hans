---
description: 您可以从基于TVSDK的发送器应用程序中转播任何流，并通过浏览器TVSDK在Chromecast上回放该流。
seo-description: 您可以从基于TVSDK的发送器应用程序中转播任何流，并通过浏览器TVSDK在Chromecast上回放该流。
seo-title: 适用于浏览器TVSDK的Google Cast应用程序
title: 适用于浏览器TVSDK的Google Cast应用程序
uuid: 018143e2-143a-4f88-97c6-4b10a2083f9e
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---


# 用于浏览器TVSDK的Google Cast应用程序{#google-cast-app-for-browser-tvsdk}

您可以从基于TVSDK的发送器应用程序中转播任何流，并通过浏览器TVSDK在Chromecast上回放该流。

<!--<a id="section_87CE5D6D46F0439EB6E63A742D6DD9C8"></a>-->

支持Cast的应用程序有两个组件：

* 发送者应用程序，充当远程控制。

   发送者应用程序包括智能电话、个人计算机等。 可使用适用于iOS、Android和Chrome的本机SDK开发应用程序。
* 接收器应用程序，它在Chromecast上运行并播放内容。

   >[!IMPORTANT]
   >
   >此应用程序只能是HTML5应用程序。

发送方和接收方通过使用Cast SDK传递消息进行通信。

## 基本工作流{#section_FAF680FF29DA4D24A50AC0A2B6402B58}

以下是该过程的概述：

1. 发送方应用程序与接收方应用程序建立连接。
1. 发送方应用程序发送消息以在接收方应用程序上加载媒体。
1. 接收器应用程序开始播放。
1. 发送方应用程序将播放、暂停、搜索、快进、快退、倒回、音量更改等播放控制消息发送给接收方应用程序。
1. 接收器应用程序将对这些消息做出响应。

## 消息格式{#section_1624159DD51D4C87B3E5803DEEBCB6B7}

您必须定义消息，以便发送方和接收方能够理解。 以下是搜索消息的示例：

```js
{ 
"type": "seek", 
"seekTo": 10000 
} 
```

在通过Cast SDK发送自定义消息（如搜索消息）时，需要自定义消息命名空间。 以下是JavaScript的示例：

```js
Custom Message Namespace 
var MSG_NAMESPACE = "urn:x-cast:com.adobe.primetime"; 
```

## 建立连接{#section_B4D40CABDD3E46FDBE7B5651DFF91653}

>[!IMPORTANT]
>
>建立连接时不涉及浏览器TVSDK API。

要建立连接，发送方和接收方必须完成以下任务:

* 发送方必须查看位于[发送方应用程序开发](https://developers.google.com/cast/docs/sender_apps)的平台文档。
* 接收方使用Cast接收方API与发送方应用程序建立连接。 例如：

   ```js
   window.castReceiverManager = cast.receiver.CastReceiverManager.getInstance(); 
   
   window.castReceiverManager.onReady = function (event) { /*handle event*/ }; 
   window.castReceiverManager.onSenderConnected = function (event) { /*handle event*/ }; 
   window.castReceiverManager.onSenderDisconnected = function (event) { /*handle event*/ }; 
   
   var customMessageBus = window.castReceiverManager.getCastMessageBus(MSG_NAMESPACE); 
   customMessageBus.onMessage = function (event) { /*handle messages*/ }; 
   
   window.castReceiverManager.start(); 
   ```

## 消息处理{#section_3E4814546F5946C9B3E7A1AE384B4FF8}

要向接收方发送消息，请参阅发送方平台的相关文档。

>[!IMPORTANT]
>
>必须在所有消息中包含自定义消息命名空间`MSG_NAMESPACE`。

对于接收器应用程序，请按照cast接收器API的文档操作。

**基于Chrome的发件人消息示例**

```js
window.session.sendMessage(MSG_NAMESPACE, message, successCallback, errorCallback); //https://developers.google.com/cast/docs/reference/chrome/chrome.cast.Session#sendMessage
```

**基于Chrome的发件人事件处理**

将事件处理程序绑定到将在触发相应事件时发送消息的UI元素。 例如，对于基于Chrome的发送者应用程序，搜索事件可能会发送如下：

```js
document.getElementById("#seekBar").addEventListener("click", seekEventHandler); 
   
function seekEventHandler(event) { 
    seekMessage = { type: "seek", seekTo: player.currentTime }; //player is an instance of AdobePSDK.MediaPlayer 
    window.session.sendMessage(MSG_NAMESPACE, seekMessage, successCallback, errorCallback); 
} 
```

**接收方消息处理**

从接收方应用程序中，以下是如何处理搜索消息的示例：

```js
customMessageBus.onMessage = function (event) { 
    var message = JSON.parse(event.data); 
    switch (message.type) { 
        case "seek":  
            player.seek(parseInt(message.seekTo)); 
            break; 
        //code for handling other events 
        default:  
            break; 
    } 
}; 
```

