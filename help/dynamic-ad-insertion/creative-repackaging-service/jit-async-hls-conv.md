---
description: CRS提供即时(JIT)和异步重新打包以及HLS到HLS的转换。 重新打包的结果是原始广告创意的HLS格式版本。 CRS将HLS格式化版本放置到内容投放网络(CDN)服务器上供在需要时使用。
seo-description: CRS提供即时(JIT)和异步重新打包以及HLS到HLS的转换。 重新打包的结果是原始广告创意的HLS格式版本。 CRS将HLS格式化版本放置到内容投放网络(CDN)服务器上供在需要时使用。
seo-title: CRS的主要用途
title: CRS的主要用途
uuid: df2caa67-bc94-4146-9b93-14edc060c3d5
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---


# CRS{#main-uses-of-crs}的主要用途

CRS提供即时(JIT)和异步重新打包以及HLS到HLS的转换。 重新打包的结果是原始广告创意的HLS格式版本。 CRS将HLS格式化版本放置到内容投放网络(CDN)服务器上供在需要时使用。

在JIT重新打包Adobe Primetime广告插入在首次遇到非HLS广告创意时开始重新打包过程。 这通常会导致在重新打包过程中失去运行广告的机会。

在异步重新打包时，广告创意会在需要之前进行转码和存储，这样可以消除这些丢失的机会。

在HLS到HLS的转换中，CRS将HLS广告创意重新格式化为适当大小的块，以确保一致的播放。

## 及时重新打包{#section_1BA344F2300B49F291865A7461EDFEAE}

JIT重新打包的顺序如下：

1. 清单服务器获取广告。
1. 如果广告格式为HLS，清单服务器会将广告插入到内容流中。
1. 如果格式不是HLS（例如MP4、FLV或WebM），清单服务器会在CDN服务器上查找转码版本。 如果找到一个，则会将转码广告插入内容流。
1. 如果格式不是HLS，且CDN服务器没有转码版本，清单服务器会将广告传递给CRS,CRS将转码广告创意并将结果存储在CDN服务器上供以后使用。
1. 清单服务器返回不含广告的内容。

## 异步重新打包{#section_ACDFB43FDA4B445CB9F2A107FEB4F2F7}

您可以使用[重新打包API](../creative-repackaging-service/api-repackage.md)中介绍的API对非HLS创意进行预转码，以最大限度地减少印象损失并实现最大化货币化。

## HLS到HLS的转换{#section_877A0E7E8FAF4C2DB086A31C24D53435}

为避免缓冲和延迟，客户端以小块下载视频。 如果区块大小不一致，则播放可能会抖动。 HLS到HLS的转换可确保数据块都具有相同的持续时间（例如，6秒）。

>[!NOTE]
>
>CRS生成HLS版本3，而不管它收到的HLS版本是什么。