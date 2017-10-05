---
title: "Создание эскизов с помощью Media Encoder Standard c использованием .NET"
description: "В данной статье рассказывается, как использовать .NET для кодирования ресурсов и одновременно с этим создавать эскизы с помощью Media Encoder Standard."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: b8dab73a-1d91-4b6d-9741-a92ad39fc3f7
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: juliako
ms.openlocfilehash: 89d15cbdf71a140e78f34e07ff208776b7d4cab3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-generate-thumbnails-using-media-encoder-standard-with-net"></a><span data-ttu-id="55d35-103">Создание эскизов с помощью Media Encoder Standard c использованием .NET</span><span class="sxs-lookup"><span data-stu-id="55d35-103">How to generate thumbnails using Media Encoder Standard with .NET</span></span>

<span data-ttu-id="55d35-104">Media Encoder Standard можно использовать для создания одного или нескольких эскизов из входящего видео в форматах файлов изображений [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics) или [BMP](https://en.wikipedia.org/wiki/BMP_file_format).</span><span class="sxs-lookup"><span data-stu-id="55d35-104">You can use Media Encoder Standard to generate one or more thumbnails from your input video in [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics), or [BMP](https://en.wikipedia.org/wiki/BMP_file_format) image file formats.</span></span> <span data-ttu-id="55d35-105">Вы можете отправлять задачи, которые создают только изображения, или объединить создание эскизов с кодированием.</span><span class="sxs-lookup"><span data-stu-id="55d35-105">You can submit Tasks that produce only images, or you can combine thumbnail generation with encoding.</span></span> <span data-ttu-id="55d35-106">В этой статье представлены несколько примеров предустановок эскизов XML и JSON для таких сценариев.</span><span class="sxs-lookup"><span data-stu-id="55d35-106">This topic provides a few sample XML and JSON thumbnail presets for such scenarios.</span></span> <span data-ttu-id="55d35-107">В конце этого раздела приведен [пример кода](#code_sample), показывающий, как с помощью пакета SDK для .NET для служб мультимедиа выполнить задачу кодирования.</span><span class="sxs-lookup"><span data-stu-id="55d35-107">At the end of the topic, there is a [sample code](#code_sample) that shows how to use the Media Services .NET SDK to accomplish the encoding task.</span></span>

<span data-ttu-id="55d35-108">Дополнительные сведения об элементах, используемых в примерах предустановок см. в статье [Схема Media Encoder Standard](media-services-mes-schema.md).</span><span class="sxs-lookup"><span data-stu-id="55d35-108">For more details on the elements that are used in sample presets, you should review [Media Encoder Standard schema](media-services-mes-schema.md).</span></span>

<span data-ttu-id="55d35-109">Обязательно изучите раздел [Рекомендации](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) .</span><span class="sxs-lookup"><span data-stu-id="55d35-109">Make sure to review the [Considerations](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) section.</span></span>

## <a name="example--single-png-file"></a><span data-ttu-id="55d35-110">Пример. Один файл PNG</span><span class="sxs-lookup"><span data-stu-id="55d35-110">Example – single PNG file</span></span>

<span data-ttu-id="55d35-111">Следующую предустановку JSON и XML можно использовать для создания одного выходного файла PNG на основе первых секунд входного видео, где кодировщик предпринимает все усилия, чтобы найти интересный кадр.</span><span class="sxs-lookup"><span data-stu-id="55d35-111">The following JSON and XML preset can be used to produce a single output PNG file out of the first few seconds of the input video, where the encoder makes a best-effort attempt at finding an “interesting” frame.</span></span> <span data-ttu-id="55d35-112">Обратите внимание, что для размера выходных изображений выбрано значение 100 %, то есть они будут совпадать с размером входного видео.</span><span class="sxs-lookup"><span data-stu-id="55d35-112">Note that the output image dimensions have been set to 100%, meaning these will match the dimensions of the input video.</span></span> <span data-ttu-id="55d35-113">При этом параметр "Format" в разделе "Outputs" должен соответствовать использованию "PngLayers" в разделе "Codecs".</span><span class="sxs-lookup"><span data-stu-id="55d35-113">Note also how the “Format” setting in “Outputs” is required to match the use of “PngLayers” in the “Codecs” section.</span></span> 

### <a name="json-preset"></a><span data-ttu-id="55d35-114">Предустановка JSON</span><span class="sxs-lookup"><span data-stu-id="55d35-114">JSON preset</span></span>

    {
      "Version": 1.0,
      "Codecs": [
        {
          "PngLayers": [
            {
              "Type": "PngLayer",
              "Width": "100%",
              "Height": "100%"
            }
          ],
          "Start": "{Best}",
          "Type": "PngImage"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "PngFormat"
          }
        }
      ]
    }
    
