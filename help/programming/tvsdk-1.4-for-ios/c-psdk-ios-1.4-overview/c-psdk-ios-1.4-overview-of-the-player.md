---
description: 适用于iOS的TVSDK包含各种功能。
title: Primetime TVSDK功能
exl-id: 1968c072-2651-442d-9e4c-412f7959bcab
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# Primetime TVSDK功能 {#primetime-tvsdk-features}

适用于iOS的TVSDK包含各种功能，并提供以下主要功能：

* VOD和实时/线性播放

   * 播放窗口的管理，包括播放、停止、暂停、搜寻和检索播放头位置的方法
   * 支持完整事件重放
   * 隐藏式字幕(608、WebVTT)和音频的替代形式，以提高可访问性
   * DVR功能
   * 自适应比特率(ABR)逻辑和ABR控制的初始设置
   * 订阅非HLS和HLS标签
   * 实时清单故障转移支持

* 广告

   * VPAID 2.0
   * 客户端广告拼接

      * 无缝广告插入，包括对VAST/VMAP的支持
      * 支持广告的自定义提示标记
      * 支持标记、替换和删除C3广告
      * 包括中断信令的可定制内容/广告插入工作流

* 内容保护

   * 访问与数字版权管理(DRM)相关的服务
   * 播放未加密或受保护的HTTP实时流(PHLS)的HLS流
   * 基于DRM策略的基于分辨率的输出控制

* 视频和广告跟踪

   * QoS事件跟踪
   * 帮助TVSDK和您的应用程序异步传递有关视频、广告和其他元素以及日志活动状态的通知
   * 与Adobe Analytics集成并支持心率

* 日志记录

   * 调试日志记录
