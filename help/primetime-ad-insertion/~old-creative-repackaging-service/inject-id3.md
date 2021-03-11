---
description: CRS可以将ID3定时元数据注入HLS格式广告创意，以便于客户端广告跟踪。
title: 使用CRS插入ID3定时元数据标记
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---


# 使用CRS插入ID3定时元数据标记{#using-crs-to-inject-id-timed-metadata-tags}

CRS可以将ID3定时元数据注入HLS格式广告创意，以便于客户端广告跟踪。

客户端播放器读取ID3元数据以启用帧精确广告跟踪。

>[!NOTE]
>
>ID3定时元数据注入仅在iOS上的Safari上有效。

## ID3注入{#workflow-for-crs-for-id3-injection}的CRS工作流

ID3注入的工作流与[ JIT重新打包的详细工作流相同。](../~old-creative-repackaging-service/jit-repackage.md) 如果清单服务器收 `ptplayer=ios-mobileweb` 到该参数，它会告知CRS在将ID3数据包上载到CDN服务器之前将其注入转码广告创意。

>[!NOTE]
>
>在多CDN设置中，清单服务器使用引导URL中的`ptcdn`参数来标识CDN服务器以上传广告创意。