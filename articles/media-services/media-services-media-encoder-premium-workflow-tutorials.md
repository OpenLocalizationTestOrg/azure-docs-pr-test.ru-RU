---
title: "учебники по aaaAvanced расширенного рабочего процесса кодировщика мультимедиа"
description: "Этот документ содержит примеры, показывающие, как tooperform сложных задач с помощью расширенного рабочего процесса кодировщика мультимедиа и также как toocreate сложных рабочих процессов с помощью конструктора рабочих процессов."
services: media-services
documentationcenter: 
author: xstof
manager: cfowler
editor: 
ms.assetid: 1ba52865-b4a8-4ca0-ac96-920d55b9d15b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: christoc;xpouyat;juliako
ms.openlocfilehash: 641bd1be3bd795b5e138fa7ffdf299ff6710904e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-media-encoder-premium-workflow-tutorials"></a><span data-ttu-id="3c217-103">Руководства по расширенному рабочему процессу кодировщика мультимедиа</span><span class="sxs-lookup"><span data-stu-id="3c217-103">Advanced Media Encoder Premium Workflow tutorials</span></span>
## <a name="overview"></a><span data-ttu-id="3c217-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="3c217-104">Overview</span></span>
<span data-ttu-id="3c217-105">Этот документ содержит пошаговые руководства, которые показывают, как toocustomize рабочих процессов с **конструктора рабочих процессов**.</span><span class="sxs-lookup"><span data-stu-id="3c217-105">This document contains walkthroughs that show how toocustomize workflows with  **Workflow Designer**.</span></span> <span data-ttu-id="3c217-106">Найти hello файлы фактического рабочего процесса [здесь](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/PremiumEncoderWorkflowSamples).</span><span class="sxs-lookup"><span data-stu-id="3c217-106">You can find hello actual workflow files [here](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/PremiumEncoderWorkflowSamples).</span></span>  

## <a name="toc"></a><span data-ttu-id="3c217-107">ОГЛАВЛЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="3c217-107">TOC</span></span>
<span data-ttu-id="3c217-108">рассматриваются следующие вопросы Hello.</span><span class="sxs-lookup"><span data-stu-id="3c217-108">hello following topics are covered:</span></span>

* [<span data-ttu-id="3c217-109">Кодирование MXF в файл MP4 с одной скоростью</span><span class="sxs-lookup"><span data-stu-id="3c217-109">Encoding MXF into a single bitrate MP4</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)
  * [<span data-ttu-id="3c217-110">Запуск нового рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="3c217-110">Starting a new workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_start_new)
  * [<span data-ttu-id="3c217-111">С помощью hello вход файл мультимедиа</span><span class="sxs-lookup"><span data-stu-id="3c217-111">Using hello Media File Input</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_file_input)
  * [<span data-ttu-id="3c217-112">Проверка потоков мультимедиа</span><span class="sxs-lookup"><span data-stu-id="3c217-112">Inspecting media streams</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_streams)
  * [<span data-ttu-id="3c217-113">Добавление видеокодировщика для создания файла MP4</span><span class="sxs-lookup"><span data-stu-id="3c217-113">Adding a video encoder for .MP4 file generation</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_file_generation)
  * [<span data-ttu-id="3c217-114">Кодировки аудиопотока hello</span><span class="sxs-lookup"><span data-stu-id="3c217-114">Encoding hello audio stream</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio)
  * [<span data-ttu-id="3c217-115">Мультиплексирование аудио- и видеопотоков в контейнер MP4</span><span class="sxs-lookup"><span data-stu-id="3c217-115">Multiplexing Audio and Video streams into an MP4 container</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio_and_fideo)
  * [<span data-ttu-id="3c217-116">Запись файла MP4 hello</span><span class="sxs-lookup"><span data-stu-id="3c217-116">Writing hello MP4 file</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_writing_mp4)
  * [<span data-ttu-id="3c217-117">Создание из выходного файла hello ресурс служб мультимедиа</span><span class="sxs-lookup"><span data-stu-id="3c217-117">Creating a Media Services Asset from hello output file</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_asset_from_output)
  * [<span data-ttu-id="3c217-118">Hello тест завершения рабочего процесса локально</span><span class="sxs-lookup"><span data-stu-id="3c217-118">Test hello finished workflow locally</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_test)
* [<span data-ttu-id="3c217-119">Кодирование MXF в файлы MP4 с несколькими скоростями со включенной динамической упаковкой</span><span class="sxs-lookup"><span data-stu-id="3c217-119">Encoding MXF into multibitrate MP4s - dynamic packaging enabled</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging)
  * [<span data-ttu-id="3c217-120">Добавление одного или нескольких дополнительных выходных файлов MP4</span><span class="sxs-lookup"><span data-stu-id="3c217-120">Adding one or more additional MP4 outputs</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_more_outputs)
  * [<span data-ttu-id="3c217-121">Настройка имен вывод файлов hello</span><span class="sxs-lookup"><span data-stu-id="3c217-121">Configuring hello file output names</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_conf_output_names)
  * [<span data-ttu-id="3c217-122">Добавление отдельной звуковой дорожки</span><span class="sxs-lookup"><span data-stu-id="3c217-122">Adding a separate Audio Track</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_audio_tracks)
  * [<span data-ttu-id="3c217-123">Добавление hello. SMIL ISM-файла</span><span class="sxs-lookup"><span data-stu-id="3c217-123">Adding hello .ISM SMIL File</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_ism_file)
