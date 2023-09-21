---
title: 投放内容
description: 投放内容
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---

# 投放内容 {#delivering-content}

Primetime DRM与内容的传输机制无关，因为运行时将网络层抽象出来，并简单地将受保护的内容提供给Primetime DRM子系统。 因此，可以通过HTTP、HTTP Dynamic Streaming、RTMP或RTMPE、HLS等传递内容。

但是，根据协议，检索受保护内容的元数据可能会涉及到一些复杂的问题( `DRMContentData`  — 通常采用侧载形式 [!DNL .metadata] 文件)。 调用任何 `DRMManager` API，例如预取许可证、DRM身份验证或加入设备域。 例如，使用RTMP/RTMPE协议时，只有FLV和F4V数据可以通过Flash Media Server(FMS)传送到客户端。 因此，客户端必须通过其他方式检索元数据blob。 解决此问题的一个选项是在HTTP Web服务器上托管元数据，并根据要播放的内容实施客户端视频播放器以检索相应的元数据。

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
