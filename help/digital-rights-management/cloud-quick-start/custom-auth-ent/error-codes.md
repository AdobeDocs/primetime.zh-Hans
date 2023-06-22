---
title: BEES错误代码
description: BEES错误代码
copied-description: true
exl-id: 36c83ee9-7e28-442e-8076-691a1bd43a01
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# BEES错误代码 {#bees-error-codes}

<!--<a id="section_81946679E1114DBA9FE173D0AA9E2F09"></a>-->

如果在BEES检查过程中出现错误， `DRMErrorEvent` 将被返回到客户端。 您可以解析此事件的属性以查找有关故障性质的详细信息。 下面列出了可能错误代码的子集。

| 错误 | 描述 |
|---|---|
| `3304:305` | Primetime Cloud DRM尝试处理身份验证/授权请求时出现一般授权错误。 通常与BEES问题无关。 如果始终遇到此错误，则应将故障票证与诊断信息一起提交给Primetime Cloud DRM团队。 |
| `3329:0` | 应用程序特定错误（来自BEES授权程序）。 如果未返回子错误代码，则错误文本将显示问题的详细信息。 例如，解析响应时出现问题，或者BEES服务器无法访问。 |
| `3329:<HTTP error code>` | BEES服务器发出了200以外的HTTP响应。 在子错误代码字段中将HTTP错误代码返回到客户端。 这可能表示存在配置问题或BEES服务器中断。 |
| `3329:<x>` | BEES服务器不允许许可证请求。 BEES服务器在JSON响应的 `error` 和 `errorText` 属性。 此类响应不应被视为错误，而应被视为来自BEES服务器的常规拒绝响应。 |
