---
title: 性能调整
description: 性能调整
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---


# 性能调整{#performance-tuning}

使用以下提示帮助提高性能：

* 使用网络HSM比使用直接连接的HSM要慢得多。
* 为了提高性能，您可以通过部署位于SDK的“thirdparty/cryptoj”文件夹中的特定平台库，选择启用对加密操作的本机支持。 要启用本机支持，请将平台的库（适用于Windows的jsafe.dll或适用于Linux的libjsafe.so）添加到路径中。

   >[!NOTE]
   >
   >如果在同一Tomcat实例中运行多个Web应用程序，并且路径上有`jsafe.dll`，则只有加载的第一个Web应用程序能够加载`jsafe.dll`库。 因此，只有第一个Web应用程序能够从本机支持中受益。 在这种情况下，要提高所有Web应用程序的性能，请将`cryptoj.jar`放在WAR文件之外。 例如，在`<tomcat_installation_folder>/lib`目录中。

* 64位操作系统（如64位版本的Red Hat®或Windows）比32位操作系统提供更好的性能。

