---
title: Primetime Offline Packager 2.x版
seo-title: Primetime Offline Packager 2.x版
description: Primetime Offline Packager 2.1和2.3.1版本的新增功能
seo-description: Primetime Offline Packager 2.1和2.3.1版本的新增功能
uuid: 01926a10-890d-477d-b832-e22847d957e0
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
discoiquuid: 933a0711-846a-4bb7-bf51-b300822a93d4
translation-type: tm+mt
source-git-commit: e644e8497e118e2d03e72bef727c4ce1455d68d6
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 0%

---


# Primetime Offline Packager版本{#primetime-offline-packager-x-releases}

Primetime Offline Packager 2.1和2.3.1版本的新增功能

## Primetime Offline Packager 2.3.1（2016年10月）{#what-s-new-in-primetime-offline-packager-oct}的新增功能

该发行版启用了MPEG-DASH的按需用户档案，增加了对PlaylistCreator工具的`validate`选项的支持，并且对下面列出的多DRM方案几乎没有关键修复。

| **问题编号** | **说明** |
|---|---|
| PTPUB-985 | HLS AAXS和Sample-AES不适用于打包程序生成的密钥 |
| PTPUB-973 | 修复了某些特定Widevine内容的加密算法错误 |
| PTPUB-964 | 某些播放器(Android TVSDK)上某些媒体类型的CENC加密已破坏。 |
| PTPUB-954 | 默认情况下，Sample-AES加密会绕过AAXS DRM/启用远程密钥投放时引发的错误。 |
| PTPUB-951 | 当未使用Widevine指定key_file_path时，脱机打包程序不会引发异常。 而是抛弃NPE。 |

有关Primetime Packager的最新文档，请访问[https://help.adobe.com/en_US/primetime/api/packagers/index.html](https://help.adobe.com/en_US/primetime/api/packagers/index.html)。

### 版本2.3.1 {#known-issue-in-version}中的已知问题

此版本中存在以下问题。

| **问题编号** | **说明** |
|---|---|
| PTPUB-1005 | PlaylistCreator未为为AAXS DRM生成的最终设置级。mpd文件中的。pssh文件提供正确的URL。 |
| PTPUB-1001 | 当通过in_path参数提供空路径时，PlaylistCreator应抛出错误 |
| PTPUB-990 | 对于DASH，当指定参数`log_vi`和`iv_out_path`时，Offline Packager不将包装程序生成的IV写入磁盘。 |
| PTPUB-980 | 当使用配置文件进行打包时，使用参数`key_url`不会从提供的输入中删除引号。 |

## Adobe Primetime脱机包装程序2.3.1 {#adobe-primetime-offline-packager}

### 最低系统要求{#minimum-system-requirements}

支持的操作系统

* Linux CentOS 6.3 64位

硬件要求

* 3.2GHz Intel® Pentium® 4处理器（建议使用双Intel Xeon®或更快的处理器）

* 64位操作系统：4GB内存（推荐8GB）

* 硬盘

（磁盘-SAS）:最少10GB，带7.5K RPM

（磁盘——固态硬盘）:400MBps读／写速度

(NAS):1 GB专用链接

软件要求

* OracleJava SE 1.8或更高版本

### Adobe Primetime脱机包装程序2.3.1 {#adobe-primetime-offline-packager-1}

1. 从[Oracle站点](https://www.oracle.com/technetwork/java/javase/downloads/index.html)下载Java SE软件，然后按照安装说明操作。
1. 将名为`PrimetimeOfflinePackager-2-3-1-b47-10142016.zip`的Adobe Primetime脱机包装程序2.3.1存档文件解压到磁盘。

### 配置Offline Packager 2.3.1 {#configuring-the-offline-packager}

有关配置说明，请参阅Primetime Offline Packager快速入门指南，网址为[https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)

## Primetime Offline Packager 2.1（2015年7月）{#what-s-new-in-primetime-offline-packager-july}的新增功能

支持PlayReady BuyDRM（用于DASH）。 有关详细信息，请参阅此处提供的帮助文档[](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)。

还对脱机包装程序进行了以下增强。

PTPUB-780增加了对EXT-X-开始标记的支持

## Primetime Offline Packager 2.0（2015年6月）的新增功能{#what-s-new-in-primetime-offline-packager-june}

已添加清晰的DASH输出支持。 有关详细信息，请参阅产品文档[此处](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)。

此版本中还修复了以下问题。

* PTPUB-783 Offline Packager现在可处理空的WebVTT文件。
* PTPUB - 781当某些经过转码的MP4资源与脱机包装器一起打包以生成MBR输出时，Chrome上HLS输出中的伪像。

## Adobe Primetime脱机包装程序2.1 {#adobe-primetime-offline-packager-2}

### 最低系统要求{#minimum-system-requirements-1}

**支持的操作系统**

* Linux CentOS 6.3 64位

**硬件要求**

* 3.2GHz Intel® Pentium® 4处理器（建议使用双Intel Xeon®或更快的处理器）

* 64位操作系统：4GB内存（推荐8GB）

* 建议使用1Gb以太网卡（还支持多个网卡和10Gb）

* 硬盘

   * （磁盘-SAS）:最少10GB，带7.5K RPM
   * （磁盘——固态硬盘）:400MBps读／写速度
   * (NAS):1 GB专用链接

**软件要求**

* OracleJava SE 1.8或更高版本

### 正在安装Offline Packager 2.1 {#installing-offline-packager}

1. 从[Oracle站点](https://www.oracle.com/technetwork/java/javase/downloads/index.html)下载Java SE软件，然后按照安装说明操作。
1. 将`Adobe Primetime - Offline Packager 2.1.0 archive file, PrimetimeOfflinePackager-2-1-0-b15-07082015.zip`解压到磁盘。

### 配置Offline Packager 2.1 {#configuring-the-offline-packager-1}

有关此处提供的配置详细信息，请参阅Primetime Offline Packager快速入门文档[https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)

## 帮助资源{#helpful-resources}

* 请参阅[Adobe Primetime学习和支持](https://helpx.adobe.com/support/primetime.html)页面上的完整帮助文档。