---
title: 使用随附的Primetime Offline Packager
description: 使用随附的Primetime Offline Packager
copied-description: true
exl-id: 6a1d0dc3-8906-4de5-8351-890c1cf31efd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# 使用随附的Primetime Offline Packager{#use-the-included-primetime-offline-packager}

您的Primetime Java Packager预配置了打包内容所需的大多数设置。 要开始操作，只需更新几个区域。

## 更新打包程序属性 {#section_99904D35E99944A28FF43D924E516CC2}

当前任务的上下文

* 在使用配置文件打包内容之前，请更新以下打包程序属性：

### 用户提供的XML配置文件属性

| 属性名称 | 描述 |
|---|---|
| `policy_file` | 策略文件路径。 Adobe应提供多个预配置的策略以供选择。 |
| `pkgr_pfx` | Packager凭据路径。 您必须提供自己的Adobe颁发的打包程序凭据( [!DNL .pfx])此处。 |
| `pkgr_pfx_pwd` | Packager凭据密码。 您必须在此处提供密码以使用Adobe颁发的打包程序凭据。 |

## 使用命令行打包 {#section_DFBE462679E34D62963BE201FD3321F9}

在打包内容之前，请确保配置文件中提供了所有必需的信息。

* 要使用配置文件打包内容，请在命令行中使用以下语法：

```
java -jar OfflinePackager.jar -conf_path [configuration filename]
```

提供了将内容打包为HLS或HDS格式的示例配置文件，名为 [!DNL config_hds.xml] 和 [!DNL config.hls.xml].

HDS或HLS内容将输出到 [!DNL /output] 文件夹（位于“保护套件”目录下）。 所有写入此目录的工件都必须托管在HTTP Web服务器上，才能播放。
