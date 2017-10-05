---
title: "Приступая к работе со Службами мобильного взаимодействия Azure для развертывания Unity в iOS"
description: "Узнайте, как использовать Службы мобильного взаимодействия Azure с аналитическими функциями и push-уведомлениями для развертывания приложений Unity на устройствах iOS."
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
ms.openlocfilehash: c8f50404771965ec636065346ac04e059d264c3d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-ios-deployment"></a><span data-ttu-id="df561-103">Приступая к работе со Службами мобильного взаимодействия Azure для развертывания Unity в iOS</span><span class="sxs-lookup"><span data-stu-id="df561-103">Get Started with Azure Mobile Engagement for Unity iOS deployment</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="df561-104">В этой статье показано, как с помощью Служб мобильного взаимодействия Azure анализировать использование приложения и как отправлять push-уведомления сегментированным пользователям приложения Unity при его развертывании на устройстве iOS.</span><span class="sxs-lookup"><span data-stu-id="df561-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and how to send push notifications to segmented users of a Unity application when deploying to an iOS device.</span></span>
<span data-ttu-id="df561-105">Это руководство основывается на классическом руководстве по создании игры в мяч в приложении Unity.</span><span class="sxs-lookup"><span data-stu-id="df561-105">This tutorial uses the classic Unity Roll a Ball tutorial as the starting point.</span></span> <span data-ttu-id="df561-106">Вам следует выполнить инструкции, приведенные в этом [руководстве](mobile-engagement-unity-roll-a-ball.md), прежде чем начинать интеграцию Служб мобильного взаимодействия, пример которой приводится в настоящем руководстве.</span><span class="sxs-lookup"><span data-stu-id="df561-106">You should follow the steps in this [tutorial](mobile-engagement-unity-roll-a-ball.md) before proceeding with the Mobile Engagement integration we showcase in the tutorial below.</span></span> 

<span data-ttu-id="df561-107">Для работы с данным учебником требуется следующее:</span><span class="sxs-lookup"><span data-stu-id="df561-107">This tutorial requires the following:</span></span>

