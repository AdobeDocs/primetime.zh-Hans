---
title: 服务器属性参考
description: 服务器属性参考
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 0%

---

# 服务器属性参考{#server-properties-reference}

<!--<a id="section_EC8810492A454BDBA6013FE376360F4E"></a>-->

## 个性化服务器

<table id="table_ats_tk2_jr">  
 <thead> 
  <tr> 
   <th class="entry"> 配置 </th> 
   <th class="entry"> 描述 </th> 
   <th class="entry"> 示例 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> 传输凭据 </td> 
   <td>传输凭据用于解密从客户端收到的请求，并对发回的响应进行签名。 请务必配置 <span class="filepath"> AdobeInitial.properties</span> 使用传输凭据文件的路径以及加密的PKCS12密码适当地生成文件。 </td> 
   <td> 
    <ul id="ul_itx_fl2_jr"> 
     <li id="li_A2E65253F37245268A41E6B9C958C8DF"><span class="codeph"> cert.i15n.transport.file = </span> [包含个性化传输证书和密钥的PKCS12文件] </li> 
     <li id="li_28CDFC0B3D684795AF4708B6D26DF83F"><span class="codeph"> cert.i15n.transport.password =</span> [PKCS12文件的加密密码] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> 个性化CA凭据 </td> 
   <td>个性化服务器使用个性化CA凭据对它颁发的计算机证书进行签名。 请务必配置 <span class="filepath"> AdobeInitial.properties</span> 与I15N CA凭据文件的路径以及加密的PKCS12密码一起进行适当的文件传输。 </td> 
   <td> 
    <ul id="ul_xsj_nl2_jr"> 
     <li id="li_5A770D8A482F41A4A9AB63CA52C2EB90"><span class="codeph"> cert.i15n.ica.file =</span> [包含个性化CA证书和密钥的PKCS12文件] </li> 
     <li id="li_C3C4A2D9AA2A4F86B6DDCFFD9CB55CBB"><span class="codeph"> cert.i15n.ica.password =</span> [PKCS12文件的加密密码] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> 个性化加密凭据 </td> 
   <td> 个性化服务器使用加密凭据来加密需要传输到个性化服务器的敏感文件。 例如，此证书支持许可证迁移，还用于加密个性化服务器的DRM私钥。 </td> 
   <td> 
    <ul id="ul_nbr_kpd_w5"> 
     <li id="li_4226AD6CC85740669DAF467EFD00BBBE"><span class="codeph"> cert.i15n.decryption.file=i15n_transport.pfx</span> </li> 
     <li id="li_F51BDD94F4724FA58CEF9470B6FEE33B"><span class="codeph"> cert.i15n.decryption.password=password</span> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> 内容缓存 </td> 
   <td>这些设置控制个性化服务器下载内容的位置以及内容在磁盘上的缓存位置。 “个性化”服务器将在启动时，按照这些属性指定的频率/时间检查内容服务器中的新内容。 <p>对于内部部署个性化服务器，我们包括一组初始的内容缓存数据。 请务必复制 <i>目录</i> 缓存文件夹（而非缓存文件夹本身）的路径更改为 <span class="filepath"> AdobeInitial.properties</span> <span class="codeph"> contentServer.localDirectory</span> 位置。 </p> </td> 
   <td> 
    <ul id="ul_r4n_1r2_jr"> 
     <li id="li_CA5F562577B04B4A9966EF46E039A137"><span class="codeph"> contentServer.localDirectory =</span> [存储本地内容的目录（通常为tomcat/temp）] </li> 
     <li id="li_9A78FBD6C54D47708226378340B46E8E"><span class="codeph"> contentServer.server =</span> [要联系以获取ECI信息的Web服务器(<i>此版本不支持</i>)] </li> 
     <li id="li_4E7D7F76085D411688B5003E855F860B"><span class="codeph"> contentServer.timeout =</span> [连接超时，以秒为单位] </li> 
     <li id="li_4B751F238A1643A7AC730CD9354887B6"><span class="codeph"> contentServer.pollFrequency =</span> [轮询服务器的频率，以天为单位（最少1天）] </li> 
     <li id="li_8E23C3C6E7EF46B0AFDD7993DE79F142"><span class="codeph"> contentServer.pollTime =</span> [轮询服务器的时间，以自午夜以来的分钟为单位] </li> 
    </ul> <p>请务必阅读此部分 <i>CRL和ECI文件</i> 更新缓存的问题。 </p> </td> 
  </tr> 
  <tr> 
   <td> 个性化CA CRL </td> 
   <td> <p>此证书吊销列表(CRL)分发点包含在由个性化服务器颁发的每个计算机证书中。 在许可证服务器上验证计算机证书期间，将从证书中列出的分发点下载CRL（如果已经下载，则从缓存中读取），并检查以确保证书未被吊销。 建议在完成创建和部署个性化CA CRL的过程后执行此服务器配置更改。 进行任何配置更改后，重新启动个性化服务器。 </p> <p>要设置CRL分发点的URL，您需要设置 <span class="filepath"> AdobeInitial.properties</span> <span class="codeph"> cert.machine.crldp</span> 字段。 </p> </td> 
   <td> 
    <ul id="ul_eq3_lv2_jr"> 
     <li id="li_5E37A9E318D742B6A5E1035120888819"><span class="codeph"> cert.machine.crldp =</span> [CRL分发点] </li> 
    </ul> <p>例如： </p>
    <p> <code>
      cert.machine.crldp__DEV=<span>tps://onprem-individualization.com</span>CRL/onprem-individualization-ca.crl
     </code></p>
     <p>许可证服务器应在处理许可证请求后自动下载此CRL。 </p> <p importance="high">注意：此分发点为 <i>非</i> 由Primetime DRM检查有效性。 您必须验证此URL是否有效。 除非许可证服务器出现验证错误，否则不会显示由无效URL导致的错误。 </p> </td> 
  </tr> 
  <tr> 
   <td> 记录 </td> 
   <td>配置 <span class="filepath"> AdobeInitial.properties</span> 进行必要的日志记录。 </td> 
   <td> 
    <ul id="ul_j1v_kw2_jr"> 
     <li id="li_B60002B33A3042FCBE1F694454966469"><span class="codeph"> adobe.weblogs.loc =</span> [将在其中创建日志文件的目录] </li> 
     <li id="li_2DD4406FBBF047589BAAAE1C9082D8B3"><span class="codeph"> log.Level =</span> [日志中可能显示的最低级别日志消息 <span class="codeph"> [调试 |信息]</span> ] </li> 
     <li id="li_610FAF239A554CE59DAC455174F0CF0A"><span class="codeph"> log.文件名称=</span> [日志文件的前缀。 日期/时间和“.log”扩展名将添加到文件名 </li> 
     <li id="li_1F2913B209BE4A0E8207FAAD052D1764"><span class="codeph"> log.RollInterval =</span> [指定日志滚动的频率。] </li> 
     <li id="li_3F46C15488114BB5B41035F710E7A19F"><span class="codeph"> log.RollSize =</span> [当日志达到此大小时滚动日志(当 <span class="codeph"> 滚动间隔</span> 或 <span class="codeph"> RollSize</span> ，以先达到者为准)] </li> 
     <li id="li_DA32E862F7B0413885DA20633B682484"><span class="codeph"> log.ReportLogging.Enabled =</span>[ [true | false ]指定是否应生成一个单独的文件，其中包含Adobe用于生成个性化报表的数据。] </li> 
     <li id="li_465CC6D81B8A484CBF4E7A39F7AF86AA"><span class="codeph"> log.ReportLogging.FileName =</span> [报告日志文件的前缀。 日期/时间和 <span class="filepath"> .log</span> 扩展名将添加到文件名中。 l<span class="codeph"> og.Level</span> 属性不适用于此日志文件，但 <span class="codeph"> log.RollInterval</span> 和 <span class="codeph"> log.RollSize</span> 可以。] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> 其他 </td> 
   <td></td> 
   <td> 
    <ul id="ul_b3b_g1f_jr"> 
     <li id="li_FACF07CB332D416E91FD34DE48152FAA"><span class="codeph"> deviceinfo.key =</span> [加密的Base64编码密钥，用于在将其包含到计算机令牌中之前HMAC设备信息。 开发/暂存/生产环境的键可以不同，但特定环境中的所有服务器的键必须相同。] </li> 
     <li id="li_B19C77FD6F91496294DBF836A1922EE1"><span class="codeph"> keys.kgs.server =</span> [Key Gen Server的位置（单个主机/端口，表示密钥服务器池）] </li> 
     <li id="li_5DA3C89770804B148EF6FAF01A5AD958"><span class="codeph"> keys.MinQueueSize =</span> [当队列中还有这么多的键时，从KGS获取另一批键] </li> 
     <li id="li_0C2E5F2FDB824182A6BE418B041D2F28"><span class="codeph"> status.Timeout =</span> [状态页将ping KGS以确定它是否可以到达服务器。 如果在指定的时间内未再次收到响应，则会超时。] </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## 密钥生成服务器 {#section_37FA8EEBA258461F8CFA3ADF37714577}

<table id="table_ats_tk2_js"> 
 <thead> 
  <tr> 
   <th class="entry"> 配置 </th> 
   <th class="entry"> 描述 </th> 
   <th class="entry"> 示例 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> 密钥生成 </td> 
   <td></td> 
   <td> 
    <ul id="ul_nlj_ydf_jr"> 
     <li id="li_E4347D572F004BF0B237A662BFE7F3ED"><span class="codeph"> kgs.Threads =</span> [用于生成密钥的线程数（应等于计算机上可用的处理器数）] </li> 
     <li id="li_EDBC2535D48E4A66AEB240DB337187FC"><span class="codeph"> kgs.BatchSize =</span> [每批要生成的键数] </li> 
     <li id="li_07B41546D94F42349103BF8AF4605E14"><span class="codeph"> kgs.KeyDirectory =</span> [存储关键批处理文件的目录] </li> 
     <li id="li_F4962C97DC3D491DA7FAC826E38A4459"><span class="codeph"> kgs.MaxQueueSize =</span> [要生成的最大关键批处理文件数] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> 记录 </td> 
   <td></td> 
   <td> 
    <ul id="ul_kwq_12f_jr"> 
     <li id="li_5E5D34FE5EB44BB898090494C7DDEBD8"><span class="codeph"> adobe.weblogs.loc =</span> [将在其中创建日志文件的目录] </li> 
     <li id="li_0E34CD32CD5E47729B69B50414F93678"><span class="codeph"> log.文件名称=</span> [日志文件的前缀。 日期/时间和 <span class="filepath"> .log</span> 扩展名将添加到文件名] </li> 
     <li id="li_8AB15ACEC39041A2A04C7301154C6EDB"><span class="codeph"> log.Level =</span> [日志中可能显示的最低级别日志消息] </li> 
     <li id="li_A17E84DA3ED243F381FF3A6184A3CAA0"><span class="codeph"> log.RollInterval =</span> [指定日志滚动的频率。] </li> 
     <li id="li_C2B3D111608945DA9D1428BE98D61664"><span class="codeph"> log.RollSize =</span> [当日志达到此大小时滚动日志(当 <span class="codeph"> 滚动间隔</span> 或 <span class="codeph"> RollSize</span> ，以先达到者为准)] </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>
