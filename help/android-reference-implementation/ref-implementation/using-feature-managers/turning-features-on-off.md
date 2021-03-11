---
description: 您可以使用管理器工厂打开或关闭功能，而无需遍历代码。
title: 使用ManagerFactory打开或关闭功能
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---


# 使用ManagerFactory{#turning-features-on-or-off-using-managerfactory}打开或关闭功能

您可以使用管理器工厂打开或关闭功能，而无需遍历代码。

以下示例中的enablement参数决定是否使用了该功能。 如果为false，则创建功能管理器，但仅为播放器提供默认功能，就像未创建功能管理器一样。 如果为true，则创建功能管理器，启用该功能，媒体播放器接受来自配置文件的输入。

例如，在`com.adobe.primetime.reference.ui.player.PlayerFragment.java`文件中：

```java
adsManager = ManagerFactory.getAdsManager( 
<b>true</b>, config, mediaPlayer);
```

**API文档**: [ManagerFactory](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/ManagerFactory.html)