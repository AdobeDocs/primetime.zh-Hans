---
description: CRS可以将ID3定时元数据注入HLS格式广告创意中以方便客户端广告跟踪。
title: 使用CRS插入ID3定时元数据标记
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---


# 使用CRS插入ID3定时元数据标记 {#using-crs-to-inject-id-timed-metadata-tags}

CRS可以将ID3定时元数据注入HLS格式广告创意中以方便客户端广告跟踪。

客户端播放器读取ID3元数据以启用帧准确的广告跟踪。

>[!NOTE]
>
>ID3定时元数据注入仅适用于iOS上的Safari。

## 用于ID3注入的CRS的工作流 {#workflow-for-crs-for-id3-injection}

ID3注入的工作流与中的相同 [详细的JIT重新打包工作流。](../~old-creative-repackaging-service/jit-repackage.md) 如果清单服务器收到 `ptplayer=ios-mobileweb` 参数，它会告知CRS在将ID3数据包上传到CDN服务器之前将其注入转码广告创意。

>[!NOTE]
>
>在多CDN设置中，清单服务器使用 `ptcdn` bootstrap URL中的参数，用于标识要上传广告创意的CDN服务器。