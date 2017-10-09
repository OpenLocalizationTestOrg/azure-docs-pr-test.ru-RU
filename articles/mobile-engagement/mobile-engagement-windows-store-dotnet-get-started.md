---
title: "aaaGet к работе с Windows универсальных приложений Azure Mobile Engagement"
description: "Узнайте, как toouse Azure Mobile Engagement с анализа и отправка уведомлений для универсальных приложений Windows."
services: mobile-engagement
documentationcenter: windows
author: piyushjo
manager: erikre
editor: 
ms.assetid: 48103867-7f64-4646-b019-42bd797d38e2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 8224a6d3789cfe4784bbc9472005f9eddb94a8b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-universal-apps"></a>Приступая к работе со Службами мобильного взаимодействия Azure для универсальных приложений для Windows
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

В этом разделе показано, как Azure Mobile Engagement toounderstand toouse использования приложений и отправлять push-уведомления пользователей toosegmented универсальное приложение для Windows приложения.
В этом учебнике показано hello простой широковещательных сценарий с помощью мобильного охвата. Вы создадите пустое универсальное приложение для Windows, которое будет собирать основные данные об использовании приложений и получать push-уведомления, используя службу push-уведомлений Windows (WNS).

> [!NOTE]
> Служба Azure Mobile Engagement Hello будет прекращено 2018 марта и в настоящее время только доступные tooexisting клиентов. Дополнительные сведения см. на странице [Службы мобильного взаимодействия](https://azure.microsoft.com/en-us/services/mobile-engagement/).

## <a name="prerequisites"></a>Предварительные требования
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="set-up-mobile-engagement-for-your-windows-universal-app"></a>Настройка Служб мобильного взаимодействия для универсального приложения для Windows
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Подключение мобильного охвата toohello внутренний сервер приложений
В этом руководстве содержатся «базовой интеграции служб, «hello минимальный набор данных требуется toocollect и отправить push-уведомление. Hello полной интеграции документацию можно найти в hello [интеграции Windows Mobile Engagement SDK универсальной](mobile-engagement-windows-store-sdk-overview.md).

Создать простое приложение с помощью Visual Studio toodemonstrate hello интеграции.

### <a name="create-a-windows-universal-app-project"></a>Создание проекта универсального приложения для Windows
Hello следующие шаги предполагают использование Visual Studio 2015 hello хотя hello действия схожи в более ранних версиях Visual Studio.

1. Запустите Visual Studio и в hello **Главная** выберите **новый проект**.
2. Во всплывающем hello выберите **Windows** -> **универсальной** -> **пустое приложение (универсальные приложения Windows)**. Заполните приложение hello **имя** и **имя решения**, а затем нажмите кнопку **ОК**.

    ![][1]

Вы создали проект универсального приложения Windows, в которую затем интегрировать hello Azure Mobile Engagement SDK.

### <a name="connect-your-app-toomobile-engagement-backend"></a>Подключение Engagement tooMobile внутренний сервер приложений
1. Установка hello [MicrosoftAzure.MobileEngagement] пакета Nuget в проекте. Если вы используете платформ Windows и Windows Phone, toodo это необходимо для обоих проектов. Для Windows 8.x и Windows Phone 8.1, hello те же Nuget пакета местах hello правильный платформой двоичные файлы в каждом проекте.
2. Откройте **Package.appxmanifest** и убедитесь, что существует добавлено, hello следующие возможности:

        Internet (Client)

    ![][2]
3. Теперь скопируйте строку подключения hello, скопированное ранее для приложения Mobile Engagement и вставьте его в hello `Resources\EngagementConfiguration.xml` файла между hello `<connectionString>` и `</connectionString>` теги:

    ![][3]

    > [!TIP]
    > Если приложение рассчитано как на платформу Windows, так и на Windows Phone, то следует создать два приложения Служб мобильного взаимодействия (по одному для каждой из поддерживаемых платформ). Наличие двух приложений обеспечивает можно создать правильный сегментации hello аудитории и может отправлять соответствующие целевые уведомления для каждой платформы.

    > [!IMPORTANT]
    > NuGet не копирует автоматически ресурсов SDK hello в приложении Windows 10 UWP. У вас есть toodo его вручную после hello шаги, которые отображаются при установке пакета Nuget hello (readme.txt).  

1. В hello `App.xaml.cs` файла:

    а. Добавить hello `using` инструкции:

            using Microsoft.Azure.Engagement;

    b. Добавьте метод, который инициализирует hello участия:

           private void InitEngagement(IActivatedEventArgs e)
           {
             EngagementAgent.Instance.Init(e);

             //... rest of hello code
           }

    c. Инициализировать hello SDK в hello **OnLaunched** метод:

            protected override void OnLaunched(LaunchActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of hello code
            }

    c. Вставьте следующие hello в hello **OnActivated** метода и добавьте метод hello в том случае, если он еще не:

            protected override void OnActivated(IActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of hello code
            }

## <a id="monitor"></a>Включение мониторинга в режиме реального времени
toostart отправляет данные и обеспечить hello пользователей активны, необходимо отправить по крайней мере один внутреннего сервера мобильного охвата toohello экрана (действие).

1. В hello **MainPage.xaml.cs**, добавьте следующее hello `using` инструкции:

    с помощью Microsoft.Azure.Engagement.Overlay.
2. Измените базовый класс hello объекта **MainPage** из **страницы** слишком**EngagementPageOverlay**:

        class MainPage : EngagementPageOverlay
3. В hello `MainPage.xaml` файла:

    а. Добавьте tooyour объявления пространств имен:

        xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"

    b. Замените hello **страницы** в имени XML-тега hello с **engagement: EngagementPageOverlay**

> [!IMPORTANT]
> Если на странице переопределяет hello `OnNavigatedTo` метода будет убедиться, что toocall `base.OnNavigatedTo(e)`. В противном случае hello не выводятся `EngagementPage` вызовы `StartActivity` внутри его `OnNavigatedTo` метода). Это особенно важно в проекте Windows Phone, где есть шаблон по умолчанию hello `OnNavigatedTo` метод.
>
> Для **универсальных приложений Windows 10**, метод hello в hello рекомендуется использовать» рекомендуется использовать метод: перегружать классов страницы «раздел [Advanced отчетов с помощью пакета SDK Engagement универсальных приложений Windows hello](mobile-engagement-windows-store-advanced-reporting.md) , вместо того чтобы hello упомянутым выше.

