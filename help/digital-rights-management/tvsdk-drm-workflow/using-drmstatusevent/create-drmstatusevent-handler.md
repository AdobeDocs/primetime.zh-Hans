---
seo-title: 创建DRMStatusEvent处理函数
title: 创建DRMStatusEvent处理函数
uuid: 64f539d9-344c-4372-88b8-c8d098af9dd8
translation-type: tm+mt
source-git-commit: 5749142d42f7d7b36c96592955d1f71f6a7956fc
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---


# 创建DRMStatusEvent处理函数{#create-a-drmstatusevent-handler}

以下示例创建一个事件处理函数，它输出发起事件的Primetime对象的DRM内容状态信息。

向指向受保护内容的Primetime对象添加事件处理程序：

```
function drmStatusEventHandler(event:DRMStatusEvent):void { trace(event); } 
```

