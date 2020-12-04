---
seo-title: BEES错误代码
title: BEES错误代码
uuid: 7b2d0dd1-9a43-47e3-b932-a4eaf784ae7a
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---


# BEES错误代码{#bees-error-codes}

<!--<a id="section_81946679E1114DBA9FE173D0AA9E2F09"></a>-->

如果在BEES检查期间出错，则`DRMErrorEvent`将返回给客户端。 您可以分析此事件的属性，以查找有关失败性质的详细信息。 下面列出了可能的错误代码的子集。

| 错误 | 说明 |
|---|---|
| `3304:305` | Primetime Cloud DRM中试图处理身份验证／授权请求的一般授权错误。 通常与BEES问题无关。 如果始终遇到此错误，您应将故障单连同诊断信息一起提交到Primetime Cloud DRM团队。 |
| `3329:0` | 应用程序特定错误（来自BEES Authorizer）。 如果未返回子错误代码，则错误文本将显示问题的详细信息。 例如，解析响应时出现问题，或者BEES服务器不可到达。 |
| `3329:<HTTP error code>` | BEES服务器发出的HTTP响应不是200。 HTTP错误代码将返回到子错误代码字段中的客户端。 这可能表示配置问题或BEES服务器中断。 |
| `3329:<x>` | BEES服务器禁止许可请求。 子错误代码和错误文本由JSON响应的`error`和`errorText`属性中的BEES服务器指定。 此类响应不应被视为错误，而应视为来自BEES服务器的常规拒绝响应。 |