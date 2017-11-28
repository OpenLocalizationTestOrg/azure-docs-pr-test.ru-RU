---
title: "aaaMultiple входных файлов и свойства компонента с помощью кодировщика Premium - Azure | Документы Microsoft"
description: "В этом разделе объясняется, как toouse setRuntimeProperties toouse несколько входных данных файлов и передать обработчик мультимедиа расширенного рабочего процесса кодировщика мультимедиа toohello пользовательские данные."
services: media-services
documentationcenter: 
author: xpouyat
manager: cfowler
editor: 
ms.assetid: 7fb35bdd-9891-4401-a65b-ef3cc8190e8a
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: xpouyat;anilmur;juliako
ms.openlocfilehash: e14d10fbf9669e0b88e5ba1c519f1ba5e0bafdd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-multiple-input-files-and-component-properties-with-premium-encoder"></a><span data-ttu-id="ea7aa-103">Использование нескольких входных файлов и свойств компонентов в кодировщике Premium</span><span class="sxs-lookup"><span data-stu-id="ea7aa-103">Using multiple input files and component properties with Premium Encoder</span></span>
## <a name="overview"></a><span data-ttu-id="ea7aa-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="ea7aa-104">Overview</span></span>
<span data-ttu-id="ea7aa-105">Существуют сценарии, в которых может потребоваться toocustomize свойства компонента, укажите XML-список Clip содержимое или отправить несколько входных файлов, при отправке задачи с помощью hello **расширенного рабочего процесса кодировщика мультимедиа** обработчика мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-105">There are scenarios in which you might need toocustomize component properties, specify Clip List XML content, or send multiple input files when you submit a task with hello **Media Encoder Premium Workflow** media processor.</span></span> <span data-ttu-id="ea7aa-106">Ниже приведены некоторые примеры.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-106">Some examples are:</span></span>

* <span data-ttu-id="ea7aa-107">Наложения текста на видео и задание hello текстовое значение (например, hello текущая дата) во время выполнения для каждого входного видео.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-107">Overlaying text on video and setting hello text value (for example, hello current date) at runtime for each input video.</span></span>
* <span data-ttu-id="ea7aa-108">Настройка hello клип списка XML (toospecify одно или несколько исходных файлов, с или без обрезки и т. д.).</span><span class="sxs-lookup"><span data-stu-id="ea7aa-108">Customizing hello Clip List XML (toospecify one or several source files, with or without trimming, etc.).</span></span>
* <span data-ttu-id="ea7aa-109">Перекрытия изображение эмблемы на входное видео hello, пока hello видео кодируется.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-109">Overlaying a logo image on hello input video while hello video is encoded.</span></span>
* <span data-ttu-id="ea7aa-110">Кодирование нескольких аудиодорожек на разных языках.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-110">Multiple audio language encoding.</span></span>

<span data-ttu-id="ea7aa-111">toolet hello **расширенного рабочего процесса кодировщика мультимедиа** знать, что некоторые свойства в рабочем процессе hello изменяется при создании задачи hello или отправить несколько входных файлов, имеют toouse строку конфигурации, содержащий  **setRuntimeProperties** и/или **transcodeSource**.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-111">toolet hello **Media Encoder Premium Workflow** know that you are changing some properties in hello workflow when you create hello task or send multiple input files, you have toouse a configuration string that contains **setRuntimeProperties** and/or **transcodeSource**.</span></span> <span data-ttu-id="ea7aa-112">В этом разделе объясняется, каким образом toouse их.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-112">This topic explains how toouse them.</span></span>

## <a name="configuration-string-syntax"></a><span data-ttu-id="ea7aa-113">Синтаксис строки конфигурации</span><span class="sxs-lookup"><span data-stu-id="ea7aa-113">Configuration string syntax</span></span>
<span data-ttu-id="ea7aa-114">tooset строка конфигурации Hello в hello кодирования задач использует XML-документ, который выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ea7aa-114">hello configuration string tooset in hello encoding task uses an XML document that looks like this:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<transcodeRequest>
  <transcodeSource>
  </transcodeSource>
  <setRuntimeProperties>
    <property propertyPath="Media File Input/filename" value="VideoFileName.mp4" />
  </setRuntimeProperties>
</transcodeRequest>
```

<span data-ttu-id="ea7aa-115">Hello ниже приведен код hello C#, который считывает из файла конфигурации XML hello, обновите его с hello право видео имя файла и передает его toohello задач в задании:</span><span class="sxs-lookup"><span data-stu-id="ea7aa-115">hello following is hello C# code that reads hello XML configuration from a file, update it with hello right video filename and passes it toohello task in a job:</span></span>

```c#
string premiumConfiguration = ReadAllText(@"D:\home\site\wwwroot\Presets\SetRuntime.xml").Replace("VideoFileName", myVideoFileName);

// Declare a new job.
IJob job = _context.Jobs.Create("Premium Workflow encoding job");

// Get a media processor reference, and pass tooit hello name of hello 
// processor toouse for hello specific task.
IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Premium Workflow");

// Create a task with hello encoding details, using a string preset.
ITask task = job.Tasks.AddNew("Premium Workflow encoding task",
                              processor,
                              premiumConfiguration,
                              TaskOptions.None);

// Specify hello input assets
task.InputAssets.Add(workflow); // workflow asset
task.InputAssets.Add(video); // video asset with multiple files

