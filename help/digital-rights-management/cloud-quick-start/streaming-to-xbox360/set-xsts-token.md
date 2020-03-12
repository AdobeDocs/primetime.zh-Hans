---
description: 'null'
seo-description: 'null'
seo-title: 在播放器中设置XSTS令牌
title: 在播放器中设置XSTS令牌
uuid: 8995e029-deee-4e23-9cda-a50de8c4f2c0
translation-type: tm+mt
source-git-commit: b7f52b71bde1d7bf59ef51d4f6f90dfaa07e347b

---


# 在播放器中设置XSTS令牌{#set-the-xsts-token-in-your-player}

在Xbox360中，您可以异步设置令牌以响应该事 `MediaPlayer.RequestKeyAttribute` 件。

设置XSTS令牌。

与软件捆绑的范例应用程序演示如何在播放器中设置XSTS令牌。 以下是示例播放器中的相关代码片断：

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

