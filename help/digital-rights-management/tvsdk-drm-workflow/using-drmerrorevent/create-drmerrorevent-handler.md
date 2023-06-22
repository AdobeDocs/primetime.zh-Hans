---
title: 创建DRMErrorEvent处理程序
description: 创建DRMErrorEvent处理程序
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---


# 创建DRMErrorEvent处理程序{#create-a-drmerrorevent-handler}

创建一个事件处理程序，以便在尝试播放受保护内容时遇到错误时处理从Primetime调度的错误事件。

通常，当应用程序遇到错误时，它会执行任意数量的清理任务。 然后，它会通知用户该错误，并提供解决问题的选项。

```
private function drmErrorEventHandler(event:DRMErrorEvent):void {  
    trace(event.toString());  
} 
```