// Add an output asset toocontain hello results of hello job. 
// This output is specified as AssetCreationOptions.None, which 
// means hello output asset is not encrypted. 
task.OutputAssets.AddNew("Output asset", AssetCreationOptions.None);
```

## <a name="customizing-component-properties"></a><span data-ttu-id="ea7aa-116">Настройка свойств компонентов</span><span class="sxs-lookup"><span data-stu-id="ea7aa-116">Customizing component properties</span></span>
### <a name="property-with-a-simple-value"></a><span data-ttu-id="ea7aa-117">Свойство с простым значением</span><span class="sxs-lookup"><span data-stu-id="ea7aa-117">Property with a simple value</span></span>
<span data-ttu-id="ea7aa-118">В некоторых случаях бывает полезно toocustomize свойство компонента вместе с файлом hello рабочего процесса, который будет выполнен задачей расширенного рабочего процесса кодировщика мультимедиа toobe.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-118">In some cases, it is useful toocustomize a component property together with hello workflow file that is going toobe executed by Media Encoder Premium Workflow.</span></span>

<span data-ttu-id="ea7aa-119">Предположим, что разработано рабочего процесса, наложений текста на видео текста hello (например, hello текущая дата) должен toobe набора во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-119">Suppose you designed a workflow that overlays text on your videos, and hello text (for example, hello current date) is supposed toobe set at runtime.</span></span> <span data-ttu-id="ea7aa-120">Это можно сделать путем отправки toobe текст hello задайте hello кодирования задач как hello новое значение для свойства текста hello hello наложения компонента.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-120">You can do this by sending hello text toobe set as hello new value for hello text property of hello overlay component from hello encoding task.</span></span> <span data-ttu-id="ea7aa-121">Этот механизм toochange других свойств компонента можно использовать в рабочем процессе hello (например, «hello положение или цвет наложения hello, скоростью hello hello AVC кодировщика и т. д.).</span><span class="sxs-lookup"><span data-stu-id="ea7aa-121">You can use this mechanism toochange other properties of a component in hello workflow (such as hello position or color of hello overlay, hello bitrate of hello AVC encoder, etc.).</span></span>

<span data-ttu-id="ea7aa-122">**setRuntimeProperties** — это свойство в компоненты hello hello рабочего процесса используется toooverride.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-122">**setRuntimeProperties** is used toooverride a property in hello components of hello workflow.</span></span>

<span data-ttu-id="ea7aa-123">Пример:</span><span class="sxs-lookup"><span data-stu-id="ea7aa-123">Example:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="MyInputVideo.mp4" />
      <property propertyPath="/primarySourceFile" value="MyInputVideo.mp4" />
      <property propertyPath="Optional Text Overlay/Text tooImage Converter/text" value="Today is Friday hello 13th of May, 2016"/>
  </setRuntimeProperties>
</transcodeRequest>
```

### <a name="property-with-an-xml-value"></a><span data-ttu-id="ea7aa-124">Свойство со значением XML</span><span class="sxs-lookup"><span data-stu-id="ea7aa-124">Property with an XML value</span></span>
<span data-ttu-id="ea7aa-125">Инкапсуляция tooset свойство, которое ожидает значение XML, с помощью `<![CDATA[ and ]]>`.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-125">tooset a property that expects an XML value, encapsulate by using `<![CDATA[ and ]]>`.</span></span>

<span data-ttu-id="ea7aa-126">Пример:</span><span class="sxs-lookup"><span data-stu-id="ea7aa-126">Example:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="/primarySourceFile" value="start.mxf" />
      <property propertyPath="/inactiveTimeout" value="65" />
      <property propertyPath="clipListXml" value="xxx">
      <extendedValue><![CDATA[<clipList>
        <clip>
          <videoSource>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
        </clipList>]]>
      </extendedValue>
      </property>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

> [!NOTE]
> <span data-ttu-id="ea7aa-127">Убедитесь, что сразу после возврата tooput каретки `<![CDATA[`.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-127">Make sure not tooput a carriage return just after `<![CDATA[`.</span></span>

### <a name="propertypath-value"></a><span data-ttu-id="ea7aa-128">Значение propertyPath</span><span class="sxs-lookup"><span data-stu-id="ea7aa-128">propertyPath value</span></span>
<span data-ttu-id="ea7aa-129">В предыдущих примерах hello был hello propertyPath «/ мультимедийных файлов входных данных и имя файла» или «/ inactiveTimeout» или «clipListXml».</span><span class="sxs-lookup"><span data-stu-id="ea7aa-129">In hello previous examples, hello propertyPath was "/Media File Input/filename" or "/inactiveTimeout" or "clipListXml".</span></span>
<span data-ttu-id="ea7aa-130">Это, как правило, имя hello hello компонента, а затем имя hello hello свойства.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-130">This is, in general, hello name of hello component, then hello name of hello property.</span></span> <span data-ttu-id="ea7aa-131">Hello путь может содержать большее или меньшее число уровней, например «/ primarySourceFile» (так как свойство hello в корне hello hello рабочего процесса) или «/ видео обработки и график наложения и непрозрачности» (так как наложение hello в группе).</span><span class="sxs-lookup"><span data-stu-id="ea7aa-131">hello path can have more or fewer levels, like "/primarySourceFile" (because hello property is at hello root of hello workflow) or "/Video Processing/Graphic Overlay/Opacity" (because hello Overlay is in a group).</span></span>    

<span data-ttu-id="ea7aa-132">toocheck hello путь и имя свойства, используйте hello кнопка, немедленно расположенный возле каждого свойства.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-132">toocheck hello path and property name, use hello action button that is immediately beside each property.</span></span> <span data-ttu-id="ea7aa-133">Вы можете нажать эту управляющую кнопку и выбрать команду **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-133">You can click this action button and select **Edit**.</span></span> <span data-ttu-id="ea7aa-134">При этом будут отображены вы hello фактическое имя свойства hello и непосредственно над ним, hello пространства имен.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-134">This will show you hello actual name of hello property, and immediately above it, hello namespace.</span></span>

![Действие/Изменить](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture6_actionedit.png)

![Свойство](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture7_viewproperty.png)

