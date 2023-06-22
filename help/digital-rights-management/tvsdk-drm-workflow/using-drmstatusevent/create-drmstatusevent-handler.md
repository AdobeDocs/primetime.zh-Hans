---
title: 创建DRMStatusEvent处理程序
description: 创建DRMStatusEvent处理程序
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---


# 创建DRMStatusEvent处理程序{#create-a-drmstatusevent-handler}

以下示例创建一个事件处理程序，该处理程序输出发起事件的Primetime对象的DRM内容状态信息。

将事件处理程序添加到指向受保护内容的Primetime对象：

```
function drmStatusEventHandler(event:DRMStatusEvent):void { trace(event); } 
```

