---
description: 本主题介绍与性能相关的注意事项。 全局配置文件中名为flashaccess-global.xml的任何设置都会影响性能。
seo-description: 本主题介绍与性能相关的注意事项。 全局配置文件中名为flashaccess-global.xml的任何设置都会影响性能。
seo-title: 全局配置文件
title: 全局配置文件
uuid: 254925b5-d441-4a35-ad6f-f99db5de7591
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# 性能调整 {#performance-tuning}

本主题介绍与性能相关的注意事项。 全局配置文件中名为flashaccess-global.xml的任何设置都会影响性能。

## 全局配置文件 {#global-configuration-file}

配置文件包括以下设置元素：

* `<Caching>` 该元 `<Caching>` 件控制内存中配置文件的缓存。 元 `<Caching>` 素支持以下语法：

```
  <Caching refreshDelaySeconds="..." numTenants="..."/>
```

* `refreshDelaySeconds` 控制服务器检查配置文件更新的频率。 较低的值会对性 `refreshDelaySeconds` 能产生负面影响，而较高的值则会提高性能。

   有关 *的详细信息* ，请参阅更新配置文件 `refreshDelaySeconds`。

* `numTenants` 指定租户数量。 低于租户数量的值会影响性能，因为向剩余租户发出的请求会导致缓存丢失。 任何配置数据的缓存缺失都会对性能产生负面影响。 因此，建议您将此值设置为高于为服务器配置的租户数量，除非您需要考虑内存限制。

* `<Logging>` 元 `<Logging>` 素指定日志记录级别和滚动日志文件的频率。 元 `<Logging>` 素支持以下语法：

   ```
   <Logging level="..." rollingFrequency="..."/>
   ```

* `<level>`  指定 `level` 日志消息。 如果值为，则 `DEBUG` 会生成许多日志消息，这可能会对性能产生负面影响。 建议您应用一个设置以获得 `WARN` 最佳性能。 但是，此值可能导致丢失基本的运行时信息，如许可证审核。 如果要保存日志信息并且对性能的影响最小，则需要应用值 `INFO`。

* `<rollingFrequency>`  指 `rollingFrequency` 定滚动日志文件的 *频率*。 *`Rolling`* 是将任何新日志文件指定为活动日志的进程。 因此，不再能够修改以前处于活动状态的日志文件，并将其视为该日志文件 *`rolled`*。 您可以将滚动间隔设 `MINUTELY`置为、 `HOURLY`、 `TWICE-DAILY`、 `DAILY`、 `WEEKLY`、 `MONTHLY`或 `NEVER`。

有关 *如何优化性能的提示，请参阅使用Adobe Primetime DRM SDK保护内容* 。