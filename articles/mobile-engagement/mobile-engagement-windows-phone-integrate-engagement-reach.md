---
title: "aaaWindows Phone Silverlight достичь SDK-интеграция"
description: "Как tooIntegrate Azure Mobile Engagement связаться с приложениями Silverlight для Windows Phone"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: d3516a6b-db9f-4cdb-a475-4148edf81af1
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 09c8767216e11963c5c600755ab8d4d11cd92034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-reach-sdk-integration"></a>Интеграция пакета SDK Reach для Windows Phone Silverlight
Необходимо выполнить процедуры интеграции hello, описанной в hello [Windows Phone Silverlight Engagement SDK-Интеграция](mobile-engagement-windows-phone-integrate-engagement.md) до следующего руководства.

## <a name="embed-hello-engagement-reach-sdk-into-your-windows-phone-silverlight-project"></a>Внедрение hello Engagement Reach SDK в проект Windows Phone Silverlight
У вас ничего tooadd. `EngagementReach` уже включены в проект.

> [!TIP]
> Образы, расположенный в hello можно настраивать `Resources` папки проекта, особенно hello фирменной символики значок (что по умолчанию toohello Engagement).
> 
> 

## <a name="add-hello-capabilities"></a>Добавление возможностей hello
Hello Engagement Reach SDK должен некоторые дополнительные возможности.

Откройте ваш `WMAppManifest.xml` файл и убедитесь, что объявлены, hello следующие возможности:

* `ID_CAP_PUSH_NOTIFICATION`
* `ID_CAP_WEBBROWSERCOMPONENT`

Hello сначала используется один по hello MPNS службы tooallow hello отображение всплывающего уведомления. Hello второе — это используемые tooembed задачу браузера в hello SDK.

Изменить hello `WMAppManifest.xml` и добавьте внутри hello `<Capabilities />` тег:

    <Capability Name="ID_CAP_PUSH_NOTIFICATION" />
    <Capability Name="ID_CAP_WEBBROWSERCOMPONENT" />

## <a name="enable-hello-microsoft-push-notification-service"></a>Включить hello Microsoft Push Notification Service
В порядке hello toouse **Microsoft Push Notification Service** (называемый MPNS) вашего `WMAppManifest.xml` файл должен иметь `<App />` тег с `Publisher` атрибут значение toohello имя проекта.

## <a name="initialize-hello-engagement-reach-sdk"></a>Инициализировать hello Engagement Reach SDK
### <a name="engagement-configuration"></a>Конфигурация Engagement
централизованный Hello проектной конфигурации в hello `Resources\EngagementConfiguration.xml` файла проекта.

Измените эту настройку reach toospecify файла:

* *Необязательный*, показывают, как активировать hello системных Push-уведомлений (MPNS) или не между `<enableNativePush>` и `</enableNativePush>` теги (`true` по умолчанию).
* *Необязательный*, указывающей hello hello принудительной канал между `<channelName>` и `</channelName>` теги, предоставляют hello же, что приложение в настоящее время может использовать или оставьте поле пустым.

Если требуется, чтобы его во время выполнения вместо этого можно вызвать следующие hello toospecify метод до инициализации агента Engagement hello:

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    engagementConfiguration.Reach.EnableNativePush = true;                  
    /* [Optional] whether hello native push (MPNS) is activated or not. */

    engagementConfiguration.Reach.ChannelName = "YOUR_PUSH_CHANNEL_NAME";   
    /* [Optional] Provide hello same channel name that your application may currently use. */

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

> [!TIP]
> Можно указать имя hello канала push hello MPNS приложения. По умолчанию Engagement создает имя, основанное на hello appId. У вас нет необходимости toospecify hello имя самостоятельно, за исключением того, если планируется канала push hello toouse за пределами обязательств.
> 
> 

### <a name="engagement-initialization"></a>Инициализация Engagement
Изменение hello `App.xaml.cs`:

* Добавить tooyour `using` инструкции:
  
      using Microsoft.Azure.Engagement;
