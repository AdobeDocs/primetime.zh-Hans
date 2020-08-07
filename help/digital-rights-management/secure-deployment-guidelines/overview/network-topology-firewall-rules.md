---
description: '在确定防火墙规则时，请考虑以下类型的URL '
seo-description: '在确定防火墙规则时，请考虑以下类型的URL '
seo-title: 防火墙规则
title: 防火墙规则
uuid: 309b35b5-8c0a-4cd7-9289-b6b035955697
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 0%

---


# 防火墙规则 {#firewall-rules}

在确定防火墙规则时，请考虑以下类型的URL:

## 传入URL {#section_F111526A9DB844CBBF21A3CAE5F50880}

您可以配置外部防火墙，使其仅显示要提供给最终用户的应用程序功能的URL。

外部用户可通过使用外部防火墙访问以下URL:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_bqs_whz_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">根URL </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">用途 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="filepath"> /flashaccess/getServerVersion/v3</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">确定服务器版本。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <ul id="ul_xr4_hdn_44"> 
     <li id="li_8C68877B0FAF427490BF826FB12BE2F2"><span class="filepath"> /flashaccess/authn/v1/*</span> </li> 
     <li id="li_BF44753FF42E40BD911D04996B962188"><span class="filepath"> /flashaccess/authn/v3/*</span> </li> 
     <li id="li_9B633CDDB3844644BD8E3BFE80FD1672"><span class="filepath"> /flashaccess/authn/v4/*</span> </li> 
     <li id="li_01B2E17BF4DB456383FD6E18E9DE28F5"><span class="filepath"> /flashaccess/authn/v5/*</span> </li> 
     <li id="li_096D349CCD7945B387CB80C3E99063C7"><span class="filepath"> /flashaccess/authn/v6/*</span> </li> 
    </ul> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">验证用户身份。 </p> <p>如果您使用Adobe PrimetimeDRM客户端API进行用户身份验证，则必须可以访问此URL。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <ul id="ul_yxs_rdn_44"> 
     <li id="li_4BEB80F46E8D4D0F90F9998AB7FAAEB7"><span class="filepath"> /flashaccess/license/v1/*</span> </li> 
     <li id="li_20DDE5B03284436F9DEF794867AFBC53"><span class="filepath"> /flashaccess/license/v3/*</span> </li> 
     <li id="li_6555F8689FF945338579C58DADC2E36D"><span class="filepath"> /flashaccess/license/v4/*</span> </li> 
     <li id="li_5112283BDCF1457099056733B633FAF1"><span class="filepath"> /flashaccess/license/v5/*</span> </li> 
     <li id="li_F73A570E2C1A45E1BBF21C1468B90D3A"><span class="filepath"> /flashaccess/license/v6/*</span> </li> 
    </ul> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">向最终用户颁发许可证。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <ul id="ul_ibl_5dn_44"> 
     <li id="li_3B984F500F6848EDBBA5ADC570417E34"><span class="filepath"> /flashaccess/sync/v3</span> </li> 
     <li id="li_3204CF10D68C4FDB97E369BD63FA3C2B"><span class="filepath"> /flashaccess/sync/v4</span> </li> 
     <li id="li_2222D27F73D0421396A4F0E18140B3F9"><span class="filepath"> /flashaccess/sync/v5</span> </li> 
     <li id="li_18020B7CE36B4C209F65FF01A00B6737"><span class="filepath"> /flashaccess/sync/v6/*</span> </li> 
    </ul> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">同步请求。 </p> <p>如果在许可证中指定同步要求，则必须可访问此URL。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <ul id="ul_plq_ydn_44"> 
     <li id="li_61F51463E2BF4ABCA4F209754D8A8052"><span class="filepath"> /flashaccess/domain/v3</span> </li> 
     <li id="li_898E849D7EA24045978D35C336AEEAFE"><span class="filepath"> /flashaccess/domain/v4</span> </li> 
     <li id="li_CF7590FDAF694EDF9685434BE8EE10CA"><span class="filepath"> /flashaccess/domain/v5</span> </li> 
     <li id="li_CA73424FDFAA4BD8BBE2C1AD165D2C31"><span class="filepath"> /flashaccess/domain/v6/*</span> </li> 
    </ul> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">注册域。 </p> <p>如果您实施域支持，则必须可访问此URL。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <ul id="ul_btm_c2n_44"> 
     <li id="li_8A0DC38312CB4D3DBD313B3DE089D39E"><span class="filepath"> /flashaccess/dereg/v3</span> </li> 
     <li id="li_5BA24F70381F465F832FF28925B622C1"><span class="filepath"> /flashaccess/dereg/v4</span> </li> 
     <li id="li_C761F14F3C97479CBA5C255739E01A28"><span class="filepath"> /flashaccess/dereg/v5</span> </li> 
     <li id="li_23A8AABE7499488EB61B7ED27CC65098"><span class="filepath"> /flashaccess/dereg/v6/*</span> </li> 
    </ul> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">取消注册域。 </p> <p>如果您实施域支持，则必须可访问此URL。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="filepath"> /flashaccess/headerconversion/v1/*</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">允许客户端将FMRMS 1.x DRM元数据转换为Primetime DRM元数据。 </p> <p>注意： 此URL必须使用SSL(HTTPS)。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="filepath"> /edcws/services/urn:EDCLicenseService/*</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">LiveCycle Rights Management ESWeb服务URL。 如果内容已通过使用FMRMS的早期版本发布，则此URL允许旧客户端连接到服务器。 系统会提示这些客户端升级到Adobe PrimetimeDRM。 </p> <p class="- topic/p ">注意：此URL必须使用SSL(HTTPS)。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="1" class="- topic/entry "> 
    <ul id="ul_382B69AB07204DD596BB375132224D96"> 
     <li id="li_24B4D42BECF8405281C73B782F8E7310"><span class="filepath"> /flashaccess/lreturn/v5</span> </li> 
     <li id="li_6B79563205D1421F89131E650D71E83B"><span class="filepath"> /flashaccess/lreturn/v6</span> </li> 
    </ul> </td> 
   <td colname="2" class="- topic/entry "> <p>退回许可证。 </p> <p> 如果您实施许可证返回支持，则必须可以访问该URL。 </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>内部防火墙应仅允许通过反向代理连接到Primetime DRM许可证服务器，并且仅允许连接到表中的URL。 要提高可伸缩性，请使用HTTP连接反向代理和Primetime DRM。

## 传出URL {#section_FFF9F7BB353149F4A27F8788E9934A48}

传出URL允许许可证服务器从Adobe下载CRL。

以下是可以使用的传出URL的列表:

* `https://crl2.adobe.com/Adobe/FlashAccessRootCA.crl`
* `https://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl`
* `https://crl3.adobe.com/AdobeSystemsIncorporatedFlashAccessRuntime/LatestCRL.crl`
* `https://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl`

