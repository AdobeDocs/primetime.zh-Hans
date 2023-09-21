---
title: Packager属性文件
description: Packager属性文件
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---

# Packager属性文件 {#packager-properties-file}

使用 [!DNL flashaccess-refimpl-packager.properties] 用于配置参考实施的Watched Folder Packager组件的文件。 至少应确保设置许可证服务器URL、许可证服务器证书、打包程序凭据和密钥保护选项。 此文件还包含每个观察文件夹(packager.watchfolder.source)的位置。 `n`). 对此属性文件中的值所做的任何更改将在下次运行观察文件夹打包程序时生效（不需要重新启动服务器）。 但是，如果打包程序中存在配置错误，监视文件夹打包程序线程将退出，并且需要重新启动服务器以重新启动打包程序线程。
