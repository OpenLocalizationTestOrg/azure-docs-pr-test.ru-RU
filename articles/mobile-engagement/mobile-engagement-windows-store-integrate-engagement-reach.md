---
title: "aaaWindows универсальных приложений достичь интеграции пакета SDK"
description: "Как tooIntegrate Azure Mobile Engagement связаться с помощью универсальных приложений Windows"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a31ca1d6-856f-4aec-898a-07969ae5f7ec
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: af311c65940014083333853875a00173b8d6783e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-reach-sdk-integration"></a>Интеграция пакета SDK Reach для универсальных приложений для Windows
Необходимо выполнить процедуры интеграции hello, описанной в hello [интеграции пакета SDK Windows универсальной Engagement](mobile-engagement-windows-store-integrate-engagement.md) до следующего руководства.

## <a name="embed-hello-engagement-reach-sdk-into-your-windows-universal-project"></a>Внедрение hello Engagement Reach SDK в проект Windows Universal.
У вас ничего tooadd. `EngagementReach` уже включены в проект.

> [!TIP]
> Образы, расположенный в hello можно настраивать `Resources` папки проекта, особенно hello фирменной символики значок (что по умолчанию toohello Engagement). Для универсальных приложений также можно перемещать hello `Resources` папку на ваш tooshare общего проекта, его содержимое между приложениями, но будет иметь tookeep hello `Resources\EngagementConfiguration.xml` файлов на расположение по умолчанию, поскольку это зависит от используемой платформы.
> 
> 

## <a name="enable-hello-windows-notification-service"></a>Включить службу уведомлений Windows hello
### <a name="windows-8x-and-windows-phone-81-only"></a>Только для Windows 8.x и Windows Phone 8.1
В порядке hello toouse **службы уведомлений Windows** (называемый WNS) в вашей `Package.appxmanifest` файлов на `Application UI` щелкните `All Image Assets` в поле слева роботов hello. В hello справа от поля hello в `Notifications`, изменить `toast capable` из `(not set)` слишком`(Yes)`.

### <a name="all-platforms"></a>Все платформы
Необходимо toosynchronize вашего приложения tooyour Microsoft учетной записи и toohello платформа для взаимодействия. Для этого требуется toocreate учетную запись или войдите в систему [центра разработчиков windows](https://dev.windows.com). После того, создайте новое приложение и найти hello SID и секретный ключ. На сервере переднего плана engagement hello, перейдите на параметры приложения в `native push` и вставьте свои учетные данные. После этого щелкните правой кнопкой мыши проект и выберите `store` и `Associate App with hello Store...`. Необходимо просто приложения hello tooselect имеют перед toosynchronize ее создании.

## <a name="initialize-hello-engagement-reach-sdk"></a>Инициализировать hello Engagement Reach SDK
Изменение hello `App.xaml.cs`:

* Вставьте `EngagementReach.Instance.Init` сразу после `EngagementAgent.Instance.Init` в методе `InitEngagement`:
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
        EngagementReach.Instance.Init(e);
      }
  
  Hello `EngagementReach.Instance.Init` выполняется в выделенном потоке. У вас toodo его самостоятельно.

