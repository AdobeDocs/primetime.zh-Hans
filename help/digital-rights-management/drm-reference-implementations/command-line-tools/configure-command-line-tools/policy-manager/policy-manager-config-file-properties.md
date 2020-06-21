---
description: 'null'
keywords: hard stop
seo-description: 'null'
seo-title: 配置属性
title: 配置属性
uuid: 216921d1-a9c1-4650-9dce-c025836986e5
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '1216'
ht-degree: 0%

---


# 配置属性 {#configuration-properties}

<!--<a id="section_20A96CDCC5C340DEAF455C6E300E5712"></a>-->

>[!NOTE]
>
>对于包含的属 `.n`性名 `n` 称，表示一个整数，它以1开始，并为属性的每个实例增加。 For example: `policy.license.customProp.n`.

<table class="+ topic/table " id="table_p3x_54y_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> 属性／命令行选项 </th> 
   <th colname="2" class="- topic/entry entry"> 说明 </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.name</span> <p class="- topic/p "><span class="codeph"> -n策略</span><i class="+ topic/ph hi-d/i ">名称</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 人可读的DRM策略名称。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.requireKeyServer</span> <p class="- topic/p "><span class="codeph"> -keyServer</span> <i class="+ topic/ph hi-d/i ">boolean</i> </p> </td> 
   <td colname="2" class="- topic/entry ">适用以下条件： 
    <ul id="ul_AF4EBD6C19DC4DFAAB4756EF24BAC57D"> 
     <li id="li_6CC48ABF78EC426E9FC51458BD946BC9">如果为true，则需要HTTPS密钥服务器才能将密钥投放到iOS。 </li> 
     <li id="li_63046A4ED7354C1E9E823B475E4AEFF7">如果未指定，则默认值为false。 </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.enforceJailbreak</span> <p class="- topic/p "><span class="codeph"> -enforceJailbreak</span> <i class="+ topic/ph hi-d/i ">boolean</i> </p> </td> 
   <td colname="2" class="- topic/entry "> 对于支持越狱检测的设备（如果为true），在检测到越狱时不允许回放。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.critical</span> <p class="- topic/p "><span class="codeph"> -critical</span> <i class="+ topic/ph hi-d/i ">boolean</i> </p> </td> 
   <td colname="2" class="- topic/entry ">设置DRM策略的重要性： 
    <ul id="ul_63F1994798894233A67AC4F8220AB642"> 
     <li id="li_D05DD9AD70464D6B9DB9DFF95846E589">如果为true，则服务器必须了解DRM策略的所有部分，这表示默认行为。 </li> 
     <li id="li_0211473DAF1F426787CC4A68F47643C6">如果为false，则服务器可以忽略它无法识别的DRM策略属性。 </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chaining.ansymmetric.certfile</span> </td> 
   <td colname="2" class="- topic/entry ">许可证服务器证书，其公钥用于加密增强的许可证链的根 <a href="https://help.adobe.com/en_US/primetime/drm/5.3/protecting_content/index.html#DRM-concept-Enhanced_License_Chaining" class="- topic/xref " format="http" scope="external"> 加密密钥</a>。 此属性指定仅包含证书的文件。 <p>注意：  支持PEM或DER格式。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.chaining.rootKey</span> <p class="- topic/p "><span class="codeph"> -rootKey</span> <i class="+ topic/ph hi-d/i ">root-key</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p>指定增强的许可证链的 <a href="https://help.adobe.com/en_US/primetime/drm/5.3/protecting_content/index.html#DRM-concept-Enhanced_License_Chaining" class="- topic/xref " format="http" scope="external"> 根加密密钥</a>。 如果未指定密钥并且启用了增强许可证链接，则会自动生成随机密钥。 </p> <p>密钥长度必须为16字节，并指定为十六进制值。 十六进制值之间的空格是可选的。 对于更新，命令行选项不可用，属性被忽略。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.url</span> <p class="- topic/p "><span class="codeph"> -domainURL</span> <i class="+ topic/ph hi-d/i ">url</i> </p> </td> 
   <td colname="2" class="- topic/entry ">如果需要域注册， <i>url</i> 将指定域服务器的URL。 对于更新，命令行选项不可用，属性被忽略。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.anonymous</span> <p class="- topic/p "><span class="codeph"> -domainAnon</span> </p> </td> 
   <td colname="2" class="- topic/entry ">指定是否允许匿名域注册。 将属性设置为true或包含此命令行选项以允许匿名访问。 <p>注意： 此选项不能与-domainAuthNS <span class="codeph"> 一起使用</span>。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.domain.authNamespace</span> <p class="- topic/p "><span class="codeph"> -domainAuthNS</span><i class="+ topic/ph hi-d/i ">命名空间</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p>域注册的身份验证命名空间。 如果指定，则客户端需要使用指定颁发机构颁发的用户名和密码进行身份验证。 </p> <p>对于更新，命令行选项不可用，属性被忽略。 </p> <p>注意： 此选项不能与-domainAnon <span class="codeph"> 一起使用</span>。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.analog</span> <p class="- topic/p "><span class="codeph"> -opAnalog</span> <i class="+ topic/ph hi-d/i ">AnalogOption</i> </p> </td> 
   <td colname="2" class="- topic/entry ">支持模拟输出保护约束和以下值： 
    <ul class="- topic/ul " id="ul_h4x_54y_n4"> 
     <li class="- topic/li " id="li_F920EC01159C4231AFBE579D487C8770"><span class="+ topic/ph pr-d/codeph codeph"> NO_PROTECTION</span> </li> 
     <li class="- topic/li " id="li_2DE0494AF8C446EB9E4567915F5E97C3"><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE</span> </li> 
     <li class="- topic/li " id="li_207D2D6256D6423FBDABA7A8627A9B7D"><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_ACP</span> </li> 
     <li class="- topic/li " id="li_E17D944BED5F403FAE94708EE6AE4BBE"><span class="+ topic/ph pr-d/codeph codeph"> USE_IF_AVAILABLE_CGMSA</span> </li> 
     <li class="- topic/li " id="li_66D5A0C8FE154445A522D91EFB05B7ED"><span class="+ topic/ph pr-d/codeph codeph"> 必需</span> </li> 
     <li class="- topic/li " id="li_AF2024F212A249ED99AEECCF3E844A11"><span class="+ topic/ph pr-d/codeph codeph"> 必需_ACP</span> </li> 
     <li class="- topic/li " id="li_FFF9B7DAE77740EE895EC35D1606A527"><span class="+ topic/ph pr-d/codeph codeph"> REQUIRED_CGMSA</span> </li> 
     <li class="- topic/li " id="li_52DED572F3AE495EB6A6450C611B440E"><span class="+ topic/ph pr-d/codeph codeph"> NO_PLAYBACK</span> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -drmBlacklist</span><i class="+ topic/ph hi-d/i ">名称／值对</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p>限制访问受保护内容的DRM客户端。 此选项指定不能使用的DRM模块的列表（块列表）。 </p> <p>该值由逗号分隔的 <span class="codeph"> name=value</span> 对组成，格式如下： </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|release|arch|model|vendor|env|screen|value</span> </p> <p class="- topic/p ">其他名称／值对必须以逗号分隔。 例如， <span class="codeph"> os=Win,release=2.0,arch=32</span>。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeVersionBlacklist.n</span> <p class="- topic/p "><span class="codeph"> -runtimeBlacklist</span> <i class="+ topic/ph hi-d/i ">name/value-pairs</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p>应用程序运行时被限制访问受保护的内容。 此选项指定不能使用的运行时模块的列表（块列表）。 </p> <p>该值由以逗号分隔的 <span class="codeph"> name=value</span> 对组成，格式如下： </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> os|release|application|arch|model|vendor|env|screen|value</span> </p> <p class="- topic/p ">其他名称／值对必须以逗号分隔。 例如， <span class="codeph"> os=Win,application=AIR</span>。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.v1DeviceCapabilities</span> <p class="- topic/p "><span class="codeph"> -devCapabilitiesV1</span><i class="+ topic/ph hi-d/i ">名称／值对</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定访问受保护内容所需的设备功能。 该值由逗号分隔的 <span class="codeph"> name=value</span> 对组成，格式如下： </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> nonUserAccessibleBus|hardwareRootOfTrust=true|false</span> </p> <p class="- topic/p ">例如， <span class="codeph"> nonUserAccessibleBus=false,hardwareRootOfTrust=true</span>。 </p> <p>在更新过程中，您需要应用- <span class="codeph"> devCapabilitiesV1</span> ，而不需要应用其余参数来删除设备功能限制。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.syncFrequency</span> <p class="- topic/p "><span class="codeph"> -sync</span> <i class="+ topic/ph hi-d/i ">name/value-pairs</i> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定客户端向服务器发送同步消息的频率。 </p> <p>如果未设置该属性，则客户端在播放使用DRM策略保护的内容时不会发送同步消息。 该值由以逗号分隔的 <span class="codeph"> name=value</span> 对组成，格式如下： </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph"> 开始|force=numberValue</span> </p> <p class="- topic/p ">以下列表提供了有关这些选项的其他信息： 
     <ul id="ul_a5j_q4t_44"> 
      <li id="li_FD2C0C6DA19E455AA1917A56E09A7F84">（必需） <span class="codeph"> 开始</span> ，指定客户端需要在自上次同步以来的指定分钟内与服务器同步。 </li> 
      <li id="li_9DEBC57385A442C3929AE3D0E3FA8992">（可选） <span class="codeph"> force</span> 是客户端在播放期间需要强制同步消息的概率(0-100)。 </li> 
     </ul>在更新过程中 <span class="codeph"> ，使用</span> -sync（不含其余参数）来删除同步要求。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.useRootLicense</span> </td> 
   <td colname="2" class="- topic/entry ">指示此DRM策略是否具有根许可证。 <p>有关详细信息，请参阅 <a href="https://help.adobe.com/en_US/primetime/drm/5.3/protecting_content/index.html#DRM-concept-Enhanced_License_Chaining" class="- topic/xref " format="http" scope="external"> 增强的许可证链</a>。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.startDate</span> </td> 
   <td colname="2" class="- topic/entry ">内容生效的日期。 您可以应用以下格式之一： 
    <ul id="ul_6610B44D0C16485098F6F45DE3F151D7"> 
     <li id="li_986707D4C6164C44B3CCBE2EEB4C09B6"><span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> <p>例如， <span class="codeph"> 2009-01-31表示</span> 1月31日凌晨12点。 </p> </li> 
     <li id="li_E15B782716124F6EAEFB04D16E5280DB"><span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:sec</span> <p>例如， <span class="codeph"> 2009-01-31-14:30:00表示1月</span> 31日下午2:30。 </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">内容变为无效的日期。 </p> <p>注意： 不能同 <span class="codeph"> 时指定policy.expiration</span> .endDate <span class="codeph"> 和policy.expiration.duration</span> 。 </p> <p>例如，2009-01-31-14:30:00表示内容将于1月31日下午2:30过期。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.expiration.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">内容变为无效的时间（以分钟为单位）。 打包内容的时间开始。 </p> <p>注意： 不能同 <span class="codeph"> 时指定policy.expiration</span> .endDate <span class="codeph"> 和policy.expiration.duration</span> 。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.duration</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">在客户端上缓存许可证的时间（以分钟为单位）。 您可以将此属性设置为0以阻止许可证缓存。 值必须为0或更高。 </p> <p>注意： 不能同 <span class="codeph"> 时指定policy.licenseCaching</span> . <span class="codeph"> duration和policy.licenseCaching.endDate</span> 。 </p> <p class="- topic/p ">此DRM策略设置仅应用于磁盘上的许可证缓存，并且不控制内存缓存的许可证持续时间。 即使未指定持续时间为零的DRM策略，许可证也可以在内存中缓存。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.licenseCaching.endDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">在此日期之后，您不能再缓存许可证。 </p> <p>注意： 不能同 <span class="codeph"> 时指定policy.licenseCaching</span> . <span class="codeph"> duration和policy.licenseCaching.endDate</span> 。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.anonymous</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指示是否允许匿名许可获取。 默认值设置为 <span class="codeph"> false</span>，这意味着需要用户名和密码。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.authNamespace</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果需要用户名和密码，则此属性为用户名指定可选的名称限定符。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">服务器在获取许可证期间使用的自定义名称／值对。 您可以应用以下格式来指定属性： <span class="+ topic/ph pr-d/codeph codeph">policy.customProp.n</span>=<span class="+ topic/ph pr-d/codeph codeph">name</span>=<span class="+ topic/ph pr-d/codeph codeph">value</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.playbackWindow </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">以分钟为单位指定播放窗口。 此值表示在首次播放受保护的内容后许可证的有效时间。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.digital</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">输出保护约束，必须是以下值之一： 
     <ul id="ul_wsb_kfp_fs"> 
      <li id="li_FE012306F22F4F3FB981FE167C7A8B94"><span class="codeph"> NO_PROTECTION</span> </li> 
      <li id="li_A5591DC8983848FE9823C2A261BF7713"><span class="codeph"> USE_IF_AVAILABLE</span> </li> 
      <li id="li_74102C36ADE841C4B9ED71156E0A4C2C"><span class="codeph"> 必需</span> </li> 
      <li id="li_769E15C85B4E4DD48213DBD019D60BA7"><span class="codeph"> NO_PLAYBACK</span> </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.ota</span> </td> 
   <td colname="2" class="- topic/entry ">指定应允许列出的无线(OTA)连接类型。 有效的连接类型包括： 
    <ul id="ul_iz5_4fp_fs"> 
     <li id="li_FB07519EFEFE4B95B3B1F5BFD4DE6591"><span class="codeph"> MIRACAST</span> </li> 
     <li id="li_51E7DE83679F4630B01264407DAD0E84"><span class="codeph"> AIRPLAY</span> </li> 
     <li id="li_D499A0487AAC409CB2CEA6164265D3CF"><span class="codeph"> DLNA</span> </li> 
     <li id="li_4FCC0EC4A0FC48F99A13EC8A1B78D6A1"><span class="codeph"> WIDI</span> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.outputProtection.resolution</span> </td> 
   <td colname="2" class="- topic/entry "> 指定在其中定义基于分辨率的约束的配置文件。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.drmMinSecurityLevel</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定允许DRM模块访问受保护内容的最低安全级别。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> policy.runtimeMinSecurityLevel</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">应用程序运行时模块必须至少具有指定的最低安全级别才能访问受保护的内容。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowedAIRApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">允许列出非Flash应用程序（Adobe AIR、iOS、Android等） 允许播放受保护的内容。 该属性必须使用以下格式： <span class="+ topic/ph pr-d/codeph codeph">PubId</span>[:<span class="+ topic/ph pr-d/codeph codeph">appId</span>[:[<span class="+ topic/ph pr-d/codeph codeph">min</span>]:[<span class="+ topic/ph pr-d/codeph codeph">max</span>]] </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.allowedSWFApplication.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">允许播放受保护内容的SWF应用程序列表。 该属性必须使用以下格式： </p> <p class="- topic/p "> 
     <ul id="ul_EC20F52AD95C4BE3B7F703048A43CDF0"> 
      <li id="li_3E4A47D925C24834A2C25BC5943279D4"><span class="+ topic/ph pr-d/codeph codeph">URL</span> </li> 
      <li id="li_9A7CAF081C5F488FB5CDA6D38C5552F6"><span class="+ topic/ph pr-d/codeph codeph">file=swf_file</span> </li> 
      <li id="li_E10EA4223137489CBE4015DE999F7154"><span class="codeph">time=max_time_to_verify</span> </li> 
     </ul> <i class="+ topic/ph hi-d/i ">swf_file</i> 是用于计算哈希的SWF文件， <i class="+ topic/ph hi-d/i ">max_time_to_verify</i> 是允许下载和验证SWF以完成的最长时间（秒）。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">向用户颁发许可证时必须包含在许可证中的自定义名称／值对。 您需要指定以下格式： </p> <p class="- topic/p "><span class="+ topic/ph pr-d/codeph codeph">policy.license.customProp.n=name</span> </p> <p class="- topic/p ">您可以多次为多个自定义属性定义此选项。 </p> </td> 
  </tr> 
 </tbody> 
</table>

