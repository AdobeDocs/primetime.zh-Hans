---
description: TVSDK功能由配置驱动，并通过MediaPlayer实现。
seo-description: TVSDK功能由配置驱动，并通过MediaPlayer实现。
seo-title: 通过将配置信息传递到MediaPlayer来创建功能管理器
title: 通过将配置信息传递到MediaPlayer来创建功能管理器
uuid: 106ececd-a670-4360-b000-a31fec65233c
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---


# 通过将配置信息传递到MediaPlayer {#creating-feature-managers-by-passing-configuration-information-to-the-mediaplayer}创建功能管理器

TVSDK功能由配置驱动，并通过MediaPlayer实现。

* 配置是该功能的特定设置的列表，如ABR控件的初始比特率和默认的隐藏式字幕可见性。

   功能管理器需要获得配置才能确定功能行为。

   在Primetime参考实施中，配置存储在共享首选项中，但您可以以任何对环境有意义的方式存储配置。

* `MediaPlayer` 是包含视频资源的TVSDK媒体播放器对象。

   功能管理器将TVSDK事件监听器注册到此播放器对象，从播放会话检索数据并将TVSDK功能触发到播放会话。

每个功能都具有相应的配置界面。 例如，`CCManager`使用`ICCConfig`检索配置。 `ICCConfig` 包含仅获取与隐藏式字幕相关的配置信息的方法。

以下示例显示了[!DNL ICCConfig.java]文件，该文件配置为从`MediaPlayer`接收有关隐藏式字幕可见性、字体样式和字体边缘的信息：

```java
// Constructor of CCManager 
 
<b>public CCManager(ICCConfig ccConfig, MediaPlayer mediaPlayer) {...}</b> 
  
// ICCConfig methods 
 
<b>public interface ICCConfig {</b> 
  
    /** 
     * Get the closed captioning visibility config 
     * 
     * @return true if visibility is set to true, false otherwise 
     */ 
    
<b> public boolean getCCVisibility();</b> 
  
    /** 
     * Get the closed captioning font style 
     * 
     * @return TextFormat.Font object represents font style 
     */ 
     
<b>public TextFormat.Font getCCFont();</b>

    /** 
     * Get the closed captioning font edge 
     * 
     * @return TextFormat.FontEdge represents of font edge 
     */ 
     
<b>public TextFormat.FontEdge getCCFontEdge();</b> 
... 
}
```

使用TVSDK功能的应用程序可以创建其功能管理器，其中包含配置提供程序和`MediaPlayer`对象。 例如：

```java
// This application needs to use the advertising workflow feature 
AdsManager adsManager = new AdsManagerOn();
```

功能管理器配置API文档：[Javadoc](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/package-summary.html)