---
title: 创建个性化CA CRL
description: 创建个性化CA CRL
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# 创建个性化CA CRL{#create-individualization-ca-crl}

此证书吊销列表(CRL)分发点包含在由个性化服务器颁发的每个计算机证书中。 在许可证服务器上验证计算机证书期间，将从证书中列出的分发点下载此CRL（如果已经下载，则从缓存中读取），并检查以确保证书未被吊销。

>[!NOTE]
>
>要设置CRL分发点的URL，您需要设置 [!DNL AdobeInitial.properties] `cert.machine.crldp` 字段。 此分发点为 *非* 由Primetime DRM检查有效性。 您必须验证此URL是否有效。 在许可证服务器上出现验证错误之前，由无效URL导致的错误不会变得明显。

下面列出了使用OpenSSL创建您的许可证服务器可以使用的CRL的简化示例说明。 Adobe建议您在获得生产个性化CA凭据后，以安全的方式和环境执行这些步骤。

1. 将工作目录更改为 [!DNL create_crl] 此分发中包含的目录。
1. 复制您的个性化CA [!DNL pfx] 到同一个 [!DNL create_crl] 目录。

   后续步骤假定已命名个性化CA pfx [!DNL i15n.pfx]. 根据您的设置相应进行调整。
1. 提取个性化CA [!DNL pfx] 文件的私钥。

   ```
   openssl pkcs12 -ini15n.pfx -nocerts -out i15n_priv.pem
   ```

1. 将私钥转换为 [!DNL pksc8] 格式。

   ```
   openssl pkcs8 -topk8 -in i15n_priv.pem -inform pem -out i15n_pk8.pem -outform pem -nocrypt
   ```

1. 生成CRL。

   ```
   openssl ca -keyform pem -keyfile ./i15n_pk8.pem -cert i15n.pem -gencrl  
     -out onprem-individualization -ca.crl
   ```

   此示例创建一个默认有效期为1个月的CRL。 使用 `-crldays` 和 `-crlhours` 选项覆盖默认值。

   生成CRL [!DNL index] 和 [!DNL crlnumber] 您在中指向的文件 [!DNL openssl.conf]. 默认情况下， [!DNL demoCA] 使用工作目录中的位置。 示例 [!DNL index] 和 [!DNL crlnumber] 文件包含在提供的 [!DNL demoCA] 目录。

1. 将上一步中生成的CRL文件部署到许可证服务器可访问的适当位置（例如：个性化服务器） [!DNL ROOT])。
1. CRL就绪后，重新启动许可证服务器。
