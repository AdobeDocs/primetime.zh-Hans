---
title: 播放窗口
description: 播放窗口
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---


# 播放窗口{#playback-window}

播放窗口指定许可证在首次用于播放受保护内容之后有效的持续时间。

示例用例：某些业务模型允许租用30天，但是，一旦开始播放，播放必须在48小时内完成。 在这种情况下，48小时的许可证持续时间是播放窗口。

**从5.3前进**  — 播放窗口还支持启用或禁用硬停止的选项，此选项指示播放的解密上下文应在播放窗口过期时停止（已启用），还是在过期时继续（已禁用）。

>[!NOTE]
>
>如果与“播放窗口”一起使用，则硬停止选项无法与“播放窗口”一起正常工作（播放窗口将不适用）。 在不安全停止的情况下使用“播放”窗口播放内容时会遵守播放窗口限制。