> [!NOTE]
> Если вы используете push-уведомлений в другом месте в приложении, то у вас слишком[совместно используют канал принудительной](#push-channel-sharing) с Engagement Reach.
> 
> 

## <a name="integration"></a>Интеграция
Engagement предоставляет два способа tooadd hello Reach в приложении ленты и interstitial представления для объявлений и для опросов в приложении: hello наложения интеграции и вручную интеграции hello web представления. Не следует сочетать оба подхода hello одной страницы.

Таким образом может описать Hello Выбор между двумя интеграции hello.

* Может выбрать интеграции наложения hello, если на страницах уже наследует от hello агента `EngagementPage`, он является лишь замены `EngagementPage` по `EngagementPageOverlay` и `xmlns:engagement="using:Microsoft.Azure.Engagement"` по `xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"` на страницах.
* Вы можете вручную интеграции hello web представления tooprecisely месте hello достичь пользовательского интерфейса внутри страницы или если вы не хотите tooadd другой страницы уровня tooyour наследования. 

### <a name="overlay-integration"></a>Интеграции наложения
наложение Engagement Hello динамически добавляет элементы пользовательского интерфейса hello используемых кампаниями Reach toodisplay на странице. Если макет не подходит для наложения hello следует hello веб-представления вручную интеграции вместо.

В изменения файла .xaml `EngagementPage` слишком ссылки`EngagementPageOverlay`

* Добавьте tooyour объявления пространств имен:
  
      xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"
* Замените `engagement:EngagementPage` на `engagement:EngagementPageOverlay`:

**EngagementPage:**

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">

            <!-- Your layout -->
        </engagement:EngagementPage>

**EngagementPageOverlay:**

        <engagement:EngagementPageOverlay 
            xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay">

            <!-- Your layout -->
        </engagement:EngagementPageOverlay>

Затем в CS-файле пометьте страницу тегом `EngagementPageOverlay`, а не `EngagementPage`, и импортируйте `Microsoft.Azure.Engagement.Overlay`.

            using Microsoft.Azure.Engagement.Overlay;

* Замените `EngagementPage` на `EngagementPageOverlay`:

**EngagementPage:**

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPage
              {
                [...]
              }
            }

**EngagementPageOverlay:**

            using Microsoft.Azure.Engagement.Overlay;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPageOverlay 
              {
                [...]
              }
            }


Hello наложения Engagement добавляет `Grid` элемент поверх страницы состоит из макета и hello двух `WebView` элементы один для hello banner и другую переменную, чтобы представление interstitial hello hello.

Можно настраивать элементы наложения hello непосредственно в hello `EngagementPageOverlay.cs` файла.

### <a name="web-views-manual-integration"></a>Интеграция веб-представлений вручную
Reach будет искать на страницах hello двух `WebView` отвечает за отображение баннера hello и hello interstitial представление элементов. Здравствуйте, только что toodo tooadd этих двух `WebView` элементы где-нибудь на страницах, ниже приведен пример:

    <Grid x:Name="engagementGrid">

      <!-- Your layout -->

      <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Stretch" VerticalAlignment="Top"/>
      <WebView x:Name="engagement_announcement_content" Visibility="Collapsed"  HorizontalAlignment="Stretch"  VerticalAlignment="Stretch"/>
    </Grid>


В этом примере hello `WebView` элементы являются растяжением toofit их контейнер, который автоматически размеров их повторно в случае изменения размера экрана поворот или окна.

> [!WARNING]
> Очень важно tookeep hello же именования `engagement_notification_content` и `engagement_announcement_content` для hello `WebView` элементов. Reach определяет элементы по имени. 
> 
> 

## <a name="handle-datapush-optional"></a>Обработка отправленных данных (необязательно)
Если требуется вашего приложения toobe может tooreceive Reach данных Push-уведомлений, имеется tooimplement двумя событиями hello EngagementReach класса:

Добавьте в App.xaml.cs в конструкторе App() hello.

            EngagementReach.Instance.DataPushStringReceived += (body) =>
            {
              Debug.WriteLine("String data push message received: " + body);
              return true;
            };

            EngagementReach.Instance.DataPushBase64Received += (decodedBody, encodedBody) =>
            {
              Debug.WriteLine("Base64 data push message received: " + encodedBody);
              // Do something useful with decodedBody like updating an image view
              return true;
            };

Вы увидите ответного вызова hello каждый метод возвращает логическое значение. Engagement отправляет отзыв tooits внутренней после отправки hello Принудительная отправка данных. Если hello обратный вызов возвращает значение false, hello `exit` отзыв будет отправлено. В противном случае отправляется `action`. Если обратный вызов не имеет значение для событий hello, hello `drop` отзыв будет возвращаться tooEngagement.

> [!WARNING]
> Engagement не может tooreceive кратные отзывы для принудительной отправки данных. Если вы планируете tooset несколько обработчиков событий, имейте в виду, что hello отзыв будет соответствовать toohello отправлено последним. В этом случае рекомендуется tooalways возвращает hello же tooavoid значение с путаницу отзывы на hello переднего плана.
> 
> 

