---
title: "H264 Single Bitrate Low Quality SD для Android | Документация Майкрософт"
description: "Этот раздел содержит общие сведения о предустановке задачи **H264 Single Bitrate Low Quality SD для Android**."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 67d3446d-e3b8-419f-bbf8-e5149c108531
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: af10b703615e35c28038ef5b8e15f3e58e0eecb1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="h264-single-bitrate-low-quality-sd-for-android"></a><span data-ttu-id="b5835-103">H264 Single Bitrate Low Quality SD для Android</span><span class="sxs-lookup"><span data-stu-id="b5835-103">H264 Single Bitrate Low Quality SD for Android</span></span>
<span data-ttu-id="b5835-104">`Media Encoder Standard` определяет набор предустановок кодирования, которые можно использовать при создании заданий кодирования.</span><span class="sxs-lookup"><span data-stu-id="b5835-104">`Media Encoder Standard` defines a set of encoding presets you can use when creating encoding jobs.</span></span> <span data-ttu-id="b5835-105">Можно также использовать `preset name`, чтобы указать, в какой формат нужно закодировать файл мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="b5835-105">You can either use a `preset name` to specify into which format you would like to encode your media file.</span></span> <span data-ttu-id="b5835-106">Или можно создать собственные предустановки в формате JSON или XML (с использованием кодировки UTF-8 или UTF-16).</span><span class="sxs-lookup"><span data-stu-id="b5835-106">Or, you can create your own JSON or XML-based presets (using UTF-8 or UTF-16 encoding.</span></span> <span data-ttu-id="b5835-107">Затем следует передавать пользовательскую предустановку в кодировщик.</span><span class="sxs-lookup"><span data-stu-id="b5835-107">You would then pass the custom preset to the encoder.</span></span> <span data-ttu-id="b5835-108">Список предустановок, поддерживаемых данным кодировщиком `Media Encoder Standard`, приведен в разделе [Предустановки задач для Media Encoder Standard](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b5835-108">For the list of all the preset names supported by this `Media Encoder Standard` encoder, see [Task Presets for Media Encoder Standard](media-services-mes-presets-overview.md).</span></span>  
  
 <span data-ttu-id="b5835-109">В этом разделе показана предустановка `H264 Single Bitrate Low Quality SD for Android` в форматах XML и JSON.</span><span class="sxs-lookup"><span data-stu-id="b5835-109">This topic shows the `H264 Single Bitrate Low Quality SD for Android` preset in XML and JSON format.</span></span>  
  
 <span data-ttu-id="b5835-110">Данная предустановка создает отдельный MP4-файл со скоростью 56 Кбит/с и стереофоническим звуком в формате AAC.</span><span class="sxs-lookup"><span data-stu-id="b5835-110">This preset produces a single MP4 file with a bitrate of 56 kbps, and stereo AAC audio.</span></span> <span data-ttu-id="b5835-111">Чтобы получить дополнительные сведения о профиле, скорости, частоте выборки и т. п. данной предустановки, ознакомьтесь с кодом XML или JSON ниже.</span><span class="sxs-lookup"><span data-stu-id="b5835-111">For detailed information about profile, bitrate, sampling rate, etc. of this preset, examine the XML or JSON defined below.</span></span> <span data-ttu-id="b5835-112">Описание каждого элемента в этих предустановках и его допустимых значений см. в разделе [Схема Media Encoder Standard](media-services-mes-schema.md).</span><span class="sxs-lookup"><span data-stu-id="b5835-112">For explanations of what each element in these presets means, and the valid values for each element, see the [Media Encoder Standard schema](media-services-mes-schema.md) topic.</span></span>  
  
 <span data-ttu-id="b5835-113">XML</span><span class="sxs-lookup"><span data-stu-id="b5835-113">XML</span></span>  
  
```  
<?xml version="1.0" encoding="utf-16"?>  
<Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">  
  <Encoding>  
    <H264Video>  
      <KeyFrameInterval>00:00:05</KeyFrameInterval>  
      <SceneChangeDetection>true</SceneChangeDetection>  
      <H264Layers>  
        <H264Layer>  
          <Bitrate>56</Bitrate>  
          <Width>176</Width>  
          <Height>144</Height>  
          <FrameRate>12/1</FrameRate>  
          <Profile>Baseline</Profile>  
          <Level>2</Level>  
          <BFrames>0</BFrames>  
          <ReferenceFrames>3</ReferenceFrames>  
          <Slices>0</Slices>  
          <AdaptiveBFrame>false</AdaptiveBFrame>  
          <EntropyMode>Cavlc</EntropyMode>  
          <BufferWindow>00:00:05</BufferWindow>  
          <MaxBitrate>56</MaxBitrate>  
        </H264Layer>  
      </H264Layers>  
      <Chapters />  
    </H264Video>  
    <AACAudio>  
      <Profile>HEAACV2</Profile>  
      <Channels>2</Channels>  
      <SamplingRate>48000</SamplingRate>  
      <Bitrate>24</Bitrate>  
    </AACAudio>  
  </Encoding>  
  <Outputs>  
    <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">  
      <MP4Format />  
    </Output>  
  </Outputs>  
</Preset>  
```  
  
 <span data-ttu-id="b5835-114">JSON</span><span class="sxs-lookup"><span data-stu-id="b5835-114">JSON</span></span>  
  
```  
{  
  "Version": 1.0,  
  "Codecs": [  
    {  
      "KeyFrameInterval": "00:00:05",  
      "SceneChangeDetection": true,  
      "H264Layers": [  
        {  
          "Profile": "Baseline",  
          "Level": "2",  
          "Bitrate": 56,  
          "MaxBitrate": 56,  
          "BufferWindow": "00:00:05",  
          "Width": 176,  
          "Height": 144,  
          "ReferenceFrames": 3,  
          "EntropyMode": "Cavlc",  
          "Type": "H264Layer",  
          "FrameRate": "12/1"  
        }  
      ],  
      "Type": "H264Video"  
    },  
    {  
      "Profile": "HEAACV2",  
      "Channels": 2,  
      "SamplingRate": 48000,  
      "Bitrate": 24,  
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