## <a name="multiple-input-files"></a><span data-ttu-id="ea7aa-137">Несколько входных файлов</span><span class="sxs-lookup"><span data-stu-id="ea7aa-137">Multiple input files</span></span>
<span data-ttu-id="ea7aa-138">Каждая задача отправки toohello **расширенного рабочего процесса кодировщика мультимедиа** требует два средства:</span><span class="sxs-lookup"><span data-stu-id="ea7aa-138">Each task that you submit toohello **Media Encoder Premium Workflow** requires two assets:</span></span>

* <span data-ttu-id="ea7aa-139">Hello сначала он *активов рабочего процесса* , содержащий файл рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-139">hello first one is a *Workflow Asset* that contains a workflow file.</span></span> <span data-ttu-id="ea7aa-140">Файлы рабочего процесса можно создать с помощью hello [конструктора рабочих процессов](media-services-workflow-designer.md).</span><span class="sxs-lookup"><span data-stu-id="ea7aa-140">You can design workflow files by using hello [Workflow Designer](media-services-workflow-designer.md).</span></span>
* <span data-ttu-id="ea7aa-141">Hello второй раз — *актив мультимедиа* , содержащий hello файлов мультимедиа, которое следует tooencode.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-141">hello second one is a *Media Asset* that contains hello media file(s) that you want tooencode.</span></span>

<span data-ttu-id="ea7aa-142">При отправке нескольких toohello файлов мультимедиа **расширенного рабочего процесса кодировщика мультимедиа** кодировщика, применяются следующие ограничения hello:</span><span class="sxs-lookup"><span data-stu-id="ea7aa-142">When you're sending multiple media files toohello **Media Encoder Premium Workflow** encoder, hello following constraints apply:</span></span>

* <span data-ttu-id="ea7aa-143">Все носители hello, файлы должны находиться в hello же *актив мультимедиа*.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-143">All hello media files must be in hello same *Media Asset*.</span></span> <span data-ttu-id="ea7aa-144">Использование нескольких ресурсов мультимедиа не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-144">Using multiple Media Assets is not supported.</span></span>
* <span data-ttu-id="ea7aa-145">Необходимо задать hello первичный файл в этот актив мультимедиа (в идеальном случае это hello основной файл видео, hello кодировщика запрашивается tooprocess).</span><span class="sxs-lookup"><span data-stu-id="ea7aa-145">You must set hello primary file in this Media Asset (ideally, this is hello main video file that hello encoder is asked tooprocess).</span></span>
* <span data-ttu-id="ea7aa-146">Это toopass необходимые данные конфигурации, включающий hello **setRuntimeProperties** и/или **transcodeSource** элемент toohello процессора.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-146">It is necessary toopass configuration data that includes hello **setRuntimeProperties** and/or **transcodeSource** element toohello processor.</span></span>
  * <span data-ttu-id="ea7aa-147">**setRuntimeProperties** toooverride используется свойство filename hello или другому свойству в компонентах hello hello рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-147">**setRuntimeProperties** is used toooverride hello filename property or another property in hello components of hello workflow.</span></span>
  * <span data-ttu-id="ea7aa-148">**transcodeSource** — используется toospecify hello XML-Clip список содержимого.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-148">**transcodeSource** is used toospecify hello Clip List XML content.</span></span>

<span data-ttu-id="ea7aa-149">Подключения в рабочем процессе hello:</span><span class="sxs-lookup"><span data-stu-id="ea7aa-149">Connections in hello workflow:</span></span>

* <span data-ttu-id="ea7aa-150">Если используется один или несколько компонентов входных данных файла мультимедиа и планирование toouse **setRuntimeProperties** toospecify Здравствуйте, имя файла, а затем компонент ПИН-кода hello первичный файл toothem не подключаются.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-150">If you use one or several Media File Input components and plan toouse **setRuntimeProperties** toospecify hello file name, then do not connect hello primary file component pin toothem.</span></span> <span data-ttu-id="ea7aa-151">Убедитесь, что соединение между объектом первичный файл hello и hello входными данными файла носителя отсутствует.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-151">Make sure that there is no connection between hello primary file object and hello Media File Input(s).</span></span>
* <span data-ttu-id="ea7aa-152">Если вы предпочитаете toouse клип списка XML и один компонент источник мультимедиа, затем можно соединить оба.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-152">If you prefer toouse Clip List XML and one Media Source component, then you can connect both together.</span></span>

![Нет соединения с tooMedia первичный файл источника входных данных файла](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture0_nopin.png)

<span data-ttu-id="ea7aa-154">*Если свойство setRuntimeProperties tooset hello filename отсутствует подключение из tooMedia hello первичный файл входных данных файла компонентов.*</span><span class="sxs-lookup"><span data-stu-id="ea7aa-154">*There is no connection from hello primary file tooMedia File Input component(s) if you use setRuntimeProperties tooset hello filename property.*</span></span>

![Подключение из коллекции списка XML tooClip источника списка](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture1_pincliplist.png)

<span data-ttu-id="ea7aa-156">*Можно подключиться tooMedia-Clip списка XML источника и использовать transcodeSource.*</span><span class="sxs-lookup"><span data-stu-id="ea7aa-156">*You can connect Clip List XML tooMedia Source and use transcodeSource.*</span></span>

### <a name="clip-list-xml-customization"></a><span data-ttu-id="ea7aa-157">Настройка XML-файла со списком клипов</span><span class="sxs-lookup"><span data-stu-id="ea7aa-157">Clip List XML customization</span></span>
<span data-ttu-id="ea7aa-158">Можно указать hello клип списка XML в рабочем процессе hello во время выполнения с помощью **transcodeSource** в конфигурации hello строки XML.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-158">You can specify hello Clip List XML in hello workflow at runtime by using **transcodeSource** in hello configuration string XML.</span></span> <span data-ttu-id="ea7aa-159">Это требуется hello клип списка XML ПИН-код toobe подключен toohello источник мультимедиа компонент в рабочем процессе hello.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-159">This requires hello Clip List XML pin toobe connected toohello Media Source component in hello workflow.</span></span>

