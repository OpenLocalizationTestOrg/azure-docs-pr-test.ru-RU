---
title: "aaaGet работы с приложениями Azure Mobile Engagement для Windows Phone Silverlight"
description: "Узнайте, как toouse Azure Mobile Engagement с анализа и отправка уведомления для приложения Windows Phone Silverlight."
services: mobile-engagement
documentationcenter: windows
author: piyushjo
manager: erikre
editor: 
ms.assetid: aa34692f-87f7-47c6-a20c-a1972750bc25
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: b39a838ab03217b2dc845cbf59d7bf8b094dac1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-phone-silverlight-apps"></a>Приступая к работе со Службами мобильного взаимодействия Azure для приложений Windows Phone Silverlight
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

В этом разделе показано, как Azure Mobile Engagement toounderstand toouse использования приложений и отправлять push-уведомления пользователей toosegmented приложения Windows Phone Silverlight.
В этом учебнике показано hello простой широковещательных сценарий с помощью мобильного охвата. Здесь вы создадите пустое приложение Windows Phone Silverlight, которое будет собирать основные данные и получать push-уведомления, используя службу push-уведомлений (Майкрософт) (MPNS).

> [!NOTE]
> Служба Azure Mobile Engagement Hello будет прекращено 2018 марта и в настоящее время только доступные tooexisting клиентов. Дополнительные сведения см. на странице [Службы мобильного взаимодействия](https://azure.microsoft.com/en-us/services/mobile-engagement/).

> [!NOTE]
> Проекты для версии Windows Phone 8.1 и более ранних версий не поддерживаются в Visual Studio 2017.  Дополнительные сведения см. в статье [Целевая платформа и совместимость для Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).

> [!NOTE]
> Если вы используете Windows Phone 8.1 (отличных от Silverlight), см. toohello [Windows Universal учебника](mobile-engagement-windows-store-dotnet-get-started.md).
> 
> 

Этот учебник требует hello следующее:

* Visual Studio 2013
* [MicrosoftAzure.MobileEngagement] 

> [!NOTE]
> toocomplete этого учебника необходимо иметь активную учетную запись Azure. Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут. Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-windows-phone-get-started).
> 
> 

## <a id="setup-azme">
            </a>Настройка Служб мобильного взаимодействия для приложения Windows Phone
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Подключение мобильного охвата toohello внутренний сервер приложений
В этом руководстве содержатся «базовой интеграции», который hello минимальный набор данных требуется toocollect и отправить push-уведомление. Hello полной интеграции документацию можно найти в hello [интеграции пакета SDK для Windows Phone Mobile Engagement](mobile-engagement-windows-phone-sdk-overview.md)

Мы создадим простое приложение с помощью Visual Studio toodemonstrate hello интеграции.

### <a name="create-a-new-windows-phone-silverlight-project"></a>Создание проекта для Windows Phone Silverlight
Hello следующие шаги предполагают использование Visual Studio 2015 hello хотя hello действия схожи в более ранних версиях Visual Studio. 

1. Запустите Visual Studio и в hello **Главная** выберите **новый проект**.
2. Во всплывающем hello выберите **Windows 8** -> **Windows Phone** -> **пустое приложение (Windows Phone Silverlight)**. Заполните приложение hello **имя** и **имя решения**, а затем нажмите кнопку **ОК**.
   
    ![][1]
3. Можно выбрать либо tootarget **Windows Phone 8.0** или **Windows Phone 8.1**.

Вы создали нового приложения Windows Phone Silverlight, в которую будет интегрировать hello Azure Mobile Engagement SDK.

### <a name="connect-your-app-toohello-mobile-engagement-backend"></a>Подключение мобильного охвата toohello внутренний сервер приложений
1. Установка hello [MicrosoftAzure.MobileEngagement] пакета nuget в проекте.
2. Откройте `WMAppManifest.xml` (папке hello свойства) и убедитесь, что объявлены следующие hello (добавить их, если они не являются) в hello `<Capabilities />` тег:
   
        <Capability Name="ID_CAP_NETWORKING" />
        <Capability Name="ID_CAP_IDENTITY_DEVICE" />
   
    ![][2]
