---
title: 性能调整
description: 性能调整
copied-description: true
exl-id: 1b54b7c2-da32-47db-b57f-b2afbaf386c4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# 性能调整{#performance-tuning}

使用下列提示帮助提高性能：

* 使用网络HSM比使用直连HSM要慢得多。
* 为了提高性能，您可以部署位于以下位置的特定于平台的库，以选择性地启用对加密操作的本机支持： [!DNL thirdparty/cryptoj] SDK的文件夹。 要启用本机支持，请将平台的库（适用于Windows的jsafe.dll或适用于Linux的libjsafe.so）添加到路径中。

   >[!NOTE]
   >
   >如果您在同一Tomcat实例中运行多个Web应用程序并具有 `jsafe.dll` 在路径上，只有加载的第一个Web应用程序才能加载 `jsafe.dll` 库。 因此，只有第一个Web应用程序才能获得本机支持的好处。 在这种情况下，为了提高所有Web应用程序的性能，请放置 `cryptoj.jar`在WAR文件之外。 例如，在 `<tomcat_installation_folder>/lib` 目录。

* 64位操作系统(如64位版本的Red Hat®或Windows)比32位操作系统提供更好的性能。

## 生成随机数(Linux) {#section_3E2E936A538F40B7BF8892C65E117907}

在某些情况下，Linux环境在执行需要生成随机数的Primetime DRM相关操作时可能会暂停，包括：

* 启动Adobe Primetime DRM许可证服务器
* 使用生成策略 [!DNL AdobePolicyManager] 实用工具
* 使用Adobe Medium Server或Primetime OfflinePackager打包受DRM保护的内容

这些操作中的延迟通常是由于Linux服务器上的低熵池造成的。

在Linux上，随机数是从服务器环境的熵池生成的。 熵池通常通过Linux内核接收硬件中断来维护。 如果服务器被隔离并且没有接收来自硬件资源（例如鼠标或键盘）的定期输入，则重新填充熵池的等待可能会被延长。 在此场景中，等待来自的数据的操作 [!DNL /dev/random] 可能会暂停。

可以在Linux服务器上使用硬件随机数生成器以确保生成足够的熵。 但是，如果硬件随机数生成器在给定的部署方案中不可用，则可以使用基于软件的解决方案来提高熵池刷新率。 在Linux上，此类软件解决方案之一是 [!DNL haveged] （Hardware Volatile Entropy Gathering and Expansion守护程序）。

## 确定可用熵 {#section_686B311FE6144566B6939E9F20915ADC}

要验证在意外延迟期间给定服务器的熵池中可用的位数，请执行以下命令：

```
cat /proc/sys/kernel/random/entropy_avail 
```

一个拥有大量可用熵的健康Linux系统将返回接近全部4,096位熵。 如果返回的值小于200，则系统运行时的熵非常低。
