---
description: 当媒体播放器将其当前用户档案切换到新用户档案时，您可以检索有关交换机的信息，包括交换机何时切换、宽度和高度信息，或使用不同比特率的原因。
seo-description: 当媒体播放器将其当前用户档案切换到新用户档案时，您可以检索有关交换机的信息，包括交换机何时切换、宽度和高度信息，或使用不同比特率的原因。
seo-title: 获取有关用户档案开关的信息
title: 获取有关用户档案开关的信息
uuid: e26ad9fb-6c54-450e-ab62-784d9033d214
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---


# 获取有关用户档案交换机的信息{#get-information-about-profile-switch}

当媒体播放器将其当前用户档案切换到新用户档案时，您可以检索有关交换机的信息，包括交换机何时切换、宽度和高度信息，或使用不同比特率的原因。

1. 听`ProfileEvent.PROFILE_CHANGED`事件。

   TVSDK媒体播放器在其自适应比特率切换算法由于网络或机器条件而切换到另一个事件时调度此用户档案。 （当位速率或周期发生变化时。）
1. 发生事件时，检查以下属性以获得有关交换机的信息：

   * `profile`:正在使用的新用户档案的标识符。
   * `time`:发生切换的流时间。
   * `description`:以分号分隔的键／值对字符串形式描述比特率更改的原因。最多包含一个`Reason`和一个`Bitrate`。 如果信息不可用或比特率没有更改，则此字符串为空。

   <table id="table_E400FD9C57FF40CBAC14AF6847CD8301"> 
    <thead> 
      <tr> 
      <th colname="col1" class="entry"> 密钥名称 </th> 
      <th colname="col2" class="entry"> 可能的值 </th> 
      </tr> 
    </thead>
    <tbody> 
      <tr> 
      <td colname="col1"> <span class="codeph"> 原因  </span> </td> 
      <td colname="col2"> 
       <ul id="ul_37DDE3F297634ED6B47DF5D73F969369"> 
       <li id="li_E374B029E1AF40689D70A9D30E057C5B">网络适应 </li> 
       <li id="li_753862EEF1C9474EA8E20C89F5EF5D8D">搜索 </li> 
       <li id="li_EC14923F92CF4D11A47928A8D2DE6D8B">用户档案不受支持 </li> 
       <li id="li_695AB4A89C9D4833AF6D8B6424FC912B">故障转移 </li> 
       </ul> </td> 
      </tr> 
      <tr> 
      <td colname="col1"> <span class="codeph"> 比特率  </span> </td> 
      <td colname="col2"> 
       <ul id="ul_1B49BD90A91147359712E1AFD8877E23"> 
       <li id="li_1C8E593C65D34742B14A8D0EAD43E0A9"> <span class="codeph"> up </span>:比特率增加 </li> 
       <li id="li_B1A00E3985A849B6855E15CF70D79BB8"> <span class="codeph"> 向下 </span>:比特率降低 </li> 
       </ul> </td> 
      </tr> 
    </tbody>
</table>

    以下是返回的“description”字符串：
    
    &quot;
    比特率：:=up；原因：:=网络适配；&quot;
    
    &quot;比特率：:=down；原因：:=故障转移；
    &quot;
    
    * &quot;width&quot;:指示宽度的整数（以像素为单位）。
    * “高度”:以像素为单位指示高度的整数。
    
    >[!NOTE]
    >
    >宽度和高度数据仅在M3U8清单的“RESOLUTION”标记中包含时才可用。如果M3U8中未包含该信息，则宽度和高度属性将设置为0，因为它们不是用户档案信息的一部分。

<!--<a id="example_A713D420AE2E4E3CB7B78C6BC732BE90"></a>-->

例如：

```
_player.addEventListener(ProfileEvent.PROFILE_CHANGED, onProfileChange); 
private function onProfileChange(event:ProfileEvent):void { 
    _logger.info("#onProfileChange Current profile/bitrate has changed.  
      {0} for reason {1} of resolution [ {2} , {3} ]",  
      event.profile, event.description, event.width, event.height); 
}
```
