---
description: 本主题介绍与性能相关的注意事项。 全局配置文件中名为flashaccess-global.xml的任何设置都会影响性能。
seo-description: 本主题介绍与性能相关的注意事项。 全局配置文件中名为flashaccess-global.xml的任何设置都会影响性能。
seo-title: 全局配置文件
title: 全局配置文件
uuid: 254925b5-d441-4a35-ad6f-f99db5de7591
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---


# 性能调整{#performance-tuning}

本主题介绍与性能相关的注意事项。 全局配置文件中名为flashaccess-global.xml的任何设置都会影响性能。

## 全局配置文件{#global-configuration-file}

配置文件包含以下设置元素：

* `<Caching>` 元 `<Caching>` 素控制内存中配置文件的缓存。`<Caching>`元素支持以下语法：

```
  <Caching refreshDelaySeconds="..." numTenants="..."/>
```

* `refreshDelaySeconds` 控制服务器检查配置文件更新的频率。`refreshDelaySeconds`的低值会对性能产生负面影响，而较高的值会提高性能。

   有关`refreshDelaySeconds`的详细信息，请参阅&#x200B;*更新配置文件*。

* `numTenants` 指定租户数量。低于租户数量的值会影响性能，因为对剩余租户的请求会导致缓存丢失。 任何配置数据的缓存缺失都会对性能产生负面影响。 因此，建议您将此值设置为高于为服务器配置的租户数量，除非您需要考虑内存限制。

* `<Logging>` 元 `<Logging>` 素指定日志记录级别和记录日志文件的频率。`<Logging>`元素支持以下语法：

   ```
   <Logging level="..." rollingFrequency="..."/>
   ```

* `<level>`  `level` 指定日志中的消息。值`DEBUG`会生成许多日志消息，这可能对性能产生负面影响。 建议应用`WARN`设置以获得最佳性能。 但是，此值可能导致丢失基本的运行时信息，如许可证审核。 如果要保存对性能影响最小的日志信息，则需要应用值`INFO`。

* `<rollingFrequency>`  `rollingFrequency` 指定滚动日志文件的 *频率*。*`Rolling`* 是将任何新日志文件指定为活动日志的进程。因此，以前活动的日志文件不再被修改，因此被视为&#x200B;*`rolled`*。 可以将滚动间隔设置为`MINUTELY`、`HOURLY`、`TWICE-DAILY`、`DAILY`、`WEEKLY`、`MONTHLY`或`NEVER`。

有关如何优化性能的提示，请参见&#x200B;*使用Adobe PrimetimeDRM SDK保护内容*。