### <a name="xml-preset"></a><span data-ttu-id="55d35-115">Предустановка XML</span><span class="sxs-lookup"><span data-stu-id="55d35-115">XML preset</span></span>

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <PngImage Start="{Best}">
          <PngLayers>
            <PngLayer>
              <Width>100%</Width>
              <Height>100%</Height>
            </PngLayer>
          </PngLayers>
        </PngImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Index}{Extension}">
          <PngFormat />
        </Output>
      </Outputs>
    </Preset>

## <a name="example--a-series-of-jpeg-images"></a><span data-ttu-id="55d35-116">Пример. Несколько изображений JPEG</span><span class="sxs-lookup"><span data-stu-id="55d35-116">Example – a series of JPEG images</span></span>

<span data-ttu-id="55d35-117">Следующую предустановку JSON и XML можно использовать для создания 10 изображений на метках времени 5 %, 15 %, ..., 95 % входной временной шкалы, где размер изображения установлен как одна четвертая от размера входного видео.</span><span class="sxs-lookup"><span data-stu-id="55d35-117">The following JSON and XML preset can be used to produce a set of 10 images at timestamps of 5%, 15%, …, 95% of the input timeline, where the image size is specified to be one quarter that of the input video.</span></span>

### <a name="json-preset"></a><span data-ttu-id="55d35-118">Предустановка JSON</span><span class="sxs-lookup"><span data-stu-id="55d35-118">JSON preset</span></span>

    {
      "Version": 1.0,
      "Codecs": [
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": "25%",
              "Height": "25%"
            }
          ],
          "Start": "5%",
          "Step": "1",
          "Range": "1",
          "Type": "JpgImage"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        }
      ]
    }

### <a name="xml-preset"></a><span data-ttu-id="55d35-119">Предустановка XML</span><span class="sxs-lookup"><span data-stu-id="55d35-119">XML preset</span></span>
    
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <JpgImage Start="5%" Step="10%" Range="96%">
          <JpgLayers>
            <JpgLayer>
              <Width>25%</Width>
              <Height>25%</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
      </Outputs>
    </Preset>

## <a name="example--one-image-at-a-specific-timestamp"></a><span data-ttu-id="55d35-120">Пример. Одно изображение на определенной метке времени</span><span class="sxs-lookup"><span data-stu-id="55d35-120">Example – one image at a specific timestamp</span></span>

<span data-ttu-id="55d35-121">Следующую предустановку JSON и XML можно использовать для создания одного изображения JPEG на 30-секундной отметке времени входного видео.</span><span class="sxs-lookup"><span data-stu-id="55d35-121">The following JSON and XML preset can be used to produce a single JPEG image at the 30 second mark of the input video.</span></span> <span data-ttu-id="55d35-122">Данная предустановка ожидает, что входное видео будет длиться более 30 секунд (иначе задание завершится ошибкой).</span><span class="sxs-lookup"><span data-stu-id="55d35-122">This preset expects the input to be more than 30 seconds in duration (else the job will fail).</span></span>

### <a name="json-preset"></a><span data-ttu-id="55d35-123">Предустановка JSON</span><span class="sxs-lookup"><span data-stu-id="55d35-123">JSON preset</span></span>

    {
      "Version": 1.0,
      "Codecs": [
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": "25%",
              "Height": "25%"
            }
          ],
          "Start": "00:00:30",
          "Step": "1",
          "Range": "1",
          "Type": "JpgImage"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        }
      ]
    }
    
