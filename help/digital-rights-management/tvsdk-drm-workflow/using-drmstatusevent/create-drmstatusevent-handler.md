---
title: 创建DRMStatusEvent处理函数
description: 创建DRMStatusEvent处理函数
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---


# 创建DRMStatusEvent处理函数{#create-a-drmstatusevent-handler}

下面的示例创建一个事件处理函数，它输出发起事件的Primetime对象的DRM内容状态信息。

向指向受保护内容的Primetime对象添加事件处理函数：

```
function drmStatusEventHandler(event:DRMStatusEvent):void { trace(event); } 
```

