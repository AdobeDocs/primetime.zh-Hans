---
seo-title: 交付内容
title: 交付内容
uuid: b277d369-fee3-4a20-9dd8-27b3a8a82a9e
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# 交付内容 {#delivering-content}

Primetime DRM与内容的交付机制无关，因为运行时提取出网络层，并且只向Primetime DRM子系统提供受保护的内容。 因此，内容可以通过HTTP、HTTP动态流、RTMP或RTMPE、HLS等交付。

但是，根据协议，检索受保护内容的元数据可能涉及复杂的问题( `DRMContentData` -通常以侧载文件的形式 [!DNL .metadata] )。 需要此DRM元数据才能调用任何 `DRMManager` API，如预取许可证、DRM身份验证或加入设备域。 例如，使用RTMP/RTMPE协议时，只有FLV和F4V数据才能通过Flash Media Server(FMS)交付到客户端。 因此，客户端必须通过其他方式检索元数据blob。 解决此问题的一个选项是将元数据托管在HTTP Web服务器上，并根据所播放的内容实现客户端视频播放器以检索相应的元数据。

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

