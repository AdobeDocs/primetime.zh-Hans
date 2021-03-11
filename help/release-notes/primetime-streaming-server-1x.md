---
title: Primetime Streaming Server版本
description: Primetime Streaming Server 1.3和1.4版本的新增功能。
products: SG_PRIMETIME
topic-tags: release-notes
translation-type: tm+mt
source-git-commit: b33240bf1b42b80389cd95a7ae4d3f85185a2d32
workflow-type: tm+mt
source-wordcount: '1916'
ht-degree: 0%

---


# Primetime Streaming Server版本{#primetime-streaming-server-x-releases}

Primetime Streaming Server 1.3和1.4版本的新增功能。

## Primetime Streaming Server 1.4（12月版）的新增功能{#what-s-new-in-primetime-streaming-server-december-release}

**Offline Packager**

* 输出HLS流现在包含MPEG-2 TS中存在的ID3元数据
* 仅HLS音频流现在可以具有关联的静态图像
* 支持将IV作为HLS AES加密工作流的用户输入
* 支持在脱机打包程序生成IV时将IV输出到文件
* Playlist Creator现在支持将多语言音频组和多语言WebVTT子标题组与媒体流关联

**来源 Server**

* HLS AES加密可用于实时和VOD工作流。 Primetime来源可以在时间上将HLS AES加密应用到传入的HLS流或MP4文件。
* 在将传入的HDS流转换为HLS流时，它还可以应用JIT HLS AES加密。
* Primetime来源现在支持SWF允许列出PHLS流。 早些时候，仅支持PHDS流

**Primetime Live Packager**

* 支持为输入RTMP和MPEG-2 TS流生成HLS AES-128流

已刷新PHDS/PHLS证书。 同样的新到期日为10/01/2016。

### **版本1.4中包含的错误修复** {#bug-fixes-included-in-release}

* PTPUB-282 — 由OfflinePackager 1.3.1创建的HLS设置级别清单没有编解码器和分辨率信息。
* PTPUB-353 - PlayListCreator不支持在设置级别清单中添加WebVTT信息
* PTPUB-583 - PlaylistCreator工具意外地预留组URI。
* PTPUB-605播放列表创建程序未在每个变体流中列出子标题组
* PTPUB-634 -Offline Packager将SpliceInsert添加到清单。
* PTPUB-635 — 为单个广告提示插入多个SpliceOut标签。

### 版本1.4 {#known-issue-in-release}中的已知问题

* 即使在脱机打包程序配置中同时提供命令行提示和流内提示时指定了DPIScte35模式，也会强制使用PTPUB-645 DPISimple模式

## Primetime Streaming Server 1.3.1（5月版）{#what-s-new-in-primetime-streaming-server-may-release}的新增功能

版本1.3.1指修补程序。 以下增强功能使客户成为推荐的升级，因为它包含针对JIT MP4使用案例的关键性能增强功能：

1. 使用DRM（包括密钥轮替）来源MP4 JIT m3u8生成的性能修复
1. 添加了配置“CopyQueryParamToJITFragmentURI”，以将查询参数从JIT清单请求复制到为MP4 JIT转换生成的片段URI。 有关示例用法，请参阅HTTP来源服务器文档
1. 通过添加到vod.xml的Config/MP4Only配置，允许无扩展的MP4文件进行JIT转换

### 1.3.1版{#bug-fixes-included-in-release-1}中包含的错误修复

* 3759167 — 并非所有SCTE35提示都由于打包时的时间戳异常导致输出清单。 在SCTE35消息中SpliceInfoSection的TimeSignal中对SpliceTime应用pts_adjustment。

### 版本1.3.1 {#known-issues-in-release}中的已知问题

* 3717039 — 当打包程序配置为生成DPI简单模式提示时，它确实应该查找特定的信号类型，如接合插入或放置机会，并仅将这些信号类型转换为简单模式提示。 它应该忽略其它类型的信号，如项目开始、网络开始等。

* 3718598 — 当来源服务器配置为通过启用HSM访问来提供受保护内容时，后端LunaSA客户端会与HSM模块进行频繁通信

## Primetime Streaming Server 1.3（4月版）{#what-s-new-in-primetime-streaming-server-april-release}的新增功能

Primetime 1.3版提供了有关流内容、更出色的可用性和安全性的几项新功能。

**Primetime Streaming Server作为Live Packager和来源 Server的统一形式**

Primetime Live Packager和Primetime来源整合在一起，作为一个组件发挥作用。 此组件可用作Packager或来源，或使用组合的功能打包和托管实时流。

这为这些服务器提供了统一的文件界面，使它们易于在单台计算机上运行。 它继续提供作为单独的包装程序或来源配置的灵活性。

**测试版MPEG-DASH支持**

Primetime Streaming Server支持实时和VOD工作流的MPEG-DASH打包。 Live Packager组件将收录的RTMP或MPEG-2-TS流转换为DASH格式。 来源组件接受DASH流。

