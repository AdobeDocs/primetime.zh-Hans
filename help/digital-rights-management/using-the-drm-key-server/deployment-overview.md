---
title: 部署Primetime DRM密钥服务器概述
description: 部署Primetime DRM密钥服务器概述
copied-description: true
exl-id: d70e8315-ed35-4159-842b-5066a2b1c4f0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 0%

---

# 部署Primetime DRM密钥服务器 {#deploy-the-primetime-drm-key-server}

在部署Primetime DRM密钥服务器之前，请确保已安装了所需的Java和Tomcat版本。 参见， [DRM关键服务器要求](../../digital-rights-management/using-the-drm-key-server/requirements.md).

Primetime DRM密钥服务器下载包括 [!DNL faxsks.war]. 要部署此WAR文件，请将文件复制到Tomcat的 [!DNL webapps] 目录。 如果您以前部署过WAR文件，您可能需要手动删除解压缩的WAR目录， [!DNL faxsks] 在Tomcat的 [!DNL webapps] 目录)。 要防止Tomcat解压缩WAR文件，请编辑 [!DNL server.xml] tomcat中的文件 [!DNL conf] 目录并设置 `unpackWARs` 属性至 `false`.

Primetime DRM密钥服务器可以选择使用平台特定的库(`jsafe.dll` 在Windows或 `libjsafe.so` （在Linux上）以提高性能。 从以下位置复制适用于您的平台的库： `thirdparty/cryptoj/platform` 到指定的位置 `PATH` 环境变量(或 `LD_LIBRARY_PATH` 在Linux上)。

>[!NOTE]
>
>的64位版本 [!DNL jsafe] 仅当操作系统和JDK都支持64位时，才应使用库，否则请使用32位版本。

## SSL配置 {#ssl-configuration}

远程HTTPS密钥投放需要SSL。 SSL连接可由应用程序服务器处理（即，通过在Tomcat中配置SSL），也可在其他服务器（即，负载平衡器、SSL加速器或Apache）上处理。 远程HTTPS密钥投放需要SSL连接。 服务器需要由受信任CA颁发的SSL证书。

配置SSL有多种选项。 以下是有关在Apache和Tomcat中使用客户端身份验证配置SSL的示例。

以下示例显示了Apache SSL配置：

```
SSLEngineon 
SSLCertificateFile "certs/server_cert.pem" 
SSLCertificateKeyFile "certs/server_key.pem" 
SSLOptions +StdEnvVars +FakeBasicAuth -ExportCertData +StrictRequire 
SSLRequireSSL 
ProxyRequests Off 
ProxyPass /https://keyserver-name:port/ 
ProxyPassReverse /https://keyserver-name:port/
```

以下示例显示了Tomcat SSL配置。 要生成证书和密钥文件，请执行以下操作：

```
Generate key:  
 openssl genrsa -des3 -out server.key 1024 
Generate CSR: 
 openssl req -new -key server.key -out server.csr 
Generate Certificate: 
 openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.cer
```

当提示您输入通用名称时，请使用服务器的完全限定域名(FQDN)。

复制 [!DNL server.cer]、和 [!DNL server.key] 到Tomcat目录。 在中指定以下连接器 [!DNL conf/server.xml]：

```
<Connector port="8443" protocol="HTTP/1.1" SSLEnabled="true" 
 maxThreads="150" scheme="https" secure="true" 
 sslProtocol="TLS" 
 SSLCertificateFile="${catalina.base}/server.cer" 
 SSLCertificateKeyFile="${catalina.base}/server.key" 
 SSLPassword="password-for-key-file" 
 SSLVerifyClient="require"/>
```

## Java系统属性 {#java-system-properties}

您可以选择设置以下两个Java系统属性，以修改Primetime DRM密钥服务器的配置和日志文件的位置：

* `KeyServer.ConfigRoot`  — 此目录包含Primetime DRM密钥服务器的所有配置文件。 有关这些文件内容的详细信息，请参见 [密钥服务器配置文件](#key-server-configuration-files). 如果未设置，则默认为 [!DNL CATALINA_BASE/keyserver].

* `KeyServer.LogRoot`  — 这是一个日志目录，其中包含iOS Key Server应用程序日志。 如果未设置，则默认值与 `KeyServer.ConfigRoot`

* `XboxKeyServer.LogRoot`  — 这是一个日志目录，其中包含Xbox Key Server应用程序日志。 如果未设置，则默认值与 `KeyServer.ConfigRoot`.

如果您使用 [!DNL catalina.bat] 或 [!DNL catalina.sh] 要启动Tomcat，可以使用轻松设置这些系统属性 `JAVA_OPTS` 环境变量。 此处设置的任何Java选项都将在启动Tomcat时使用。 例如，设置：

```
JAVA_OPTS=-DKeyServer.ConfigRoot=”absolute-path-to-config-folder” 
  -DKeyServer.LogRoot=”absolute-path-to-log-folder”
```

## Primetime DRM凭据 {#primetime-drm-credentials}

要处理来自Primetime DRM iOS和Xbox 360客户端的密钥请求，必须使用Adobe颁发的一组凭据配置Primetime DRM密钥服务器。 这些凭据可以存储在PKCS#12 ( [!DNL .pfx])文件或HSM上。

此 [!DNL .pfx] 文件可以位于任何位置，但为了便于配置，Adobe建议将 [!DNL .pfx] 租户配置目录中的文件。 有关更多信息，请参阅 [密钥服务器配置文件](#key-server-configuration-files).

### HSM配置 {#section_13A19E3E32934C5FA00AEF621F369877}

如果选择使用HSM存储服务器凭据，则必须将私钥和证书加载到HSM上并创建 *pkcs11.cfg* 配置文件。 该文件必须位于 *KeyServer.ConfigRoot* 目录。 请参阅 `<Primetime DRM Key Server>/configs` PKCS 11配置文件的示例目录。 有关格式的信息 [!DNL pkcs11.cfg]请参见Sun PKCS11提供程序文档。

要验证HSM和Sun PKCS11配置文件是否正确配置，可以使用以下目录中的命令： [!DNL pkcs11.cfg] 文件位于( [!DNL keytool] 随Java JRE和JDK一起安装)：

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

如果在列表中看到您的凭据，则HSM已正确配置，并且密钥服务器将能够访问凭据。

## 密钥服务器配置文件 {#key-server-configuration-files}

Primetime DRM密钥服务器需要两种类型的配置文件：

* 全局配置文件， [!DNL flashaccess-keyserver-global.xml]
* 每个租户的租户配置文件， [!DNL flashaccess-keyserver-tenant.xml]

如果对配置文件进行了更改，则必须重新启动服务器以使更改生效。

为避免在配置文件中以明文形式提供密码，必须对全局配置文件和租户配置文件中指定的所有密码进行加密。 有关加密密码的详细信息，请参阅 [*密码加扰器* 在 *使用Primetime DRM服务器进行受保护的流*](../protected-streaming/understanding-deployment/drm-for-protected-streaming-utilities/password-scrambler.md).

## 配置目录结构 {#configuration-directory-structure}

配置目录具有以下结构：

```
KeyServer.ConfigRoot/  
--flashaccess-keyserver-global.xml 
--pkcs11.cfg (optional) 
--faxsks/ 
----tenants/ 
------tenantname/
---------flashaccess-keyserver-tenant.xml 
---------credential.pfx (optional) 
```

## 全局配置文件 {#global-configuration-file}

此 [!DNL flashaccess-keyserver-global.xml] 配置文件包含适用于密钥服务器的所有租户的设置。 此文件必须位于 `KeyServer.ConfigRoot`. 请参阅 [!DNL configs] 目录中的示例全局配置文件。 全局配置文件包含以下内容：

* 日志记录 — 指定日志记录级别和日志文件滚动的频率。
* HSM密码 — 仅当使用HSM存储服务器凭据时才需要。

请参见位于以下位置的示例全局配置文件中的注释： `<Primetime DRM Key Server>/configs` 了解更多详细信息。

## 租户配置文件 {#tenant-configuration-files}

此 [!DNL flashaccess-ioskeyserver-tenant.xml] 和 [!DNL flashaccess-xboxkeyserver-tenant.xml] 配置文件包含应用于Primetime DRM密钥服务器的特定租户的设置。 每个租户都有其自己的配置文件实例，位于 [!DNL <KeyServer.ConfigRoot>/faxsks/tenants/tenantname]. 请参阅 [!DNL configs/faxsks/tenants/sampletenant] 示例租户配置文件的目录。

您可以将租户配置文件中的所有文件路径指定为绝对路径或相对于租户配置目录的路径( [!DNL <KeyServer.ConfigRoot>/faxsks/tenants/tenantname])。

所有租户配置文件包括：

* Key Server凭据 — 指定Adobe颁发的一个或多个密钥服务器凭据（证书和私钥）。 可以指定为路径 [!DNL .pfx] 文件和密码，或存储在HSM上的凭据的别名。 可在此处指定多个此类凭据，或者指定为文件路径，或者指定为密钥别名，或者同时指定这两者。

此 **iOS** 租户配置文件包括：

* 密钥提交窗口 — （可选）指定密钥提交请求时间戳有效期（以秒为单位）。 默认值为500秒。

此 **Xbox 360** 租户配置文件包括：

* XSTS凭据 — 指定用于解密XSTS令牌的应用程序开发人员凭据
* XSTS签名证书 — 指定用于验证XSTS令牌上的签名的证书。
* Packager允许列表 — 密钥服务器信任的打包程序证书。 如果列表中未包含任何打包程序证书，则所有打包程序证书都将被信任。

## 日志文件 {#log-files}

由Primetime DRM密钥服务器应用程序生成的日志文件( [!DNL flashaccess-ioskeyserver_*.log] 和 [!DNL flashaccess-xboxkeyserver_*.log])将位于指定的目录中 `KeyServer.LogRoot`.

日志文件按客户机类型进行区分。 每种客户端类型有两个日志：

* An *访问日志*  — 仅监控请求和响应。
* A *上下文日志*  — 包含详细的错误消息和栈栈跟踪。

## 启动密钥服务器 {#starting-the-key-server}

要启动密钥服务器，请启动Tomcat。
