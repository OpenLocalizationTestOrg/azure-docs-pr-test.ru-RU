---
title: "MPEG-DASH адаптивной потоковой передачи видео в приложение HTML5 с помощью DASH.js aaaEmbedding | Документы Microsoft"
description: "В этом разделе показано, как tooembed видео MPEG-DASH адаптивной потоковой передачи в приложение HTML5 с помощью DASH.js."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 5aa0e7b6-f5c3-4cc1-aa33-ed16ea4780c2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: a73713d20f95262654532b94576ae9669d829354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="embedding-a-mpeg-dash-adaptive-streaming-video-in-an-html5-application-with-dashjs"></a><span data-ttu-id="c6add-103">Встраивание адаптивного потокового видео MPEG-DASH в приложение HTML5 с помощью DASH.js</span><span class="sxs-lookup"><span data-stu-id="c6add-103">Embedding a MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span></span>
## <a name="overview"></a><span data-ttu-id="c6add-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="c6add-104">Overview</span></span>
<span data-ttu-id="c6add-105">MPEG-DASH — это стандарт ISO для адаптивной потоковой передачи видео содержимого, что обеспечивает значительные преимущества для тех, кто обратиться toodeliver высокого качества, адаптивной потоковой передачи видео вывода hello.</span><span class="sxs-lookup"><span data-stu-id="c6add-105">MPEG-DASH is an ISO standard for hello adaptive streaming of video content, which offers significant benefits for those who wish toodeliver high-quality, adaptive video streaming output.</span></span> <span data-ttu-id="c6add-106">С MPEG-DASH hello видеопотока автоматического удаления определения нижней tooa, при перегрузке сети hello.</span><span class="sxs-lookup"><span data-stu-id="c6add-106">With MPEG-DASH, hello video stream will automatically drop tooa lower definition when hello network becomes congested.</span></span> <span data-ttu-id="c6add-107">Это снижает вероятность hello hello просмотра отображается «приостановлена» видео, пока игрок hello загрузит hello рядом несколько tooplay секунд (также называемого буферизации).</span><span class="sxs-lookup"><span data-stu-id="c6add-107">This reduces hello likelihood of hello viewer seeing a "paused" video while hello player downloads hello next few seconds tooplay (aka buffering).</span></span> <span data-ttu-id="c6add-108">Уменьшает перегрузки сети, видеопроигрыватель hello в свою очередь вернет tooa выше качество потока.</span><span class="sxs-lookup"><span data-stu-id="c6add-108">As network congestion reduces, hello video player will in turn return tooa higher quality stream.</span></span> <span data-ttu-id="c6add-109">Это возможность tooadapt hello пропускной способности, необходимой также приведет к более быстрое время начала для видео.</span><span class="sxs-lookup"><span data-stu-id="c6add-109">This ability tooadapt hello bandwidth required also results in a faster start time for video.</span></span> <span data-ttu-id="c6add-110">Что означает, что hello первые несколько секунд может воспроизводиться в сегменте ниже качество fast для загрузки, а затем сделать шаг вверх tooa более высокого качества после содержимое передано в буфер.</span><span class="sxs-lookup"><span data-stu-id="c6add-110">That means that hello first few seconds can be played in a fast-to-download lower quality segment and then step up tooa higher quality once sufficient content has been buffered.</span></span>

<span data-ttu-id="c6add-111">Dash.js — это проигрыватель видео MPEG-DASH с открытым кодом, написанный на языке JavaScript.</span><span class="sxs-lookup"><span data-stu-id="c6add-111">Dash.js is an open source MPEG-DASH video player written in JavaScript.</span></span> <span data-ttu-id="c6add-112">Его задача — tooprovide надежными, кросс платформенных проигрыватель, который можно свободно использовать в приложениях, требующих воспроизведения видео.</span><span class="sxs-lookup"><span data-stu-id="c6add-112">Its goal is tooprovide a robust, cross-platform player that can be freely reused in applications that require video playback.</span></span> <span data-ttu-id="c6add-113">Он обеспечивает воспроизведение MPEG-DASH в любом браузере, который поддерживает hello W3C Media Source Extensions (MSE), т.е. сегодня Chrome, Microsoft Edge и IE11 (других браузеров было заявлено их намерения toosupport MSE).</span><span class="sxs-lookup"><span data-stu-id="c6add-113">It provides MPEG-DASH playback in any browser that supports hello W3C Media Source Extensions (MSE), today that is Chrome, Microsoft Edge and IE11 (other browsers have indicated their intent toosupport MSE).</span></span> <span data-ttu-id="c6add-114">Дополнительные сведения о DASH.js js разделе репозиторий dash.js GitHub hello.</span><span class="sxs-lookup"><span data-stu-id="c6add-114">For more information about DASH.js, js see hello GitHub dash.js repository.</span></span>

