---
description: 您可以使用管理器工厂打开或关闭功能，而无需浏览代码。
title: 使用ManagerFactory打开或关闭功能
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---

# 使用ManagerFactory打开或关闭功能{#turning-features-on-or-off-using-managerfactory}

您可以使用管理器工厂打开或关闭功能，而无需浏览代码。

以下示例中的enablement参数可确定是否使用该功能。 如果为false，则创建特征管理器，但只为播放器提供默认功能，就像未创建特征管理器一样。 如果为true，则创建功能管理器，启用该功能，并且媒体播放器接受来自配置文件的输入。

例如，在 `com.adobe.primetime.reference.ui.player.PlayerFragment.java` 文件：

```java
adsManager = ManagerFactory.getAdsManager( 
<b>true</b>, config, mediaPlayer);
```

**API文档**： [经理工厂](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/ManagerFactory.html)
