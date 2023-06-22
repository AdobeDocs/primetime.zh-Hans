---
title: 关于ECI文件
description: 关于ECI文件
copied-description: true
exl-id: ac452897-3c64-4481-a3b7-4b69ef6edb61
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# 关于ECI文件{#about-eci-files}

除了CRL之外，您还需要定期更新嵌入式公共接口(ECI)文件。 每当Adobe添加对新的Primetime DRM客户端平台(例如：iOS、Android、Windows FlashPlayer等)的支持时，都会创建新的ECI记录。 为了支持此客户端的个性化，个性化服务器上需要存在相应的ECI记录。

由于新的Primetime DRM客户端的发布不太频繁，因此Adobe将根据需要发布更新的ECI数据。 Adobe会定期收集ECI文件，并将其托管到以下位置以供分发：

```
http://cdmdownload.adobe.com/indiv/onprem/eci/Latest.txt
```

此 [!DNL Latest.txt] 文件将包含指向最新CRL分发文件的URL。

Adobe将按如下所述的方式创建ECI zip文件：

文件夹结构：

```
ECI\*
```

文件夹的内容将按递归方式压缩：

```
zip -R ECI ECI.zip
```

将针对zip文件计算OpenSSL SHA--256摘要：

```
openssl dgst -sha256 -hex ECI.zip
```

zip文件将重命名以包含存档日期和SHA-256摘要：

```
Rename ECI.zip to <DATE_SHA-256>.zip
```

例如：

```
20150310_aea45bf06241f04fba2b310ff9a8066c6aba73c8d22387b60509481e9cefc43e.zip
```

您应定期检查上述位置是否有更新的ECI文件。

下载后执行以下安装过程：

1. 记下SHA-256摘要，并使用OpenSSL或等效工具重新计算它。
1. 将其与文件名中指定的进行比较。
1. 将文件重命名为 [!DNL ECI.zip].
1. 解压缩 [!DNL ECI] 目录。
1. 将旧的ECI目录替换为新的ECI目录。
1. 重新启动个性化服务器。
