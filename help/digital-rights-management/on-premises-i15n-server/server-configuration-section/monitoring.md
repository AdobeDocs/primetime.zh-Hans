---
seo-title: 监控
title: 监控
uuid: ee62c55f-0d44-40f4-a2c7-39456f4d3d99
translation-type: tm+mt
source-git-commit: 1547eb3dd220fafc08df923f40504736c16a866c
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# 监视{#monitoring}

个性化服务器和密钥生成服务器都有一个状态页，您可以使用它确定服务器的运行状况。

* **个性化状态页：** [!DNL https://SERVER:PORT/flashaccess/status]

   * 如果应用程序服务器正在运行且应用程序可以向密钥生成服务器发出GET请求，则报告“活动”
   * 该页面报告“活动”或不报告任何内容。 没有显示有关应用程序的信息，因此此页可用于从防火墙外进行监视。

* **“密钥生成状态”页：** [!DNL https://SERVER:PORT/flashaccess-kgs/status]

   * 如果应用程序服务器正在运行，则报告“活动”
   * 所有密钥生成URL必须只能在内部访问

* **“个性化统计信息”页：** [!DNL https://SERVER:PORT/flashaccess/admin/appstats]

   * 包括有关个性化服务器的统计信息，如已服务的请求数和缓存中可用的密钥数
   * 此页面必须仅可在内部访问

* **“密钥生成统计信息”页：** [!DNL https://SERVER:PORT/flashaccess-kgs/appstats]

   * 包括关于密钥生成服务器的统计信息，如所服务的请求数和磁盘上可用的密钥文件数
   * 所有密钥生成URL必须只能在内部访问

