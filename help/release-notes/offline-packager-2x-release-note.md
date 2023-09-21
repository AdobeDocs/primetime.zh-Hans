---
title: Primetime Offline Packager 2.x版本
description: Primetime Offline Packager 2.1和2.3.1版的新增功能
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 0%

---

# Primetime Offline Packager版本 {#primetime-offline-packager-x-releases}

Primetime Offline Packager 2.1和2.3.1版的新增功能

## Primetime Offline Packager 2.3.1的新增功能（2016年10月）  {#what-s-new-in-primetime-offline-packager-oct}

此发行版本为MPEG-DASH启用了On-demand Profile，添加了对 `validate` 选项，对于下面列出的多DRM方案有一些关键修复。

| **问题编号** | **描述** |
|---|---|
| PTPUB-985 | HLS AAXS和Sample-AES不适用于打包程序生成的密钥 |
| PTPUB-973 | 修复了某些特定Widevine内容的加密算法错误 |
| PTPUB-964 | 某些播放器(Android TVSDK)上的某些媒体类型的CENC加密已中断。 |
| PTPUB-954 | 示例AES加密在默认情况下绕过AAXS DRM /在启用远程密钥传递的情况下引发错误。 |
| PTPUB-951 | 未使用Widevine指定key_file_path时，Offline Packager不会引发异常。 而是会引发NPE。 |

有关Primetime打包程序的最新文档，请访问 [https://help.adobe.com/en_US/primetime/api/packagers/index.html](https://help.adobe.com/en_US/primetime/api/packagers/index.html).

### 版本2.3.1中的已知问题 {#known-issue-in-version}

此版本中存在以下问题。

| **问题编号** | **描述** |
|---|---|
| PTPUB-1005 | 在为AAXS DRM生成的最终设置级别.mpd文件中，PlaylistCreator没有为.pssh文件提供正确的URL。 |
| PTPUB-1001 | 通过in_path参数提供空路径时，PlaylistCreator应引发错误 |
| PTPUB-990 | 对于DASH， Offline Packager不会将打包程序生成的IV写入磁盘 `log_vi` 和 `iv_out_path` 已指定。 |
| PTPUB-980 | 当配置文件用于打包时，使用参数 `key_url` 不会从提供的输入中删除引号。 |

## Adobe Primetime Offline Packager 2.3.1 {#adobe-primetime-offline-packager}

### 最低系统要求 {#minimum-system-requirements}

支持的操作系统

* Linux CentOS 6.3 64位

硬件要求

* 3.2GHz英特尔®奔腾® 4处理器(建议采用双英特尔至强®或更高速的处理器)

* 64位操作系统：4GB RAM（建议使用8GB）

* 硬盘

（磁盘 — SAS）：最低10 GB，7.5K RPM

（磁盘 — 固态硬盘）：400 MBps读/写速度

(NAS)：1 GB专用链路

软件要求

* oracleJava SE 1.8或更高版本

### Adobe Primetime Offline Packager 2.3.1 {#adobe-primetime-offline-packager-1}

1. 从以下位置下载Java SE软件： [oracle站点](https://www.oracle.com/technetwork/java/javase/downloads/index.html) 并按照安装说明操作。
1. 解压缩Adobe Primetime Offline Packager 2.3.1存档文件（名为） `PrimetimeOfflinePackager-2-3-1-b47-10142016.zip` 到磁盘。

### 配置Offline Packager 2.3.1 {#configuring-the-offline-packager}

有关配置说明，请参阅Primetime Offline Packager入门指南，网址为 [https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)

## Primetime Offline Packager 2.1的新增功能（2015年7月） {#what-s-new-in-primetime-offline-packager-july}

支持PlayReady BuyDRM（用于DASH）。 有关详细信息，请参阅帮助文档 [此处提供](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html).

对脱机打包程序进行了以下增强。

PTPUB-780添加了对EXT-X-START标记的支持

## Primetime Offline Packager 2.0的新增功能（2015年6月） {#what-s-new-in-primetime-offline-packager-june}

添加了清除DASH输出支持。 请参阅产品文档 [此处](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html) 以了解详细信息。

此版本中还修复了以下问题。

* PTPUB-783 Offline Packager现在可以处理空WebVTT文件。
* PTPUB- 781某些转码的MP4资源与离线打包程序打包以生成MBR输出时，Chrome上的HLS输出中的工件。

## Adobe Primetime Offline Packager 2.1 {#adobe-primetime-offline-packager-2}

### 最低系统要求 {#minimum-system-requirements-1}

**支持的操作系统**

* Linux CentOS 6.3 64位

**硬件要求**

* 3.2GHz英特尔®奔腾® 4处理器(建议采用双英特尔至强®或更高速的处理器)

* 64位操作系统：4GB RAM（建议使用8GB）

* 推荐使用1 Gb以太网卡（同时支持多块网卡和10 Gb网卡）

* 硬盘

   * （磁盘 — SAS）：最低10 GB，7.5K RPM
   * （磁盘 — 固态硬盘）：400 MBps读/写速度
   * (NAS)：1 GB专用链路

**软件要求**

* oracleJava SE 1.8或更高版本

### 安装Offline Packager 2.1 {#installing-offline-packager}

1. 从以下位置下载Java SE软件： [oracle站点](https://www.oracle.com/technetwork/java/javase/downloads/index.html) 并按照安装说明操作。
1. 提取 `Adobe Primetime - Offline Packager 2.1.0 archive file, PrimetimeOfflinePackager-2-1-0-b15-07082015.zip`，复制到您的磁盘。

### 配置脱机打包程序2.1 {#configuring-the-offline-packager-1}

有关此处提供的配置详细信息，请参阅Primetime Offline Packager快速入门文档 [https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)

## 有用资源 {#helpful-resources}

* 请参阅完整的帮助文档，网址为 [Adobe Primetime学习与支持](https://helpx.adobe.com/support/primetime.html) 页面。
