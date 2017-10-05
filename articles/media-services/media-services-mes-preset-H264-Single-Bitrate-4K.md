---
title: "Предустановка Media Encoder Standard в Azure: H264 Single Bitrate 4K | Документация Майкрософт"
description: "Этот раздел содержит общие сведения о предустановке задачи **H264 Single Bitrate 4K**."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 8e437aea-8193-49a0-9ff2-4fd391c80972
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 64c68363d4ba89e9ebbcaca8ff45d12f771e3a8c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="h264-single-bitrate-4k"></a><span data-ttu-id="621e7-103">H264 Single Bitrate 4K</span><span class="sxs-lookup"><span data-stu-id="621e7-103">H264 Single Bitrate 4K</span></span>
<span data-ttu-id="621e7-104">`Media Encoder Standard` определяет набор предустановок кодирования, которые можно использовать при создании заданий кодирования.</span><span class="sxs-lookup"><span data-stu-id="621e7-104">`Media Encoder Standard` defines a set of encoding presets you can use when creating encoding jobs.</span></span> <span data-ttu-id="621e7-105">Можно также использовать `preset name`, чтобы указать, в какой формат нужно закодировать файл мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="621e7-105">You can either use a `preset name` to specify into which format you would like to encode your media file.</span></span> <span data-ttu-id="621e7-106">Или можно создать собственные предустановки в формате JSON или XML (с использованием кодировки UTF-8 или UTF-16).</span><span class="sxs-lookup"><span data-stu-id="621e7-106">Or, you can create your own JSON or XML-based presets (using UTF-8 or UTF-16 encoding.</span></span> <span data-ttu-id="621e7-107">Затем следует передавать пользовательскую предустановку в кодировщик.</span><span class="sxs-lookup"><span data-stu-id="621e7-107">You would then pass the custom preset to the encoder.</span></span> <span data-ttu-id="621e7-108">Список предустановок, поддерживаемых данным кодировщиком `Media Encoder Standard`, приведен в разделе [Предустановки задач для Media Encoder Standard](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="621e7-108">For the list of all the preset names supported by this `Media Encoder Standard` encoder, see [Task Presets for Media Encoder Standard](media-services-mes-presets-overview.md).</span></span>  
  
 <span data-ttu-id="621e7-109">В этом разделе показана предустановка `H264 Single Bitrate 4K` в форматах XML и JSON.</span><span class="sxs-lookup"><span data-stu-id="621e7-109">This topic shows the `H264 Single Bitrate 4K` preset in XML and JSON format.</span></span>  
  
 <span data-ttu-id="621e7-110">Данная предустановка создает отдельный MP4-файл со скоростью 18 000 Кбит/с и стереофоническим звуком в формате AAC.</span><span class="sxs-lookup"><span data-stu-id="621e7-110">This preset produces a single MP4 file with a bitrate of 18000 kbps, and stereo AAC audio.</span></span> <span data-ttu-id="621e7-111">Чтобы получить дополнительные сведения о профиле, скорости, частоте выборки и т. п. данной предустановки, ознакомьтесь с кодом XML или JSON ниже.</span><span class="sxs-lookup"><span data-stu-id="621e7-111">For detailed information about profile, bitrate, sampling rate, etc. of this preset, examine the XML or JSON defined below.</span></span> <span data-ttu-id="621e7-112">Описание каждого элемента в этих предустановках и его допустимых значений см. в разделе [Схема Media Encoder Standard](media-services-mes-schema.md).</span><span class="sxs-lookup"><span data-stu-id="621e7-112">For explanations of what each element in these presets means, and the valid values for each element, see the [Media Encoder Standard schema](media-services-mes-schema.md) topic.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="621e7-113">Для кодирования в формат 4K необходимы зарезервированные единицы типа "Премиум".</span><span class="sxs-lookup"><span data-stu-id="621e7-113">You should get the Premium reserved unit type with 4K encodes.</span></span> <span data-ttu-id="621e7-114">Дополнительные сведения см. в статье [Масштабирование кодирования](https://azure.microsoft.com/en-us/documentation/articles/media-services-portal-encoding-units).</span><span class="sxs-lookup"><span data-stu-id="621e7-114">For more information, see [How to Scale Encoding](https://azure.microsoft.com/en-us/documentation/articles/media-services-portal-encoding-units).</span></span>  
  
 <span data-ttu-id="621e7-115">XML</span><span class="sxs-lookup"><span data-stu-id="621e7-115">XML</span></span>  
  
```  
<?xml version="1.0" encoding="utf-16"?>  
<Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">  
  <Encoding>  
    <H264Video>  
      <KeyFrameInterval>00:00:02</KeyFrameInterval>  
      <SceneChangeDetection>true</SceneChangeDetection>  
      <H264Layers>  
        <H264Layer>  
          <Bitrate>18000</Bitrate>  
          <Width>3840</Width>  
          <Height>2160</Height>  
          <FrameRate>0/1</FrameRate>  
          <Profile>Auto</Profile>  
          <Level>auto</Level>  
          <BFrames>3</BFrames>  
          <ReferenceFrames>3</ReferenceFrames>  
          <Slices>0</Slices>  
          <AdaptiveBFrame>true</AdaptiveBFrame>  
          <EntropyMode>Cabac</EntropyMode>  
          <BufferWindow>00:00:05</BufferWindow>  
          <MaxBitrate>18000</MaxBitrate>  
        </H264Layer>  
      </H264Layers>  
      <Chapters />  
    </H264Video>  
    <AACAudio>  
      <Profile>AACLC</Profile>  
      <Channels>2</Channels>  
      <SamplingRate>48000</SamplingRate>  
      <Bitrate>128</Bitrate>  
    </AACAudio>  
  </Encoding>  
  <Outputs>  
    <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">  
      <MP4Format />  
    </Output>  
  </Outputs>  
</Preset>  
```  
  
 <span data-ttu-id="621e7-116">JSON</span><span class="sxs-lookup"><span data-stu-id="621e7-116">JSON</span></span>  
  
```  
{  
  "Version": 1.0,  
  "Codecs": [  
    {  
      "KeyFrameInterval": "00:00:02",  
      "SceneChangeDetection": true,  
      "H264Layers": [  
        {  
          "Profile": "Auto",  
          "Level": "auto",  
          "Bitrate": 18000,  
          "MaxBitrate": 18000,  
          "BufferWindow": "00:00:05",  
          "Width": 3840,  
          "Height": 2160,  
          "BFrames": 3,  
          "ReferenceFrames": 3,  
          "AdaptiveBFrame": true,  
          "Type": "H264Layer",  
          "FrameRate": "0/1"  
        }  
      ],  
      "Type": "H264Video"  
    },  
    {  
      "Profile": "AACLC",  
      "Channels": 2,  
      "SamplingRate": 48000,  
      "Bitrate": 128,  
      "Type": "AACAudio"  
    }  
  ],  
  "Outputs": [  
    {  
      "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",  
      "Format": {  
        "Type": "MP4Format"  
      }  
    }  
  ]  
}  
```