## <a name="creating-a-browser-based-streaming-video-player"></a><span data-ttu-id="c6add-115">Создание браузерного потокового видеопроигрывателя</span><span class="sxs-lookup"><span data-stu-id="c6add-115">Creating a browser-based streaming video player</span></span>
<span data-ttu-id="c6add-116">toocreate простой веб-страницы, отображающий видеопроигрывателя с hello ожидается управляет такой воспроизведение, пауза, перемотки и т.д., вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="c6add-116">toocreate a simple web page that displays a video player with hello expected controls such a play, pause, rewind etc., you will need to:</span></span>

1. <span data-ttu-id="c6add-117">Создайте страницу HTML.</span><span class="sxs-lookup"><span data-stu-id="c6add-117">Create an HTML page</span></span>
2. <span data-ttu-id="c6add-118">Добавление тега видео hello</span><span class="sxs-lookup"><span data-stu-id="c6add-118">Add hello video tag</span></span>
3. <span data-ttu-id="c6add-119">Добавить hello dash.js проигрывателя</span><span class="sxs-lookup"><span data-stu-id="c6add-119">Add hello dash.js player</span></span>
4. <span data-ttu-id="c6add-120">Инициализировать проигрывателя hello</span><span class="sxs-lookup"><span data-stu-id="c6add-120">Initialize hello player</span></span>
5. <span data-ttu-id="c6add-121">Добавьте нужный стиль CSS.</span><span class="sxs-lookup"><span data-stu-id="c6add-121">Add some CSS style</span></span>
6. <span data-ttu-id="c6add-122">Просмотр результатов hello в браузере, который реализует MSE</span><span class="sxs-lookup"><span data-stu-id="c6add-122">View hello results in a browser that implements MSE</span></span>

<span data-ttu-id="c6add-123">Инициализация hello проигрывателя могут выполняться только небольшое число строк кода JavaScript.</span><span class="sxs-lookup"><span data-stu-id="c6add-123">Initializing hello player can be completed in just a handful of lines of JavaScript code.</span></span> <span data-ttu-id="c6add-124">С помощью dash.js, это простой tooembed MPEG-DASH видео в приложениях на основе браузера.</span><span class="sxs-lookup"><span data-stu-id="c6add-124">Using dash.js, it really is that simple tooembed MPEG-DASH video in your browser based applications.</span></span>

## <a name="creating-hello-html-page"></a><span data-ttu-id="c6add-125">Создание HTML-страница приветствия</span><span class="sxs-lookup"><span data-stu-id="c6add-125">Creating hello HTML Page</span></span>
<span data-ttu-id="c6add-126">Hello первым шагом является toocreate стандартный код HTML-страницу, содержащую hello **видео** элемент, сохраните этот файл как basicPlayer.html как hello следующий пример иллюстрирует:</span><span class="sxs-lookup"><span data-stu-id="c6add-126">hello first step is toocreate a standard HTML page containing hello **video** element, save this file as basicPlayer.html, as hello following example illustrates:</span></span>

    <!DOCTYPE html>
    <html>
      <head><title>Adaptive Streaming in HTML5</title></head>
      <body>
        <h1>Adaptive Streaming with HTML5</h1>
        <video id="videoplayer" controls></video>
      </body>
    </html>

