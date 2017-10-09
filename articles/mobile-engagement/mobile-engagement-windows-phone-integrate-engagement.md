---
title: "aaaWindows Phone Silverlight Engagement SDK-интеграция"
description: "Как tooIntegrate Azure Mobile Engagement с приложениями Silverlight для Windows Phone"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 447fea8d-f4e3-4ad4-8ec0-8e3cf1ad3ab0
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: f65683a62e5256cea469a3a73d99ade4331cb6bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-engagement-sdk-integration"></a>Интеграция пакета SDK Engagement для Windows Phone Silverlight
> [!div class="op_single_selector"]
> * [Windows Universal](mobile-engagement-windows-store-integrate-engagement.md) 
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [iOS](mobile-engagement-ios-integrate-engagement.md) 
> * [Android](mobile-engagement-android-integrate-engagement.md) 
> 
> 

Эта процедура описывает hello простейший способ tooactivate Azure Mobile Engagement аналитики и наблюдение за функциями в приложении Windows Phone Silverlight.

следующие шаги Hello — это отчет hello достаточно tooactivate журналов необходимости toocompute все статистические данные о пользователей, сеансы, действия, сбои и Technicals. Hello журналов требуется отчет toocompute другие статистические данные, как события, ошибок и задания должны выполняться вручную с помощью hello Engagement API (в разделе [как toouse hello дополнительные теги API в приложения Windows Phone Silverlight мобильного охвата](mobile-engagement-windows-phone-use-engagement-api.md) см. ниже), так как эти статистические данные, зависящие от приложения.

## <a name="supported-versions"></a>Поддерживаемые версии
только Hello SDK Mobile Engagement для Windows Silverlight можно интегрировать в приложения, предназначенные для:

* Windows Phone 8.0
* Windows Phone 8.1 Silverlight

> [!NOTE]
> Если в качестве цели Windows Phone 8.1 (отличных от Silverlight), а затем ссылаться toohello [Windows универсальной процедуры интеграции](mobile-engagement-windows-store-integrate-engagement.md).
> 
> 

## <a name="install-hello-mobile-engagement-silverlight-sdk"></a>Установить пакет SDK Mobile Engagement Silverlight hello
Hello SDK Mobile Engagement для Windows Silverlight доступен как пакет Nuget вызывается *MicrosoftAzure.MobileEngagement*. Его можно установить из hello диспетчера пакетов Nuget для Visual Studio. 

## <a name="add-hello-capabilities"></a>Добавление возможностей hello
Hello Engagement SDK должен некоторые возможности hello пакет SDK для Windows Phone Silverlight в порядке toowork должным образом.

Откройте ваш `WMAppManifest.xml` файл и убедитесь, что hello следующие возможности, объявляются в hello `Capabilities` панели:

* `ID_CAP_NETWORKING`
* `ID_CAP_IDENTITY_DEVICE`

## <a name="initialize-hello-engagement-sdk"></a>Инициализировать hello Engagement SDK
### <a name="engagement-configuration"></a>Конфигурация Engagement
централизованный Hello проектной конфигурации в hello `Resources\EngagementConfiguration.xml` файла проекта.

Измените этот файл toospecify:

* строку подключения приложения между тегами `<connectionString>` and `<\connectionString>`.

Если требуется, чтобы его во время выполнения вместо этого можно вызвать следующие hello toospecify метод до инициализации агента Engagement hello:

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

Hello строку подключения для приложения отображается на hello классический портал Azure.

### <a name="engagement-initialization"></a>Инициализация Engagement
При создании проекта создается файл `App.xaml.cs` . Этот класс наследуется из `Application` и содержит множество важных методов. Он также будет hello используется tooinitialize Engagement SDK.

Изменение hello `App.xaml.cs`:

* Добавить tooyour `using` инструкции:
  
      using Microsoft.Azure.Engagement;
* Вставить `EngagementAgent.Instance.Init` в hello `Application_Launching` метод:
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
        EngagementAgent.Instance.Init();
      }
* Вставить `EngagementAgent.Instance.OnActivated` в hello `Application_Activated` метод:
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
      }

> [!WARNING]
> Настоятельно рекомендуется не вы tooadd hello Engagement инициализации в другом месте приложения. Однако учтите, что hello `EngagementAgent.Instance.Init` метод выполняется в выделенном потоке, а не на hello поток пользовательского интерфейса.
> 
> 

## <a name="basic-reporting"></a>Упрощенные отчеты
### <a name="recommended-method--overload-your-phoneapplicationpage-classes"></a>Рекомендуемый метод: перегрузка классов `PhoneApplicationPage`
В отчете hello tooactivate порядок всех журналов hello, необходимых в Engagement toocompute пользователей, сеансы, действия, сбои и технические данные, можно просто сделать все вашей `PhoneApplicationPage` вложенные классы наследуют от hello `EngagementPage` классы.

Ниже приведен пример того, как toodo это для страницы приложения. Можно сделать hello одинаково для всех страниц приложения.

#### <a name="c-source-file"></a>Исходный файл на C#
Измените файл страницы `.xaml.cs` :

* Добавить tooyour `using` инструкции:
  
      using Microsoft.Azure.Engagement;
* Замените `PhoneApplicationPage` на `EngagementPage`:

**Без Engagement:**

        namespace Example
        {
          public partial class ExamplePage : PhoneApplicationPage
          {
            [...]
          }
        }

