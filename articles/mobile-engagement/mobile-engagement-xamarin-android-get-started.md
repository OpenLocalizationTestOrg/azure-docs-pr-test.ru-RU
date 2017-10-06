---
title: "aaaGet работы с Azure Mobile Engagement для Xamarin.Android"
description: "Узнайте, как toouse Azure Mobile Engagement с аналитики и Push-уведомления для Xamarin.Android приложений."
services: mobile-engagement
documentationcenter: xamarin
author: piyushjo
manager: erikre
editor: 
ms.assetid: fb68cf98-08a2-41b5-8e59-757469de3fe7
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/16/2016
ms.author: piyushjo
ms.openlocfilehash: 9d584fea8e8153d511258cf9b6f87f31dac6aeca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinandroid-apps"></a>Начало работы со Службами мобильного взаимодействия Azure для приложений Xamarin.Android
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

В этом разделе показано, как Azure Mobile Engagement toounderstand toouse использовании веб-приложения и как toosend push-уведомления пользователей toosegmented Xamarin.Android приложения.
В этом учебнике показано hello простой широковещательных сценарий с помощью мобильного охвата. В рассматриваемом сценарии создается пустое приложение Xamarin.Android, которое собирает основные данные и получает push-уведомления с помощью службы Google Cloud Messaging (GCM).

> [!NOTE]
> Служба Azure Mobile Engagement Hello будет прекращено 2018 марта и в настоящее время только доступные tooexisting клиентов. Дополнительные сведения см. на странице [Службы мобильного взаимодействия](https://azure.microsoft.com/en-us/services/mobile-engagement/).

Этот учебник требует hello следующее:

* [Xamarin Studio](http://xamarin.com/studio). Вы также можете использовать Visual Studio с расширением Xamarin, но в этом руководстве используется Xamarin Studio. Инструкции см. в руководстве по [установке и настройке Visual Studio и Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).
* [пакет Xamarin SDK для Служб мобильного взаимодействия](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> toocomplete этого учебника необходимо иметь активную учетную запись Azure. Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут. Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started).
> 
> 

## <a id="setup-azme">
            </a>Настройка Служб мобильного взаимодействия для вашего приложения Android
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Подключение мобильного охвата toohello внутренний сервер приложений
В этом руководстве содержатся «базовой интеграции», который hello минимальный набор данных требуется toocollect и отправить push-уведомление. 

Мы создадим простое приложение с интеграцией hello toodemonstrate Xamarin Studio.

### <a name="create-a-new-xamarinandroid-project"></a>Создание нового проекта Xamarin.Android
1. Запустите **Xamarin Studio** Go слишком**файл** -> **New** -> **решения** 
   
    ![][1]
2. Выберите **приложения Android** убедитесь, что выбран hello язык — **C#** и нажмите кнопку **Далее**.
   
    ![][2]
3. Заполните hello **имя приложения** и hello **идентификатор организации**. Убедитесь, что toocheckmark **службы Google Play** и нажмите кнопку **Далее**. 
   
    ![][3]
4. Обновление hello **имя проекта**, **имя решения** и **расположение** , если требуется и нажмите кнопку **создать**.
   
    ![][4]

Xamarin Studio создаст приложение hello, в котором будет интегрировать мобильного охвата. 

### <a name="connect-your-app-toomobile-engagement-backend"></a>Подключение Engagement tooMobile внутренний сервер приложений
1. Щелкните правой кнопкой мыши hello **пакетов** папки в windows hello решений и выберите **Добавление пакетов...**
   
    ![][5]
2. Поиск hello **Microsoft Azure Mobile Engagement Xamarin SDK** и добавьте его tooyour решения.  
   
    ![][6]
3. Откройте **MainActivity.cs** и добавьте следующее hello операторы using:
   
        using Microsoft.Azure.Engagement;
        using Microsoft.Azure.Engagement.Activity;
4. В hello `OnCreate` метод, добавить следующие tooinitialize hello соединения с внутреннего сервера мобильного охвата hello. Убедитесь, что tooadd вашей **ConnectionString**. 
   
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.ConnectionString = "YourConnectionStringFromAzurePortal";
        EngagementAgent.Init(engagementConfiguration);

### <a name="add-permissions-and-a-service-declaration"></a>Добавление разрешений и объявления службы
1. Откройте hello **Manifest.xml** файл в папке свойства hello. Перейдите на вкладку источника, чтобы непосредственного изменения XML-источник hello.
2. Добавьте эти разрешения toohello Manifest.xml (который можно найти в разделе hello **свойства** папки) проекта непосредственно перед или после hello `<application>` тег:
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
3. Добавьте следующий код hello между hello `<application>` и `</application>` теги toodeclare hello агент службы:
   
        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
4. В коде hello только что вставленного замените `"<Your application name>"` в метке hello. Это отражается в hello **параметры** меню, где пользователи могут видеть службы, работающие на устройстве hello. Можно добавить слово hello «Служба» в этой метке например.

### <a name="send-a-screen-toomobile-engagement"></a>Отправить экрана tooMobile Engagement
В toostart порядок отправки данных и убедитесь, что пользователи hello активны необходимо отправить по крайней мере один внутреннего сервера мобильного охвата toohello экрана. Для этого-убедитесь, что hello `MainActivity` наследует от `EngagementActivity` вместо `Activity`.

    public class MainActivity : EngagementActivity

Если наследование от `EngagementActivity` невозможно, необходимо добавить методы `.StartActivity` и `.EndActivity` в `OnResume` и `OnPause` соответственно.  

        protected override void OnResume()
            {
                EngagementAgent.StartActivity(EngagementAgentUtils.BuildEngagementActivityName(Java.Lang.Class.FromType(this.GetType())), null);
                base.OnResume();             
            }

            protected override void OnPause()
            {
                EngagementAgent.EndActivity();
                base.OnPause();            
            }

## <a id="monitor"></a>Подключение приложения с возможностью его отслеживания в режиме реального времени
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Включение функции отправки и приема push-уведомлений и обмена сообщениями в приложении
Mobile Engagement позволяет вам toointeract с и доступа пользователей с push-уведомления и сообщения в контексте hello кампаний в приложения. Этот модуль вызывается REACH на портале мобильного охвата hello.
Hello в следующих разделах Настройка вашего приложения tooreceive их.

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

<!-- Images -->
[1]: ./media/mobile-engagement-xamarin-android-get-started/1.png
[2]: ./media/mobile-engagement-xamarin-android-get-started/2.png
[3]: ./media/mobile-engagement-xamarin-android-get-started/3.png
[4]: ./media/mobile-engagement-xamarin-android-get-started/4.png
[5]: ./media/mobile-engagement-xamarin-android-get-started/5.png
[6]: ./media/mobile-engagement-xamarin-android-get-started/6.png
