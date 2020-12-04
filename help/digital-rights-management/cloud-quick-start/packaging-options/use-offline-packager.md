---
seo-title: 使用随附的Primetime Offline Packager
title: 使用随附的Primetime Offline Packager
uuid: 16b535a9-81b5-43bc-9e42-a64eb6649d9a
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# 使用随附的Primetime Offline Packager{#use-the-included-primetime-offline-packager}

Primetime Java Packager预配置了打包内容所需的大多数设置。 只有几个区域需要更新才能开始。

## 更新包装程序属性{#section_99904D35E99944A28FF43D924E516CC2}

当前任务的上下文

* 在使用配置文件打包内容之前，请更新以下打包程序属性：

### 用户提供的XML配置文件属性

| 属性名称 | 说明 |
|---|---|
| `policy_file` | 策略文件路径。 Adobe应提供几种预先配置的政策供选择。 |
| `pkgr_pfx` | 打包程序凭据路径。 您必须在此处提供您自己的Adobe颁发的包装程序凭据([!DNL .pfx])。 |
| `pkgr_pfx_pwd` | 打包程序凭据密码。 必须在此处为Adobe颁发的包装程序凭据提供密码。 |

## 使用命令行{#section_DFBE462679E34D62963BE201FD3321F9}进行打包

在打包内容之前，请确保在配置文件中提供了所有必需的信息。

* 要将内容与配置文件打包，请在命令行上使用以下语法：

```
java -jar OfflinePackager.jar -conf_path [configuration filename]
```

提供了将内容打包为HLS或HDS格式的示例配置文件，名称为[!DNL config_hds.xml]和[!DNL config.hls.xml]。

HDS或HLS内容将输出到保护工具包目录下的[!DNL /output]文件夹。 写入此目录的所有对象都必须托管在HTTP Web服务器上才能播放。