* [<span data-ttu-id="3c217-124">Расширенная схема кодирования файла MXF в файл MP4 с несколькими скоростями</span><span class="sxs-lookup"><span data-stu-id="3c217-124">Encoding MXF into multibitrate MP4 - enhanced blueprint</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4)
  * [<span data-ttu-id="3c217-125">Общие сведения о tooenhance рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="3c217-125">Workflow overview tooenhance</span></span>](#workflow-overview-to-enhance)
  * [<span data-ttu-id="3c217-126">Соглашения об именовании файлов</span><span class="sxs-lookup"><span data-stu-id="3c217-126">File Naming Conventions</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_file_naming)
  * [<span data-ttu-id="3c217-127">Свойства публикации компонента на hello корневого рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="3c217-127">Publishing component properties onto hello workflow root</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_publishing)
  * [<span data-ttu-id="3c217-128">Создание зависимости имен созданных выходных файлов от значений опубликованных свойств</span><span class="sxs-lookup"><span data-stu-id="3c217-128">Have generated output file names rely on published property values</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_output_files)
* [<span data-ttu-id="3c217-129">Добавление выходных данных MP4 toomultibitrate эскизов</span><span class="sxs-lookup"><span data-stu-id="3c217-129">Adding thumbnails toomultibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4)
  * [<span data-ttu-id="3c217-130">Для эскизов tooadd обзор рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="3c217-130">Workflow overview tooadd thumbnails to</span></span>](#workflow-overview-to-add-thumbnails-to)
  * [<span data-ttu-id="3c217-131">Добавление кодировки JPG</span><span class="sxs-lookup"><span data-stu-id="3c217-131">Adding JPG Encoding</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4__with_jpg)
  * [<span data-ttu-id="3c217-132">Работа с преобразованием цветового пространства</span><span class="sxs-lookup"><span data-stu-id="3c217-132">Dealing with Color Space conversion</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_color_space)
  * [<span data-ttu-id="3c217-133">Написание hello эскизов</span><span class="sxs-lookup"><span data-stu-id="3c217-133">Writing hello thumbnails</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_writing_thumbnails)
  * [<span data-ttu-id="3c217-134">Обнаружение ошибок в рабочем процессе</span><span class="sxs-lookup"><span data-stu-id="3c217-134">Detecting errors in a workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_errors)
  * [<span data-ttu-id="3c217-135">Завершенный рабочий процесс</span><span class="sxs-lookup"><span data-stu-id="3c217-135">Finished Workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_finish)
* [<span data-ttu-id="3c217-136">Обрезка выходных файлов MP4 с несколькими скоростями по времени</span><span class="sxs-lookup"><span data-stu-id="3c217-136">Time-based trimming of multibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim)
  * [<span data-ttu-id="3c217-137">Добавление усечение toostart обзор рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="3c217-137">Workflow overview toostart adding trimming to</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_start)
  * [<span data-ttu-id="3c217-138">С помощью hello поток устройство обрезки</span><span class="sxs-lookup"><span data-stu-id="3c217-138">Using hello Stream Trimmer</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_use_stream_trimmer)
  * [<span data-ttu-id="3c217-139">Завершенный рабочий процесс</span><span class="sxs-lookup"><span data-stu-id="3c217-139">Finished Workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_finish)
* [<span data-ttu-id="3c217-140">Знакомство с hello компонента в скрипт</span><span class="sxs-lookup"><span data-stu-id="3c217-140">Introducing hello Scripted Component</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#scripting)
  * [<span data-ttu-id="3c217-141">Создание сценариев в рабочем процессе: hello world</span><span class="sxs-lookup"><span data-stu-id="3c217-141">Scripting within a workflow: hello world</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#scripting_hello_world)
* [<span data-ttu-id="3c217-142">Обрезка выходных файлов MP4 с несколькими скоростями по кадрам</span><span class="sxs-lookup"><span data-stu-id="3c217-142">Frame-based trimming of multibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim)
  * [<span data-ttu-id="3c217-143">План toostart Общие сведения о добавлении усечение</span><span class="sxs-lookup"><span data-stu-id="3c217-143">Blueprint overview toostart adding trimming to</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_start)
  * [<span data-ttu-id="3c217-144">С помощью hello клип списка XML</span><span class="sxs-lookup"><span data-stu-id="3c217-144">Using hello Clip List XML</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clip_list)
  * [<span data-ttu-id="3c217-145">Изменение списка hello клип из компонента в скрипт</span><span class="sxs-lookup"><span data-stu-id="3c217-145">Modifying hello clip list from a Scripted Component</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_modify_clip_list)
  * [<span data-ttu-id="3c217-146">Добавление удобного свойства ClippingEnabled</span><span class="sxs-lookup"><span data-stu-id="3c217-146">Adding a ClippingEnabled convenience property</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clippingenabled_prop)

## <span data-ttu-id="3c217-147"><a id="MXF_to_MP4"></a>Кодирование MXF в файл MP4 с одной скоростью</span><span class="sxs-lookup"><span data-stu-id="3c217-147"><a id="MXF_to_MP4"></a>Encoding MXF into a single bitrate MP4</span></span>
<span data-ttu-id="3c217-148">В этом разделе мы создадим из входного файла MXF аудиофайл MP4 с одной скоростью, используя кодирование AAC-HE.</span><span class="sxs-lookup"><span data-stu-id="3c217-148">In this walkthrough we'll create a single bitrate .MP4 file with AAC-HE encoded audio from an .MXF input file.</span></span>

### <span data-ttu-id="3c217-149"><a id="MXF_to_MP4_start_new"></a>Запуск нового рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="3c217-149"><a id="MXF_to_MP4_start_new"></a>Starting a new workflow</span></span>
<span data-ttu-id="3c217-150">Откройте конструктор рабочих процессов и последовательно щелкните "Файл" > "Создать рабочую область" > "Схема перекодирования".</span><span class="sxs-lookup"><span data-stu-id="3c217-150">Open Workflow Designer and select "File"-"New Workspace"-"Transcode Blueprint"</span></span>

<span data-ttu-id="3c217-151">Hello новый рабочий процесс будет показывать три элемента:</span><span class="sxs-lookup"><span data-stu-id="3c217-151">hello new workflow will show 3 elements:</span></span>

* <span data-ttu-id="3c217-152">основной исходный файл;</span><span class="sxs-lookup"><span data-stu-id="3c217-152">Primary Source File</span></span>
* <span data-ttu-id="3c217-153">XML-файл списка клипов;</span><span class="sxs-lookup"><span data-stu-id="3c217-153">Clip List XML</span></span>
* <span data-ttu-id="3c217-154">выходной файл и ресурс-контейнер.</span><span class="sxs-lookup"><span data-stu-id="3c217-154">Output File/Asset</span></span>  

![Новый рабочий процесс кодирования](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-transcode-blueprint.png)

<span data-ttu-id="3c217-156">*Новый рабочий процесс кодирования*</span><span class="sxs-lookup"><span data-stu-id="3c217-156">*New Encoding Workflow*</span></span>

### <span data-ttu-id="3c217-157"><a id="MXF_to_MP4_with_file_input"></a>С помощью hello вход файл мультимедиа</span><span class="sxs-lookup"><span data-stu-id="3c217-157"><a id="MXF_to_MP4_with_file_input"></a>Using hello Media File Input</span></span>
<span data-ttu-id="3c217-158">В порядке tooaccept нашей входного файла мультимедиа, один начинается с добавления компонента входного файла мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="3c217-158">In order tooaccept our input media file, one starts with adding a Media File Input component.</span></span> <span data-ttu-id="3c217-159">tooadd toohello рабочего процесса компонента, искать его в поле поиска репозитория hello и перетащите hello требуемого входа на панель конструктора hello.</span><span class="sxs-lookup"><span data-stu-id="3c217-159">tooadd a component toohello workflow, look for it in hello Repository search box and drag hello desired entry onto hello designer pane.</span></span> <span data-ttu-id="3c217-160">Это необходимо сделать для входного файла мультимедиа hello и подключите hello основной исходный файл компонента toohello имя файла ввода ПИН-кода hello входного файла мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="3c217-160">Do this for hello Media File Input and connect hello Primary Source File component toohello Filename input pin from hello Media File Input.</span></span>

![Соединение области "Входные файлы мультимедиа"](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-input.png)

<span data-ttu-id="3c217-162">*Соединение области "Входные файлы мультимедиа"*</span><span class="sxs-lookup"><span data-stu-id="3c217-162">*Connected Media File Input*</span></span>

<span data-ttu-id="3c217-163">Прежде чем мы еще большую мы сначала потребуется конструктора рабочих процессов toohello tooindicate какие образец файла мы хотели бы toouse toodesign с рабочим процессом.</span><span class="sxs-lookup"><span data-stu-id="3c217-163">Before we can do much else, we'll first need tooindicate toohello workflow designer what sample file we'd like toouse toodesign our workflow with.</span></span> <span data-ttu-id="3c217-164">toodo таким образом, щелкните фон конструктора области hello и найдите свойство hello основной исходный файл на панели справа свойство hello.</span><span class="sxs-lookup"><span data-stu-id="3c217-164">toodo so, click hello designer pane background and look for hello Primary Source File property on hello right-hand property pane.</span></span> <span data-ttu-id="3c217-165">Щелкните значок папки hello и выберите hello требуемого файла tootest hello рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="3c217-165">Click hello folder icon and select hello desired file tootest hello workflow with.</span></span> <span data-ttu-id="3c217-166">Сразу же после этого компонент hello входных данных файла мультимедиа Проверьте файл hello и заполнить его выходные данные ПИН-кодов tooreflect hello файл, который его изучить.</span><span class="sxs-lookup"><span data-stu-id="3c217-166">As soon as this is done, hello Media File Input component will inspect hello file and populate its output pins tooreflect hello file it inspected.</span></span>

![Заполненная область "Входные файлы мультимедиа"](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-populated-media-file-input.png)

<span data-ttu-id="3c217-168">*Заполненная область "Входные файлы мультимедиа"*</span><span class="sxs-lookup"><span data-stu-id="3c217-168">*Populated Media File Input*</span></span>

<span data-ttu-id="3c217-169">Хотя указывает с что входе, мы хотели бы toowork с, он не сообщает еще где выходные данные в кодировке hello должен быть доставлен.</span><span class="sxs-lookup"><span data-stu-id="3c217-169">While this specifies with what input we'd like toowork with, it doesn't tell yet where hello encoded output should go to.</span></span> <span data-ttu-id="3c217-170">Аналогичные hello toohow настроенного первичный файл источника теперь настроить hello выходной папки переменной свойства, непосредственно под.</span><span class="sxs-lookup"><span data-stu-id="3c217-170">Similar toohow hello Primary Source File was configured, now configure hello Output Folder Variable property, just below it.</span></span>

![Указанные свойства входных и выходных данных](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configured-io-properties.png)

<span data-ttu-id="3c217-172">*Указанные свойства входных и выходных данных*</span><span class="sxs-lookup"><span data-stu-id="3c217-172">*Configured Input and Output properties*</span></span>

### <span data-ttu-id="3c217-173"><a id="MXF_to_MP4_streams"></a>Проверка потоков мультимедиа</span><span class="sxs-lookup"><span data-stu-id="3c217-173"><a id="MXF_to_MP4_streams"></a>Inspecting media streams</span></span>
<span data-ttu-id="3c217-174">Часто желательно, как поток hello выглядит подобно показанному tooknow проходит через hello рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="3c217-174">Often it's desired tooknow how hello stream looks like that flows through hello workflow.</span></span> <span data-ttu-id="3c217-175">tooinspect потока в любой момент в рабочем процессе hello, просто щелкните выходного или ввода ПИН-кода на любой из компонентов hello.</span><span class="sxs-lookup"><span data-stu-id="3c217-175">tooinspect a stream at any point in hello workflow, just click an output or input pin on any of hello components.</span></span> <span data-ttu-id="3c217-176">В этом случае попробуйте щелкнуть на закрепление вывода видео без сжатия hello нашей входных данных в файл мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="3c217-176">In this case, try clicking on hello Uncompressed Video output pin from our Media File Input.</span></span> <span data-ttu-id="3c217-177">Диалоговое окно будет открыт, позволяющий tooinspect hello исходящих видео.</span><span class="sxs-lookup"><span data-stu-id="3c217-177">A dialog will open up that allows tooinspect hello outbound video.</span></span>

![Проверка закрепление вывода hello видео без сжатия](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-inspecting-uncompressed-video-output.png)

<span data-ttu-id="3c217-179">*Проверка закрепление вывода hello видео без сжатия*</span><span class="sxs-lookup"><span data-stu-id="3c217-179">*Inspecting hello Uncompressed Video output pin*</span></span>

<span data-ttu-id="3c217-180">На рисунке выше показано, что входной видеофайл имеет разрешение 1920 x 1080, скорость 24 кадра в секунду, формат выборки 4:2:2 и продолжительность почти 2 минуты.</span><span class="sxs-lookup"><span data-stu-id="3c217-180">In our case, it tells us for example that we're dealing with a 1920x1080 input at 24 frames per second in 4:2:2 sampling for a video of almost 2 minutes.</span></span>

### <span data-ttu-id="3c217-181"><a id="MXF_to_MP4_file_generation"></a>Добавление видеокодировщика для создания файла MP4</span><span class="sxs-lookup"><span data-stu-id="3c217-181"><a id="MXF_to_MP4_file_generation"></a>Adding a video encoder for .MP4 file generation</span></span>
<span data-ttu-id="3c217-182">Обратите внимание, что теперь в области "Входные файлы мультимедиа" есть несколько точек выходных соединений: одна для компонента "Видео без сжатия" и по одной для каждого компонента "Аудио без сжатия".</span><span class="sxs-lookup"><span data-stu-id="3c217-182">Note that now, an Uncompressed Video and multiple Uncompressed Audio output pins are available for use on our Media File Input.</span></span> <span data-ttu-id="3c217-183">В порядке tooencode Здравствуйте входящих видео, мы должны компонента кодирования — в этом случае для создания. MP4-файлов.</span><span class="sxs-lookup"><span data-stu-id="3c217-183">In order tooencode hello inbound video, we need an encoding component - in this case for generating .MP4 files.</span></span>

<span data-ttu-id="3c217-184">tooencode hello tooH.264 потокового видео, добавьте hello кодировщик видео AVC компонент toohello рабочую область конструктора.</span><span class="sxs-lookup"><span data-stu-id="3c217-184">tooencode hello video stream tooH.264, add hello AVC Video Encoder component toohello designer surface.</span></span> <span data-ttu-id="3c217-185">Этот компонент преобразовывает видеопоток без сжатия в сжатый видеопоток AVC в соответствующей выходной точке.</span><span class="sxs-lookup"><span data-stu-id="3c217-185">This component takes an uncompress video stream as input and delivers an AVC compressed video stream on its output pin.</span></span>

![Несоединенный кодировщик AVC](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-avc-encoder.png)

<span data-ttu-id="3c217-187">*Несоединенный кодировщик AVC*</span><span class="sxs-lookup"><span data-stu-id="3c217-187">*Unconnected AVC Encoder*</span></span>

<span data-ttu-id="3c217-188">Его свойства определяют, как именно кодирование hello происходит.</span><span class="sxs-lookup"><span data-stu-id="3c217-188">Its properties determine how hello encoding exactly happens.</span></span> <span data-ttu-id="3c217-189">Давайте посмотрим на некоторые hello более важные параметры:</span><span class="sxs-lookup"><span data-stu-id="3c217-189">Let's have a look at some of hello more important settings:</span></span>

* <span data-ttu-id="3c217-190">Вывод ширины и высоты выходных данных: они определяют разрешения hello hello кодирования видео.</span><span class="sxs-lookup"><span data-stu-id="3c217-190">Output width and Output height: these determine hello resolution of hello encoded video.</span></span> <span data-ttu-id="3c217-191">В нашем примере мы выберем 640 x 360.</span><span class="sxs-lookup"><span data-stu-id="3c217-191">In our case let's go with 640x360</span></span>
* <span data-ttu-id="3c217-192">Частота кадров: когда toopassthrough набора, он будет просто внедрить частота кадров источника hello, это возможных toooverride этом хотя.</span><span class="sxs-lookup"><span data-stu-id="3c217-192">Frame Rate: when set toopassthrough it will just adopt hello source frame rate, it's possible toooverride this though.</span></span> <span data-ttu-id="3c217-193">Обратите внимание, что такое преобразование частоты кадров не имеет компенсации движения.</span><span class="sxs-lookup"><span data-stu-id="3c217-193">Note that such framerate conversion is not motion-compensated.</span></span>
* <span data-ttu-id="3c217-194">Профиль и уровень: эти свойства определяют hello AVC профиля и уровень.</span><span class="sxs-lookup"><span data-stu-id="3c217-194">Profile and Level: these determine hello AVC profile and level.</span></span> <span data-ttu-id="3c217-195">tooconveniently получить дополнительные сведения о разных уровнях hello и профили, щелкните значок вопросительного знака hello компонент кодировщик видео AVC hello и страница справки hello будет отображаться более подробные сведения о каждом из уровней hello.</span><span class="sxs-lookup"><span data-stu-id="3c217-195">tooconveniently get more information about hello different levels and profiles, click hello question mark icon on hello AVC Video Encoder component and hello help page will show more detail about each of hello levels.</span></span> <span data-ttu-id="3c217-196">В нашем примере выберем основного профиля на уровне 3.2 (по умолчанию hello).</span><span class="sxs-lookup"><span data-stu-id="3c217-196">For our sample, let's go with Main Profile at level 3.2 (hello default).</span></span>
* <span data-ttu-id="3c217-197">Режим управления скоростью и скорость (Кбит/с). В нашем сценарии мы хотим получить выходной файл с постоянной скоростью (CBR) 1200 Кбит/с.</span><span class="sxs-lookup"><span data-stu-id="3c217-197">Rate Control Mode and Bitrate (kbps): in our scenario we opt for a constant bitrate (CBR) output at 1200 kbps</span></span>
* <span data-ttu-id="3c217-198">: Видео это имеет место в формате hello VUI (сведения о применимости видео), записывается в поток hello H.264 (декодирования стороне сведения, которые могут быть использованы отображения hello tooenhance декодер, но не необходимым toocorrectly):</span><span class="sxs-lookup"><span data-stu-id="3c217-198">Video Format: this is about hello VUI (Video Usability Information) that gets written into hello H.264 stream (side information that might be used by a decoder tooenhance hello display but not essential toocorrectly decode):</span></span>
* <span data-ttu-id="3c217-199">NTSC (формат для США и Японии, используется скорость 30 кадров/с);</span><span class="sxs-lookup"><span data-stu-id="3c217-199">NTSC (typical for US or Japan, using 30 fps)</span></span>
* <span data-ttu-id="3c217-200">PAL (формат для Европы, используется скорость 25 кадров/с).</span><span class="sxs-lookup"><span data-stu-id="3c217-200">PAL (typical for Europe, using 25 fps)</span></span>
* <span data-ttu-id="3c217-201">Режим размера группы изображений (GOP). Для наших целей мы выберем фиксированный размер групп GOP, 2-секундный интервал опорных кадров и закрытые группы GPO.</span><span class="sxs-lookup"><span data-stu-id="3c217-201">GOP Size Mode: we'll configure Fixed GOP Size for our purposes with a Key Interval of 2 seconds with Closed GOPs.</span></span> <span data-ttu-id="3c217-202">Это обеспечивает совместимость с динамической упаковки служб мультимедиа Azure предоставляет приветствия.</span><span class="sxs-lookup"><span data-stu-id="3c217-202">This ensures compatibility with hello dynamic packaging Azure Media Services provides.</span></span>

<span data-ttu-id="3c217-203">toofeed нашей кодировщика AVC подключение из hello входного файла мультимедиа компонент toohello видео без сжатия ввода ПИН-кода из кодировщика hello AVC закрепление вывода hello видео без сжатия.</span><span class="sxs-lookup"><span data-stu-id="3c217-203">toofeed our AVC encoder, connect hello Uncompressed Video output pin from hello Media File Input component toohello Uncompressed Video input pin from hello AVC encoder.</span></span>

![Соединенный кодировщик AVC](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-avc-encoder.png)

<span data-ttu-id="3c217-205">*Соединение основного кодировщика AVC*</span><span class="sxs-lookup"><span data-stu-id="3c217-205">*Connected AVC Main encoder*</span></span>

### <span data-ttu-id="3c217-206"><a id="MXF_to_MP4_audio"></a>Кодировки аудиопотока hello</span><span class="sxs-lookup"><span data-stu-id="3c217-206"><a id="MXF_to_MP4_audio"></a>Encoding hello audio stream</span></span>
<span data-ttu-id="3c217-207">На этом этапе закодированные видео, но hello исходного несжатые аудиопотока по-прежнему нужна toobe сжимаются.</span><span class="sxs-lookup"><span data-stu-id="3c217-207">At this point, we have encoded video but hello original uncompressed audio stream still needs toobe compressed.</span></span> <span data-ttu-id="3c217-208">Для этого мы обратимся AAC по hello кодирование кодировщика AAC (Dolby) компонента.</span><span class="sxs-lookup"><span data-stu-id="3c217-208">For this we'll go with AAC encoding by hello AAC Encoder (Dolby) component.</span></span> <span data-ttu-id="3c217-209">Добавьте toohello рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="3c217-209">Add it toohello workflow.</span></span>

![Несоединенный кодировщик AVC](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-aac-encoder.png)

<span data-ttu-id="3c217-211">*Несоединенный кодировщик AAC*</span><span class="sxs-lookup"><span data-stu-id="3c217-211">*Unconnected AAC encoder*</span></span>

<span data-ttu-id="3c217-212">Теперь несовместимы: имеется только один несжатые аудио ввода ПИН-код из hello AAC кодировщика при более одного входного файла мультимедиа вероятно hello будет иметь два разных несжатых данных поток звука: один для hello слева аудио канал и один для hello Правильно.</span><span class="sxs-lookup"><span data-stu-id="3c217-212">Now there's an incompatibility: there's only a single uncompressed audio input pin from hello AAC Encoder while more than likely hello Media File Input will have two different uncompressed audio stream available: one for hello left audio channel and one for hello right.</span></span> <span data-ttu-id="3c217-213">Если речь идет об объемном звучании, каналов будет шесть. Поэтому невозможно toodirectly подключиться hello звука из источника входных данных файла мультимедиа hello в кодировщик аудио AAC hello.</span><span class="sxs-lookup"><span data-stu-id="3c217-213">(If you're dealing with surround sound, that's 6 channels.) So it's not possible toodirectly connect hello audio from hello Media File Input source into hello AAC audio encoder.</span></span> <span data-ttu-id="3c217-214">Hello AAC ожидается, что компонент так называемые «чередованием» аудиопотока: один поток, в котором содержатся оба hello слева и hello правого каналов, чередуются друг с другом.</span><span class="sxs-lookup"><span data-stu-id="3c217-214">hello AAC component expects a so-called "interleaved" audio stream: a single stream that has both hello left and hello right channels interleaved with each other.</span></span> <span data-ttu-id="3c217-215">Когда мы знаем, что из наших исходного файла мультимедиа какие звуковые дорожки на какой позиции в источнике hello, мы можно создать такие с чередованием аудиопотока с hello правильно назначаются динамика позиции для влево и вправо.</span><span class="sxs-lookup"><span data-stu-id="3c217-215">Once we know from our source media file which audio tracks are on what position in hello source, we can generate such interleaved audio stream with hello correctly assigned speaker positions for left and right.</span></span>

<span data-ttu-id="3c217-216">Сначала один требуется, чтобы toogenerated поток с чередованием из аудиоканалов источника необходимые hello.</span><span class="sxs-lookup"><span data-stu-id="3c217-216">First one will want toogenerated an interleaved stream from hello required source audio channels.</span></span> <span data-ttu-id="3c217-217">Hello аудио поток Interleaver компонент будет обрабатывать это за нас.</span><span class="sxs-lookup"><span data-stu-id="3c217-217">hello Audio Stream Interleaver component will handle this for us.</span></span> <span data-ttu-id="3c217-218">Добавьте его toohello рабочего процесса и подключите аудио выходы hello hello входных данных файла мультимедиа в него.</span><span class="sxs-lookup"><span data-stu-id="3c217-218">Add it toohello workflow and connect hello audio outputs from hello Media File Input into it.</span></span>

![Соединение компонента чередования аудиопотоков](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-audio-stream-interleaver.png)

<span data-ttu-id="3c217-220">*Соединение компонента чередования аудиопотоков*</span><span class="sxs-lookup"><span data-stu-id="3c217-220">*Connected Audio Stream Interleaver*</span></span>

<span data-ttu-id="3c217-221">Теперь, когда у нас есть с чередованием аудиопоток, мы по-прежнему не был указан где разрядов tooassign динамика hello влево или вправо.</span><span class="sxs-lookup"><span data-stu-id="3c217-221">Now that we have an interleaved audio stream, we still didn't specify where tooassign hello left or right speaker positions to.</span></span> <span data-ttu-id="3c217-222">В заказывать toospecify, можно использовать hello назначено позиции говорящего.</span><span class="sxs-lookup"><span data-stu-id="3c217-222">In order toospecify this, we can leverage hello Speaker Position Assigner.</span></span>

![Добавление компонента "Назначение положения динамиков"](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-speaker-position-assigner.png)

<span data-ttu-id="3c217-224">*Добавление компонента "Назначение положения динамиков"*</span><span class="sxs-lookup"><span data-stu-id="3c217-224">*Adding a Speaker Position Assigner*</span></span>

<span data-ttu-id="3c217-225">Настроить hello динамика позиции назначено для использования с стерео входного потока через фильтр конфигурации кодировщика для «Custom» и hello предустановку канал называется «2.0 ("L", "R")».</span><span class="sxs-lookup"><span data-stu-id="3c217-225">Configure hello Speaker Position Assigner for use with a stereo input stream through an Encoder Preset Filter of "Custom" and hello Channel Preset called "2.0 (L,R)".</span></span> <span data-ttu-id="3c217-226">(Это будет назначить toochannel положение левого динамика hello 1 и hello динамика правой позиции toochannel 2).</span><span class="sxs-lookup"><span data-stu-id="3c217-226">(This will assign hello left speaker position toochannel 1 and hello right speaker position toochannel 2.)</span></span>

<span data-ttu-id="3c217-227">Подключите выход hello hello назначено позиции динамика toohello ввода оператора hello AAC кодировщика.</span><span class="sxs-lookup"><span data-stu-id="3c217-227">Connect hello output of hello Speaker Position Assigner toohello input of hello AAC Encoder.</span></span> <span data-ttu-id="3c217-228">Затем сообщить toowork AAC кодировщика hello» 2.0 ("L", "R")» заданы канал, чтобы он доверял toodeal с стереозвук в качестве входных данных.</span><span class="sxs-lookup"><span data-stu-id="3c217-228">Then, tell hello AAC Encoder toowork with a "2.0 (L,R)" Channel Preset, so it knows toodeal with stereo audio as input.</span></span>

### <span data-ttu-id="3c217-229"><a id="MXF_to_MP4_audio_and_fideo"></a>Мультиплексирование аудио- и видеопотоков в контейнер MP4</span><span class="sxs-lookup"><span data-stu-id="3c217-229"><a id="MXF_to_MP4_audio_and_fideo"></a>Multiplexing Audio and Video streams into an MP4 container</span></span>
<span data-ttu-id="3c217-230">Видеопоток в кодировке AVC и аудиопоток в кодировке AAC можно объединить в контейнере MP4.</span><span class="sxs-lookup"><span data-stu-id="3c217-230">Given our AVC encoded video stream and our AAC encoded audio stream, we can capture both into an .MP4 container.</span></span> <span data-ttu-id="3c217-231">процесс Hello смешивание разных потоков в один из них, называется «мультиплексирование» (или «muxing»).</span><span class="sxs-lookup"><span data-stu-id="3c217-231">hello process of mixing different streams into a single one is called "multiplexing" (or "muxing").</span></span> <span data-ttu-id="3c217-232">В этом случае мы чередование hello аудио- и видеопотоки hello в одном согласовано. Пакет MP4.</span><span class="sxs-lookup"><span data-stu-id="3c217-232">In this case we're interleaving hello audio and hello video streams in a single coherent .MP4 package.</span></span> <span data-ttu-id="3c217-233">Hello компонент, координирующий для. Контейнер MP4 называется мультиплексор ISO MPEG-4 hello.</span><span class="sxs-lookup"><span data-stu-id="3c217-233">hello component that coordinates this for an .MP4 container is called hello ISO MPEG-4 Multiplexer.</span></span> <span data-ttu-id="3c217-234">Добавьте один toohello рабочую область конструктора и подключите кодировщик видео AVC hello и входные данные tooits AAC кодировщика hello.</span><span class="sxs-lookup"><span data-stu-id="3c217-234">Add one toohello designer surface and connect both hello AVC Video Encoder and hello AAC Encoder tooits inputs.</span></span>

![Соединение мультиплексора MPEG4](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-mpeg4-multiplexer.png)

<span data-ttu-id="3c217-236">*Соединение мультиплексора MPEG4*</span><span class="sxs-lookup"><span data-stu-id="3c217-236">*Connected MPEG4 Multiplexer*</span></span>

### <span data-ttu-id="3c217-237"><a id="MXF_to_MP4_writing_mp4"></a>Запись файла MP4 hello</span><span class="sxs-lookup"><span data-stu-id="3c217-237"><a id="MXF_to_MP4_writing_mp4"></a>Writing hello MP4 file</span></span>
<span data-ttu-id="3c217-238">При записи в выходной файл, используется компонент hello выходной файл.</span><span class="sxs-lookup"><span data-stu-id="3c217-238">When writing an output file, hello File Output component is used.</span></span> <span data-ttu-id="3c217-239">Представленный вывод toohello мультиплексор ISO MPEG-4 hello можно будет подключить, чтобы toodisk возвращает запись его выходных данных.</span><span class="sxs-lookup"><span data-stu-id="3c217-239">We can connect this toohello output of hello ISO MPEG-4 Multiplexer so that its output gets written toodisk.</span></span> <span data-ttu-id="3c217-240">toodo этого подключения hello контейнера (MPEG-4) выходного ПИН-код toohello записи входного контакта из hello выходной файл.</span><span class="sxs-lookup"><span data-stu-id="3c217-240">toodo this, connect hello Container (MPEG-4) output pin toohello Write input pin of hello File Output.</span></span>

![Соединение компонента "Вывод файла"](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-file-output.png)

<span data-ttu-id="3c217-242">*Соединение компонента "Вывод файла"*</span><span class="sxs-lookup"><span data-stu-id="3c217-242">*Connected File Output*</span></span>

<span data-ttu-id="3c217-243">Hello имя файла, который будет использоваться определяется hello свойства файла.</span><span class="sxs-lookup"><span data-stu-id="3c217-243">hello filename that will be used is determined by hello File property.</span></span> <span data-ttu-id="3c217-244">Это свойство может быть tooa жестко заданное значение, скорее всего один будете tooset его через выражение вместо него.</span><span class="sxs-lookup"><span data-stu-id="3c217-244">While that property can be hardcoded tooa given value, most likely one will want tooset it through an expression instead.</span></span>

<span data-ttu-id="3c217-245">рабочий процесс toohave hello автоматически определять hello выходные данные файла имя свойства из выражения, щелкните имя файла далее toohello hello кнопки (следующий значок toohello папки).</span><span class="sxs-lookup"><span data-stu-id="3c217-245">toohave hello workflow automatically determine hello output File name property from an expression, click hello buton next toohello File name (next toohello folder icon).</span></span> <span data-ttu-id="3c217-246">В hello раскрывающемся меню выберите команду «Выражение».</span><span class="sxs-lookup"><span data-stu-id="3c217-246">From hello drop down menu then select "Expression".</span></span> <span data-ttu-id="3c217-247">Откроется редактор выражений hello.</span><span class="sxs-lookup"><span data-stu-id="3c217-247">This will bring up hello expression editor.</span></span> <span data-ttu-id="3c217-248">Сначала очистите содержимое hello hello редактора.</span><span class="sxs-lookup"><span data-stu-id="3c217-248">Clear hello contents of hello editor first.</span></span>

![Пустой редактор выражений](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-empty-expression-editor.png)

<span data-ttu-id="3c217-250">*Пустой редактор выражений*</span><span class="sxs-lookup"><span data-stu-id="3c217-250">*Empty Expression Editor*</span></span>

<span data-ttu-id="3c217-251">Редактор выражений Hello позволяет tooenter любое литеральное значение, одновременно с одной или нескольких переменных.</span><span class="sxs-lookup"><span data-stu-id="3c217-251">hello expression editor allows tooenter any literal value, mixed with one or more variables.</span></span> <span data-ttu-id="3c217-252">Переменные начинаются со знака доллара.</span><span class="sxs-lookup"><span data-stu-id="3c217-252">Variables start with a dollar sign.</span></span> <span data-ttu-id="3c217-253">Как клавишу hello $ hello редакторе отобразится раскрывающийся список с помощью набора доступных переменных.</span><span class="sxs-lookup"><span data-stu-id="3c217-253">As you hit hello $ key, hello editor will show a dropdown box with a choice of available variables.</span></span> <span data-ttu-id="3c217-254">В нашем случае мы будем использовать сочетание hello выходной каталог переменной и hello базовый входной файл имя переменной:</span><span class="sxs-lookup"><span data-stu-id="3c217-254">In our case we'll use a combination of hello output directory variable and hello base input file name variable:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}.MP4

![Редактор выражений с указанным значением](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-expression-editor.png)

<span data-ttu-id="3c217-256">*Редактор выражений с указанным значением*</span><span class="sxs-lookup"><span data-stu-id="3c217-256">*Filled out Expression Editor*</span></span>

> [!NOTE]
> <span data-ttu-id="3c217-257">В порядке toosee просмотреть выходной файл задания кодирования в Azure, необходимо ввести значение в редактор выражений hello.</span><span class="sxs-lookup"><span data-stu-id="3c217-257">In order toosee see an output file of your encoding job in Azure, you must provide a value in hello expression editor.</span></span>
>
>

<span data-ttu-id="3c217-258">После подтверждения выражение hello, нажав ОК, окно свойств hello будет Предварительный просмотр toowhat значение hello файла свойство разрешает на данный момент времени.</span><span class="sxs-lookup"><span data-stu-id="3c217-258">When you confirm hello expression by hitting ok, hello property window will preview toowhat value hello File property resolves at this point in time.</span></span>

![Полученный из выражения конечный каталог](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-expression-resolves-output-dir.png)

<span data-ttu-id="3c217-260">*Полученный из выражения конечный каталог*</span><span class="sxs-lookup"><span data-stu-id="3c217-260">*File Expression resolves output dir*</span></span>

### <span data-ttu-id="3c217-261"><a id="MXF_to_MP4_asset_from_output"></a>Создание из выходного файла hello ресурс служб мультимедиа</span><span class="sxs-lookup"><span data-stu-id="3c217-261"><a id="MXF_to_MP4_asset_from_output"></a>Creating a Media Services Asset from hello output file</span></span>
<span data-ttu-id="3c217-262">Хотя мы написали выходной файл MP4, мы по-прежнему должны tooindicate, этот файл относится toohello выходной актив, какие службы мультимедиа создаст в результате выполнения этого рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="3c217-262">While we have written an MP4 output file, we still need tooindicate that this file belongs toohello output asset which media services will generate as a result of executing this workflow.</span></span> <span data-ttu-id="3c217-263">используется toothis end, узел hello выходной файл или ресурс на холсте hello рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="3c217-263">toothis end, hello Output File/Asset node on hello workflow canvas is used.</span></span> <span data-ttu-id="3c217-264">Все файлы, входящие в этот узел будет сделать частью hello полученный активов Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="3c217-264">All incoming files into this node will make part of hello resulting Azure Media Services asset.</span></span>

<span data-ttu-id="3c217-265">Подключите hello выходной файл компонента toohello выходной файл или ресурс toofinish hello рабочий процесс компонента.</span><span class="sxs-lookup"><span data-stu-id="3c217-265">Connect hello File Output component toohello Output File/Asset component toofinish hello workflow.</span></span>

![Завершенный рабочий процесс](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow.png)

<span data-ttu-id="3c217-267">*Завершенный рабочий процесс*</span><span class="sxs-lookup"><span data-stu-id="3c217-267">*Finished Workflow*</span></span>

### <span data-ttu-id="3c217-268"><a id="MXF_to_MP4_test"></a>Hello тест завершения рабочего процесса локально</span><span class="sxs-lookup"><span data-stu-id="3c217-268"><a id="MXF_to_MP4_test"></a>Test hello finished workflow locally</span></span>
<span data-ttu-id="3c217-269">tootest рабочего процесса hello локально, нажмите кнопку "play hello" в панели инструментов hello вверху hello.</span><span class="sxs-lookup"><span data-stu-id="3c217-269">tootest hello workflow locally, hit hello play button in hello toolbar at hello top.</span></span> <span data-ttu-id="3c217-270">По окончании выполнения рабочего процесса hello проверьте hello выходные данные, созданные в выходную папку hello настроен.</span><span class="sxs-lookup"><span data-stu-id="3c217-270">When hello workflow finished executing, inspect hello output generated in hello configured output folder.</span></span> <span data-ttu-id="3c217-271">Вы увидите, что выходной файл MP4, закодированную из файла источника входных данных MXF hello завершения hello.</span><span class="sxs-lookup"><span data-stu-id="3c217-271">You'll see hello finished MP4 output file that was encoded from hello MXF input source file.</span></span>

## <span data-ttu-id="3c217-272"><a id="MXF_to_MP4_with_dyn_packaging"></a>Кодирование файлов MXF в файлы MP4 с разными скоростями со включенной динамической упаковкой</span><span class="sxs-lookup"><span data-stu-id="3c217-272"><a id="MXF_to_MP4_with_dyn_packaging"></a>Encoding MXF into MP4 - multibitrate dynamic packaging enabled</span></span>
<span data-ttu-id="3c217-273">В этом разделе мы создадим из одного входного файла MXF набор файлов MP4 с несколькими скоростями и аудиокодированием AAC.</span><span class="sxs-lookup"><span data-stu-id="3c217-273">In this walkthrough we'll create a set of multiple bitrate MP4 files with AAC encoded audio from a single .MXF input file.</span></span>

<span data-ttu-id="3c217-274">Когда выходные данные средства с несколькими скоростями требуемого для использования в сочетании с возможностями динамической упаковки hello, предлагаемых службами мультимедиа Azure, несколькими GOP-файлами формата MP4 каждого разным битрейтом и разрешение потребуется toobe создан.</span><span class="sxs-lookup"><span data-stu-id="3c217-274">When a multi-bitrate asset output is desired for use in combination with hello Dynamic Packaging features offered by Azure Media Services, multiple GOP-aligned MP4 files of each a different bitrate and resolution will need toobe generated.</span></span> <span data-ttu-id="3c217-275">Таким образом, hello toodo [MXF кодировку в односкоростной MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4) Пошаговое руководство предоставляет отправную точку.</span><span class="sxs-lookup"><span data-stu-id="3c217-275">toodo so, hello [Encoding MXF into a single bitrate MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4) walkthrough provides us with a good starting point.</span></span>

![Запуск рабочего процесса](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow.png)

<span data-ttu-id="3c217-277">*Запуск рабочего процесса*</span><span class="sxs-lookup"><span data-stu-id="3c217-277">*Starting Workflow*</span></span>

### <span data-ttu-id="3c217-278"><a id="MXF_to_MP4_with_dyn_packaging_more_outputs"></a>Добавление одного или нескольких дополнительных выходных файлов MP4</span><span class="sxs-lookup"><span data-stu-id="3c217-278"><a id="MXF_to_MP4_with_dyn_packaging_more_outputs"></a>Adding one or more additional MP4 outputs</span></span>
<span data-ttu-id="3c217-279">Каждый файл MP4 в конечном ресурсе-контейнере служб мультимедиа Azure будет поддерживать разные скорость и разрешение.</span><span class="sxs-lookup"><span data-stu-id="3c217-279">Every MP4 file in our resulting Azure Media Services asset will support a different bitrate and resolution.</span></span> <span data-ttu-id="3c217-280">Давайте добавим один или несколько MP4 выходной файлы toohello рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="3c217-280">Let's add one or more MP4 output files toohello workflow.</span></span>

<span data-ttu-id="3c217-281">toomake убедиться, что у нас есть все наши видео кодировщики создан с Здравствуйте одинаковые параметры, наиболее удобным tooduplicate hello уже существующих кодировщик видео AVC и настроить другое сочетание разрешения и скорости (добавим один 960 x 540 на 25 кадров в секунду в 2,5 МБ/с).</span><span class="sxs-lookup"><span data-stu-id="3c217-281">toomake sure we have all our video encoders created with hello same settings, it's most convenient tooduplicate hello already existing AVC Video Encoder and configure another combination of resolution and bitrate (let's add one of 960 x 540 at 25 frames per second at 2,5 Mbps).</span></span> <span data-ttu-id="3c217-282">tooduplicate hello существующих кодировщиков, копировать вставьте его на поверхность конструктора hello.</span><span class="sxs-lookup"><span data-stu-id="3c217-282">tooduplicate hello existing encoder, copy paste it on hello designer surface.</span></span>

<span data-ttu-id="3c217-283">Подключите hello видео без сжатия вывода ПИН-код hello входных данных файла мультимедиа в наш новый компонент AVC.</span><span class="sxs-lookup"><span data-stu-id="3c217-283">Connect hello Uncompressed Video output pin of hello Media File Input into our new AVC component.</span></span>

![Соединение со вторым кодировщиком AVC](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-avc-encoder-connected.png)

<span data-ttu-id="3c217-285">*Соединение со вторым кодировщиком AVC*</span><span class="sxs-lookup"><span data-stu-id="3c217-285">*Second AVC encoder connected*</span></span>

<span data-ttu-id="3c217-286">Теперь адаптировать hello конфигурации для нашей новой AVC кодировщика toooutput 960 x 540 в 2,5 Мбит/с.</span><span class="sxs-lookup"><span data-stu-id="3c217-286">Now adapt hello configuration for our new AVC encoder toooutput 960x540 at 2,5 Mbps.</span></span> <span data-ttu-id="3c217-287">Эти параметры указываются в свойствах "Ширина выходного файла", "Высота выходного файла" и "Скорость (Кбит/с)".</span><span class="sxs-lookup"><span data-stu-id="3c217-287">(Use its properties "Output width", "Output height", and "Bitrate (kbps)" for this.)</span></span>

<span data-ttu-id="3c217-288">Учитывая мы хотим полученный активов toouse hello вместе с динамической упаковки служб мультимедиа Azure, конечной точки потоковой передачи hello должен toobe может создать из этих файлов MP4, HLS или Fragmented MP4 или ТИРЕ фрагментов, которые точно выровнены tooeach другим способом Клиенты, переключение между различными значениями скорости получение один непрерывный видео- и аудиопотоки удобства.</span><span class="sxs-lookup"><span data-stu-id="3c217-288">Given we want toouse hello resulting asset together with Azure Media Services' dynamic packaging, hello streaming endpoint needs toobe capable of generating from these MP4 files HLS/Fragmented MP4/DASH fragments that are exactly aligned tooeach other in a way that clients that are switching between different bitrates get a single smooth continuous video and audio experience.</span></span> <span data-ttu-id="3c217-289">Возможно, нам нужно, в свойства hello кодировщиков AVC hello размер GOP («группа изображений») для обоих MP4-файлов задается tooensure toomake too2 секунд, которые могут быть выполнены по:</span><span class="sxs-lookup"><span data-stu-id="3c217-289">toomake that happen, we need tooensure that, in hello properties of both AVC encoders hello GOP ("group of pictures") size for both MP4 files is set too2 seconds, which can be done by:</span></span>

* <span data-ttu-id="3c217-290">Установка размера GOP tooFixed режима установки размеров GOP hello и</span><span class="sxs-lookup"><span data-stu-id="3c217-290">setting hello GOP Size Mode tooFixed GOP size and</span></span>
* <span data-ttu-id="3c217-291">Hello интервал кадра ключ tootwo секунд.</span><span class="sxs-lookup"><span data-stu-id="3c217-291">hello Key Frame Interval tootwo seconds.</span></span>
* <span data-ttu-id="3c217-292">также задайте hello управления IDR GOP tooClosed GOP tooensure, все GOP основано на свои собственные без зависимостей</span><span class="sxs-lookup"><span data-stu-id="3c217-292">also set hello GOP IDR Control tooClosed GOP tooensure all GOP's are standing on their own without dependencies</span></span>

<span data-ttu-id="3c217-293">toomake удобный toounderstand нашей рабочего процесса, переименуйте первый AVC кодировщика hello слишком» кодировщик видео AVC 640 x 360 1200 Кбит/с» и hello второй AVC кодировщика «кодировщик видео AVC 960 x 540 2500 Кбит/с».</span><span class="sxs-lookup"><span data-stu-id="3c217-293">toomake our workflow convenient toounderstand, rename hello first AVC encoder too"AVC Video Encoder 640x360 1200kbps" and hello second AVC encoder "AVC Video Encoder 960x540 2500 kbps".</span></span>

<span data-ttu-id="3c217-294">Теперь добавьте второй компонент "Мультиплексор ISO MPEG-4" и второй компонент "Вывод файла".</span><span class="sxs-lookup"><span data-stu-id="3c217-294">Now add a second ISO MPEG-4 Multiplexer and a second File Output.</span></span> <span data-ttu-id="3c217-295">Подключите hello мультиплексор toohello нового AVC кодировщика и убедитесь, что его выходные данные направляются в hello выходной файл.</span><span class="sxs-lookup"><span data-stu-id="3c217-295">Connect hello multiplexer toohello new AVC encoder and make sure its output is directed into hello File Output.</span></span> <span data-ttu-id="3c217-296">Также подключения hello AAC аудио кодировщика вывода toohello новый мультиплексор элемента ввода.</span><span class="sxs-lookup"><span data-stu-id="3c217-296">Then also connect hello AAC audio encoder output toohello new multiplexer's input.</span></span> <span data-ttu-id="3c217-297">Hello выходной файл в свою очередь после этого можно tooadd узла выходной файл или ресурс подключенных toohello его toohello актив служб мультимедиа, который будет создан.</span><span class="sxs-lookup"><span data-stu-id="3c217-297">hello File Output in turn can then be connected toohello Output File/Asset node tooadd it toohello Media Services Asset that will be created.</span></span>

![Соединение второго мультиплексора с компонентом "Вывод файла"](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-muxer-file-output-connected.png)

<span data-ttu-id="3c217-299">*Соединение второго мультиплексора с компонентом "Вывод файла"*</span><span class="sxs-lookup"><span data-stu-id="3c217-299">*Second Muxer and File Output connected*</span></span>

<span data-ttu-id="3c217-300">Для обеспечения совместимости с динамической упаковки служб мультимедиа Azure настроить число tooGOP hello мультиплексор в режиме блока или длительность и выбрать hello Gop на too1 фрагмента данных.</span><span class="sxs-lookup"><span data-stu-id="3c217-300">For compatibility with Azure Media Services dynamic packaging, configure hello multiplexer's Chunk Mode tooGOP count or duration and set hello GOPs per chunk too1.</span></span> <span data-ttu-id="3c217-301">(Должно быть по умолчанию hello.)</span><span class="sxs-lookup"><span data-stu-id="3c217-301">(This should be hello default.)</span></span>

![Режимы фрагментирования в мультиплексоре](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-muxer-chunk-modes.png)

<span data-ttu-id="3c217-303">*Режимы фрагментирования в мультиплексоре*</span><span class="sxs-lookup"><span data-stu-id="3c217-303">*Muxer Chunk Modes*</span></span>

<span data-ttu-id="3c217-304">Примечание: вы можете toorepeat этот процесс для других скоростью и выходные данные средства toohello добавлены сочетания требуется toohave разрешения.</span><span class="sxs-lookup"><span data-stu-id="3c217-304">Note: you may want toorepeat this process for any other bitrate and resolution combinations you want toohave added toohello asset output.</span></span>

### <span data-ttu-id="3c217-305"><a id="MXF_to_MP4_with_dyn_packaging_conf_output_names"></a>Настройка имен вывод файлов hello</span><span class="sxs-lookup"><span data-stu-id="3c217-305"><a id="MXF_to_MP4_with_dyn_packaging_conf_output_names"></a>Configuring hello file output names</span></span>
<span data-ttu-id="3c217-306">У нас есть несколько отдельных файлов добавлены toohello выходной актив.</span><span class="sxs-lookup"><span data-stu-id="3c217-306">We have more than one single file added toohello output asset.</span></span> <span data-ttu-id="3c217-307">Это позволяет убедиться, что hello toomake необходимость, имена файлов для каждого hello выходные файлы отличаются друг от друга и может быть даже применяются соглашения об именах файлов, становится ясно, от имени файла hello вы имеете дело с.</span><span class="sxs-lookup"><span data-stu-id="3c217-307">This provides a need toomake sure hello filenames for each of hello output files are different from each other and maybe even apply a file-naming convention so it becomes clear from hello file name what you're dealing with.</span></span>

<span data-ttu-id="3c217-308">Имени выходного файла можно управлять через выражениях в конструкторе hello.</span><span class="sxs-lookup"><span data-stu-id="3c217-308">File output naming can be controlled through expressions in hello designer.</span></span> <span data-ttu-id="3c217-309">Откройте панель свойств hello для одного из компонентов выходной файл hello и редактор выражений hello для hello свойство файла.</span><span class="sxs-lookup"><span data-stu-id="3c217-309">Open hello property pane for one of hello File Output components and open hello expression editor for hello File property.</span></span> <span data-ttu-id="3c217-310">Наш первый выходной файл был настроен через hello, следующее выражение (см. Учебник hello для перехода из [MXF tooa односкоростной вывода MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)):</span><span class="sxs-lookup"><span data-stu-id="3c217-310">Our first output file was configured through hello following expression (see hello tutorial for going from [MXF tooa single bitrate MP4 output](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)):</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}.MP4

<span data-ttu-id="3c217-311">Это означает, что наши filename определяется две переменные: hello выходных каталогов toowrite в и hello базовое имя исходного файла.</span><span class="sxs-lookup"><span data-stu-id="3c217-311">This means that our filename is determined by two variables: hello output directory toowrite in and hello source file base name.</span></span> <span data-ttu-id="3c217-312">Бывшая Hello предоставляется как свойство корневого рабочего процесса hello и последнем hello определяется hello входящего файла.</span><span class="sxs-lookup"><span data-stu-id="3c217-312">hello former is exposed as a property on hello workflow root and hello latter is determined by hello incoming file.</span></span> <span data-ttu-id="3c217-313">Обратите внимание, что выходной каталог hello используется для локального тестирования; Это свойство будет переопределено hello потоков работ при выполнении рабочего процесса hello hello процессоров носитель на основе облачных служб мультимедиа Azure.</span><span class="sxs-lookup"><span data-stu-id="3c217-313">Note that hello output directory is what you use for local testing; this property will be overridden by hello workflow engine when hello workflow is executed by hello cloud-based media processor in Azure Media Services.</span></span>
<span data-ttu-id="3c217-314">Сначала toogive оба наши выходные данные файлы вероятен согласованный результат, hello изменение файла именования выражение для:</span><span class="sxs-lookup"><span data-stu-id="3c217-314">toogive both our output files a consistent output naming, change hello first file naming expression to:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

<span data-ttu-id="3c217-315">и hello во-вторых, чтобы:</span><span class="sxs-lookup"><span data-stu-id="3c217-315">and hello second to:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_960x540_2.MP4

<span data-ttu-id="3c217-316">Выполнение промежуточных тестового запуска toomake убедиться, что правильно формируются выходные файлы обеих MP4.</span><span class="sxs-lookup"><span data-stu-id="3c217-316">Execute an intermediate test run toomake sure both MP4 output files are properly generated.</span></span>

### <span data-ttu-id="3c217-317"><a id="MXF_to_MP4_with_dyn_packaging_audio_tracks"></a>Добавление отдельной звуковой дорожки</span><span class="sxs-lookup"><span data-stu-id="3c217-317"><a id="MXF_to_MP4_with_dyn_packaging_audio_tracks"></a>Adding a separate Audio Track</span></span>
<span data-ttu-id="3c217-318">Как мы рассмотрим позже, когда мы создаем toogo файл .ism с нашей выходных файлов MP4, мы также требуется только звук MP4-файл как hello звуковой дорожки для наших адаптивной потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="3c217-318">As we'll see later when we generate an .ism file toogo with our MP4 output files, we will also require a audio-only MP4 file as hello audio track for our adaptive streaming.</span></span> <span data-ttu-id="3c217-319">toocreate этот файл, добавьте дополнительные muxer toohello workflow (мультиплексор ISO-MPEG-4) и соедините закрепление вывода hello AAC кодировщика с ее ввода ПИН-кода для направления 1.</span><span class="sxs-lookup"><span data-stu-id="3c217-319">toocreate this file, add an additional muxer toohello workflow (ISO-MPEG-4 Multiplexer) and connect hello AAC encoder's output pin with its input pin for Track 1.</span></span>

![Добавление мультиплексора звука](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-added.png)

<span data-ttu-id="3c217-321">*Добавление мультиплексора звука*</span><span class="sxs-lookup"><span data-stu-id="3c217-321">*Audio Muxer Added*</span></span>

<span data-ttu-id="3c217-322">Создайте третий выходной файл компонента toooutput hello исходящим потоком из hello muxer и настройте hello файл именования выражения в виде:</span><span class="sxs-lookup"><span data-stu-id="3c217-322">Create a third File Output component toooutput hello outbound stream from hello muxer and configure hello file naming expression as:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_128kbps_audio.MP4

![Мультиплексор звука создает выходной файл](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-creating-file-output.png)

<span data-ttu-id="3c217-324">*Мультиплексор звука создает выходной файл*</span><span class="sxs-lookup"><span data-stu-id="3c217-324">*Audio Muxer creating File Output*</span></span>

### <span data-ttu-id="3c217-325"><a id="MXF_to_MP4_with_dyn_packaging_ism_file"></a>Добавление hello. SMIL ISM-файла</span><span class="sxs-lookup"><span data-stu-id="3c217-325"><a id="MXF_to_MP4_with_dyn_packaging_ism_file"></a>Adding hello .ISM SMIL File</span></span>
<span data-ttu-id="3c217-326">Hello toowork динамической упаковки в сочетании с обоих MP4 файлы (и hello только звук MP4) в нашей актив служб мультимедиа, мы также требуется файл манифеста (также называемый файлом «SMIL»: язык синхронизации для интеграции мультимедиа).</span><span class="sxs-lookup"><span data-stu-id="3c217-326">For hello dynamic packaging toowork in combination with both MP4 files (and hello audio-only MP4) in our Media Services asset, we also need a manifest file (also called a "SMIL" file: Synchronized Multimedia Integration Language).</span></span> <span data-ttu-id="3c217-327">Этот файл указывает tooAzure Media Services, то, какие файлы MP4 доступно для динамической упаковки и какие из этих tooconsider для потоковой передачи аудио hello.</span><span class="sxs-lookup"><span data-stu-id="3c217-327">This file indicates tooAzure Media Services what MP4 files are available for dynamic packaging and which of those tooconsider for hello audio streaming.</span></span> <span data-ttu-id="3c217-328">Типичный файл манифеста для набора файлов MP4 с одним звуковым потоком выглядит так:</span><span class="sxs-lookup"><span data-stu-id="3c217-328">A typical manifest file for a set of MP4's with a single audio stream looks like this:</span></span>

    <?xml version="1.0" encoding="utf-8" standalone="yes"?>
    <smil xmlns="http://www.w3.org/2001/SMIL20/Language">
      <head>
        <meta name="formats" content="mp4" />
      </head>
      <body>
        <switch>
          <video src="H264_1900kbps_AAC_und_ch2_96kbps.mp4" />
          <video src="H264_1300kbps_AAC_und_ch2_96kbps.mp4" />
          <video src="H264_900kbps_AAC_und_ch2_96kbps.mp4" />
          <audio src="AAC_ch2_96kbps.mp4" title="AAC_und_ch2_96kbps" />
        </switch>
      </body>
    </smil>

<span data-ttu-id="3c217-329">Hello ISM-файле содержится в операторе switch tooeach ссылка hello отдельных MP4 видеофайлов и кроме звуковой файл toothose также один (или более) ссылается на tooan MP4, содержащую только звук hello.</span><span class="sxs-lookup"><span data-stu-id="3c217-329">hello .ism file contains within a switch statement, a reference tooeach of hello individual MP4 video files and in addition toothose also one (or more) audio file references tooan MP4 that only contains hello audio.</span></span>

<span data-ttu-id="3c217-330">Создание файла манифеста hello для наших набора MP4 можно сделать с помощью компонентом, называется «Писатель манифеста AMS» hello.</span><span class="sxs-lookup"><span data-stu-id="3c217-330">Generating hello manifest file for our set of MP4's can be done through a component called hello "AMS Manifest Writer".</span></span> <span data-ttu-id="3c217-331">toouse, перетащите его на поверхность hello и подключите hello «Записывать полный набор» закрепления вывода компонентов toohello hello три выходной файл манифеста записи AMS входных данных.</span><span class="sxs-lookup"><span data-stu-id="3c217-331">toouse it, drag it onto hello surface and connect hello "Write Complete" output pins from hello three File Output components toohello AMS Manifest Writer input.</span></span> <span data-ttu-id="3c217-332">Убедитесь, что tooconnect hello выходные данные hello записи манифеста AMS toohello выходной файл или ресурс.</span><span class="sxs-lookup"><span data-stu-id="3c217-332">Then make sure tooconnect hello output of hello AMS Manifest Writer toohello Output File/Asset.</span></span>

<span data-ttu-id="3c217-333">Как и в наших других файл выходных данных компонентов, настройте hello .ism имя выходного файла с помощью выражения.</span><span class="sxs-lookup"><span data-stu-id="3c217-333">As with our other file output components, configure hello .ism file output name with an expression:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_manifest.ism

<span data-ttu-id="3c217-334">По завершении рабочего процесса выглядит следующим образом hello ниже.</span><span class="sxs-lookup"><span data-stu-id="3c217-334">Our finished workflow looks like hello below:</span></span>

![По завершении рабочего процесса MP4 MXF toomultibitrate](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-mxf-to-multibitrate-mp4-workflow.png)

<span data-ttu-id="3c217-336">*По завершении рабочего процесса MP4 MXF toomultibitrate*</span><span class="sxs-lookup"><span data-stu-id="3c217-336">*Finished MXF toomultibitrate MP4 workflow*</span></span>

## <span data-ttu-id="3c217-337"><a id="MXF_to__multibitrate_MP4"></a>Расширенная схема кодирования файла MXF в файл MP4 с несколькими скоростями</span><span class="sxs-lookup"><span data-stu-id="3c217-337"><a id="MXF_to__multibitrate_MP4"></a>Encoding MXF into multibitrate MP4 - enhanced blueprint</span></span>
<span data-ttu-id="3c217-338">В hello [предыдущем пошаговом руководстве рабочего процесса](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging) мы рассмотрели, как один входной актив MXF может быть преобразован в выходной актив MP4-файлов с разными скоростями, только звук MP4-файл и файл манифеста для использования в сочетании с мультимедиа Azure Динамическая упаковка служб.</span><span class="sxs-lookup"><span data-stu-id="3c217-338">In hello [previous workflow walkthrough](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging) we've seen how a single MXF input asset can be converted into an output asset with multi-bitrate MP4 files, an audio-only MP4 file and a manifest file for use in conjunction with Azure Media Services dynamic packaging.</span></span>

<span data-ttu-id="3c217-339">Это пошаговое руководство покажет, как некоторые аспекты hello могут быть улучшены и сделать более удобной.</span><span class="sxs-lookup"><span data-stu-id="3c217-339">This walkthrough will show how some of hello aspects can be enhanced and made more convenient.</span></span>

### <span data-ttu-id="3c217-340"><a id="MXF_to_multibitrate_MP4_overview"></a>Общие сведения о tooenhance рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="3c217-340"><a id="MXF_to_multibitrate_MP4_overview"></a>Workflow overview tooenhance</span></span>
![Tooenhance многоскоростных MP4 рабочего процесса](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-enhance.png)

<span data-ttu-id="3c217-342">*Tooenhance многоскоростных MP4 рабочего процесса*</span><span class="sxs-lookup"><span data-stu-id="3c217-342">*Multibitrate MP4 workflow tooenhance*</span></span>

### <span data-ttu-id="3c217-343"><a id="MXF_to__multibitrate_MP4_file_naming"></a>Соглашения об именовании файлов</span><span class="sxs-lookup"><span data-stu-id="3c217-343"><a id="MXF_to__multibitrate_MP4_file_naming"></a>File Naming Conventions</span></span>
<span data-ttu-id="3c217-344">В предыдущий рабочий процесс hello простое выражение указан как hello основания для создания имен файлов выходных данных.</span><span class="sxs-lookup"><span data-stu-id="3c217-344">In hello previous workflow we specified a simple expression as hello basis for generating output file names.</span></span> <span data-ttu-id="3c217-345">У нас есть некоторые дублирования хотя: все компоненты файла отдельного выхода hello hello указаны такие выражения.</span><span class="sxs-lookup"><span data-stu-id="3c217-345">We have some duplication though: all of hello hello individual output file components specified such expression.</span></span>

<span data-ttu-id="3c217-346">Например нашей компонента выходные данные файла для первого видеофайла hello настраивается с помощью этого выражения:</span><span class="sxs-lookup"><span data-stu-id="3c217-346">For example, our file output component for hello first video file is configured with this expression:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

<span data-ttu-id="3c217-347">Хотя для hello второй выход видео, у нас есть выражение, подобное:</span><span class="sxs-lookup"><span data-stu-id="3c217-347">While for hello second output video, we have an expression like:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_960x540_2.MP4

<span data-ttu-id="3c217-348">Если бы мы могли вместо этого удалить некоторые из таких повторов, мы бы сделали настройку более гибкой, аккуратной и удобной, не так ли? Кроме того, это позволит снизить вероятность возникновения ошибок.</span><span class="sxs-lookup"><span data-stu-id="3c217-348">Wouldn't it be cleaner, less error prone and more convenient if we could remove some of this duplication and make things more configurable instead?</span></span> <span data-ttu-id="3c217-349">К счастью мы можем: hello конструктор возможности выражения в сочетании с пользовательскими свойствами hello возможность toocreate на нашем корневого рабочего процесса даст нам обеспечивает дополнительный уровень удобства.</span><span class="sxs-lookup"><span data-stu-id="3c217-349">Luckily we can: hello designer's expression capabilities in combination with hello ability toocreate custom properties on our workflow root will give us an added layer of convenience.</span></span>

<span data-ttu-id="3c217-350">Предположим, мы будем диска имя файла конфигурации из битрейтах hello hello отдельных MP4-файлов.</span><span class="sxs-lookup"><span data-stu-id="3c217-350">Let's assume we'll drive filename configuration from hello bitrates of hello individual MP4 files.</span></span> <span data-ttu-id="3c217-351">Эти битрейтов, мы будем стремятся tooconfigure в один центральный поместите (hello корень графа нашей), из которой будете иметь доступ к которым осуществляется tooconfigure и диск создания имени файла.</span><span class="sxs-lookup"><span data-stu-id="3c217-351">These bitrates we'll aim tooconfigure in one central place (on hello root of our graph), from where they'll be accessed tooconfigure and drive file name generation.</span></span> <span data-ttu-id="3c217-352">toodo это, начнем с публикации свойство bitrate hello от корня toohello кодировщики AVC обоих рабочим процессом, чтобы он стал доступен с обоих корневой hello также в аспекте hello AVC кодировщиков.</span><span class="sxs-lookup"><span data-stu-id="3c217-352">toodo this, we start by publishing hello bitrate property from both AVC encoders toohello root of our workflow, so that it becomes accessible from both hello root as well as from hello AVC encoders.</span></span> <span data-ttu-id="3c217-353">(Даже при отображении в двух разных местах существует только одно базовое значение.)</span><span class="sxs-lookup"><span data-stu-id="3c217-353">(Even if displayed in two different spots, there's only one underlying value.)</span></span>

### <span data-ttu-id="3c217-354"><a id="MXF_to__multibitrate_MP4_publishing"></a>Свойства публикации компонента на hello корневого рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="3c217-354"><a id="MXF_to__multibitrate_MP4_publishing"></a>Publishing component properties onto hello workflow root</span></span>
<span data-ttu-id="3c217-355">Откройте первый AVC кодировщика hello, перейдите свойство toohello скорость (Кбит/с) и hello раскрывающемся списке выберите публикации.</span><span class="sxs-lookup"><span data-stu-id="3c217-355">Open hello first AVC encoder, go toohello Bitrate (kbps) property and from hello dropdown choose Publish.</span></span>

![Свойство публикации bitrate hello](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-bitrate-property.png)

<span data-ttu-id="3c217-357">*Свойство публикации bitrate hello*</span><span class="sxs-lookup"><span data-stu-id="3c217-357">*Publishing hello bitrate property*</span></span>

<span data-ttu-id="3c217-358">Настройка hello публикации корневой toohello toopublish диалоговое окно графа наш рабочий процесс с опубликованное название «video1bitrate» и для чтения отображаемое имя «Скоростью видео 1».</span><span class="sxs-lookup"><span data-stu-id="3c217-358">Configure hello publish dialog toopublish toohello root of our workflow graph, with a published name of "video1bitrate" and a readable display name of "Video 1 Bitrate".</span></span> <span data-ttu-id="3c217-359">Укажите для пользовательской группы имя "Streaming Bitrates" и нажмите кнопку "Опубликовать".</span><span class="sxs-lookup"><span data-stu-id="3c217-359">Configure a custom group name called "Streaming Bitrates" and hit Publish.</span></span>

![Свойство публикации bitrate hello](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-bitrate-property.png)

<span data-ttu-id="3c217-361">*Диалоговое окно публикации для свойства скорости*</span><span class="sxs-lookup"><span data-stu-id="3c217-361">*Publishing dialog for bitrate property*</span></span>

<span data-ttu-id="3c217-362">Повторите hello одинаковы для свойства bitrate hello hello второй AVC кодировщика и присвойте ей имя «video2bitrate» с отображаемым именем «Скоростью видео 2», что в hello одну группа «Битрейтах потоковой передачи».</span><span class="sxs-lookup"><span data-stu-id="3c217-362">Repeat hello same for hello bitrate property of hello second AVC encoder and name it "video2bitrate" with a display name of "Video 2 Bitrate", in hello same custom group "Streaming Bitrates".</span></span>

<span data-ttu-id="3c217-363">Если мы теперь проверить свойства корневого рабочего процесса hello, мы рассмотрим нашей пользовательской группе отображаются два свойства опубликованного приветствия.</span><span class="sxs-lookup"><span data-stu-id="3c217-363">If we now inspect hello workflow root properties, we'll see our custom group with hello two published properties show up.</span></span> <span data-ttu-id="3c217-364">Оба отражения значение hello их соответствующих скоростью AVC кодировщика.</span><span class="sxs-lookup"><span data-stu-id="3c217-364">Both are reflecting hello value of their respective AVC encoder bitrate.</span></span>

![Опубликованные свойства скорости в корне рабочего процесса](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-bitrate-props-on-workflow-root.png)

<span data-ttu-id="3c217-366">Каждый раз, когда мы хотим tooaccess эти свойства из кода или из выражения, мы можно сделать следующим образом:</span><span class="sxs-lookup"><span data-stu-id="3c217-366">Whenever we want tooaccess these properties from code or from an expression, we can do so like this:</span></span>

* <span data-ttu-id="3c217-367">из встроенного кода в компоненте прямо под корневым hello: node.getPropertyAsString('.. / video1bitrate', null)</span><span class="sxs-lookup"><span data-stu-id="3c217-367">from inline code from a component right below hello root: node.getPropertyAsString('../video1bitrate',null)</span></span>
* <span data-ttu-id="3c217-368">в выражении: ${ROOT_video1bitrate}.</span><span class="sxs-lookup"><span data-stu-id="3c217-368">within an expression: ${ROOT_video1bitrate}</span></span>

<span data-ttu-id="3c217-369">Давайте завершите группы «Потоковой передачи Битрейтах» hello, публикации нашей звуковой дорожки скоростью в нем также.</span><span class="sxs-lookup"><span data-stu-id="3c217-369">Let's complete hello "Streaming Bitrates" group by publishing our audio track bitrate on it as well.</span></span> <span data-ttu-id="3c217-370">В пределах свойства hello hello AAC кодировщика поиск приветствия скоростью и выберите публикации из следующего tooit hello раскрывающийся список.</span><span class="sxs-lookup"><span data-stu-id="3c217-370">Within hello properties of hello AAC Encoder, search for hello Bitrate setting and select Publish from hello dropdown next tooit.</span></span> <span data-ttu-id="3c217-371">Публикация toohello корень графа hello с именем «audio1bitrate» и отображаемое имя «Битрейт аудио 1» в нашей пользовательской группы «Битрейтах потоковой передачи».</span><span class="sxs-lookup"><span data-stu-id="3c217-371">Publish toohello root of hello graph with name "audio1bitrate" and display name "Audio 1 Bitrate" within our custom group "Streaming Bitrates".</span></span>

![Диалоговое окно публикации для скорости аудиопотока](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-audio-bitrate.png)

<span data-ttu-id="3c217-373">*Диалоговое окно публикации для скорости аудиопотока*</span><span class="sxs-lookup"><span data-stu-id="3c217-373">*Publishing dialog for audio bitrate*</span></span>

![Итоговые свойства видео и аудио в корне](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-resulting-video-and-audio-props-on-root.png)

<span data-ttu-id="3c217-375">*Итоговые свойства видео и аудио в корне*</span><span class="sxs-lookup"><span data-stu-id="3c217-375">*Resulting video and audio props on root*</span></span>

<span data-ttu-id="3c217-376">Обратите внимание, что при изменении любого из этих трех значений также повторно настраивает значения для соответствующих компонентов hello, они связаны с hello изменения (и, где публикуется из).</span><span class="sxs-lookup"><span data-stu-id="3c217-376">Note that changing any of those three values also re-configures and changes hello values on hello respective components they are linked with (and where published from).</span></span>

### <span data-ttu-id="3c217-377"><a id="MXF_to__multibitrate_MP4_output_files"></a>Создание зависимости имен созданных выходных файлов от значений опубликованных свойств</span><span class="sxs-lookup"><span data-stu-id="3c217-377"><a id="MXF_to__multibitrate_MP4_output_files"></a>Have generated output file names rely on published property values</span></span>
<span data-ttu-id="3c217-378">Вместо жесткого задания нашей имена созданный файл, мы теперь можно изменить наше выражение имя файла, на каждом toorely компоненты hello выходной файл на hello bitrate свойства, которые мы только что опубликованной в корневом каталоге graph hello.</span><span class="sxs-lookup"><span data-stu-id="3c217-378">Instead of hardcoding our generated file names, we can now change our filename expression on each of hello File Output components toorely on hello bitrate properties we just published on hello graph root.</span></span> <span data-ttu-id="3c217-379">Начиная с нашей первый выходной файл, найти свойство файла hello и изменить выражение hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="3c217-379">Starting with our first file output, find hello File property and edit hello expression like this:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video1bitrate}kbps.MP4

<span data-ttu-id="3c217-380">Hello различные параметры в этом выражении можно получить доступ к и ввести, нажав знак доллара hello на клавиатуре hello в окно приветствия выражений.</span><span class="sxs-lookup"><span data-stu-id="3c217-380">hello different parameters in this expression can be accessed and entered by hitting hello dollar sign on hello keyboard while in hello expression window.</span></span> <span data-ttu-id="3c217-381">Один из доступных параметров hello, наши video1bitrate свойства, которое мы ранее опубликованные.</span><span class="sxs-lookup"><span data-stu-id="3c217-381">One of hello available parameters is our video1bitrate property which we published earlier.</span></span>

![Доступ к параметрам в редакторе выражений](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-accessing-parameters-within-an-expression.png)

<span data-ttu-id="3c217-383">*Доступ к параметрам в редакторе выражений*</span><span class="sxs-lookup"><span data-stu-id="3c217-383">*Accessing parameters within an expression*</span></span>

<span data-ttu-id="3c217-384">Здравствуйте, то же самое hello выходной файл для наших второй видео:</span><span class="sxs-lookup"><span data-stu-id="3c217-384">Do hello same for hello file output for our second video:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video2bitrate}kbps.MP4

<span data-ttu-id="3c217-385">и для вывода hello звукового файла:</span><span class="sxs-lookup"><span data-stu-id="3c217-385">and for hello audio-only file output:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_audio1bitrate}bps_audio.MP4

