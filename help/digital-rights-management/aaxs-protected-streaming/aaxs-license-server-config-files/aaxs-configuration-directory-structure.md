---
description: Adobe Access Server for Protected Streaming需要两种类型的配置文件，即全局配置文件(flashaccess-global.xml)和每个租户的租户配置文件(flashaccess-tenant.xml)。
title: 配置目录结构
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# 许可证服务器配置文件和配置目录结构 {#configuration-directory-structure}

Adobe Access Server for Protected Streaming需要两种类型的配置文件：全局配置文件(flashaccess-global.xml)和每个租户的租户配置文件(flashaccess-tenant.xml)。

编辑配置文件后，Adobe建议使用随Adobe Access Server for Protected Streaming提供的实用程序来验证文件的格式是否正确。 有关更多信息，请参阅&quot;[配置验证器](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/configuration-validator.md)“。

为了避免在配置文件中以明文形式提供密码，必须对全局配置文件和租户配置文件中指定的所有密码进行加密。 有关加密密码的更多信息，请参阅&quot;[密码加扰器](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/password-scrambler.md)“。

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
