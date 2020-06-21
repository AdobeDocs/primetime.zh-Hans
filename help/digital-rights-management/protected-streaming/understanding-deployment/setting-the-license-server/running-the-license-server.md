---
seo-title: 为受保护的流运行DRM服务器
title: 为受保护的流运行DRM服务器
uuid: 9bbe211d-268b-43c2-9e55-7ce62de40d30
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 0%

---


# 为受保护的流运行DRM服务器 {#running-the-drm-server-for-protected-streaming}

在开始Adobe Primetime DRM Server for Protected Streaming之前，建议您验证配置文件中设置的有效性。

您可以使用随许可证服务器提供的实用程序验证设置的有效性。 (请参 *阅本指南* 中的Configuration Validator。

如果要开始Tomcat和许可证服务器，则需要运行或 [!DNL catalina.bat start] 从 [!DNL catalina.sh start] Tomcat的目录 [!DNL bin] 运行。

服务器启动后，您需要通过打开ense-server-host:port>/flashaccessserver/ [!DNL https://<lic<span></span>来验证是否已正确配置服务器<tenant-name>/flashaccess/license] /v1。 如果租户配置已成功加载，则会显示确认消息。

## 日志文件 {#log-files}

Adobe Primetime DRM Server为受保护的流应用程序生成的日志文件位于LicenseServer.LogRoot指定的目录中。

>[!NOTE] {class=&quot;-主题／注释&quot;
>
>如果当前日志文件在服务器运行时被删除或移动，则不能重新创建日志文件。 因此，某些日志信息可能会被删除。

### 日志目录结构 {#section_F490A483D60145ADBC21038914C39203}

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

### 全局日志文件 {#section_1CFA90748142439C9F3BE380969539DA}

全局日志文件 [!DNL flashaccess-global.log]位于LicenseServer. *LogRoot中*。 日志可能包括Adobe Primetime DRM Java SDK或日志消息在服务器初始化期间生成的日志消息。

### 分区日志文件 {#section_5660137CD6AA40519E72A4315534846B}

分区日志文 [!DNL flashaccess-partition.log]件位于目录 [!DNL <LicenseServer.LogRoot>/flashaccesserver] 中。 它包括在处理许可证请求期间生成的日志消息。

### 租户日志文件 {#section_F0257CC0831647F18A746B4F02E3E910}

每个租户的租户日志 [!DNL flashaccess-tenant.log]文件位 [!DNL 于&lt;LicenseServer.LogRoot>/flashaccesserver/armoes/<tenantname>]. 租户日志包含审计信息，用于描述为此租户生成的每个许可证。

## 更新配置文件 {#updating-configuration-files}

一旦许可证服务器读取许可证服务器配置文件（全局或租户配置）之一，配置信息就缓存在内存中。 因此，对于每个许可证请求，都不必从磁盘读取文件。 但是，服务器还允许修改配置文件中的大多数值，而无需服务器重新启动，更改才能生效。

只要修改配置文件，许可证服务器就会存储文件上次修改的时间。 服务器以可配置的时间间隔检查文件修改时间是否已更改。 如果它已更改，服务器将自动重新加载配置文件的内容。

如果要控制服务器检查更新的频率，您需要在全局配 `refreshDelaySeconds` 置文件的元 `Caching` 素中设置属性。 例如，如果 `refreshDelaySeconds` 设置为3600秒，则服务器将在配置文件修改时间起的最多一小时内更新配置。 如果 `refreshDelaySeconds` 设置为0，则服务器会在每次请求时检查配置更新。 不建议在任何生产环境 `refreshDelaySeconds` 中设置低值，因为这样做会影响性能。

元 `Caching` 素还控制一次缓存的租户配置数。 您可以将此值设置为小于租户总数的数字，以限制用于缓存配置信息的内存量。 如果接收到不在缓存中的租户的请求，则在处理请求之前加载配置。 如果缓存已满，则从缓存中删除最近使用最少的租户。

在以下情况下（直到下次服务器检查更新时），配置的缓存版本仍继续使用：

* 如果在服务器尝试读取文件时，将更改保存到配置文件或文件中引 [!DNL flashaccess-tenant.xml] 用的任何证书文件中
* 如果发现文件的时间戳比当前时间早一秒
* 如果文件的时间戳将在将来

如果没有缓存版本，则加载配置失败，并且向客户端返回错误。 然后，服务器在下次收到该租户的请求时再次尝试加载该文件。

### 更新全局配置文件 {#section_AA546C72442646CFB8906AEEBDF50587}

您可以随时修改 [!DNL flashaccess-global.xml] HSM密码。 这些更改将在服务器下次重新加载配置文件时生效。 但是，不会重新加载对记录和缓存元素所做的更改。 在对这些元素所做的任何更改生效之前，您需要重新启动服务器。

### 更新租户配置文件 {#section_71624DB8DF28480F84F34F0FF7FD4365}

可以随时修改文件中指 [!DNL flashaccess-tenant.xml] 定的所有值。 这些更改将在服务器下次重新加载配置文件时生效。 此外，服务器检查所有凭据()文件中是否有任何 [!DNL .pfx]修改，并且打包程序允许列表证书文件在租户配置文件中引用。