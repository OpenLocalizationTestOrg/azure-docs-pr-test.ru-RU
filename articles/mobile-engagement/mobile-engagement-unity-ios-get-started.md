---
title: "aaaGet работы с Azure Mobile Engagement для развертывания iOS Unity"
description: "Узнайте, как toouse Azure Mobile Engagement Analytics и Push-уведомления для развертывания устройства tooiOS приложениями Unity."
services: mobile-engagement
documentationcenter: unity
author: piyushjo
manager: erikre
editor: 
ms.assetid: 7ddfbac3-8d13-4ebe-b061-c865f357297f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-unity-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: f4247b0a9240cbe2bf1a6618388919d3554c07fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-ios-deployment"></a>Приступая к работе со Службами мобильного взаимодействия Azure для развертывания Unity в iOS
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

В этом разделе показано, как Azure Mobile Engagement toounderstand toouse использовании веб-приложения и как toosend отправить уведомления пользователей toosegmented приложения Unity, при развертывании tooan устройства iOS.
В этом учебнике используется hello классический наката Unity учебник шарик как начальная точка hello. Необходимо выполнить шаги hello в этом [учебника](mobile-engagement-unity-roll-a-ball.md) перед продолжением hello интеграции мобильного охвата, мы демонстрации в учебнике hello ниже. 

Этот учебник требует hello следующее:

* приложение [Unity Editor](http://unity3d.com/get-unity);
* [пакет SDK Unity для Служб мобильного взаимодействия](https://aka.ms/azmeunitysdk)
* редактор XCode.

> [!NOTE]
> toocomplete этого учебника необходимо иметь активную учетную запись Azure. Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут. Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started).
> 
> 

## <a id="setup-azme">
            </a>Настройка Служб мобильного взаимодействия для вашего приложения iOS
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
1. Откройте hello **EngagementConfiguration** файл скрипта из папки и обновление hello hello SDK **IOS\_подключения\_строка** со строкой подключения hello, полученного ранее из hello портал Azure.  
   
    ![][73]
2. Сохраните файл hello. 

### <a name="configure-hello-app-for-basic-tracking"></a>Настройте приложение hello для отслеживания основных
1. Откройте hello **PlayerController** сценарий присоединен объект toohello проигрывателя для редактирования. 
2. Добавьте следующее hello с помощью инструкции:
   
        using Microsoft.Azure.Engagement.Unity;
3. Добавьте следующие toohello hello `Start()` метод
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-hello-app"></a>Развертывание и запуск приложения hello
1. Подключите машину tooyour устройства iOS. 
2. Откройте **Файл -> Параметры сборки**. 
   
    ![][40]
3. Выберите **iOS** и щелкните **Переключить платформу**.
   
    ![][41]
   
    ![][42]
4. Щелкните **Настройка проигрывателя** и укажите допустимый идентификатор пакета. 
   
    ![][53]
5. Наконец, нажмите кнопку **Сборка и запуск**
   
    ![][54]
6. Возможно, задаваемые tooprovide пакета iOS hello toostore имя папки. 
   
    ![][43]
7. Если все пойдет хорошо, будет выполнена компиляция проекта hello, и следует открыть его на работу приложения в XCode. 
8. Убедитесь в том, что hello **идентификатор пакета** правильно в проекте hello.  
   
    ![][75]
9. Теперь запустите приложение hello в XCode, чтобы пакет hello развернутой tooyour подключенном устройстве, а на телефоне должна появиться игру Unity! 

## <a id="monitor"></a>Подключение приложения с возможностью его отслеживания в режиме реального времени
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Включение функции отправки и приема push-уведомлений и обмена сообщениями в приложении
Mobile Engagement позволяет toointeract со своими пользователями и получить доступ с push-уведомления и сообщения в контексте hello кампаний в приложения. Этот модуль вызывается REACH на портале мобильного охвата hello.
Не нужно toodo какой-либо дополнительной настройки уведомлений tooreceive вашего приложения, и он уже настроен для него.

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- Images. -->
[40]: ./media/mobile-engagement-unity-ios-get-started/40.png
[41]: ./media/mobile-engagement-unity-ios-get-started/41.png
[42]: ./media/mobile-engagement-unity-ios-get-started/42.png
[43]: ./media/mobile-engagement-unity-ios-get-started/43.png
[53]: ./media/mobile-engagement-unity-ios-get-started/53.png
[54]: ./media/mobile-engagement-unity-ios-get-started/54.png
[70]: ./media/mobile-engagement-unity-ios-get-started/70.png
[71]: ./media/mobile-engagement-unity-ios-get-started/71.png
[72]: ./media/mobile-engagement-unity-ios-get-started/72.png
[73]: ./media/mobile-engagement-unity-ios-get-started/73.png
[74]: ./media/mobile-engagement-unity-ios-get-started/74.png
[75]: ./media/mobile-engagement-unity-ios-get-started/75.png
