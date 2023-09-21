---
title: 全局配置文件
description: 全局配置文件
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---

# 全局配置文件{#global-configuration-file}

对性能影响最大的是使用全局配置文件flashaccess-global.xml中的设置。 这些设置包括 `<Caching>` 和 `<Logging>` 元素。

* `<Caching>` 此 `<Caching>` element控制内存中配置文件的缓存。 此 `<Caching>` 元素的语法如下：

  ```
  <Caching refreshDelaySeconds="..." numTenants="..."/>
  ```

   * `refreshDelaySeconds` 控制服务器检查配置文件更新的频率。 的值过低 `refreshDelaySeconds` 会对性能产生负面影响，而较高的值可以改善性能。 有关的详细信息 `refreshDelaySeconds`，请参见&quot;[正在更新配置文件](../../aaxs-protected-streaming/updating-configuration-files/updating-configuration-files-overview.md)“。

   * `numTenants` 指定租户的数量。 如果值小于租户的数量，则可能会影响性能，因为对剩余租户的请求会导致缓存未命中。 配置数据的缓存缺失会对性能产生负面影响。 因此，Adobe建议将此值设置为大于为服务器配置的租户数量，除非考虑内存限制。

* `<Logging>` 此 `<Logging>` 元素指定日志记录级别和日志文件的滚动频率。 此 `<Logging>` 元素的语法如下：

  ```
  <Logging level="..." rollingFrequency=""/>
  ```

   * `level` 指定要记录的消息。 值“DEBUG”会生成大量日志消息，并且可能对性能产生负面影响。 Adobe建议将设置为“警告”以获得最佳性能。 但是，该价值确实存在丢失许可证审核等重要的运行时信息的风险。 要保留有价值的日志信息并对性能影响最小，请使用值“INFO”。
   * `rollingFrequency` 指定日志文件的频率 *已滚动*. 滚动是一个过程，在该过程中，新日志文件成为活动日志，而之前活动的日志文件不再写入，并且被视为滚动。 滚动间隔可以设置为“详细”、“每小时”、“每日两次”、“每日”、“每周”、“每月”或“从不”。

请参阅 *使用Adobe访问SDK保护内容* 以获取有关优化性能的其他提示。