**С Engagement:**

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!WARNING]
> Если на странице наследуется от hello `OnNavigatedTo` метод, быть тщательно toolet hello `base.OnNavigatedTo(e)` вызова. В противном случае действие hello не будут отображаться. На самом деле hello `EngagementPage` вызывает `StartActivity` внутри hello `OnNavigatedTo` метод.
> 
> 

#### <a name="xaml-file"></a>XAML-файл
Измените файл страницы `.xaml` :

* Добавьте tooyour объявления пространств имен:
  
      xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
* Замените `phone:PhoneApplicationPage` на `engagement:EngagementPage`:

**Без Engagement:**

        <phone:PhoneApplicationPage>
            <!-- layout -->
        </phone:PhoneApplicationPage>

**С Engagement:**

        <engagement:EngagementPage 
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP">

            <!-- layout -->
        </engagement:EngagementPage >

#### <a name="override-hello-default-behavior"></a>Переопределить поведение по умолчанию hello
По умолчанию имя класса hello страницы приветствия отображается как имя действия hello с без дополнительных. Если класс hello использует hello суффикс «Страница», Engagement также удалит ее.

Если требуется поведение по умолчанию hello toooverride имени hello, просто добавьте следующий код tooyour.

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
           /* your code */
           return "new name";
        }

Если требуется tooreport некоторыми дополнительными сведениями с действием, можно добавить этот код tooyour:

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
           /* your code */
           return extra;
        }

Эти методы вызываются из внутри hello `OnNavigatedTo` метод страницы.

### <a name="alternate-method-call-startactivity-manually"></a>Альтернативный метод: вызов `StartActivity()` вручную
Если невозможно или нежелательно toooverload вашей `PhoneApplicationPage` классы, вместо этого можно запустить ваши действия путем вызова `EngagementAgent` методы напрямую.

Советуем вызывать `StartActivity` в методе `OnNavigatedTo` класса PhoneApplicationPage.

        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
           base.OnNavigatedTo(e);
           EngagementAgent.Instance.StartActivity("MyPage");
        }

> [!IMPORTANT]
> Убедитесь, что сеанс завершен правильно.
> 
> пакет SDK для Hello автоматически вызывает hello `EndActivity` метод при закрытии приложения hello. Таким образом, **высокой** рекомендуется toocall hello `StartActivity` метод изменении hello действий пользователя hello и слишком**никогда** hello вызовов `EndActivity` метод. Этот метод отправляет сообщение сервера Engagement toohello что hello текущий пользователь покинул приложения hello, и это влияет на все журналы приложений.
> 
> 

## <a name="advanced-reporting"></a>Расширенные отчеты
При необходимости вы можете tooreport приложения определенных событий, ошибок и задания, toodo таким образом, использование hello другие методы найдены в hello `EngagementAgent` класса. Hello Engagement API позволяет toouse всем Engagement расширенные возможности.

Дополнительные сведения см. в разделе [как toouse hello дополнительные теги API в приложения Windows Phone Silverlight мобильного охвата](mobile-engagement-windows-phone-use-engagement-api.md).

## <a name="advanced-configuration"></a>Расширенная конфигурация
### <a name="disable-automatic-crash-reporting"></a>Отключение автоматического создания отчетов о сбоях
Можно отключить hello аварийного завершения автоматического компонент рвением отчетов. После этого при возникновении необработанного исключения Engagement не будет предпринимать никаких действий.

> [!WARNING]
> Если планируется toodisable эту функцию, помните, что, когда необработанное сбоя будет появляться в вашем приложении, Engagement не будет отправлять hello аварийного завершения **AND** не закроет сеанс hello и заданий.
> 
> 

автоматического создания отчетов, о сбоях toodisable просто настроить конфигурацию, в зависимости от того, она была объявлена как hello:

#### <a name="from-engagementconfigurationxml-file"></a>Из файла `EngagementConfiguration.xml`
Отчет набора аварийное завершение работы слишком`false` между `<reportCrash>` и `</reportCrash>` тегов.

#### <a name="from-engagementconfiguration-object-at-run-time"></a>Из объекта `EngagementConfiguration` во время выполнения
Задать toofalse сбоя отчетов с помощью объекта EngagementConfiguration.

        /* Engagement configuration. */

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration(); engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";
        /\* Disable Engagement crash reporting. \*/ engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a>Пакетный режим
По умолчанию hello Engagement службы отчетов входит в режиме реального времени. Если приложение сообщает журналов производится очень часто, это лучше toobuffer hello журналы и tooreport их все за один раз на обычное время базового (это называется «пакетный режим» hello).

toodo таким образом, необходимо вызвать метод hello:

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

Hello аргумент представляет собой значение в **миллисекунд**. В любое время Если требуется ведение журнала hello в режиме реального времени для tooreactivate просто вызовите метод hello без какого-либо параметра или со значением hello 0.

Hello пакетный режим немного увеличить батареи hello жизни но оказывает влияние на hello монитор Engagement: все сеансы и задания будут скругленными toohello пороговое значение пакетного режима (таким образом, сеансы и задания короче, чем порог повышения hello не могут быть видны). Это рекомендуется toouse Повышение порогового значения больше чем 30000 (30s). Необходимо учитывать, сохраненные журналы являются элементами ограниченный too300 toobe. Если отправка занимает слишком много времени, некоторые журналы могут быть потеряны.

> [!WARNING]
> Hello пороговое значение пакета не может быть настроен меньший период tooa одного раза в секунду. При попытке toodo таким образом, hello SDK будет отображать трассировку с ошибкой hello и автоматически сбросить toohello значение по умолчанию, то есть, ноль секунд. Это приведет к началу hello SDK tooreport hello журналы в режиме реального времени.
> 
> 

