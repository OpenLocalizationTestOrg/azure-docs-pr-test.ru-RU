---
title: "SDK-интеграция универсальных приложений Engagement aaaWindows"
description: "Как tooIntegrate Azure Mobile Engagement с универсальные приложения Windows"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 71236b68-5ebd-44aa-8c82-c7ca8098ea05
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 18543798099c233dbe55cc387ba0216e369c8596
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-engagement-sdk-integration"></a>Интеграция пакета SDK Engagement для универсальных приложений для Windows
> [!div class="op_single_selector"]
> * [Универсальная платформа Windows](mobile-engagement-windows-store-integrate-engagement.md) 
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [iOS](mobile-engagement-ios-integrate-engagement.md) 
> * [Android](mobile-engagement-android-integrate-engagement.md) 
> 
> 

Эта процедура описывает hello простейший способ tooactivate Engagement аналитики и наблюдение за функциями в приложении Windows Universal.

следующие шаги Hello — это отчет hello достаточно tooactivate журналов необходимости toocompute все статистические данные о пользователей, сеансы, действия, сбои и Technicals. Hello журналов требуется отчет toocompute другие статистические данные, как события, ошибок и задания должны выполняться вручную с помощью hello Engagement API (в разделе [как toouse hello дополнительные теги API в приложении универсальное приложение для Windows Mobile Engagement](mobile-engagement-windows-store-use-engagement-api.md) с момента Эти статистические данные зависит от приложения.

## <a name="supported-versions"></a>Поддерживаемые версии
только Hello Mobile Engagement SDK для универсальных приложений Windows можно интегрировать в среды выполнения Windows и приложений универсальной платформы Windows, предназначенных для:

* Windows 8
* Windows 8.1
* Windows Phone 8.1
* Windows 10 (настольных компьютеров и мобильных устройств)

> [!NOTE]
> Если в качестве цели Windows Phone Silverlight, а затем ссылаться toohello [процедуры интеграции Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md).
> 
> 

## <a name="install-hello-mobile-engagement-universal-apps-sdk"></a>Установить пакет SDK Mobile Engagement универсальные приложения hello
### <a name="all-platforms"></a>Все платформы
Mobile Engagement SDK для Windows универсального приложения Hello доступен как пакет Nuget вызывается *MicrosoftAzure.MobileEngagement*. Его можно установить из hello диспетчера пакетов Nuget для Visual Studio.

### <a name="windows-8x-and-windows-phone-81"></a>Windows 8.x и Windows Phone 8.1
NuGet автоматически развертывает ресурсы SDK hello hello `Resources` папки корневого каталога проекта приложения hello.

### <a name="windows-10-universal-windows-platform-applications"></a>Универсальные приложения для Windows 10
NuGet не развертывает ресурсы SDK hello в приложении UWP еще автоматически. У вас есть toodo его вручную до развертывания ресурсов возникает снова в NuGet:

1. Откройте обозреватель файлов.
2. Перейдите в следующие расположения toohello (**x.x.x** версия hello взаимодействия при установке): *% USERPROFILE %\\.nuget\packages\MicrosoftAzure.MobileEngagement\\*  *x.x.x**\\content\win81*
3. Перетаскивание hello **ресурсов** папку из корня toohello explorer hello файл проекта в Visual Studio.
4. В Visual Studio выберите проект и активировать hello **Показать все файлы** значок поверх hello **обозревателе решений**.
5. Некоторые файлы не будут включены в проект hello. их за один раз щелкните правой кнопкой мыши hello tooimport **ресурсов** папки, **исключить из проекта** то другой щелкните правой кнопкой мыши hello **ресурсов** папки, **Include в проекте** toore-включить hello всю папку. Все файлы из hello **ресурсов** папки теперь включены в проект.

## <a name="add-hello-capabilities"></a>Добавление возможностей hello
Hello Engagement SDK должен некоторые возможности hello пакета SDK для Windows в порядке toowork должным образом.

Откройте ваш `Package.appxmanifest` файл и убедитесь, что объявлены, hello следующие возможности:

* `Internet (Client)`

## <a name="initialize-hello-engagement-sdk"></a>Инициализировать hello Engagement SDK
### <a name="engagement-configuration"></a>Конфигурация Engagement
централизованный Hello проектной конфигурации в hello `Resources\EngagementConfiguration.xml` файла проекта.

Измените этот файл toospecify:

* строку подключения приложения между тегами `<connectionString>` and `<\connectionString>`.

Если требуется, чтобы его во время выполнения вместо этого можно вызвать следующие hello toospecify метод до инициализации агента Engagement hello:

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set hello Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);

Hello строку подключения для приложения отображается на hello классический портал Azure.

### <a name="engagement-initialization"></a>Инициализация Engagement
При создании проекта создается файл `App.xaml.cs` . Этот класс наследуется из `Application` и содержит множество важных методов. Он также будет hello используется tooinitialize Engagement SDK.

Изменение hello `App.xaml.cs`:

* Добавить tooyour `using` инструкции:
  
      using Microsoft.Azure.Engagement;
* Определите инициализации метода tooshare hello Engagement один раз для всех вызовов.
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
  
        // or
  
        EngagementAgent.Instance.Init(e, engagementConfiguration);
      }
* Вызовите `InitEngagement` в hello `OnLaunched` метод:
  
      protected override void OnLaunched(LaunchActivatedEventArgs e)
      {
        InitEngagement(e);
      }
