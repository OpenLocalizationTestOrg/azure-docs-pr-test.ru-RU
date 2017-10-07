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
# <a name="get-started-with-azure-mobile-engagement-for-unity-ios-deployment"></a><span data-ttu-id="8b3c7-103">Приступая к работе со Службами мобильного взаимодействия Azure для развертывания Unity в iOS</span><span class="sxs-lookup"><span data-stu-id="8b3c7-103">Get Started with Azure Mobile Engagement for Unity iOS deployment</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="8b3c7-104">В этом разделе показано, как Azure Mobile Engagement toounderstand toouse использовании веб-приложения и как toosend отправить уведомления пользователей toosegmented приложения Unity, при развертывании tooan устройства iOS.</span><span class="sxs-lookup"><span data-stu-id="8b3c7-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and how toosend push notifications toosegmented users of a Unity application when deploying tooan iOS device.</span></span>
<span data-ttu-id="8b3c7-105">В этом учебнике используется hello классический наката Unity учебник шарик как начальная точка hello.</span><span class="sxs-lookup"><span data-stu-id="8b3c7-105">This tutorial uses hello classic Unity Roll a Ball tutorial as hello starting point.</span></span> <span data-ttu-id="8b3c7-106">Необходимо выполнить шаги hello в этом [учебника](mobile-engagement-unity-roll-a-ball.md) перед продолжением hello интеграции мобильного охвата, мы демонстрации в учебнике hello ниже.</span><span class="sxs-lookup"><span data-stu-id="8b3c7-106">You should follow hello steps in this [tutorial](mobile-engagement-unity-roll-a-ball.md) before proceeding with hello Mobile Engagement integration we showcase in hello tutorial below.</span></span> 

<span data-ttu-id="8b3c7-107">Этот учебник требует hello следующее:</span><span class="sxs-lookup"><span data-stu-id="8b3c7-107">This tutorial requires hello following:</span></span>

