---
description: 清单服务器返回M3U8格式的主控播放列表，符合建议的HTTP实时流标准。 它包含一组变体传输流(TS)，每个流都包含相同内容的演绎版，以供不同的比特率和格式使用。 Adobe Primetime ad insertion添加EXT-X-MARKER指令标记，以供客户端视频播放器解释。
title: EXT-X-MARKER指令
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 0%

---


# EXT-X-MARKER指令 {#ext-x-marker-directive}

清单服务器返回M3U8格式的主控播放列表，符合建议的HTTP实时流标准。 它包含一组变体传输流(TS)，每个流都包含相同内容的演绎版，以供不同的比特率和格式使用。 Adobe Primetime ad insertion添加EXT-X-MARKER指令标记，以供客户端视频播放器解释。

有关EXT-X-MARKER标记的详细信息，请参阅 [Adobe Primetime HTTP实时流配置文件](https://wwwimages2.adobe.com/content/dam/acom/en/devnet/primetime/PrimetimeHLS_April2014.pdf).

>[!NOTE]
>
>仅当引导清单服务器URL不包含 `pttrackingmode` 参数。

>[!NOTE]
>
>EXT-X-MARKER标记会添加到广告区段，而不是内容区段。

标准草案位于 [HTTP实时流](https://tools.ietf.org/html/draft-pantos-http-live-streaming-23) 描述变体播放列表的内容和格式。 EXT-X-MARKER标记指示客户端调用回调。 它包含以下组件：

* **ID** 项目流上下文中此回调事件的唯一标识符（字符串）。

* **类型** 回调事件的类型（字符串）： PodBegin、PodEnd、PrerollPodBegin、PrerollPodEnd或AdBegin

* **持续时间** 从包含指令仍然有效的标记的区段开始算起的时间长度（以秒为单位）。

* **偏移** 可选。 必须调用回调时相对于区段播放开始的偏移（以秒为单位）。

   * `PodBegin` 和 `PrerollPodBegin` 在DATA属性中包含信标信息，并在区段开头触发。 所以 `OFFSET` 标记在此处不可用。

   * `AdBegin` 包含DATA属性中的信标信息，并在该区段开头触发展示标记。 所以 `OFFSET` 标记在此也不可用。

   * `PodEnd` 和 `PrerollPodEnd` 在DATA属性中包含信标信息，但这些信息会在当前区段末尾触发，因为这些标记应在面板中最后一个广告区段的末尾触发。 在这个案例中， `OFFSET` 设置为 `<duration of segment>` 以指定在当前区段结束时触发信标。

* **数据** 包含在双引号中的Base64编码字符串，其中包含要在调用回调时传递到应用程序的数据。 它包含符合VMAP1.0和VAST3.0规范的广告跟踪信息。

* **计数** 将在广告时间拼接的广告数。

   仅在TYPE组件设置为PodBegin或PrerollPodBegin时适用。

* **BREAKDUR** 已填充广告时间的总持续时间（以秒为单位）。

   仅在TYPE组件设置为PodBegin或PrerollPodBegin时适用。

构造回调时，按如下方式解释EXT-X-MARKER组件：

* 当标记包含 `OFFSET`，在相对于该区段中内容播放开始的指定偏移处触发回调。 否则，在该区段中的内容开始播放后立即触发回调。
* 使用 `DURATION` 以跟踪广告内容的进度，并请求用于跟踪事件的URL。
* 通过 `ID`， `TYPE`、和 `DATA` 到回调。

使用 `PrerollPodBegin`、和 `PrerollPodEnd` 值 `TYPE` 决定要在实时/线性流中首先播放哪个TS区段。

>[!NOTE]
>
>此 `PrerollPodBegin`、和 `PrerollPodEnd` 只有在实时流中插入前置式广告时，值才可用。

清单服务器在以下区段中包含EXT-X-MARKER标记：

* 广告时间中的第一个区段，用于跟踪广告面板的开始。
* 广告的第一个区段，用于跟踪广告面板中单个广告的开始/完成/进度。
* 广告时间的最后一个区段，用于跟踪广告面板的结尾。

清单服务器发送 `VMAP1.0-conformant` 用于跟踪每个广告时间的开始和结束的XML文档。 它是广告服务器返回的实际VMAP1.0响应的过滤版本，主要包含如下所示的跟踪事件：

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

对于清单服务器插入到程序内容中的每个广告创意，它会发送一个VAST3.0符合项XML文档来跟踪该广告。 每个XML文档都包含 `<InLine>` 描述插入的线性广告创意的元素，或 `<Wrapper>` 元素（包装广告）（即链接或重定向广告）以及任何关联的伴随广告和扩展名的情况下的元素。 如果VAST响应包含序列属性（例如，当广告是广告面板的一部分时），则文档将包含该属性。 以下是用于跟踪单个广告的VAST3.0-conformant XML文档示例：

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