```xml
<?xml version="1.0" encoding="utf-16"?>
  <transcodeRequest>
    <transcodeSource>
      <clipList>
        <clip>
          <videoSource>
            <mediaFile>
              <file>video-part1.mp4</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <mediaFile>
              <file>video-part1.mp4</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
      </clipList>
    </transcodeSource>
    <setRuntimeProperties>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

<span data-ttu-id="ea7aa-160">Если вы хотите toouse /primarySourceFile toospecify этих выходных данных свойство tooname hello файлов при помощи «Expressions», то рекомендуется передача hello клип списка XML как свойство *после* свойство /primarySourceFile hello, tooavoid наличие hello картинки переопределяться /primarySourceFile приветствия.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-160">If you want toospecify /primarySourceFile toouse this property tooname hello output files by using 'Expressions', then we recommend passing hello Clip List XML as a property *after* hello /primarySourceFile property, tooavoid having hello Clip List be overridden by hello /primarySourceFile setting.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="/primarySourceFile" value="c:\temp\start.mxf" />
      <property propertyPath="/inactiveTimeout" value="65" />
      <property propertyPath="clipListXml" value="xxx">
      <extendedValue><![CDATA[<clipList>
        <clip>
          <videoSource>
            <mediaFile>
              <file>c:\temp\start.mxf</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <mediaFile>
              <file>c:\temp\start.mxf</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
        </clipList>]]>
      </extendedValue>
      </property>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

<span data-ttu-id="ea7aa-161">Ниже приведен код с дополнительной точной обрезкой кадров.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-161">With additional frame-accurate trimming:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="/primarySourceFile" value="start.mxf" />
      <property propertyPath="/inactiveTimeout" value="65" />
      <property propertyPath="clipListXml" value="xxx">
      <extendedValue><![CDATA[<clipList>
        <clip>
          <videoSource>
            <trim>
              <inPoint fps="25">00:00:05:24</inPoint>
              <outPoint fps="25">00:00:10:24</outPoint>
            </trim>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <trim>
              <inPoint fps="25">00:00:05:24</inPoint>
              <outPoint fps="25">00:00:10:24</outPoint>
            </trim>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
        </clipList>]]>
      </extendedValue>
      </property>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

## <a name="example-1--overlay-an-image-on-top-of-hello-video"></a><span data-ttu-id="ea7aa-162">Пример 1: Наложение изображение поверх видео hello</span><span class="sxs-lookup"><span data-stu-id="ea7aa-162">Example 1 : Overlay an image on top of hello video</span></span>

### <a name="presentation"></a><span data-ttu-id="ea7aa-163">Уровень представления</span><span class="sxs-lookup"><span data-stu-id="ea7aa-163">Presentation</span></span>
<span data-ttu-id="ea7aa-164">Рассмотрим пример, в котором нужно toooverlay изображение эмблемы на входное видео hello во время кодирования видео hello.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-164">Consider an example in which you want toooverlay a logo image on hello input video while hello video is encoded.</span></span> <span data-ttu-id="ea7aa-165">В этом примере hello входное видео с именем «Microsoft_HoloLens_Possibilities_816p24.mp4» и эмблема hello называется «logo.png».</span><span class="sxs-lookup"><span data-stu-id="ea7aa-165">In this example, hello input video is named "Microsoft_HoloLens_Possibilities_816p24.mp4" and hello logo is named "logo.png".</span></span> <span data-ttu-id="ea7aa-166">Необходимо выполнить следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ea7aa-166">You should perform hello following steps:</span></span>

* <span data-ttu-id="ea7aa-167">Создание активов рабочего процесса с файлом hello рабочих процессов (см. следующий пример hello).</span><span class="sxs-lookup"><span data-stu-id="ea7aa-167">Create a Workflow Asset with hello workflow file (see hello following example).</span></span>
* <span data-ttu-id="ea7aa-168">Создать актив мультимедиа, который содержит два файла: MyInputVideo.mp4 как hello первичный файл и MyLogo.png.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-168">Create a Media Asset, which contains two files: MyInputVideo.mp4 as hello primary file and MyLogo.png.</span></span>
* <span data-ttu-id="ea7aa-169">Отправка toohello задача расширенного рабочего процесса кодировщика мультимедиа media ресурсы процессора с hello выше входных данных и укажите hello, следующая строка конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-169">Send a task toohello Media Encoder Premium Workflow media processor with hello above input assets and specify hello following configuration string.</span></span>

<span data-ttu-id="ea7aa-170">Конфигурация:</span><span class="sxs-lookup"><span data-stu-id="ea7aa-170">Configuration:</span></span>

```xml
<?xml version="1.0" encoding="utf-16"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="/primarySourceFile" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

<span data-ttu-id="ea7aa-171">В приведенном выше примере hello имя hello hello видеофайл отправляется toohello вход файл мультимедиа компонента и hello primarySourceFile свойство.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-171">In hello example above, hello name of hello video file is sent toohello Media File Input component and hello primarySourceFile property.</span></span> <span data-ttu-id="ea7aa-172">Имя файла логотипа hello Hello отправляется tooanother входных данных файла мультимедиа, являющийся компонентом графические наложения подключенных toohello.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-172">hello name of hello logo file is sent tooanother Media File Input that is connected toohello graphic overlay component.</span></span>

