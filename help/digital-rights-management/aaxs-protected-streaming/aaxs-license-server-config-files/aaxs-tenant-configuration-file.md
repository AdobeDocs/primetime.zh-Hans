---
seo-title: 租户配置文件
title: 租户配置文件
uuid: 6e5c82c9-b8f5-4fca-8325-a884b2c779f7
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 0%

---


# 租户配置文件 {#tenant-configuration-file}

flashaccess-tenant.xml配置文件包含适用于许可证服务器的特定租户的设置。 每个租户都有其自己的此配置文件实 *例位于LicenseServer.ConfigRoot* [!DNL /flashaccessserver/tenants/]*tenantname中&#x200B;*。 请参阅[!DNL configs/flashaccessserver/tenants/sampletenant]示例租户配置文件的目录。

可以将租户配置文件中的所有文件路径指定为相对于租户配置目录(LicenseServer.ConfigRootTenantname)的&#x200B;*绝对路径*[!DNL /flashaccessserver/tenants/]*或路径&#x200B;*。

租户配置文件包括：

* **传输凭证** -指定由Adobe颁发的一个或多个传输凭证（证书和私钥）。 可以指定为。pfx文件和密码的路径，或存储在HSM上的凭据的别名。 可以在此处指定多个此类凭据，例如文件路径或密钥别名，或同时指定这些凭据。 有关何时[需要其他凭据](../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-cert-updates.md)，请参 *阅使用Adobe Access SDK for Protecting Content* ，中的“处理证书更新”。
* **License Server Credential** —指定由Adobe颁发的一个或多个License Server凭据（证书和私钥）。 可以指定为。pfx文件和密码的路径，或存储在HSM上的凭据的别名。 可以在此处指定多个此类凭据，例如文件路径或密钥别名，或同时指定这些凭据。 有关何时需要额外凭据的更多信息，请参阅*使用Adobe Access SDK保护内容*中的处理证书更新。
* **密钥服务器证书** —可选。 指定Adobe颁发的密钥服务器的许可证服务器证书。 可以指定为。cer文件的路径或HSM上存储的证书的别名。 必须指定此选项，才能为与要求iOS设备远程密钥投放的策略一起打包的内容颁发许可证。
* **自定义授权者** -可选。 指定要为每个许可证请求调用的自定义授权器类。 如果指定了多个授权者，则按所列顺序调用它们。 有关详细信息，请参阅“[自定义授权扩展](../../aaxs-protected-streaming/custom-authorization-extensions.md)”。
* **列表授权包装者** -可选。 指定用于标识授权打包此许可证服务器内容的实体的证书。 如果未指定打包程序证书，服务器将为由任何打包程序打包的内容颁发许可证。
* **支持的最低客户端版** 本( *请参阅使用Adobe Access SDK保护内容*)。
* **使用规则**

   * **许可证缓存** —可选。 指定许可证可存储在客户端上的时间。 默认情况下，许可证缓存处于禁用状态。 要在限定的时间段内启用许可证缓存，请设置结束日期或应存储许可证的秒数（从颁发许可证开始）。 将秒数设置为0将禁用许可证缓存。

      请注意，服务器为受保护流发放的所有许可证的有效期为24小时（86400秒）。 因此，此值将隐式作为上限应用于为许可证缓存设置的任何结束日期或持续时间，最大值为86400秒，即使模式强制使用更高的界限。

   * **播放权** —必须至少指定一个权限。 如果指定了多个权限，则客户端将使用其符合所有要求的第一个权限。

      * **输出保护** -控制输出到外部渲染设备是否应受保护。
      * **AIR和SWF应用程序限制** -可选允许播放内容的SWF和AIR应用程序列表（即，仅允许指定的应用程序）。 SWF应用程序由URL或SWF的摘要来标识，并且允许下载和验证摘要的最长时间。 有关计算SWF摘要的信息，请参阅“SWF哈希计算器”部分。 AIR和iOS应用程序由发布者ID和可选应用程序 ID、最低版本和最高版本标识。 如果未指定任何应用程序限制，任何SWF或AIR应用程序都可以播放该内容。
      * **DRM和运行时模块限制** —指定DRM/运行时模块所需的最低安全级别。 可选地包括不允许播放内容的版本的块列表。 模块版本由诸如操作系统和／或版本号之类的属性来标识。 DRM模块限制和运行时模块限制现在支持以下附加属性：

         * `oemVendor`
         * `model`
         * `screenType`
         以下属性现在是可选的：

         * `osVersion`
         * `version`
      * **设备功能要求** —（可选）指定访问内容所需的硬件功能。
      * **越狱检测要求** -（可选）指定在检测到越狱的设备上不允许播放。



有关详细信息，请参阅示例租户配置文件中的注释。
