---
seo-title: 包装程序属性文件
title: 包装程序属性文件
uuid: 156624ec-66f0-4718-8a66-ed04a47f234d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 包装程序属性文件 {#packager-properties-file}

使用该文 [!DNL flashaccess-refimpl-packager.properties] 件可配置引用实现的监视文件夹打包程序组件。 至少，请务必设置许可证服务器URL、许可证服务器证书、打包程序凭据和密钥保护选项。 此文件还包含每个监视文件夹(packager.watchfolder.source)的位置。 `n`). 对此属性文件中的值所做的任何更改将在下次运行监视的文件夹打包程序时生效（不需要重新启动服务器）。 但是，如果打包程序中存在配置错误，则监视的文件夹打包程序线程将退出，并且需要重新启动服务器以重新启动打包程序线程。
