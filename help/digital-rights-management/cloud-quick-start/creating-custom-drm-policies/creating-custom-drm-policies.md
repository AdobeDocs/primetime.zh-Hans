---
title: 创建自定义DRM策略（可选）
description: 创建自定义DRM策略（可选）
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# 创建自定义DRM策略（可选）{#create-custom-drm-policies-optional}

Primetime Cloud DRM Protection Kit附带几个可在打包期间使用的预配置策略。 如果需要其他策略配置(例如，特定的SWF允许列表权限)，则可以使用所包含的Primetime DRM策略管理器来生成自定义策略。

>[!NOTE]
>
>所有策略都必须使用匿名身份验证（不是用户名密码或自定义） — 无论是否使用自定义身份验证/授权工作流。

策略管理器包括 [!DNL flashaccesstools.properties] 配置文件，已修改为仅显示Primetime云DRM服务支持的可配置策略选项。 设置Primetime云DRM服务不支持的策略选项将导致许可证获取错误。 有关使用Primetime DRM策略管理器的信息，请参阅： [Primetime DRM参考实施：策略管理器](https://help.adobe.com/en_US/primetime/drm/5.3/reference_implementations/index.html#concept-DRM_Policy_Manager).

要创建新策略，请更新 [!DNL flashaccesstools.properties] 文件，然后使用命令：

```
java -jar libs/AdobePolicyManager.jar new myPolicy.pol
```

## 为自定义身份验证/授权动态创建策略{#create-policies-dynamically-for-custom-auth-entitlement}

如果您使用Primetime Cloud DRM自定义身份验证/授权，并且希望为每个许可证请求动态创建新的DRM策略（而不是从预生成的池中提取策略），Adobe建议您直接使用Primetime DRM Java SDK。 直接使用Java SDK比使用 [!DNL AdobePolicyManager.jar] 工具自动将策略文件输出到磁盘，从而产生磁盘I/O开销。

使用Java SDK的示例代码位于 [!DNL /Primetime DRM PolicyManager/sampleCode/] 目录，已命名 [!DNL CreatePolicy.java] 和 [!DNL CreatePolicyWithOutputProtection.java]. 有关Java SDK的Javadoc和文档，请访问 [Adobe Primetime DRM SDK概述](../../../digital-rights-management/drm-sdk-overview/overview.md)

要生成并运行示例，请将.java文件复制到……/libs/文件夹并运行：

```
javac -cp adobe-flashaccess-sdk.jar:. CreatePolicy.java
java -cp adobe-flashaccess-sdk.jar:. CreatePolicy
```
