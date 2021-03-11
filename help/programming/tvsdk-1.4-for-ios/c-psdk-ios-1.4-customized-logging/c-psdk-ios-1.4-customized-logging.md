---
description: 您可以实施自己的日志记录系统。
title: 自定义日志
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---


# 自定义日志{#customized-logging}

您可以实施自己的日志记录系统。

除了使用预定义的通知进行记录外，您还可以实施使用TVSDK生成的日志消息和消息的记录系统。 有关预定义通知的详细信息，请参阅[通知系统](../c-psdk-ios-1.4-notification-system/c-psdk-ios-1.4-notification-system.md)。 您可以使用这些日志对播放器应用程序进行疑难解答，并更好地了解播放和广告工作流程。

自定义日志记录使用`PSDKPTLogFactory`的共享单一实例，该实例提供了将消息记录到多个日志程序的机制。 定义一个或多个记录器并将其添加（注册）到`PTLogFactory`。 这允许您使用自定义实现定义多个日志记录器，如控制台记录器、Web记录器或控制台历史记录记录器。

TVSDK为其许多活动生成日志消息，`PTLogFactory`将其转发到所有已注册的日志。 您的应用程序还可以生成自定义日志消息，这些消息将转发到所有已注册的日志服务器。 每个记录器都可以过滤消息并采取适当的操作。

`PTLogFactory`有两个实现：

* 用于侦听日志。
* 用于向`PTLogFactory`添加日志。

## 侦听日志{#listen-to-logs}

要注册以侦听日志，请执行以下操作：
1. 实现遵循协议`PTLogger`的自定义类：

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

1. 要注册该实例以接收日志条目，请将`PTLogger`的实例添加到`PTLoggerFactory`:

   ```
   PTConsoleLogger *logger = [PTConsoleLogger consoleLogger]; 
   // Either use the addLogger method: 
   [[PTLogFactory sharedInstance] addLogger:(logger)] 
   
   //Or replace the preceding line with this macro for ease of use 
   //PTLogAddLogger(logger); 
   ```

<!--<a id="example_3738B5A8B4C048D28695E62297CF39E3"></a>-->

以下是使用`PTLogEntry`类型过滤日志的示例：

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

## 添加新日志消息{#add-new-log-messages}

要注册以侦听日志，请执行以下操作：
1. 新建一个`PTLogEntry`并将其添加到`thePTLogFactory`:

   您可以手动实例化`PTLogEntry`并将其添加到`PTLogFactory`共享实例，或使用其中一个宏来实现相同的任务。

   以下是使用`PTLogDebug`宏进行记录的示例：

<!--<a id="example_F014436E1686468F941F4EBD1A21B18E"></a>-->

```
// The following line creates an instance of PTLogEntry with type PTLogEntryDebug, 
// tag "DEBUG_PLAYBACK", and message "Playback has started". 
// Then the PTLogEntry is automatically added to the PTLogFactory  
 
PTLogDebug(@"[DEBUG_PLAYBACK] Playback has started");
```
