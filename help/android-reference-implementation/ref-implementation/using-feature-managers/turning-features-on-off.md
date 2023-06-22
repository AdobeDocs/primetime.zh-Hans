---
description: 您可以使用管理器工厂打开或关闭功能，而无需浏览代码。
title: 使用“管理中心”打开或关闭功能
exl-id: 4e288a6e-80e5-43c1-aba2-374723dd9957
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---

# 使用“管理中心”打开或关闭功能{#turning-features-on-or-off-using-managerfactory}

您可以使用管理器工厂打开或关闭功能，而无需浏览代码。

以下示例中的enablement参数可确定是否使用该功能。 如果为false，则会创建特征管理器，但只为播放器提供默认功能，就像未创建特征管理器一样。 如果为true，则创建功能管理器，启用该功能，并且媒体播放器接受来自配置文件的输入。

例如，在 `com.adobe.primetime.reference.ui.player.PlayerFragment.java` 文件：

```java
adsManager = ManagerFactory.getAdsManager( 
<b>true</b>, config, mediaPlayer);
```

**API文档**： [经理工厂](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/ManagerFactory.html)
