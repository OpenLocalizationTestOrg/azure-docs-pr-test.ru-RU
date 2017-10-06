---
title: "aaaPerform advanced кодирования, настроив предустановок MES | Документы Microsoft"
description: "В этом разделе показано, как tooperform advanced кодирования, настроив Media Encoder Стандартная предустановки задачи."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 2a4ade25-e600-4bce-a66e-e29cf4a38369
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: juliako
ms.openlocfilehash: 9caa68fafacaf51f91f0554c5bafe491928d8c77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="perform-advanced-encoding-by-customizing-mes-presets"></a>Настройка предустановок MES для расширенного кодирования 

## <a name="overview"></a>Обзор

В этом разделе показано, как стили toocustomize стандартный кодировщик мультимедиа. Hello [кодирование стандарту Media Encoder с помощью пользовательские стили](media-services-custom-mes-presets-with-dotnet.md) разделе показано, как задача toocreate .NET toouse кодировку, а также заданий, в которой выполняется эта задача. После настройки стиля, задачу кодирования toohello пользовательские стили hello питания. 

>[!NOTE]
>При использовании XML-Предустановка, выполнения убедиться, что порядок hello toopreserve элементов, как показано в ниже примеров XML (например, KeyFrameInterval должны предваряться SceneChangeDetection).
>

В этом разделе приведены hello пользовательские стили, которые выполняют следующие задачи кодирования hello.

## <a name="support-for-relative-sizes"></a>Поддержка относительных размеров

При создании эскизов, не требуется задать tooalways вывода ширину и высоту в пикселях. Можно указать их в процентах в диапазоне hello [1%,..., 100%].

### <a name="json-preset"></a>Предустановка JSON
    "Width": "100%",
    "Height": "100%"

### <a name="xml-preset"></a>Предустановка XML
    <Width>100%</Width>
    <Height>100%</Height>

## <a id="thumbnails"></a>Создание эскизов

В этом разделе показано, как toocustomize предварительной установки, создает эскизы. Hello стиль указанных ниже содержит сведения о способе tooencode файле также сведения, необходимые toogenerate эскизы. Может принимать любую из предустановок MES hello задокументированы [это](media-services-mes-presets-overview.md) статьи и добавьте код, который создает эскизы.  

> [!NOTE]
> Hello **SceneChangeDetection** в следующих предустановленных hello можно только установить tootrue Если tooa постоянным битрейтом видео кодируется. Если кодирование выполняется с разными скоростями tooa видео- и задайте **SceneChangeDetection** tootrue, кодировщик hello возвращает сообщение об ошибке.  
>
>

Сведения о схеме см. [здесь](media-services-mes-schema.md).

Убедитесь, что hello tooreview [вопросы](#considerations) раздела.

### <a id="json"></a>Предустановка JSON
    {
      "Version": 1.0,
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "SceneChangeDetection": "true",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 4500,
              "MaxBitrate": 4500,
              "BufferWindow": "00:00:05",
              "Width": 1280,
              "Height": 720,
              "ReferenceFrames": 3,
              "EntropyMode": "Cabac",
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"

            }
          ],
          "Type": "H264Video"
        },
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": 640,
              "Height": 360
            }
          ],
          "Start": "{Best}",
          "Type": "JpgImage"
        },
        {
          "PngLayers": [
            {
              "Type": "PngLayer",
              "Width": 640,
              "Height": 360,
            }
          ],
          "Start": "00:00:01",
          "Step": "00:00:10",
          "Range": "00:00:58",
          "Type": "PngImage"
        },
        {
          "BmpLayers": [
            {
              "Type": "BmpLayer",
              "Width": 640,
              "Height": 360
            }
          ],
          "Start": "10%",
          "Step": "10%",
          "Range": "90%",
          "Type": "BmpImage"
        },
        {
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        },
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "PngFormat"
          }
        },
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "BmpFormat"
          }
        },
        {
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }


### <a id="xml"></a>Предустановка XML
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <SceneChangeDetection>true</SceneChangeDetection>
          <H264Layers>
            <H264Layer>
              <Bitrate>4500</Bitrate>
              <Width>1280</Width>
              <Height>720</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>4500</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <AACAudio>
          <Profile>AACLC</Profile>
          <Channels>2</Channels>
          <SamplingRate>48000</SamplingRate>
          <Bitrate>128</Bitrate>
        </AACAudio>
        <JpgImage Start="{Best}">
          <JpgLayers>
            <JpgLayer>
              <Width>640</Width>
              <Height>360</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
        <BmpImage Start="10%" Step="10%" Range="90%">
          <BmpLayers>
            <BmpLayer>
              <Width>640</Width>
              <Height>360</Height>
            </BmpLayer>
          </BmpLayers>
        </BmpImage>
        <PngImage Start="00:00:01" Step="00:00:10" Range="00:00:58">
          <PngLayers>
            <PngLayer>
              <Width>640</Width>
              <Height>360</Height>
            </PngLayer>
          </PngLayers>
        </PngImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <BmpFormat />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <PngFormat />
        </Output>
      </Outputs>
    </Preset>

### <a name="considerations"></a>Рекомендации

применить Hello следующие вопросы:

* Использование Hello явные отметки времени для начала/шаг или Range предполагается, что этот источник входных hello — менее 1 минуты long.
* Элементы Jpg, Png и BmpImage обладают строковыми атрибутами Start, Step и Range, которые можно интерпретировать следующим образом:

  * номер кадра, если эти атрибуты выражены неотрицательными целыми числами, например "Start": "120";
  * Длительность относительный toosource Если выразить в виде % суффиксом, например «Start»: «% 15», или
  * Отметка времени, если атрибуты имеют формат ЧЧ:ММ:СС, например "Start" : "00:01:00".

    При желании условные обозначения можно комбинировать.

    Кроме того, также поддерживает запуск специального макроса: {наилучшим образом}, который осуществляет toodetermine hello первый «Город» кадр hello содержимого Примечание: (шаг и диапазон игнорируются при начале задано слишком {наиболее})
  * По умолчанию Start:{Best}
* Формат вывода должно явно предоставляться для каждого формата изображения toobe: Jpg, Png или BmpFormat. При наличии MES соответствует JpgVideo tooJpgFormat и т. д. Выходнойформат появился новый указанного макроса кодек изображений: {индекс}, требующие toobe присутствует (один раз и только один раз) для форматов вывода изображения.

## <a id="trim_video"></a>Монтаж видео (обрезка)
Этом разделе рассказывается об изменении кодировщика hello стили tooclip или trim hello входное видео, где hello ввода так называемого мезонинный файл или файл по требованию. Hello кодировщика можно также использовать tooclip или trim активов, который является захвата или архивированных из обновляющегося потока — hello подробные сведения для этого доступны в [этот блог](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).

tootrim видео, можно использовать любой из предустановок MES hello описаны [это](media-services-mes-presets-overview.md) статьи и изменения hello **источников** (как показано ниже). Hello значение StartTime должно toomatch hello абсолютный отметки времени hello входное видео. Например, если hello первый кадр hello входное видео имеет отметку времени, 12:00:10.000, то время начала должно быть по крайней мере 12:00:10.000 и более поздней версии. В следующем примере hello мы предположим, что входные данные hello видео имеет отметку времени начала равно нулю. **Источники** должны размещаться в начале hello Предустановка hello.

