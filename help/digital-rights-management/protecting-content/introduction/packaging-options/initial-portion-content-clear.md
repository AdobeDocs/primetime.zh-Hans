---
title: 清除内容中的初始部分
description: 清除内容中的初始部分
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# 清除内容中的初始部分{#initial-portion-of-content-in-the-clear}

此可选参数指定从内容开始保持未加密状态所经过的时间（以秒为单位）。

示例用例：当Primetime DRM客户端在后台下载许可证时，这样可加快播放启动时间。 当在后台进行初始化和许可证获取时，视频的未加密部分立即开始回放。 当此功能关闭时，用户可能会注意到播放体验的延迟，因为客户端计算机在视频播放之前执行了所有许可步骤。
