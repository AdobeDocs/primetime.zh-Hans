---
description: 清单服务器返回M3U8格式的主控播放列表，符合建议的HTTP实时流化标准。 它包含一组可变传输流(TS)，每个流都包含针对不同比特率和格式的相同内容的再现。 Adobe Primetime广告插入添加了EXT-X-MARKER指令标签，客户端视频播放器将对其进行解释。
title: EXT-X-MARKER指令
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 0%

---


# EXT-X-MARKER指令{#ext-x-marker-directive}

清单服务器返回M3U8格式的主控播放列表，符合建议的HTTP实时流化标准。 它包含一组可变传输流(TS)，每个流都包含针对不同比特率和格式的相同内容的再现。 Adobe Primetime广告插入添加了EXT-X-MARKER指令标签，客户端视频播放器将对其进行解释。

有关EXT-X-MARKER标记的详细信息，请参阅[Adobe Primetime HTTP Live Streaming用户档案](https://wwwimages2.adobe.com/content/dam/acom/en/devnet/primetime/PrimetimeHLS_April2014.pdf)。

>[!NOTE]
>
>仅当引导清单服务器URL不包含`pttrackingmode`参数时，此功能才可用。

>[!NOTE]
>
>EXT-X-MARKER标记添加到广告区段，而不是内容区段。

位于[HTTP实时流](https://tools.ietf.org/html/draft-pantos-http-live-streaming-23)的草稿标准描述了变体播放列表的内容和格式。 EXT-X-MARKER标签指示客户端调用回调。 它包含以下组件：

* **在** 项目流的上下文中此回调事件的IDU唯一标识符（字符串）。

* **回** 调事件的TYPEype（字符串）：PodBegin、PodEnd、PrerollPodBegin、PrerollPodEnd或AdBegin

* **DURATIONL** 长度（以秒为单位），它来自包含指令仍然有效的标签的区段的开始。

* **** 可选。必须调用回调时相对于段播放开始的偏移（以秒为单位）。

   * `PodBegin` 和 `PrerollPodBegin` 在DATA属性中包含信标信息，并在区段开始触发。因此，`OFFSET`标签在此处不可用。

   * `AdBegin` 包含DATA属性中的信标信息，并且该区段的开始触发印象标记。因此，`OFFSET`标签在此也不可用。

   * `PodEnd` 和 `PrerollPodEnd` 包含DATA属性中的信标信息，但在当前区段的末尾触发，因为这些标记预期在窗格中最后一个广告的最后区段结束时触发。在这种情况下，将`OFFSET`设置为`<duration of segment>`以指定在当前段的末尾触发信标。

* **DATABase64编** 码的字符串，包含在多次引号中，该字符串包含在调用回调时要传递到应用程序的数据。它包含符合VMAP1.0和VAST3.0规范的广告跟踪信息。

* **国** 家/地区在广告分时段内拼接的广告数。

   仅当TYPE组件设置为PodBegin或PrerollPodBegin时适用。

* **BREAKDURT已填** 写广告分段的总持续时间（以秒为单位）。

   仅当TYPE组件设置为PodBegin或PrerollPodBegin时适用。

构建回调时，请按如下说明解释EXT-X-MARKER组件：

* 当标记包含`OFFSET`时，以相对于该区段中内容播放开始的指定偏移量触发回调。 否则，当区段开始中的内容播放时立即触发回调。
* 使用`DURATION`跟踪广告内容的进度并请求URL以跟踪事件。
* 将`ID`、`TYPE`和`DATA`传递到回调。

使用`PrerollPodBegin`和`PrerollPodEnd`的`TYPE`值确定在实时/线性流中首先播放的TS段。

>[!NOTE]
>
>`PrerollPodBegin`和`PrerollPodEnd`值仅在将前滚广告插入实时流时可用。

清单服务器在以下区段中包括EXT-X-MARKER标记：

* 用于跟踪广告窗格开头的广告片段。
* 广告的第一个部分，用于跟踪广告窗格内单个广告的开始/完整/进度。
* 用于跟踪广告窗格结尾的广告分段中的最后一段。

清单服务器发送一个`VMAP1.0-conformant` XML文档，以跟踪每个广告中断的开始和结束。 它是广告服务器返回的实际VMAP1.0响应的筛选版本，主要包含跟踪事件，如下所示：

```xml
<?xml version="1.0"?> 
<AdTrackingFragments> 
<AdTrackingFragment> 
<vmap:VMAP xmlns:vmap="https://www.iab.net/vmap-1.0" version="1.0"> 
    <vmap:AdBreak breakType="linear" breakId="mypre" timeOffset="start"> 
        <vmap:TrackingEvents> 
            <vmap:Tracking event="breakStart"> 
                https://MyServer.com/breakstart.gif 
            </vmap:Tracking> 
            <vmap:Tracking event="breakEnd"> 
                https://MyServer.com/breakend.gif 
            </vmap:Tracking> 
            <vmap:Tracking event="error"> 
                https://MyServer.com/error.gif 
            </vmap:Tracking> 
        </vmap:TrackingEvents> 
    </vmap:AdBreak> 
</vmap:VMAP> 
</AdTrackingFragment> 
</AdTrackingFragments>
```

对于每个广告创意，清单服务器插入到项目内容中，它会发送一个VAST3.0一致的XML文档来跟踪该广告。 每个XML文档都包含一个描述插入的线性广告创意的`<InLine>`元素，或包装广告（即链接或重定向广告）的`<Wrapper>`元素，以及任何关联的附属广告和扩展。 如果VAST响应包含序列属性，例如当广告是广告窗格的一部分时，文档会包含该属性。 以下是用于跟踪单个广告的VAST3.0一致性XML文档示例：

```xml
<?xml version="1.0"?> 
<AdTrackingFragments> 
<AdTrackingFragment> 
<VAST xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"  
      version="3.0"  
      xsi:noNamespaceSchemaLocation="https://service.videoplaza.com/schema/iab/vast-3.0.xsd"> 
<Ad id="903395"> 
    <InLine> 
      <AdSystem version="1.0">Auditude</AdSystem> 
      <AdTitle/> 
      <Error>https://ad.qa.auditude.com/adserver/?ErrAd1=[ERRORCODE]</Error> 
      <Impression id="urn:aeid:903395">https://ad.qa.auditude.com/adserver/e?type=adimp&amp; 
                 cid=127860991&amp; 
                 z=50183&amp; 
                 a=903395&amp; 
                 s=ef8c51dc&amp; 
                 t=1355309735&amp; 
                 w=100000&amp; 
                 uid=_CxLm0b1SeKD8KXco__5TQ&amp; 
                 l=1355280906&amp; 
                 u=956c3cd141086a1da44dcae8ea4ed14a&amp; 
                 br=1&amp; 
                 sq=1&amp; 
                 pod=id:1,ctype:l,ptype:p,dur:400,lot:8,cpos:1,edur:400,elot:8&amp; 
                 ax=0,0,1720,0/?ContentPosition=[CONTENTPLAYHEAD] 
                               ?Cashcash=[CACHEBUSTING] 
                               ?Asset=[ASSETURI] 
      </Impression> 
      <Creatives> 
        <Creative> 
          <Linear> 
            <Duration>00:00:15</Duration> 
            <TrackingEvents> 
              ... 
              <Tracking event="firstQuartile"> 
                https://ad.qa.auditude.com/adserver/e?type=AD_PROGRESS&amp; 
                  a=903395&amp; 
                  a1=105&amp; 
                  ref=urn:asset:903395:105&amp; 
                  unit=percent&amp; 
                  progress=25&amp; 
                  cid=127860991&amp; 
                  z=50183&amp; 
                  a=903395&amp; 
                  s=ef8c51dc&amp; 
                  t=1355309735&amp; 
                  w=100000&amp; 
                  uid=_CxLm0b1SeKD8KXco__5TQ&amp; 
                  l=1355280906&amp; 
                  u=956c3cd141086a1da44dcae8ea4ed14a&amp; 
                  br=1&amp; 
                  sq=1&amp; 
                  pod=id:1,ctype:l,ptype:p,dur:400,lot:8,cpos:1,edur:400,elot:8&amp; 
                  ax=0,0,1720,0/?ContentPosition=[CONTENTPLAYHEAD] 
                                ?Cashcash=[CACHEBUSTING] 
                                ?Asset=[ASSETURI] 
              </Tracking>                
              <Tracking event="midpoint"> 
                https://ad.qa.auditude.com/adserver/e?type=AD_PROGRESS&amp; 
                  a=903395&amp; 
                  a1=105&amp; 
                  ref=urn:asset:903395:105&amp; 
                  unit=percent&amp; 
                  progress=50&amp; 
                  cid=127860991&amp; 
                  z=50183&amp; 
                  a=903395&amp; 
                  s=ef8c51dc&amp; 
                  t=1355309735&amp; 
                  w=100000&amp; 
                  uid=_CxLm0b1SeKD8KXco__5TQ&amp; 
                  l=1355280906&amp; 
                  u=956c3cd141086a1da44dcae8ea4ed14a&amp; 
                  br=1&amp; 
                  sq=1&amp; 
                  pod=id:1,ctype:l,ptype:p,dur:400,lot:8,cpos:1,edur:400,elot:8&amp; 
                  ax=0,0,1720,0/?ContentPosition=[CONTENTPLAYHEAD] 
                                ?Cashcash=[CACHEBUSTING] 
                                ?Asset=[ASSETURI] 
              </Tracking> 
              <Tracking event="firstQuartile"> 
                https://www.Tweeeen.com/?ContentPosition=[CONTENTPLAYHEAD] 
                                       ?Cashcash=[CACHEBUSTING] 
                                       ?Asset=[ASSETURI] 
              </Tracking> 
              <Tracking event="midpoint"> 
                https://www.Fiftyyyy.com/?ContentPosition=[CONTENTPLAYHEAD] 
                                        ?Cashcash=[CACHEBUSTING] 
                                        ?Asset=[ASSETURI] 
              </Tracking> 
              ... 
            </TrackingEvents> 
            <VideoClicks> 
              <ClickTracking> 
                https://www.MP4-Vid-ClickTrack.com/?ContentPosition=[CONTENTPLAYHEAD] 
                                                  ?Cashcash=[CACHEBUSTING] 
                                                  ?Asset=[ASSETURI] 
              </ClickTracking> 
              <ClickThrough> 
                https://www.cnn.com/?ContentPosition=[CONTENTPLAYHEAD] 
                                   ?Cashcash=[CACHEBUSTING] 
                                   ?Asset=[ASSETURI] 
              </ClickThrough> 
              ... 
            </VideoClicks> 
            <AdParameters>campaign_id=7012</AdParameters> 
            <MediaFiles> 
              ...            
            </MediaFiles> 
          </Linear> 
        </Creative> 
        <Creative> 
          <CompanionAds> 
            <Companion id="103" width="300" height="250"> 
              <StaticResource creativeType="image/jpeg"> 
                https://ad.qa.auditude.com/adserver/c/z=50183; 
                  l=1355280906; 
                  u=956c3cd141086a1da44dcae8ea4ed14a; 
                  uid=_CxLm0b1SeKD8KXco__5TQ; 
                  cid=127860991; 
                  s=ef8c51dc; 
                  t=1355309735; 
                  br=1; 
                  sq=1; 
                  pod=id%3a1%2cctype%3al%2cptype%3ap%2cdur 
                    %3a400%2clot%3a8%2ccpos%3a1%2cedur%3a400%2celot%3a8; 
                  ax=0%2c0%2c1720%2c0; 
                  w=100000; 
                  a=903395; 
                  a1=103/c300x250.jpeg 
              </StaticResource> 
              <CompanionClickThrough> 
                https://ad.qa.auditude.com/adserver/l/a=903395%3Ba1=103 
                  %3Ba2=1%3Bz=50183%3Bl=1355280906%3Bu=956c3cd141086a1da44dcae8ea4ed14a 
                  %3Bcid=127860991%3Bs=ef8c51dc%3Buid=_CxLm0b1SeKD8KXco__5TQ 
                  %3Bt=1355309735%3Bbr=1%3Bsq=1%3Bpod=id%3a1%2cctype%3al%2cptype 
                  %3ap%2cdur%3a400%2clot%3a8%2ccpos%3a1%2cedur%3a400%2celot%3a8 
                  %3Bax=0%2c0%2c1720%2c0 
              </CompanionClickThrough> 
              <AdParameters>campaign_id=7012</AdParameters> 
            </Companion> 
          </CompanionAds> 
        </Creative> 
        ... 
      </Creatives> 
      <Extensions> 
        <Extension type="Behavior"> 
          ... 
        </Extension> 
      </Extensions> 
    </InLine> 
  </Ad> 
  </VAST> 
</AdTrackingFragment> 
</AdTrackingFragments> 
```