<span data-ttu-id="3c217-386">Если теперь мы изменили bitrate hello по одной из видео hello или звуковые файлы, соответствующие кодировщика hello будет перенастроен и hello bitrate-файл имя соглашение будет соблюдаться все автоматического.</span><span class="sxs-lookup"><span data-stu-id="3c217-386">If we now change hello bitrate for any of hello video or audio files, hello respective encoder will be reconfigured and hello bitrate-based file name convention will be honored all automatic.</span></span>

## <span data-ttu-id="3c217-387"><a id="thumbnails_to__multibitrate_MP4"></a>Добавление выходных данных MP4 toomultibitrate эскизов</span><span class="sxs-lookup"><span data-stu-id="3c217-387"><a id="thumbnails_to__multibitrate_MP4"></a>Adding thumbnails toomultibitrate MP4 output</span></span>
<span data-ttu-id="3c217-388">Начиная с рабочий процесс, который приводит к возникновению ошибки [многоскоростных MP4 вывод MXF ввода](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), мы теперь заинтересованы в Добавление выходных данных toohello эскизы.</span><span class="sxs-lookup"><span data-stu-id="3c217-388">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into adding thumbnails toohello output.</span></span>

### <span data-ttu-id="3c217-389"><a id="thumbnails_to__multibitrate_MP4_overview"></a>Для эскизов tooadd обзор рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="3c217-389"><a id="thumbnails_to__multibitrate_MP4_overview"></a>Workflow overview tooadd thumbnails to</span></span>
![Toostart многоскоростных MP4 рабочего процесса из](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-start-from.png)

