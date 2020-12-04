---
seo-title: 代码投放/包内容
title: 代码投放/包内容
uuid: 13de2fd4-9079-496c-a087-25176c118864
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# 代码投放/包内容{#code-delivery-package-contents}

Adobe PrimetimeDRM本地个性化服务器包包含以下内容：

* [!DNL flashaccess.war] -个性化服务器
* [!DNL flashaccess-kgs.war] -可选的密钥生成服务器
* [!DNL /shared] -包含：

   * [!DNL adobe-flashaccess-certs.jar]
   * [!DNL AdobeInitial.properties] -示例属性文件

* [!DNL thirdparty/] -将Crypto-J支持作为本机库：

   * [!DNL libjsafe.so] (Linux)
   * [!DNL jsafe.dll] (Windows)

* [!DNL adobe-flashaccess-i15n-setup.jar] -用于加密服务器凭据密码的实用程序
* [!DNL ROOT] -包含文 [!DNL crossdomain.xml] 件

* ECI缓存文件——预下载
* [!DNL addIndivCert.py] -用于更新许可证服务器的信任根以支持本地个性化的脚本
* [!DNL CreateMetadata.jar] -用于创建本地DRM元数据的实用程序
* [!DNL client_sample/] -包含客户端代码片段的文件夹
* 发行说明——对于文档的任何最后添加内容

