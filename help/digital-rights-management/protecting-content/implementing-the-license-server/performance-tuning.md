---
seo-title: 性能调整
title: 性能调整
uuid: db8889c7-ecf5-4551-a6fc-1d3ab992b9ff
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---


# 性能调整{#performance-tuning}

使用以下提示帮助提高性能：

* 使用网络HSM比使用直接连接的HSM要慢得多。
* 为了提高性能，您可以选择通过部署位于SDK文件夹中的平台特定库来启用对加 [!DNL thirdparty/cryptoj] 密操作的本机支持。 要启用本机支持，请将平台的库（适用于Windows的jsafe.dll或适用于Linux的libjsafe.so）添加到路径中。

   >[!NOTE]
   >
   >如果在同一Tomcat实例中运行多个Web应用 `jsafe.dll` 程序并且路径上有，则只有加载的第一个Web应用程序能够加载 `jsafe.dll` 库。 因此，只有第一个Web应用程序能够从本机支持中受益。 在这种情况下，要提高所有Web应用程序的性能， `cryptoj.jar`请置于WAR文件之外。 例如，在目 `<tomcat_installation_folder>/lib` 录中。

* 64位操作系统（如64位版本的Red Hat®或Windows）比32位操作系统提供更好的性能。

## 生成随机数(Linux) {#section_3E2E936A538F40B7BF8892C65E117907}

在某些情况下，Linux环境在进行需要随机数生成的与Primetime DRM相关的操作时可能会暂停，包括：

* 启动Adobe PrimetimeDRM许可证服务器
* 使用实用程序生成策 [!DNL AdobePolicyManager] 略
* 将DRM保护的内容与AdobeMedia Server或Primetime OfflinePackager打包

这些操作中的延迟通常是Linux服务器上熵值池低的结果。

在Linux上，随机数从服务器环境的熵池中产生。 熵池通常由Linux内核接收硬件中断来维护。 如果服务器被隔离并且没有从硬件资源（例如鼠标或键盘）接收常规输入，则等待重新填充熵池可以被扩展。 在这种情况下，等待数据的操作可 [!DNL /dev/random] 能会暂停。

您可以在Linux服务器上使用硬件随机数生成器来确保生成足够的熵。 但是，如果在给定部署方案中硬件随机数生成器不可用，则可以使用基于软件的解决方案来增加熵池刷新率。 在Linux上，这样的软件解决方 [!DNL haveged] 案之一是（HArdware Volatile Entropy Gagering and Expansion守护程序）。

## 确定可用熵 {#section_686B311FE6144566B6939E9F20915ADC}

要在意外延迟期间验证给定服务器的熵池中可用的位数，请执行以下命令：

```
cat /proc/sys/kernel/random/entropy_avail 
```

一个有大量可用熵的健康Linux系统将返回接近4,096位熵的状态。 如果返回的值小于200，则系统在熵值上运行非常低。