### <a id="json"></a>Предустановка JSON
    {
      "Version": 1.0,
      "Sources": [
        {
          "StartTime": "00:00:04",
          "Duration": "00:00:16"
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 3400,
              "MaxBitrate": 3400,
              "BufferWindow": "00:00:05",
              "Width": 1280,
              "Height": 720,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 2250,
              "MaxBitrate": 2250,
              "BufferWindow": "00:00:05",
              "Width": 960,
              "Height": 540,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1500,
              "MaxBitrate": 1500,
              "BufferWindow": "00:00:05",
              "Width": 960,
              "Height": 540,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1000,
              "MaxBitrate": 1000,
              "BufferWindow": "00:00:05",
              "Width": 640,
              "Height": 360,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 650,
              "MaxBitrate": 650,
              "BufferWindow": "00:00:05",
              "Width": 640,
              "Height": 360,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 400,
              "MaxBitrate": 400,
              "BufferWindow": "00:00:05",
              "Width": 320,
              "Height": 180,
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

### <a name="xml-preset"></a>Предустановка XML
tootrim видео, можно использовать любой из предустановок MES hello описаны [здесь](media-services-mes-presets-overview.md) и изменения hello **источников** (как показано ниже).

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Sources>
        <Source StartTime="PT4S" Duration="PT14S"/>
      </Sources>
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <H264Layers>
            <H264Layer>
              <Bitrate>3400</Bitrate>
              <Width>1280</Width>
              <Height>720</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>3400</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>2250</Bitrate>
              <Width>960</Width>
              <Height>540</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>2250</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>1500</Bitrate>
              <Width>960</Width>
              <Height>540</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1500</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>1000</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1000</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>650</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>650</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>400</Bitrate>
              <Width>320</Width>
              <Height>180</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>400</MaxBitrate>
            </H264Layer>
          </H264Layers>
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

## <a id="overlay"></a>Создание наложения

Стандартный кодировщик мультимедиа Hello позволяет toooverlay изображение на существующие видео. В настоящее время поддерживаются следующие форматы hello: png, jpg, gif и bmp. Hello предустановки, заданной ниже представлен Простейший пример наложения видео.

В дополнение к этому toodefining файл набора параметров, также имеется toolet Media Services знать, какой файл в ресурсе hello является изображение перекрытия hello и файл, который является hello источник видео, на котором необходимо toooverlay hello изображение. видеофайл Hello имеет toobe hello **основной** файла.

Если вы используете .NET, добавьте hello, следующие две функции, определенные toohello в следующем примере в [это](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) раздела. Hello **UploadMediaFilesFromFolder** функция отправляет файлы из папки (например, BigBuckBunny.mp4 и Image001.png) и наборы hello mp4 toobe файл hello первичный файл актива hello. Hello **EncodeWithOverlay** функция использует hello файла пользовательского стиля, переданный tooit (например, hello конфигурации, следующим) toocreate hello задачу кодирования.


    static public IAsset UploadMediaFilesFromFolder(string folderPath)
    {
        IAsset asset = _context.Assets.CreateFromFolder(folderPath, AssetCreationOptions.None);
    
        foreach (var af in asset.AssetFiles)
        {
            // hello following code assumes 
            // you have an input folder with one MP4 and one overlay image file.
            if (af.Name.Contains(".mp4"))
                af.IsPrimary = true;
            else
                af.IsPrimary = false;
    
            af.Update();
        }
    
        return asset;
    }

    static public IAsset EncodeWithOverlay(IAsset assetSource, string customPresetFileName)
    {
        // Declare a new job.
        IJob job = _context.Jobs.Create("Media Encoder Standard Job");
        // Get a media processor reference, and pass tooit hello name of hello 
        // processor toouse for hello specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Load hello XML (or JSON) from hello local file.
        string configuration = File.ReadAllText(customPresetFileName);

        // Create a task
        ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            configuration,
            TaskOptions.None);

        // Specify hello input assets toobe encoded.
        // This asset contains a source file and an overlay file.
        task.InputAssets.Add(assetSource);

        // Add an output asset toocontain hello results of hello job. 
        task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.None);

        job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
        job.Submit();
        job.GetExecutionProgressTask(CancellationToken.None).Wait();

        return job.OutputMediaAssets[0];
    }


> [!NOTE]
> Текущие ограничения:
>
> прозрачность наложения приветствия не поддерживается.
>
> Ваш исходный файл и файл изображения наложения hello имеют toobe в hello одного средства и hello видеофайл потребностей toobe набор как основной файл hello в этом ресурсе.
>
>

### <a name="json-preset"></a>Предустановка JSON
    {
      "Version": 1.0,
      "Sources": [
        {
          "Streams": [],
          "Filters": {
            "VideoOverlay": {
              "Position": {
                "X": 100,
                "Y": 100,
                "Width": 100,
                "Height": 50
              },
              "AudioGainLevel": 0.0,
              "MediaParams": [
                {
                  "OverlayLoopCount": 1
                },
                {
                  "IsOverlay": true,
                  "OverlayLoopCount": 1,
                  "InputLoop": true
                }
              ],
              "Source": "Image001.png",
              "Clip": {
                "Duration": "00:00:05"
              },
              "FadeInDuration": {
                "Duration": "00:00:01"
              },
              "FadeOutDuration": {
                "StartTime": "00:00:03",
                "Duration": "00:00:04"
              }
            }
          },
          "Pad": true
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1045,
              "MaxBitrate": 1045,
              "BufferWindow": "00:00:05",
              "ReferenceFrames": 3,
              "EntropyMode": "Cavlc",
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "Width": "640",
              "Height": "360",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
          "Type": "CopyAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}{Extension}",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }


### <a name="xml-preset"></a>Предустановка XML
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Sources>
        <Source>
          <Streams />
          <Filters>
            <VideoOverlay>
              <Source>Image001.png</Source>
              <Clip Duration="PT5S" />
              <FadeInDuration Duration="PT1S" />
              <FadeOutDuration StartTime="PT3S" Duration="PT4S" />
              <Position X="100" Y="100" Width="100" Height="50" />
              <Opacity>0</Opacity>
              <AudioGainLevel>0</AudioGainLevel>
              <MediaParams>
                <MediaParam>
                  <IsOverlay>false</IsOverlay>
                  <OverlayLoopCount>1</OverlayLoopCount>
                  <InputLoop>false</InputLoop>
                </MediaParam>
                <MediaParam>
                  <IsOverlay>true</IsOverlay>
                  <OverlayLoopCount>1</OverlayLoopCount>
                  <InputLoop>true</InputLoop>
                </MediaParam>
              </MediaParams>
            </VideoOverlay>
          </Filters>
          <Pad>true</Pad>
        </Source>
      </Sources>
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <H264Layers>
            <H264Layer>
              <Bitrate>1045</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>0</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cavlc</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1045</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <CopyAudio />
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}{Extension}">
          <MP4Format />
        </Output>
      </Outputs>
    </Preset>


## <a id="silent_audio"></a>Вставка звуковой дорожки с тишиной, если входные данные не содержат звука
По умолчанию при отправке входных toohello кодировщик, содержит только видео и без звука нажмите hello выходной актив содержит файлы, содержащие только видео данные. Некоторые проигрыватели не удается toohandle такого потока вывода. В этом сценарии можно использовать этот параметр tooforce hello кодировщика tooadd является выходом toohello автоматической звуковой дорожки.

tooforce hello кодировщика tooproduce актив, содержащий автоматической звуковой дорожки, когда входные данные не содержит звука, укажите значение «InsertSilenceIfNoAudio» hello.

Можно использовать любой hello предустановок MES задокументированы в [это](media-services-mes-presets-overview.md) статьи и внесите следующие изменения hello:

### <a name="json-preset"></a>Предустановка JSON
    {
      "Channels": 2,
      "SamplingRate": 44100,
      "Bitrate": 96,
      "Type": "AACAudio",
      "Condition": "InsertSilenceIfNoAudio"
    }

### <a name="xml-preset"></a>Предустановка XML
    <AACAudio Condition="InsertSilenceIfNoAudio">
      <Channels>2</Channels>
      <SamplingRate>44100</SamplingRate>
      <Bitrate>96</Bitrate>
    </AACAudio>

## <a id="deinterlacing"></a>Отключение автоматического устранения чересстрочной развертки
Клиентам не требуется toodo ничего, если они как hello чередования toobe содержимое автоматически отменяется с чередованием. При hello автоматически отменяется чередование на MES hello приветствия (по умолчанию) автоматического обнаружения чередующихся кадров, только отменить interlaces кадры с пометкой с чередованием.

Можно отключить hello автоматически отменяется чередование. Однако это делать не рекомендуется.

### <a name="json-preset"></a>Предустановка JSON
    "Sources": [
    {
     "Filters": {
        "Deinterlace": {
          "Mode": "Off"
        }
      },
    }
    ]

### <a name="xml-preset"></a>Предустановка XML
    <Sources>
    <Source>
      <Filters>
        <Deinterlace>
          <Mode>Off</Mode>
        </Deinterlace>
      </Filters>
    </Source>
    </Sources>


## <a id="audio_only"></a>Предустановки только для звука
В этом разделе демонстрируются две предустановки стандартного кодировщика мультимедиа только для звука: "Звук в формате AAC" и "Звук в формате AAC хорошего качества".

### <a name="aac-audio"></a>Звук в формате AAC
    {
      "Version": 1.0,
      "Codecs": [
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
          "FileName": "{Basename}_AAC_{AudioBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

### <a name="aac-good-quality-audio"></a>Звук в формате AAC хорошего качества
    {
      "Version": 1.0,
      "Codecs": [
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 192,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_AAC_{AudioBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

## <a id="concatenate"></a>Сцепка нескольких видеофайлов

Hello следующем примере показано, как можно создать стиль tooconcatenate два или несколько файлов. наиболее распространенным сценарием Hello удобно, если нужно tooadd заголовок или основного видео с toohello прицепа. Hello предназначено применяется, когда hello видеофайлов редактируемого вместе обладают свойствами (разрешение экрана, частота кадров, число звуковой дорожки, и т. д.). Следует позаботиться не toomix видео частота кадров или с другим числом звуковые дорожки.

>[!NOTE]
>Hello текущего конструктора функции объединения hello ожидает ввода, hello видеоклипы согласованы с точки зрения разрешение, частота кадров и т. д. 

### <a name="requirements-and-considerations"></a>Требования и рекомендации

* В исходных видеофайлах должна быть только одна аудиодорожка.
* Видео входных данных должны иметь hello же частота кадров.
* Необходимо передать видео на отдельных средств и сделайте видео hello hello первичного файла в каждого средства.
* Требуется длительность hello tooknow видео.
* Hello предустановленную приведенных ниже примерах предполагается запуска всех hello входного видео с меткой времени, равной нулю. Требуется значения StartTime hello toomodify Если видео hello имеют другой меткой времени начала, как это обычно бывает hello динамической архивы.
* Hello Предустановка JSON делает явные ссылки значения AssetID toohello входные активы hello.
* Образец Hello кода предполагается, что конфигурации JSON, приветствия был сохранен tooa локального файла, например «C:\supportFiles\preset.json». Также предполагается, что два активы были созданы путем передачи двух видеофайлов и знать hello итоговые значения AssetID.
* Здравствуйте, фрагмент кода и JSON Предустановка показан пример объединения двух файлов видео. Вы можете расширить его toomore чем двух видео с:

  1. Задача для вызова метода. InputAssets.Add() многократно tooadd дополнительные видео, в порядке.
  2. Внесения соответствующих изменяет элемент toohello «источники» в hello JSON, добавив дополнительные записи в hello порядке.

### <a name="net-code"></a>Код .NET

    IAsset asset1 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:606db602-efd7-4436-97b4-c0b867ba195b").FirstOrDefault();
    IAsset asset2 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:a7e2b90f-0565-4a94-87fe-0a9fa07b9c7e").FirstOrDefault();

    // Declare a new job.
    IJob job = _context.Jobs.Create("Media Encoder Standard Job for Concatenating Videos");
    // Get a media processor reference, and pass tooit hello name of the
    // processor toouse for hello specific task.
    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

    // Load hello XML (or JSON) from hello local file.
    string configuration = File.ReadAllText(@"c:\supportFiles\preset.json");

    // Create a task
    ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
        processor,
        configuration,
        TaskOptions.None);

    // Specify hello input videos toobe concatenated (in order).
    task.InputAssets.Add(asset1);
    task.InputAssets.Add(asset2);
    // Add an output asset toocontain hello results of hello job.
    // This output is specified as AssetCreationOptions.None, which
    // means hello output asset is not encrypted.
    task.OutputAssets.AddNew("Output asset",
        AssetCreationOptions.None);

    job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
    job.Submit();
    job.GetExecutionProgressTask(CancellationToken.None).Wait();

### <a name="json-preset"></a>Предустановка JSON

Обновите пользовательский стиль с идентификаторами, которые должны tooconcatenate активов hello и с сегментом hello подходящее время для каждого видео.

    {
      "Version": 1.0,
      "Sources": [
        {
          "AssetID": "606db602-efd7-4436-97b4-c0b867ba195b",
          "StartTime": "00:00:01",
          "Duration": "00:00:15"
        },
        {
          "AssetID": "a7e2b90f-0565-4a94-87fe-0a9fa07b9c7e",
          "StartTime": "00:00:02",
          "Duration": "00:00:05"
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "SceneChangeDetection": true,
          "H264Layers": [
            {
              "Level": "auto",
              "Bitrate": 1800,
              "MaxBitrate": 1800,
              "BufferWindow": "00:00:05",
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "Width": "640",
              "Height": "360",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
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

## <a id="crop"></a>Обрезка видео с помощью стандартного кодировщика мультимедиа
. В разделе hello [обрезать видео стандарту кодировщик мультимедиа](media-services-crop-video.md) раздела.

## <a id="no_video"></a>Вставка видеодорожки, если во входных данных нет видео

По умолчанию при отправке входных toohello кодировщик, содержит только аудио и видео не, то hello выходной актив содержит файлы, содержащие только звуковых данных. Проигрыватели, включая Azure Media Player (см. [это](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/8082468-audio-only-scenarios)) может оказаться может toohandle такие потоки. Можно использовать этот параметр tooforce hello кодировщика tooadd является выходом toohello монохромный видеодорожки в этом сценарии.

> [!NOTE]
> Принудительное tooinsert кодировщика hello выходных данных повышает видеодорожки hello размер hello выходных активов и Здравствуйте, тем самым затраты на кодирование задачи hello. Выполняйте тесты tooverify, этот итоговый увеличение имеет только ограниченное влияние на ваш ежемесячные расходы.
>

### <a name="inserting-video-at-only-hello-lowest-bitrate"></a>Вставка видео битрейтом hello низкий

Предположим, что вы используете несколько bitrate кодировку в конфигурации, такие как [«H264 Multiple Bitrate 720p»](media-services-mes-preset-h264-multiple-bitrate-720p.md) tooencode всего входных данных каталога для потоковой передачи, которая содержит сочетание видеофайлов и файлов только со звуком. В этом случае после ввода hello нет изображения можно tooforce hello кодировщика tooinsert отслеживать видео монохромный режим определяются в только что hello низкий битрейт, как противоположность tooinserting каждый выходной битрейте видео. tooachieve это, необходимо toouse hello **InsertBlackIfNoVideoBottomLayerOnly** флаг.

Можно использовать любой hello предустановок MES задокументированы в [это](media-services-mes-presets-overview.md) статьи и внесите следующие изменения hello:

#### <a name="json-preset"></a>Предустановка JSON
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideoBottomLayerOnly",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a>Предустановка XML

При использовании XML, использовать условие = «InsertBlackIfNoVideoBottomLayerOnly» как атрибут toohello **H264Video** элемент и условие = «InsertSilenceIfNoAudio» как атрибут слишком**AACAudio**.

```
. . .
<Encoding>
  <H264Video Condition="InsertBlackIfNoVideoBottomLayerOnly">
    <KeyFrameInterval>00:00:02</KeyFrameInterval>
    <SceneChangeDetection>true</SceneChangeDetection>
    <StretchMode>AutoSize</StretchMode>
    <H264Layers>
      <H264Layer>
        . . .
      </H264Layer>
    </H264Layers>
    <Chapters />
  </H264Video>
  <AACAudio Condition="InsertSilenceIfNoAudio">
    <Profile>AACLC</Profile>
    <Channels>2</Channels>
    <SamplingRate>48000</SamplingRate>
    <Bitrate>128</Bitrate>
  </AACAudio>
</Encoding>
. . .
```

### <a name="inserting-video-at-all-output-bitrates"></a>Вставка видео со всеми выходными скоростями
Предположим, что вы используете несколько bitrate кодировку в конфигурации, такие как [«H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) tooencode всего входных данных каталога для потоковой передачи, которая содержит сочетание видеофайлов и файлов только со звуком. В этом случае после ввода hello нет изображения можно tooforce hello кодировщика tooinsert монохромный Видеодорожка на всех битрейтах hello в выходных данных. Это гарантирует, что выходные данные средства — все однородные с относительно toonumber видеодорожек и звуковые дорожки. tooachieve это, необходимо toospecify hello флаг «InsertBlackIfNoVideo».

Можно использовать любой hello предустановок MES задокументированы в [это](media-services-mes-presets-overview.md) статьи и внесите следующие изменения hello:

#### <a name="json-preset"></a>Предустановка JSON
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideo",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a>Предустановка XML

При использовании XML, использовать условие = «InsertBlackIfNoVideo» как атрибут toohello **H264Video** элемент и условие = «InsertSilenceIfNoAudio» как атрибут слишком**AACAudio**.

```
. . .
<Encoding>
  <H264Video Condition="InsertBlackIfNoVideo">
    <KeyFrameInterval>00:00:02</KeyFrameInterval>
    <SceneChangeDetection>true</SceneChangeDetection>
    <StretchMode>AutoSize</StretchMode>
    <H264Layers>
      <H264Layer>
        . . .
      </H264Layer>
    </H264Layers>
    <Chapters />
  </H264Video>
  <AACAudio Condition="InsertSilenceIfNoAudio">
    <Profile>AACLC</Profile>
    <Channels>2</Channels>
    <SamplingRate>48000</SamplingRate>
    <Bitrate>128</Bitrate>
  </AACAudio>
</Encoding>
. . .  
```

## <a id="rotate_video"></a>Поворот видео
Hello [Media Encoder Стандартная](media-services-dotnet-encode-with-media-encoder-standard.md) поддерживает поворот по углы 0/90/180 или 270. поведение по умолчанию Hello — «Авто», где пытается toodetect hello поворота метаданных в hello входящих видеофайлов и компенсации для него. Включить следующие hello **источников** tooone элемент hello стилей, определенных в [это](media-services-mes-presets-overview.md) раздела:

### <a name="json-preset"></a>Предустановка JSON
    "Sources": [
    {
      "Streams": [],
      "Filters": {
        "Rotation": "90"
      }
    }
    ],
    "Codecs": [

    ...
### <a name="xml-preset"></a>Предустановка XML
    <Sources>
           <Source>
          <Streams />
          <Filters>
            <Rotation>90</Rotation>
          </Filters>
        </Source>
    </Sources>

Кроме того, в разделе [это](media-services-mes-schema.md#PreserveResolutionAfterRotation) приведены дополнительные сведения об как кодировщик hello интерпретирует hello параметры ширины и высоты в hello, то по умолчанию при запуске поворота компенсации.

Можно использовать hello значение «0» tooindicate toohello кодировщика tooignore поворота метаданных, если он имеется, входное видео hello.

## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>См. также
[Обзор кодирования с помощью служб мультимедиа](media-services-encode-asset.md)