> [!NOTE]
> <span data-ttu-id="ea7aa-173">Имя файла видео Hello отправляется toohello primarySourceFile свойство.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-173">hello video file name is sent toohello primarySourceFile property.</span></span> <span data-ttu-id="ea7aa-174">Здравствуйте, причиной этого является toouse это свойство в рабочем процессе hello для построения с помощью выражений, например имя hello правильный выходного файла.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-174">hello reason for this is toouse this property in hello workflow for building hello correct output file name using Expressions, for example.</span></span>

### <a name="step-by-step-workflow-creation"></a><span data-ttu-id="ea7aa-175">Пошаговое создание рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="ea7aa-175">Step-by-step workflow creation</span></span>
<span data-ttu-id="ea7aa-176">Ниже приведены шаги toocreate hello рабочий процесс, который принимает в качестве входных данных два файла: видео и изображения.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-176">Here are hello steps toocreate a workflow that takes two files as input: a video and an image.</span></span> <span data-ttu-id="ea7aa-177">Он отправляет сообщение hello изображение поверх видео hello.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-177">It will overlay hello image on top of hello video.</span></span>

<span data-ttu-id="ea7aa-178">Откройте **конструктор рабочих процессов** и последовательно щелкните **Файл** > **Создать рабочую область** > **Схема перекодирования**.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-178">Open **Workflow Designer** and select **File** > **New Workspace** > **Transcode Blueprint**.</span></span>

<span data-ttu-id="ea7aa-179">новый рабочий процесс Hello показано три элемента:</span><span class="sxs-lookup"><span data-stu-id="ea7aa-179">hello new workflow shows three elements:</span></span>

* <span data-ttu-id="ea7aa-180">основной исходный файл;</span><span class="sxs-lookup"><span data-stu-id="ea7aa-180">Primary Source File</span></span>
* <span data-ttu-id="ea7aa-181">XML-файл списка клипов;</span><span class="sxs-lookup"><span data-stu-id="ea7aa-181">Clip List XML</span></span>
* <span data-ttu-id="ea7aa-182">выходной файл и ресурс-контейнер.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-182">Output File/Asset</span></span>  

![Новый рабочий процесс кодирования](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture9_empty.png)

<span data-ttu-id="ea7aa-184">*Новый рабочий процесс кодирования*</span><span class="sxs-lookup"><span data-stu-id="ea7aa-184">*New Encoding Workflow*</span></span>

<span data-ttu-id="ea7aa-185">В порядке tooaccept hello входного файла мультимедиа начните с добавления компонент входного файла мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-185">In order tooaccept hello input media file, start with adding a Media File Input component.</span></span> <span data-ttu-id="ea7aa-186">tooadd toohello рабочего процесса компонента, искать его в поле поиска репозитория hello и перетащите hello требуемого входа на панель конструктора hello.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-186">tooadd a component toohello workflow, look for it in hello Repository search box and drag hello desired entry onto hello designer pane.</span></span>

<span data-ttu-id="ea7aa-187">Затем добавьте toobe hello видеофайлов, используемых при разработке рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-187">Next, add hello video file toobe used for designing your workflow.</span></span> <span data-ttu-id="ea7aa-188">toodo таким образом, нажмите кнопку область фона hello в конструкторе рабочих процессов и найдите свойство hello основной исходный файл на панели справа свойство hello.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-188">toodo so, click hello background pane in Workflow Designer and look for hello Primary Source File property on hello right-hand property pane.</span></span> <span data-ttu-id="ea7aa-189">Щелкните значок папки hello и выберите соответствующий файл видео hello.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-189">Click hello folder icon and select hello appropriate video file.</span></span>

![Основной источник файла](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture10_primaryfile.png)

<span data-ttu-id="ea7aa-191">*Основной источник файла*</span><span class="sxs-lookup"><span data-stu-id="ea7aa-191">*Primary File Source*</span></span>

<span data-ttu-id="ea7aa-192">Затем укажите видеофайл hello в компоненте hello входных данных файла мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-192">Next, specify hello video file in hello Media File Input component.</span></span>   

![Источник входного файла мультимедиа](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture11_mediafileinput.png)

<span data-ttu-id="ea7aa-194">*Источник входного файла мультимедиа*</span><span class="sxs-lookup"><span data-stu-id="ea7aa-194">*Media File Input Source*</span></span>

<span data-ttu-id="ea7aa-195">Сразу же после этого компонент hello входных данных файла мультимедиа Проверьте файл hello и заполнения его выходной ПИН-кодов tooreflect hello файл, который его изучить.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-195">As soon as this is done, hello Media File Input component will inspect hello file and populate its output pins tooreflect hello file that it inspected.</span></span>

<span data-ttu-id="ea7aa-196">Hello следующим шагом является tooadd tooRec.709 пространства toospecify hello «Видео данных тип обновления» цвета.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-196">hello next step is tooadd a "Video Data Type Updater" toospecify hello color space tooRec.709.</span></span> <span data-ttu-id="ea7aa-197">Добавить «Видео формата преобразователь», заданный тип макета и макета tooData = плоские можно настроить.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-197">Add a "Video Format Converter" that is set tooData Layout/Layout type = Configurable Planar.</span></span> <span data-ttu-id="ea7aa-198">Это преобразует hello видеопотока tooa формат, который может считаться исходного компонента наложения hello.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-198">This will convert hello video stream tooa format that can be taken as a source of hello overlay component.</span></span>

![Компоненты "Обновление типа видеоданных" и "Конвертер форматов видео"](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter.png)

<span data-ttu-id="ea7aa-200">*Компоненты "Обновление типа видеоданных" и "Конвертер форматов видео"*</span><span class="sxs-lookup"><span data-stu-id="ea7aa-200">*Video Data Type Updater and Format Converter*</span></span>

![Тип макета — Configurable Planar (Настраиваемый переключатель)](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter2.png)

<span data-ttu-id="ea7aa-202">*Тип макета — "Configurable Planar"*</span><span class="sxs-lookup"><span data-stu-id="ea7aa-202">*Layout type is Configurable Planar*</span></span>

