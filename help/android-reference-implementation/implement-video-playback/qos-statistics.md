---
description: 您可以设置播放器，以根据需要从QoSProvider中读取播放和设备统计信息。
seo-description: 您可以设置播放器，以根据需要从QoSProvider中读取播放和设备统计信息。
seo-title: 显示QoS回放和设备统计
title: 显示QoS回放和设备统计
uuid: 8fc45a2f-03d4-4fa0-979b-eb816419c4f7
translation-type: tm+mt
source-git-commit: e1c6ab1d50f9262aaf70aef34854cf293fb4f30d
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---


# 显示QoS播放和设备统计信息{#display-qos-playback-and-device-statistics}

您可以设置播放器，以根据需要从QoSProvider中读取播放和设备统计信息。

`QoSProvider`类提供各种统计信息，包括帧速率、用户档案比特率、缓冲所用的总时间、缓冲尝试次数、从第一个视频片段获取第一个字节所花的时间、呈现第一个帧所花的时间、当前缓冲的长度和缓冲时间。

引用实现提供一个`QoSManager`类，在该类中可以启用QoS叠加的显示。 您还可以在设置用户界面中启用QoS可见性：

![](assets/qos-configuration.jpg)

`QoSManager`通过获取设备信息、连接到媒体播放器并使用最新的QoS信息进行更新来跟踪QoS统计。

**启用或禁用QoS统计报告**

1. 创建QosManager或使用ManagerFactory启用QoS报告。

   * 创建QosManager:
      * 此应用程序需要使用广告工作流程功能

   QoSManager qosManager =新的QosManagerOn();

   * 要使用ManagerFactory来显示QoS统计信息，请执行以下操作：

   qosManager = ManagerFactory.getQosManager(
   <b>true</b>、config、mediaPlayer);

   >[!NOTE]
   >
   >将布尔值更改为`false`将禁用QoS报告。

2. 添加事件监听器：

   `qosManager.addEventListener(qosManagerEventListener);`

3. 创建QoS提供者并将其连接到播放器活动上下文：

   `qosManager.createQOSProvider(getActivity());`

   >[!NOTE]
   >
   >当播放器活动将被破坏时，请确保通过从媒体播放器中分离来调用[qosManager.destroyQOSProvider](https://help.adobe.com/en_US/primetime/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.html#destroyQOSProvider())来清理QOS提供器。

**相关API文档**

* [类QosManager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.html)
* [类QosManagerOn](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManagerOn.html)
* [QosManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.QosManagerEventListener.html)
* [QosItem](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.QosItem.html)
