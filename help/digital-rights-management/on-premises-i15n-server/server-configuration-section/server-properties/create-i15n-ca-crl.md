---
title: 创建个性化CA CRL
description: 创建个性化CA CRL
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---


# 创建个性化CA CRL{#create-individualization-ca-crl}

此证书吊销列表(CRL)分发点包含在由个性化服务器颁发的每个计算机证书中。 在许可证服务器上的计算机证书验证过程中，将从证书中列出的分发点下载此CRL（如果已下载，则从缓存中读取），并检查以确保证书未被吊销。

>[!NOTE]
>
>要设置CRL分发点的URL，您需要设置[!DNL AdobeInitial.properties] `cert.machine.crldp`字段。 此分发点由Primetime DRM检查有效性。 **&#x200B;您必须验证此URL是否有效。 在许可证服务器中出现验证错误之前，无效URL导致的错误不会变得明显。

下面简要介绍了使用OpenSSL创建许可证服务器可使用的CRL的示例说明。 Adobe建议您在获得生产个性化CA凭据后，以安全的方式和环境执行这些步骤。

1. 将工作目录更改为此分发中包含的[!DNL create_crl]目录。
1. 将您的个性化CA [!DNL pfx]复制到同一[!DNL create_crl]目录。

   后续步骤假定个性化CA pfx的名称为[!DNL i15n.pfx]。 根据您的设置进行适当调整。
1. 解压CA [!DNL pfx]文件的私钥。

   ```
   openssl pkcs12 -ini15n.pfx -nocerts -out i15n_priv.pem
   ```

1. 将私钥转换为[!DNL pksc8]格式。

   ```
   openssl pkcs8 -topk8 -in i15n_priv.pem -inform pem -out i15n_pk8.pem -outform pem -nocrypt
   ```

1. 生成CRL。

   ```
   openssl ca -keyform pem -keyfile ./i15n_pk8.pem -cert i15n.pem -gencrl  
     -out onprem-individualization -ca.crl
   ```

   此示例创建一个CRL，其默认有效期为1个月。 使用`-crldays`和`-crlhours`选项覆盖默认值。

   生成CRL时使用[!DNL openssl.conf]中指向的[!DNL index]和[!DNL crlnumber]文件。 默认情况下，使用工作目录中的[!DNL demoCA]位置。 示例[!DNL index]和[!DNL crlnumber]文件包含在提供的[!DNL demoCA]目录中。

1. 将上一步中生成的CRL文件部署到许可证服务器可以访问的适当位置(例如：个性化服务器[!DNL ROOT])。
1. CRL到位后，重新启动许可证服务器。
