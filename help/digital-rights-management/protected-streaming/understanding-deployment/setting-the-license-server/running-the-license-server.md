---
title: 运行用于受保护流的DRM服务器
description: 运行用于受保护流的DRM服务器
copied-description: true
exl-id: 05dc4c55-a97e-4bdc-aea8-32741299454c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 0%

---

# 运行用于受保护流的DRM服务器 {#running-the-drm-server-for-protected-streaming}

在启动Adobe Primetime DRM Server for Protected Streaming之前，建议您验证配置文件中的设置的有效性。

您可以使用许可证服务器随附的实用程序来验证设置的有效性。 (请参阅 *配置验证器* 本指南内容。

如果要启动Tomcat和许可证服务器，则需要运行 [!DNL catalina.bat start] 或 [!DNL catalina.sh start] 来自Tomcat [!DNL bin] 目录。

服务器启动后，您需要通过打开 `https://<lic<span></span>ense-server-host:port>/flashaccessserver/<tenant-name>/flashaccess/license/v1` 在浏览器窗口中。 如果已成功加载租户配置，则会显示一条确认消息。

## 日志文件 {#log-files}

Adobe Primetime DRM Server for Protected Streaming应用程序生成的日志文件位于LicenseServer.LogRoot指定的目录中。

>[!NOTE]
>
>如果在服务器运行时删除或移动了当前日志文件，则可能无法重新创建日志文件。 因此，某些日志信息可能会被删除。

### 日志目录结构 {#section_F490A483D60145ADBC21038914C39203}

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

### 全局日志文件 {#section_1CFA90748142439C9F3BE380969539DA}

全局日志文件， [!DNL flashaccess-global.log]，位于 *LicenseServer.LogRoot*. 该日志可以包括Adobe Primetime DRM Java SDK或日志消息可能在服务器初始化期间生成的日志消息。

### 分区日志文件 {#section_5660137CD6AA40519E72A4315534846B}

分区日志文件， [!DNL flashaccess-partition.log]，位于 `<LicenseServer.LogRoot>/flashaccesserver` 目录。 其中包括在处理许可证请求期间生成的日志消息。

### 租户日志文件 {#section_F0257CC0831647F18A746B4F02E3E910}

每个租户的租户日志文件， [!DNL flashaccess-tenant.log]，位于 `<LicenseServer.LogRoot>/flashaccesserver/tenants/<tenantname>`. 租户日志包含描述为此租户生成的每个许可证的审核信息。

## 更新配置文件 {#updating-configuration-files}

一旦许可证服务器读取一个许可证服务器配置文件（全局或租户配置），配置信息就缓存在内存中。 因此，不必为每个许可证请求从磁盘读取文件。 但是，服务器还允许修改配置文件中的大多数值，而无需重新启动服务器以使更改生效。

无论何时修改配置文件，许可证服务器都会存储上次修改文件的时间。 服务器以可配置的间隔检查文件修改时间是否已更改。 如果更改，服务器将自动重新加载配置文件的内容。

如果要控制服务器检查更新的频率，您需要设置 `refreshDelaySeconds` 中的属性 `Caching` 全局配置文件中的元素。 例如，如果 `refreshDelaySeconds` 设置为3600秒，则服务器将在自配置文件的修改时间起最多一小时内更新配置。 如果 `refreshDelaySeconds` 设置为0，则服务器会在每次请求时检查配置更新。 建议不要设置 `refreshDelaySeconds` 在任何生产环境中降低值，因为这样做会影响性能。

此 `Caching` element还可控制一次缓存多少租户的配置。 您可以将此值设置为小于租户总数的数字，以限制用于缓存配置信息的内存量。 如果收到针对不在缓存中的租户的请求，则在处理该请求之前会加载配置。 如果缓存已满，则从缓存中删除最近最少使用的租户。

缓存版本的配置继续在以下情况下使用（直到下次服务器检查更新时为止）：

* 如果将更改保存到配置文件或中引用的任何证书文件 [!DNL flashaccess-tenant.xml] 文件，而服务器尝试读取文件
* 如果发现文件的时间戳早于当前时间的一秒
* 如果文件的时间戳为未来

如果没有缓存版本，则配置加载失败，并向客户端返回错误。 然后，服务器在下次收到对该租户的请求时尝试再次加载文件。

### 更新全局配置文件 {#section_AA546C72442646CFB8906AEEBDF50587}

您可在以下位置修改HSM密码 [!DNL flashaccess-global.xml] 随时。 这些更改将在下次服务器重新加载配置文件时生效。 但是，不会重新加载对“日志记录”和“缓存”元素的更改。 对这些元素所做的任何更改生效之前，需要重新启动服务器。

### 更新租户配置文件 {#section_71624DB8DF28480F84F34F0FF7FD4365}

您可以修改 [!DNL flashaccess-tenant.xml] 任何时候的档案。 这些更改将在下次服务器重新加载配置文件时生效。 此外，服务器还会检查所有凭据( [!DNL .pfx])在租户配置文件中引用的文件和Packager允许列表证书文件。