3. Теперь вставьте строку подключения hello, скопированное ранее для приложения Mobile Engagement и вставьте его в hello `Resources\EngagementConfiguration.xml` файла между hello `<connectionString>` и `</connectionString>` теги:
   
    ![][3]
4. В hello `App.xaml.cs` файла:
   
    а. Добавить hello `using` инструкции:
   
            using Microsoft.Azure.Engagement;
   
    b. Инициализировать hello SDK в hello `Application_Launching` метод:
   
            private void Application_Launching(object sender, LaunchingEventArgs e)
            {
              EngagementAgent.Instance.Init();
            }
   
    c. Вставьте следующие hello в hello `Application_Activated`:
   
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
               EngagementAgent.Instance.OnActivated(e);
            }

## <a id="monitor"></a>Включение мониторинга в режиме реального времени
В toostart порядок отправки данных и убедитесь, что пользователи hello active необходимо отправить по крайней мере один внутреннего сервера мобильного охвата toohello экрана (действие).

1. Добавьте в hello MainPage.xaml.cs hello `using` инструкции:
   
        using Microsoft.Azure.Engagement;
2. Замените hello базовый класс **MainPage**, который предшествует **PhoneApplicationPage**, с **EngagementPage**.
   
        class MainPage : EngagementPage 
3. В файле `MainPage.xml`:
   
    а. Добавьте tooyour объявления пространств имен:
   
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
   
    b. Замените `phone:PhoneApplicationPage` в имени XML-тега hello с `engagement:EngagementPage`.

## <a id="monitor"></a>Подключение приложения с возможностью его отслеживания в режиме реального времени
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Включение функции отправки и приема push-уведомлений и обмена сообщениями в приложении
Mobile Engagement позволяет вам toointeract и доступа пользователей с Push-уведомления и обмен сообщениями в приложении в контексте hello кампаний. Этот модуль вызывается REACH на портале мобильного охвата hello.
Hello следующих разделах Настройка вашего приложения tooreceive их.

### <a name="enable-your-app-tooreceive-mpns-push-notifications"></a>Включить вашего приложения tooreceive Push-уведомления MPNS
Добавить новые возможности tooyour `WMAppManifest.xml` файла:

        ID_CAP_PUSH_NOTIFICATION
        ID_CAP_WEBBROWSERCOMPONENT

   ![][5]

### <a name="initialize-hello-reach-sdk"></a>Инициализировать hello пакет SDK для REACH
1. В `App.xaml.cs`, вызовите `EngagementReach.Instance.Init();` в hello **Application_Launching** функция сразу же после инициализации агента hello:
   
        private void Application_Launching(object sender, LaunchingEventArgs e)
        {
           EngagementAgent.Instance.Init();
           EngagementReach.Instance.Init();
        }
2. В `App.xaml.cs`, вызовите `EngagementReach.Instance.OnActivated(e);` в hello **Application_Activated** функция сразу же после инициализации агента hello:
   
        private void Application_Activated(object sender, ActivatedEventArgs e)
        {
           EngagementAgent.Instance.OnActivated(e);
           EngagementReach.Instance.OnActivated(e);
        }

Все готово. Теперь убедимся, что базовая интеграция выполнена правильно.

## <a id="send"></a>Отправить уведомление о tooyour приложение
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

Вы увидите уведомление на вашем устройстве, на котором будут отображаться как уведомление в приложении Если приложение hello еще открыт, в противном случае значение в виде всплывающих уведомлений hello следующим образом: 

![][6]

<!-- URLs. -->
[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9874664
[Mobile Engagement Windows Phone SDK documentation]: ../mobile-engagement-windows-phone-integrate-engagement/

<!-- Images. -->
[1]: ./media/mobile-engagement-windows-phone-get-started/project-properties.png
[2]: ./media/mobile-engagement-windows-phone-get-started/wmappmanifest-capabilities.png
[3]: ./media/mobile-engagement-windows-phone-get-started/add-connection-string.png
[5]: ./media/mobile-engagement-windows-phone-get-started/reach-capabilities.png
[6]: ./media/mobile-engagement-windows-phone-get-started/push-screenshot.png