<span data-ttu-id="ea7aa-203">Затем добавьте компонент наложения видео и подключения hello (без сжатия) видео ПИН-код toohello (без сжатия) видео контакта входного файла мультимедиа hello.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-203">Next, add a Video Overlay component and connect hello (uncompressed) video pin toohello (uncompressed) video pin of hello media file input.</span></span>

<span data-ttu-id="ea7aa-204">Добавления другой входного файла мультимедиа (файл эмблемы hello tooload), щелкните этот компонент и переименуйте его слишком «Logo входных данных файла мультимедиа», а затем выберите образ (PNG-файл для примера) свойство файла hello.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-204">Add another Media File Input (tooload hello logo file), click on this component and rename it too"Media File Input Logo", and select an image (a .png file for example) in hello file property.</span></span> <span data-ttu-id="ea7aa-205">Подключения контакта hello без сжатия изображения ПИН-код toohello без сжатия изображения hello наложения.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-205">Connect hello Uncompressed image pin toohello Uncompressed image pin of hello overlay.</span></span>

![Компонент наложения и источник файла изображения](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture13_overlay.png)

<span data-ttu-id="ea7aa-207">*Компонент наложения и источник файла изображения*</span><span class="sxs-lookup"><span data-stu-id="ea7aa-207">*Overlay component and image file source*</span></span>

<span data-ttu-id="ea7aa-208">Если следует toomodify положение hello hello эмблемы на видео hello (например, может потребоваться tooposition на 10 процентов от верхней hello левом углу hello видео), снимите флажок «Ручной ввод» hello.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-208">If you want toomodify hello position of hello logo on hello video (for example, you might want tooposition it at 10 percent off of hello top left corner of hello video), clear hello "Manual Input" check box.</span></span> <span data-ttu-id="ea7aa-209">Это можно сделать, так как вы используете входных данных файла мультимедиа tooprovide hello логотип файл toohello наложения компонента.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-209">You can do this because you are using a Media File Input tooprovide hello logo file toohello overlay component.</span></span>

![Положение наложения](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture14_overlay_position.png)

<span data-ttu-id="ea7aa-211">*Положение наложения*</span><span class="sxs-lookup"><span data-stu-id="ea7aa-211">*Overlay position*</span></span>

<span data-ttu-id="ea7aa-212">tooencode hello tooH.264 потокового видео, добавьте hello кодировщик видео AVC и AAC кодировщика компонентов toohello рабочую область конструктора.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-212">tooencode hello video stream tooH.264, add hello AVC Video Encoder and AAC encoder components toohello designer surface.</span></span> <span data-ttu-id="ea7aa-213">Подключите hello ПИН-кодов.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-213">Connect hello pins.</span></span>
<span data-ttu-id="ea7aa-214">Настройка кодировщика AAC hello и выберите преобразование формата аудио/стиль: 2.0 ("L", "R").</span><span class="sxs-lookup"><span data-stu-id="ea7aa-214">Set up hello AAC encoder and select Audio Format Conversion/Preset : 2.0 (L, R).</span></span>

![Кодировщики аудио и видео](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture15_encoders.png)

<span data-ttu-id="ea7aa-216">*Кодировщики аудио и видео*</span><span class="sxs-lookup"><span data-stu-id="ea7aa-216">*Audio and Video Encoders*</span></span>

<span data-ttu-id="ea7aa-217">Теперь добавьте hello **ISO Mpeg-4 мультиплексор** и **выходной файл** компоненты и подключите hello ПИН-коды, как показано.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-217">Now add hello **ISO Mpeg-4 Multiplexer** and **File Output** components and connect hello pins as shown.</span></span>

![Мультиплексор MP4 и вывод файла](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture16_mp4output.png)

<span data-ttu-id="ea7aa-219">*Мультиплексор MP4 и вывод файла*</span><span class="sxs-lookup"><span data-stu-id="ea7aa-219">*MP4 multiplexer and file output*</span></span>

<span data-ttu-id="ea7aa-220">Требуется имя hello tooset для hello выходного файла.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-220">You need tooset hello name for hello output file.</span></span> <span data-ttu-id="ea7aa-221">Нажмите кнопку hello **выходной файл** компонента и измените выражение hello hello файла:</span><span class="sxs-lookup"><span data-stu-id="ea7aa-221">Click hello **File Output** component and edit hello expression for hello file:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_withoverlay.mp4

![Имя вывода файла](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture17_filenameoutput.png)

<span data-ttu-id="ea7aa-223">*Имя вывода файла*</span><span class="sxs-lookup"><span data-stu-id="ea7aa-223">*File output name*</span></span>

<span data-ttu-id="ea7aa-224">Можно запустить рабочий процесс hello локально toocheck, на котором работает правильно.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-224">You can run hello workflow locally toocheck that it is running correctly.</span></span>

<span data-ttu-id="ea7aa-225">После завершения его можно запустить в службах мультимедиа Azure.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-225">After it finishes, you can run it in Azure Media Services.</span></span>