* При запуске приложения с использованием пользовательской схемы другого приложения или hello командной строки затем hello `OnActivated` вызывается метод. Необходимо также tooinitiate hello Engagement SDK при активации приложения. Таким образом, переопределите toodo `OnActivated` метод:
  
      protected override void OnActivated(IActivatedEventArgs args)
      {
        InitEngagement(args);
      }

> [!IMPORTANT]
> Настоятельно рекомендуется не вы tooadd hello Engagement инициализации в другом месте приложения.
> 
> 

## <a name="basic-reporting"></a>Упрощенные отчеты
### <a name="recommended-method-overload-your-page-classes"></a>Рекомендуемый метод: перегрузка классов `Page`
В отчете hello tooactivate порядок всех журналов hello, необходимых в Engagement toocompute пользователей, сеансы, действия, сбои и технические данные, можно просто сделать все вашей `Page` вложенные классы наследуют от hello `EngagementPage` классы.

Ниже приведен пример того, как toodo это для страницы приложения. Можно сделать hello одинаково для всех страниц приложения.

#### <a name="c-source-file"></a>Исходный файл на C#
Измените файл страницы `.xaml.cs` :

* Добавить tooyour `using` инструкции:
  
      using Microsoft.Azure.Engagement;
* Замените `Page` на `EngagementPage`:

**Без Engagement:**

        namespace Example
        {
          public sealed partial class ExamplePage : Page
          {
            [...]
          }
        }

**С Engagement:**

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public sealed partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!IMPORTANT]
> Если на странице переопределяет hello `OnNavigatedTo` метода будет убедиться, что toocall `base.OnNavigatedTo(e)`. В противном случае не будет указано действие hello (hello `EngagementPage` вызовы `StartActivity` внутри его `OnNavigatedTo` метода).
> 
> 

#### <a name="xaml-file"></a>XAML-файл
Измените файл страницы `.xaml` :

* Добавьте tooyour объявления пространств имен:
  
      xmlns:engagement="using:Microsoft.Azure.Engagement"
* Замените `Page` на `engagement:EngagementPage`:

**Без Engagement:**

        <Page>
            <!-- layout -->
            ...
        </Page>

**С Engagement:**

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">
            <!-- layout -->
            ...
        </engagement:EngagementPage >

#### <a name="override-hello-default-behaviour"></a>Переопределение поведения по умолчанию hello
По умолчанию имя класса hello страницы приветствия отображается как имя действия hello с без дополнительных. Если класс hello использует hello суффикс «Страница», Engagement также удалит ее.

Если требуется поведение по умолчанию hello toooverride имени hello, просто добавьте следующий код tooyour.

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

Если вы хотите tooreport некоторые дополнительные сведения с действием, можно добавить этот код tooyour:

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

Эти методы вызываются из внутри hello `OnNavigatedTo` метод страницы.

### <a name="alternate-method-call-startactivity-manually"></a>Альтернативный метод: вызов `StartActivity()` вручную
Если невозможно или нежелательно toooverload вашей `Page` классы, вместо этого можно запустить ваши действия путем вызова `EngagementAgent` методы напрямую.

Мы рекомендуем toocall `StartActivity` внутри вашей `OnNavigatedTo` метод страницы.

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> Убедитесь, что сеанс завершен правильно.
> 
> пакет SDK для Universal Windows Hello автоматически вызывает hello `EndActivity` метод при закрытии приложения hello. Таким образом, **высокой** рекомендуется toocall hello `StartActivity` метод изменении hello действий пользователя hello и слишком**никогда** hello вызовов `EndActivity` метода, этот метод отправляет tooEngagement сервер, текущий пользователь имеет приложение hello оставьте, именно она влияет на все журналы приложений.
> 
> 

## <a name="advanced-reporting"></a>Расширенные отчеты
При необходимости вы можете tooreport приложения определенных событий, ошибок и задания, toodo таким образом, использование hello другие методы найдены в hello `EngagementAgent` класса. Hello Engagement API позволяет toouse всем Engagement расширенные возможности.

Дополнительные сведения см. в разделе [как toouse hello дополнительные теги API в приложении универсальное приложение для Windows Mobile Engagement](mobile-engagement-windows-store-use-engagement-api.md).

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
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a>Пакетный режим
По умолчанию hello Engagement службы отчетов входит в режиме реального времени. Если приложение сообщает журналов производится очень часто, это лучше toobuffer hello журналы и tooreport их все за один раз на обычное время базового (это называется «пакетный режим» hello).

toodo таким образом, необходимо вызвать метод hello:

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

Hello аргумент представляет собой значение в **миллисекунд**. В любое время Если требуется ведение журнала hello в режиме реального времени для tooreactivate просто вызовите метод hello без какого-либо параметра или со значением hello 0.

Hello пакетный режим немного увеличить батареи hello жизни но оказывает влияние на hello монитор Engagement: все сеансы и задания будут скругленными toohello пороговое значение пакетного режима (таким образом, сеансы и задания короче, чем порог повышения hello не могут быть видны). Это рекомендуется toouse Повышение порогового значения больше чем 30000 (30s). Необходимо учитывать, сохраненные журналы являются элементами ограниченный too300 toobe. Если отправка занимает слишком много времени, некоторые журналы могут быть потеряны.

> [!WARNING]
> Порог повышения Hello нельзя настроить период tooa меньше единицы. При попытке toodo таким образом, hello SDK будет отображать трассировку с ошибкой hello и автоматически сбросить значение по умолчанию toohello, т. е. 0. Это приведет к началу hello SDK tooreport hello журналы в режиме реального времени.
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview

