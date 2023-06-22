---
title: 监测
description: 监测
copied-description: true
exl-id: edf62298-4082-4ac1-b2b7-8d0e0959ed04
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# 监测{#monitoring}

“个性化”服务器和密钥生成服务器都有一个状态页面，您可以使用该页面确定服务器的运行状况。

* **个性化状态页面：** [!DNL https://SERVER:PORT/flashaccess/status]

   * 如果应用程序服务器正在运行，且应用程序可以向密钥生成服务器发出GET请求，则会报告“活动”
   * 该页面报告“活动”或没有任何内容。 不会显示任何有关应用程序的信息，因此此页面可用于从防火墙外部进行监视。

* **“密钥生成状态”页：** [!DNL https://SERVER:PORT/flashaccess-kgs/status]

   * 如果应用服务器正在运行，则报告“活动”
   * 所有密钥生成URL必须只能在内部访问

* **“个性化统计信息”页：** [!DNL https://SERVER:PORT/flashaccess/admin/appstats]

   * 包含有关个性化服务器的统计信息，例如提供的请求数和缓存中可用的密钥数
   * 此页面必须只能在内部访问

* **“密钥生成统计信息”页：** [!DNL https://SERVER:PORT/flashaccess-kgs/appstats]

   * 包含有关密钥生成服务器的统计信息，例如提供的请求数和磁盘上可用的密钥文件数
   * 所有密钥生成URL必须只能在内部访问