对于VOD工作流,Offline Packager组件会将MP4和TS资源转换为MPEG-DASH ISOBFF格式。

**实时到VOD转换**

现在提供了新的组件“录制服务器”，它支持捕获实时流和存档以进行VOD回放。 它支持创建完整事件重放以及部分事件的剪辑/高光。 它可以配置为在实时内容中录制纯音频流、删除广告或存储。 Recording Server可与Primetime Streaming Server及第三方来源配合使用。

**Primetime Live Packager中的RTMP到HLS转换**

Primetime Live Packager组件支持从RTMP流创建HLS流。 它还允许向输出HLS流中添加Primetime DRM和受保护流。

**对传入RTMP流到Primetime Live Packager的身份验证**

现在，Primetime Live Packager随附一个usermgmt.jar，用于在将RTMP流发送到Primetime Live Packager时使用可信凭据配置访问

现在，可以将编码器配置为在向Live Packager发送流时使用用户名/密码。

**用于为HDS和HLS创建顶级清单的PlaylistCreator工具**

Primetime Offline Packager现在提供了一个绝佳的实用程序PlaylistCreator.jar，可轻松创建用于HDS和HLS资产的顶级清单文件。

**包含硬件安全模块的附加安全功能**

Primetime Offline Packager现在支持从硬件安全模块访问Packager凭据证书和公用密钥。

硬件安全模块为这些机密资产提供额外保护。

**改进了VOD打包性能**

为缩短Primetime Offline Packager中夹层资产的打包时间，已经纳入了多项性能增强功能

**改进了JIT MP4打包的性能**

Primetime来源的JIT打包功能已融入多项性能增强功能，以处理用户对大型VOD资源库的请求。

## Adobe Primetime Streaming Server 1.4 {#adobe-primetime-streaming-server}

### 最低系统要求{#minimum-system-requirements}

**网络要求**

* 应启用“网络多播”，以将MPEG-TS流从编码器发送到Live Packager。 Live Packager还接受来自不需要多播网络的编码器的RTMP流。

**支持的操作系统**

* Linux CentOS 6.3 64位

**硬件要求**

* 3.2GHz Intel® Pentium® 4处理器（建议使用双核Intel Xeon®或更快的处理器）
* 64位操作系统：4GB内存（推荐8GB）
* 建议使用1Gb以太网卡（还支持多个网卡和10Gb）
* 磁盘：

   * （磁盘 — SAS）：最少10GB，带7.5K RPM
   * （磁盘 — 固态硬盘）：400MBps读/写
   * (NAS):1 GB专用链接

**软件要求**

* Oracle Java JRE 1.7(建议：Sun/Oracle热点JVM)。 JConsole访问JMX API需要JDK

### 安装和配置Primetime Streaming Server {#install-and-configure-primetime-streaming-server}

**安装流服务器**

