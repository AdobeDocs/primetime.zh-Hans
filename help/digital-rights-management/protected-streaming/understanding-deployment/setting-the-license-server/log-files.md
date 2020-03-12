---
description: Adobe Primetime DRM Server为受保护的流应用程序生成的日志文件位于LicenseServer.LogRoot指定的目录中。
seo-description: Adobe Primetime DRM Server为受保护的流应用程序生成的日志文件位于LicenseServer.LogRoot指定的目录中。
seo-title: 日志文件
title: 日志文件
uuid: 4498fe60-65af-4f99-8f9b-e85013d0c9e9
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 日志文件{#log-files}

Adobe Primetime DRM Server为受保护的流应用程序生成的日志文件位于LicenseServer.LogRoot指定的目录中。

>[!NOTE] {class=&quot;- topic/note &quot;}
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

全局日志文件 [!DNL flashaccess-global.log]位于 *LicenseServer.LogRoot中*。 日志可能包括Adobe Primetime DRM Java SDK或日志消息在服务器初始化期间可能生成的日志消息。

## 分区日志文件 {#section_5660137CD6AA40519E72A4315534846B}

分区日志文 [!DNL flashaccess-partition.log]件位于目录 [!DNL <LicenseServer.LogRoot>/flashaccesserver] 中。 它包括在处理许可证请求期间生成的日志消息。

## 租户日志文件 {#section_F0257CC0831647F18A746B4F02E3E910}

每个租户的租户日志 [!DNL flashaccess-tenant.log]文件位于 [!DNL &lt;LicenseServer.LogRoot>/flashaccesserver/arkes/<tenantname>]. 租户日志包含审计信息，用于描述为此租户生成的每个许可证。
