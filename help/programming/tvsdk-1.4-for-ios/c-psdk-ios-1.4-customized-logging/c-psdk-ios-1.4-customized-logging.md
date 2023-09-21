---
description: 您可以实施自己的日志记录系统。
title: 自定义日志记录
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---

# 自定义日志记录 {#customized-logging}

您可以实施自己的日志记录系统。

除了使用预定义通知进行日志记录之外，您还可以实施一个日志记录系统，该系统使用您的日志消息和TVSDK生成的消息。 有关预定义通知的详细信息，请参阅 [通知系统](../c-psdk-ios-1.4-notification-system/c-psdk-ios-1.4-notification-system.md). 您可以使用这些日志对播放器应用程序进行故障排除，并更好地了解播放和广告工作流。

自定义日志记录使用 `PSDKPTLogFactory`，提供将消息记录到多个记录器的机制。 您可以定义一个或多个记录器，并将其添加（注册）到 `PTLogFactory`. 这允许您使用自定义实施定义多个记录器，例如控制台记录器、网络记录器或控制台历史记录记录器。

TVSDK会为其许多活动生成日志消息， `PTLogFactory` 转发到所有已注册的记录器。 您的应用程序还可以生成自定义日志消息，这些消息将转发到所有注册的日志程序。 每个日志记录器都可以过滤消息并采取适当措施。

有两种实施 `PTLogFactory`：

* 用于侦听日志。
* 用于将日志添加到 `PTLogFactory`.

## 侦听日志 {#listen-to-logs}

要注册以侦听日志，请执行以下操作：
1. 实施遵循协议的自定义类 `PTLogger`：

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

1. 要注册实例以接收日志记录条目，请添加 `PTLogger` 到 `PTLoggerFactory`：

   ```
   PTConsoleLogger *logger = [PTConsoleLogger consoleLogger]; 
   // Either use the addLogger method: 
   [[PTLogFactory sharedInstance] addLogger:(logger)] 
   
   //Or replace the preceding line with this macro for ease of use 
   //PTLogAddLogger(logger); 
   ```

<!--<a id="example_3738B5A8B4C048D28695E62297CF39E3"></a>-->

以下是使用 `PTLogEntry` 类型：

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

注册以侦听日志：
1. 新建 `PTLogEntry` 并将其添加到 `thePTLogFactory`：

   您可以手动实例化 `PTLogEntry` 并将其添加到 `PTLogFactory` 共享实例或使用其中一个宏完成相同的任务。

   以下是使用 `PTLogDebug` 宏：

<!--<a id="example_F014436E1686468F941F4EBD1A21B18E"></a>-->

```
// The following line creates an instance of PTLogEntry with type PTLogEntryDebug, 
// tag "DEBUG_PLAYBACK", and message "Playback has started". 
// Then the PTLogEntry is automatically added to the PTLogFactory  
 
PTLogDebug(@"[DEBUG_PLAYBACK] Playback has started");
```
