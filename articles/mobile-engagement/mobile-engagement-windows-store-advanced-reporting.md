---
title: "aaaWindows универсальной дополнительные отчеты с MobileApps Engagement"
description: "Как tooIntegrate Azure Mobile Engagement с универсальные приложения Windows"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: ea5030bf-73ac-49b7-bc3e-c25fc10e945a
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 20968f238ef7ae9dc0b8bb6dac3fb8bdb9bc3a10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-reporting-with-hello-windows-universal-apps-engagement-sdk"></a>Дополнительных отчетов с помощью пакета SDK Engagement универсальных приложений Windows hello
> [!div class="op_single_selector"]
> * [Универсальная платформа Windows](mobile-engagement-windows-store-advanced-reporting.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-advanced-reporting.md)
> 
> 

В этом разделе описаны дополнительные сценарии создания отчетов в универсальном приложении для Windows. К таким сценариям относятся параметры, которые вы можете tooapply toohello приложения, созданного в hello [Приступая к работе](mobile-engagement-windows-store-dotnet-get-started.md) учебника.

## <a name="prerequisites"></a>Предварительные требования
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

Перед запуском этого учебника, необходимо сначала выполнить hello [Приступая к работе](mobile-engagement-windows-store-dotnet-get-started.md) руководство, в котором намеренно прямой и простой. В этом учебнике рассматриваются дополнительные параметры, доступные для выбора.

## <a name="specifying-engagement-configuration-at-runtime"></a>Указание конфигурации Engagement во время выполнения
централизованный Hello проектной конфигурации в hello `Resources\EngagementConfiguration.xml` файл проекта, где он был задан в hello [Приступая к работе](mobile-engagement-windows-store-dotnet-get-started.md) раздела.

Но также можно указать во время выполнения: вы можете вызвать следующий метод до инициализации агента Engagement hello hello:

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set hello Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);



## <a name="recommended-method-overload-your-page-classes"></a>Рекомендуемый метод: перегрузка классов `Page`
tooactivate hello reporting всех журналов hello, необходимых в Engagement toocompute пользователей, сеансы, действия, сбои и технические данные, внести все вашей `Page` вложенные классы наследуют от hello `EngagementPage` классы.

Ниже приведен пример страницы приложения. Можно сделать hello одинаково для всех страниц приложения.

### <a name="c-source-file"></a>Исходный файл на C#
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
> Если на странице переопределяет hello `OnNavigatedTo` метода будет убедиться, что toocall `base.OnNavigatedTo(e)`. В противном случае действие hello не будут отображаться (hello `EngagementPage` вызовы `StartActivity` внутри его `OnNavigatedTo` метода).
> 
> 

### <a name="xaml-file"></a>XAML-файл
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

### <a name="override-hello-default-behaviour"></a>Переопределение поведения по умолчанию hello
По умолчанию имя класса hello страницы приветствия отображается как имя действия hello с без дополнительных. Если класс hello использует hello суффикс «Страница», Engagement удаляет его.

поведение по умолчанию hello toooverride имени hello, добавьте следующий код:

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

tooreport дополнительных сведений с действием, добавьте следующий код:

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

Эти методы вызываются из внутри hello `OnNavigatedTo` метод страницы.

### <a name="alternate-method-call-startactivity-manually"></a>Альтернативный метод: вызов `StartActivity()` вручную
Если невозможно или нежелательно toooverload вашей `Page` классы, вместо этого можно запустить ваши действия путем вызова `EngagementAgent` методы напрямую.

Рекомендуем вызывать `StartActivity` внутри метода `OnNavigatedTo` своей страницы.

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> Убедитесь, что сеанс завершен правильно.
> 
> пакет SDK для Universal Windows Hello автоматически вызывает hello `EndActivity` метод при закрытии приложения hello. Таким образом, **высокой** рекомендуется toocall hello `StartActivity` метод изменении hello действий пользователя hello и слишком**никогда** hello вызовов `EndActivity` метод. Этот метод уведомляет сервер занят hello что hello текущий пользователь покинул приложения hello, что повлияет на все журналы приложений.
> 
> 

## <a name="advanced-reporting"></a>Расширенные отчеты
При необходимости вы можете tooreport события конкретного приложения, ошибок и задания, toodo таким образом, использование hello другие методы найдены в hello `EngagementAgent` класса. Hello Engagement API позволяет использовать расширенные возможности всех обязательств.

Дополнительные сведения см. в разделе [как toouse hello дополнительные теги API в приложении универсальное приложение для Windows Mobile Engagement](mobile-engagement-windows-store-use-engagement-api.md).

