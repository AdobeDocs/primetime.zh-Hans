---
title: 部署Primetime DRM Key Server概述
description: 部署Primetime DRM Key Server概述
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 0%

---


# 部署Primetime DRM密钥服务器{#deploy-the-primetime-drm-key-server}

在部署Primetime DRM Key Server之前，请确保您已安装所需版本的Java和Tomcat。 请参阅[DRM关键服务器要求](../../digital-rights-management/using-the-drm-key-server/requirements.md)。

Primetime DRM密钥服务器下载包含[!DNL faxsks.war]。 要部署此WAR文件，请将该文件复制到Tomcat的[!DNL webapps]目录。 如果之前已部署WAR文件，则可能需要手动删除解压缩的WAR目录（位于Tomcat的[!DNL webapps]目录中的[!DNL faxsks]）。 要防止Tomcat解包WAR文件，请编辑Tomcat的[!DNL conf]目录中的[!DNL server.xml]文件，并将`unpackWARs`属性设置为`false`。

Primetime DRM密钥服务器（可选）使用平台特定库（Windows上的`jsafe.dll`或Linux上的`libjsafe.so`）以提高性能。 将平台的相应库从`thirdparty/cryptoj/platform`复制到由`PATH`环境变量（或Linux上的`LD_LIBRARY_PATH`）指定的位置。

>[!NOTE]
>
>[!DNL jsafe]库的64位版本仅在操作系统和JDK都支持64位时才应使用，否则请使用32位版本。

## SSL配置{#ssl-configuration}

远程HTTPS密钥投放需要SSL。 SSL连接可以由应用程序服务器处理（即，在Tomcat中配置SSL），也可以在另一台服务器（即负载平衡器、SSL加速器或Apache）上处理。 远程HTTPS密钥投放需要SSL连接。 服务器需要由受信任的CA颁发的SSL证书。

配置SSL有多种选项。 下面是在Apache和Tomcat中通过客户端身份验证配置SSL的示例。

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

当系统提示输入通用名称时，请使用服务器的“完全限定域名”(FQDN)。

将[!DNL server.cer]和[!DNL server.key]复制到Tomcat目录。 在[!DNL conf/server.xml]中指定以下连接器：

```
<Connector port="8443" protocol="HTTP/1.1" SSLEnabled="true" 
 maxThreads="150" scheme="https" secure="true" 
 sslProtocol="TLS" 
 SSLCertificateFile="${catalina.base}/server.cer" 
 SSLCertificateKeyFile="${catalina.base}/server.key" 
 SSLPassword="password-for-key-file" 
 SSLVerifyClient="require"/>
```

## Java系统属性{#java-system-properties}

您可以选择设置以下两个Java系统属性来修改Primetime DRM密钥服务器的配置和日志文件的位置：

* `KeyServer.ConfigRoot`  — 此目录包含Primetime DRM密钥服务器的所有配置文件。有关这些文件内容的详细信息，请参阅[关键服务器配置文件](#key-server-configuration-files)。 如果未设置，则默认值为[!DNL CATALINA_BASE/keyserver]。

* `KeyServer.LogRoot`  — 这是包含iOS密钥服务器应用程序日志的日志目录。如果未设置，则默认值与`KeyServer.ConfigRoot`相同

* `XboxKeyServer.LogRoot`  — 这是一个日志目录，其中包含Xbox Key Server应用程序日志。如果未设置，则默认值与`KeyServer.ConfigRoot`相同。

如果您使用[!DNL catalina.bat]或[!DNL catalina.sh]开始Tomcat，则可以使用`JAVA_OPTS`环境变量轻松设置这些系统属性。 启动Tomcat时，将使用此处设置的任何Java选项。 例如，设置：

```
JAVA_OPTS=-DKeyServer.ConfigRoot=”absolute-path-to-config-folder” 
  -DKeyServer.LogRoot=”absolute-path-to-log-folder”
```

## Primetime DRM凭据{#primetime-drm-credentials}

要处理来自Primetime DRM iOS和Xbox 360客户端的密钥请求，Primetime DRM密钥服务器必须配置由Adobe发出的一组凭据。 这些凭据可以存储在PKCS#12([!DNL .pfx])文件中，也可以存储在HSM中。

[!DNL .pfx]文件可以位于任何位置，但为了便于配置，Adobe建议将[!DNL .pfx]文件放在租户的配置目录中。 有关详细信息，请参阅[密钥服务器配置文件](#key-server-configuration-files)。

### HSM配置{#section_13A19E3E32934C5FA00AEF621F369877}

如果选择使用HSM存储服务器凭据，则必须将私钥和证书加载到HSM上并创建&#x200B;*pkcs11.cfg*&#x200B;配置文件。 此文件必须位于&#x200B;*KeyServer.ConfigRoot*&#x200B;目录中。 有关PKCS 11配置文件的示例，请参见`<Primetime DRM Key Server>/configs`目录。 有关[!DNL pkcs11.cfg]格式的信息，请参阅Sun PKCS11提供程序文档。

要验证您的HSM和Sun PKCS11配置文件是否配置正确，可以从[!DNL pkcs11.cfg]文件所在的目录（[!DNL keytool]随Java JRE和JDK一起安装）中使用以下命令：

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

如果您在列表中看到凭据，则HSM配置正确，密钥服务器将能够访问凭据。

## 密钥服务器配置文件{#key-server-configuration-files}

Primetime DRM密钥服务器需要两种类型的配置文件：

* 全局配置文件[!DNL flashaccess-keyserver-global.xml]
* 每个租户的租户配置文件，[!DNL flashaccess-keyserver-tenant.xml]

如果对配置文件进行了更改，则必须重新启动服务器才能使更改生效。

为避免在配置文件中以明文提供密码，必须加密全局配置文件和租户配置文件中指定的所有密码。 有关加密密码的详细信息，请参阅&#x200B;*使用Primetime DRM Server for Protected Streaming*](../protected-streaming/understanding-deployment/drm-for-protected-streaming-utilities/password-scrambler.md)&#x200B;中的&#x200B;[*密码剪贴器*。

## 配置目录结构{#configuration-directory-structure}

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

## 全局配置文件{#global-configuration-file}

[!DNL flashaccess-keyserver-global.xml]配置文件包含适用于密钥服务器的所有租户的设置。 此文件必须位于`KeyServer.ConfigRoot`中。 有关示例全局配置文件，请参阅[!DNL configs]目录。 全局配置文件包括：

* 日志记录 — 指定日志记录级别以及滚动日志文件的频率。
* HSM密码 — 仅当使用HSM存储服务器凭据时才需要。

有关详细信息，请参阅`<Primetime DRM Key Server>/configs`中示例全局配置文件中的注释。

## 租户配置文件{#tenant-configuration-files}

[!DNL flashaccess-ioskeyserver-tenant.xml]和[!DNL flashaccess-xboxkeyserver-tenant.xml]配置文件包含适用于Primetime DRM密钥服务器的特定租户的设置。 每个租户都有其自己的这些配置文件实例位于[!DNL <KeyServer.ConfigRoot>/faxsks/tenants/tenantname]中。 有关示例租户配置文件，请参阅[!DNL configs/faxsks/tenants/sampletenant]目录。

可以将租户配置文件中的所有文件路径指定为相对于租户配置目录([!DNL <KeyServer.ConfigRoot>/faxsks/tenants/tenantname])的绝对路径或路径。

所有租户配置文件包括：

* 密钥服务器凭据 — 指定由Adobe颁发的一个或多个密钥服务器凭据（证书和私钥）。 可以指定为[!DNL .pfx]文件和密码的路径，或HSM上存储的凭据的别名。 可以在此处指定多个此类凭据，例如文件路径或密钥别名，或同时指定这两个凭据。

**iOS**&#x200B;租户配置文件包括：

* 键投放窗口 — （可选）指定键投放请求时间戳有效性窗口（以秒为单位）。 默认值为500秒。

**Xbox 360**&#x200B;租户配置文件包括：

* XSTS凭据 — 指定用于解密XSTS令牌的应用程序开发者的凭据
* XSTS签名证书 — 指定用于验证XSTS令牌上签名的证书。
* Packager允许列表 — 密钥服务器信任的Packager证书。 如果列表中没有包装程序证书，则所有打包程序证书都将受信任。

## 日志文件{#log-files}

由Primetime DRM密钥服务器应用程序（[!DNL flashaccess-ioskeyserver_*.log]和[!DNL flashaccess-xboxkeyserver_*.log]）生成的日志文件将位于由`KeyServer.LogRoot`指定的目录中。

日志文件可按客户端类型进行区分。 每个客户端类型有两个日志：

* *访问日志* — 仅监视请求和响应。
* *上下文日志* — 包含详细的错误消息和堆栈跟踪。

## 启动密钥服务器{#starting-the-key-server}

要开始密钥服务器，请开始Tomcat。