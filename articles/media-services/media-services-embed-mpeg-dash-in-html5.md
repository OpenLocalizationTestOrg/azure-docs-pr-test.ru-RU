---
title: "Встраивание адаптивного потокового видео MPEG-DASH в приложение HTML5 с помощью DASH.js | Документация Майкрософт"
description: "В этом разделе демонстрируется встраивание адаптивного потокового видео MPEG-DASH в приложение HTML5 с помощью DASH.js."
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
ms.openlocfilehash: 27ce6325773ba1f9fd9cd9ab9e07ea9f5e2488ac
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="embedding-a-mpeg-dash-adaptive-streaming-video-in-an-html5-application-with-dashjs"></a><span data-ttu-id="78845-103">Встраивание адаптивного потокового видео MPEG-DASH в приложение HTML5 с помощью DASH.js</span><span class="sxs-lookup"><span data-stu-id="78845-103">Embedding a MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span></span>
## <a name="overview"></a><span data-ttu-id="78845-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="78845-104">Overview</span></span>
<span data-ttu-id="78845-105">MPEG-DASH — это стандарт ISO для адаптивной потоковой передачи видеосодержимого, который обеспечивает значительные преимущества для тех, кому требуется высококачественный адаптивный потоковый вывод видео.</span><span class="sxs-lookup"><span data-stu-id="78845-105">MPEG-DASH is an ISO standard for the adaptive streaming of video content, which offers significant benefits for those who wish to deliver high-quality, adaptive video streaming output.</span></span> <span data-ttu-id="78845-106">С MPEG-DASH поток видео будет автоматически сжиматься до более низкой четкости, если сеть перегружена.</span><span class="sxs-lookup"><span data-stu-id="78845-106">With MPEG-DASH, the video stream will automatically drop to a lower definition when the network becomes congested.</span></span> <span data-ttu-id="78845-107">Это снижает вероятность того, что зритель увидит видео "на паузе", в то время как проигрыватель будет загружать следующие несколько секунд для воспроизведения (т. н. буферизация).</span><span class="sxs-lookup"><span data-stu-id="78845-107">This reduces the likelihood of the viewer seeing a "paused" video while the player downloads the next few seconds to play (aka buffering).</span></span> <span data-ttu-id="78845-108">Когда нагрузка на сеть снизится, видеопроигрыватель вернется к потоку более высокого качества.</span><span class="sxs-lookup"><span data-stu-id="78845-108">As network congestion reduces, the video player will in turn return to a higher quality stream.</span></span> <span data-ttu-id="78845-109">Такая возможность адаптировать требуемую пропускную способность также способствует ускорению запуска видео.</span><span class="sxs-lookup"><span data-stu-id="78845-109">This ability to adapt the bandwidth required also results in a faster start time for video.</span></span> <span data-ttu-id="78845-110">Это означает, что первые несколько секунд можно воспроизвести в виде быстро загружаемого сегмента низкого качества, а затем перейти к более высокому качеству, как только достаточный объем содержимого будет загружен в буфер.</span><span class="sxs-lookup"><span data-stu-id="78845-110">That means that the first few seconds can be played in a fast-to-download lower quality segment and then step up to a higher quality once sufficient content has been buffered.</span></span>

<span data-ttu-id="78845-111">Dash.js — это проигрыватель видео MPEG-DASH с открытым кодом, написанный на языке JavaScript.</span><span class="sxs-lookup"><span data-stu-id="78845-111">Dash.js is an open source MPEG-DASH video player written in JavaScript.</span></span> <span data-ttu-id="78845-112">Цель этого проект — предоставить надежный, межплатформенный проигрыватель, который можно свободно встраивать в приложения, требующие воспроизведения видео.</span><span class="sxs-lookup"><span data-stu-id="78845-112">Its goal is to provide a robust, cross-platform player that can be freely reused in applications that require video playback.</span></span> <span data-ttu-id="78845-113">Он обеспечивает воспроизведение MPEG-DASH в любом браузере, поддерживающем расширения источников мультимедиа W3C (Media Source Extensions, MSE). На сегодняшний день это Chrome, Microsoft Edge и IE11 (разработчики других браузеров заявили о намерении добавить поддержку MSE).</span><span class="sxs-lookup"><span data-stu-id="78845-113">It provides MPEG-DASH playback in any browser that supports the W3C Media Source Extensions (MSE), today that is Chrome, Microsoft Edge and IE11 (other browsers have indicated their intent to support MSE).</span></span> <span data-ttu-id="78845-114">Дополнительные сведения о DASH.js см. в репозитории dash.js на GitHub.</span><span class="sxs-lookup"><span data-stu-id="78845-114">For more information about DASH.js, js see the GitHub dash.js repository.</span></span>

