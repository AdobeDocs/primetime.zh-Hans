---
title: 交付内容
description: 交付内容
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---


# 传送内容{#delivering-content}

Primetime DRM与内容的投放机制不相关，因为运行时将网络层抽象出来，而只是将受保护的内容提供给Primetime DRM子系统。 因此，内容可以通过HTTP、HTTP Dynamic Streaming、RTMP或RTMPE、HLS等进行交付。

但是，根据协议，检索受保护内容的元数据时可能涉及复杂问题（`DRMContentData` — 通常以侧加载[!DNL .metadata]文件的形式）。 需要此DRM元数据才能调用任何`DRMManager` API，如预取许可证、DRM身份验证或加入设备域。 例如，使用RTMP/RTMPE协议，只能通过Flash Media Server(FMS)将FLV和F4V数据交付到客户端。 因此，客户端必须通过其他方式检索元数据Blob。 解决此问题的一个选项是在HTTP Web服务器上托管元数据，并实现客户端视频播放器以检索相应的元数据，具体取决于正在播放的内容。

```
private function getMetadata():void { 
    extrapolated-path-to-metadata = "https://metadatas.mywebserver.com/" + videoname; 
     var urlRequest : URLRequest =  
      new URLRequest(extrapolated-path-to-the-metadata + ".metadata");  
    var urlStream : URLStream = new URLStream();  
    urlStream.addEventListener(Event.COMPLETE, handleMetadata);  
    urlStream.addEventListener(IOErrorEvent.NETWORK_ERROR, handleIOError);  
    urlStream.addEventListener(IOErrorEvent.IO_ERROR, handleIOError);  
    urlStream.addEventListener(IOErrorEvent.VERIFY_ERROR, handleIOError);  
 
    try { 
        urlStream.load(urlRequest);  
    } catch(se:SecurityError) { 
        videoLog.text += se.toString() + "\n";  
    } catch(e:Error) { 
        videoLog.text += e.toString() + "\n";  
    } 
} 
```

