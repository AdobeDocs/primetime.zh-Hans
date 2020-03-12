---
seo-title: BEES错误代码
title: BEES错误代码
uuid: 7b2d0dd1-9a43-47e3-b932-a4eaf784ae7a
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5

---


# BEES错误代码 {#bees-error-codes}

<!--<a id="section_81946679E1114DBA9FE173D0AA9E2F09"></a>-->

如果在BEES检查过程中出错， `DRMErrorEvent` 将向客户端返回。 您可以解析此事件的属性，以查找有关失败性质的详细信息。 下面列出了可能的错误代码子集。

| 错误 | 说明 |
|---|---|
| `3304:305` | Primetime Cloud DRM中试图处理身份验证／授权请求的常规授权错误。 通常不与BEES问题关联。 如果一贯遇到此错误，您应将故障单连同诊断信息一起提交到Primetime Cloud DRM团队。 |
| `3329:0` | 应用程序特定错误（来自BEES Authorizer）。 如果未返回子错误代码，则错误文本将显示问题的详细信息。 例如，解析响应时出现问题，或BEES服务器无法访问。 |
| `3329:<HTTP error code>` | BEES服务器发出的HTTP响应不是200。 HTTP错误代码将返回到子错误代码字段中的客户端。 这可能表示配置问题或BEES服务器中断。 |
| `3329:<x>` | BEES服务器不允许许可请求。 子错误代码和错误文本由BEES服务器在JSON响应的和属性中指 `error` 定 `errorText` 。 此类响应不应视为错误，而应视为来自BEES服务器的常规拒绝响应。 |