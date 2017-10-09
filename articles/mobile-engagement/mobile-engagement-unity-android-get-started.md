---
title: "aaaGet работы с Azure Mobile Engagement для Unity Android развертывания"
description: "Узнайте, как toouse Azure Mobile Engagement Analytics и Push-уведомления для развертывания устройства tooiOS приложениями Unity."
services: mobile-engagement
documentationcenter: unity
author: piyushjo
manager: erikre
editor: 
ms.assetid: d5f0ef79-be00-4cec-97a5-a0b2fdaa380e
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-unity-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: c4d34691daeb7544b11c2d6895b2474af0f902b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-android-deployment"></a>Приступая к работе со Службами мобильного взаимодействия Azure для развертывания Unity в Android
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

В этом разделе показано, как Azure Mobile Engagement toounderstand toouse использовании веб-приложения и как toosend отправить уведомления пользователей toosegmented приложения Unity, при развертывании tooan устройства Android.
В этом учебнике используется hello классический наката Unity учебник шарик как начальная точка hello. Необходимо выполнить шаги hello в этом [учебника](mobile-engagement-unity-roll-a-ball.md) перед продолжением hello интеграции мобильного охвата, мы демонстрации в учебнике hello ниже. 

Этот учебник требует hello следующее:

* приложение [Unity Editor](http://unity3d.com/get-unity);
* [пакет SDK Unity для Служб мобильного взаимодействия](https://aka.ms/azmeunitysdk)
* пакет SDK для Google Android.

> [!NOTE]
> toocomplete этого учебника необходимо иметь активную учетную запись Azure. Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут. Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started).
> 
> 

## <a id="setup-azme">
            </a>Настройка Служб мобильного взаимодействия для вашего приложения Android
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Подключение мобильного охвата toohello внутренний сервер приложений
### <a name="import-hello-unity-package"></a>Импорт пакета Unity hello
1. Загрузите hello [пакет Mobile Engagement Unity](https://aka.ms/azmeunitysdk) и сохраните его tooyour локального компьютера. 
2. Go слишком**активы -> Импорт пакета -> Настройка пакета** и hello выберите пакет, загруженный в hello выше шаг. 
   
    ![][70] 
3. Убедитесь, что выбраны все файлы, а затем нажмите кнопку **Импорт** . 
   
    ![][71] 
4. Если импорт прошел успешно, вы увидите hello импортировать файлы пакета SDK в своем проекте.  
   
    ![][72] 

### <a name="update-hello-engagementconfiguration"></a>Обновление hello EngagementConfiguration
1. Откройте hello **EngagementConfiguration** файл скрипта из папки и обновление hello hello SDK **ANDROID\_подключения\_строка** со строкой подключения hello полученный ранее из hello портал Azure.  
   
    ![][73]
2. Сохраните файл hello 
3. Щелкните **Файл -> Engagement -> Generate Android Manifest** (Создание манифеста Android). Это hello подключаемый модуль, добавленные hello Mobile Engagement SDK и щелкнув его автоматически обновит параметры проекта. 
   
    ![][74]

> [!IMPORTANT]
> Сделать tooexecute убедиться, что каждый раз при обновлении hello **EngagementConfiguration** файла в противном случае изменения не будут отражены в приложение hello. 
> 
> 

### <a name="configure-hello-app-for-basic-tracking"></a>Настройте приложение hello для отслеживания основных
1. Откройте hello **PlayerController** сценарий присоединен объект toohello проигрывателя для редактирования. 
2. Добавьте следующее hello с помощью инструкции:
   
        using Microsoft.Azure.Engagement.Unity;
3. Добавьте следующие toohello hello `Start()` метод
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-hello-app"></a>Развертывание и запуск приложения hello
Убедитесь, что Android SDK, которые установлены на компьютере, прежде чем toodeploy это устройство tooyour приложения Unity. 

1. Подключение компьютера к устройству Android tooyour. 
2. Откройте **Файл -> Параметры сборки**. 
   
    ![][40]
3. Выберите **Android** и щелкните **Switch Platform** (Переключить платформу).
   
    ![][51]
   
    ![][52]
4. Щелкните **Настройка проигрывателя** и укажите допустимый идентификатор пакета. 
   
    ![][53]
5. Наконец, нажмите кнопку **Сборка и запуск**
   
    ![][54]
6. Возможно, задаваемые tooprovide папки имя toostore hello Android пакета. 
7. Если все пойдет хорошо, hello пакета будет развернутой tooyour подключенных устройств и увидеть игру Unity на телефоне! 

## <a id="monitor"></a>Подключение приложения с возможностью его отслеживания в режиме реального времени
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Включение функции отправки и приема push-уведомлений и обмена сообщениями в приложении
[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

### <a name="update-hello-engagementconfiguration"></a>Обновление hello EngagementConfiguration
1. Откройте hello **EngagementConfiguration** файл скрипта из папки и обновление hello hello SDK **ANDROID\_GOOGLE\_номер** с hello **проекта Google Номер** полученный ранее из портала разработчиков облачных Google hello. Это строковое значение, поэтому следует убедиться, что tooenclose его в двойные кавычки. 
   
    ![][75]
2. Сохраните файл hello. 
3. Щелкните **Файл -> Engagement -> Generate Android Manifest** (Создание манифеста Android). Это hello подключаемый модуль, добавленные hello Mobile Engagement SDK и щелкнув его автоматически обновит параметры проекта. 
   
    ![][74]

### <a name="configure-hello-app-tooreceive-notifications"></a>Настройка уведомлений tooreceive приложения hello
1. Откройте hello **PlayerController** сценарий присоединен объект toohello проигрывателя для редактирования. 
2. Добавьте следующие toohello hello `Start()` метод
   
        EngagementReachAgent.Initialize();
3. Теперь, когда hello приложение обновляется, разверните и запустите приложение hello на устройстве на hello, приведенным ниже. 

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

<!-- Images -->
[40]: ./media/mobile-engagement-unity-android-get-started/40.png
[70]: ./media/mobile-engagement-unity-android-get-started/70.png
[71]: ./media/mobile-engagement-unity-android-get-started/71.png
[72]: ./media/mobile-engagement-unity-android-get-started/72.png
[73]: ./media/mobile-engagement-unity-android-get-started/73.png
[74]: ./media/mobile-engagement-unity-android-get-started/74.png
[75]: ./media/mobile-engagement-unity-android-get-started/75.png
[51]: ./media/mobile-engagement-unity-android-get-started/51.png
[52]: ./media/mobile-engagement-unity-android-get-started/52.png
[53]: ./media/mobile-engagement-unity-android-get-started/53.png
[54]: ./media/mobile-engagement-unity-android-get-started/54.png
