---
title: 清除内容中的初始部分
description: 清除内容中的初始部分
copied-description: true
exl-id: f291e0f5-ce26-41c4-b468-36b111cb7a1c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# 清除内容中的初始部分{#initial-portion-of-content-in-the-clear}

此可选参数指定从内容开始起将保持未加密状态的时间量（以秒为单位）。

示例用例：当Primetime DRM客户端在后台下载许可证时，这允许更快的播放启动时间。 当在后台进行初始化和许可证获取时，视频的未加密部分立即开始回放。 当此功能关闭时，用户可能会注意到播放体验的延迟，因为客户端计算机在可以播放任何视频之前执行了所有许可步骤。