## <a name="adding-hello-dashjs-player"></a><span data-ttu-id="c6add-127">Добавление hello DASH.js проигрывателя</span><span class="sxs-lookup"><span data-stu-id="c6add-127">Adding hello DASH.js Player</span></span>
<span data-ttu-id="c6add-128">tooadd hello dash.js реализацию toohello заявлению, вам потребуется файл dash.all.js toograb hello из версии hello 1.0 dash.js проекта.</span><span class="sxs-lookup"><span data-stu-id="c6add-128">tooadd hello dash.js reference implementation toohello application, you’ll need toograb hello dash.all.js file from hello 1.0 release of dash.js project.</span></span> <span data-ttu-id="c6add-129">Это должен быть сохранен в папке приложения hello JavaScript.</span><span class="sxs-lookup"><span data-stu-id="c6add-129">This should be saved in hello JavaScript folder of your application.</span></span> <span data-ttu-id="c6add-130">Этот файл является файлом удобства, которая запрашивает весь код необходимые dash.js hello в один файл.</span><span class="sxs-lookup"><span data-stu-id="c6add-130">This file is a convenience file that pulls together all hello necessary dash.js code into a single file.</span></span> <span data-ttu-id="c6add-131">Если выглядел примерно репозиторий dash.js hello, необходимо найти hello отдельные файлы, проверки кода и многое другое но, если все toodo dash.js использования, то файл dash.all.js hello вам нужен.</span><span class="sxs-lookup"><span data-stu-id="c6add-131">If you have a look around hello dash.js repository, you will find hello individual files, test code and much more, but if all you want toodo is use dash.js, then hello dash.all.js file is what you need.</span></span>

<span data-ttu-id="c6add-132">tooadd hello dash.js tooyour видеопроигрывателей, добавить скрипт тег toohello раздел head basicPlayer.html:</span><span class="sxs-lookup"><span data-stu-id="c6add-132">tooadd hello dash.js player tooyour applications, add a script tag toohello head section of basicPlayer.html:</span></span>

    <!-- DASH-AVC/265 reference implementation -->
    < script src="js/dash.all.js"></script>


<span data-ttu-id="c6add-133">Создайте проигрыватель hello tooinitialize функции при загрузке страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="c6add-133">Next, create a function tooinitialize hello player when hello page loads.</span></span> <span data-ttu-id="c6add-134">Добавьте следующий сценарий после строки hello, в котором загружаются dash.all.js hello:</span><span class="sxs-lookup"><span data-stu-id="c6add-134">Add hello following script after hello line in which you load dash.all.js:</span></span>

    <script>
    // setup hello video element and attach it toohello Dash player
    function setupVideo() {
      var url = "http://wams.edgesuite.net/media/MPTExpressionData02/BigBuckBunny_1080p24_IYUV_2ch.ism/manifest(format=mpd-time-csf)";
      var context = new Dash.di.DashContext();
      var player = new MediaPlayer(context);
                      player.startup();
                      player.attachView(document.querySelector("#videoplayer"));
                      player.attachSource(url);
    }
    </script>

<span data-ttu-id="c6add-135">Эта функция сначала создает DashContext.</span><span class="sxs-lookup"><span data-stu-id="c6add-135">This function first creates a DashContext.</span></span> <span data-ttu-id="c6add-136">Это приложение hello используется tooconfigure для среды выполнения требуемой среды.</span><span class="sxs-lookup"><span data-stu-id="c6add-136">This is used tooconfigure hello application for a specific runtime environment.</span></span> <span data-ttu-id="c6add-137">С технической точки зрения он определяет классы, которые hello framework внедрения зависимостей следует использовать при создании приложения hello приветствия.</span><span class="sxs-lookup"><span data-stu-id="c6add-137">From a technical point of view, it defines hello classes that hello dependency injection framework should use when constructing hello application.</span></span> <span data-ttu-id="c6add-138">В большинстве случаев будет использоваться Dash.di.DashContext.</span><span class="sxs-lookup"><span data-stu-id="c6add-138">In most cases, you will use Dash.di.DashContext.</span></span>

<span data-ttu-id="c6add-139">Далее создайте экземпляр hello основной класс Framework dash.js hello, MediaPlayer.</span><span class="sxs-lookup"><span data-stu-id="c6add-139">Next, instantiate hello primary class of hello dash.js framework, MediaPlayer.</span></span> <span data-ttu-id="c6add-140">Этот класс содержит ядро hello методы, такие как необходимые воспроизведения и приостановки, управляет hello связь с помощью элемента видео hello и также управляет hello интерпретацию hello презентации описание носителя (MPD) файл, который описывает видео toobe hello воспроизводиться.</span><span class="sxs-lookup"><span data-stu-id="c6add-140">This class contains hello core methods needed such as play and pause, manages hello relationship with hello video element and also manages hello interpretation of hello Media Presentation Description (MPD) file which describes hello video toobe played.</span></span>

