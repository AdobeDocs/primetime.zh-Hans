---
description: 您可以通过将pttrackingmode和pttrackingversion参数添加到BootstrapURL请求来启用客户端广告跟踪。
title: 启用客户端广告跟踪
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---


# 启用客户端广告跟踪 {#enable-client-side-ad-tracking}

您可以通过添加 `pttrackingmode` 和 `pttrackingversion` BootstrapURL请求的参数。

启用客户端广告跟踪后，您还可以使用跟踪API URL检索广告跟踪元数据。 有关更多详细信息，请参阅 [查询参数](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/notvsdk-csat-ms-interface.md).

要执行客户端广告跟踪，请使用跟踪API URL。

1. 将以下查询参数添加到清单服务器请求URL：

   * `pttrackingmode=simple`
   * `pttrackingversion={format version}`

例如：

```URL
https://. . .?. . .&pttrackingmode=simple&pttrackingversion=v1
```
