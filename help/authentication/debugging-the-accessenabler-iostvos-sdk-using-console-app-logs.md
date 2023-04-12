---
title: 使用控制台应用程序日志调试AccessEnabler iOS/tvOS SDK
description: 使用控制台应用程序日志调试AccessEnabler iOS/tvOS SDK
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---


# 使用控制台应用程序日志调试AccessEnabler iOS/tvOS SDK {#debugging-the-accessenabler-iostvos-sdk-using-console-app-logs}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。


## 概述

本文档的范围是捕获并展示AccessEnabler的iOS/tvOS SDK日志记录机制的演变，以及一些使用控制台应用程序日志调试AccessEnabler框架的有用详细信息。

## 日志记录机制状态

AccessEnabler iOS/tvOS日志记录机制的目的是发出有用的消息，以排除使用AccessEnabler框架的应用程序可能因此而遇到的问题。

### AccessEnabler iOS/tvOS 3.5.0及更高版本

从AccessEnabler iOS/tvOS 3.5.0版本开始，日志记录机制在更改时引入了以下改进：

* AccessEnabler框架使用Apple的建议 [OSLog](https://developer.apple.com/documentation/os/oslog) 实施。

* AccessEnabler框架引入了根据子系统过滤控制台应用程序日志的功能： **com.adobe.pass.AccessEnabler**. SDK发出的所有消息都是com.adobe.pass.AccessEnabler的一部分。

* AccessEnabler框架引入了基于任意（前缀）筛选控制台应用程序日志的功能： **[AccessEnabler]**. SDK发出的所有消息均带有前缀 [AccessEnabler].

* AccessEnabler框架引入了根据类别过滤控制台应用程序日志的功能： **调试**, **错误** 与上述两个标准中的任意一个标准结合使用：子系统或任意（前缀）。

## 使用控制台应用程序日志进行调试

根据所调查的问题，您可能希望包括或排除AccessEnabler框架发出的日志记录消息，因此您可以在下面找到一些有用的详细信息，这些信息可能有助于您在调查期间和使用控制台应用程序日志。


### AccessEnabler iOS/tvOS 3.5.0及更高版本

#### 包括 {#including}

首先，为了能够看到AccessEnabler框架发出的任何日志消息 **必须** 在控制台应用程序的“操作”部分选择“包含信息消息”和“包含调试消息”，如下图所示。

![](assets/include-info-debug-msg.png)


为了能够调试AccessEnabler iOS/tvOS SDK和 **请参阅** AccessEnabler框架日志可以：

* 在控制台应用程序中使用 **子系统** 选项，等同于下图中的com.adobe.pass.AccessEnabler值。

![](assets/subsys-console-app.png)

* 在控制台应用程序中使用 **任意** 选项，其中包含
   [AccessEnabler] 值。

![](assets/any-optn-console-app.png)

除了上述两个标准之外，您还可以使用 **类别** 与 **子系统** 或 **Any（前缀）** 以明确搜索 **调试** 或 **错误** AccessEnabler iOS/tvOS SDK发出的级别消息。

#### 排除

以便能够更好地调试其他组件和 **排除** AccessEnabler框架日志可以：

* 在控制台应用程序中使用 **子系统** 不等于com.adobe.pass.AccessEnabler值的选项。
* 在控制台应用程序中使用 **任意** 不包含的选项 [AccessEnabler] 值。

## 报告问题

向Adobe Primetime身份验证报告问题时，请考虑以下建议：

* 请尝试提供复制步骤。
* 请尝试提供出现问题的操作系统版本和设备型号。
* 请尝试提供遇到问题的AccessEnabler iOS/tvOS SDK版本。
* 请尝试使用 [包括](#including) 中。
