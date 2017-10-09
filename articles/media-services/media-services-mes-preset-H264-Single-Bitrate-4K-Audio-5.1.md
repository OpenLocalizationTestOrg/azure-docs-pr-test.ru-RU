---
title: "Односкоростной 4K aaaH264 звук 5.1 | Документы Microsoft"
description: "Hello разделе приводится обзор hello ** Предустановка H264 Односкоростной 4K аудио 5.1* * задачи."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 72cb95ac-2cd6-4ef4-9938-8f22cea04920
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 8ed5d85a0c58eaa9b076be667f4499659d90b19e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="h264-single-bitrate-4k-audio-51"></a><span data-ttu-id="c5ecd-103">H264 Single Bitrate 4K Audio 5.1</span><span class="sxs-lookup"><span data-stu-id="c5ecd-103">H264 Single Bitrate 4K Audio 5.1</span></span>
<span data-ttu-id="c5ecd-104">`Media Encoder Standard` определяет набор предустановок кодирования, которые можно использовать при создании заданий кодирования.</span><span class="sxs-lookup"><span data-stu-id="c5ecd-104">`Media Encoder Standard` defines a set of encoding presets you can use when creating encoding jobs.</span></span> <span data-ttu-id="c5ecd-105">Можно использовать либо `preset name` toospecify в формат, который вы хотите tooencode файла мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="c5ecd-105">You can either use a `preset name` toospecify into which format you would like tooencode your media file.</span></span> <span data-ttu-id="c5ecd-106">Или можно создать собственные предустановки в формате JSON или XML (с использованием кодировки UTF-8 или UTF-16).</span><span class="sxs-lookup"><span data-stu-id="c5ecd-106">Or, you can create your own JSON or XML-based presets (using UTF-8 or UTF-16 encoding.</span></span> <span data-ttu-id="c5ecd-107">Затем следует передавать hello toohello пользовательской предустановки кодировщика.</span><span class="sxs-lookup"><span data-stu-id="c5ecd-107">You would then pass hello custom preset toohello encoder.</span></span> <span data-ttu-id="c5ecd-108">Список всех hello hello предустановленный набор имен, поддерживаемых этим `Media Encoder Standard` кодировщик, см. [предустановки задачи для Media Encoder Standard](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c5ecd-108">For hello list of all hello preset names supported by this `Media Encoder Standard` encoder, see [Task Presets for Media Encoder Standard](media-services-mes-presets-overview.md).</span></span>  
  
 <span data-ttu-id="c5ecd-109">В этом разделе показано hello `H264 Single Bitrate 4K Audio 5.1` конфигурации (в формате XML и JSON).</span><span class="sxs-lookup"><span data-stu-id="c5ecd-109">This topic shows hello `H264 Single Bitrate 4K Audio 5.1` preset (in XML and JSON format).</span></span>  
  
 <span data-ttu-id="c5ecd-110">Данная предустановка создает отдельный MP4-файл со скоростью 18 000 Кбит/с и звуком в формате AAC 5.1.</span><span class="sxs-lookup"><span data-stu-id="c5ecd-110">This preset produces a single MP4 file with a bitrate of 18000 kbps, and AAC 5.1 audio.</span></span> <span data-ttu-id="c5ecd-111">Подробные сведения о профиле скоростью, выборки скорость, т. д. это стиль, проверьте hello XML или JSON, описанные ниже.</span><span class="sxs-lookup"><span data-stu-id="c5ecd-111">For detailed information about profile, bitrate, sampling rate, etc. of this preset, examine hello XML or JSON defined below.</span></span> <span data-ttu-id="c5ecd-112">Для объяснения означает, что каждый элемент и hello допустимые значения для каждого элемента в разделе hello [Media Encoder стандартной схеме](media-services-mes-schema.md).</span><span class="sxs-lookup"><span data-stu-id="c5ecd-112">For explanations of what each element means, and hello valid values for each element, see hello [Media Encoder Standard schema](media-services-mes-schema.md).</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="c5ecd-113">Вы должны получить hello Premium защищены кодирует тип единицы измерения с 4 КБ.</span><span class="sxs-lookup"><span data-stu-id="c5ecd-113">You should get hello Premium reserved unit type with 4K encodes.</span></span> <span data-ttu-id="c5ecd-114">Дополнительные сведения см. в разделе [как tooScale кодировка](https://azure.microsoft.com/en-us/documentation/articles/media-services-portal-encoding-units).</span><span class="sxs-lookup"><span data-stu-id="c5ecd-114">For more information, see [How tooScale Encoding](https://azure.microsoft.com/en-us/documentation/articles/media-services-portal-encoding-units).</span></span>  
  
 <span data-ttu-id="c5ecd-115">XML</span><span class="sxs-lookup"><span data-stu-id="c5ecd-115">XML</span></span>  
  
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
      <Channels>6</Channels>  
      <SamplingRate>48000</SamplingRate>  
      <Bitrate>384</Bitrate>  
    </AACAudio>  
  </Encoding>  
  <Outputs>  
    <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">  
      <MP4Format />  
    </Output>  
  </Outputs>  
</Preset>  
```  
  
 <span data-ttu-id="c5ecd-116">JSON</span><span class="sxs-lookup"><span data-stu-id="c5ecd-116">JSON</span></span>  
  
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
      "Channels": 6,  
      "SamplingRate": 48000,  
      "Bitrate": 384,  
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