<span data-ttu-id="3c217-391">*Toostart многоскоростных MP4 рабочего процесса из*</span><span class="sxs-lookup"><span data-stu-id="3c217-391">*Multibitrate MP4 workflow toostart from*</span></span>

### <span data-ttu-id="3c217-392"><a id="thumbnails_to__multibitrate_MP4__with_jpg"></a>Добавление кодировки JPG</span><span class="sxs-lookup"><span data-stu-id="3c217-392"><a id="thumbnails_to__multibitrate_MP4__with_jpg"></a>Adding JPG Encoding</span></span>
<span data-ttu-id="3c217-393">Hello суть нашей создание эскизов будет компонент hello кодировщика JPG, может toooutput JPG-файлы.</span><span class="sxs-lookup"><span data-stu-id="3c217-393">hello heart of our thumbnail generation will be hello JPG Encoder component, able toooutput JPG files.</span></span>

![Кодировщик JPG](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-jpg-encoder.png)

<span data-ttu-id="3c217-395">*Кодировщик JPG*</span><span class="sxs-lookup"><span data-stu-id="3c217-395">*JPG Encoder*</span></span>

<span data-ttu-id="3c217-396">Мы не может подключиться напрямую, однако наши видео без сжатия потока hello входных данных файла мультимедиа в кодировщик JPG hello.</span><span class="sxs-lookup"><span data-stu-id="3c217-396">We cannot however directly connect our Uncompressed Video stream from hello Media File Input into hello JPG encoder.</span></span> <span data-ttu-id="3c217-397">Вместо этого он ожидает, что toobe передающееся отдельным кадрам.</span><span class="sxs-lookup"><span data-stu-id="3c217-397">Instead, it expects toobe handed individual frames.</span></span> <span data-ttu-id="3c217-398">Это, мы можем сделать через компонент шлюза кадра видео hello.</span><span class="sxs-lookup"><span data-stu-id="3c217-398">This, we can do through hello Video Frame Gate component.</span></span>

