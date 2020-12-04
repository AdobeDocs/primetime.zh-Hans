---
description: 适用于Android 2.5的TVSDK包含可在播放器中实现的各种功能。
seo-description: 适用于Android 2.5的TVSDK包含可在播放器中实现的各种功能。
seo-title: Primetime TVSDK功能
title: Primetime TVSDK功能
uuid: 20ef9abf-1a33-4afc-bb2e-4910e3398a7a
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---


# Primetime TVSDK功能{#primetime-tvsdk-features}

适用于Android 2.7的TVSDK包含可在播放器中实现的各种功能。

TVSDK功能：

* **VOD和实时／线性播放**

   * 播放窗口的管理，包括播放、停止、暂停、搜索和检索播放头位置的方法
   * 支持全事件重播
   * 隐藏式字幕(608、708、WebVTT)和替代形式的音频以增强辅助功能
   * 字幕中的文本样式控件
   * DVR功能、快进和快退（后两者称为&#x200B;*技巧播放模式*）
   * 自适应比特率(ABR)逻辑和ABR控件的初始设置
   * 实时清单故障转移支持
   * 可调整的播放缓冲器
   * 片段持续时间、大小和下载时间跟踪支持

* **广告**

   * VPAID 2.0
   * 客户端广告拼接

      * 无缝广告插入，包括对VAST/VMAP的支持
      * 支持广告的自定义提示标签
      * 支持标记、替换和删除C3广告
      * 包括封锁信号的可自定义内容／广告插入工作流

* **内容保护**

   * 访问数字版权管理(DRM)相关服务
   * HLS流播放未加密或使用受保护的HTTP实时流(PHLS)
   * 基于DRM策略的基于分辨率的输出控制

* **视频和广告跟踪**

   * QoS事件跟踪
   * 帮助TVSDK和您的应用程序异步通信视频、广告和其他元素状态的通知。 通知还会记录活动。

* **记录**

   * 调试日志记录
   * 片段持续时间、大小和下载时间的跟踪支持。