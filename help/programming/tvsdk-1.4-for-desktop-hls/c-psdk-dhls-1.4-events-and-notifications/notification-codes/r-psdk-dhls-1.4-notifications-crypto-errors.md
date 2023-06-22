---
description: Adobe视频引擎的加密模块在NATIVE_ERROR元数据对象中返回这些通知。
title: NATIVE_ERROR加密值
exl-id: c14b35c1-ed91-4a44-b826-fd6a05dbe345
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 8%

---

# NATIVE_ERROR：加密值{#native-error-crypto-values}

Adobe视频引擎的加密模块在NATIVE_ERROR元数据对象中返回这些通知。

| RUNTIME_CODE元数据键的值 | RUNTIME_CODE_MESSAGE元数据键的值 | 含义 |
|---|---|---|
| 300 | `CRYPTO_ALGORITHM_NOT_SUPPORTED` | 不支持正在使用的算法。 |
| 301 | `CRYPTO_ERROR_CORRUPTED_DATA` | 数据已损坏。 |
| 302 | `CRYPTO_ERROR_BUFFER_TOO_SMALL` | 缓冲区太小。 |
| 303 | `CRYPTO_ERROR_BAD_CERTIFICATE` | 证书无效。 |
| 304 | `CRYPTO_ERROR_DIGEST_UPDATE` | 摘要更新。 |
| 305 | `CRYPTO_ERROR_DIGEST_FINISH` | 摘要结束。 |
| 306 | `CRYPTO_ERROR_BAD_PARAMETER` | 参数错误。 |
