---
seo-title: 创建个性化CA CRL
title: 创建个性化CA CRL
uuid: f722f3d1-517f-43e3-b892-f9287527fbe6
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 创建个性化CA CRL{#create-individualization-ca-crl}

此证书撤销列表(CRL)分发点包含在由个性化服务器颁发的每个计算机证书中。 在许可证服务器上的计算机证书验证过程中，将从证书中列出的分发点下载此CRL（如果已下载，则从缓存中读取），并检查以确保证书未被吊销。

>[!NOTE]
>
>要设置CRL分发点的URL，您需要设置字 [!DNL AdobeInitial.properties]`cert.machine.crldp` 段。 Primetime DRM不检 *查此分* 发点的有效性。 您必须验证此URL是否有效。 在从许可证服务器显示验证错误之前，无效URL导致的错误不会变得明显。

下面简要介绍了使用OpenSSL创建许可证服务器可使用的CRL的示例说明。 Adobe建议您在获得Production Indifilization CA凭证后，以安全的方式和环境执行这些步骤。

1. 将工作目录更改为此分 [!DNL create_crl] 发中包含的目录。
1. 将您的个性化CA复 [!DNL pfx] 制到同一 [!DNL create_crl] 目录。

   后续步骤假定将“个性化CA pfx”命名 [!DNL i15n.pfx]。 根据您的设置进行相应调整。
1. 提取个性化CA [!DNL pfx] 文件的私钥。

   ```
   openssl pkcs12 -ini15n.pfx -nocerts -out i15n_priv.pem
   ```

1. 将私钥转换为格 [!DNL pksc8] 式。

   ```
   openssl pkcs8 -topk8 -in i15n_priv.pem -inform pem -out i15n_pk8.pem -outform pem -nocrypt
   ```

1. 生成CRL。

   ```
   openssl ca -keyform pem -keyfile ./i15n_pk8.pem -cert i15n.pem -gencrl  
     -out onprem-individualization -ca.crl
   ```

   此示例创建一个默认有效期为1个月的CRL。 使用和 `-crldays` 选项 `-crlhours` 覆盖默认值。

   生成CRL时，将使 [!DNL index] 用您 [!DNL crlnumber] 中指向的和文件 [!DNL openssl.conf]。 默认情况下， [!DNL demoCA] 使用工作目录中的位置。 示例 [!DNL index] 和文 [!DNL crlnumber] 件包含在提供的目录中 [!DNL demoCA] 。

1. 将上一步中生成的CRL文件部署到许可证服务器可以访问的合适位置(例如：个性化服 [!DNL ROOT]务器)。
1. CRL到位后，重新启动许可证服务器。
