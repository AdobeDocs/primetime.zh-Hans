---
seo-title: 关于ECI文件
title: 关于ECI文件
uuid: 124d8ab1-933b-4a1b-992a-919f3d799460
translation-type: tm+mt
source-git-commit: d8e4c39c297d69b154baf0b4d67cf09b5cf0a9d4
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---


# 关于ECI文件{#about-eci-files}

除CRL外，您还需要定期更新嵌入式公用接口(ECI)文件。 只要Adobe添加对新Primetime DRM客户端平台的支持(例如：iOS、Android、Windows FlashPlayer等)，将创建新的ECI记录。 为了支持此客户端的个性化，需要在个性化服务器上存在相应的ECI记录。

由于新Primetime DRM客户机的发布并不频繁，Adobe将根据需要发布更新的ECI数据。 Adobe将定期收集ECI文件并将其托管到以下位置进行分发：

```
http://cdmdownload.adobe.com/indiv/onprem/eci/Latest.txt
```

[!DNL Latest.txt]文件将包含最新CRL分发文件的URL。

Adobe将按照如下所述的方式创建ECI zip文件：

文件夹结构：

```
ECI\*
```

文件夹的内容将定期进行压缩：

```
zip -R ECI ECI.zip
```

将计算zip文件的OpenSSL SHA-256摘要：

```
openssl dgst -sha256 -hex ECI.zip
```

zip文件将重命名为包含存档日期和SHA-256摘要：

```
Rename ECI.zip to <DATE_SHA-256>.zip
```

例如：

```
20150310_aea45bf06241f04fba2b310ff9a8066c6aba73c8d22387b60509481e9cefc43e.zip
```

您应定期检查上面的位置，以了解更新的ECI文件。

下载后，请执行以下安装过程：

1. 请注意SHA-256摘要，然后使用OpenSSL或等效工具重新计算它。
1. 将其与文件名中指定的进行比较。
1. 将文件重命名为[!DNL ECI.zip]。
1. 解压缩[!DNL ECI]目录。
1. 将旧ECI目录替换为新目录。
1. 重新启动个性化服务器。

