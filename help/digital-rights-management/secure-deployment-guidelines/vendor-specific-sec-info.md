---
description: 您的Adobe PrimetimeDRM解决方案包含操作系统和应用程序服务器。
seo-description: 您的Adobe PrimetimeDRM解决方案包含操作系统和应用程序服务器。
seo-title: 供应商特定的安全信息
title: 供应商特定的安全信息
uuid: 331baa42-5e19-40a5-bc74-0b1a2cb9370e
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---


# 供应商特定安全信息{#vendor-specific-security-information}

您的Adobe PrimetimeDRM解决方案包含操作系统和应用程序服务器。

要查找操作系统和应用程序服务器的供应商特定安全信息，请参阅使用Adobe PrimetimeDRM密钥服务器。

## 操作系统安全信息{#section_53CAD802FCA54C4D8CE0C4E1B3045E52}

保护操作系统时，必须实施操作系统供应商描述的措施。

以下是一些措施：

* 定义和控制用户、角色和权限
* 监视日志和审计跟踪
* 删除不必要的服务和应用程序
* 备份文件

以下是有关Adobe PrimetimeDRM支持的操作系统的一些信息：

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_ugl_kjz_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">操作系统 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">安全资源 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Microsoft® Windows Server® 2008 Enterprise或Standard Edition </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">Windows Server 2008安全指南</i> </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Red Hat® Enterprise Linux® 5.4、5.5和5.6。 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p "><i class="+ topic/ph hi-d/i ">Red Hat Enterprise Linux 5安全指南</i> </p> </td> 
  </tr> 
 </tbody> 
</table>

以下是一些有关最小化操作系统中安全漏洞的方法的信息：

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_whl_kjz_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">项目 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">说明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">安全修补程序 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果供应商安全修补程序和升级不能及时应用，则未授权用户可能获得对应用程序服务器的访问权限的风险增加。 </p> <p>注意： 确保在将安全修补程序应用到生产服务器之前先测试它们。 </p> <p class="- topic/p ">您必须创建策略和过程，以定期检查和安装修补程序。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">病毒防护软件 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">病毒扫描程序可以通过扫描签名或异常行为来识别感染病毒的文件。 </p> <p>扫描程序将其病毒签名保留在文件中，该文件通常存储在本地硬盘上。 新病毒经常被发现，因此您必须确保定期更新此文件。 这样，病毒扫描程序始终可以识别所有当前病毒。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">网络时间协议(NTP) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">为获得正确的操作和法证分析，请准确掌握Primetime DRM服务器和包装程序。 使用安全版NTP在所有连接到Internet的系统上同步Primetime DRM时间。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 应用程序服务器安全信息{#section_22986936F1A547CEAB2D97E9E9D4825C}

保护应用程序服务器时，必须实施服务器供应商描述的度量。

以下是一些措施：

* 使用非明显的管理员用户名
* 禁用不必要的服务
* 保护控制台管理器
* 启用安全Cookie
* 关闭不需要的端口
* 按IP地址或域限制管理接口
* 使用Java™ Security Manager

