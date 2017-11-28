---
title: "эскизы toogenerate aaaHow с помощью Media Encoder стандартный в .NET Framework"
description: "В этом разделе показано, как tooencode .NET toouse актива и создания эскизов на hello одновременно с помощью стандартных кодировщика мультимедиа."
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
ms.openlocfilehash: 23d3e4d9bf64a688d45499c045f19d2792167990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogenerate-thumbnails-using-media-encoder-standard-with-net"></a><span data-ttu-id="419c4-103">Как toogenerate эскизы с помощью Media Encoder стандартный в .NET Framework</span><span class="sxs-lookup"><span data-stu-id="419c4-103">How toogenerate thumbnails using Media Encoder Standard with .NET</span></span>

<span data-ttu-id="419c4-104">Стандартный кодировщик мультимедиа toogenerate можно использовать один или несколько эскизов из введенных видео в [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics), или [BMP](https://en.wikipedia.org/wiki/BMP_file_format) форматам файлов.</span><span class="sxs-lookup"><span data-stu-id="419c4-104">You can use Media Encoder Standard toogenerate one or more thumbnails from your input video in [JPEG](https://en.wikipedia.org/wiki/JPEG), [PNG](https://en.wikipedia.org/wiki/Portable_Network_Graphics), or [BMP](https://en.wikipedia.org/wiki/BMP_file_format) image file formats.</span></span> <span data-ttu-id="419c4-105">Вы можете отправлять задачи, которые создают только изображения, или объединить создание эскизов с кодированием.</span><span class="sxs-lookup"><span data-stu-id="419c4-105">You can submit Tasks that produce only images, or you can combine thumbnail generation with encoding.</span></span> <span data-ttu-id="419c4-106">В этой статье представлены несколько примеров предустановок эскизов XML и JSON для таких сценариев.</span><span class="sxs-lookup"><span data-stu-id="419c4-106">This topic provides a few sample XML and JSON thumbnail presets for such scenarios.</span></span> <span data-ttu-id="419c4-107">В конце раздела hello hello — [пример кода](#code_sample) , показано, как tooaccomplish Media Services .NET SDK hello toouse hello задачу кодирования.</span><span class="sxs-lookup"><span data-stu-id="419c4-107">At hello end of hello topic, there is a [sample code](#code_sample) that shows how toouse hello Media Services .NET SDK tooaccomplish hello encoding task.</span></span>

<span data-ttu-id="419c4-108">Дополнительные сведения о hello элементы, используемые в образце предустановок Изучите [Media Encoder стандартной схеме](media-services-mes-schema.md).</span><span class="sxs-lookup"><span data-stu-id="419c4-108">For more details on hello elements that are used in sample presets, you should review [Media Encoder Standard schema](media-services-mes-schema.md).</span></span>

<span data-ttu-id="419c4-109">Убедитесь, что hello tooreview [вопросы](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) раздела.</span><span class="sxs-lookup"><span data-stu-id="419c4-109">Make sure tooreview hello [Considerations](media-services-dotnet-generate-thumbnail-with-mes.md#considerations) section.</span></span>

## <a name="example--single-png-file"></a><span data-ttu-id="419c4-110">Пример. Один файл PNG</span><span class="sxs-lookup"><span data-stu-id="419c4-110">Example – single PNG file</span></span>

<span data-ttu-id="419c4-111">Hello следующий JSON и XML-Предустановка может быть используется tooproduce один выходной PNG файл из hello несколько секунд, входное видео hello, где кодировщика hello предпринимает все усилия на поиск кадр с «Город».</span><span class="sxs-lookup"><span data-stu-id="419c4-111">hello following JSON and XML preset can be used tooproduce a single output PNG file out of hello first few seconds of hello input video, where hello encoder makes a best-effort attempt at finding an “interesting” frame.</span></span> <span data-ttu-id="419c4-112">Обратите внимание, что размеры изображения: hello выходные данные были установлены too100%, это означает, что эти данные будут совпадать hello размеры hello входное видео.</span><span class="sxs-lookup"><span data-stu-id="419c4-112">Note that hello output image dimensions have been set too100%, meaning these will match hello dimensions of hello input video.</span></span> <span data-ttu-id="419c4-113">Обратите внимание, как параметр «Формат» hello в окне «Выходные данные» требуется использование hello toomatch «PngLayers» в разделе «Кодеки» hello.</span><span class="sxs-lookup"><span data-stu-id="419c4-113">Note also how hello “Format” setting in “Outputs” is required toomatch hello use of “PngLayers” in hello “Codecs” section.</span></span> 

### <a name="json-preset"></a><span data-ttu-id="419c4-114">Предустановка JSON</span><span class="sxs-lookup"><span data-stu-id="419c4-114">JSON preset</span></span>

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
    
### <a name="xml-preset"></a><span data-ttu-id="419c4-115">Предустановка XML</span><span class="sxs-lookup"><span data-stu-id="419c4-115">XML preset</span></span>

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

## <a name="example--a-series-of-jpeg-images"></a><span data-ttu-id="419c4-116">Пример. Несколько изображений JPEG</span><span class="sxs-lookup"><span data-stu-id="419c4-116">Example – a series of JPEG images</span></span>

<span data-ttu-id="419c4-117">Здравствуйте следующий JSON и XML-Предустановка может быть используется tooproduce набор 10 изображений на отметки времени 5% 15%,..., 95% hello входной временной шкалы, где hello составляет указанного toobe один квартал, hello ввода видео.</span><span class="sxs-lookup"><span data-stu-id="419c4-117">hello following JSON and XML preset can be used tooproduce a set of 10 images at timestamps of 5%, 15%, …, 95% of hello input timeline, where hello image size is specified toobe one quarter that of hello input video.</span></span>

### <a name="json-preset"></a><span data-ttu-id="419c4-118">Предустановка JSON</span><span class="sxs-lookup"><span data-stu-id="419c4-118">JSON preset</span></span>

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

### <a name="xml-preset"></a><span data-ttu-id="419c4-119">Предустановка XML</span><span class="sxs-lookup"><span data-stu-id="419c4-119">XML preset</span></span>
    
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

## <a name="example--one-image-at-a-specific-timestamp"></a><span data-ttu-id="419c4-120">Пример. Одно изображение на определенной метке времени</span><span class="sxs-lookup"><span data-stu-id="419c4-120">Example – one image at a specific timestamp</span></span>

<span data-ttu-id="419c4-121">Привет, следующая Предустановка JSON и XML может быть используется tooproduce одного изображения JPEG в hello 30-секундная отметка hello входного видео.</span><span class="sxs-lookup"><span data-stu-id="419c4-121">hello following JSON and XML preset can be used tooproduce a single JPEG image at hello 30 second mark of hello input video.</span></span> <span data-ttu-id="419c4-122">Данная конфигурация ожидает ввода toobe hello более 30 секунд в поле длительности (else hello задание будет завершаться с ошибкой).</span><span class="sxs-lookup"><span data-stu-id="419c4-122">This preset expects hello input toobe more than 30 seconds in duration (else hello job will fail).</span></span>

### <a name="json-preset"></a><span data-ttu-id="419c4-123">Предустановка JSON</span><span class="sxs-lookup"><span data-stu-id="419c4-123">JSON preset</span></span>

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
    
### <a name="xml-preset"></a><span data-ttu-id="419c4-124">Предустановка XML</span><span class="sxs-lookup"><span data-stu-id="419c4-124">XML preset</span></span>
    
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

## <span data-ttu-id="419c4-125"><a id="code_sample"></a> Пример. Кодирование видео и создание эскиза</span><span class="sxs-lookup"><span data-stu-id="419c4-125"><a id="code_sample"></a>Example – encode video and generate thumbnail</span></span>

<span data-ttu-id="419c4-126">Следующий пример кода Hello использует hello tooperform Media Services .NET SDK следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="419c4-126">hello following code example uses Media Services .NET SDK tooperform hello following tasks:</span></span>

* <span data-ttu-id="419c4-127">Создание задания кодирования.</span><span class="sxs-lookup"><span data-stu-id="419c4-127">Create an encoding job.</span></span>
* <span data-ttu-id="419c4-128">Получите кодировщик Media Encoder Стандартная toohello ссылки.</span><span class="sxs-lookup"><span data-stu-id="419c4-128">Get a reference toohello Media Encoder Standard encoder.</span></span>
* <span data-ttu-id="419c4-129">Предустановка hello нагрузки [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) или [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) , содержащие hello кодирования предустановку также сведения, необходимые toogenerate эскизы.</span><span class="sxs-lookup"><span data-stu-id="419c4-129">Load hello preset [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) or [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) that contain hello encoding preset as well as information needed toogenerate thumbnails.</span></span> <span data-ttu-id="419c4-130">Можно сохранить это [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) или [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) в файл и используйте hello, следующие файл hello tooload кода.</span><span class="sxs-lookup"><span data-stu-id="419c4-130">You can save this  [XML](media-services-dotnet-generate-thumbnail-with-mes.md#xml) or [JSON](media-services-dotnet-generate-thumbnail-with-mes.md#json) in a file and use hello following code tooload hello file.</span></span>
  
        // Load hello XML (or JSON) from hello local file.
        string configuration = File.ReadAllText(fileName);  
* <span data-ttu-id="419c4-131">Добавьте одно задание toohello задач кодирования.</span><span class="sxs-lookup"><span data-stu-id="419c4-131">Add a single encoding task toohello job.</span></span> 
* <span data-ttu-id="419c4-132">Укажите входной hello toobe активов кодировке.</span><span class="sxs-lookup"><span data-stu-id="419c4-132">Specify hello input asset toobe encoded.</span></span>
* <span data-ttu-id="419c4-133">Создание выходного актива, который будет содержать активов hello в кодировке.</span><span class="sxs-lookup"><span data-stu-id="419c4-133">Create an output asset that will contain hello encoded asset.</span></span>
* <span data-ttu-id="419c4-134">Добавьте событие обработчика toocheck hello ход выполнения задания.</span><span class="sxs-lookup"><span data-stu-id="419c4-134">Add an event handler toocheck hello job progress.</span></span>
* <span data-ttu-id="419c4-135">Отправка задания hello.</span><span class="sxs-lookup"><span data-stu-id="419c4-135">Submit hello job.</span></span>

<span data-ttu-id="419c4-136">В разделе hello [разработки служб мультимедиа с помощью .NET](media-services-dotnet-how-to-use.md) разделе инструкции о том, как tooset настроить среду разработки.</span><span class="sxs-lookup"><span data-stu-id="419c4-136">See hello [Media Services development with .NET](media-services-dotnet-how-to-use.md) topic for directions on how tooset up your dev environment.</span></span>

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
            // Read values from hello App.config file.
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

            // Encode and generate hello thumbnails.
            EncodeToAdaptiveBitrateMP4Set(asset);

            Console.ReadLine();
            }

            static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
            {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Job");
            // Get a media processor reference, and pass tooit hello name of hello 
            // processor toouse for hello specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Load hello XML (or JSON) from hello local file.
            string configuration = File.ReadAllText("ThumbnailPreset_JSON.json");

            // Create a task
            ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
                processor,
                configuration,
                TaskOptions.None);

            // Specify hello input asset toobe encoded.
            task.InputAssets.Add(asset);
            // Add an output asset toocontain hello results of hello job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means hello output asset is not encrypted. 
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

## <span data-ttu-id="419c4-137"><a id="json"></a>Предопределенный эскиз JSON</span><span class="sxs-lookup"><span data-stu-id="419c4-137"><a id="json"></a>Thumbnail JSON preset</span></span>
<span data-ttu-id="419c4-138">Сведения о схеме см. [здесь](https://msdn.microsoft.com/library/mt269962.aspx).</span><span class="sxs-lookup"><span data-stu-id="419c4-138">For information about schema, see [this](https://msdn.microsoft.com/library/mt269962.aspx) topic.</span></span>

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

## <span data-ttu-id="419c4-139"><a id="xml"></a>Предопределенный эскиз XML</span><span class="sxs-lookup"><span data-stu-id="419c4-139"><a id="xml"></a>Thumbnail XML preset</span></span>
<span data-ttu-id="419c4-140">Сведения о схеме см. [здесь](https://msdn.microsoft.com/library/mt269962.aspx).</span><span class="sxs-lookup"><span data-stu-id="419c4-140">For information about schema, see [this](https://msdn.microsoft.com/library/mt269962.aspx) topic.</span></span>
    
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

## <a name="considerations"></a><span data-ttu-id="419c4-141">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="419c4-141">Considerations</span></span>
<span data-ttu-id="419c4-142">применить Hello следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="419c4-142">hello following considerations apply:</span></span>

* <span data-ttu-id="419c4-143">Использование Hello явные отметки времени для начала/шаг или Range предполагается, что этот источник входных hello — менее 1 минуты long.</span><span class="sxs-lookup"><span data-stu-id="419c4-143">hello use of explicit timestamps for Start/Step/Range assumes that hello input source is at least 1 minute long.</span></span>
* <span data-ttu-id="419c4-144">Элементы Jpg, Png и BmpImage обладают атрибутами Start, Step и Range, которые можно интерпретировать следующим образом.</span><span class="sxs-lookup"><span data-stu-id="419c4-144">Jpg/Png/BmpImage elements have Start, Step and Range string attributes – these can be interpreted as:</span></span>
  
  * <span data-ttu-id="419c4-145">Номер кадра, если эти атрибуты выражены неотрицательными целыми числами, например,</span><span class="sxs-lookup"><span data-stu-id="419c4-145">Frame Number if they are non-negative integers, eg.</span></span> <span data-ttu-id="419c4-146">"Start": "120",</span><span class="sxs-lookup"><span data-stu-id="419c4-146">"Start": "120",</span></span>
  * <span data-ttu-id="419c4-147">Если выразить в виде добавляется суффикс %, например относительный toosource длительность.</span><span class="sxs-lookup"><span data-stu-id="419c4-147">Relative toosource duration if expressed as %-suffixed, eg.</span></span> <span data-ttu-id="419c4-148">"Start": "15%", ИЛИ</span><span class="sxs-lookup"><span data-stu-id="419c4-148">"Start": "15%", OR</span></span>
  * <span data-ttu-id="419c4-149">Отметка времени, если атрибуты имеют формат</span><span class="sxs-lookup"><span data-stu-id="419c4-149">Timestamp if expressed as HH:MM:SS…</span></span> <span data-ttu-id="419c4-150">ЧЧ:ММ:СС...</span><span class="sxs-lookup"><span data-stu-id="419c4-150">format.</span></span> <span data-ttu-id="419c4-151">Например,</span><span class="sxs-lookup"><span data-stu-id="419c4-151">Eg.</span></span> <span data-ttu-id="419c4-152">"Start" : "00:01:00"</span><span class="sxs-lookup"><span data-stu-id="419c4-152">"Start" : "00:01:00"</span></span>
    
    <span data-ttu-id="419c4-153">При желании условные обозначения можно комбинировать.</span><span class="sxs-lookup"><span data-stu-id="419c4-153">You can mix and match notations as you please.</span></span>
    
    <span data-ttu-id="419c4-154">Кроме того, также поддерживает запуск специального макроса: {наилучшим образом}, который осуществляет toodetermine hello первый «Город» кадр hello содержимого Примечание: (шаг и диапазон игнорируются при начале задано слишком {наиболее})</span><span class="sxs-lookup"><span data-stu-id="419c4-154">Additionally, Start also supports a special Macro:{Best}, which attempts toodetermine hello first “interesting” frame of hello content NOTE: (Step and Range are ignored when Start is set too{Best})</span></span>
  * <span data-ttu-id="419c4-155">По умолчанию Start:{Best}</span><span class="sxs-lookup"><span data-stu-id="419c4-155">Defaults: Start:{Best}</span></span>
* <span data-ttu-id="419c4-156">Формат вывода должно явно предоставляться для каждого формата изображения toobe: Jpg, Png или BmpFormat.</span><span class="sxs-lookup"><span data-stu-id="419c4-156">Output format needs toobe explicitly provided for each Image format: Jpg/Png/BmpFormat.</span></span> <span data-ttu-id="419c4-157">При наличии MES будет соответствовать JpgVideo tooJpgFormat и т. д.</span><span class="sxs-lookup"><span data-stu-id="419c4-157">When present, MES will match JpgVideo tooJpgFormat and so on.</span></span> <span data-ttu-id="419c4-158">Выходнойформат появился новый указанного макроса кодек изображений: {индекс}, требующие toobe присутствует (один раз и только один раз) для форматов вывода изображения.</span><span class="sxs-lookup"><span data-stu-id="419c4-158">OutputFormat introduces a new image-codec specific Macro: {Index}, which needs toobe present (once and only once) for image output formats.</span></span>

## <a name="next-steps"></a><span data-ttu-id="419c4-159">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="419c4-159">Next steps</span></span>

<span data-ttu-id="419c4-160">Вы можете проверить hello [задание выполняется](media-services-check-job-progress.md) при hello отложенные задания кодирования.</span><span class="sxs-lookup"><span data-stu-id="419c4-160">You can check hello [job progress](media-services-check-job-progress.md) while hello encoding job is pending.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="419c4-161">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="419c4-161">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="419c4-162">Отзывы</span><span class="sxs-lookup"><span data-stu-id="419c4-162">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="419c4-163">См. также</span><span class="sxs-lookup"><span data-stu-id="419c4-163">See Also</span></span>
[<span data-ttu-id="419c4-164">Обзор кодирования с помощью служб мультимедиа</span><span class="sxs-lookup"><span data-stu-id="419c4-164">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)

