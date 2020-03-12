---
description: 您可以使用Manager工厂打开或关闭功能，无需遍历代码。
seo-description: 您可以使用Manager工厂打开或关闭功能，无需遍历代码。
seo-title: 使用ManagerFactory打开或关闭功能
title: 使用ManagerFactory打开或关闭功能
uuid: 385c2707-95f7-4628-8d25-67731151cb6a
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# 使用ManagerFactory打开或关闭功能{#turning-features-on-or-off-using-managerfactory}

您可以使用Manager工厂打开或关闭功能，无需遍历代码。

以下示例中的启用参数决定是否使用了该功能。 如果为false，则创建功能管理器，但仅为播放器提供默认功能，就像未创建功能管理器一样。 如果为真，则创建功能管理器，启用该功能，媒体播放器接受来自配置文件的输入。

例如，在文件 `com.adobe.primetime.reference.ui.player.PlayerFragment.java` 中：

```java
adsManager = ManagerFactory.getAdsManager( 
<b>true</b>, config, mediaPlayer);
```

**API文档**:ManagerFactory [](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/ManagerFactory.html)