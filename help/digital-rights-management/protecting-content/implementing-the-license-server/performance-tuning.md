---
title: 性能调整
description: 性能调整
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# 性能调整{#performance-tuning}

使用下列提示帮助提高性能：

* 使用网络HSM比使用直连HSM要慢得多。
* 为了提高性能，您可以选择通过部署位于以下位置的特定于平台的库来启用对加密操作的本机支持： [!DNL thirdparty/cryptoj] SDK的文件夹。 要启用本机支持，请将平台的库（适用于Windows的jsafe.dll或适用于Linux的libjsafe.so）添加到路径中。

  >[!NOTE]
  >
  >如果您在同一Tomcat实例中运行多个Web应用程序并且具有 `jsafe.dll` 在路径上，只有加载的第一个Web应用程序才能加载 `jsafe.dll` 库。 因此，只有第一个Web应用程序才能从本机支持中获益。 在这种情况下，为了提高所有Web应用程序的性能，请放置 `cryptoj.jar`在WAR文件之外。 例如，在 `<tomcat_installation_folder>/lib` 目录。

* 64位操作系统(如64位版本的Red Hat®或Windows)比32位操作系统提供更好的性能。

## 生成随机数(Linux) {#section_3E2E936A538F40B7BF8892C65E117907}

在某些情况下，Linux环境在执行需要生成随机数的Primetime DRM相关操作时可能会暂停，包括：

* Adobe Primetime DRM许可证服务器的启动
* 使用生成策略 [!DNL AdobePolicyManager] 效用
* 使用Adobe Media Server或Primetime OfflinePackager打包受DRM保护的内容

这些操作中的延迟通常是Linux服务器上低熵池的结果。

在Linux上，从服务器环境的熵池中生成随机数。 熵池通常通过Linux内核接收硬件中断来维护。 如果服务器被隔离且未接收来自硬件资源（如鼠标或键盘）的定期输入，则重新填充熵池的等待时间可能会延长。 在此方案中，操作等待来自的数据 [!DNL /dev/random] 可能会暂停。

可以在Linux服务器上使用硬件随机数生成器以确保生成足够的熵。 但是，如果硬件随机数生成器在给定部署方案中不可用，则可以使用基于软件的解决方案来增加熵池刷新率。 在Linux上，一种这样的软件解决方案是 [!DNL haveged] （HArdware Volatile Entropy Gathering and Expansion守护程序）。

## 确定可用熵 {#section_686B311FE6144566B6939E9F20915ADC}

要验证在意外延迟期间给定服务器的熵池中可用的位数，请执行以下命令：

```
cat /proc/sys/kernel/random/entropy_avail 
```

一个拥有大量可用熵的健康Linux系统将会返回接近4,096位熵的完整值。 如果返回的值小于200，则系统运行时的熵会非常低。