## <a name="creating-a-browser-based-streaming-video-player"></a><span data-ttu-id="78845-115">Создание браузерного потокового видеопроигрывателя</span><span class="sxs-lookup"><span data-stu-id="78845-115">Creating a browser-based streaming video player</span></span>
<span data-ttu-id="78845-116">Чтобы создать простую веб-страницу, на которой будет отображаться видеопроигрыватель с привычными элементами управления для воспроизведения, паузы, перемотки и т. д., выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="78845-116">To create a simple web page that displays a video player with the expected controls such a play, pause, rewind etc., you will need to:</span></span>

1. <span data-ttu-id="78845-117">Создайте страницу HTML.</span><span class="sxs-lookup"><span data-stu-id="78845-117">Create an HTML page</span></span>
2. <span data-ttu-id="78845-118">Добавьте тег video.</span><span class="sxs-lookup"><span data-stu-id="78845-118">Add the video tag</span></span>
3. <span data-ttu-id="78845-119">Добавьте проигрыватель dash.js.</span><span class="sxs-lookup"><span data-stu-id="78845-119">Add the dash.js player</span></span>
4. <span data-ttu-id="78845-120">Инициализируйте проигрыватель.</span><span class="sxs-lookup"><span data-stu-id="78845-120">Initialize the player</span></span>
5. <span data-ttu-id="78845-121">Добавьте нужный стиль CSS.</span><span class="sxs-lookup"><span data-stu-id="78845-121">Add some CSS style</span></span>
6. <span data-ttu-id="78845-122">Просмотрите результаты в браузере, который поддерживает расширения MSE.</span><span class="sxs-lookup"><span data-stu-id="78845-122">View the results in a browser that implements MSE</span></span>

<span data-ttu-id="78845-123">Инициализацию проигрывателя можно выполнить всего лишь несколькими строками кода JavaScript.</span><span class="sxs-lookup"><span data-stu-id="78845-123">Initializing the player can be completed in just a handful of lines of JavaScript code.</span></span> <span data-ttu-id="78845-124">С помощью dash.js встраивать видео MPEG-DASH в браузерные приложения действительно просто.</span><span class="sxs-lookup"><span data-stu-id="78845-124">Using dash.js, it really is that simple to embed MPEG-DASH video in your browser based applications.</span></span>

## <a name="creating-the-html-page"></a><span data-ttu-id="78845-125">Создание страницы HTML</span><span class="sxs-lookup"><span data-stu-id="78845-125">Creating the HTML Page</span></span>
<span data-ttu-id="78845-126">Первым шагом является создание стандартной страницы HTML, содержащей элемент **video**, и сохранение ее в виде файла с именем basicPlayer.html, как показано в примере ниже.</span><span class="sxs-lookup"><span data-stu-id="78845-126">The first step is to create a standard HTML page containing the **video** element, save this file as basicPlayer.html, as the following example illustrates:</span></span>

    <!DOCTYPE html>
    <html>
      <head><title>Adaptive Streaming in HTML5</title></head>
      <body>
        <h1>Adaptive Streaming with HTML5</h1>
        <video id="videoplayer" controls></video>
      </body>
    </html>