![Подключение кодировщик кадра шлюза toohello JPG](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-frame-gate-to-jpg-encoder.png)

<span data-ttu-id="3c217-400">*Подключение кодировщик кадра шлюза toohello JPG*</span><span class="sxs-lookup"><span data-stu-id="3c217-400">*Connecting a frame gate toohello JPG encoder*</span></span>

<span data-ttu-id="3c217-401">шлюз кадра Hello после каждого такого большого количества секунд или кадры позволяет toopass кадров видео.</span><span class="sxs-lookup"><span data-stu-id="3c217-401">hello frame gate once every so many seconds or frames allows a video frame toopass.</span></span> <span data-ttu-id="3c217-402">Hello интервал hello время и смещение, с которой это происходит, можно изменить в свойствах hello.</span><span class="sxs-lookup"><span data-stu-id="3c217-402">hello interval and hello time offset with which this happens is configurable in hello properties.</span></span>

![Свойства шлюза видеокадров](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-video-frame-gate-properties.png)

<span data-ttu-id="3c217-404">*Свойства шлюза видеокадров*</span><span class="sxs-lookup"><span data-stu-id="3c217-404">*Video Frame Gate properties*</span></span>

<span data-ttu-id="3c217-405">Рассмотрим Создание эскиза каждую минуту, задав режим hello tooTime (в секундах) и hello too60 интервал.</span><span class="sxs-lookup"><span data-stu-id="3c217-405">Let's create a thumbnail every minute by setting hello mode tooTime (seconds) and hello Interval too60.</span></span>

### <span data-ttu-id="3c217-406"><a id="thumbnails_to__multibitrate_MP4_color_space"></a>Работа с преобразованием цветового пространства</span><span class="sxs-lookup"><span data-stu-id="3c217-406"><a id="thumbnails_to__multibitrate_MP4_color_space"></a>Dealing with Color Space conversion</span></span>
<span data-ttu-id="3c217-407">Хотя может показаться логических ПИН-кодов без сжатия видео шлюза кадра hello и hello входных данных файла мультимедиа теперь может быть подключен, мы бы появляется предупреждение, если мы следует делать.</span><span class="sxs-lookup"><span data-stu-id="3c217-407">While it would seem logical both Uncompressed Video pins of hello frame gate and hello Media File Input can now be connected, we would get a warning if we would do so.</span></span>

![Ошибка входного цветового пространства](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-input-color-space-error.png)

<span data-ttu-id="3c217-409">*Ошибка входного цветового пространства*</span><span class="sxs-lookup"><span data-stu-id="3c217-409">*Input color space error*</span></span>

<span data-ttu-id="3c217-410">Это объясняется способ hello в какой цветной сведения представлены в наш исходный необработанный несжатые видеопотока, поступающих от наших MXF отличается от какие hello ожидается JPG кодировщика.</span><span class="sxs-lookup"><span data-stu-id="3c217-410">This is because hello way in which colour information is represented in our original raw uncompressed video stream, coming from our MXF, is different from what hello JPG Encoder is expecting.</span></span> <span data-ttu-id="3c217-411">Больше — в частности, так называемые «цветовое пространство» «RGB» или «Оттенки серого» ожидается tooflow в.</span><span class="sxs-lookup"><span data-stu-id="3c217-411">More specifically, a so-called "color space" of "RGB" or "Grayscale" is expected tooflow in.</span></span> <span data-ttu-id="3c217-412">Это означает, что входящий видеопоток, hello видео кадра Gate потребуется toohave преобразования, сначала применяется относительно его цветовое пространство.</span><span class="sxs-lookup"><span data-stu-id="3c217-412">This means that hello Video Frame Gate's inbound video stream will need toohave a conversion applied regarding its color space first.</span></span>

<span data-ttu-id="3c217-413">Перетащите hello рабочего процесса hello цвет пространства преобразователь - Intel и подключите его tooour кадра шлюза.</span><span class="sxs-lookup"><span data-stu-id="3c217-413">Drag onto hello workflow hello Color Space Converter - Intel and connect it tooour frame gate.</span></span>

![Соединение преобразователя цветового пространства](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-color-space-convertor.png)

<span data-ttu-id="3c217-415">*Соединение преобразователя цветового пространства*</span><span class="sxs-lookup"><span data-stu-id="3c217-415">*Connecting a Color Space Convertor*</span></span>

