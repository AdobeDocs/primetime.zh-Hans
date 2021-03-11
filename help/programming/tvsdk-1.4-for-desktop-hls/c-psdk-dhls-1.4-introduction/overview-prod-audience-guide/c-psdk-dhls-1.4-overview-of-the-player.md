---
description: '桌面HLS的TVSDK包含多种功能，并提供以下主要功能 '
title: Primetime TVSDK功能
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# Primetime TVSDK功能{#primetime-tvsdk-features}

桌面HLS的TVSDK包含多种功能，并提供以下主要功能：

* VOD和实时/线性回放

   * 播放窗口的管理，包括播放、停止、暂停、搜索和检索播放头位置的方法。
   * 隐藏式字幕(608、708、WebVTT)和替代形式的音频以增加可访问性
   * 字幕中的文本样式控制
   * DVR功能、快进/快退（特技播放模式）
   * 实时和VOD内容的特技播放
   * 自适应比特率(ABR)逻辑和ABR控件的初始设置
   * 实时清单故障转移支持
   * 可调节的播放缓冲
   * 302重定向优化
   * 片段持续时间、大小和下载时间跟踪支持

* 广告

   * VPAID 2.0
   * 客户端广告拼接

      * 无缝广告插入，包括对VAST/VMAP的支持
      * 支持广告的自定义提示标签
      * 支持标记、替换和删除C3广告
      * 包括封锁信令的可定制内容/广告插入工作流

* 内容保护

   * 访问与数字版权管理(DRM)相关的服务
   * HLS流播放未加密或使用受保护的HTTP实时流(PHLS)
   * 基于DRM策略的基于分辨率的输出控制
   * 会话Cookie和媒体身份验证Cookie支持
   * 多域令牌打包

* 视频和广告跟踪

   * QoS事件跟踪
   * 帮助TVSDK和您的应用程序异步通信视频、广告和其他元素的状态以及日志活动的通知。
   * 与Adobe Analytics和心率支持集成

* 日志记录

   * 调试日志记录。
   * 片段持续时间、大小和下载时间的跟踪支持。