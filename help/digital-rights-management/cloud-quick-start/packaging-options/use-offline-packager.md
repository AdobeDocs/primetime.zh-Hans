---
title: 使用随附的Primetime Offline Packager
description: 使用随附的Primetime Offline Packager
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# 使用随附的Primetime Offline Packager{#use-the-included-primetime-offline-packager}

您的Primetime Java Packager已预配置打包内容所需的大部分设置。 只有几个区域需要更新才能开始。

## 更新包装程序属性{#section_99904D35E99944A28FF43D924E516CC2}

当前任务的上下文

* 在使用配置文件打包您的内容之前，请更新以下打包程序属性：

### 用户提供的XML配置文件属性

| 属性名称 | 说明 |
|---|---|
| `policy_file` | 策略文件路径。 Adobe应提供若干预先配置的政策供选择。 |
| `pkgr_pfx` | 打包程序凭据路径。 必须在此处提供您自己的Adobe颁发的包装程序凭据([!DNL .pfx])。 |
| `pkgr_pfx_pwd` | 打包程序凭据密码。 必须在此处为Adobe颁发的包装程序凭据提供密码。 |

## 使用命令行{#section_DFBE462679E34D62963BE201FD3321F9}进行打包

在打包内容之前，请确保在配置文件中提供了所有必需的信息。

* 要将内容与配置文件打包，请在命令行中使用以下语法：

```
java -jar OfflinePackager.jar -conf_path [configuration filename]
```

提供了将您的内容打包到HLS或HDS格式的示例配置文件，名为[!DNL config_hds.xml]和[!DNL config.hls.xml]。

HDS或HLS内容将输出到Protection Kit目录下的[!DNL /output]文件夹。 写入此目录的所有对象都必须托管在HTTP Web服务器上才能播放。