<span data-ttu-id="3c217-416">В окне свойств hello подбора hello BGR 24 входа из списка Предустановка hello.</span><span class="sxs-lookup"><span data-stu-id="3c217-416">In hello properties window, pick hello BGR 24 entry from hello Preset list.</span></span>

### <span data-ttu-id="3c217-417"><a id="thumbnails_to__multibitrate_MP4_writing_thumbnails"></a>Написание hello эскизов</span><span class="sxs-lookup"><span data-stu-id="3c217-417"><a id="thumbnails_to__multibitrate_MP4_writing_thumbnails"></a>Writing hello thumbnails</span></span>
<span data-ttu-id="3c217-418">Отличается от наших видео MP4, hello кодировщика JPG, компонент будет выдавать более одного файла.</span><span class="sxs-lookup"><span data-stu-id="3c217-418">Different from our MP4 video's, hello JPG Encoder component will output more than one file.</span></span> <span data-ttu-id="3c217-419">В порядке toodeal с этим, можно использовать компонент записи файла JPG сцены поиска: он будет принимать входящие JPG эскизы hello и записи их, имени каждого файла снабженное другой номер.</span><span class="sxs-lookup"><span data-stu-id="3c217-419">In order toodeal with this, a Scene Search JPG File Writer component can be used: it will take hello incoming JPG thumbnails and write them out, each filename being suffixed by a different number.</span></span> <span data-ttu-id="3c217-420">(hello число обычно количеству hello секунд или единицы в потоке hello, соединяющей какие эскиз hello.)</span><span class="sxs-lookup"><span data-stu-id="3c217-420">(hello number typically indicating hello number of seconds/units in hello stream which hello thumbnail was drawn from.)</span></span>

![Общие сведения о записи файла JPG поиска сцены hello](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer.png)

<span data-ttu-id="3c217-422">*Общие сведения о записи файла JPG поиска сцены hello*</span><span class="sxs-lookup"><span data-stu-id="3c217-422">*Introducing hello Scene Search JPG File Writer*</span></span>

<span data-ttu-id="3c217-423">Настройка hello путь к папке выходных данных свойство с выражением hello: ${ROOT_outputWriteDirectory}</span><span class="sxs-lookup"><span data-stu-id="3c217-423">Configure hello Output Folder Path property with hello expression: ${ROOT_outputWriteDirectory}</span></span>

<span data-ttu-id="3c217-424">и hello свойство префикса имени файла с:</span><span class="sxs-lookup"><span data-stu-id="3c217-424">and hello Filename Prefix property with:</span></span>

    ${ROOT_sourceFileBaseName}_thumb_

<span data-ttu-id="3c217-425">префикс Hello определяют правила именования файлов эскизов hello.</span><span class="sxs-lookup"><span data-stu-id="3c217-425">hello prefix will determine how hello thumbnail files are being named.</span></span> <span data-ttu-id="3c217-426">Они будут заканчиваться с число, указывающее hello ползунка позицию в потоке hello.</span><span class="sxs-lookup"><span data-stu-id="3c217-426">They will be suffixed with a number indicating hello thumb's position in hello stream.</span></span>

![Свойства компонента записи файлов JPG для поиска сцен](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer-properties.png)

<span data-ttu-id="3c217-428">*Свойства компонента записи файлов JPG для поиска сцен*</span><span class="sxs-lookup"><span data-stu-id="3c217-428">*Scene Search JPG File Writer properties*</span></span>

<span data-ttu-id="3c217-429">Подключите hello записи файла JPG поиска сцены toohello выходной файл или ресурс узел.</span><span class="sxs-lookup"><span data-stu-id="3c217-429">Connect hello Scene Search JPG File Writer toohello Output File/Asset node.</span></span>

### <span data-ttu-id="3c217-430"><a id="thumbnails_to__multibitrate_MP4_errors"></a>Обнаружение ошибок в рабочем процессе</span><span class="sxs-lookup"><span data-stu-id="3c217-430"><a id="thumbnails_to__multibitrate_MP4_errors"></a>Detecting errors in a workflow</span></span>
<span data-ttu-id="3c217-431">Подключите ввода hello hello цвет пространства преобразователь toohello необработанные без сжатия видео выходных данных.</span><span class="sxs-lookup"><span data-stu-id="3c217-431">Connect hello input of hello color space converter toohello raw uncompressed video output.</span></span> <span data-ttu-id="3c217-432">Теперь можно выполните локального тестового запуска для рабочего процесса hello.</span><span class="sxs-lookup"><span data-stu-id="3c217-432">Now perform a local test run for hello workflow.</span></span> <span data-ttu-id="3c217-433">Рабочий процесс hello высока вероятность внезапно будет останавливать выполнение и указывают красным контуром в компоненте hello, произошла ошибка:</span><span class="sxs-lookup"><span data-stu-id="3c217-433">There's a good chance hello workflow will suddenly stop executing and indicate with a red outline on hello component that encountered an error:</span></span>

![Ошибка преобразователя цветового пространства](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error.png)

<span data-ttu-id="3c217-435">*Ошибка преобразователя цветового пространства*</span><span class="sxs-lookup"><span data-stu-id="3c217-435">*Color Space Converter error*</span></span>

<span data-ttu-id="3c217-436">Щелкните hello немного красный значок «E» в верхнем правом углу hello toosee компонента цвета пространства преобразователь hello, какова причина hello hello кодирования попытка не удалась.</span><span class="sxs-lookup"><span data-stu-id="3c217-436">Click hello little red "E" icon in hello top right corner of hello Color Space Converter component toosee what's hello reason hello encoding attempt failed.</span></span>

![Диалоговое окно с ошибкой преобразователя цветового пространства](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error-dialog.png)

<span data-ttu-id="3c217-438">*Диалоговое окно с ошибкой преобразователя цветового пространства*</span><span class="sxs-lookup"><span data-stu-id="3c217-438">*Color Space Converter error dialog*</span></span>

<span data-ttu-id="3c217-439">Оказывается, как вы видите, что hello входящих цветовое пространство Стандартная hello цвет пространства преобразователя имеет rec601 toobe для наших Запрошенное преобразование YUV tooRGB.</span><span class="sxs-lookup"><span data-stu-id="3c217-439">It turns out, as you can see, that hello incoming color space standard for hello color space converter has toobe rec601 for our requested conversion of YUV tooRGB.</span></span> <span data-ttu-id="3c217-440">а в нашем потоке не указано, что он отвечает стандарту rec601.</span><span class="sxs-lookup"><span data-stu-id="3c217-440">Apparently our stream doesn't indicate it's rec601.</span></span> <span data-ttu-id="3c217-441">(Rec 601 — это стандарт кодирования чередующихся аналоговых видеосигналов в форме цифрового видео.</span><span class="sxs-lookup"><span data-stu-id="3c217-441">(Rec 601 is a standard for encoding interlaced analog video signals in digital video form.</span></span> <span data-ttu-id="3c217-442">Этот стандарт указывает активную область, охватывающую 720 отсчетов сигнала яркости и 360 цветовых отсчетов для каждой строки.</span><span class="sxs-lookup"><span data-stu-id="3c217-442">It specifies an active region covering 720 luminance samples and 360 chrominance samples per line.</span></span> <span data-ttu-id="3c217-443">цвет Hello системы кодирования называется YCbCr 4:2:2.)</span><span class="sxs-lookup"><span data-stu-id="3c217-443">hello color encoding system is known as YCbCr 4:2:2.)</span></span>

<span data-ttu-id="3c217-444">toofix это, мы будет указывать на наш поток, который мы имеем дело с содержимым rec601 hello метаданных.</span><span class="sxs-lookup"><span data-stu-id="3c217-444">toofix this, we'll indicate on hello metadata of our stream that we're dealing with rec601 content.</span></span> <span data-ttu-id="3c217-445">toodo, поэтому мы будем использовать компонент видео данных тип обновления, который мы будет размещаться между нашей необработанный источник и hello цвет пространства компонент преобразования.</span><span class="sxs-lookup"><span data-stu-id="3c217-445">toodo so we'll use a Video Data Type Updater component, which we'll put in between our raw source and hello color space conversion component.</span></span> <span data-ttu-id="3c217-446">Это средство обновления типа данных позволяет hello ручное обновление некоторых данных видео свойства типа.</span><span class="sxs-lookup"><span data-stu-id="3c217-446">This data type updater allows for hello manual update of certain video data type properties.</span></span> <span data-ttu-id="3c217-447">Настройте tooindicate цвет пространства стандарт «Rec 601».</span><span class="sxs-lookup"><span data-stu-id="3c217-447">Configure it tooindicate a Color Space Standard of "Rec 601".</span></span> <span data-ttu-id="3c217-448">Это приведет к tootag hello hello видео данных типа обновления потока с цветовое пространство «Rec 601» hello, если не было цвет места еще не определен.</span><span class="sxs-lookup"><span data-stu-id="3c217-448">This will cause hello Video Data Type Updater tootag hello stream with hello "Rec 601" color space if there was no color space defined yet.</span></span> <span data-ttu-id="3c217-449">(Он не переопределяет все существующие метаданные, если не был установлен флажок переопределения hello.)</span><span class="sxs-lookup"><span data-stu-id="3c217-449">(It will not override any existing metadata, unless hello Override checkbox was checked.)</span></span>

![Обновление стандартный цвет пространства на hello Updater тип данных](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-update-color-space-standard-on-data-type.png)

<span data-ttu-id="3c217-451">*Обновление стандартный цвет пространства на hello Updater тип данных*</span><span class="sxs-lookup"><span data-stu-id="3c217-451">*Updating Color Space Standard on hello Data Type Updater*</span></span>

### <span data-ttu-id="3c217-452"><a id="thumbnails_to__multibitrate_MP4_finish"></a>Завершенный рабочий процесс</span><span class="sxs-lookup"><span data-stu-id="3c217-452"><a id="thumbnails_to__multibitrate_MP4_finish"></a>Finished Workflow</span></span>
<span data-ttu-id="3c217-453">Теперь, когда наши завершения рабочего процесса, выполните другой toosee тестового запуска, передать его.</span><span class="sxs-lookup"><span data-stu-id="3c217-453">Now that our our workflow is finished, do another test run toosee it pass.</span></span>

![Завершенный рабочий процесс для вывода нескольких файлов MP4 с эскизами](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-for-multi-mp4-thumbnails.png)

<span data-ttu-id="3c217-455">*Завершенный рабочий процесс для вывода нескольких файлов MP4 с эскизами*</span><span class="sxs-lookup"><span data-stu-id="3c217-455">*Finished workflow for multi-mp4 output with thumbnails*</span></span>

## <span data-ttu-id="3c217-456"><a id="time_based_trim"></a>Обрезка выходных файлов MP4 с несколькими скоростями по времени</span><span class="sxs-lookup"><span data-stu-id="3c217-456"><a id="time_based_trim"></a>Time-based trimming of multibitrate MP4 output</span></span>
<span data-ttu-id="3c217-457">Начиная с рабочий процесс, который приводит к возникновению ошибки [многоскоростных MP4 вывод MXF ввода](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), мы теперь заинтересованы в обрезки hello источник видео на основе меток времени.</span><span class="sxs-lookup"><span data-stu-id="3c217-457">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into trimming hello source video based on time-stamps.</span></span>

### <span data-ttu-id="3c217-458"><a id="time_based_trim_start"></a>Добавление усечение toostart обзор рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="3c217-458"><a id="time_based_trim_start"></a>Workflow overview toostart adding trimming to</span></span>
![Запуск рабочего процесса tooadd усечение](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow-to-add-trimming.png)

<span data-ttu-id="3c217-460">*Запуск рабочего процесса tooadd усечение*</span><span class="sxs-lookup"><span data-stu-id="3c217-460">*Starting workflow tooadd trimming to*</span></span>

### <span data-ttu-id="3c217-461"><a id="time_based_trim_use_stream_trimmer"></a>С помощью hello поток устройство обрезки</span><span class="sxs-lookup"><span data-stu-id="3c217-461"><a id="time_based_trim_use_stream_trimmer"></a>Using hello Stream Trimmer</span></span>
<span data-ttu-id="3c217-462">Hello устройство обрезки поток дает tootrim hello начало и конец входной поток основан на данных о времени (секунды, минуты,...). устройство обрезки Hello не поддерживает усечения, основанных на кадре.</span><span class="sxs-lookup"><span data-stu-id="3c217-462">hello Stream Trimmer component allows tootrim hello beginning and ending of an input stream base on timing information (seconds, minutes, ...). hello trimmer does not support frame-based trimming.</span></span>

![Компонент обрезки потока](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-stream-trimmer.png)

<span data-ttu-id="3c217-464">*Компонент обрезки потока*</span><span class="sxs-lookup"><span data-stu-id="3c217-464">*Stream Trimmer*</span></span>

<span data-ttu-id="3c217-465">Вместо соединения непосредственно hello AVC кодировщиков и toohello назначено динамика позиции ввода файла мультимедиа, мы поместили между этими устройство обрезки поток hello.</span><span class="sxs-lookup"><span data-stu-id="3c217-465">Instead of linking hello AVC encoders and speaker position assigner toohello Media File Input directly, we'll put in between those hello stream trimmer.</span></span> <span data-ttu-id="3c217-466">(Один для hello видеосигнала и один для hello чередуются звуковых сигналов).</span><span class="sxs-lookup"><span data-stu-id="3c217-466">(One for hello video signal and one for hello interleaved audio signal.)</span></span>

![Добавление компонента обрезки потока](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-put-stream-trimmer-in-between.png)

<span data-ttu-id="3c217-468">*Добавление компонента обрезки потока*</span><span class="sxs-lookup"><span data-stu-id="3c217-468">*Put Stream Trimmer in between*</span></span>

<span data-ttu-id="3c217-469">Настроим устройство обрезки hello, чтобы мы будет обрабатывать только видео и аудио от 15 до 60 секунд в видео hello.</span><span class="sxs-lookup"><span data-stu-id="3c217-469">Let's configure hello trimmer so that we will only process video and audio between 15 seconds and 60 seconds in hello video.</span></span>

<span data-ttu-id="3c217-470">Перейдите toohello свойства hello устройство обрезки потока видео и настройте время начала (сумм, равных 15) и свойства времени окончания (60s).</span><span class="sxs-lookup"><span data-stu-id="3c217-470">Go toohello properties of hello Video Stream Trimmer and configure both Start Time (15s) and End Time (60s) properties.</span></span> <span data-ttu-id="3c217-471">toomake убедитесь, что и устройство обрезки нашей аудио и видео всегда настроенных toohello же начала и окончания для значений, мы опубликуем этих toohello корневой hello рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="3c217-471">toomake sure both our audio and video trimmer are always configured toohello same start and end values, we will publish those toohello root of hello workflow.</span></span>

![Публикация свойства времени начала из компонента обрезки потока](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-start-time-from-stream-trimmer.png)

<span data-ttu-id="3c217-473">*Публикация свойства времени начала из компонента обрезки потока*</span><span class="sxs-lookup"><span data-stu-id="3c217-473">*Publish start time property from Stream Trimmer*</span></span>

![Диалоговое окно публикации свойства для времени начала](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-start-time.png)

<span data-ttu-id="3c217-475">*Диалоговое окно публикации свойства для времени начала*</span><span class="sxs-lookup"><span data-stu-id="3c217-475">*Publish property dialog for start time*</span></span>

![Диалоговое окно публикации свойства для времени окончания](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-end-time.png)

<span data-ttu-id="3c217-477">*Диалоговое окно публикации свойства для времени окончания*</span><span class="sxs-lookup"><span data-stu-id="3c217-477">*Publish property dialog for end time*</span></span>

<span data-ttu-id="3c217-478">Если мы теперь проверить hello корнем рабочего процесса, оба свойства будет аккуратно отображаются и настраиваемые оттуда.</span><span class="sxs-lookup"><span data-stu-id="3c217-478">If we now inspect hello root of our workflow, both properties will be neatly displayed and configurable from there.</span></span>

![Опубликованные свойства, доступные в корне](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-properties-available-on-root.png)

<span data-ttu-id="3c217-480">*Опубликованные свойства, доступные в корне*</span><span class="sxs-lookup"><span data-stu-id="3c217-480">*Published properties available on root*</span></span>

<span data-ttu-id="3c217-481">Теперь откройте свойства усечения hello из аудио устройство обрезки hello и настроить время начала и окончания выражение со ссылкой toohello опубликованные свойства в корневом каталоге hello нашей рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="3c217-481">Now open hello trimming properties from hello audio trimmer and configure both start and end times with an expression that refers toohello published properties on hello root of our workflow.</span></span>

<span data-ttu-id="3c217-482">Время начала аудио усечения для hello:</span><span class="sxs-lookup"><span data-stu-id="3c217-482">For hello audio trimming start time:</span></span>

    ${ROOT_TrimmingStartTime}

<span data-ttu-id="3c217-483">Для времени окончания обрезки аудио:</span><span class="sxs-lookup"><span data-stu-id="3c217-483">and for its end time:</span></span>

    ${ROOT_TrimmingEndTime}

### <span data-ttu-id="3c217-484"><a id="time_based_trim_finish"></a>Завершенный рабочий процесс</span><span class="sxs-lookup"><span data-stu-id="3c217-484"><a id="time_based_trim_finish"></a>Finished Workflow</span></span>
![Завершенный рабочий процесс](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-time-base-trimming.png)

