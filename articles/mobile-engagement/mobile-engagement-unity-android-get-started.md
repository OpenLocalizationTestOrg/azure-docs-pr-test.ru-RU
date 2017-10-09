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
# <a name="get-started-with-azure-mobile-engagement-for-unity-android-deployment"></a><span data-ttu-id="21e67-103">Приступая к работе со Службами мобильного взаимодействия Azure для развертывания Unity в Android</span><span class="sxs-lookup"><span data-stu-id="21e67-103">Get Started with Azure Mobile Engagement for Unity Android deployment</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="21e67-104">В этом разделе показано, как Azure Mobile Engagement toounderstand toouse использовании веб-приложения и как toosend отправить уведомления пользователей toosegmented приложения Unity, при развертывании tooan устройства Android.</span><span class="sxs-lookup"><span data-stu-id="21e67-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and how toosend push notifications toosegmented users of a Unity application when deploying tooan Android device.</span></span>
<span data-ttu-id="21e67-105">В этом учебнике используется hello классический наката Unity учебник шарик как начальная точка hello.</span><span class="sxs-lookup"><span data-stu-id="21e67-105">This tutorial uses hello classic Unity Roll a Ball tutorial as hello starting point.</span></span> <span data-ttu-id="21e67-106">Необходимо выполнить шаги hello в этом [учебника](mobile-engagement-unity-roll-a-ball.md) перед продолжением hello интеграции мобильного охвата, мы демонстрации в учебнике hello ниже.</span><span class="sxs-lookup"><span data-stu-id="21e67-106">You should follow hello steps in this [tutorial](mobile-engagement-unity-roll-a-ball.md) before proceeding with hello Mobile Engagement integration we showcase in hello tutorial below.</span></span> 

<span data-ttu-id="21e67-107">Этот учебник требует hello следующее:</span><span class="sxs-lookup"><span data-stu-id="21e67-107">This tutorial requires hello following:</span></span>