## <a id="monitor"></a>Подключение приложения с возможностью его отслеживания в режиме реального времени
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Включение функции отправки и приема push-уведомлений и обмена сообщениями в приложении
Mobile Engagement позволяет вам toointeract и доступа пользователей с push-уведомления и сообщения в контексте hello кампаний в приложения. Этот модуль вызывается REACH на портале мобильного охвата hello.
Hello следующих разделах Настройка вашего приложения tooreceive их.

### <a name="enable-your-app-tooreceive-wns-push-notifications"></a>Включить вашего приложения tooreceive Push-уведомления WNS
1. В hello `Package.appxmanifest` файла в hello **приложения** в разделе **уведомления**, задайте **всплывающие уведомления:** слишком**Да**

    ![][5]

### <a name="initialize-hello-reach-sdk"></a>Инициализировать hello пакет SDK для REACH
В `App.xaml.cs`, вызовите **EngagementReach.Instance.Init(e);** в hello **InitEngagement** функция сразу же после инициализации агента hello:

        private void InitEngagement(IActivatedEventArgs e)
        {
           EngagementAgent.Instance.Init(e);
           EngagementReach.Instance.Init(e);
        }

Теперь вы готовы toosend всплывающее уведомление. Теперь убедимся, что базовая интеграция выполнена правильно.

### <a name="grant-access-toomobile-engagement-toosend-notifications"></a>Предоставление доступа к tooMobile Engagement toosend уведомления
1. Откройте в веб-браузере [Центр разработки Магазина Windows] , войдите и при необходимости создайте учетную запись.
2. Нажмите кнопку **мониторинга** справа вверху hello углу, а затем нажмите кнопку **создайте новое приложение** hello левой панели меню.

    ![][9]
3. Создайте приложение, резервируя его имя.

    ![][10]
4. После создания приложения hello перейдите слишком**службы -> Push-уведомления** из меню слева hello.

    ![][11]
5. В hello Push-уведомления, нажмите кнопку hello **узла службы Live** ссылку.

    ![][12]
6. Переместитесь раздел учетных данных toohello Push. Убедитесь, что вы находитесь в hello **параметры приложения** статьи и скопируйте вашей **ИД безопасности пакета** и **секрет клиента**

    ![][13]
7. Перейдите toohello **параметры** из порталу мобильного охвата и нажмите кнопку hello **системные Push-уведомления** раздел слева hello. Нажмите кнопку hello **изменить** tooenter кнопку вашей **пакета идентификатор безопасности (SID)** и **секретный ключ** как показано:

    ![][6]
8. Наконец убедитесь, что с помощью этого приложения, созданного в магазине приложений hello связаны приложения Visual Studio. В Visual Studio щелкните **Associate App with Store** (Связать приложение с магазином).

    ![][7]

## <a id="send"></a>Отправить уведомление о tooyour приложение
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

Если приложение hello работает, может появиться уведомление в приложении. в противном случае приложение hello закрыт, вы увидите всплывающее уведомление.
Если вы видите уведомление в приложении, но не всплывающее уведомление и выполнении приложение hello в режиме отладки в Visual Studio, затем повторите **события жизненного цикла -> Suspend** в tooensure инструментов hello приостанавливается, приложение hello. Если была нажата кнопка домашней hello во время отладки приложения hello в Visual Studio, затем он не всегда была приостановлена и во время уведомления hello вы увидите, как в приложении, он не отображается в виде всплывающих уведомлений.  

![][8]

<!-- URLs. -->
[Mobile Engagement Windows Universal SDK documentation]: ../mobile-engagement-windows-store-integrate-engagement/
[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9864592
[Центр разработки Магазина Windows]: https://dev.windows.com
[Windows Universal Apps - Overlay integration]: ../mobile-engagement-windows-store-integrate-engagement-reach/#overlay-integration

<!-- Images. -->
[1]: ./media/mobile-engagement-windows-store-dotnet-get-started/universal-app-creation.png
[2]: ./media/mobile-engagement-windows-store-dotnet-get-started/manifest-capabilities.png
[3]: ./media/mobile-engagement-windows-store-dotnet-get-started/add-connection-info.png
[5]: ./media/mobile-engagement-windows-store-dotnet-get-started/manifest-toast.png
[6]: ./media/mobile-engagement-windows-store-dotnet-get-started/enter-credentials.png
[7]: ./media/mobile-engagement-windows-store-dotnet-get-started/associate-app-store.png
[8]: ./media/mobile-engagement-windows-store-dotnet-get-started/vs-suspend.png
[9]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_create_app.png
[10]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_app_name.png
[11]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push.png
[12]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push_1.png
[13]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push_creds.png