## <a name="adding-the-dashjs-player"></a><span data-ttu-id="78845-127">Добавление проигрывателя DASH.js</span><span class="sxs-lookup"><span data-stu-id="78845-127">Adding the DASH.js Player</span></span>
<span data-ttu-id="78845-128">Чтобы добавить в приложение эталонную реализацию dash.js, необходимо получить файл dash.all.js из выпуска 1.0 проекта dash.js.</span><span class="sxs-lookup"><span data-stu-id="78845-128">To add the dash.js reference implementation to the application, you’ll need to grab the dash.all.js file from the 1.0 release of dash.js project.</span></span> <span data-ttu-id="78845-129">Его необходимо сохранить в папку JavaScript вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="78845-129">This should be saved in the JavaScript folder of your application.</span></span> <span data-ttu-id="78845-130">Этот файл создан для удобства и извлекает весь необходимый код dash.js в один файл.</span><span class="sxs-lookup"><span data-stu-id="78845-130">This file is a convenience file that pulls together all the necessary dash.js code into a single file.</span></span> <span data-ttu-id="78845-131">Если рассмотреть репозиторий dash.js, вы найдете отдельные файлы, тестовый код и многое другое, но если необходимо только использовать dash.js, то файл dash.all.js — то, что вам потребуется.</span><span class="sxs-lookup"><span data-stu-id="78845-131">If you have a look around the dash.js repository, you will find the individual files, test code and much more, but if all you want to do is use dash.js, then the dash.all.js file is what you need.</span></span>

<span data-ttu-id="78845-132">Чтобы добавить проигрыватель dash.js в приложения, добавьте тег script в раздел head файла basicPlayer.html:</span><span class="sxs-lookup"><span data-stu-id="78845-132">To add the dash.js player to your applications, add a script tag to the head section of basicPlayer.html:</span></span>

    <!-- DASH-AVC/265 reference implementation -->
    < script src="js/dash.all.js"></script>


<span data-ttu-id="78845-133">Затем создайте функцию для инициализации проигрывателя при загрузке страницы.</span><span class="sxs-lookup"><span data-stu-id="78845-133">Next, create a function to initialize the player when the page loads.</span></span> <span data-ttu-id="78845-134">После строки, в которой загружается dash.all.js, добавьте следующий скрипт:</span><span class="sxs-lookup"><span data-stu-id="78845-134">Add the following script after the line in which you load dash.all.js:</span></span>

    <script>
    // setup the video element and attach it to the Dash player
    function setupVideo() {
      var url = "http://wams.edgesuite.net/media/MPTExpressionData02/BigBuckBunny_1080p24_IYUV_2ch.ism/manifest(format=mpd-time-csf)";
      var context = new Dash.di.DashContext();
      var player = new MediaPlayer(context);
                      player.startup();
                      player.attachView(document.querySelector("#videoplayer"));
                      player.attachSource(url);
    }
    </script>

<span data-ttu-id="78845-135">Эта функция сначала создает DashContext.</span><span class="sxs-lookup"><span data-stu-id="78845-135">This function first creates a DashContext.</span></span> <span data-ttu-id="78845-136">Он используется для настройки приложения для конкретной среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="78845-136">This is used to configure the application for a specific runtime environment.</span></span> <span data-ttu-id="78845-137">С технической точки зрения он определяет классы, которые следует использовать платформой внедрения зависимостей при построении приложения.</span><span class="sxs-lookup"><span data-stu-id="78845-137">From a technical point of view, it defines the classes that the dependency injection framework should use when constructing the application.</span></span> <span data-ttu-id="78845-138">В большинстве случаев будет использоваться Dash.di.DashContext.</span><span class="sxs-lookup"><span data-stu-id="78845-138">In most cases, you will use Dash.di.DashContext.</span></span>

<span data-ttu-id="78845-139">Далее создайте экземпляр основного класса платформы dash.js, MediaPlayer.</span><span class="sxs-lookup"><span data-stu-id="78845-139">Next, instantiate the primary class of the dash.js framework, MediaPlayer.</span></span> <span data-ttu-id="78845-140">Этот класс содержит основные необходимые методы, такие как воспроизведение и пауза, управляет связью с элементом video, а также управляет интерпретацией файла описания представления носителя (Media Presentation Description, MPD), который описывает воспроизводимое видео.</span><span class="sxs-lookup"><span data-stu-id="78845-140">This class contains the core methods needed such as play and pause, manages the relationship with the video element and also manages the interpretation of the Media Presentation Description (MPD) file which describes the video to be played.</span></span>

