---
description: 您可以实施自己的日志记录系统。
seo-description: 您可以实施自己的日志记录系统。
seo-title: 了解自定义日志记录
title: 了解自定义日志记录
uuid: f056d7d7-ec3a-4cf1-997f-72a89bbc9447
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# 自定义日志记录 {#customized-logging}

您可以实施自己的日志记录系统。

除了使用预定义通知进行记录外，您还可以实现一个记录系统，该系统使用TVSDK生成的日志消息和消息。 有关预定义通知的详细信息，请参 [阅通知系统](https://help.adobe.com/en_US/primetime/psdk/ios/index.html#PSDKs-concept-The_Notification_System)。 您可以使用这些日志对播放器应用程序进行疑难解答，并更好地了解播放和广告工作流程。

自定义日志记录使用的共享单例 `PSDKPTLogFactory`程，该实例提供了将消息记录到多个记录器的机制。 您可以定义并向中添加（注册）一个或多个记录器 `PTLogFactory`。 这允许您使用自定义实现定义多个记录器，如控制台记录器、Web记录器或控制台历史记录器。

TVSDK会为其许多活动生成日志消息，并将其转 `PTLogFactory` 发给所有已注册的记录器。 您的应用程序还可以生成自定义日志消息，这些消息将转发到所有已注册的记录器。 每个记录器都可以过滤消息并采取相应的操作。

有两种实现方 `PTLogFactory`式：

* 用于监听日志。
* 用于向添加日志 `PTLogFactory`。

## 侦听日志 {#listen-to-logs}

要注册以监听日志，请执行以下操作：
1. 实现遵循协议的自定义类 `PTLogger`:

   ```
   @implementation PTConsoleLogger 
   
   + (PTConsoleLogger *) consoleLogger { 
       return [[[PTConsoleLogger alloc] init] autorelease]; 
   } 
   
   - (void)logEntry:(PTLogEntry *)entry { 
       //Log the message to the console using NSLog  
       NSLog(@"[%@] %@", entry.tag, entry.message); 
   } 
   
   @end
   ```

1. 要注册该实例以接收日志记录条目，请将该实例的一个实例 `PTLogger` 添加到 `PTLoggerFactory`:

   ```
   PTConsoleLogger *logger = [PTConsoleLogger consoleLogger]; 
   // Either use the addLogger method: 
   [[PTLogFactory sharedInstance] addLogger:(logger)] 
   
   //Or replace the preceding line with this macro for ease of use 
   //PTLogAddLogger(logger); 
   ```

<!--<a id="example_3738B5A8B4C048D28695E62297CF39E3"></a>-->

以下是使用类型筛选日志的示 `PTLogEntry` 例：

```
@implementation PTConsoleLogger 
 
+ (PTConsoleLogger *) consoleLogger { 
    return [[[PTConsoleLogger alloc] init] autorelease]; 
} 
 
- (id) init { 
    self = [super init]; 
 
    if (self) { 
        self.logLevel = PTLogEntryTypeInfo; 
    } 
 
    return self; 
} 
 
- (void)logEntry:(PTLogEntry *) entry { 
    //Filtering the entry by log level  
    if (entry.type < _logLevel) { 
        return; 
    } 
 
    //Log the message to the console using NSLog NSLog(@"[%@] %@", entry.tag, entry.message); 
} 
 
@end
```

## 添加新日志消息 {#add-new-log-messages}

要注册以侦听日志，请执行以下操作：

新建并 `PTLogEntry` 将其添加到 `thePTLogFactory`:

您可以手动实例化某 `PTLogEntry` 个实例并将其添加到共享 `PTLogFactory` 实例中，或使用其中一个宏完成同一任务。

以下是使用宏进行记录的示 `PTLogDebug` 例：

<!--<a id="example_F014436E1686468F941F4EBD1A21B18E"></a>-->

```
// The following line creates an instance of PTLogEntry with type PTLogEntryDebug, 
// tag "DEBUG_PLAYBACK", and message "Playback has started". 
// Then the PTLogEntry is automatically added to the PTLogFactory  
 
PTLogDebug(@"[DEBUG_PLAYBACK] Playback has started");
```
