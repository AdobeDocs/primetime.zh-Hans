---
description: 您可以将播放器设置为根据需要经常从QoSProvider中读取播放和设备统计信息。
title: 显示QoS播放和设备统计信息
exl-id: 369b6e9a-70a2-4f62-a1bf-f69030c5d6c3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# 显示QoS播放和设备统计信息 {#display-qos-playback-and-device-statistics}

您可以将播放器设置为根据需要经常从QoSProvider中读取播放和设备统计信息。

此 `QoSProvider` class提供了各种统计信息，包括帧速率、配置文件比特率、缓冲所花费的总时间、缓冲尝试次数、从第一个视频片段获得第一个字节所需的时间、渲染第一个帧所需的时间、当前缓冲的长度以及缓冲时间。

参考实施提供了 `QoSManager` 类可以启用显示QoS覆盖。 您还可以在“设置”用户界面中启用QoS可见性：

![](assets/qos-configuration.jpg)

此 `QoSManager` 通过获取设备信息、连接到媒体播放器并使用最新的QoS信息更新来跟踪QoS统计信息。

**启用或禁用QoS统计信息报告**

1. 使用ManagerFactory创建QosManager或启用QoS报告。

   * 创建QosManager：
      * 此应用程序需要使用广告工作流功能

   QoSManager qosManager =新的QosManagerOn()；

   * 要使用ManagerFactory启用QoS统计信息的显示，请执行以下操作：

   qosManager = ManagerFactory.getQosManager(
   <b>true</b>，配置， mediaPlayer)；

   >[!NOTE]
   >
   >将布尔值更改为 `false` 禁用QoS报告。

2. 添加事件侦听器：

   `qosManager.addEventListener(qosManagerEventListener);`

3. 创建QoS提供程序，并将其附加到播放器活动上下文：

   `qosManager.createQOSProvider(getActivity());`

   >[!NOTE]
   >
   >当播放器活动将被破坏时，请确保调用 [qosManager.destroyQOSProvider](https://help.adobe.com/en_US/primetime/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.html#destroyQOSProvider()) 通过从媒体播放器分离QOS提供程序来清理QOS提供程序。

**相关API文档**

* [类QosManager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.html)
* [QosManagerOn类](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManagerOn.html)
* [QosManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.QosManagerEventListener.html)
* [QosItem](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.QosItem.html)
