---
title: "Пошаговое руководство скрытия лиц с помощью аналитики мультимедиа Azure | Документация Майкрософт"
description: "В этом разделе приведены пошаговые инструкции по выполнению полного рабочего процесса скрытия с помощью Azure Media Services Explorer (AMSE) и Azure Media Redactor Visualizer (инструмент с открытым кодом)."
services: media-services
documentationcenter: 
author: Lichard
manager: cfowler
editor: 
ms.assetid: d6fa21b8-d80a-41b7-80c1-ff1761bc68f2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/03/2017
ms.author: rli; juliako;
ms.openlocfilehash: c0c622237f8cdca65fb6933f14cc21e9eb9ac036
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="redact-faces-with-azure-media-analytics-walkthrough"></a><span data-ttu-id="ddf9c-103">Пошаговое руководство скрытия лиц с помощью аналитики мультимедиа Azure</span><span class="sxs-lookup"><span data-stu-id="ddf9c-103">Redact faces with Azure Media Analytics walkthrough</span></span>

## <a name="overview"></a><span data-ttu-id="ddf9c-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="ddf9c-104">Overview</span></span>

<span data-ttu-id="ddf9c-105">**Редактор мультимедиа Azure** — это обработчик [медиа-аналитики Azure ](media-services-analytics-overview.md) с возможностью масштабируемого скрытия лиц в облаке.</span><span class="sxs-lookup"><span data-stu-id="ddf9c-105">**Azure Media Redactor** is an [Azure Media Analytics](media-services-analytics-overview.md) media processor (MP) that offers scalable face redaction in the cloud.</span></span> <span data-ttu-id="ddf9c-106">Функция скрытия лиц позволяет изменять видео, размывая изображения лиц выбранных пользователей.</span><span class="sxs-lookup"><span data-stu-id="ddf9c-106">Face redaction enables you to modify your video in order to blur faces of selected individuals.</span></span> <span data-ttu-id="ddf9c-107">Вы можете использовать функцию скрытия лиц в ситуациях, требующих соблюдения общественной безопасности, а также при работе с новостями.</span><span class="sxs-lookup"><span data-stu-id="ddf9c-107">You may want to use the face redaction service in public safety and news media scenarios.</span></span> <span data-ttu-id="ddf9c-108">Редактирование короткого материала с несколькими лицами вручную может занять несколько часов, тогда как при использовании функции скрытия лиц достаточно выполнить несколько простых действий.</span><span class="sxs-lookup"><span data-stu-id="ddf9c-108">A few minutes of footage that contains multiple faces can take hours to redact manually, but with this service the face redaction process will require just a few simple steps.</span></span> <span data-ttu-id="ddf9c-109">Дополнительные сведения см. в [этом блоге](https://azure.microsoft.com/blog/azure-media-redactor/).</span><span class="sxs-lookup"><span data-stu-id="ddf9c-109">For  more information, see [this](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span></span>

<span data-ttu-id="ddf9c-110">Подробные сведения о **Azure Media Redactor** см. в разделе [Скрытие лиц с помощью медиа-аналитики Azure](media-services-face-redaction.md).</span><span class="sxs-lookup"><span data-stu-id="ddf9c-110">For details about  **Azure Media Redactor**, see the [Face redaction overview](media-services-face-redaction.md) topic.</span></span>

<span data-ttu-id="ddf9c-111">В этом разделе приведены пошаговые инструкции по выполнению полного рабочего процесса скрытия с помощью Azure Media Services Explorer (AMSE) и Azure Media Redactor Visualizer (инструмент с открытым кодом).</span><span class="sxs-lookup"><span data-stu-id="ddf9c-111">This topic shows step by step instructions on how to run a full redaction workflow using Azure Media Services Explorer (AMSE) and Azure Media Redactor Visualizer (open source tool).</span></span>

<span data-ttu-id="ddf9c-112">Сейчас **редактор мультимедиа Azure Media** доступен в предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="ddf9c-112">The **Azure Media Redactor** MP is currently in Preview.</span></span> <span data-ttu-id="ddf9c-113">Он доступен во всех общедоступных регионах Azure, а также в центрах обработки данных для государственных организаций США и для Китая.</span><span class="sxs-lookup"><span data-stu-id="ddf9c-113">It is available in all public Azure regions as well as US Government and China data centers.</span></span> <span data-ttu-id="ddf9c-114">В настоящее время эта предварительная версия предоставляется бесплатно.</span><span class="sxs-lookup"><span data-stu-id="ddf9c-114">This preview is currently free of charge.</span></span> <span data-ttu-id="ddf9c-115">В текущем выпуске продолжительность обработки видео ограничена 10 минутами.</span><span class="sxs-lookup"><span data-stu-id="ddf9c-115">In the current release, there is a 10 minute limit on processed video length.</span></span>

<span data-ttu-id="ddf9c-116">Дополнительную информацию см. в [этом](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) блоге.</span><span class="sxs-lookup"><span data-stu-id="ddf9c-116">For more information, see [this](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) blog.</span></span>

## <a name="azure-media-services-explorer-workflow"></a><span data-ttu-id="ddf9c-117">Рабочий процесс Azure Media Services Explorer</span><span class="sxs-lookup"><span data-stu-id="ddf9c-117">Azure Media Services Explorer workflow</span></span>

<span data-ttu-id="ddf9c-118">Проще всего приступить к работе с Redactor можно с помощью инструмента с открытым кодом AMSE на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="ddf9c-118">The easiest way to get started with Redactor is to use the open source AMSE tool on github.</span></span> <span data-ttu-id="ddf9c-119">Можно выполнить упрощенный рабочий процесс в **комбинированном** режиме, если не требуется доступ к аннотациям в формате JSON или изображениям лиц в формате JPG.</span><span class="sxs-lookup"><span data-stu-id="ddf9c-119">You can run a simplified workflow via **combined** mode if you don’t need access to the annotation json or the face jpg images.</span></span>

### <a name="download-and-setup"></a><span data-ttu-id="ddf9c-120">Скачивание и установка</span><span class="sxs-lookup"><span data-stu-id="ddf9c-120">Download and setup</span></span>

1. <span data-ttu-id="ddf9c-121">Скачайте инструмент AMSE [отсюда](https://github.com/Azure/Azure-Media-Services-Explorer).</span><span class="sxs-lookup"><span data-stu-id="ddf9c-121">Download the AMSE tool from [here](https://github.com/Azure/Azure-Media-Services-Explorer).</span></span>
1. <span data-ttu-id="ddf9c-122">Войдите в свою учетную запись служб мультимедиа с помощью ключа службы.</span><span class="sxs-lookup"><span data-stu-id="ddf9c-122">Log in to your Media Services account using your service key.</span></span>

    <span data-ttu-id="ddf9c-123">Чтобы получить имя учетной записи и сведения о ключе, перейдите на [портал Azure](https://portal.azure.com/) и выберите свою учетную запись AMS.</span><span class="sxs-lookup"><span data-stu-id="ddf9c-123">To obtain the account name and key information, go to the [Azure portal](https://portal.azure.com/) and select your AMS account.</span></span> <span data-ttu-id="ddf9c-124">Последовательно выберите "Параметры" > "Ключи".</span><span class="sxs-lookup"><span data-stu-id="ddf9c-124">Then, select Settings > Keys.</span></span> <span data-ttu-id="ddf9c-125">В окне "Управление ключами" отображается имя учетной записи, а также первичный и вторичный ключи.</span><span class="sxs-lookup"><span data-stu-id="ddf9c-125">The Manage keys windows shows the account name and the primary and secondary keys is displayed.</span></span> <span data-ttu-id="ddf9c-126">Скопируйте значения имени учетной записи и первичного ключа.</span><span class="sxs-lookup"><span data-stu-id="ddf9c-126">Copy values of the account name and the primary key.</span></span>

![Скрытие лиц](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough001.png)

### <a name="first-pass--analyze-mode"></a><span data-ttu-id="ddf9c-128">Первый цикл — режим анализа</span><span class="sxs-lookup"><span data-stu-id="ddf9c-128">First pass – analyze mode</span></span>

1. <span data-ttu-id="ddf9c-129">Передайте файл мультимедиа, щелкнув "Ресурс-контейнер" > "Отправить" или перетащив его.</span><span class="sxs-lookup"><span data-stu-id="ddf9c-129">Upload your media file through Asset –> Upload, or via drag and drop.</span></span> 
1. <span data-ttu-id="ddf9c-130">Щелкните правой кнопкой мыши файла мультимедиа и обработайте его, выбрав "Media Analytics" (Медиа-аналитика) > "Azure Media Redactor" > "Analyze mode" (Режим анализа).</span><span class="sxs-lookup"><span data-stu-id="ddf9c-130">Right click and process your media file using Media Analytics –> Azure Media Redactor –> Analyze mode.</span></span> 


![Скрытие лиц](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough002.png)

![Скрытие лиц](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough003.png)

<span data-ttu-id="ddf9c-133">Выходные данные будут содержать JSON-файл аннотаций с данными расположения лиц и JPG-файл каждого обнаруженного лица.</span><span class="sxs-lookup"><span data-stu-id="ddf9c-133">The output will include an annotations json file with face location data, as well as a jpg of each detected face.</span></span> 

![Скрытие лиц](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough004.png)

###<a name="second-pass--redact-mode"></a><span data-ttu-id="ddf9c-135">Второй цикл — режим скрытия</span><span class="sxs-lookup"><span data-stu-id="ddf9c-135">Second pass – redact mode</span></span>

1. <span data-ttu-id="ddf9c-136">Передайте первоначальный ресурс видео в выходные данные из первого цикла и укажите в качестве основного ресурса.</span><span class="sxs-lookup"><span data-stu-id="ddf9c-136">Upload your original video asset to the output from the first pass and set as a primary asset.</span></span> 

    ![Скрытие лиц](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough005.png)

2. <span data-ttu-id="ddf9c-138">(Необязательно.) Передайте файл Dance_idlist.txt, содержащий разделенный символами новой строки список идентификаторов, который нужно скрыть.</span><span class="sxs-lookup"><span data-stu-id="ddf9c-138">(Optional) Upload a 'Dance_idlist.txt' file which includes a newline delimited list of the IDs you wish to redact.</span></span> 

    ![Скрытие лиц](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough006.png)

3. <span data-ttu-id="ddf9c-140">(Необязательно.) Внесите необходимые изменения в файл annotations.json, например, увеличьте ограничивающую рамку.</span><span class="sxs-lookup"><span data-stu-id="ddf9c-140">(Optional) Make any edits to the annotations.json file such as increasing the bounding box boundaries.</span></span> 
4. <span data-ttu-id="ddf9c-141">Щелкните правой кнопкой мыши выходной ресурс из первого цикла, выберите "Redactor" и запустите Azure Media Redactor в режиме **Redact** (Скрытие).</span><span class="sxs-lookup"><span data-stu-id="ddf9c-141">Right click the output asset from the first pass, select the Redactor, and run with the **Redact** mode.</span></span> 

    ![Скрытие лиц](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough007.png)

5. <span data-ttu-id="ddf9c-143">Скачайте окончательный отредактированный выходной ресурс или поделитесь им.</span><span class="sxs-lookup"><span data-stu-id="ddf9c-143">Download or share the final redacted output asset.</span></span> 

    ![Скрытие лиц](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough008.png)

##<a name="azure-media-redactor-visualizer-open-source-tool"></a><span data-ttu-id="ddf9c-145">Инструмент с открытым кодом Azure Media Redactor Visualizer</span><span class="sxs-lookup"><span data-stu-id="ddf9c-145">Azure Media Redactor Visualizer open source tool</span></span>

<span data-ttu-id="ddf9c-146">[Инструмент визуализации](https://github.com/Microsoft/azure-media-redactor-visualizer) с открытым кодом предназначен помочь разработчикам, только приступающим к работе с форматом аннотаций, выполнять анализ и использовать выходные данные.</span><span class="sxs-lookup"><span data-stu-id="ddf9c-146">An open source [visualizer tool](https://github.com/Microsoft/azure-media-redactor-visualizer) is designed to help developers just starting with the annotations format with parsing and using the output.</span></span>

<span data-ttu-id="ddf9c-147">После клонирования репозитория, чтобы запустить проект, необходимо скачать компонент FFMPEG с [официального сайта](https://ffmpeg.org/download.html) его поставщика.</span><span class="sxs-lookup"><span data-stu-id="ddf9c-147">After you clone the repo, in order to run the project, you will need to download FFMPEG from their [official site](https://ffmpeg.org/download.html).</span></span>

<span data-ttu-id="ddf9c-148">Если вы являетесь разработчиком, пытающимся анализировать данные аннотаций в формате JSON, то вы можете ознакомиться с примерами кода в Models.MetaData.</span><span class="sxs-lookup"><span data-stu-id="ddf9c-148">If you are a developer trying to parse the JSON annotation data, look inside Models.MetaData for sample code examples.</span></span>

### <a name="set-up-the-tool"></a><span data-ttu-id="ddf9c-149">Настройка инструмента</span><span class="sxs-lookup"><span data-stu-id="ddf9c-149">Set up the tool</span></span>

1.  <span data-ttu-id="ddf9c-150">Скачайте полное решение и выполните его сборку.</span><span class="sxs-lookup"><span data-stu-id="ddf9c-150">Download and build the entire solution.</span></span> 

    ![Скрытие лиц](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough009.png)

2.  <span data-ttu-id="ddf9c-152">Скачайте компонент FFMPEG [отсюда](https://ffmpeg.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="ddf9c-152">Download FFMPEG from [here](https://ffmpeg.org/download.html).</span></span> <span data-ttu-id="ddf9c-153">Данный проект первоначально был разработан с использованием версии be1d324 (2016-10-04) со статическим связыванием.</span><span class="sxs-lookup"><span data-stu-id="ddf9c-153">This project was originally developed with version be1d324 (2016-10-04) with static linking.</span></span> 
3.  <span data-ttu-id="ddf9c-154">Скопируйте файлы ffmpeg.exe и ffprobe.exe в ту же папку выходных данных, что и AzureMediaRedactor.exe.</span><span class="sxs-lookup"><span data-stu-id="ddf9c-154">Copy ffmpeg.exe and ffprobe.exe to the same output folder as AzureMediaRedactor.exe.</span></span> 

    ![Скрытие лиц](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough010.png)

4. <span data-ttu-id="ddf9c-156">Запустите AzureMediaRedactor.exe.</span><span class="sxs-lookup"><span data-stu-id="ddf9c-156">Run AzureMediaRedactor.exe.</span></span> 

### <a name="use-the-tool"></a><span data-ttu-id="ddf9c-157">Использование инструмента</span><span class="sxs-lookup"><span data-stu-id="ddf9c-157">Use the tool</span></span>

1. <span data-ttu-id="ddf9c-158">Обработайте видео в учетной записи служб мультимедиа Azure с помощью Redactor MP в режиме анализа.</span><span class="sxs-lookup"><span data-stu-id="ddf9c-158">Process your video in your Azure Media Services account with the Redactor MP on Analyze mode.</span></span> 
2. <span data-ttu-id="ddf9c-159">Скачайте первоначальный видеофайл и выходные данные задания Redaction - Analyze.</span><span class="sxs-lookup"><span data-stu-id="ddf9c-159">Download both the original video file and the output of the Redaction - Analyze job.</span></span> 
3. <span data-ttu-id="ddf9c-160">Запустите приложение визуализатора и выберите указанные выше файлы.</span><span class="sxs-lookup"><span data-stu-id="ddf9c-160">Run the visualizer application and choose the files above.</span></span> 

    ![Скрытие лиц](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough011.png)

4. <span data-ttu-id="ddf9c-162">Воспользуйтесь предварительным просмотром файла.</span><span class="sxs-lookup"><span data-stu-id="ddf9c-162">Preview your file.</span></span> <span data-ttu-id="ddf9c-163">Выберите лица, которые следует размыть, с помощью боковой панели справа.</span><span class="sxs-lookup"><span data-stu-id="ddf9c-163">Select which faces you'd like to blur via the sidebar on the right.</span></span> 
    
    ![Скрытие лиц](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough012.png)

5.  <span data-ttu-id="ddf9c-165">В текстовом поле внизу появятся идентификаторы лиц.</span><span class="sxs-lookup"><span data-stu-id="ddf9c-165">The bottom text field will update with the face IDs.</span></span> <span data-ttu-id="ddf9c-166">Создайте файл idlist.txt, содержащий эти идентификаторы в виде списка, разделенного символами новой строки.</span><span class="sxs-lookup"><span data-stu-id="ddf9c-166">Create a file called "idlist.txt" with these IDs as a newline delimited list.</span></span> 

    >[!NOTE]
    > <span data-ttu-id="ddf9c-167">Файл idlist.txt необходимо сохранить в формате ANSI.</span><span class="sxs-lookup"><span data-stu-id="ddf9c-167">The idlist.txt should be saved in ANSI.</span></span> <span data-ttu-id="ddf9c-168">Для сохранения в формате ANSI можно использовать Блокнот.</span><span class="sxs-lookup"><span data-stu-id="ddf9c-168">You can use notepad to save in ANSI.</span></span>
    
6.  <span data-ttu-id="ddf9c-169">Передайте этот файл в выходной ресурс из шага 1.</span><span class="sxs-lookup"><span data-stu-id="ddf9c-169">Upload this file to the output asset from step 1.</span></span> <span data-ttu-id="ddf9c-170">Передайте первоначальное видео в этот ресурс и укажите его в качестве основного ресурса.</span><span class="sxs-lookup"><span data-stu-id="ddf9c-170">Upload the original video to this asset as well and set as primary asset.</span></span> 
7.  <span data-ttu-id="ddf9c-171">Выполните задание Redaction для этого ресурса в режиме "Redact" (Скрытие), чтобы получить окончательное отредактированное видео.</span><span class="sxs-lookup"><span data-stu-id="ddf9c-171">Run Redaction job on this asset with "Redact" mode to get the final redacted video.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ddf9c-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ddf9c-172">Next steps</span></span> 

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ddf9c-173">Отзывы</span><span class="sxs-lookup"><span data-stu-id="ddf9c-173">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="ddf9c-174">Связанные ссылки</span><span class="sxs-lookup"><span data-stu-id="ddf9c-174">Related links</span></span>
[<span data-ttu-id="ddf9c-175">Общие сведения об аналитике служб мультимедиа Azure</span><span class="sxs-lookup"><span data-stu-id="ddf9c-175">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="ddf9c-176">Демонстрационные материалы для медиааналитики Azure</span><span class="sxs-lookup"><span data-stu-id="ddf9c-176">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

<span data-ttu-id="ddf9c-177">[Announcing Face Redaction for Azure Media Analytics](https://azure.microsoft.com/blog/azure-media-redactor/) (Анонс функции скрытия лиц с помощью медиа-аналитики Azure)</span><span class="sxs-lookup"><span data-stu-id="ddf9c-177">[Announcing Face Redaction for Azure Media Analytics](https://azure.microsoft.com/blog/azure-media-redactor/)</span></span>
