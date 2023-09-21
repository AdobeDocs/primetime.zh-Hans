---
description: 您可以从基于TVSDK的发件人应用程序中转换任何流，并使用浏览器TVSDK在Chromecast上播放该流。
title: 适用于浏览器TVSDK的Google Cast应用程序
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# 适用于浏览器TVSDK的Google Cast应用程序{#google-cast-app-for-browser-tvsdk}

您可以从基于TVSDK的发件人应用程序中转换任何流，并使用浏览器TVSDK在Chromecast上播放该流。

<!--<a id="section_87CE5D6D46F0439EB6E63A742D6DD9C8"></a>-->

启用了强制转换的应用程序包含两个组件：

* 发件人应用程序，充当远程控件。

  发件人应用程序包括智能手机、个人电脑等。 可以使用适用于iOS、Android和Chrome的原生SDK开发应用程序。
* 接收方应用程序，在Chromecast上运行并播放内容。

  >[!IMPORTANT]
  >
  >此应用程序只能是HTML5应用程序。

发送者和接收者通过使用Cast SDK传递消息来进行通信。

## 基本工作流 {#section_FAF680FF29DA4D24A50AC0A2B6402B58}

以下是此过程的概述：

1. 发件人应用程序与接收人应用程序建立连接。
1. 发送方应用程序发送消息，以在接收方应用程序上加载媒体。
1. 接收方应用程序开始播放。
1. 发送方应用程序向接收方应用程序发送播放控制消息，如播放、暂停、搜寻、快进、快速倒带、倒带、音量更改等。
1. 接收方应用程序对这些消息做出反应。

## 消息格式 {#section_1624159DD51D4C87B3E5803DEEBCB6B7}

您必须定义报文，以便发送者和接收者能够理解。 以下是搜寻消息的示例：

```js
{ 
"type": "seek", 
"seekTo": 10000 
} 
```

通过Cast SDK发送自定义消息（如搜寻消息）时，需要自定义消息命名空间。 以下是JavaScript中的示例：

```js
Custom Message Namespace 
var MSG_NAMESPACE = "urn:x-cast:com.adobe.primetime"; 
```

## 建立连接 {#section_B4D40CABDD3E46FDBE7B5651DFF91653}

>[!IMPORTANT]
>
>建立连接时不包括浏览器TVSDK API。

要建立连接，发送者和接收者必须完成以下任务：

* 发件人必须查看位于的平台文档 [发件人应用程序开发](https://developers.google.com/cast/docs/sender_apps).
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

## 消息处理 {#section_3E4814546F5946C9B3E7A1AE384B4FF8}

要向接收者发送消息，请参阅有关发件人平台的文档。

>[!IMPORTANT]
>
>您必须包括自定义消息命名空间， `MSG_NAMESPACE` 所有消息中。

对于接收器应用程序，请按照铸造接收器API的文档操作。

**基于Chrome的发件人消息示例**

```js
window.session.sendMessage(MSG_NAMESPACE, message, successCallback, errorCallback); //https://developers.google.com/cast/docs/reference/chrome/chrome.cast.Session#sendMessage
```

**基于Chrome的发件人事件处理**

将事件处理程序绑定到UI元素，这些元素将在触发相应事件时发送消息。 例如，对于基于Chrome的发件人应用程序，搜寻事件可能会按如下方式发送：

```js
document.getElementById("#seekBar").addEventListener("click", seekEventHandler); 
   
function seekEventHandler(event) { 
    seekMessage = { type: "seek", seekTo: player.currentTime }; //player is an instance of AdobePSDK.MediaPlayer 
    window.session.sendMessage(MSG_NAMESPACE, seekMessage, successCallback, errorCallback); 
} 
```

**接收方消息处理**

在接收方应用程序中，以下是如何处理搜寻消息的示例：

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
