---
product: primetime
audience: end-user
user-guide-title: Primetime 引用实施帮助
user-guide-description: 帮助理解 TVSDK 并修改功能管理器以自定义您的个人播放器。
source-git-commit: 95626ebde981d1996652a67bc9e0cea05f24aa6d
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# 适用于Android的PSDK 1.4参考实施 {#reference-implementation}

+ [Android参考实施概述](home.md)
+ Primetime参考实施 {#reference}
   + [如何使用Primetime参考实施](ref-implementation/how-to-use-ref-player.md)
   + [参考实现结构](ref-implementation/ref-player-structure.md)
   + 如何使用功能管理器 {#feature-managers}
      + [如何使用功能管理器](ref-implementation/using-feature-managers/how-to-use-feature-managers.md)
      + [通过将配置信息传递到MediaPlayer来创建功能管理器……](ref-implementation/using-feature-managers/creating-feature-managers.md)
      + [使用ManagerFactory打开或关闭功能](ref-implementation/using-feature-managers/turning-features-on-off.md)
      + [处理事件](ref-implementation/using-feature-managers/handling-events.md)
   + 设置开发环境 {#setup-dev}
      + [设置开发环境](set-up-dev-environment/set-up-dev-environment-overview.md)
      + [下载并配置先决软件](set-up-dev-environment/download-prereqs-android.md)
      + [构建Primetime参考实施](set-up-dev-environment/install-the-ref-player-project.md)
   + 浏览代码 {#explore-code}
      + [PlayerFragment](set-up-dev-environment/exploring-code/player-fragment.md)
      + [功能管理器](set-up-dev-environment/exploring-code/about-psdk-feature-managers.md)
      + [ConfigProvider](set-up-dev-environment/exploring-code/config-provider.md)
      + [SettingsActivity](set-up-dev-environment/exploring-code/settings-activity.md)
      + [目录格式](set-up-dev-environment/exploring-code/catalog-format.md)
      + [Primetime广告的JSON对象](set-up-dev-environment/exploring-code/json-pt-ads.md)
      + [用于直接广告时间的JSON对象](set-up-dev-environment/exploring-code/json-direct-ad-breaks.md)
      + [自定义广告标记的JSON对象](set-up-dev-environment/exploring-code/json-custom-ad-markers.md)
      + [授权资源ID的JSON对象](set-up-dev-environment/exploring-code/json-entitlement-resource-id.md)
      + [JSON信息源格式示例](set-up-dev-environment/exploring-code/example-json-feed-format.md)
   + 实施视频播放 {#implement-video}
      + [视频播放的基本操作](implement-video-playback/video-playback.md)
      + [启用视频播放](implement-video-playback/enable-video-playback.md)
      + [DRM内容保护](implement-video-playback/content-protection.md)
   + [多比特率](implement-video-playback/mbr.md)
   + 设置播放器以播放包含广告的DVR {#dvr}
      + [不含广告插入的DVR](implement-video-playback/dvr/dvr-without-ad-insertion.md)
      + [带广告插入的DVR](implement-video-playback/dvr/dvr-with-ad-insertion.md)
      + [为DVR选择自定义起点](implement-video-playback/dvr/dvr-custom-start-point.md)
      + [在引用实施中设置自定义开始时间](implement-video-playback/dvr/set-custom-start-time-dvr.md)
   + [显示QoS播放和设备统计信息](implement-video-playback/qos-statistics.md)
   + 插入广告 {#insert-ads}
      + [广告插入](insert-ads/ad-insertion.md)
      + [广告插入类型](insert-ads/ad-insertion-types.md)
      + [添加广告](insert-ads/add-advertising.md)
      + [相关API文档](insert-ads/aps-callbacks-ad-insertion.md)
   + 延迟绑定音频 {#late-binding-audio}
      + [概述](late-binding-audio/late-binding-audio-overview.md)
      + [集成延迟绑定音频](late-binding-audio/aa-enable.md)
      + [选择音轨](late-binding-audio/select-audio-tracks.md)
      + [相关API文档](late-binding-audio/aa-api-callbacks.md)
   + Primetime身份验证授权流 {#primetime-authentications}
      + [概述](paytvpass-entitlement/paytvpass-entitlement-overview.md)
      + [授权管理器概述](paytvpass-entitlement/entitlement-overvivew.md)
      + [集成Primetime身份验证](paytvpass-entitlement/integrate-pass.md)
      + [配置Adobe Analytics报表](paytvpass-entitlement/pass-analytics-setup.md)
      + [相关API文档](paytvpass-entitlement/pass-apis-callbacks.md)
   + Video Analytics {#video-analytics}
      + [Video Analytics](video-analytics/video-analytics-overview.md)
      + [创建视频分析管理器](video-analytics/create-video-analytics-manager.md)
      + [配置Video Analytics](video-analytics/configure-video-analytics-manager.md)
      + [相关API文档](video-analytics/va-apis-callbacks.md)
   + [构建自定义用户界面](build-custom-ui.md)
   + [疑难解答](troubleshooting.md)