### <a name="xml-preset"></a><span data-ttu-id="55d35-124">Предустановка XML</span><span class="sxs-lookup"><span data-stu-id="55d35-124">XML preset</span></span>
    
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <JpgImage Start="00:00:30" Step="00:00:02" Range="00:00:01">
          <JpgLayers>
            <JpgLayer>
              <Width>25%</Width>
              <Height>25%</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
      </Outputs>
    </Preset>

## <span data-ttu-id="55d35-125"><a id="code_sample"></a> Пример. Кодирование видео и создание эскиза</span><span class="sxs-lookup"><span data-stu-id="55d35-125"><a id="code_sample"></a>Example – encode video and generate thumbnail</span></span>

<span data-ttu-id="55d35-126">В следующем примере кода пакет SDK служб мультимедиа используется для выполнения следующих задач.</span><span class="sxs-lookup"><span data-stu-id="55d35-126">The following code example uses Media Services .NET SDK to perform the following tasks:</span></span>

* <span data-ttu-id="55d35-127">Создание задания кодирования.</span><span class="sxs-lookup"><span data-stu-id="55d35-127">Create an encoding job.</span></span>
* <span data-ttu-id="55d35-128">Получение ссылки на стандартный кодировщик мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="55d35-128">Get a reference to the Media Encoder Standard encoder.</span></span>
* <span data-ttu-id="55d35-129">Загрузка предопределенного кода [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) или [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json), содержащего предопределенную кодировку, а также сведения, необходимые для создания эскизов.</span><span class="sxs-lookup"><span data-stu-id="55d35-129">Load the preset [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) or [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) that contain the encoding preset as well as information needed to generate thumbnails.</span></span> <span data-ttu-id="55d35-130">Вы можете сохранить этот [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml)- или [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json)-код в файл и использовать указанный ниже код для загрузки файла.</span><span class="sxs-lookup"><span data-stu-id="55d35-130">You can save this  [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) or [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) in a file and use the following code to load the file.</span></span>
  
        // Load the XML (or JSON) from the local file.
        string configuration = File.ReadAllText(fileName);  
* <span data-ttu-id="55d35-131">Добавление одной задачи кодирования в задание.</span><span class="sxs-lookup"><span data-stu-id="55d35-131">Add a single encoding task to the job.</span></span> 
* <span data-ttu-id="55d35-132">Указание входного ресурса-контейнера для кодирования.</span><span class="sxs-lookup"><span data-stu-id="55d35-132">Specify the input asset to be encoded.</span></span>
* <span data-ttu-id="55d35-133">Создание выходного ресурса-контейнера, который будет содержать закодированный ресурс-контейнер.</span><span class="sxs-lookup"><span data-stu-id="55d35-133">Create an output asset that will contain the encoded asset.</span></span>
* <span data-ttu-id="55d35-134">Добавление обработчика событий для проверки хода выполнения задания.</span><span class="sxs-lookup"><span data-stu-id="55d35-134">Add an event handler to check the job progress.</span></span>
* <span data-ttu-id="55d35-135">Отправка задания.</span><span class="sxs-lookup"><span data-stu-id="55d35-135">Submit the job.</span></span>