## <a name="customize-ui-optional"></a>Настройка пользовательского интерфейса (необязательно)
### <a name="first-step"></a>Первый шаг
Мы даем reach hello toocustomize пользовательского интерфейса.

toodo таким образом, у вас есть toocreate подкласс hello `EngagementReachHandler` класса.

**Пример кода:**

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              internal class ExampleReachHandler : EngagementReachHandler
              {
               // Override EngagementReachHandler methods depending on your needs
              }
            }

Задайте содержимое hello hello `EngagementReach.Instance.Handler` пользовательского объекта в поле вашего `App.xaml.cs` класс внутри hello `App()` метод.

**Пример кода:**

            protected override void OnLaunched(LaunchActivatedEventArgs args)
            {
              // your app initialization 
              EngagementReach.Instance.Handler = new ExampleReachHandler();
              // Engagement Agent and Reach initialization
            }

> [!NOTE]
> По умолчанию Engagement использует собственную реализацию `EngagementReachHandler`.
> Нет toocreate собственный, и при этом, у вас нет toooverride каждого метода. поведение по умолчанию Hello — tooselect hello Engagement базовый объект.
> 
> 

### <a name="web-view"></a>Веб-представление
По умолчанию Reach будет использовать hello внедренные ресурсы hello DLL toodisplay hello уведомлений и страниц.

tooprovide полной возможности настройки, воспользуемся веб-представление. Если toocustomize макеты, переопределите непосредственно файлы ресурсов hello `EngagementAnnouncement.html` и `EngagementNotification.html`. Engagement должен весь код в `<body></body>` toorun правильно. Однако можно добавить тег снаружи `engagement_webview_area`.

Однако можно решить toouse собственные ресурсы.

Можно переопределить `EngagementReachHandler` методы в ваш подкласс tootell Engagement toouse макеты, но принимают механизм engagement hello tooembedded осторожность:

**Пример кода:**

            // In your subclass of EngagementReachHandler

            public override string GetAnnouncementHTML()
            {
              return base.GetAnnouncementHTML();
            }
            public override string GetAnnouncementName()
            {
              return base.GetAnnouncementName();
            }
            public override string GetNotfificationHTML()
            {
              return base.GetNotfificationHTML();
            }
            public override string GetNotfificationName()
            {
              return base.GetNotfificationName();
            }


По умолчанию AnnouncementHTML — это `ms-appx-web:///Resources/EngagementAnnouncement.html`. Он представляет hello HTML-файл, разрабатывать hello содержимое сообщения push (текст объявления, Web anoucement и объявления опроса). AnnouncementName — `engagement_announcement_content`. Это имя hello hello проектирования webview в xaml-страницы.

NotfificationHTML — `ms-appx-web:///Resources/EngagementNotification.html`. Он представляет hello HTML-файл, создать уведомление о push-сообщение hello. NotfificationName — `engagement_notification_content`. Это имя hello hello проектирования webview в xaml-страницы.

### <a name="customization"></a>Настройка
Вы можете настроить необходимое веб-представление уведомлений и объявлений, если сохраните объект Engagement. Будьте внимательны, веб-представление объекта описан три раза — hello первый раз в xaml, второй раз в CS-файл в методе «setwebview()» hello и третий раз в HTML-файле hello.

* В коде xaml описывают hello текущего компонента webview графическом макете.
* В CS-файл можно определить «setwebview()», в котором заданы hello измерение hello два веб-представление (уведомления, объявления). Он является весьма эффективным, когда меняет размер приложения hello.
* В HTML-файле Engagement hello описывают hello webview содержимого, разработки и hello позиций элементов друг с другом.

### <a name="launch-message"></a>Запуск сообщения
Когда пользователь щелкает Системное уведомление (всплывающее уведомление), Engagement запускает приложение hello, содержимое hello нагрузки hello отправляют сообщения и отображения страницы приветствия для соответствующей кампании hello.

Возникает задержка между запуска hello hello приложения и hello отображения страницы приветствия (в зависимости от скорости сети hello).