<span data-ttu-id="3c217-486">*Завершенный рабочий процесс*</span><span class="sxs-lookup"><span data-stu-id="3c217-486">*Finished Workflow*</span></span>

## <span data-ttu-id="3c217-487"><a id="scripting"></a>Знакомство с hello компонента в скрипт</span><span class="sxs-lookup"><span data-stu-id="3c217-487"><a id="scripting"></a>Introducing hello Scripted Component</span></span>
<span data-ttu-id="3c217-488">Скрипт компоненты могут выполняться произвольные скрипты этапах выполнения hello рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="3c217-488">Scripted Components can execute arbitrary scripts during hello execution phases of our workflow.</span></span> <span data-ttu-id="3c217-489">Существует четыре различных наборов символов, которые могут быть выполнены с определенными характеристиками и собственные место в жизненного цикла рабочего процесса hello:</span><span class="sxs-lookup"><span data-stu-id="3c217-489">There are four different scripts that can be executed, each with specific characteristics and their own place in hello workflow life-cycle:</span></span>

* <span data-ttu-id="3c217-490">**commandScript**</span><span class="sxs-lookup"><span data-stu-id="3c217-490">**commandScript**</span></span>
* <span data-ttu-id="3c217-491">**realizeScript**</span><span class="sxs-lookup"><span data-stu-id="3c217-491">**realizeScript**</span></span>
* <span data-ttu-id="3c217-492">**processInputScript**</span><span class="sxs-lookup"><span data-stu-id="3c217-492">**processInputScript**</span></span>
* <span data-ttu-id="3c217-493">**lifeCycleScript**</span><span class="sxs-lookup"><span data-stu-id="3c217-493">**lifeCycleScript**</span></span>

<span data-ttu-id="3c217-494">Hello документации hello в скрипт выполняется более подробно для каждого hello выше.</span><span class="sxs-lookup"><span data-stu-id="3c217-494">hello documentation of hello Scripted Component goes in more detail for each of hello above.</span></span> <span data-ttu-id="3c217-495">В [hello следующий раздел](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim), hello **realizeScript** сценарий компонента — используется tooconstruct cliplist xml на лету hello при запуске рабочего процесса hello.</span><span class="sxs-lookup"><span data-stu-id="3c217-495">In [hello following section](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim), hello **realizeScript** scripting component is used tooconstruct a cliplist xml on hello fly when hello workflow starts.</span></span> <span data-ttu-id="3c217-496">Этот сценарий вызывается во время установки компонентов hello, который происходит один раз в его жизненного цикла.</span><span class="sxs-lookup"><span data-stu-id="3c217-496">This script is called during hello component setup, which happens only once in it's lifecycle.</span></span>

### <span data-ttu-id="3c217-497"><a id="scripting_hello_world"></a>Создание сценариев в рабочем процессе: hello world</span><span class="sxs-lookup"><span data-stu-id="3c217-497"><a id="scripting_hello_world"></a>Scripting within a workflow: hello world</span></span>
<span data-ttu-id="3c217-498">Перетащите компонент включен в скрипт на область конструктора hello и переименуйте его (например, «SetClipListXML»).</span><span class="sxs-lookup"><span data-stu-id="3c217-498">Drag a Scripted Component onto hello designer surface and rename it (for example, "SetClipListXML").</span></span>

