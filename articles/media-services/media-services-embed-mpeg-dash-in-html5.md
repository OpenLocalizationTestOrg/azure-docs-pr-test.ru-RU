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
# <a name="embedding-a-mpeg-dash-adaptive-streaming-video-in-an-html5-application-with-dashjs"></a>Встраивание адаптивного потокового видео MPEG-DASH в приложение HTML5 с помощью DASH.js
## <a name="overview"></a>Обзор
MPEG-DASH — это стандарт ISO для адаптивной потоковой передачи видео содержимого, что обеспечивает значительные преимущества для тех, кто обратиться toodeliver высокого качества, адаптивной потоковой передачи видео вывода hello. С MPEG-DASH hello видеопотока автоматического удаления определения нижней tooa, при перегрузке сети hello. Это снижает вероятность hello hello просмотра отображается «приостановлена» видео, пока игрок hello загрузит hello рядом несколько tooplay секунд (также называемого буферизации). Уменьшает перегрузки сети, видеопроигрыватель hello в свою очередь вернет tooa выше качество потока. Это возможность tooadapt hello пропускной способности, необходимой также приведет к более быстрое время начала для видео. Что означает, что hello первые несколько секунд может воспроизводиться в сегменте ниже качество fast для загрузки, а затем сделать шаг вверх tooa более высокого качества после содержимое передано в буфер.

Dash.js — это проигрыватель видео MPEG-DASH с открытым кодом, написанный на языке JavaScript. Его задача — tooprovide надежными, кросс платформенных проигрыватель, который можно свободно использовать в приложениях, требующих воспроизведения видео. Он обеспечивает воспроизведение MPEG-DASH в любом браузере, который поддерживает hello W3C Media Source Extensions (MSE), т.е. сегодня Chrome, Microsoft Edge и IE11 (других браузеров было заявлено их намерения toosupport MSE). Дополнительные сведения о DASH.js js разделе репозиторий dash.js GitHub hello.

## <a name="creating-a-browser-based-streaming-video-player"></a>Создание браузерного потокового видеопроигрывателя
toocreate простой веб-страницы, отображающий видеопроигрывателя с hello ожидается управляет такой воспроизведение, пауза, перемотки и т.д., вам потребуется:

1. Создайте страницу HTML.
2. Добавление тега видео hello
3. Добавить hello dash.js проигрывателя
4. Инициализировать проигрывателя hello
5. Добавьте нужный стиль CSS.
6. Просмотр результатов hello в браузере, который реализует MSE

Инициализация hello проигрывателя могут выполняться только небольшое число строк кода JavaScript. С помощью dash.js, это простой tooembed MPEG-DASH видео в приложениях на основе браузера.

## <a name="creating-hello-html-page"></a>Создание HTML-страница приветствия
Hello первым шагом является toocreate стандартный код HTML-страницу, содержащую hello **видео** элемент, сохраните этот файл как basicPlayer.html как hello следующий пример иллюстрирует:

    <!DOCTYPE html>
    <html>
      <head><title>Adaptive Streaming in HTML5</title></head>
      <body>
        <h1>Adaptive Streaming with HTML5</h1>
        <video id="videoplayer" controls></video>
      </body>
    </html>

## <a name="adding-hello-dashjs-player"></a>Добавление hello DASH.js проигрывателя
tooadd hello dash.js реализацию toohello заявлению, вам потребуется файл dash.all.js toograb hello из версии hello 1.0 dash.js проекта. Это должен быть сохранен в папке приложения hello JavaScript. Этот файл является файлом удобства, которая запрашивает весь код необходимые dash.js hello в один файл. Если выглядел примерно репозиторий dash.js hello, необходимо найти hello отдельные файлы, проверки кода и многое другое но, если все toodo dash.js использования, то файл dash.all.js hello вам нужен.

tooadd hello dash.js tooyour видеопроигрывателей, добавить скрипт тег toohello раздел head basicPlayer.html:

    <!-- DASH-AVC/265 reference implementation -->
    < script src="js/dash.all.js"></script>


Создайте проигрыватель hello tooinitialize функции при загрузке страницы приветствия. Добавьте следующий сценарий после строки hello, в котором загружаются dash.all.js hello:

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

Эта функция сначала создает DashContext. Это приложение hello используется tooconfigure для среды выполнения требуемой среды. С технической точки зрения он определяет классы, которые hello framework внедрения зависимостей следует использовать при создании приложения hello приветствия. В большинстве случаев будет использоваться Dash.di.DashContext.

Далее создайте экземпляр hello основной класс Framework dash.js hello, MediaPlayer. Этот класс содержит ядро hello методы, такие как необходимые воспроизведения и приостановки, управляет hello связь с помощью элемента видео hello и также управляет hello интерпретацию hello презентации описание носителя (MPD) файл, который описывает видео toobe hello воспроизводиться.

функция startup() Hello hello MediaPlayer класс называется tooensure игрок hello — Готово tooplay видео. Среди прочего эта функция гарантирует, что все необходимые классы hello (как определено контекстом hello) были загружены. После подготовки hello проигрывателя можно присоединить tooit элемент video hello, с помощью функции attachView() hello. Это позволяет видеопотока hello tooinject MediaPlayer hello в элемент hello, а также управления воспроизведением при необходимости.

Передать URL-адрес hello hello MPD файл toohello MediaPlayer, чтобы его было известно о hello видео предполагается функция setupVideo() tooplay.hello только что создали потребуется toobe, выполненных после полной загрузки страницы приветствия. Для этого с помощью события onload hello элемента текста hello. Измените элемент <body> на:

    <body onload="setupVideo()">

Задайте размер hello hello видео элемента с помощью CSS. В среде адаптивной потоковой передачи это особенно важно, так как размер hello hello видео воспроизводится могут изменяться по мере воспроизведения адаптирует toochanging состояния сети. В этой демонстрации простых просто принудительно toobe элемент video hello 80% доступной браузере hello, добавив следующий раздел head toohello CSS страницы приветствия hello:

    <style>
    video {
      width: 80%;
      height: 80%;
    }
    </style>

## <a name="playing-a-video"></a>Воспроизведение видео
tooplay видео, укажите в браузере в файле basicPlayback.html hello и нажмите кнопку воспроизведения на hello видеопроигрыватель отображается.

## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>См. также
[Разработка приложений видеопроигрывателя](media-services-develop-video-players.md)

[Репозиторий dash.js на GitHub](https://github.com/Dash-Industry-Forum/dash.js) 

