---
seo-title: 创建DRMErrorEvent处理函数
title: 创建DRMErrorEvent处理函数
uuid: dde660fc-6899-47d4-97d4-46acda2db262
translation-type: tm+mt
source-git-commit: 5749142d42f7d7b36c96592955d1f71f6a7956fc
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---


# 创建DRMErrorEvent处理函数{#create-a-drmerrorevent-handler}

创建一个事件处理程序，以在尝试播放受保护的内容时遇到错误时处理从Primetime调度的错误事件。

通常，当应用程序遇到错误时，它会执行任意数量的清理任务。 然后，它会通知用户该错误并提供解决该问题的选项。

```
private function drmErrorEventHandler(event:DRMErrorEvent):void {  
    trace(event.toString());  
} 
```