![Добавление компонента сценариев](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

<span data-ttu-id="3c217-500">*Добавление компонента сценариев*</span><span class="sxs-lookup"><span data-stu-id="3c217-500">*Adding a Scripted Component*</span></span>

<span data-ttu-id="3c217-501">При проверке свойств hello hello компонента в скрипт, приветствия отображаются четыре типа различных сценариев, каждый настраиваемых tooa другой сценарий.</span><span class="sxs-lookup"><span data-stu-id="3c217-501">When you inspect hello properties of hello Scripted Component, hello four different script types will be shown, each configurable tooa different script.</span></span>

![Свойства компонента сценариев](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

<span data-ttu-id="3c217-503">*Свойства компонента сценариев*</span><span class="sxs-lookup"><span data-stu-id="3c217-503">*Scripted Component properties*</span></span>

<span data-ttu-id="3c217-504">Отмените hello processInputScript и откройте редактор hello для hello realizeScript.</span><span class="sxs-lookup"><span data-stu-id="3c217-504">Clear hello processInputScript and open hello editor for hello realizeScript.</span></span> <span data-ttu-id="3c217-505">Теперь мы установлено и Готово toostart сценариев.</span><span class="sxs-lookup"><span data-stu-id="3c217-505">Now we're set up and ready toostart scripting.</span></span>

<span data-ttu-id="3c217-506">Скрипты на языке Groovy динамически скомпилированного язык сценариев для hello Java platform, сохраняет совместимость с Java.</span><span class="sxs-lookup"><span data-stu-id="3c217-506">Scripts are written in Groovy, a dynamically compiled scripting language for hello Java platform that retains compatibility with Java.</span></span> <span data-ttu-id="3c217-507">Фактически, практически весь код Java можно использовать в качестве кода Groovy.</span><span class="sxs-lookup"><span data-stu-id="3c217-507">Actually, most Java code is valid Groovy code.</span></span>

<span data-ttu-id="3c217-508">В контексте hello нашей realizeScript напишем сценарий хорошую простой hello world.</span><span class="sxs-lookup"><span data-stu-id="3c217-508">Let's write a simple hello world groovy script in hello context of our realizeScript.</span></span> <span data-ttu-id="3c217-509">Введите в редакторе hello hello следующие данные:</span><span class="sxs-lookup"><span data-stu-id="3c217-509">Enter hello following in hello editor:</span></span>

    node.log("hello world");

<span data-ttu-id="3c217-510">Теперь выполните локальный тестовый запуск.</span><span class="sxs-lookup"><span data-stu-id="3c217-510">Now execute a local test run.</span></span> <span data-ttu-id="3c217-511">После этого запуска проверки (через вкладку система hello на hello в скрипт компонента) hello свойство журналы.</span><span class="sxs-lookup"><span data-stu-id="3c217-511">After this run, inspect (through hello System tab on hello Scripted Component) hello Logs property.</span></span>

![Запись "hello world" в журнале](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output.png)

<span data-ttu-id="3c217-513">*Запись "hello world" в журнале*</span><span class="sxs-lookup"><span data-stu-id="3c217-513">*Hello world log output*</span></span>

<span data-ttu-id="3c217-514">Hello объекта узла, которые мы называем метод журнала hello, ссылается текущий tooour «узел» или hello компонент, который мы сценарии в рамках.</span><span class="sxs-lookup"><span data-stu-id="3c217-514">hello node object we call hello log method on, refers tooour current "node" or hello component we're scripting within.</span></span> <span data-ttu-id="3c217-515">Таким образом, каждый компонент имеет hello данных журналов toooutput возможности, доступные через вкладка "система" hello. В этом случае мы вывода строковый литерал hello «hello world».</span><span class="sxs-lookup"><span data-stu-id="3c217-515">Every component as such has hello ability toooutput logging data, available through hello system tab. In this case, we output hello string literal "hello world".</span></span> <span data-ttu-id="3c217-516">Здесь важно toounderstand заключается в том, что это может оказаться toobe бесценным средством отладки, предоставляя подробные сведения о делать какие сценарии hello.</span><span class="sxs-lookup"><span data-stu-id="3c217-516">Important toounderstand here is that this can prove toobe an invaluable debugging tool, providing you with insight on what hello script is actually doing.</span></span>

<span data-ttu-id="3c217-517">Из в нашей среде скриптов, нам требуется также tooproperties доступа от других компонентов.</span><span class="sxs-lookup"><span data-stu-id="3c217-517">From within our scripting environment, we also have access tooproperties on other components.</span></span> <span data-ttu-id="3c217-518">Попробуйте выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="3c217-518">Try this:</span></span>

    //inspect current node:
    def nodepath = node.getNodePath();
    node.log("this node path: " + nodepath);

    //walking up tooother nodes:
    def parentnode = node.getParentNode();
    def parentnodepath = parentnode.getNodePath();
    node.log("parent node path: " + parentnodepath);

    //read properties from a node:
    def sourceFileExt = parentnode.getPropertyAsString( "sourceFileExtension", null );
    def sourceFileName = parentnode.getPropertyAsString("sourceFileBaseName", null);
    node.log("source file name with extension " + sourceFileExt + " is: " + sourceFileName);

<span data-ttu-id="3c217-519">Наш окно журнала будут показаны следующие hello:</span><span class="sxs-lookup"><span data-stu-id="3c217-519">Our log window will show us hello following:</span></span>

![Вывод журнала для доступа к путям узла](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output2.png)

<span data-ttu-id="3c217-521">*Вывод журнала для доступа к путям узла*</span><span class="sxs-lookup"><span data-stu-id="3c217-521">*Log output for accessing node paths*</span></span>

## <span data-ttu-id="3c217-522"><a id="frame_based_trim"></a>Обрезка выходных файлов MP4 с несколькими скоростями по кадрам</span><span class="sxs-lookup"><span data-stu-id="3c217-522"><a id="frame_based_trim"></a>Frame-based trimming of multibitrate MP4 output</span></span>
<span data-ttu-id="3c217-523">Начиная с рабочий процесс, который приводит к возникновению ошибки [многоскоростных MP4 вывод MXF ввода](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), мы теперь заинтересованы в обрезки hello исходного видео, в зависимости от числа кадров.</span><span class="sxs-lookup"><span data-stu-id="3c217-523">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into trimming hello source video based on frame counts.</span></span>

### <span data-ttu-id="3c217-524"><a id="frame_based_trim_start"></a>План toostart Общие сведения о добавлении усечение</span><span class="sxs-lookup"><span data-stu-id="3c217-524"><a id="frame_based_trim_start"></a>Blueprint overview toostart adding trimming to</span></span>
![Добавление усечение toostart рабочего процесса](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-workflow-start-adding-trimming-to.png)

<span data-ttu-id="3c217-526">*Добавление усечение toostart рабочего процесса*</span><span class="sxs-lookup"><span data-stu-id="3c217-526">*Workflow toostart adding trimming to*</span></span>

### <span data-ttu-id="3c217-527"><a id="frame_based_trim_clip_list"></a>С помощью hello клип списка XML</span><span class="sxs-lookup"><span data-stu-id="3c217-527"><a id="frame_based_trim_clip_list"></a>Using hello Clip List XML</span></span>
<span data-ttu-id="3c217-528">В всех предыдущих занятий рабочего процесса мы использовали компонент входного файла мультимедиа hello как наши видео источника входных данных.</span><span class="sxs-lookup"><span data-stu-id="3c217-528">In all previous workflow tutorials, we used hello Media File Input component as our video input source.</span></span> <span data-ttu-id="3c217-529">Для этого конкретного сценария, мы будем работать с hello клип списка исходный компонент вместо него.</span><span class="sxs-lookup"><span data-stu-id="3c217-529">For this specific scenario though, we'll be using hello Clip List Source component instead.</span></span> <span data-ttu-id="3c217-530">Обратите внимание, что это не должна быть hello предпочтительный способ работы; Используйте hello источника коллекции списка, только если имеется toodo особого смысла, так (как и в hello ниже вариант, где мы сделали использование возможностей фильтрации по ролям список clip hello).</span><span class="sxs-lookup"><span data-stu-id="3c217-530">Note that this should not be hello preferred way of working; only use hello Clip List Source when there's a real reason toodo so (like in hello below case, where we're making use of hello clip list trimming capabilities).</span></span>

<span data-ttu-id="3c217-531">tooswitch из наших toohello вход файл мультимедиа источника коллекции списка, перетащите hello клип списка исходный компонент в рабочую область конструктора hello и подключите hello XML-Clip список ПИН-код toohello клип списка XML узел hello конструктора рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="3c217-531">tooswitch from our Media File Input toohello Clip List Source, drag hello Clip List Source component onto hello design surface and connect hello Clip List XML pin toohello Clip List XML node of hello workflow designer.</span></span> <span data-ttu-id="3c217-532">Это необходимо заполнить hello источника коллекции списка с выходных контактов, в соответствии с tooour входное видео.</span><span class="sxs-lookup"><span data-stu-id="3c217-532">This should populate hello Clip List Source with output pins, according tooour input video.</span></span> <span data-ttu-id="3c217-533">Теперь подключение hello без сжатия видео и аудио несжатые ПИН-коды из toohello источника списка Clip hello hello соответствующих AVC кодировщиков и Interleaver поток аудио.</span><span class="sxs-lookup"><span data-stu-id="3c217-533">Now connect hello Uncompressed Video and Uncompressed Audio pins from hello hello Clip List Source toohello respective AVC Encoders and Audio Stream Interleaver.</span></span> <span data-ttu-id="3c217-534">Теперь можно удалите hello входных данных файла мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="3c217-534">Now remove hello Media File Input.</span></span>

![Заменены hello источника списка Clip hello вход файл мультимедиа](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-replaced-media-file-with-clip-source.png)

<span data-ttu-id="3c217-536">*Заменены hello источника списка Clip hello вход файл мультимедиа*</span><span class="sxs-lookup"><span data-stu-id="3c217-536">*Replaced hello Media File Input with hello Clip List Source*</span></span>

<span data-ttu-id="3c217-537">Hello клип списка исходный компонент принимает в качестве входного «XML клип списка».</span><span class="sxs-lookup"><span data-stu-id="3c217-537">hello Clip List Source component takes as its input a "Clip List XML".</span></span> <span data-ttu-id="3c217-538">При выборе hello исходный файл tootest с локально, этот XML-документ клип список автоматически заполняется автоматически.</span><span class="sxs-lookup"><span data-stu-id="3c217-538">When selecting hello source file tootest with locally, this clip list xml is auto-populated for you.</span></span>

![Автоматически заполненное свойство "XML-файл списка клипов"](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-auto-populated-clip-list-xml-property.png)

<span data-ttu-id="3c217-540">*Автоматически заполненное свойство "XML-файл списка клипов"*</span><span class="sxs-lookup"><span data-stu-id="3c217-540">*Auto-populated Clip List XML property*</span></span>

<span data-ttu-id="3c217-541">Нужна немного более подробно toohello xml, это, как оно выглядит:</span><span class="sxs-lookup"><span data-stu-id="3c217-541">Looking a bit closer toohello xml, this is how it looks like:</span></span>

![Диалоговое окно изменения списка клипов](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-edit-clip-list-dialog.png)

<span data-ttu-id="3c217-543">*Диалоговое окно изменения списка клипов*</span><span class="sxs-lookup"><span data-stu-id="3c217-543">*Edit clip list dialog*</span></span>

<span data-ttu-id="3c217-544">Однако это не отражает возможности hello hello клип списка xml.</span><span class="sxs-lookup"><span data-stu-id="3c217-544">This however does not reflect hello capabilities of hello clip list xml.</span></span> <span data-ttu-id="3c217-545">У нас есть один параметр — tooadd элемент «Обрезать» в разделе hello видео и аудио источника, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="3c217-545">One option we have is tooadd a "Trim" element under both hello video and audio source, like this:</span></span>

![Добавление списка clip toohello обрезки элемента](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-trim-element-to-clip-list.png)

<span data-ttu-id="3c217-547">*Добавление списка clip toohello обрезки элемента*</span><span class="sxs-lookup"><span data-stu-id="3c217-547">*Adding a trim element toohello clip list*</span></span>

<span data-ttu-id="3c217-548">Если изменять список XML-clip hello следующим выше и выполнения локального тестового запуска, вы увидите видео hello были правильно усекаются от 10 до 20 секунд в видео hello.</span><span class="sxs-lookup"><span data-stu-id="3c217-548">If you modify hello clip list xml like this above and perform a local test run, you'll see hello video correctly been trimmed between 10 and 20 seconds in hello video.</span></span>

<span data-ttu-id="3c217-549">Противоположные toowhat происходит при выполнении локального запуска, хотя это то же самое cliplist xml не будет иметь тот же эффект, при применении в рабочий процесс, который выполняется в Azure Media Services hello.</span><span class="sxs-lookup"><span data-stu-id="3c217-549">Contrary toowhat happens when you do a local run though, this very same cliplist xml would not have hello same effect when applied in a workflow that runs in Azure Media Services.</span></span> <span data-ttu-id="3c217-550">При запуске кодировщика Premium в Azure, hello cliplist xml создается каждый раз, чтобы еще раз, на основании кодирования hello hello входного файла был передан задания.</span><span class="sxs-lookup"><span data-stu-id="3c217-550">When Azure Premium Encoder starts, hello cliplist xml is generated every time again, based on hello input file hello encoding job was given.</span></span> <span data-ttu-id="3c217-551">Это означает, что любые изменения, которые мы делаем hello XML-был бы к сожалению переопределен.</span><span class="sxs-lookup"><span data-stu-id="3c217-551">This means that any changes we do on hello xml would unfortunately be overridden.</span></span>

<span data-ttu-id="3c217-552">toocounter hello cliplist xml стирание памяти при запуске задания кодирования, мы повторно создать его на лету hello сразу после начала hello нашей рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="3c217-552">toocounter hello cliplist xml being wiped when an encoding job is started, we can re-generate it on hello fly just after hello start of our workflow.</span></span> <span data-ttu-id="3c217-553">Такие действия можно выполнять с помощью компонента сценариев.</span><span class="sxs-lookup"><span data-stu-id="3c217-553">Such custom actions can be taken through what is called a "Scripted Component".</span></span> <span data-ttu-id="3c217-554">Дополнительные сведения см. в разделе [введение hello в скрипт компонента](media-services-media-encoder-premium-workflow-tutorials.md#scripting).</span><span class="sxs-lookup"><span data-stu-id="3c217-554">For more information, see [Introducing hello Scripted Component](media-services-media-encoder-premium-workflow-tutorials.md#scripting).</span></span>

<span data-ttu-id="3c217-555">Перетащите компонент включен в скрипт на область конструктора hello и переименуйте его слишком «SetClipListXML».</span><span class="sxs-lookup"><span data-stu-id="3c217-555">Drag a Scripted Component onto hello designer surface and rename it too"SetClipListXML".</span></span>

![Добавление компонента сценариев](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

<span data-ttu-id="3c217-557">*Добавление компонента сценариев*</span><span class="sxs-lookup"><span data-stu-id="3c217-557">*Adding a Scripted Component*</span></span>

<span data-ttu-id="3c217-558">При проверке свойств hello hello компонента в скрипт, приветствия отображаются четыре типа различных сценариев, каждый настраиваемых tooa другой сценарий.</span><span class="sxs-lookup"><span data-stu-id="3c217-558">When you inspect hello properties of hello Scripted Component, hello four different script types will be shown, each configurable tooa different script.</span></span>

![Свойства компонента сценариев](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

<span data-ttu-id="3c217-560">*Свойства компонента сценариев*</span><span class="sxs-lookup"><span data-stu-id="3c217-560">*Scripted Component properties*</span></span>

### <span data-ttu-id="3c217-561"><a id="frame_based_trim_modify_clip_list"></a>Изменение списка hello клип из компонента в скрипт</span><span class="sxs-lookup"><span data-stu-id="3c217-561"><a id="frame_based_trim_modify_clip_list"></a>Modifying hello clip list from a Scripted Component</span></span>
<span data-ttu-id="3c217-562">Прежде чем повторно можно написать hello cliplist xml, который создается во время запуска рабочего процесса, мы должны, toohave доступ toohello cliplist xml свойства и содержимое.</span><span class="sxs-lookup"><span data-stu-id="3c217-562">Before we can re-write hello cliplist xml that is generated during workflow startup, we'll need toohave access toohello cliplist xml property and contents.</span></span> <span data-ttu-id="3c217-563">Это можно сделать следующим образом.</span><span class="sxs-lookup"><span data-stu-id="3c217-563">We can do so like this:</span></span>

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: " + clipListXML);

![Записи о входящем списке клипов в журнале](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-incoming-clip-list-logged.png)

<span data-ttu-id="3c217-565">*Записи о входящем списке клипов в журнале*</span><span class="sxs-lookup"><span data-stu-id="3c217-565">*Incoming clip list being logged*</span></span>

<span data-ttu-id="3c217-566">Сначала мы должны toodetermine способом начиная с какого момента до чего мы хотим tootrim hello видео.</span><span class="sxs-lookup"><span data-stu-id="3c217-566">First we need a way toodetermine from which point till which point we want tootrim hello video.</span></span> <span data-ttu-id="3c217-567">Публикация этого пользователя-специалистами удобный toohello hello рабочего процесса, toomake два свойства toohello корень графа hello.</span><span class="sxs-lookup"><span data-stu-id="3c217-567">toomake this convenient toohello less-technical user of hello workflow, publish two properties toohello root of hello graph.</span></span> <span data-ttu-id="3c217-568">toodo это, щелкните правой кнопкой мыши область конструктора hello и выберите «Добавить свойство»:</span><span class="sxs-lookup"><span data-stu-id="3c217-568">toodo this, right click hello designer surface and select "Add Property":</span></span>

* <span data-ttu-id="3c217-569">Первое свойство — ClippingTimeStart. Тип — TIMECODE.</span><span class="sxs-lookup"><span data-stu-id="3c217-569">First property: "ClippingTimeStart" of type: "TIMECODE"</span></span>
* <span data-ttu-id="3c217-570">Второе свойство — ClippingTimeEnd. Тип — TIMECODE.</span><span class="sxs-lookup"><span data-stu-id="3c217-570">Second property: "ClippingTimeEnd" of type: "TIMECODE"</span></span>

![Диалоговое окно добавления свойства для времени начала обрезки](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-start-time.png)

<span data-ttu-id="3c217-572">*Диалоговое окно добавления свойства для времени начала обрезки*</span><span class="sxs-lookup"><span data-stu-id="3c217-572">*Add Property dialog for clipping start time*</span></span>

![Опубликованные свойства времени обрезки в корне рабочего процесса](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-time-props.png)

<span data-ttu-id="3c217-574">*Опубликованные свойства времени обрезки в корне рабочего процесса*</span><span class="sxs-lookup"><span data-stu-id="3c217-574">*Published clipping time props on workflow root*</span></span>

<span data-ttu-id="3c217-575">Настройте оба свойства tooa подходящее значение.</span><span class="sxs-lookup"><span data-stu-id="3c217-575">Configure both properties tooa suitable value:</span></span>

![Настройка hello, изменение свойств начала и окончания](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configure-clip-start-end-prop.png)

<span data-ttu-id="3c217-577">*Настройка hello, изменение свойств начала и окончания*</span><span class="sxs-lookup"><span data-stu-id="3c217-577">*Configure hello clipping start and end properties*</span></span>

<span data-ttu-id="3c217-578">Теперь оба свойства можно передать в сценарий.</span><span class="sxs-lookup"><span data-stu-id="3c217-578">Now, from within our script, we can access both properties, like this:</span></span>

    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    node.log("clipping start: " + clipstart);
    node.log("clipping end: " + clipend);

![Окно журнала, показывающее начало и конец обрезки](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-show-start-end-clip.png)

<span data-ttu-id="3c217-580">*Окно журнала, показывающее начало и конец обрезки*</span><span class="sxs-lookup"><span data-stu-id="3c217-580">*Log window showing start and end of clipping*</span></span>

<span data-ttu-id="3c217-581">Давайте анализ строк hello код времени в виде toouse более удобным, с помощью простого регулярного выражения:</span><span class="sxs-lookup"><span data-stu-id="3c217-581">Let's parse hello timecode strings into a more convenient toouse form, using a simple regular expression:</span></span>

    //parse hello start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse hello end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);
    node.log("framerate end is: " + endframerate);

![Окно журнала с преобразованными кодами времени](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-output-parsed-timecode.png)

<span data-ttu-id="3c217-583">*Окно журнала с преобразованными кодами времени*</span><span class="sxs-lookup"><span data-stu-id="3c217-583">*Log window with output of parsed timecode*</span></span>

<span data-ttu-id="3c217-584">Под рукой такую информацию теперь можете изменить hello cliplist xml tooreflect hello начала и время окончания hello требуемого точные рамки обрезки hello фильма.</span><span class="sxs-lookup"><span data-stu-id="3c217-584">With this information at hand, we can now modify hello cliplist xml tooreflect hello start and end times for hello desired frame-accurate clipping of hello movie.</span></span>

![Элементы trim tooadd код сценария](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-trim-elements.png)

<span data-ttu-id="3c217-586">*Элементы trim tooadd код сценария*</span><span class="sxs-lookup"><span data-stu-id="3c217-586">*Script code tooadd trim elements*</span></span>

<span data-ttu-id="3c217-587">Мы это сделали с помощью обычных операций по обработке строк.</span><span class="sxs-lookup"><span data-stu-id="3c217-587">This was done through normal string manipulation operations.</span></span> <span data-ttu-id="3c217-588">Hello результирующий xml списка измененной картинки записываются обратно свойство clipListXML toohello в корневом каталоге hello рабочего процесса с помощью метода SetProperty» —» hello.</span><span class="sxs-lookup"><span data-stu-id="3c217-588">hello resulting modified clip list xml is written back toohello clipListXML property on hello workflow root through hello "setProperty" method.</span></span> <span data-ttu-id="3c217-589">окно журнала Hello после другого теста будет показывать нам hello следующие:</span><span class="sxs-lookup"><span data-stu-id="3c217-589">hello log window after another test run would show us hello following:</span></span>

![Ведение журнала hello полученный список клип](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-result-clip-list.png)

<span data-ttu-id="3c217-591">*Ведение журнала hello полученный список клип*</span><span class="sxs-lookup"><span data-stu-id="3c217-591">*Logging hello resulting clip list*</span></span>

<span data-ttu-id="3c217-592">Сделайте toosee тестового запуска, как видео- и аудиопотоки hello было обрезано.</span><span class="sxs-lookup"><span data-stu-id="3c217-592">Do a test-run toosee how hello video and audio streams have been clipped.</span></span> <span data-ttu-id="3c217-593">Вам предстоит выполнить более одного тестового запуска с различными значениями для точки усечения hello, вы заметите, что те будет не принимать во внимание Однако!</span><span class="sxs-lookup"><span data-stu-id="3c217-593">As you'll do more than one test-run with different values for hello trimming points, you'll notice that those will not be taken into account however!</span></span> <span data-ttu-id="3c217-594">Hello причиной этого является hello конструктора, в отличие от hello среды выполнения Azure, не переопределение hello cliplist xml каждого запуска.</span><span class="sxs-lookup"><span data-stu-id="3c217-594">hello reason for this is that hello designer, unlike hello Azure runtime, does NOT override hello cliplist xml every run.</span></span> <span data-ttu-id="3c217-595">Это означает, что только hello первом установки hello и выхода из системы точек, будет привести hello xml tootransform, все другие hello постоянно, в нашей guard предложения (если (clipListXML.indexOf («<trim>») == -1)) предотвратит добавление другого trim hello рабочего процесса элемент, если таковой уже существует.</span><span class="sxs-lookup"><span data-stu-id="3c217-595">This means that only hello very first time you have set hello in and out points, will cause hello xml tootransform, all hello other times, our guard clause (if(clipListXML.indexOf("<trim>") == -1)) will prevent hello workflow from adding another trim element when there's already one present.</span></span>

<span data-ttu-id="3c217-596">toomake наш рабочий процесс удобный tootest локально, мы наиболее добавить хранение дома код, который проверяет, если trim элемент уже существует.</span><span class="sxs-lookup"><span data-stu-id="3c217-596">toomake our workflow convenient tootest locally, we best add some house-keeping code that inspects if a trim element was already present.</span></span> <span data-ttu-id="3c217-597">Если Да, мы можем удалить перед продолжением путем изменения XML-кода hello с новыми значениями hello.</span><span class="sxs-lookup"><span data-stu-id="3c217-597">If so, we can remove it before continuing by modifying hello xml with hello new values.</span></span> <span data-ttu-id="3c217-598">Вместо использования простых операций со строками, это, возможно, более безопасные toodo этого с помощью объекта реальные xml модели синтаксического анализа.</span><span class="sxs-lookup"><span data-stu-id="3c217-598">Rather than using plain string manipulations, it's probably safer toodo this through real xml object model parsing.</span></span>

<span data-ttu-id="3c217-599">Для такой код можно добавить Впрочем, мы потребуется tooadd нашей сценария сначала запустить несколько операторов импорта на hello.</span><span class="sxs-lookup"><span data-stu-id="3c217-599">Before we can add such code though, we'll need tooadd a number of import statements at hello start of our script first:</span></span>

    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

<span data-ttu-id="3c217-600">После этого можно добавить необходимые очистки кода hello:</span><span class="sxs-lookup"><span data-stu-id="3c217-600">After this, we can add hello required cleaning code:</span></span>

    //for local testing: delete any pre-existing trim elements from hello clip list xml by parsing hello xml into a DOM:
    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find hello trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements,dom,XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about toodelete any existing trim nodes");
     //delete hello trim nodes:
    elementsToDelete.each{
        e -> e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize hello modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

<span data-ttu-id="3c217-601">Этот код представляет над hello точки, с которой мы добавляем toohello cliplist hello trim элементы xml.</span><span class="sxs-lookup"><span data-stu-id="3c217-601">This code goes just above hello point at which we add hello trim elements toohello cliplist xml.</span></span>

<span data-ttu-id="3c217-602">На этом этапе мы запустить и изменить можно как почти так же, мы хотим во время изменения hello, когда-либо применены время рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="3c217-602">At this point, we can run and modify our workflow as much as we want while having hello changes applied ever time.</span></span>    

### <span data-ttu-id="3c217-603"><a id="frame_based_trim_clippingenabled_prop"></a>Добавление удобного свойства ClippingEnabled</span><span class="sxs-lookup"><span data-stu-id="3c217-603"><a id="frame_based_trim_clippingenabled_prop"></a>Adding a ClippingEnabled convenience property</span></span>
<span data-ttu-id="3c217-604">Может не всегда необходимо toohappen усечения, давайте завершить создание рабочего процесса, добавив удобный логический флаг, который указывает ли мы хотим tooenable обрезки / обрезки.</span><span class="sxs-lookup"><span data-stu-id="3c217-604">As you might not always want trimming toohappen, let's finish off our workflow by adding a convenient boolean flag that indicates whether or not we want tooenable trimming / clipping.</span></span>

<span data-ttu-id="3c217-605">Так же как и ранее, публикации новый корневой элемент toohello свойство из наших рабочий процесс с именем «ClippingEnabled» типа «BOOLEAN».</span><span class="sxs-lookup"><span data-stu-id="3c217-605">Just as before, publish a new property toohello root of our workflow called "ClippingEnabled" of type "BOOLEAN".</span></span>

![Публикация свойства для включения обрезки](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-enable-clip.png)

<span data-ttu-id="3c217-607">*Публикация свойства для включения обрезки*</span><span class="sxs-lookup"><span data-stu-id="3c217-607">*Published a property for enabling clipping*</span></span>

<span data-ttu-id="3c217-608">С hello ниже простое условие предложения мы установите флажок, если требуется фильтрация по ролям и решить, если наш список clip таким образом должен toobe, изменены или нет.</span><span class="sxs-lookup"><span data-stu-id="3c217-608">With hello below simple guard clause, we can check if trimming is required and decide if our clip list as such needs toobe modified or not.</span></span>

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }


### <span data-ttu-id="3c217-609"><a id="code"></a>Полный код</span><span class="sxs-lookup"><span data-stu-id="3c217-609"><a id="code"></a>Complete code</span></span>
    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: \n" + clipListXML);
    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    //parse hello start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse hello end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);

    node.log("framerate end is: " + endframerate);

    //for local testing: delete any pre-existing trim elements
    //from hello clip list xml by parsing hello xml into a DOM:

    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find hello trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements, dom, XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about toodelete any existing trim nodes");
    //delete hello trim nodes:
    elementsToDelete.each{ e ->
        e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize hello modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }

    //add trim elements toocliplist xml
    if ( clipListXML.indexOf("<trim>") == -1 )
    {
        //trim video
        clipListXML = clipListXML.replace("<videoSource>","<videoSource>\n <trim>\n <inPoint fps=\""+
            startframerate +"\">" + starttimecode +
            "</inPoint>\n" + "<outPoint fps=\"" + endframerate +"\"> " + endtimecode +
            " </outPoint>\n </trim> \n");
        //trim audio
        clipListXML = clipListXML.replace("<audioSource>","<audioSource>\n <trim>\n <inPoint fps=\""+
            startframerate +"\">" + starttimecode +
            "</inPoint>\n" + "<outPoint fps=\""+ endframerate +"\">" +
            endtimecode + "</outPoint>\n </trim>\n");
        node.log( "clip list going out: \n" +clipListXML );
        node.setProperty("../clipListXml",clipListXML);
    }


## <a name="also-see"></a><span data-ttu-id="3c217-610">См. также:</span><span class="sxs-lookup"><span data-stu-id="3c217-610">Also see</span></span>
[<span data-ttu-id="3c217-611">Знакомство со Службой кодирования категории "Премиум" в службах мультимедиа Azure</span><span class="sxs-lookup"><span data-stu-id="3c217-611">Introducing Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)

[<span data-ttu-id="3c217-612">Как tooUse расширенной кодировки в службах мультимедиа Azure</span><span class="sxs-lookup"><span data-stu-id="3c217-612">How tooUse Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)

[<span data-ttu-id="3c217-613">Обзор и сравнение кодировщиков мультимедиа Azure по запросу</span><span class="sxs-lookup"><span data-stu-id="3c217-613">Encoding On-Demand Content with Azure Media Service</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)

[<span data-ttu-id="3c217-614">Форматы и кодеки рабочего процесса Premium Media Encoder</span><span class="sxs-lookup"><span data-stu-id="3c217-614">Media Encoder Premium Workflow Formats and Codecs</span></span>](media-services-premium-workflow-encoder-formats.md)

[<span data-ttu-id="3c217-615">Примеры файлов рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="3c217-615">Sample workflow files</span></span>](http://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows)

[<span data-ttu-id="3c217-616">Средство Explorer для служб мультимедиа Azure</span><span class="sxs-lookup"><span data-stu-id="3c217-616">Azure Media Services Explorer tool</span></span>](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a><span data-ttu-id="3c217-617">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="3c217-617">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="3c217-618">Отзывы</span><span class="sxs-lookup"><span data-stu-id="3c217-618">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
