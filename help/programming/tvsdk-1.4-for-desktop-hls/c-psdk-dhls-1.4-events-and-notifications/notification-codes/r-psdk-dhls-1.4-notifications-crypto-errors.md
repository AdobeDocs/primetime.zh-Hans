---
description: Adobe视频引擎的加密模块在NATIVE_ERROR元数据对象中返回这些通知。
title: NATIVE_ERROR加密值
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
| 303 | `CRYPTO_ERROR_BAD_CERTIFICATE` | 证书错误。 |
| 304 | `CRYPTO_ERROR_DIGEST_UPDATE` | 摘要更新。 |
| 305 | `CRYPTO_ERROR_DIGEST_FINISH` | 摘要完成。 |
| 306 | `CRYPTO_ERROR_BAD_PARAMETER` | 参数错误。 |
