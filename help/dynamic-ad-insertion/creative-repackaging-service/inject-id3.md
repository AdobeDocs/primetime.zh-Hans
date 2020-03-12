---
description: CRS可以将ID3定时元数据注入HLS格式的广告创意中，以便于客户端广告跟踪。
seo-description: CRS可以将ID3定时元数据注入HLS格式的广告创意中，以便于客户端广告跟踪。
seo-title: 使用CRS插入ID3定时元数据标记
title: 使用CRS插入ID3定时元数据标记
uuid: 491bbb9e-15de-4871-baa1-f7bb0ea0dde2
translation-type: tm+mt
source-git-commit: c2216a5089d23ca1fcbb77c87b4a01a6fa1807ff

---


# 使用CRS插入ID3定时元数据标记 {#using-crs-to-inject-id-timed-metadata-tags}

CRS可以将ID3定时元数据注入HLS格式的广告创意中，以便于客户端广告跟踪。

客户端播放器读取ID3元数据以启用帧精确的广告跟踪。

>[!NOTE]
>
>ID3定时元数据注入仅在iOS上的Safari上有效。

## ID3注入的CRS工作流 {#workflow-for-crs-for-id3-injection}

ID3注入的工作流与JIT重新打包的详 [细工作流中的工作流相同。](../creative-repackaging-service/jit-repackage.md) 如果清单服务器收 `ptplayer=ios-mobileweb` 到该参数，它会告知CRS在将ID3包上传到CDN服务器之前，将其注入转码广告创意中。

>[!NOTE]
>
>在多CDN设置中，清单服务器使用引导URL `ptcdn` 中的参数来标识CDN服务器以上传广告创意。