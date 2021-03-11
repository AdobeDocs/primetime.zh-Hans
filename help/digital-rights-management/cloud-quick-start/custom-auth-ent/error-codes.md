---
title: BEES错误代码
description: BEES错误代码
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---


# BEES错误代码{#bees-error-codes}

<!--<a id="section_81946679E1114DBA9FE173D0AA9E2F09"></a>-->

如果在BEES检查期间出错，将向客户端返回`DRMErrorEvent`。 您可以分析此事件的属性，以查找有关失败性质的详细信息。 以下列出了可能的错误代码的子集。

| 错误 | 说明 |
|---|---|
| `3304:305` | 尝试处理身份验证/授权请求的Primetime Cloud DRM中的常规授权错误。 通常与BEES问题无关。 如果遇到此错误，您应将故障单连同诊断信息一起提交到Primetime Cloud DRM团队。 |
| `3329:0` | 应用程序特定错误（来自BEES授权程序）。 如果未返回子错误代码，则错误文本将显示问题的详细信息。 例如，分析响应时出现问题，或者BEES服务器不可到达。 |
| `3329:<HTTP error code>` | BEES服务器发出的HTTP响应不是200。 HTTP错误代码将返回到子错误代码字段中的客户端。 这可能表示配置问题或BEES服务器中断。 |
| `3329:<x>` | BEES服务器不允许许可证请求。 子错误代码和错误文本由JSON响应的`error`和`errorText`属性中的BEES服务器指定。 此类响应不应被视为错误，而应视为来自BEES服务器的定期拒绝响应。 |