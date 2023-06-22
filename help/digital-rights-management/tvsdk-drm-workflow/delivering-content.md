---
title: 交付内容
description: 交付内容
copied-description: true
exl-id: a55293f0-ef9b-468f-a1b2-8222ebab0b4b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---

# 交付内容 {#delivering-content}

Primetime DRM与内容的投放机制无关，因为运行时从网络层抽象出并简单地将受保护的内容提供给Primetime DRM子系统。 因此，可以通过HTTP、HTTP Dynamic Streaming、RTMP或RTMPE、HLS等传递内容。

但是，根据协议，检索受保护内容的元数据可能会涉及一些错综复杂的问题( `DRMContentData`  — 通常采用侧载的形式 [!DNL .metadata] 文件)。 调用任何DRM都需要此DRM元数据 `DRMManager` API，例如预取许可证、DRM身份验证或加入设备域。 例如，使用RTMP/RTMPE协议时，只能通过Flash Media Server(FMS)将FLV和F4V数据传递给客户端。 因此，客户端必须通过其他方式检索元数据blob。 解决此问题的一个选项是将元数据托管在HTTP Web服务器上，并根据要播放的内容实施客户端视频播放器以检索相应的元数据。

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
