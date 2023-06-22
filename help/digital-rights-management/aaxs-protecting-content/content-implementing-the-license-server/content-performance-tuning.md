---
title: 性能调整
description: 性能调整
copied-description: true
exl-id: f6b2338e-a209-4881-a599-ded5f1498daf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---

# 性能调整{#performance-tuning}

使用下列提示帮助提高性能：

* 使用网络HSM比使用直连HSM要慢得多。
* 为了提高性能，您可以选择通过部署位于SDK的“第三方/cryptoj”文件夹中的平台特定库来启用对加密操作的本机支持。 要启用本机支持，请将平台的库（适用于Windows的jsafe.dll或适用于Linux的libjsafe.so）添加到路径中。

   >[!NOTE]
   >
   >如果您在同一Tomcat实例中运行多个Web应用程序并具有 `jsafe.dll` 在路径上，只有加载的第一个Web应用程序才能加载 `jsafe.dll` 库。 因此，只有第一个Web应用程序才能获得本机支持的好处。 在这种情况下，为了提高所有Web应用程序的性能，请放置 `cryptoj.jar`在WAR文件之外。 例如，在 `<tomcat_installation_folder>/lib` 目录。

* 64位操作系统(如64位版本的Red Hat®或Windows)比32位操作系统提供更好的性能。
