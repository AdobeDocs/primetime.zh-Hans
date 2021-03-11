---
description: “受保护流”的Adobe Access Server需要两种类型的配置文件：全局配置文件(flashaccess-global.xml)和每个租户的租户配置文件(flashaccess-tenant.xml)。
title: 配置目录结构
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# 许可证服务器配置文件和配置目录结构{#configuration-directory-structure}

Adobe Access Server for Protected Streaming需要两种类型的配置文件：每个租户的全局配置文件(flashaccess-global.xml)和租户配置文件(flashaccess-tenant.xml)。

在编辑配置文件后，Adobe建议使用随“受保护流”Adobe Access Server提供的实用程序来验证文件的格式是否正确。 有关详细信息，请参阅“[Configuration Validator](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/configuration-validator.md)”。

为避免在配置文件中以明文提供密码，必须加密全局配置文件和租户配置文件中指定的所有密码。 有关加密密码的详细信息，请参阅“[密码剪贴器](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/password-scrambler.md)”。

配置目录具有以下结构：

```
<i class="+ topic ph hi-d="" i "="">
  LicenseServer.ConfigRoot/  
  flashaccess-global.xml  
  pkcs11.cfg (optional)  
  flashaccessserver/  
   libs/ (optional)  
   tenants/  
     
 <i class="+ topic ph hi-d="" i "="">
   tenantname/  
      flashaccess-tenant.xml  
       
  <i class="+ topic ph hi-d="" i "="">
    credential.pfx (optional)  
        
   <i class="+ topic ph hi-d="" i "="">
     packagercert.cer (optional) 
   </i class="+ topic> 
  </i class="+ topic> 
 </i class="+ topic> 
</i class="+ topic>
```

