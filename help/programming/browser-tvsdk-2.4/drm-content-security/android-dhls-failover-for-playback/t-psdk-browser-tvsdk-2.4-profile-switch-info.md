---
description: 当媒体播放器将其当前配置文件切换到新配置文件时，您可以检索有关该切换器的信息，包括切换时间、宽度和高度信息，或者为何使用不同的比特率。
title: 获取有关配置文件切换的信息
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 0%

---

# 获取有关配置文件切换的信息{#get-information-about-profile-switch}

当媒体播放器将其当前配置文件切换到新配置文件时，您可以检索有关该切换器的信息，包括切换时间、宽度和高度信息，或者为何使用不同的比特率。

1. 聆听 `AdobePSDK.PSDKEventType.PROFILE_CHANGED` 事件。

   当浏览器TVSDK媒体播放器的自适应比特率切换算法因网络或计算机条件而切换至另一个配置文件时，该播放器会调度此事件。 （当比特率或周期改变时。）
1. 发生该事件时，请检查以下属性以了解有关交换机的信息：

   * `profile`：正在使用的新配置文件的标识符。
   * `time`：切换发生的流时间。
   * `description`：以分号分隔的键/值对字符串形式说明比特率更改的原因。 最多包含一个 `Reason` 和一个 `Bitrate`. 如果该信息不可用，或者比特率未发生更改，则此字符串为空。

   <table id="table_E400FD9C57FF40CBAC14AF6847CD8301"> 
    <thead> 
      <tr> 
      <th colname="col1" class="entry"> 键名称 </th> 
      <th colname="col2" class="entry"> 可能值 </th> 
      </tr> 
    </thead>
    <tbody> 
      <tr> 
      <td colname="col1"> <span class="codeph"> 原因 </span> </td> 
      <td colname="col2"> 
        <ul id="ul_37DDE3F297634ED6B47DF5D73F969369"> 
        <li id="li_E374B029E1AF40689D70A9D30E057C5B">网络自适应 </li> 
        <li id="li_753862EEF1C9474EA8E20C89F5EF5D8D">搜寻 </li> 
        <li id="li_EC14923F92CF4D11A47928A8D2DE6D8B">配置文件不受支持 </li> 
        <li id="li_695AB4A89C9D4833AF6D8B6424FC912B">故障转移 </li> 
        </ul> </td> 
      </tr> 
      <tr> 
      <td colname="col1"> <span class="codeph"> 比特率 </span> </td> 
      <td colname="col2"> 
        <ul id="ul_1B49BD90A91147359712E1AFD8877E23"> 
        <li id="li_1C8E593C65D34742B14A8D0EAD43E0A9"> <span class="codeph"> 向上 </span>：比特率增加 </li> 
        <li id="li_B1A00E3985A849B6855E15CF70D79BB8"> <span class="codeph"> 下 </span>：比特率降低 </li> 
        </ul> </td> 
      </tr> 
    </tbody> 
    </table>

   以下是返回的一些示例 `description` 字符串：

   ```
   "Bitrate::=up;Reason::=Network Adaptation;" 
   
   "Bitrate::=down;Reason::=Failover;"
   ```

   * `width`：表示宽度（以像素为单位）的整数。
   * `height`：表示高度的整数（以像素为单位）。

   >[!NOTE]
   >
   >宽度和高度数据仅在包含在以下项中时可用 `RESOLUTION` M3U8清单中的标记。 如果信息未包含在M3U8中，则width和height属性将设置为0，因为它们不是配置文件信息的一部分。
