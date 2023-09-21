---
title: Primetime流服务器版本
description: Primetime Streaming Server 1.3和1.4版本中的新增功能。
products: SG_PRIMETIME
topic-tags: release-notes
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1916'
ht-degree: 0%

---

# Primetime流服务器版本 {#primetime-streaming-server-x-releases}

Primetime Streaming Server 1.3和1.4版本中的新增功能。

## Primetime Streaming Server 1.4的新增功能（12月版） {#what-s-new-in-primetime-streaming-server-december-release}

**Offline Packager**

* 输出HLS流现在包含MPEG-2 TS中存在的ID3元数据
* 仅限HLS音频的流现在可以具有关联的静态图像
* 支持将IV作为HLS AES加密工作流的用户输入
* 支持在脱机打包程序生成IV时将输出IV输出到文件
* 播放列表创建器现在支持将多语言音频组和多语言WebVTT字幕组与媒体流相关联

**原始服务器**

* HLS AES加密可用于Live和VOD工作流。 Primetime Origin可以及时将HLS AES加密应用于传入的HLS流或MP4文件。
* 当它用于将传入的HDS流转换为HLS流时，也可以应用JIT HLS AES加密。
* Primetime Origin现在支持SWF将PHLS流列入允许列表。 以前，仅支持PHDS流

**Primetime Live Packager**

* 支持为输入RTMP和MPEG-2 TS流生成HLS AES-128流

已更新PHDS/PHLS证书。 新到期日将为2016年10月1日。

### **1.4版中包含的错误修复** {#bug-fixes-included-in-release}

* PTPUB-282- OfflinePackager 1.3.1创建的HLS设置级别清单没有编解码器和分辨率信息。
* PTPUB-353 - PlayListCreator不支持在设置级别清单中添加WebVTT信息
* PTPUB-583 - PlaylistCreator工具意外地在组URI的前面加上。
* PTPUB-605播放列表创建程序未在每个变体流中列出SUBTITLE组
* PTPUB-634 -Offline Packager将SpliceInsert添加到清单中。
* PTPUB-635 — 为单个广告提示插入多个SpliceOut标记。

### 1.4版中的已知问题 {#known-issue-in-release}

* PTPUB- 645 DPISimple Mode强制执行，即使在命令行提示和流内提示均以脱机打包程序配置提供的情况下指定了DPIScte35模式

## Primetime Streaming Server 1.3.1的新增功能（5月版） {#what-s-new-in-primetime-streaming-server-may-release}

版本1.3.1是指修补程序。 以下增强功能使其成为客户的推荐升级，因为它包含针对JIT MP4用例的关键性能增强：

1. 使用DRM在原点上对MP4 JIT m3u8的生成进行性能修复，包括密钥轮替
1. 添加了配置“CopyQueryParamToJITFragmentURIs”，以将查询参数从JIT清单请求复制到生成的片段URI以进行MP4 JIT转换。 有关示例用法，请参阅HTTP源服务器文档
1. 通过添加到vod.xml的Config/MP4Only配置，允许不带扩展名的MP4文件进行JIT转换

### 1.3.1版中包含的错误修复 {#bug-fixes-included-in-release-1}

* 3759167 — 由于打包时时间戳异常，并非所有SCTE35提示都会将其添加到输出清单。 对SCTE35消息中SpliceInfoSection的TimeSignal中的SpliceTime应用pts_adjustment。

### 1.3.1版中的已知问题 {#known-issues-in-release}

* 3717039 — 当将打包程序配置为生成DPI简单模式提示时，它实际上应该查找特定的信号类型，如接头插入或放置机会，并且只将这些信号转换为简单模式提示。 它应忽略其它类型的信号，如程序启动、网络启动等。

* 3718598 — 当源服务器配置为在启用HSM访问的情况下提供受保护的内容时，后端LunaSA客户端会与HSM模块频繁通信

## Primetime Streaming Server 1.3的新增功能（4月版） {#what-s-new-in-primetime-streaming-server-april-release}

Primetime 1.3版本围绕流内容提供了几项新功能，提高了可用性和安全性。

**Primetime Streaming Server作为Live Packager和源服务器的统一形式**

Primetime Live Packager和Primetime Origin相结合，作为单个组件使用。 此组件可用作打包程序或用作源位置，或者使用组合的功能来打包和托管实时流。

这为这些服务器提供了统一的文件接口，使它们可以轻松地在单个计算机上运行。 它继续提供了灵活性，可以配置为单独的Packager或Origin。

**Beta MPEG — 短划线支持**

Primetime Streaming Server支持MPEG-DASH打包以用于实时和VOD工作流。 Live Packager组件将摄取RTMP或MPEG-2-TS流转换为DASH格式。 原始组件接受DASH流。

对于VOD工作流，离线打包程序组件将MP4和TS资源转换为MPEG-DASH ISOBFF格式。

**实时到VOD转换**