1. 从[Oracle站点](https://www.oracle.com/technetwork/java/javase/downloads/index.html)下载Java SE和JDK软件，然后按照安装说明操作。
2. 将Adobe Primetime-Streaming Server 1.4存档文件`Primetime- StreamingServer-1-4-0-b206-12042014.zip`解压到磁盘。

**开始Primetime Streaming Server**

要开始流服务器，请从流服务器根目录中的命令行执行以下命令：\
`$./pss_start.sh`

**将Primetime流服务器配置为Live Packager或HTTP来源服务器**

要将流服务器配置为Live Packager或来源 Server，请更新位于流服务器根目录conf目录中的pss.xml配置文件：

```
<Config> 
<!-- Set this false to disable the Origin Component. --> 
<OriginEnabled&gt;true&lt;/OriginEnabled>  
<!-- Set this false to disable the Packager Component. -->  
<PackagerEnabled&gt;true&lt;/PackagerEnabled>
</Config>
```

**停止Primetime Streaming Server**

要停止流服务器，请在流服务器的根目录中执行以下命令：\
`$./pss_stop.sh`

**重新启动Primetime Streaming Server**

要重新启动Streaming Server，请停止并开始Streaming Server。

<!-- 

Comment Type: draft

**Configuring Primetime Streaming Server**

Refer the Primetime Streaming Server Getting Started document for the configuration details available at [https://help.adobe.com/en_US/primetime/platform/primetime_streaming_server.pdf](https://help.adobe.com/en_US/primetime/platform/primetime_streaming_server.pdf).

-->

**卸载Primetime Streaming Server**

要卸载流服务器，请停止流服务器，并删除Primetime目录中Streaming Server的pss目录

## 使用Live Packager和来源 Server 1.4 {#working-with-live-packager-and-origin-server}

本部分在未使用Primetime Streaming Server，而是正在部署Primetime Live Packager AND/OR Primetime来源服务器时适用

### 最低系统要求{#minimum-system-requirements-1}

**网络要求**

* 应启用“网络多播”，以将MPEG-TS流从编码器发送到Live Packager。 Live Packager还接受来自不需要多播网络的编码器的RTMP流。

**支持的操作系统**

* Linux CentOS 6.3 64位

**硬件要求**

* 3.2GHz Intel® Pentium® 4处理器（建议使用双核Intel Xeon®或更快的处理器）
* 64位操作系统：4GB内存（推荐8GB）
* 建议使用1Gb以太网卡（还支持多个网卡和10Gb）
* 磁盘：

   * （磁盘 — SAS）：最少10GB，带7.5K RPM
   * （磁盘 — 固态硬盘）：400MBps读/写
   * (NAS):1 GB专用链接

**软件要求**

* Oracle Java JRE 1.7(建议：Sun/Oracle热点JVM)。 JConsole访问JMX API需要JDK

上述最低系统要求适用于来源 Server和Live Packager。

### 安装和配置Live Packager {#install-and-configure-the-live-packager}

**安装Live Packager**

1. 从[Oracle站点](https://www.oracle.com/technetwork/java/javase/downloads/index.html)下载Java SE和JDK软件，然后按照安装说明操作。
1. 将Adobe Primetime - Live Packager 1.4存档文件`Primetime-LivePackager-1-4-0-b206-12042014.zip`解压到磁盘中。

**安装HTTP来源服务器**

1. 从[Oracle站点](https://www.oracle.com/technetwork/java/javase/downloads/index.html)下载Java JRE和JDK软件，然后按照安装说明操作。
1. 将Adobe Primetime - HTTP 来源 Server 1.4存档文件`Primetime-HttpOrigin-1-4-0-b206-12042014.zip`解压到磁盘中。

**要开始Live PackagerTo** 开始打包程序，请从打包程序的根目录中执行以下命令：\
`$packager_start.sh`

**开始HTTP来源服务器**

要开始HTTP来源服务器，请从来源服务器根目录的命令行执行以下命令：\
`$./origin_start.sh`

**停止Live Packager**

要停止打包程序，请从打包程序的根目录中执行以下命令：\
`$packager_stop.sh`

**停止HTTP来源服务器**

要停止HTTP来源服务器，请在来源服务器的根目录中执行以下命令：\
`$./origin_stop.sh`

**重新启动Live Packager**

要重新启动打包程序，请停止并开始打包程序。

**注意**:当打包程序开始时，它尝试从临时目录中的片段目标初始化引导信息。如果在片段目标中找到引导信息，则表示已重新启动打包程序。 在重新启动时，打包程序会等到下一个片段边界，然后开始打包。 打包程序在引导中插入一个间隙条目以指示存在缺少片段。

**重新启动HTTP来源服务器**

要重新启动HTTP来源服务器，请停止并开始HTTP来源服务器。

**配置Live Packager**

分发文件包含可用于测试打包程序的示例配置。

解压Adobe Primetime - Live Packager 1.4归档文件后，将目录更改为packager目录，并运行packager_开始.sh脚本。 示例配置监听多播地址239.235.0.3:14000，并在端口8080上运行本地来源服务器。 输出配置为写入`packager/webroot/_default_/_default_/ directory`。

<!-- 

Comment Type: draft

For more details about the configuration refer [the Primetime Live Packager document](https://help.adobe.com/en_US/primetime/api/packagers/index.html).

-->

**配置HTTP来源服务器**

有关此处提供的配置详细信息，请参阅Primetime HTTP来源服务器快速入门文档。

**卸载Live Packager**

要卸载打包程序，请停止打包程序，并从Primetime目录中删除打包程序目录。

**卸载HTTP来源服务器**

要卸载HTTP来源服务器，请停止HTTP来源服务器，并删除Primetime目录中HTTP来源服务器的httporigin目录。

## Adobe Primetime Offline Packager 1.4 {#adobe-primetime-offline-packager}

### 最低系统要求{#minimum-system-requirements-2}

**支持的操作系统**

* Linux CentOS 6.3 64位

**硬件要求**

* 3.2GHz Intel® Pentium® 4处理器（建议使用双核Intel Xeon®或更快的处理器）
* 64位操作系统：4GB内存（推荐8GB）
* 建议使用1Gb以太网卡（还支持多个网卡和10Gb）
* 磁盘：

   * （磁盘 — SAS）：最少10GB，带7.5K RPM
   * （磁盘 — 固态硬盘）：400MBps读/写
   * (NAS):1 GB专用链接

**软件要求**

* Oracle Java JRE 1.7或更高版本。

### 安装和配置Offline Packager {#install-and-configure-offline-packager}

要安装Offline Packager，请执行以下步骤：

1. 从[Oracle站点](https://www.oracle.com/technetwork/java/javase/downloads/index.html)下载Java SE软件，然后按照安装说明操作。
1. 将Adobe Primetime - Offline Packager 1.4存档文件`Primetime- OfflinePackager-1-4-0-b206-12042014.zip`解压到磁盘。

有关[此处](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html)提供的配置详细信息，请参阅Primetime Offline Packager快速入门文档。

## 有用资源{#helpful-resources}

* 请参阅[Adobe Primetime学习和支持](https://helpx.adobe.com/support/primetime.html)页面上的完整帮助文档。