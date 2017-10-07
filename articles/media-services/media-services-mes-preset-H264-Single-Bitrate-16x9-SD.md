---
title: "Стандартный кодировщик мультимедиа Односкоростной 16 x 9 SD Предустановка aaaH264 - Azure | Документы Microsoft"
description: "Hello разделе приводится обзор hello ** задач Предустановка H264 Односкоростной 16 x 9 SD **."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: ce0efc07-3461-44f6-a7bc-c4877bc09529
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: e5fbf6b8accaf779014bee67ee4f5fd6910b2d25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="h264-single-bitrate-16x9-sd"></a><span data-ttu-id="9b5d9-103">H264 Single Bitrate 16x9 SD</span><span class="sxs-lookup"><span data-stu-id="9b5d9-103">H264 Single Bitrate 16x9 SD</span></span>
<span data-ttu-id="9b5d9-104">`Media Encoder Standard` определяет набор предустановок кодирования, которые можно использовать при создании заданий кодирования.</span><span class="sxs-lookup"><span data-stu-id="9b5d9-104">`Media Encoder Standard` defines a set of encoding presets you can use when creating encoding jobs.</span></span> <span data-ttu-id="9b5d9-105">Можно использовать либо `preset name` toospecify в формат, который вы хотите tooencode файла мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="9b5d9-105">You can either use a `preset name` toospecify into which format you would like tooencode your media file.</span></span> <span data-ttu-id="9b5d9-106">Или можно создать собственные предустановки в формате JSON или XML (с использованием кодировки UTF-8 или UTF-16).</span><span class="sxs-lookup"><span data-stu-id="9b5d9-106">Or, you can create your own JSON or XML-based presets (using UTF-8 or UTF-16 encoding.</span></span> <span data-ttu-id="9b5d9-107">Затем следует передавать hello toohello пользовательской предустановки кодировщика.</span><span class="sxs-lookup"><span data-stu-id="9b5d9-107">You would then pass hello custom preset toohello encoder.</span></span> <span data-ttu-id="9b5d9-108">Список всех hello hello предустановленный набор имен, поддерживаемых этим `Media Encoder Standard` кодировщик, см. [предустановки задачи для Media Encoder Standard](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9b5d9-108">For hello list of all hello preset names supported by this `Media Encoder Standard` encoder, see [Task Presets for Media Encoder Standard](media-services-mes-presets-overview.md).</span></span>  
  
 <span data-ttu-id="9b5d9-109">В этом разделе показано hello `H264 Single Bitrate 16x9 SD` конфигурации в формате XML и JSON.</span><span class="sxs-lookup"><span data-stu-id="9b5d9-109">This topic shows hello `H264 Single Bitrate 16x9 SD` preset in XML and JSON format.</span></span>  
  
 <span data-ttu-id="9b5d9-110">Данная предустановка создает отдельный MP4-файл со скоростью 2200 Кбит/с и стереофоническим звуком в формате AAC.</span><span class="sxs-lookup"><span data-stu-id="9b5d9-110">This preset produces a single MP4 file with a bitrate of 2200 kbps, and stereo AAC audio.</span></span> <span data-ttu-id="9b5d9-111">Подробные сведения о профиле скоростью, выборки скорость, т. д. это стиль, проверьте hello XML или JSON, описанные ниже.</span><span class="sxs-lookup"><span data-stu-id="9b5d9-111">For detailed information about profile, bitrate, sampling rate, etc. of this preset, examine hello XML or JSON defined below.</span></span> <span data-ttu-id="9b5d9-112">Объяснение какие каждого элемента в этих стилей означает и hello допустимые значения для каждого элемента в разделе hello [Media Encoder стандартной схеме](media-services-mes-schema.md) раздела.</span><span class="sxs-lookup"><span data-stu-id="9b5d9-112">For explanations of what each element in these presets means, and hello valid values for each element, see hello [Media Encoder Standard schema](media-services-mes-schema.md) topic.</span></span>  
  
 <span data-ttu-id="9b5d9-113">XML</span><span class="sxs-lookup"><span data-stu-id="9b5d9-113">XML</span></span>  
  
```  
<?xml version="1.0" encoding="utf-16"?>  
<Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">  
  <Encoding>  
    <H264Video>  
      <KeyFrameInterval>00:00:02</KeyFrameInterval>  
      <SceneChangeDetection>true</SceneChangeDetection>  
      <H264Layers>  
        <H264Layer>  
          <Bitrate>2200</Bitrate>  
          <Width>848</Width>  
          <Height>480</Height>  
          <FrameRate>0/1</FrameRate>  
          <Profile>Auto</Profile>  
          <Level>auto</Level>  
          <BFrames>3</BFrames>  
          <ReferenceFrames>3</ReferenceFrames>  
          <Slices>0</Slices>  
          <AdaptiveBFrame>true</AdaptiveBFrame>  
          <EntropyMode>Cabac</EntropyMode>  
          <BufferWindow>00:00:05</BufferWindow>  
          <MaxBitrate>2200</MaxBitrate>  
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
  
 <span data-ttu-id="9b5d9-114">JSON</span><span class="sxs-lookup"><span data-stu-id="9b5d9-114">JSON</span></span>  
  
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
          "Bitrate": 2200,  
          "MaxBitrate": 2200,  
          "BufferWindow": "00:00:05",  
          "Width": 848,  
          "Height": 480,  
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