新组件记录服务器现已可用，该服务器支持捕获实时流并存档以进行VOD播放。 它支持创建完整的事件重播以及部分事件的剪辑/高亮。 它可以配置为录制纯音频流、删除广告或录制实时内容。 录制服务器可与Primetime流服务器以及第三方源配合使用。

**Primetime Live Packager中的RTMP到HLS转换**

Primetime Live Packager组件支持从RTMP流创建HLS流。 它还允许将Primetime DRM和Protected Streaming添加到输出HLS流。

**对Primetime Live Packager的传入RTMP流的身份验证**

usermgmt.jar现在随Primetime Live Packager提供，用于在向Primetime Live Packager发送RTMP流时配置使用可信凭据的访问

现在，可以将编码器配置为在向Live Packager发送流时使用用户名/密码。

**用于创建HDS和HLS顶级清单的播放列表创建器工具**

Primetime Offline Packager现在提供了简洁的实用程序PlaylistCreator.jar，可以轻松创建HDS和HLS资产的顶级清单文件。

**附加安全功能，用于合并硬件安全模块**

Primetime Offline Packager现在支持从Hardware Security Module访问Packager凭据证书和公用密钥。

Hardware Security模块为这些机密资产提供了额外的保护。

**改进了VOD打包性能**

已引入几项性能增强功能，以缩短Primetime Offline Packager中夹层资产的打包时间

**改进了JIT MP4打包性能**

Primetime Origin的JIT打包功能中引入了几项性能增强，以处理用户对大型VOD资产库提出的请求。

## Adobe Primetime Streaming Server 1.4 {#adobe-primetime-streaming-server}

### 最低系统要求 {#minimum-system-requirements}

**网络要求**

* 网络应启用多播，以便从编码器将MPEG-TS流发送到Live Packager。 Live Packager还接受来自不需要多播网络的编码器的RTMP流。

**支持的操作系统**

* Linux CentOS 6.3 64位

**硬件要求**

* 3.2GHz英特尔®奔腾® 4处理器(建议采用双英特尔至强®或更高速的处理器)
* 64位操作系统：4GB RAM（建议使用8GB）
* 推荐使用1 Gb以太网卡（同时支持多块网卡和10 Gb网卡）
* 磁盘：

   * （磁盘 — SAS）：最低10 GB，7.5K RPM
   * （磁盘 — 固态硬盘）：400 MBps读/写
   * (NAS) ：1 GB专用链路

**软件要求**

* oracleJava JRE 1.7(推荐：Sun/Oracle热点JVM)。 JConsole访问JMX API需要JDK

### 安装和配置Primetime流服务器 {#install-and-configure-primetime-streaming-server}

**安装流服务器**