* <span data-ttu-id="df561-108">приложение [Unity Editor](http://unity3d.com/get-unity);</span><span class="sxs-lookup"><span data-stu-id="df561-108">[Unity Editor](http://unity3d.com/get-unity)</span></span>
* [<span data-ttu-id="df561-109">пакет SDK Unity для Служб мобильного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="df561-109">Mobile Engagement Unity SDK</span></span>](https://aka.ms/azmeunitysdk)
* <span data-ttu-id="df561-110">редактор XCode.</span><span class="sxs-lookup"><span data-stu-id="df561-110">XCode Editor</span></span>

> [!NOTE]
> <span data-ttu-id="df561-111">Для работы с этим учебником необходима активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="df561-111">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="df561-112">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="df561-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="df561-113">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="df561-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started).</span></span>
> 
> 

## <span data-ttu-id="df561-114"><a id="setup-azme"></a>Настройка Служб мобильного взаимодействия для вашего приложения iOS</span><span class="sxs-lookup"><span data-stu-id="df561-114"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="df561-115"><a id="connecting-app">
            </a>Подключение приложения к серверной части Служб мобильного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="df561-115"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
### <a name="import-the-unity-package"></a><span data-ttu-id="df561-116">Импорт пакета Unity</span><span class="sxs-lookup"><span data-stu-id="df561-116">Import the Unity package</span></span>
1. <span data-ttu-id="df561-117">Загрузите пакет [Служб мобильного взаимодействия для Unity](https://aka.ms/azmeunitysdk) и сохраните его на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="df561-117">Download the [Mobile Engagement Unity package](https://aka.ms/azmeunitysdk) and save it to your local machine.</span></span> 
2. <span data-ttu-id="df561-118">Выберите **Ресурсы -> Импорт пакета -> Custom Package** (Пользовательский пакет) и выберите пакет, скачанный на предыдущем этапе.</span><span class="sxs-lookup"><span data-stu-id="df561-118">Go to **Assets -> Import Package -> Custom Package** and select the package you downloaded in the above step.</span></span> 
   
    ![][70] 
3. <span data-ttu-id="df561-119">Убедитесь, что выбраны все файлы, а затем нажмите кнопку **Импорт** .</span><span class="sxs-lookup"><span data-stu-id="df561-119">Make sure all files are selected and click **Import** button.</span></span> 
   
    ![][71] 
4. <span data-ttu-id="df561-120">Когда импорт будет завершен, в вашем проекте отобразятся импортированные файлы пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="df561-120">Once Import is successful, you will see the imported SDK files in your project.</span></span>  
   
    ![][72] 

### <a name="update-the-engagementconfiguration"></a><span data-ttu-id="df561-121">Обновление конфигурации EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="df561-121">Update the EngagementConfiguration</span></span>
1. <span data-ttu-id="df561-122">В папке пакета SDK откройте файл сценария **EngagementConfiguration** и обновите **IOS\_CONNECTION\_STRING** с помощью строки подключения, которую вы получили ранее на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="df561-122">Open up the **EngagementConfiguration** script file from the SDK folder and update the **IOS\_CONNECTION\_STRING** with the connection string you obtained earlier from the Azure portal.</span></span>  
   
    ![][73]
2. <span data-ttu-id="df561-123">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="df561-123">Save the file.</span></span> 

### <a name="configure-the-app-for-basic-tracking"></a><span data-ttu-id="df561-124">Настройка базового отслеживания в приложении</span><span class="sxs-lookup"><span data-stu-id="df561-124">Configure the app for basic tracking</span></span>
1. <span data-ttu-id="df561-125">Откройте сценарий **PlayerController** , вложенный для редактирования в объект Player.</span><span class="sxs-lookup"><span data-stu-id="df561-125">Open up the **PlayerController** script attached to the Player object for editing.</span></span> 
2. <span data-ttu-id="df561-126">Добавьте следующую инструкцию using:</span><span class="sxs-lookup"><span data-stu-id="df561-126">Add the following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Unity;
3. <span data-ttu-id="df561-127">Добавьте следующую строку в метод `Start()`.</span><span class="sxs-lookup"><span data-stu-id="df561-127">Add the following to the `Start()` method</span></span>
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-the-app"></a><span data-ttu-id="df561-128">Развертывание и запуск приложения</span><span class="sxs-lookup"><span data-stu-id="df561-128">Deploy and run the app</span></span>
1. <span data-ttu-id="df561-129">Подключите устройство iOS к компьютеру.</span><span class="sxs-lookup"><span data-stu-id="df561-129">Connect an iOS device to your machine.</span></span> 
2. <span data-ttu-id="df561-130">Откройте **Файл -> Параметры сборки**.</span><span class="sxs-lookup"><span data-stu-id="df561-130">Open up **File -> Build Settings**</span></span> 
   
    ![][40]
3. <span data-ttu-id="df561-131">Выберите **iOS** и щелкните **Переключить платформу**.</span><span class="sxs-lookup"><span data-stu-id="df561-131">Select **iOS** and then click on **Switch Platform**</span></span>
   
    ![][41]
   
    ![][42]
4. <span data-ttu-id="df561-132">Щелкните **Настройка проигрывателя** и укажите допустимый идентификатор пакета.</span><span class="sxs-lookup"><span data-stu-id="df561-132">Click on **Player settings** and provide a valid Bundle Identifier.</span></span> 
   
    ![][53]
5. <span data-ttu-id="df561-133">Наконец, нажмите кнопку **Сборка и запуск**</span><span class="sxs-lookup"><span data-stu-id="df561-133">Finally click on **Build And Run**</span></span>
   
    ![][54]
6. <span data-ttu-id="df561-134">Возможно, вам потребуется указать имя папки для хранения пакета iOS.</span><span class="sxs-lookup"><span data-stu-id="df561-134">You may be asked to provide a folder name to store the iOS package.</span></span> 
   
    ![][43]
7. <span data-ttu-id="df561-135">Если все пойдет хорошо и проект будет скомпилирован, откройте его в приложении XCode.</span><span class="sxs-lookup"><span data-stu-id="df561-135">If everything goes fine, then the project will be compiled and you should open it up on your XCode application.</span></span> 
8. <span data-ttu-id="df561-136">Убедитесь, что в проекте указан правильный **идентификатор пакета** .</span><span class="sxs-lookup"><span data-stu-id="df561-136">Make sure that the **Bundle identifier** is correct in the project.</span></span>  
   
    ![][75]
9. <span data-ttu-id="df561-137">Теперь запустите приложение XCode, чтобы развернуть пакет на подключенном устройстве, и вы увидите игру Unity у себя на телефоне.</span><span class="sxs-lookup"><span data-stu-id="df561-137">Now run the app in XCode so that the package is deployed to your connected device and you should see your Unity game on your phone!</span></span> 

## <span data-ttu-id="df561-138"><a id="monitor"></a>Подключение приложения с мониторингом в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="df561-138"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="df561-139"><a id="integrate-push"></a>Включение push-уведомлений и обмена сообщениями в приложении</span><span class="sxs-lookup"><span data-stu-id="df561-139"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="df561-140">Службы мобильного взаимодействия позволяют взаимодействовать и связываться с пользователями с помощью push-уведомлений и сообщений в приложении в контексте кампаний.</span><span class="sxs-lookup"><span data-stu-id="df561-140">Mobile Engagement allows you to interact with your users and REACH with push notifications and in-app messaging in the context of campaigns.</span></span> <span data-ttu-id="df561-141">На портале Служб мобильного взаимодействия этот модуль называется МОДУЛЕМ ОБРАБОТКИ РЕКЛАМНЫХ КАМПАНИЙ.</span><span class="sxs-lookup"><span data-stu-id="df561-141">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="df561-142">Дополнительно настраивать в приложении получение уведомлений не нужно, так как эта функция уже настроена.</span><span class="sxs-lookup"><span data-stu-id="df561-142">You don't have to do any additional configuration in your app to receive notifications and it is already setup for it.</span></span>

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
