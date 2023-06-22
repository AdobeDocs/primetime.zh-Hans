---
description: Adobe Primetime DRM Server for Protected Streaming应用程序生成的日志文件位于LicenseServer.LogRoot指定的目录中。
title: 日志文件
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# 日志文件{#log-files}

Adobe Primetime DRM Server for Protected Streaming应用程序生成的日志文件位于LicenseServer.LogRoot指定的目录中。

>[!NOTE]
>
>如果在服务器运行时删除或移动了当前日志文件，则可能无法重新创建日志文件。 因此，某些日志信息可能会被删除。

## 日志目录结构 {#section_F490A483D60145ADBC21038914C39203}

日志目录的结构便于使用。 日志目录具有以下结构：

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

全局日志文件， `flashaccess-global.log`，位于 *LicenseServer.LogRoot*. 该日志可以包括Adobe Primetime DRM Java SDK或日志消息可能在服务器初始化期间生成的日志消息。

## 分区日志文件 {#section_5660137CD6AA40519E72A4315534846B}

分区日志文件， `flashaccess-partition.log`，位于 `<LicenseServer.LogRoot>/flashaccesserver` 目录。 其中包括在处理许可证请求期间生成的日志消息。

## 租户日志文件 {#section_F0257CC0831647F18A746B4F02E3E910}

每个租户的租户日志文件， `flashaccess-tenant.log`，位于 `<LicenseServer.LogRoot>/flashaccesserver/tenants/<tenantname>`. 租户日志包含描述为此租户生成的每个许可证的审核信息。
