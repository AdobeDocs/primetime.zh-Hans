---
description: 本主题介绍与性能相关的注意事项。 全局配置文件中名为flashaccess-global.xml的任何设置都会影响性能。
title: 全局配置文件
exl-id: 52d41476-d352-4c02-8af6-25c0fe6bcaa7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# 性能调整 {#performance-tuning}

本主题介绍与性能相关的注意事项。 全局配置文件中名为flashaccess-global.xml的任何设置都会影响性能。

## 全局配置文件 {#global-configuration-file}

配置文件包含以下设置元素：

* `<Caching>` 此 `<Caching>` element控制内存中配置文件的缓存。 此 `<Caching>` 元素支持以下语法：

```
  <Caching refreshDelaySeconds="..." numTenants="..."/>
```

* `refreshDelaySeconds` 控制服务器检查配置文件更新的频率。 的值较低 `refreshDelaySeconds` 会对性能产生负面影响，而较高的值可以改善性能。

   参见 *更新配置文件* 有关的详细信息 `refreshDelaySeconds`.

* `numTenants` 指定租户的数量。 如果值小于租户的数量，则会影响性能，因为请求剩余租户会导致缓存未命中。 任何配置数据的缓存缺失都会对性能产生负面影响。 因此，除非需要考虑内存限制，否则建议将此值设置为高于为服务器配置的租户数量。

* `<Logging>` 此 `<Logging>` element指定日志记录级别和日志文件的滚动频率。 此 `<Logging>` 元素支持以下语法：

   ```
   <Logging level="..." rollingFrequency="..."/>
   ```

* `<level>`  `level` 指定日志消息。 值 `DEBUG` 会生成许多日志消息，这可能会对性能产生负面影响。 建议您应用 `WARN` 以获得最佳性能。 但是，此值可能会导致丢失重要的运行时信息，如许可证审核。 如果要以最小的性能影响保存日志信息，则需要应用值 `INFO`.

* `<rollingFrequency>`  `rollingFrequency` 指定日志文件的频率 *已滚动*. *`Rolling`* 是将任何新日志文件指定为活动日志的进程。 因此，以前活动的日志文件将不再被修改，并将被视为 *`rolled`*. 您可以将滚动间隔设置为 `MINUTELY`， `HOURLY`， `TWICE-DAILY`， `DAILY`， `WEEKLY`， `MONTHLY`，或 `NEVER`.

参见 *使用Adobe Primetime DRM SDK保护内容* 以获取有关如何优化性能的提示。
