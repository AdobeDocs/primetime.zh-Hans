---
seo-title: 性能调整
title: 性能调整
uuid: db8889c7-ecf5-4551-a6fc-1d3ab992b9ff
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 性能调整{#performance-tuning}

使用以下提示帮助提高性能：

* 使用网络HSM比使用直连HSM要慢得多。
* 为提高性能，您可以选择通过部署SDK文件夹中的平台特定库来启用对加密操 [!DNL thirdparty/cryptoj] 作的本机支持。 要启用本机支持，请将平台的库（Windows的jsafe.dll或Linux的libjsafe.so）添加到路径中。

   >[!NOTE] {class=&quot;- topic/note &quot;}
   >
   >如果在同一Tomcat实例中运行多个Web应用程 `jsafe.dll` 序并且路径上有，则只有加载的第一个Web应用程序能够加载该 `jsafe.dll` 库。 因此，只有第一个Web应用程序能够从本机支持中受益。 在这种情况下，要提高所有Web应用程序的性能，请 `cryptoj.jar`置于WAR文件之外。 例如，在目 `<tomcat_installation_folder>/lib` 录中。

* 64位操作系统（如64位版本的Red Hat®或Windows）比32位操作系统提供更好的性能。

## 生成随机数(Linux) {#section_3E2E936A538F40B7BF8892C65E117907}

在某些情况下，Linux环境在执行需要随机数生成的与Primetime DRM相关的操作时可能会暂停，包括：

* 启动Adobe Primetime DRM许可证服务器
* 使用实用程序生成策 [!DNL AdobePolicyManager] 略
* 将受DRM保护的内容与Adobe Media Server或Primetime OfflinePackager打包

这些操作中的延迟通常是Linux服务器上熵值池低的结果。

在Linux上，随机数从服务器环境的熵池中产生。 熵池通常通过Linux内核接收硬件中断来维护。 如果服务器被隔离并且没有从HW资源（例如鼠标或键盘）接收常规输入，则等待重新填充熵池可以延长。 在此方案中，等待数据的操作可 [!DNL /dev/random] 能会暂停。

您可以在Linux服务器上使用硬件随机数生成器来确保生成足够的熵。 但是，如果在给定部署方案中硬件随机数生成器不可用，则可以使用基于软件的解决方案来增加熵池刷新率。 在Linux上，这样的软件解决方案 [!DNL haveged] 之一是（HArdware Volatile Entropy Gaghering and Expansion守护程序）。

## 确定可用熵 {#section_686B311FE6144566B6939E9F20915ADC}

要在意外延迟期间验证给定服务器的熵池中可用的位数，请执行以下命令：

```
cat /proc/sys/kernel/random/entropy_avail 
```

一个健康的Linux系统，有大量可用的熵值，将回到接近4,096位的熵值。 如果返回的值小于200，则系统在熵值上运行得非常低。
