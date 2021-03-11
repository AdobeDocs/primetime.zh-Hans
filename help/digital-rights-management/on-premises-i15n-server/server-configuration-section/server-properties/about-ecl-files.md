---
title: 关于ECI文件
description: 关于ECI文件
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---


# 关于ECI文件{#about-eci-files}

除CRL外，您还需要定期更新嵌入式公用接口(ECI)文件。 每当Adobe添加对新Primetime DRM客户端平台的支持时(例如：iOS、Android、Windows FlashPlayer等)，将创建新的ECI记录。 为了支持此客户端的个性化，需要在个性化服务器上存在相应的ECI记录。

由于新Primetime DRM客户机的发布并不频繁，Adobe将根据需要发布更新的ECI数据。 Adobe将定期收集ECI文件并将其托管到以下位置进行分发：

```
http://cdmdownload.adobe.com/indiv/onprem/eci/Latest.txt
```

[!DNL Latest.txt]文件将包含指向最新CRL分发文件的URL。

Adobe将以下描述的方式创建ECI zip文件：

文件夹结构：

```
ECI\*
```

文件夹的内容将定期压缩：

```
zip -R ECI ECI.zip
```

将计算zip文件的OpenSSL SHA-256摘要：

```
openssl dgst -sha256 -hex ECI.zip
```

将重命名zip文件，使其包含存档日期和SHA-256摘要：

```
Rename ECI.zip to <DATE_SHA-256>.zip
```

例如：

```
20150310_aea45bf06241f04fba2b310ff9a8066c6aba73c8d22387b60509481e9cefc43e.zip
```

您应定期查看上面的位置，了解更新的ECI文件。

下载后，请执行以下安装过程：

1. 请注意SHA-256摘要，然后使用OpenSSL或等效工具重新计算它。
1. 将其与在文件名中指定的进行比较。
1. 将文件重命名为[!DNL ECI.zip]。
1. 解压缩[!DNL ECI]目录。
1. 用新目录替换旧ECI目录。
1. 重新启动个性化服务器。

