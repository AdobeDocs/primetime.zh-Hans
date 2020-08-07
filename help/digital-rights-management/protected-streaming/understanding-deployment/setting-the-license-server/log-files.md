---
description: 由Adobe PrimetimeDRM服务器为受保护流应用程序生成的日志文件位于LicenseServer.LogRoot指定的目录中。
seo-description: 由Adobe PrimetimeDRM服务器为受保护流应用程序生成的日志文件位于LicenseServer.LogRoot指定的目录中。
seo-title: 日志文件
title: 日志文件
uuid: 4498fe60-65af-4f99-8f9b-e85013d0c9e9
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 0%

---


# 日志文件{#log-files}

由Adobe PrimetimeDRM服务器为受保护流应用程序生成的日志文件位于LicenseServer.LogRoot指定的目录中。

>[!NOTE]
>
>如果当前日志文件在服务器运行时被删除或移动，则不能重新创建日志文件。 因此，某些日志信息可能会被删除。

## 日志目录结构 {#section_F490A483D60145ADBC21038914C39203}

日志目录的结构化便于使用。 日志目录具有以下结构：

```
<i class="+ topic ph hi-d="" i "="">
 LicenseServer.LogRoot/ 
 flashaccess-global.log 
     flashaccessserver/ 
         flashaccess-partition.log 
         tenants/ 
             
 <i class="+ topic ph hi-d="" i "="">
  tenantname/ 
                  flashaccess-tenant.log
 </i class="+ topic>
</i class="+ topic>
```

## 全局日志文件 {#section_1CFA90748142439C9F3BE380969539DA}

全局日志文件 [!DNL flashaccess-global.log]位于LicenseServer. *LogRoot中*。 日志可能包括在服务器初始化期间Adobe PrimetimeDRM Java SDK或日志消息可能生成的日志消息。

## 分区日志文件 {#section_5660137CD6AA40519E72A4315534846B}

分区日志文 [!DNL flashaccess-partition.log]件位于目录 [!DNL <LicenseServer.LogRoot>/flashaccesserver] 中。 它包括在处理许可证请求期间生成的日志消息。

## 租户日志文件 {#section_F0257CC0831647F18A746B4F02E3E910}

每个租户的租户日志 [!DNL flashaccess-tenant.log]文件位 [!DNL 于&lt;LicenseServer.LogRoot>/flashaccesserver/armoes/<tenantname>]. 租户日志包含审计信息，用于描述为此租户生成的每个许可证。