* <span data-ttu-id="21e67-108">приложение [Unity Editor](http://unity3d.com/get-unity);</span><span class="sxs-lookup"><span data-stu-id="21e67-108">[Unity Editor](http://unity3d.com/get-unity)</span></span>
* [<span data-ttu-id="21e67-109">пакет SDK Unity для Служб мобильного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="21e67-109">Mobile Engagement Unity SDK</span></span>](https://aka.ms/azmeunitysdk)
* <span data-ttu-id="21e67-110">пакет SDK для Google Android.</span><span class="sxs-lookup"><span data-stu-id="21e67-110">Google Android SDK</span></span>

> [!NOTE]
> <span data-ttu-id="21e67-111">toocomplete этого учебника необходимо иметь активную учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="21e67-111">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="21e67-112">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="21e67-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="21e67-113">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="21e67-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started).</span></span>
> 
> 

## <span data-ttu-id="21e67-114"><a id="setup-azme">
            </a>Настройка Служб мобильного взаимодействия для вашего приложения Android</span><span class="sxs-lookup"><span data-stu-id="21e67-114"><a id="setup-azme"></a>Setup Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="21e67-115"><a id="connecting-app"></a>Подключение мобильного охвата toohello внутренний сервер приложений</span><span class="sxs-lookup"><span data-stu-id="21e67-115"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
### <a name="import-hello-unity-package"></a><span data-ttu-id="21e67-116">Импорт пакета Unity hello</span><span class="sxs-lookup"><span data-stu-id="21e67-116">Import hello Unity package</span></span>
1. <span data-ttu-id="21e67-117">Загрузите hello [пакет Mobile Engagement Unity](https://aka.ms/azmeunitysdk) и сохраните его tooyour локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="21e67-117">Download hello [Mobile Engagement Unity package](https://aka.ms/azmeunitysdk) and save it tooyour local machine.</span></span> 
2. <span data-ttu-id="21e67-118">Go слишком**активы -> Импорт пакета -> Настройка пакета** и hello выберите пакет, загруженный в hello выше шаг.</span><span class="sxs-lookup"><span data-stu-id="21e67-118">Go too**Assets -> Import Package -> Custom Package** and select hello package you downloaded in hello above step.</span></span> 
   
    ![][70] 
3. <span data-ttu-id="21e67-119">Убедитесь, что выбраны все файлы, а затем нажмите кнопку **Импорт** .</span><span class="sxs-lookup"><span data-stu-id="21e67-119">Make sure all files are selected and click **Import** button.</span></span> 
   
    ![][71] 
4. <span data-ttu-id="21e67-120">Если импорт прошел успешно, вы увидите hello импортировать файлы пакета SDK в своем проекте.</span><span class="sxs-lookup"><span data-stu-id="21e67-120">Once Import is successful, you will see hello imported SDK files in your project.</span></span>  
   
    ![][72] 

### <a name="update-hello-engagementconfiguration"></a><span data-ttu-id="21e67-121">Обновление hello EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="21e67-121">Update hello EngagementConfiguration</span></span>
1. <span data-ttu-id="21e67-122">Откройте hello **EngagementConfiguration** файл скрипта из папки и обновление hello hello SDK **ANDROID\_подключения\_строка** со строкой подключения hello полученный ранее из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="21e67-122">Open up hello **EngagementConfiguration** script file from hello SDK folder and update hello **ANDROID\_CONNECTION\_STRING** with hello connection string you obtained earlier from hello Azure portal.</span></span>  
   
    ![][73]
2. <span data-ttu-id="21e67-123">Сохраните файл hello</span><span class="sxs-lookup"><span data-stu-id="21e67-123">Save hello file</span></span> 
3. <span data-ttu-id="21e67-124">Щелкните **Файл -> Engagement -> Generate Android Manifest** (Создание манифеста Android).</span><span class="sxs-lookup"><span data-stu-id="21e67-124">Execute **File -> Engagement -> Generate Android Manifest**.</span></span> <span data-ttu-id="21e67-125">Это hello подключаемый модуль, добавленные hello Mobile Engagement SDK и щелкнув его автоматически обновит параметры проекта.</span><span class="sxs-lookup"><span data-stu-id="21e67-125">This is hello plugin added by hello Mobile Engagement SDK and clicking on it will automatically update your project settings.</span></span> 
   
    ![][74]

> [!IMPORTANT]
> <span data-ttu-id="21e67-126">Сделать tooexecute убедиться, что каждый раз при обновлении hello **EngagementConfiguration** файла в противном случае изменения не будут отражены в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="21e67-126">Make sure tooexecute this every time you update hello **EngagementConfiguration** file otherwise your changes will not be reflected in hello app.</span></span> 
> 
> 

### <a name="configure-hello-app-for-basic-tracking"></a><span data-ttu-id="21e67-127">Настройте приложение hello для отслеживания основных</span><span class="sxs-lookup"><span data-stu-id="21e67-127">Configure hello app for basic tracking</span></span>
1. <span data-ttu-id="21e67-128">Откройте hello **PlayerController** сценарий присоединен объект toohello проигрывателя для редактирования.</span><span class="sxs-lookup"><span data-stu-id="21e67-128">Open up hello **PlayerController** script attached toohello Player object for editing.</span></span> 
2. <span data-ttu-id="21e67-129">Добавьте следующее hello с помощью инструкции:</span><span class="sxs-lookup"><span data-stu-id="21e67-129">Add hello following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Unity;
3. <span data-ttu-id="21e67-130">Добавьте следующие toohello hello `Start()` метод</span><span class="sxs-lookup"><span data-stu-id="21e67-130">Add hello following toohello `Start()` method</span></span>
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-hello-app"></a><span data-ttu-id="21e67-131">Развертывание и запуск приложения hello</span><span class="sxs-lookup"><span data-stu-id="21e67-131">Deploy and run hello app</span></span>
<span data-ttu-id="21e67-132">Убедитесь, что Android SDK, которые установлены на компьютере, прежде чем toodeploy это устройство tooyour приложения Unity.</span><span class="sxs-lookup"><span data-stu-id="21e67-132">Make sure that you have Android SDK installed on your machine before attempting toodeploy this Unity app tooyour device.</span></span> 

1. <span data-ttu-id="21e67-133">Подключение компьютера к устройству Android tooyour.</span><span class="sxs-lookup"><span data-stu-id="21e67-133">Connect an Android device tooyour machine.</span></span> 
2. <span data-ttu-id="21e67-134">Откройте **Файл -> Параметры сборки**.</span><span class="sxs-lookup"><span data-stu-id="21e67-134">Open up **File -> Build Settings**</span></span> 
   
    ![][40]
3. <span data-ttu-id="21e67-135">Выберите **Android** и щелкните **Switch Platform** (Переключить платформу).</span><span class="sxs-lookup"><span data-stu-id="21e67-135">Select **Android** and then click on **Switch Platform**</span></span>
   
    ![][51]
   
    ![][52]
4. <span data-ttu-id="21e67-136">Щелкните **Настройка проигрывателя** и укажите допустимый идентификатор пакета.</span><span class="sxs-lookup"><span data-stu-id="21e67-136">Click on **Player settings** and provide a valid Bundle Identifier.</span></span> 
   
    ![][53]
5. <span data-ttu-id="21e67-137">Наконец, нажмите кнопку **Сборка и запуск**</span><span class="sxs-lookup"><span data-stu-id="21e67-137">Finally click on **Build And Run**</span></span>
   
    ![][54]
6. <span data-ttu-id="21e67-138">Возможно, задаваемые tooprovide папки имя toostore hello Android пакета.</span><span class="sxs-lookup"><span data-stu-id="21e67-138">You may be asked tooprovide a folder name toostore hello Android package.</span></span> 
7. <span data-ttu-id="21e67-139">Если все пойдет хорошо, hello пакета будет развернутой tooyour подключенных устройств и увидеть игру Unity на телефоне!</span><span class="sxs-lookup"><span data-stu-id="21e67-139">If everything goes fine, then hello package will be deployed tooyour connected device and you should see your Unity game on your phone!</span></span> 

## <span data-ttu-id="21e67-140"><a id="monitor"></a>Подключение приложения с возможностью его отслеживания в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="21e67-140"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="21e67-141"><a id="integrate-push"></a>Включение функции отправки и приема push-уведомлений и обмена сообщениями в приложении</span><span class="sxs-lookup"><span data-stu-id="21e67-141"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

### <a name="update-hello-engagementconfiguration"></a><span data-ttu-id="21e67-142">Обновление hello EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="21e67-142">Update hello EngagementConfiguration</span></span>
1. <span data-ttu-id="21e67-143">Откройте hello **EngagementConfiguration** файл скрипта из папки и обновление hello hello SDK **ANDROID\_GOOGLE\_номер** с hello **проекта Google Номер** полученный ранее из портала разработчиков облачных Google hello.</span><span class="sxs-lookup"><span data-stu-id="21e67-143">Open up hello **EngagementConfiguration** script file from hello SDK folder and update hello **ANDROID\_GOOGLE\_NUMBER** with hello **Google Project Number** you obtained earlier from hello Google Cloud Developer portal.</span></span> <span data-ttu-id="21e67-144">Это строковое значение, поэтому следует убедиться, что tooenclose его в двойные кавычки.</span><span class="sxs-lookup"><span data-stu-id="21e67-144">This is a string value so make sure tooenclose it in double quotes.</span></span> 
   
    ![][75]
2. <span data-ttu-id="21e67-145">Сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="21e67-145">Save hello file.</span></span> 
3. <span data-ttu-id="21e67-146">Щелкните **Файл -> Engagement -> Generate Android Manifest** (Создание манифеста Android).</span><span class="sxs-lookup"><span data-stu-id="21e67-146">Execute **File -> Engagement -> Generate Android Manifest**.</span></span> <span data-ttu-id="21e67-147">Это hello подключаемый модуль, добавленные hello Mobile Engagement SDK и щелкнув его автоматически обновит параметры проекта.</span><span class="sxs-lookup"><span data-stu-id="21e67-147">This is hello plugin added by hello Mobile Engagement SDK and clicking on it will automatically update your project settings.</span></span> 
   
    ![][74]

### <a name="configure-hello-app-tooreceive-notifications"></a><span data-ttu-id="21e67-148">Настройка уведомлений tooreceive приложения hello</span><span class="sxs-lookup"><span data-stu-id="21e67-148">Configure hello app tooreceive notifications</span></span>
1. <span data-ttu-id="21e67-149">Откройте hello **PlayerController** сценарий присоединен объект toohello проигрывателя для редактирования.</span><span class="sxs-lookup"><span data-stu-id="21e67-149">Open up hello **PlayerController** script attached toohello Player object for editing.</span></span> 
2. <span data-ttu-id="21e67-150">Добавьте следующие toohello hello `Start()` метод</span><span class="sxs-lookup"><span data-stu-id="21e67-150">Add hello following toohello `Start()` method</span></span>
   
        EngagementReachAgent.Initialize();
3. <span data-ttu-id="21e67-151">Теперь, когда hello приложение обновляется, разверните и запустите приложение hello на устройстве на hello, приведенным ниже.</span><span class="sxs-lookup"><span data-stu-id="21e67-151">Now that hello app is updated, deploy and run hello app on a device per hello instructions provided below.</span></span> 

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
