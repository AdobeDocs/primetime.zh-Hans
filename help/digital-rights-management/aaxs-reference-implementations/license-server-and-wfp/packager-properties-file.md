---
title: 打包程序属性文件
description: 打包程序属性文件
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---


# 包装程序属性文件{#packager-properties-file}

使用[!DNL flashaccess-refimpl-packager.properties]文件配置引用实现的监视文件夹打包程序组件。 至少，请务必设置许可证服务器URL、许可证服务器证书、打包程序凭据和密钥保护选项。 此文件还包含每个监视文件夹(packager.watchfolder.source)的位置。 `n`)。对此属性文件中的值所做的任何更改将在下次运行监视的文件夹打包程序时生效（不需要重新启动服务器）。 但是，如果打包程序中存在配置错误，监视的文件夹打包程序线程将退出，并且需要重新启动服务器以重新启动打包程序线程。
