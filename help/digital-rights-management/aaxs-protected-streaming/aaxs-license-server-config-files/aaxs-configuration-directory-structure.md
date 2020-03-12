---
description: Adobe Access Server的受保护流需要两种类型的配置文件：全局配置文件(flashaccess-global.xml)和每个租户的租户配置文件(flashaccess-tenant.xml)。
seo-description: Adobe Access Server的受保护流需要两种类型的配置文件：全局配置文件(flashaccess-global.xml)和每个租户的租户配置文件(flashaccess-tenant.xml)。
seo-title: 配置目录结构
title: 配置目录结构
uuid: c6cfc734-6b7c-4502-9bdb-c7aaca156e0e
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 许可证服务器配置文件和配置目录结构 {#configuration-directory-structure}

Adobe Access Server的受保护流需要两种类型的配置文件：每个租户的全局配置文件(flashaccess-global.xml)和租户配置文件(flashaccess-tenant.xml)。

编辑配置文件后，Adobe建议使用随Adobe Access Server for Protected Streaming提供的实用程序验证文件的格式是否正确。 有关详细信息，请参[阅“Configuration Validator](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/configuration-validator.md)”。

为避免在配置文件中以明文形式提供口令，必须在全局配置文件和租户配置文件中指定的所有口令都必须经过加密。 有关加密密码的更多信息，请参阅“[密码剪贴](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/password-scrambler.md)”。

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