<span data-ttu-id="c6add-141">функция startup() Hello hello MediaPlayer класс называется tooensure игрок hello — Готово tooplay видео.</span><span class="sxs-lookup"><span data-stu-id="c6add-141">hello startup() function of hello MediaPlayer class is called tooensure that hello player is ready tooplay video.</span></span> <span data-ttu-id="c6add-142">Среди прочего эта функция гарантирует, что все необходимые классы hello (как определено контекстом hello) были загружены.</span><span class="sxs-lookup"><span data-stu-id="c6add-142">Amongst other things this function ensures that all hello necessary classes (as defined by hello context) have been loaded.</span></span> <span data-ttu-id="c6add-143">После подготовки hello проигрывателя можно присоединить tooit элемент video hello, с помощью функции attachView() hello.</span><span class="sxs-lookup"><span data-stu-id="c6add-143">Once hello player is ready, you can attach hello video element tooit using hello attachView() function.</span></span> <span data-ttu-id="c6add-144">Это позволяет видеопотока hello tooinject MediaPlayer hello в элемент hello, а также управления воспроизведением при необходимости.</span><span class="sxs-lookup"><span data-stu-id="c6add-144">This enables hello MediaPlayer tooinject hello video stream into hello element and also control playback as necessary.</span></span>

<span data-ttu-id="c6add-145">Передать URL-адрес hello hello MPD файл toohello MediaPlayer, чтобы его было известно о hello видео предполагается функция setupVideo() tooplay.hello только что создали потребуется toobe, выполненных после полной загрузки страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="c6add-145">Pass hello URL of hello MPD file toohello MediaPlayer so that it knows about hello video it is expected tooplay.hello setupVideo() function just created will need toobe executed once hello page has fully loaded.</span></span> <span data-ttu-id="c6add-146">Для этого с помощью события onload hello элемента текста hello.</span><span class="sxs-lookup"><span data-stu-id="c6add-146">Do this by using hello onload event of hello body element.</span></span> <span data-ttu-id="c6add-147">Измените элемент <body> на:</span><span class="sxs-lookup"><span data-stu-id="c6add-147">Change your <body> element to:</span></span>

    <body onload="setupVideo()">

<span data-ttu-id="c6add-148">Задайте размер hello hello видео элемента с помощью CSS.</span><span class="sxs-lookup"><span data-stu-id="c6add-148">Finally, set hello size of hello video element using CSS.</span></span> <span data-ttu-id="c6add-149">В среде адаптивной потоковой передачи это особенно важно, так как размер hello hello видео воспроизводится могут изменяться по мере воспроизведения адаптирует toochanging состояния сети.</span><span class="sxs-lookup"><span data-stu-id="c6add-149">In an adaptive streaming environment, this is especially important because hello size of hello video being played may change as playback adapts toochanging network conditions.</span></span> <span data-ttu-id="c6add-150">В этой демонстрации простых просто принудительно toobe элемент video hello 80% доступной браузере hello, добавив следующий раздел head toohello CSS страницы приветствия hello:</span><span class="sxs-lookup"><span data-stu-id="c6add-150">In this simple demo simply force hello video element toobe 80% of hello available browser window by adding hello following CSS toohello head section of hello page:</span></span>

    <style>
    video {
      width: 80%;
      height: 80%;
    }
    </style>

## <a name="playing-a-video"></a><span data-ttu-id="c6add-151">Воспроизведение видео</span><span class="sxs-lookup"><span data-stu-id="c6add-151">Playing a Video</span></span>
<span data-ttu-id="c6add-152">tooplay видео, укажите в браузере в файле basicPlayback.html hello и нажмите кнопку воспроизведения на hello видеопроигрыватель отображается.</span><span class="sxs-lookup"><span data-stu-id="c6add-152">tooplay a video, point your browser at hello basicPlayback.html file and click play on hello video player displayed.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="c6add-153">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="c6add-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c6add-154">Отзывы</span><span class="sxs-lookup"><span data-stu-id="c6add-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="c6add-155">См. также</span><span class="sxs-lookup"><span data-stu-id="c6add-155">See Also</span></span>
[<span data-ttu-id="c6add-156">Разработка приложений видеопроигрывателя</span><span class="sxs-lookup"><span data-stu-id="c6add-156">Develop video player applications</span></span>](media-services-develop-video-players.md)

[<span data-ttu-id="c6add-157">Репозиторий dash.js на GitHub</span><span class="sxs-lookup"><span data-stu-id="c6add-157">GitHub dash.js repository</span></span>](https://github.com/Dash-Industry-Forum/dash.js) 