пользователь toohello tooindicate, что-то загружается, необходимо предоставить visual сведения, например, индикатор выполнения или индикатор хода выполнения. Engagement не может обработать ее самостоятельно, но предоставляет несколько обработчиков, которыми вы можете воспользоваться.

Добавление обратного вызова hello tooimplement в App.xaml.cs в «{} открытый App()»:

            /* hello application has launched and hello content is loading.
             * You should display an indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageStarted += () => { [...] };

            /* hello application has finished loading hello content and hello page
             * is about toobe displayed.
             * You should hide hello indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageCompleted += () => { [...] };

            /* hello content has been loaded, but an error has occurred.
             * You can provide an information toohello user.
             * You should hide hello indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageFailed += () => { [...] };

Hello обратного вызова можно задать в методе «Открытый App() {}» из вашей `App.xaml.cs` файла предпочтительно перед hello `EngagementReach.Instance.Init()` вызова.

> [!TIP]
> Каждый обработчик вызывается hello потока пользовательского интерфейса. У вас tooworry при использовании MessageBox или что-нибудь связанные с Пользовательским интерфейсом.
> 
> 

## <a id="push-channel-sharing"></a> Общий доступ к каналу push-уведомлений
При использовании push-уведомлений для других целей в приложении есть toouse hello принудительной канала функции hello Engagement SDK общего доступа. Это tooavoid пропущенных push.

* Вы можете предоставить свои собственные push toohello Engagement Reach инициализации канала. Hello SDK будет использовать его вместо нового запроса.

Обновить hello Engagement Reach инициализации канала push в hello `InitEngagement` метод hello `App.xaml.cs` файла:

    /* Your own push channel logic... */
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    /*...Engagement initialization */
    EngagementAgent.Instance.Init(e);
    EngagementReach.Instance.Init(e,pushChannel);

* Кроме того Если необходимо просто tooconsume hello push канала после инициализации Reach hello обратного вызова можно задать на Engagement Reach канала push tooget hello после его создания, пакет SDK для hello.

Задать обратного вызова в любом месте **после** hello Reach инициализации:

    /* Set action on hello SDK push channel. */
    EngagementReach.Instance.SetActionOnPushChannel((PushNotificationChannel channel) => 
    {
      /* hello forwarded channel can be null if its creation fails for any reason. */
      if (channel != null)
      {
        /* Your own push channel logic... */
      });
    }

## <a name="custom-scheme-tip"></a>Совет по настраиваемой схеме
Мы предоставляем возможность использования настраиваемой схемы. Можно отправить другой тип URI из toobe engagement переднего плана, в приложении обязательств. Управление схемой по умолчанию, например `http, ftp, ...`, осуществляет операционная система Windows. Если на устройстве не установлено приложение по умолчанию, появится окно с запросом. Также можно создать собственную настраиваемую схему для своего приложения.

простой способ Hello tooset пользовательской схемы в приложении является tooopen вашей `Package.appxmanifest` перейдите в `Declarations` панель. Выберите `Protocol` в прокрутите доступные объявления hello и добавить его. Изменить hello `Name` имя требуемого поля с вашего нового протокола.

Теперь toouse этот протокол изменить ваш `App.xaml.cs` с hello `OnActivated` метод и также не забывайте tooinitialize engagement здесь:

            /// <summary>
            /// Enter point when app his called by another way than user click
            /// </summary>
            /// <param name="args">Activation args</param>
            protected override void OnActivated(IActivatedEventArgs args)
            {
              /* Init engagement like it was launch by a custom uri scheme */
              EngagementAgent.Instance.Init(args);
              EngagementReach.Instance.Init(args);

              //TODO design action toodo when app is launch

              #region Custom scheme use
              if (args.Kind == ActivationKind.Protocol)
              {
                ProtocolActivatedEventArgs myProtocol = (ProtocolActivatedEventArgs)args;

                if (myProtocol.Uri.Scheme.Equals("protocolName"))
                {
                  string path = myProtocol.Uri.AbsolutePath;
                }
              }
              #endregion