* Вставьте `EngagementReach.Instance.Init` сразу `EngagementAgent.Instance.Init` после в `Application_Launching`:
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
         EngagementAgent.Instance.Init();
         EngagementReach.Instance.Init();
      }
* Вставить `EngagementReach.Instance.OnActivated` в hello `Application_Activated` метод:
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
         EngagementReach.Instance.OnActivated(e);
      }

> [!IMPORTANT]
> Hello `EngagementReach.Instance.Init` выполняется в выделенном потоке. У вас toodo его самостоятельно.
> 
> 

## <a name="app-store-submission-considerations"></a>Замечания по отправке приложений в Магазин
Microsoft накладывает некоторые правила, при использовании hello push-уведомлений:

Из hello Microsoft [политики применения] документации, разделе 2.9:

1) Должно попросите hello пользователя tooaccept tooreceive push-уведомлений. В параметрах, добавьте способом toodisable hello push-уведомлений.

Объект EngagementReach Hello предоставляет два методы toomanage hello в/opt отказаться, `EnableNativePush()` и `DisableNativePush()`. Например, невозможно создать параметр в параметрах hello с toodisable переключателя или включить MPNS.

Можно также toodeactivate MPNS через конфигурацию hello Engagement\<windows phone-sdk-reach конфигурации\>.

> 2.9.1) приложения hello сначала необходимо описать предоставленный toobe уведомления hello и **получения явного разрешения пользователя hello (opt-in)**, и **необходимо предоставить механизм, посредством которой hello пользователя можно отказаться от получения Push-уведомления**. Все уведомления с помощью hello Microsoft Push Notification Service должны быть согласованы с пользователем toohello описание hello и должны соблюдать все применимые [политики применения] [ Content Policies]и [Дополнительные требования для конкретного приложения типов].
> 
> 

2) Не следует использовать слишком много push-уведомлений. Управлять уведомлениями будет Engagement.

> 2.9.2) приложение hello и ее использование hello Microsoft Push Notification Service должен не слишком пропускной способности сети или пропускной способности hello Microsoft Push Notification Service, а в противном случае происходит чрезмерного обременять Windows Phone или другие устройства Microsoft или службы с чрезмерным push-уведомления, по определению корпорации Майкрософт по ее обоснованному усмотрению и не должно нанести вред или помешать любой сетей Майкрософт или серверов или все серверы сторонних производителей или toohello подключенной сети служба Push-уведомлений Microsoft.
> 
> 

3) Не следует полагаться на MPNS toosend criticals сведения. Engagement использует MPNS, поэтому это правило также применяется для кампаний hello, созданный внутри hello Engagement переднего плана.

> 2.9.3) hello Microsoft Push Notification Service не может быть используется toosend уведомлений, которые являются критически важных или иным образом может повлиять на вопросы и ответы жизни или смерти, включая без ограничения критических уведомлений связанные tooa Медицинские устройства или условий. Майкрософт ПРЯМО отказывается от ANY никаких гарантий, hello используйте из hello MICROSOFT PUSH уведомления службы или ДОСТАВКИ из MICROSOFT PUSH-УВЕДОМЛЕНИЙ службы уведомления будет быть без ПЕРЕРЫВА, ошибка свободного или, в противном случае ГАРАНТИРУЕТСЯ tooOCCUR ON в реальном времени ОТДЕЛЬНО.
> 
> 

**Мы не можем гарантировать, приложение передаст hello процесса проверки, если вы не влияют на следующие рекомендации.**

## <a name="handle-data-push-optional"></a>Обработка отправленных данных (необязательно)
Если требуется вашего приложения toobe может tooreceive Reach данных Push-уведомлений, имеется tooimplement двумя событиями hello EngagementReach класса:

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

Задайте содержимое hello hello `EngagementReach.Instance.Handler` пользовательского объекта в поле вашего `App.xaml.cs` класс внутри hello `Application_Launching` метод.

