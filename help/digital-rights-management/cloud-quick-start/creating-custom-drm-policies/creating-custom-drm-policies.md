---
seo-title: 创建自定义DRM策略（可选）
title: 创建自定义DRM策略（可选）
uuid: 701b51d9-6dde-4c21-bc5b-09e612582968
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---


# 创建自定义DRM策略（可选）{#create-custom-drm-policies-optional}

Primetime Cloud DRM保护包附带一些预配置策略，可在打包过程中使用。 如果需要其他策略配置，例如特定的SWF允许列表权限，可以使用包含的Primetime DRM策略管理器生成自定义策略。

>[!NOTE]
>
>所有策略都必须使用匿名身份验证（不是用户名密码或自定义）-无论是否使用自定义身份验证／授权工作流。

策略管理器附带的配 [!DNL flashaccesstools.properties] 置文件已修改，仅提供Primetime Cloud DRM服务支持的可配置策略选项。 设置Primetime Cloud DRM服务不支持的策略选项将导致许可证获取错误。 有关使用Primetime DRM策略管理器的信息，请参阅： [Primetime DRM参考实施： 策略管理器](https://help.adobe.com/en_US/primetime/drm/5.3/reference_implementations/index.html#concept-DRM_Policy_Manager)。

要创建新策略，请根据需 [!DNL flashaccesstools.properties] 要更新文件，然后使用命令：

```
java -jar libs/AdobePolicyManager.jar new myPolicy.pol
```

## 为自定义身份验证／授权动态创建策略{#create-policies-dynamically-for-custom-auth-entitlement}

如果您使用Primetime Cloud DRM自定义身份验证／授权，并且希望为每个许可证请求动态创建新的DRM策略（而不是从预生成的池中提取策略）,Adobe建议您直接使用Primetime DRM Java SDK。 直接使用Java SDK比自动将策略文 [!DNL AdobePolicyManager.jar] 件输出到磁盘的工具速度更快，从而产生磁盘I/O开销。

使用Java SDK的示例代码可在名为和 [!DNL /Primetime DRM PolicyManager/sampleCode/] 的目录中 [!DNL CreatePolicy.java] 找到 [!DNL CreatePolicyWithOutputProtection.java]。 有关Java SDK的Javadoc和文档，请参 [阅Adobe Primetime DRM SDK概述](../../../digital-rights-management/drm-sdk-overview/overview.md)

要构建并运行示例，请将。java文件复制到。./libs/文件夹中并运行：

```
javac -cp adobe-flashaccess-sdk.jar:. CreatePolicy.java
java -cp adobe-flashaccess-sdk.jar:. CreatePolicy
```
