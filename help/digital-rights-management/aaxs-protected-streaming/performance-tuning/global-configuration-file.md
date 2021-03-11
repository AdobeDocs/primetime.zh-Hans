---
title: 全局配置文件
description: 全局配置文件
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---


# 全局配置文件{#global-configuration-file}

对性能的影响最大的是使用全局配置文件flashaccess-global.xml中的设置。 这些设置包括`<Caching>`和`<Logging>`元素。

* `<Caching>` 该元 `<Caching>` 素控制内存中配置文件的缓存。`<Caching>`元素的语法如下：

   ```
   <Caching refreshDelaySeconds="..." numTenants="..."/>
   ```

   * `refreshDelaySeconds` 控制服务器检查配置文件更新的频率。`refreshDelaySeconds`的低值会对性能产生负面影响，而较高值会改善性能。 有关`refreshDelaySeconds`的详细信息，请参阅“[更新配置文件](../../aaxs-protected-streaming/updating-configuration-files/updating-configuration-files-overview.md)”。

   * `numTenants` 指定租户的数量。低于租户数量的值可能会影响性能，因为向剩余租户发出的请求会导致缓存丢失。 配置数据的缓存丢失会对性能产生负面影响。 因此，Adobe建议您将此值设置为高于为服务器配置的租户数，除非需要考虑内存限制。

* `<Logging>` 元 `<Logging>` 素指定日志级别和滚动日志文件的频率。`<Logging>`元素的语法如下：

   ```
   <Logging level="..." rollingFrequency=""/>
   ```

   * `level` 指定要记录的消息。值“DEBUG”会生成大量日志消息，并会对性能产生负面影响。 Adobe建议设置“WARN”以获得最佳性能。 但是，这一价值确实有可能丢失基本的运行时信息，如许可证审核。 要保留有价值的日志信息，同时降低性能影响，请使用“INFO”值。
   * `rollingFrequency` 指定滚动日志文件的 *频率*。“滚动”是新日志文件变为活动日志的过程，而以前活动的日志文件不再写入并被视为已滚动的过程。 滚动间隔可设置为“MINUTELY”、“HOURLY”、“TWICE-DAILY”、“DAILY”、“WEEKLY”、“MONTHLY”或“NEVER”。

有关优化性能的其他提示，请参阅&#x200B;*使用Adobe Access SDK for Protecting Content*。