* <span data-ttu-id="8b3c7-108">приложение [Unity Editor](http://unity3d.com/get-unity);</span><span class="sxs-lookup"><span data-stu-id="8b3c7-108">[Unity Editor](http://unity3d.com/get-unity)</span></span>
* [<span data-ttu-id="8b3c7-109">пакет SDK Unity для Служб мобильного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="8b3c7-109">Mobile Engagement Unity SDK</span></span>](https://aka.ms/azmeunitysdk)
* <span data-ttu-id="8b3c7-110">редактор XCode.</span><span class="sxs-lookup"><span data-stu-id="8b3c7-110">XCode Editor</span></span>

> [!NOTE]
> <span data-ttu-id="8b3c7-111">toocomplete этого учебника необходимо иметь активную учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="8b3c7-111">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="8b3c7-112">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="8b3c7-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="8b3c7-113">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="8b3c7-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started).</span></span>
> 
> 

## <span data-ttu-id="8b3c7-114"><a id="setup-azme">
            </a>Настройка Служб мобильного взаимодействия для вашего приложения iOS</span><span class="sxs-lookup"><span data-stu-id="8b3c7-114"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="8b3c7-115"><a id="connecting-app"></a>Подключение мобильного охвата toohello внутренний сервер приложений</span><span class="sxs-lookup"><span data-stu-id="8b3c7-115"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
### <a name="import-hello-unity-package"></a><span data-ttu-id="8b3c7-116">Импорт пакета Unity hello</span><span class="sxs-lookup"><span data-stu-id="8b3c7-116">Import hello Unity package</span></span>
1. <span data-ttu-id="8b3c7-117">Загрузите hello [пакет Mobile Engagement Unity](https://aka.ms/azmeunitysdk) и сохраните его tooyour локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="8b3c7-117">Download hello [Mobile Engagement Unity package](https://aka.ms/azmeunitysdk) and save it tooyour local machine.</span></span> 
2. <span data-ttu-id="8b3c7-118">Go слишком**активы -> Импорт пакета -> Настройка пакета** и hello выберите пакет, загруженный в hello выше шаг.</span><span class="sxs-lookup"><span data-stu-id="8b3c7-118">Go too**Assets -> Import Package -> Custom Package** and select hello package you downloaded in hello above step.</span></span> 
   
    ![][70] 
3. <span data-ttu-id="8b3c7-119">Убедитесь, что выбраны все файлы, а затем нажмите кнопку **Импорт** .</span><span class="sxs-lookup"><span data-stu-id="8b3c7-119">Make sure all files are selected and click **Import** button.</span></span> 
   
    ![][71] 
4. <span data-ttu-id="8b3c7-120">Если импорт прошел успешно, вы увидите hello импортировать файлы пакета SDK в своем проекте.</span><span class="sxs-lookup"><span data-stu-id="8b3c7-120">Once Import is successful, you will see hello imported SDK files in your project.</span></span>  
   
    ![][72] 

### <a name="update-hello-engagementconfiguration"></a><span data-ttu-id="8b3c7-121">Обновление hello EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="8b3c7-121">Update hello EngagementConfiguration</span></span>
1. <span data-ttu-id="8b3c7-122">Откройте hello **EngagementConfiguration** файл скрипта из папки и обновление hello hello SDK **IOS\_подключения\_строка** со строкой подключения hello, полученного ранее из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8b3c7-122">Open up hello **EngagementConfiguration** script file from hello SDK folder and update hello **IOS\_CONNECTION\_STRING** with hello connection string you obtained earlier from hello Azure portal.</span></span>  
   
    ![][73]
2. <span data-ttu-id="8b3c7-123">Сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="8b3c7-123">Save hello file.</span></span> 

### <a name="configure-hello-app-for-basic-tracking"></a><span data-ttu-id="8b3c7-124">Настройте приложение hello для отслеживания основных</span><span class="sxs-lookup"><span data-stu-id="8b3c7-124">Configure hello app for basic tracking</span></span>
1. <span data-ttu-id="8b3c7-125">Откройте hello **PlayerController** сценарий присоединен объект toohello проигрывателя для редактирования.</span><span class="sxs-lookup"><span data-stu-id="8b3c7-125">Open up hello **PlayerController** script attached toohello Player object for editing.</span></span> 
2. <span data-ttu-id="8b3c7-126">Добавьте следующее hello с помощью инструкции:</span><span class="sxs-lookup"><span data-stu-id="8b3c7-126">Add hello following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Unity;
3. <span data-ttu-id="8b3c7-127">Добавьте следующие toohello hello `Start()` метод</span><span class="sxs-lookup"><span data-stu-id="8b3c7-127">Add hello following toohello `Start()` method</span></span>
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-hello-app"></a><span data-ttu-id="8b3c7-128">Развертывание и запуск приложения hello</span><span class="sxs-lookup"><span data-stu-id="8b3c7-128">Deploy and run hello app</span></span>
1. <span data-ttu-id="8b3c7-129">Подключите машину tooyour устройства iOS.</span><span class="sxs-lookup"><span data-stu-id="8b3c7-129">Connect an iOS device tooyour machine.</span></span> 
2. <span data-ttu-id="8b3c7-130">Откройте **Файл -> Параметры сборки**.</span><span class="sxs-lookup"><span data-stu-id="8b3c7-130">Open up **File -> Build Settings**</span></span> 
   
    ![][40]
3. <span data-ttu-id="8b3c7-131">Выберите **iOS** и щелкните **Переключить платформу**.</span><span class="sxs-lookup"><span data-stu-id="8b3c7-131">Select **iOS** and then click on **Switch Platform**</span></span>
   
    ![][41]
   
    ![][42]
4. <span data-ttu-id="8b3c7-132">Щелкните **Настройка проигрывателя** и укажите допустимый идентификатор пакета.</span><span class="sxs-lookup"><span data-stu-id="8b3c7-132">Click on **Player settings** and provide a valid Bundle Identifier.</span></span> 
   
    ![][53]
5. <span data-ttu-id="8b3c7-133">Наконец, нажмите кнопку **Сборка и запуск**</span><span class="sxs-lookup"><span data-stu-id="8b3c7-133">Finally click on **Build And Run**</span></span>
   
    ![][54]
6. <span data-ttu-id="8b3c7-134">Возможно, задаваемые tooprovide пакета iOS hello toostore имя папки.</span><span class="sxs-lookup"><span data-stu-id="8b3c7-134">You may be asked tooprovide a folder name toostore hello iOS package.</span></span> 
   
    ![][43]
7. <span data-ttu-id="8b3c7-135">Если все пойдет хорошо, будет выполнена компиляция проекта hello, и следует открыть его на работу приложения в XCode.</span><span class="sxs-lookup"><span data-stu-id="8b3c7-135">If everything goes fine, then hello project will be compiled and you should open it up on your XCode application.</span></span> 
8. <span data-ttu-id="8b3c7-136">Убедитесь в том, что hello **идентификатор пакета** правильно в проекте hello.</span><span class="sxs-lookup"><span data-stu-id="8b3c7-136">Make sure that hello **Bundle identifier** is correct in hello project.</span></span>  
   
    ![][75]
9. <span data-ttu-id="8b3c7-137">Теперь запустите приложение hello в XCode, чтобы пакет hello развернутой tooyour подключенном устройстве, а на телефоне должна появиться игру Unity!</span><span class="sxs-lookup"><span data-stu-id="8b3c7-137">Now run hello app in XCode so that hello package is deployed tooyour connected device and you should see your Unity game on your phone!</span></span> 

## <span data-ttu-id="8b3c7-138"><a id="monitor"></a>Подключение приложения с возможностью его отслеживания в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="8b3c7-138"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="8b3c7-139"><a id="integrate-push"></a>Включение функции отправки и приема push-уведомлений и обмена сообщениями в приложении</span><span class="sxs-lookup"><span data-stu-id="8b3c7-139"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="8b3c7-140">Mobile Engagement позволяет toointeract со своими пользователями и получить доступ с push-уведомления и сообщения в контексте hello кампаний в приложения.</span><span class="sxs-lookup"><span data-stu-id="8b3c7-140">Mobile Engagement allows you toointeract with your users and REACH with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="8b3c7-141">Этот модуль вызывается REACH на портале мобильного охвата hello.</span><span class="sxs-lookup"><span data-stu-id="8b3c7-141">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="8b3c7-142">Не нужно toodo какой-либо дополнительной настройки уведомлений tooreceive вашего приложения, и он уже настроен для него.</span><span class="sxs-lookup"><span data-stu-id="8b3c7-142">You don't have toodo any additional configuration in your app tooreceive notifications and it is already setup for it.</span></span>

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
