---
seo-title: 全局配置文件
title: 全局配置文件
uuid: 48c45f56-55c2-4526-b854-5552caf21541
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 全局配置文件{#global-configuration-file}

对性能的影响最大的是使用全局配置文件flashaccess-global.xml中的设置。 这些设置包括 `<Caching>` 和元 `<Logging>` 素。

* `<Caching>` 该元 `<Caching>` 件控制内存中配置文件的缓存。 元素 `<Caching>` 的语法如下：

   ```
   <Caching refreshDelaySeconds="..." numTenants="..."/>
   ```

   * `refreshDelaySeconds` 控制服务器检查配置文件更新的频率。 较低的值会对性 `refreshDelaySeconds` 能产生负面影响，而较高的值则会提高性能。 有关的详细信息， `refreshDelaySeconds`请参阅“更[新配置文件](../../aaxs-protected-streaming/updating-configuration-files/updating-configuration-files-overview.md)”。

   * `numTenants` 指定租户数量。 低于租户数量的值可能会影响性能，因为向剩余租户发出的请求会导致缓存丢失。 配置数据的缓存缺失会对性能产生负面影响。 因此，Adobe建议您将此值设置为高于为服务器配置的租户数量，除非需要考虑内存限制。

* `<Logging>` 元 `<Logging>` 素指定日志记录级别和滚动日志文件的频率。 元素 `<Logging>` 的语法如下：

   ```
   <Logging level="..." rollingFrequency=""/>
   ```

   * `level` 指定要记录的消息。 “DEBUG”值会生成大量日志消息，并会对性能产生负面影响。 Adobe建议设置“WARN”以获得最佳性能。 但是，该价值确实有可能丢失基本的运行时信息，如许可证审核。 要保留有价值的日志信息，并尽可能降低对性能的影响，请使用“INFO”值。
   * `rollingFrequency` 指定滚动日志文件的 *频率*。 “滚动”是新日志文件成为活动日志的过程，而以前活动的日志文件不再写入并被视为滚动。 滚动间隔可设置为“MINUTELY”、“HOURLY”、“TWICE-DAILY”、“DAILY”、“WEEKLY”、“MONTHLY”或“NEVER”。

有关 *优化性能的其他提示，请参阅使用Adobe Access SDK for Protecting Content* 。