<span data-ttu-id="55d35-136">Дополнительные сведения о настройке среды разработки см. в статье [Разработка служб мультимедиа с помощью .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="55d35-136">See the [Media Services development with .NET](media-services-dotnet-how-to-use.md) topic for directions on how to set up your dev environment.</span></span>

        using System;
        using System.Configuration;
        using System.IO;
        using System.Linq;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;

        namespace EncodeAndGenerateThumbnails
        {
        class Program
        {
            // Read values from the App.config file.
            private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
            private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

            private static CloudMediaContext _context = null;

            private static readonly string _mediaFiles =
            Path.GetFullPath(@"../..\Media");

            private static readonly string _singleMP4File =
            Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

            static void Main(string[] args)
            {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Get an uploaded asset.
            var asset = _context.Assets.FirstOrDefault();

            // Encode and generate the thumbnails.
            EncodeToAdaptiveBitrateMP4Set(asset);

            Console.ReadLine();
            }

            static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
            {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Job");
            // Get a media processor reference, and pass to it the name of the 
            // processor to use for the specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Load the XML (or JSON) from the local file.
            string configuration = File.ReadAllText("ThumbnailPreset_JSON.json");

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
                processor,
                configuration,
                TaskOptions.None);

            // Specify the input asset to be encoded.
            task.InputAssets.Add(asset);
            // Add an output asset to contain the results of the job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means the output asset is not encrypted. 
            task.OutputAssets.AddNew("Output asset",
                AssetCreationOptions.None);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
            }

            private static void JobStateChanged(object sender, JobStateChangedEventArgs e)
            {
            Console.WriteLine("Job state changed event:");
            Console.WriteLine("  Previous state: " + e.PreviousState);
            Console.WriteLine("  Current state: " + e.CurrentState);
            switch (e.CurrentState)
            {
                case JobState.Finished:
                Console.WriteLine();
                Console.WriteLine("Job is finished. Please wait while local tasks or downloads complete...");
                break;
                case JobState.Canceling:
                case JobState.Queued:
                case JobState.Scheduled:
                case JobState.Processing:
                Console.WriteLine("Please wait...\n");
                break;
                case JobState.Canceled:
                case JobState.Error:

                // Cast sender as a job.
                IJob job = (IJob)sender;

                // Display or log error details as needed.
                break;
                default:
                break;
            }
            }

            private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
            {
            var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
            ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
                throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
            }
        }
        }

## <span data-ttu-id="55d35-137"><a id="json"></a>Предопределенный эскиз JSON</span><span class="sxs-lookup"><span data-stu-id="55d35-137"><a id="json"></a>Thumbnail JSON preset</span></span>
<span data-ttu-id="55d35-138">Сведения о схеме см. [здесь](https://msdn.microsoft.com/library/mt269962.aspx).</span><span class="sxs-lookup"><span data-stu-id="55d35-138">For information about schema, see [this](https://msdn.microsoft.com/library/mt269962.aspx) topic.</span></span>

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
              "Width": "100%",
              "Height": "100%"
            }
          ],
          "Start": "{Best}",
          "Type": "JpgImage"
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
          "FileName": "{Basename}_{Resolution}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

## <span data-ttu-id="55d35-139"><a id="xml"></a>Предопределенный эскиз XML</span><span class="sxs-lookup"><span data-stu-id="55d35-139"><a id="xml"></a>Thumbnail XML preset</span></span>
<span data-ttu-id="55d35-140">Сведения о схеме см. [здесь](https://msdn.microsoft.com/library/mt269962.aspx).</span><span class="sxs-lookup"><span data-stu-id="55d35-140">For information about schema, see [this](https://msdn.microsoft.com/library/mt269962.aspx) topic.</span></span>
    
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
              <Width>100%</Width>
              <Height>100%/Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Resolution}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
      </Outputs>
    </Preset>

## <a name="considerations"></a><span data-ttu-id="55d35-141">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="55d35-141">Considerations</span></span>
<span data-ttu-id="55d35-142">Действительны следующие условия.</span><span class="sxs-lookup"><span data-stu-id="55d35-142">The following considerations apply:</span></span>