<span data-ttu-id="78845-141">Функция startup() класса MediaPlayer вызывается для обеспечения готовности проигрывателя к воспроизведению видео.</span><span class="sxs-lookup"><span data-stu-id="78845-141">The startup() function of the MediaPlayer class is called to ensure that the player is ready to play video.</span></span> <span data-ttu-id="78845-142">Кроме всего прочего эта функция гарантирует, чтобы все необходимые классы (как определено контекстом) были загружены.</span><span class="sxs-lookup"><span data-stu-id="78845-142">Amongst other things this function ensures that all the necessary classes (as defined by the context) have been loaded.</span></span> <span data-ttu-id="78845-143">Когда проигрыватель готов, можно подключить к нему элемент video с помощью функции attachView().</span><span class="sxs-lookup"><span data-stu-id="78845-143">Once the player is ready, you can attach the video element to it using the attachView() function.</span></span> <span data-ttu-id="78845-144">Это позволяет MediaPlayer внедрить видеопоток в элемент, а также управлять воспроизведением при необходимости.</span><span class="sxs-lookup"><span data-stu-id="78845-144">This enables the MediaPlayer to inject the video stream into the element and also control playback as necessary.</span></span>

<span data-ttu-id="78845-145">Передайте URL-адрес MPD-файла объекту MediaPlayer, чтобы уведомить его о видео, воспроизведение которого ожидается. После полной загрузки страницы необходимо будет выполнить только что созданную функцию setupVideo().</span><span class="sxs-lookup"><span data-stu-id="78845-145">Pass the URL of the MPD file to the MediaPlayer so that it knows about the video it is expected to play.The setupVideo() function just created will need to be executed once the page has fully loaded.</span></span> <span data-ttu-id="78845-146">Сделайте это с помощью события onload в элементе body.</span><span class="sxs-lookup"><span data-stu-id="78845-146">Do this by using the onload event of the body element.</span></span> <span data-ttu-id="78845-147">Измените элемент <body> на:</span><span class="sxs-lookup"><span data-stu-id="78845-147">Change your <body> element to:</span></span>

    <body onload="setupVideo()">

<span data-ttu-id="78845-148">Наконец, задайте размер элемента video с помощью CSS.</span><span class="sxs-lookup"><span data-stu-id="78845-148">Finally, set the size of the video element using CSS.</span></span> <span data-ttu-id="78845-149">В среде адаптивной потоковой передачи это особенно важно, так как размер воспроизводимого видео может меняться по мере адаптации воспроизведения к изменению сетевых условий.</span><span class="sxs-lookup"><span data-stu-id="78845-149">In an adaptive streaming environment, this is especially important because the size of the video being played may change as playback adapts to changing network conditions.</span></span> <span data-ttu-id="78845-150">В этой простой демонстрации можно принудительно задать для элемента video размер 80 % от доступного окна браузера, добавив следующий код CSS в секцию head страницы:</span><span class="sxs-lookup"><span data-stu-id="78845-150">In this simple demo simply force the video element to be 80% of the available browser window by adding the following CSS to the head section of the page:</span></span>

    <style>
    video {
      width: 80%;
      height: 80%;
    }
    </style>

## <a name="playing-a-video"></a><span data-ttu-id="78845-151">Воспроизведение видео</span><span class="sxs-lookup"><span data-stu-id="78845-151">Playing a Video</span></span>
<span data-ttu-id="78845-152">Чтобы воспроизвести видео, откройте в браузере файл basicPlayback.html и нажмите кнопку воспроизведения в видеопроигрывателе, который отобразится.</span><span class="sxs-lookup"><span data-stu-id="78845-152">To play a video, point your browser at the basicPlayback.html file and click play on the video player displayed.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="78845-153">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="78845-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="78845-154">Отзывы</span><span class="sxs-lookup"><span data-stu-id="78845-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="78845-155">См. также</span><span class="sxs-lookup"><span data-stu-id="78845-155">See Also</span></span>
[<span data-ttu-id="78845-156">Разработка приложений видеопроигрывателя</span><span class="sxs-lookup"><span data-stu-id="78845-156">Develop video player applications</span></span>](media-services-develop-video-players.md)

[<span data-ttu-id="78845-157">Репозиторий dash.js на GitHub</span><span class="sxs-lookup"><span data-stu-id="78845-157">GitHub dash.js repository</span></span>](https://github.com/Dash-Industry-Forum/dash.js) 

