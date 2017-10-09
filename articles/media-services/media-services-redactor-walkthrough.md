---
title: "грани aaaRedact с медиа-аналитика Azure Пошаговое руководство | Документы Microsoft"
description: "В этом разделе показано пошаговые инструкции о том, как toorun полного исправления рабочего процесса с помощью обозревателя служб мультимедиа Azure (AMSE) и Azure Media Redactor визуализатора (средство с открытым исходным кодом)."
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
ms.openlocfilehash: ab28f4052b73fdb74fcd5766235eab35402a0c9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="redact-faces-with-azure-media-analytics-walkthrough"></a><span data-ttu-id="d89fa-103">Пошаговое руководство скрытия лиц с помощью аналитики мультимедиа Azure</span><span class="sxs-lookup"><span data-stu-id="d89fa-103">Redact faces with Azure Media Analytics walkthrough</span></span>

## <a name="overview"></a><span data-ttu-id="d89fa-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="d89fa-104">Overview</span></span>

<span data-ttu-id="d89fa-105">**Azure Media Redactor** — [медиа-аналитика Azure](media-services-analytics-overview.md) обработчик мультимедиа (MP), который предлагает исправления масштабируемой лицевой стороны в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="d89fa-105">**Azure Media Redactor** is an [Azure Media Analytics](media-services-analytics-overview.md) media processor (MP) that offers scalable face redaction in hello cloud.</span></span> <span data-ttu-id="d89fa-106">Исправления лицевой стороны позволяет вам toomodify видео в гранях tooblur порядок выбранных сотрудников.</span><span class="sxs-lookup"><span data-stu-id="d89fa-106">Face redaction enables you toomodify your video in order tooblur faces of selected individuals.</span></span> <span data-ttu-id="d89fa-107">Вы можете toouse hello начертания исправления службы в общих сценариях безопасности и новости мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="d89fa-107">You may want toouse hello face redaction service in public safety and news media scenarios.</span></span> <span data-ttu-id="d89fa-108">Через несколько минут, содержащий несколько начертаний материал может занять tooredact часы вручную, но с этой службы hello начертания процесс исправления потребуется всего несколько простых шагов.</span><span class="sxs-lookup"><span data-stu-id="d89fa-108">A few minutes of footage that contains multiple faces can take hours tooredact manually, but with this service hello face redaction process will require just a few simple steps.</span></span> <span data-ttu-id="d89fa-109">Дополнительные сведения см. в [этом блоге](https://azure.microsoft.com/blog/azure-media-redactor/).</span><span class="sxs-lookup"><span data-stu-id="d89fa-109">For  more information, see [this](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span></span>

<span data-ttu-id="d89fa-110">Дополнительные сведения о **Redactor мультимедиа Azure**, hello в разделе [Обзор исправления лицевой](media-services-face-redaction.md) раздела.</span><span class="sxs-lookup"><span data-stu-id="d89fa-110">For details about  **Azure Media Redactor**, see hello [Face redaction overview](media-services-face-redaction.md) topic.</span></span>

<span data-ttu-id="d89fa-111">В этом разделе показано пошаговые инструкции о том, как toorun полного исправления рабочего процесса с помощью обозревателя служб мультимедиа Azure (AMSE) и Azure Media Redactor визуализатора (средство с открытым исходным кодом).</span><span class="sxs-lookup"><span data-stu-id="d89fa-111">This topic shows step by step instructions on how toorun a full redaction workflow using Azure Media Services Explorer (AMSE) and Azure Media Redactor Visualizer (open source tool).</span></span>

<span data-ttu-id="d89fa-112">Hello **Redactor мультимедиа Azure** MP в настоящее время находится в предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="d89fa-112">hello **Azure Media Redactor** MP is currently in Preview.</span></span> <span data-ttu-id="d89fa-113">Он доступен во всех общедоступных регионах Azure, а также в центрах обработки данных для государственных организаций США и для Китая.</span><span class="sxs-lookup"><span data-stu-id="d89fa-113">It is available in all public Azure regions as well as US Government and China data centers.</span></span> <span data-ttu-id="d89fa-114">В настоящее время эта предварительная версия предоставляется бесплатно.</span><span class="sxs-lookup"><span data-stu-id="d89fa-114">This preview is currently free of charge.</span></span> <span data-ttu-id="d89fa-115">В текущем выпуске hello отсутствует ограничение по 10-минутного обработанные продолжительность видео.</span><span class="sxs-lookup"><span data-stu-id="d89fa-115">In hello current release, there is a 10 minute limit on processed video length.</span></span>

<span data-ttu-id="d89fa-116">Дополнительную информацию см. в [этом](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) блоге.</span><span class="sxs-lookup"><span data-stu-id="d89fa-116">For more information, see [this](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) blog.</span></span>

## <a name="azure-media-services-explorer-workflow"></a><span data-ttu-id="d89fa-117">Рабочий процесс Azure Media Services Explorer</span><span class="sxs-lookup"><span data-stu-id="d89fa-117">Azure Media Services Explorer workflow</span></span>

<span data-ttu-id="d89fa-118">Hello tooget простой способ работы с Redactor — средство AMSE toouse hello открытым исходным кодом на сайте github.</span><span class="sxs-lookup"><span data-stu-id="d89fa-118">hello easiest way tooget started with Redactor is toouse hello open source AMSE tool on github.</span></span> <span data-ttu-id="d89fa-119">Можно запустить упрощенный рабочего процесса через **вместе** режим, если не требуется доступ к toohello заметки json или hello начертания изображений jpg.</span><span class="sxs-lookup"><span data-stu-id="d89fa-119">You can run a simplified workflow via **combined** mode if you don’t need access toohello annotation json or hello face jpg images.</span></span>

### <a name="download-and-setup"></a><span data-ttu-id="d89fa-120">Скачивание и установка</span><span class="sxs-lookup"><span data-stu-id="d89fa-120">Download and setup</span></span>

1. <span data-ttu-id="d89fa-121">Загрузите средство AMSE hello из [здесь](https://github.com/Azure/Azure-Media-Services-Explorer).</span><span class="sxs-lookup"><span data-stu-id="d89fa-121">Download hello AMSE tool from [here](https://github.com/Azure/Azure-Media-Services-Explorer).</span></span>
1. <span data-ttu-id="d89fa-122">Войдите в tooyour учетная запись служб мультимедиа с помощью ключа службы.</span><span class="sxs-lookup"><span data-stu-id="d89fa-122">Log in tooyour Media Services account using your service key.</span></span>

    <span data-ttu-id="d89fa-123">Здравствуйте tooobtain имя учетной записи и сведения о ключе, последовательно выберите toohello [портал Azure](https://portal.azure.com/) и выберите свою учетную запись AMS.</span><span class="sxs-lookup"><span data-stu-id="d89fa-123">tooobtain hello account name and key information, go toohello [Azure portal](https://portal.azure.com/) and select your AMS account.</span></span> <span data-ttu-id="d89fa-124">Последовательно выберите "Параметры" > "Ключи".</span><span class="sxs-lookup"><span data-stu-id="d89fa-124">Then, select Settings > Keys.</span></span> <span data-ttu-id="d89fa-125">ключи windows Hello управление показывает имя учетной записи hello и отображается hello первичного и вторичного ключей.</span><span class="sxs-lookup"><span data-stu-id="d89fa-125">hello Manage keys windows shows hello account name and hello primary and secondary keys is displayed.</span></span> <span data-ttu-id="d89fa-126">Скопируйте значения hello имя учетной записи и первичный ключ hello.</span><span class="sxs-lookup"><span data-stu-id="d89fa-126">Copy values of hello account name and hello primary key.</span></span>

![Скрытие лиц](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough001.png)

### <a name="first-pass--analyze-mode"></a><span data-ttu-id="d89fa-128">Первый цикл — режим анализа</span><span class="sxs-lookup"><span data-stu-id="d89fa-128">First pass – analyze mode</span></span>

1. <span data-ttu-id="d89fa-129">Передайте файл мультимедиа, щелкнув "Ресурс-контейнер" > "Отправить" или перетащив его.</span><span class="sxs-lookup"><span data-stu-id="d89fa-129">Upload your media file through Asset –> Upload, or via drag and drop.</span></span> 
1. <span data-ttu-id="d89fa-130">Щелкните правой кнопкой мыши файла мультимедиа и обработайте его, выбрав "Media Analytics" (Медиа-аналитика) > "Azure Media Redactor" > "Analyze mode" (Режим анализа).</span><span class="sxs-lookup"><span data-stu-id="d89fa-130">Right click and process your media file using Media Analytics –> Azure Media Redactor –> Analyze mode.</span></span> 


![Скрытие лиц](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough002.png)

![Скрытие лиц](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough003.png)

<span data-ttu-id="d89fa-133">Hello результат будет включать файл json заметки с данными расположение лицевой стороны, а также jpg каждого обнаруженного гарнитур.</span><span class="sxs-lookup"><span data-stu-id="d89fa-133">hello output will include an annotations json file with face location data, as well as a jpg of each detected face.</span></span> 

![Скрытие лиц](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough004.png)

###<a name="second-pass--redact-mode"></a><span data-ttu-id="d89fa-135">Второй цикл — режим скрытия</span><span class="sxs-lookup"><span data-stu-id="d89fa-135">Second pass – redact mode</span></span>

1. <span data-ttu-id="d89fa-136">Отправка исходного toohello видео активов выходные данные из первого этапа hello и задайте в качестве основного средства.</span><span class="sxs-lookup"><span data-stu-id="d89fa-136">Upload your original video asset toohello output from hello first pass and set as a primary asset.</span></span> 

    ![Скрытие лиц](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough005.png)

2. <span data-ttu-id="d89fa-138">(Необязательно) Отправьте файл «Dance_idlist.txt», который включает список hello идентификаторы, которые вы хотите tooredact перехода на новую строку с разделителями.</span><span class="sxs-lookup"><span data-stu-id="d89fa-138">(Optional) Upload a 'Dance_idlist.txt' file which includes a newline delimited list of hello IDs you wish tooredact.</span></span> 

    ![Скрытие лиц](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough006.png)

3. <span data-ttu-id="d89fa-140">(Необязательно) Сделайте любые изменения toohello annotations.json файл как увеличение hello ограничивающего границы рамки.</span><span class="sxs-lookup"><span data-stu-id="d89fa-140">(Optional) Make any edits toohello annotations.json file such as increasing hello bounding box boundaries.</span></span> 
4. <span data-ttu-id="d89fa-141">Щелкните правой кнопкой мыши hello выходной ресурс из первого этапа hello hello Redactor и запускать с hello **Redact** режим.</span><span class="sxs-lookup"><span data-stu-id="d89fa-141">Right click hello output asset from hello first pass, select hello Redactor, and run with hello **Redact** mode.</span></span> 

    ![Скрытие лиц](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough007.png)

5. <span data-ttu-id="d89fa-143">Загрузите или совместно использовать hello окончательный размер выходного актива.</span><span class="sxs-lookup"><span data-stu-id="d89fa-143">Download or share hello final redacted output asset.</span></span> 

    ![Скрытие лиц](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough008.png)

##<a name="azure-media-redactor-visualizer-open-source-tool"></a><span data-ttu-id="d89fa-145">Инструмент с открытым кодом Azure Media Redactor Visualizer</span><span class="sxs-lookup"><span data-stu-id="d89fa-145">Azure Media Redactor Visualizer open source tool</span></span>

<span data-ttu-id="d89fa-146">Открытой [средство визуализатор](https://github.com/Microsoft/azure-media-redactor-visualizer) — разработчики спроектированный toohelp только начиная с hello формат заметки с синтаксический анализ и применение предложения output hello.</span><span class="sxs-lookup"><span data-stu-id="d89fa-146">An open source [visualizer tool](https://github.com/Microsoft/azure-media-redactor-visualizer) is designed toohelp developers just starting with hello annotations format with parsing and using hello output.</span></span>

<span data-ttu-id="d89fa-147">После клонирования репозитория hello, в порядке toorun hello проекта, необходимо будет toodownload FFMPEG из их [официальный сайт](https://ffmpeg.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="d89fa-147">After you clone hello repo, in order toorun hello project, you will need toodownload FFMPEG from their [official site](https://ffmpeg.org/download.html).</span></span>

<span data-ttu-id="d89fa-148">Если вы являетесь разработчиком попытки hello tooparse заметки данных JSON, поиск внутри Models.MetaData примеры кода для образца.</span><span class="sxs-lookup"><span data-stu-id="d89fa-148">If you are a developer trying tooparse hello JSON annotation data, look inside Models.MetaData for sample code examples.</span></span>

### <a name="set-up-hello-tool"></a><span data-ttu-id="d89fa-149">Настройка средства hello</span><span class="sxs-lookup"><span data-stu-id="d89fa-149">Set up hello tool</span></span>

1.  <span data-ttu-id="d89fa-150">Загрузить и построить все решение hello.</span><span class="sxs-lookup"><span data-stu-id="d89fa-150">Download and build hello entire solution.</span></span> 

    ![Скрытие лиц](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough009.png)

2.  <span data-ttu-id="d89fa-152">Скачайте компонент FFMPEG [отсюда](https://ffmpeg.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="d89fa-152">Download FFMPEG from [here](https://ffmpeg.org/download.html).</span></span> <span data-ttu-id="d89fa-153">Данный проект первоначально был разработан с использованием версии be1d324 (2016-10-04) со статическим связыванием.</span><span class="sxs-lookup"><span data-stu-id="d89fa-153">This project was originally developed with version be1d324 (2016-10-04) with static linking.</span></span> 
3.  <span data-ttu-id="d89fa-154">Скопируйте ffmpeg.exe и ffprobe.exe toohello AzureMediaRedactor.exe папке выходных данных.</span><span class="sxs-lookup"><span data-stu-id="d89fa-154">Copy ffmpeg.exe and ffprobe.exe toohello same output folder as AzureMediaRedactor.exe.</span></span> 

    ![Скрытие лиц](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough010.png)

4. <span data-ttu-id="d89fa-156">Запустите AzureMediaRedactor.exe.</span><span class="sxs-lookup"><span data-stu-id="d89fa-156">Run AzureMediaRedactor.exe.</span></span> 

### <a name="use-hello-tool"></a><span data-ttu-id="d89fa-157">Используйте средство hello</span><span class="sxs-lookup"><span data-stu-id="d89fa-157">Use hello tool</span></span>

1. <span data-ttu-id="d89fa-158">Обрабатывать видео в учетную запись служб мультимедиа Azure с hello Redactor MP режим анализа.</span><span class="sxs-lookup"><span data-stu-id="d89fa-158">Process your video in your Azure Media Services account with hello Redactor MP on Analyze mode.</span></span> 
2. <span data-ttu-id="d89fa-159">Загрузка исходного файла видео hello и выходные данные hello hello исправления - анализ задания.</span><span class="sxs-lookup"><span data-stu-id="d89fa-159">Download both hello original video file and hello output of hello Redaction - Analyze job.</span></span> 
3. <span data-ttu-id="d89fa-160">Выберите файлы hello выше и приложение hello визуализатора.</span><span class="sxs-lookup"><span data-stu-id="d89fa-160">Run hello visualizer application and choose hello files above.</span></span> 

    ![Скрытие лиц](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough011.png)

4. <span data-ttu-id="d89fa-162">Воспользуйтесь предварительным просмотром файла.</span><span class="sxs-lookup"><span data-stu-id="d89fa-162">Preview your file.</span></span> <span data-ttu-id="d89fa-163">Укажите, какие стороной хотел tooblur через hello боковой панели на hello вправо.</span><span class="sxs-lookup"><span data-stu-id="d89fa-163">Select which faces you'd like tooblur via hello sidebar on hello right.</span></span> 
    
    ![Скрытие лиц](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough012.png)

5.  <span data-ttu-id="d89fa-165">hello начертания идентификаторы будут обновлены Hello нижней текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="d89fa-165">hello bottom text field will update with hello face IDs.</span></span> <span data-ttu-id="d89fa-166">Создайте файл idlist.txt, содержащий эти идентификаторы в виде списка, разделенного символами новой строки.</span><span class="sxs-lookup"><span data-stu-id="d89fa-166">Create a file called "idlist.txt" with these IDs as a newline delimited list.</span></span> 

    >[!NOTE]
    > <span data-ttu-id="d89fa-167">Hello idlist.txt должен быть сохранен в формате ANSI.</span><span class="sxs-lookup"><span data-stu-id="d89fa-167">hello idlist.txt should be saved in ANSI.</span></span> <span data-ttu-id="d89fa-168">Можно использовать Блокнот toosave в ANSI.</span><span class="sxs-lookup"><span data-stu-id="d89fa-168">You can use notepad toosave in ANSI.</span></span>
    
6.  <span data-ttu-id="d89fa-169">Отправьте этот файл toohello выходной актив из шага 1.</span><span class="sxs-lookup"><span data-stu-id="d89fa-169">Upload this file toohello output asset from step 1.</span></span> <span data-ttu-id="d89fa-170">Hello исходного видео toothis средства также загрузить и установить в качестве основного средства.</span><span class="sxs-lookup"><span data-stu-id="d89fa-170">Upload hello original video toothis asset as well and set as primary asset.</span></span> 
7.  <span data-ttu-id="d89fa-171">Запустите задание исправления этого актива с «Redact» tooget hello окончательный размер видео в режиме.</span><span class="sxs-lookup"><span data-stu-id="d89fa-171">Run Redaction job on this asset with "Redact" mode tooget hello final redacted video.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d89fa-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d89fa-172">Next steps</span></span> 

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d89fa-173">Отзывы</span><span class="sxs-lookup"><span data-stu-id="d89fa-173">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="d89fa-174">Связанные ссылки</span><span class="sxs-lookup"><span data-stu-id="d89fa-174">Related links</span></span>
[<span data-ttu-id="d89fa-175">Общие сведения об аналитике служб мультимедиа Azure</span><span class="sxs-lookup"><span data-stu-id="d89fa-175">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="d89fa-176">Демонстрационные материалы для медиааналитики Azure</span><span class="sxs-lookup"><span data-stu-id="d89fa-176">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

<span data-ttu-id="d89fa-177">[Announcing Face Redaction for Azure Media Analytics](https://azure.microsoft.com/blog/azure-media-redactor/) (Анонс функции скрытия лиц с помощью медиа-аналитики Azure)</span><span class="sxs-lookup"><span data-stu-id="d89fa-177">[Announcing Face Redaction for Azure Media Analytics](https://azure.microsoft.com/blog/azure-media-redactor/)</span></span>