* <span data-ttu-id="55d35-143">Использование явных меток времени для элементов Start, Step или Range предполагает, что входные данные составляют не менее одной минуты.</span><span class="sxs-lookup"><span data-stu-id="55d35-143">The use of explicit timestamps for Start/Step/Range assumes that the input source is at least 1 minute long.</span></span>
* <span data-ttu-id="55d35-144">Элементы Jpg, Png и BmpImage обладают атрибутами Start, Step и Range, которые можно интерпретировать следующим образом.</span><span class="sxs-lookup"><span data-stu-id="55d35-144">Jpg/Png/BmpImage elements have Start, Step and Range string attributes – these can be interpreted as:</span></span>
  
  * <span data-ttu-id="55d35-145">Номер кадра, если эти атрибуты выражены неотрицательными целыми числами, например,</span><span class="sxs-lookup"><span data-stu-id="55d35-145">Frame Number if they are non-negative integers, eg.</span></span> <span data-ttu-id="55d35-146">"Start": "120",</span><span class="sxs-lookup"><span data-stu-id="55d35-146">"Start": "120",</span></span>
  * <span data-ttu-id="55d35-147">Отношение к длительности источника, если атрибуты выражены как %-суффикс, например,</span><span class="sxs-lookup"><span data-stu-id="55d35-147">Relative to source duration if expressed as %-suffixed, eg.</span></span> <span data-ttu-id="55d35-148">"Start": "15%", ИЛИ</span><span class="sxs-lookup"><span data-stu-id="55d35-148">"Start": "15%", OR</span></span>
  * <span data-ttu-id="55d35-149">Отметка времени, если атрибуты имеют формат</span><span class="sxs-lookup"><span data-stu-id="55d35-149">Timestamp if expressed as HH:MM:SS…</span></span> <span data-ttu-id="55d35-150">ЧЧ:ММ:СС...</span><span class="sxs-lookup"><span data-stu-id="55d35-150">format.</span></span> <span data-ttu-id="55d35-151">Например,</span><span class="sxs-lookup"><span data-stu-id="55d35-151">Eg.</span></span> <span data-ttu-id="55d35-152">"Start" : "00:01:00"</span><span class="sxs-lookup"><span data-stu-id="55d35-152">"Start" : "00:01:00"</span></span>
    
    <span data-ttu-id="55d35-153">При желании условные обозначения можно комбинировать.</span><span class="sxs-lookup"><span data-stu-id="55d35-153">You can mix and match notations as you please.</span></span>
    
    <span data-ttu-id="55d35-154">Кроме того, атрибут Start поддерживает также специальный макрос {Best}, который пытается определить первый "интересный" кадр содержимого NOTE: (если атрибут Start имеет значение {Best}, атрибуты Step и Range игнорируются)</span><span class="sxs-lookup"><span data-stu-id="55d35-154">Additionally, Start also supports a special Macro:{Best}, which attempts to determine the first “interesting” frame of the content NOTE: (Step and Range are ignored when Start is set to {Best})</span></span>
  * <span data-ttu-id="55d35-155">По умолчанию Start:{Best}</span><span class="sxs-lookup"><span data-stu-id="55d35-155">Defaults: Start:{Best}</span></span>
* <span data-ttu-id="55d35-156">Для атрибута Image должен быть указан формат выходных данных: Jpg/Png/BmpFormat.</span><span class="sxs-lookup"><span data-stu-id="55d35-156">Output format needs to be explicitly provided for each Image format: Jpg/Png/BmpFormat.</span></span> <span data-ttu-id="55d35-157">MES, если он присутствует, соответствует JpgVideo для JpgFormat и т. д.</span><span class="sxs-lookup"><span data-stu-id="55d35-157">When present, MES will match JpgVideo to JpgFormat and so on.</span></span> <span data-ttu-id="55d35-158">OutputFormat представляет новый макрос, связанный с кодеком изображений: {Index}, который необходимо указывать для форматов вывода изображений (один и только один раз).</span><span class="sxs-lookup"><span data-stu-id="55d35-158">OutputFormat introduces a new image-codec specific Macro: {Index}, which needs to be present (once and only once) for image output formats.</span></span>

## <a name="next-steps"></a><span data-ttu-id="55d35-159">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="55d35-159">Next steps</span></span>

<span data-ttu-id="55d35-160">Вы можете проверить [ход выполнения задания](media-services-check-job-progress.md), пока задание кодировки находится в ожидании.</span><span class="sxs-lookup"><span data-stu-id="55d35-160">You can check the [job progress](media-services-check-job-progress.md) while the encoding job is pending.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="55d35-161">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="55d35-161">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="55d35-162">Отзывы</span><span class="sxs-lookup"><span data-stu-id="55d35-162">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="55d35-163">См. также</span><span class="sxs-lookup"><span data-stu-id="55d35-163">See Also</span></span>
[<span data-ttu-id="55d35-164">Обзор кодирования с помощью служб мультимедиа</span><span class="sxs-lookup"><span data-stu-id="55d35-164">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