<span data-ttu-id="ea7aa-226">Во-первых, Подготовка актива в службах мультимедиа Azure с двумя файлами в нем: hello видеофайлов и эмблема hello.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-226">First, prepare an asset in Azure Media Services with two files in it: hello video file and hello logo.</span></span> <span data-ttu-id="ea7aa-227">Это можно сделать с помощью hello .NET или REST API.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-227">You can do this by using hello .NET or REST API.</span></span> <span data-ttu-id="ea7aa-228">Также это можно сделать с помощью портала Azure hello или [обозреватель служб мультимедиа Azure](https://github.com/Azure/Azure-Media-Services-Explorer) (AMSE).</span><span class="sxs-lookup"><span data-stu-id="ea7aa-228">You can also do this by using hello Azure portal or [Azure Media Services Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (AMSE).</span></span>

<span data-ttu-id="ea7aa-229">В этом учебнике показано как активы toomanage с AMSE.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-229">This tutorial shows you how toomanage assets with AMSE.</span></span> <span data-ttu-id="ea7aa-230">Существует два способа tooadd файлы tooan активов.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-230">There are two ways tooadd files tooan asset:</span></span>

* <span data-ttu-id="ea7aa-231">Создать локальную папку, скопируйте файлы hello двумя и перетащите toohello папку hello **активов** вкладки.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-231">Create a local folder, copy hello two files in it, and drag and drop hello folder toohello **Asset** tab.</span></span>
* <span data-ttu-id="ea7aa-232">Передача hello видеофайл как основное средство, отобразить сведения об активе hello, перейдите на вкладку файлы toohello и передать дополнительный файл (эмблема).</span><span class="sxs-lookup"><span data-stu-id="ea7aa-232">Upload hello video file as an asset, display hello asset information, go toohello files tab, and upload an additional file (logo).</span></span>

> [!NOTE]
> <span data-ttu-id="ea7aa-233">Сделать tooset убедиться, что первичный файл в ресурсе hello (hello основного видео-файл).</span><span class="sxs-lookup"><span data-stu-id="ea7aa-233">Make sure tooset a primary file in hello asset (hello main video file).</span></span>

![Файлы ресурсов в AMSE](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture18_assetinamse.png)

<span data-ttu-id="ea7aa-235">*Файлы ресурсов в AMSE*</span><span class="sxs-lookup"><span data-stu-id="ea7aa-235">*Asset files in AMSE*</span></span>

<span data-ttu-id="ea7aa-236">Выберите средство hello и выберите tooencode с помощью кодировщика Premium.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-236">Select hello asset and choose tooencode it with Premium Encoder.</span></span> <span data-ttu-id="ea7aa-237">Отправить рабочий процесс hello и выберите его.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-237">Upload hello workflow and select it.</span></span>

<span data-ttu-id="ea7aa-238">Щелкните hello кнопка toopass данных toohello процессора и добавьте следующие свойства среды выполнения hello tooset XML hello.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-238">Click hello button toopass data toohello processor, and add hello following XML tooset hello runtime properties:</span></span>

![Кодировщик Premium в AMSE](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture19_amsepremium.png)

<span data-ttu-id="ea7aa-240">*Кодировщик Premium в AMSE*</span><span class="sxs-lookup"><span data-stu-id="ea7aa-240">*Premium Encoder in AMSE*</span></span>

<span data-ttu-id="ea7aa-241">Вставьте hello следующие XML-данных.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-241">Then, paste hello following XML data.</span></span> <span data-ttu-id="ea7aa-242">Требуется имя hello toospecify hello видеофайла hello входных данных файла мультимедиа и primarySourceFile.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-242">You need toospecify hello name of hello video file for both hello Media File Input and primarySourceFile.</span></span> <span data-ttu-id="ea7aa-243">Укажите имя hello hello имя файла для логотипа hello слишком.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-243">Specify hello name of hello file name for hello logo too.</span></span>

```xml
<?xml version="1.0" encoding="utf-16"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="/primarySourceFile" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

![setRuntimeProperties](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture20_amsexmldata.png)

<span data-ttu-id="ea7aa-245">*setRuntimeProperties*</span><span class="sxs-lookup"><span data-stu-id="ea7aa-245">*setRuntimeProperties*</span></span>

<span data-ttu-id="ea7aa-246">Если вы используете .NET SDK toocreate hello и запуска задачи «hello», этот XML-данных имеет toobe передаются как строка hello конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-246">If you use hello .NET SDK toocreate and run hello task, this XML data has toobe passed as hello configuration string.</span></span>

```c#
public ITask AddNew(string taskName, IMediaProcessor mediaProcessor, string configuration, TaskOptions options);
```

<span data-ttu-id="ea7aa-247">После завершения задания hello hello MP4-файл в hello выходные данные средства, которое отображает hello наложения!</span><span class="sxs-lookup"><span data-stu-id="ea7aa-247">After hello job is complete, hello MP4 file in hello output asset displays hello overlay!</span></span>

![Наложение на hello видео](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture21_resultoverlay.png)

<span data-ttu-id="ea7aa-249">*Наложение на hello видео*</span><span class="sxs-lookup"><span data-stu-id="ea7aa-249">*Overlay on hello video*</span></span>

<span data-ttu-id="ea7aa-250">Вы можете загрузить пример hello рабочего процесса из [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/).</span><span class="sxs-lookup"><span data-stu-id="ea7aa-250">You can download hello sample workflow from [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/).</span></span>

## <a name="example-2--multiple-audio-language-encoding"></a><span data-ttu-id="ea7aa-251">Пример 2. Кодирование нескольких аудиодорожек на разных языках</span><span class="sxs-lookup"><span data-stu-id="ea7aa-251">Example 2 : Multiple audio language encoding</span></span>

<span data-ttu-id="ea7aa-252">Пример рабочего процесса кодирования нескольких аудиодорожек на разных языках доступен в [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/MultilanguageAudioEncoding).</span><span class="sxs-lookup"><span data-stu-id="ea7aa-252">An example of multiple audio language encoding workfkow is available in [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/MultilanguageAudioEncoding).</span></span>

<span data-ttu-id="ea7aa-253">Эта папка содержит образец рабочего процесса, который можно использовать tooencode ресурс MXF файл tooa несколькими MP4 файлы с нескольких звуковых дорожек.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-253">This folder contains a sample workflow which can be used tooencode a MXF file tooa multi MP4 files asset with multiple audio tracks.</span></span>

<span data-ttu-id="ea7aa-254">Этот рабочий процесс предполагает, что этот файл MXF hello содержит один звуковой дорожки; Hello дополнительных звуковые дорожки должны передаваться как отдельные файлы звука (WAV или MP4...).</span><span class="sxs-lookup"><span data-stu-id="ea7aa-254">This workflow assumes that hello MXF file contains one audio track ; hello additional audio tracks should be passed as seperate audio files (WAV or MP4...).</span></span>

<span data-ttu-id="ea7aa-255">tooencode, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="ea7aa-255">tooencode, please follow these steps:</span></span>

* <span data-ttu-id="ea7aa-256">Создайте актив служб мультимедиа с помощью файла MXF hello и hello звуковые файлы (0 too18 аудио).</span><span class="sxs-lookup"><span data-stu-id="ea7aa-256">Create a Media Services asset with hello MXF file and hello Audio files (0 too18 audio files).</span></span>
* <span data-ttu-id="ea7aa-257">Убедитесь, что этот файл MXF hello задан как первичный файл.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-257">Make sure that hello MXF file is set as a primary file.</span></span>
* <span data-ttu-id="ea7aa-258">Создание заданий и задач, с помощью обработчика рабочего процесса кодировщика Premium hello.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-258">Create a job and a task using hello Premium Workflow Encoder processor.</span></span> <span data-ttu-id="ea7aa-259">Используйте рабочий процесс hello, предоставляемые (MultiMP4-1080p-19audio-v1.workflow).</span><span class="sxs-lookup"><span data-stu-id="ea7aa-259">Use hello workflow provided (MultiMP4-1080p-19audio-v1.workflow).</span></span>
* <span data-ttu-id="ea7aa-260">Передайте задачу toohello hello setruntime.xml данных (если используется обозреватель служб мультимедиа Azure, кнопка «передать рабочего процесса toohello данных xml» hello ").</span><span class="sxs-lookup"><span data-stu-id="ea7aa-260">Pass hello setruntime.xml data toohello task (if you use Azure Media Services Explorer, use hello “pass xml data toohello workflow” button).</span></span>
  * <span data-ttu-id="ea7aa-261">Обновите hello XML данных toospecify hello правильный файл языки и имена тегов.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-261">Please update hello XML data toospecify hello correct file names and languages tags.</span></span>
  * <span data-ttu-id="ea7aa-262">Hello рабочий процесс состоит из аудио компонентов с именем tooAudio аудио 1 18.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-262">hello workflow has audio components named Audio 1 tooAudio 18.</span></span>
  * <span data-ttu-id="ea7aa-263">RFC5646 поддерживается для тега языка hello.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-263">RFC5646 is supported for hello language tag.</span></span>

```xml
<?xml version="1.0" encoding="utf-16"?>
<transcodeRequest>
  <setRuntimeProperties>
    <property propertyPath="Media File Input Video/filename" value="MainVideo.mxf" />
    <property propertyPath="Language/language_code" value="en" />
    <property propertyPath="/primarySourceFile" value="MainVideo.mxf" />
    <property propertyPath="Audio 1/Media File Input/filename" value="french-audio.wav" />
    <property propertyPath="Audio 1/Language/language_code" value="fr" />
    <property propertyPath="Audio 2/Media File Input/filename" value="german-audio.wav" />
    <property propertyPath="Audio 2/Language/language_code" value="de" />
    <property propertyPath="Audio 3/Media File Input/filename" value="japanese-audio.wav" />
    <property propertyPath="Audio 3/Language/language_code" value="ja" />
  </setRuntimeProperties>
</transcodeRequest>
```

* <span data-ttu-id="ea7aa-264">Hello кодировке активов будет содержать звуковые дорожки нескольких языков и эти записи должно быть доступным для выбора в Azure Media Player.</span><span class="sxs-lookup"><span data-stu-id="ea7aa-264">hello encoded asset will contain multi language audio tracks and these tracks should be selectable in Azure Media Player.</span></span>

## <a name="see-also"></a><span data-ttu-id="ea7aa-265">См. также</span><span class="sxs-lookup"><span data-stu-id="ea7aa-265">See also</span></span>
* [<span data-ttu-id="ea7aa-266">Знакомство со Службой кодирования категории "Премиум" в службах мультимедиа Azure</span><span class="sxs-lookup"><span data-stu-id="ea7aa-266">Introducing Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)
* [<span data-ttu-id="ea7aa-267">Как toouse расширенной кодировки в службах мультимедиа Azure</span><span class="sxs-lookup"><span data-stu-id="ea7aa-267">How toouse Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)
* [<span data-ttu-id="ea7aa-268">Обзор и сравнение кодировщиков мультимедиа Azure по запросу</span><span class="sxs-lookup"><span data-stu-id="ea7aa-268">Encoding on-demand content with Azure Media Services</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)
* [<span data-ttu-id="ea7aa-269">Форматы и кодеки рабочего процесса Premium Media Encoder</span><span class="sxs-lookup"><span data-stu-id="ea7aa-269">Media Encoder Premium Workflow formats and codecs</span></span>](media-services-premium-workflow-encoder-formats.md)
* [<span data-ttu-id="ea7aa-270">Примеры файлов рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="ea7aa-270">Sample workflow files</span></span>](https://github.com/AzureMediaServicesSamples/Encoding-Presets/tree/master/VoD/MediaEncoderPremiumWorkfows)
* [<span data-ttu-id="ea7aa-271">Средство Explorer для служб мультимедиа Azure</span><span class="sxs-lookup"><span data-stu-id="ea7aa-271">Azure Media Services Explorer tool</span></span>](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a><span data-ttu-id="ea7aa-272">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="ea7aa-272">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ea7aa-273">Отзывы</span><span class="sxs-lookup"><span data-stu-id="ea7aa-273">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