1. 从下载Java SE和JDK软件 [oracle站点](https://www.oracle.com/technetwork/java/javase/downloads/index.html) 并按照安装说明操作。
2. 提取Adobe Primetime-Streaming Server 1.4存档文件， `Primetime- StreamingServer-1-4-0-b206-12042014.zip` 到你的光盘。

**启动Primetime流服务器**

要启动流服务器，请从流服务器的根目录中的命令行执行以下命令：\
`$./pss_start.sh`

**将Primetime流服务器配置为Live Packager或HTTP源服务器**

要将流服务器配置为Live Packager或源服务器，请更新位于流服务器根目录下conf目录下的pss.xml配置文件：

```
<Config> 
<!-- Set this false to disable the Origin Component. --> 
<OriginEnabled&gt;true&lt;/OriginEnabled>  
<!-- Set this false to disable the Packager Component. -->  
<PackagerEnabled&gt;true&lt;/PackagerEnabled>
</Config>
```

**停止Primetime流服务器**

要停止流服务器，请在流服务器的根目录中执行以下命令：\
`$./pss_stop.sh`

**重新启动Primetime流服务器**

要重新启动流服务器，请停止并启动流服务器。

<!-- 

Comment Type: draft

**Configuring Primetime Streaming Server**

Refer the Primetime Streaming Server Getting Started document for the configuration details available at [https://help.adobe.com/en_US/primetime/platform/primetime_streaming_server.pdf](https://help.adobe.com/en_US/primetime/platform/primetime_streaming_server.pdf).

-->

**卸载Primetime流服务器**

要卸载流服务器，请停止流服务器并删除Primetime目录中的流服务器的pss目录

## 使用Live Packager和Origin Server 1.4 {#working-with-live-packager-and-origin-server}

此部分适用于未使用Primetime流服务器，而是部署Primetime Live Packager和/或Primetime源服务器的情况

### 最低系统要求 {#minimum-system-requirements-1}

**网络要求**

* 网络应启用多播，以便从编码器将MPEG-TS流发送到Live Packager。 Live Packager还接受来自不需要多播网络的编码器的RTMP流。

**支持的操作系统**

* Linux CentOS 6.3 64位

**硬件要求**

* 3.2GHz英特尔®奔腾® 4处理器(建议采用双英特尔至强®或更高速的处理器)
* 64位操作系统：4GB RAM（建议使用8GB）
* 推荐使用1 Gb以太网卡（同时支持多块网卡和10 Gb网卡）
* 磁盘：

   * （磁盘 — SAS）：最低10 GB，7.5K RPM
   * （磁盘 — 固态硬盘）：400 MBps读/写
   * (NAS) ：1 GB专用链路

**软件要求**

* oracleJava JRE 1.7(推荐：Sun/Oracle热点JVM)。 JConsole访问JMX API需要JDK

以上最低系统要求对于Origin Server和Live Packager都成立。

### 安装和配置Live Packager {#install-and-configure-the-live-packager}

**安装Live Packager**

1. 从下载Java SE和JDK软件 [oracle站点](https://www.oracle.com/technetwork/java/javase/downloads/index.html) 并按照安装说明操作。
1. 提取Adobe Primetime - Live Packager 1.4存档文件 `Primetime-LivePackager-1-4-0-b206-12042014.zip` 到你的光盘。

**安装HTTP源服务器**

1. 从下载Java JRE和JDK软件 [oracle站点](https://www.oracle.com/technetwork/java/javase/downloads/index.html) 并按照安装说明操作。
1. 提取Adobe Primetime - HTTP Origin Server 1.4存档文件， `Primetime-HttpOrigin-1-4-0-b206-12042014.zip`，复制到您的磁盘。

**启动Live Packager** 要启动打包程序，请从打包程序的根目录执行以下命令：\
`$packager_start.sh`

**启动HTTP源服务器**

要启动HTTP原始服务器，请从原始服务器的根目录中的命令行执行以下命令：\
`$./origin_start.sh`

**停止Live Packager**

要停止打包程序，请从打包程序的根目录执行以下命令：\
`$packager_stop.sh`

**停止HTTP源服务器**

要停止HTTP源服务器，请在源服务器的根目录中执行以下命令：\
`$./origin_stop.sh`

**重新启动Live Packager**

要重新启动打包程序，请停止并启动打包程序。

**注意**：当打包程序启动时，它会尝试从temp目录中的片段目标初始化引导信息。 如果在片段目标上找到引导程序信息，则表示打包程序已重新启动。 如果重新启动，打包程序将等待下一个片段边界，然后开始打包。 打包器在引导中插入一个间隙条目，以指示缺少片段。

**重新启动HTTP源服务器**

要重新启动HTTP源服务器，请停止并启动HTTP源服务器。

**配置Live Packager**

分发文件包含一个示例配置，可用于测试打包程序。

解压缩Adobe Primetime - Live Packager 1.4归档文件后，将目录更改为packager目录，然后运行packager_start.sh脚本。 示例配置侦听多播地址239.235.0.3：14000，并在端口8080上运行本地源服务器。 输出配置为写入 `packager/webroot/_default_/_default_/ directory`.

<!-- 

Comment Type: draft

For more details about the configuration refer [the Primetime Live Packager document](https://help.adobe.com/en_US/primetime/api/packagers/index.html).

-->

**配置HTTP源服务器**

有关此处提供的配置详细信息，请参阅Primetime HTTP源服务器入门文档。

**卸载Live Packager**

要卸载打包程序，请停止打包程序并从Primetime目录中删除打包程序目录。

**卸载HTTP源服务器**

要卸载HTTP源服务器，请停止HTTP源服务器并删除Primetime目录中的HTTP源服务器的httporigin目录。

## Adobe Primetime Offline Packager 1.4 {#adobe-primetime-offline-packager}

### 最低系统要求 {#minimum-system-requirements-2}

**支持的操作系统**

* Linux CentOS 6.3 64位

**硬件要求**

* 3.2GHz英特尔®奔腾® 4处理器(建议采用双英特尔至强®或更高速的处理器)
* 64位操作系统：4GB RAM（建议使用8GB）
* 推荐使用1 Gb以太网卡（同时支持多块网卡和10 Gb网卡）
* 磁盘：

   * （磁盘 — SAS）：最低10 GB，7.5K RPM
   * （磁盘 — 固态硬盘）：400 MBps读/写
   * (NAS) ：1 GB专用链路

**软件要求**

* oracleJava JRE 1.7或更高版本。

### 安装和配置Offline Packager {#install-and-configure-offline-packager}

要安装Offline Packager，请执行以下步骤：

1. 从以下位置下载Java SE软件： [oracle站点](https://www.oracle.com/technetwork/java/javase/downloads/index.html) 并按照安装说明操作。
1. 提取Adobe Primetime - Offline Packager 1.4存档文件， `Primetime- OfflinePackager-1-4-0-b206-12042014.zip`，复制到您的磁盘。

有关可用的配置详细信息，请参阅Primetime Offline Packager快速入门文档 [此处](https://help.adobe.com/en_US/primetime/api/packagers/offline/index.html).

## 有用资源 {#helpful-resources}

* 请参阅完整的帮助文档，网址为 [Adobe Primetime学习与支持](https://helpx.adobe.com/support/primetime.html) 页面。