**Пример кода:**

    private void Application_Launching(object sender, LaunchingEventArgs e)
    {
       // your app initialization 
       EngagementReach.Instance.Handler = new ExampleReachHandler();
       // Engagement Agent and Reach initialization
    }

> [!NOTE]
> По умолчанию Engagement использует собственную реализацию `EngagementReachHandler`. Нет toocreate собственный, и при этом, у вас нет toooverride каждого метода. поведение по умолчанию Hello — tooselect hello Engagement базовый объект.
> 
> 

### <a name="layouts"></a>Макеты
По умолчанию Reach будет использовать hello внедренные ресурсы hello DLL toodisplay hello уведомлений и страниц.

Тем не менее, вы можете toouse собственные ресурсы tooreflect фирменного стиля в этих компонентах.

Можно переопределить `EngagementReachHandler` методы в ваш подкласс tootell Engagement toouse макеты:

**Пример кода:**

    // In your subclass of EngagementReachHandler

    public override string GetTextViewAnnouncementUri()
    {
       // return hello path of your own xaml
    }

    public override string GetWebViewAnnouncementUri()
    {
       // return hello path of your own xaml
    }

    public override string GetPollUri()
    {
       // return hello path of your own xaml
    }

    public override EngagementNotificationView CreateNotification(EngagementNotificationViewModel viewModel)
    {
       // return a new instance of your own notification
    }

> [!TIP]
> Hello `CreateNotification` метод может возвращать значение null. Hello уведомления не будут отображаться и кампании reach hello, будут удалены.
> 
> 

toosimplify реализация макета, мы также предоставляем нашим собственным xaml, который можно использовать в качестве основы для кода. Они находятся в архиве Engagement SDK hello (/ src/reach /).

> [!WARNING]
> Hello источники, которые мы предоставляем hello точное используются те же, которые мы используем. Поэтому при необходимости toomodify их напрямую, не забыть toochange приветствия имен и hello имя.
> 
> 

### <a name="notification-position"></a>Расположение уведомлений
По умолчанию уведомление в приложении отображается в нижней левой hello приложения hello. Это поведение можно изменить путем переопределения hello `GetNotificationPosition` метод hello `EngagementReachHandler` объекта.

    // In your subclass of EngagementReachHandler

    public override EngagementReachHandler.NotificationPosition GetNotificationPosition(EngagementNotificationViewModel viewModel)
    {
       // return a value of hello EngagementReachHandler.NotificationPosition enum (TOP or BOTTOM)
    }

В настоящее время можно выбрать между hello `BOTTOM` (по умолчанию) и `TOP` позиций.

### <a name="launch-message"></a>Запуск сообщения
При щелчке Системное уведомление (всплывающее уведомление) запускает Engagement hello приложения, содержимое hello нагрузки hello отправляют сообщения и отображения страницы приветствия для hello соответствующий кампании.

Возникает задержка между запуска hello hello приложения и hello отображения страницы приветствия (в зависимости от скорости сети hello).

пользователь toohello tooindicate, что-то загружается, необходимо предоставить visual сведения, например, индикатор выполнения или индикатор хода выполнения. Engagement не может обработать ее самостоятельно, но предоставляет несколько обработчиков, которыми вы можете воспользоваться.

tooimplement hello обратного вызова, выполните действия.

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

Hello обратного вызова можно задать в вашей `Application_Launching` метод вашей `App.xaml.cs` файла предпочтительно перед hello `EngagementReach.Instance.Init()` вызова.

> [!TIP]
> Каждый обработчик вызывается hello потока пользовательского интерфейса. У вас tooworry при использовании MessageBox или что-нибудь связанные с Пользовательским интерфейсом.
> 
> 

[политики применения]:http://msdn.microsoft.com/library/windows/apps/hh184841(v=vs.105).aspx
[Content Policies]:http://msdn.microsoft.com/library/windows/apps/hh184842(v=vs.105).aspx
[Дополнительные требования для конкретного приложения типов]:http://msdn.microsoft.com/library/windows/apps/hh184838(v=vs.105).aspx

