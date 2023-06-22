---
title: 在播放器中设置XSTS令牌
description: 在播放器中设置XSTS令牌
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '64'
ht-degree: 0%

---


# 在播放器中设置XSTS令牌{#set-the-xsts-token-in-your-player}

在Xbox360中，您异步设置令牌以响应 `MediaPlayer.RequestKeyAttribute` 事件。

设置XSTS令牌。

与您的软件捆绑在一起的示例应用程序说明了如何在播放器中设置XSTS令牌。 以下是示例播放器中的相关代码片段：

```
   MediaPlayer mMediaPlayer;  
 
mMediaPlayer.RequestKeyAttribute += Player_RequestKeyAttribute;  
 
private void Player_RequestKeyAttribute(object sender, RequestKeyAttributeEventArgs args) {  
    string token = "";  
    // XBOX XSTS Token...  
    KeyAttribute keyAttribute = new KeyAttribute(System.Text.Encoding.UTF8.GetBytes(token), null);  
    mMediaPlayer.SetKeyAttribute(args.RequestIdentifier, keyAttribute);  
} 
```

