---
title: "Приступая к работе со Службами мобильного взаимодействия Azure для развертывания Unity в Android"
description: "Узнайте, как использовать Службы мобильного взаимодействия Azure с аналитическими функциями и push-уведомлениями для развертывания приложений Unity на устройствах iOS."
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
ms.openlocfilehash: bf0b758159d475b4ed7eadb84227e4824e11ba86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-android-deployment"></a><span data-ttu-id="570a3-103">Приступая к работе со Службами мобильного взаимодействия Azure для развертывания Unity в Android</span><span class="sxs-lookup"><span data-stu-id="570a3-103">Get Started with Azure Mobile Engagement for Unity Android deployment</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="570a3-104">В этой статье показано, как с помощью Служб мобильного взаимодействия Azure анализировать использование приложения и как отправлять push-уведомления сегментированным пользователям приложения Unity при его развертывании на устройстве Android.</span><span class="sxs-lookup"><span data-stu-id="570a3-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and how to send push notifications to segmented users of a Unity application when deploying to an Android device.</span></span>
<span data-ttu-id="570a3-105">Это руководство основывается на классическом руководстве по создании игры в мяч в приложении Unity.</span><span class="sxs-lookup"><span data-stu-id="570a3-105">This tutorial uses the classic Unity Roll a Ball tutorial as the starting point.</span></span> <span data-ttu-id="570a3-106">Вам следует выполнить инструкции, приведенные в этом [руководстве](mobile-engagement-unity-roll-a-ball.md), прежде чем начинать интеграцию Служб мобильного взаимодействия, пример которой приводится в настоящем руководстве.</span><span class="sxs-lookup"><span data-stu-id="570a3-106">You should follow the steps in this [tutorial](mobile-engagement-unity-roll-a-ball.md) before proceeding with the Mobile Engagement integration we showcase in the tutorial below.</span></span> 

<span data-ttu-id="570a3-107">Для работы с данным учебником требуется следующее:</span><span class="sxs-lookup"><span data-stu-id="570a3-107">This tutorial requires the following:</span></span>

* <span data-ttu-id="570a3-108">приложение [Unity Editor](http://unity3d.com/get-unity);</span><span class="sxs-lookup"><span data-stu-id="570a3-108">[Unity Editor](http://unity3d.com/get-unity)</span></span>
* [<span data-ttu-id="570a3-109">пакет SDK Unity для Служб мобильного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="570a3-109">Mobile Engagement Unity SDK</span></span>](https://aka.ms/azmeunitysdk)
* <span data-ttu-id="570a3-110">пакет SDK для Google Android.</span><span class="sxs-lookup"><span data-stu-id="570a3-110">Google Android SDK</span></span>

> [!NOTE]
> <span data-ttu-id="570a3-111">Для работы с этим учебником необходима активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="570a3-111">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="570a3-112">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="570a3-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="570a3-113">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="570a3-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started).</span></span>
> 
> 

## <span data-ttu-id="570a3-114"><a id="setup-azme"></a>Настройка Служб мобильного взаимодействия для вашего приложения Android</span><span class="sxs-lookup"><span data-stu-id="570a3-114"><a id="setup-azme"></a>Setup Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="570a3-115"><a id="connecting-app">
            </a>Подключение приложения к серверной части Служб мобильного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="570a3-115"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
### <a name="import-the-unity-package"></a><span data-ttu-id="570a3-116">Импорт пакета Unity</span><span class="sxs-lookup"><span data-stu-id="570a3-116">Import the Unity package</span></span>
1. <span data-ttu-id="570a3-117">Загрузите пакет [Служб мобильного взаимодействия для Unity](https://aka.ms/azmeunitysdk) и сохраните его на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="570a3-117">Download the [Mobile Engagement Unity package](https://aka.ms/azmeunitysdk) and save it to your local machine.</span></span> 
2. <span data-ttu-id="570a3-118">Выберите **Ресурсы -> Импорт пакета -> Custom Package** (Пользовательский пакет) и выберите пакет, скачанный на предыдущем этапе.</span><span class="sxs-lookup"><span data-stu-id="570a3-118">Go to **Assets -> Import Package -> Custom Package** and select the package you downloaded in the above step.</span></span> 
   
    ![][70] 
3. <span data-ttu-id="570a3-119">Убедитесь, что выбраны все файлы, а затем нажмите кнопку **Импорт** .</span><span class="sxs-lookup"><span data-stu-id="570a3-119">Make sure all files are selected and click **Import** button.</span></span> 
   
    ![][71] 
4. <span data-ttu-id="570a3-120">Когда импорт будет завершен, в вашем проекте отобразятся импортированные файлы пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="570a3-120">Once Import is successful, you will see the imported SDK files in your project.</span></span>  
   
    ![][72] 

### <a name="update-the-engagementconfiguration"></a><span data-ttu-id="570a3-121">Обновление конфигурации EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="570a3-121">Update the EngagementConfiguration</span></span>
1. <span data-ttu-id="570a3-122">В папке пакета SDK откройте файл скрипта **EngagementConfiguration** и обновите **ANDROID\_CONNECTION\_STRING** с помощью строки подключения, полученной ранее на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="570a3-122">Open up the **EngagementConfiguration** script file from the SDK folder and update the **ANDROID\_CONNECTION\_STRING** with the connection string you obtained earlier from the Azure portal.</span></span>  
   
    ![][73]
2. <span data-ttu-id="570a3-123">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="570a3-123">Save the file</span></span> 
3. <span data-ttu-id="570a3-124">Щелкните **Файл -> Engagement -> Generate Android Manifest** (Создание манифеста Android).</span><span class="sxs-lookup"><span data-stu-id="570a3-124">Execute **File -> Engagement -> Generate Android Manifest**.</span></span> <span data-ttu-id="570a3-125">Это подключаемый модуль, добавленный в ваш пакет SDK для Служб мобильного взаимодействия. Если его щелкнуть, параметры проекта будут автоматически обновлены.</span><span class="sxs-lookup"><span data-stu-id="570a3-125">This is the plugin added by the Mobile Engagement SDK and clicking on it will automatically update your project settings.</span></span> 
   
    ![][74]

> [!IMPORTANT]
> <span data-ttu-id="570a3-126">Его нужно запускать всегда, когда обновляется файл **EngagementConfiguration**. В противном случае изменения не отражаются в приложении.</span><span class="sxs-lookup"><span data-stu-id="570a3-126">Make sure to execute this every time you update the **EngagementConfiguration** file otherwise your changes will not be reflected in the app.</span></span> 
> 
> 

### <a name="configure-the-app-for-basic-tracking"></a><span data-ttu-id="570a3-127">Настройка базового отслеживания в приложении</span><span class="sxs-lookup"><span data-stu-id="570a3-127">Configure the app for basic tracking</span></span>
1. <span data-ttu-id="570a3-128">Откройте сценарий **PlayerController** , вложенный для редактирования в объект Player.</span><span class="sxs-lookup"><span data-stu-id="570a3-128">Open up the **PlayerController** script attached to the Player object for editing.</span></span> 
2. <span data-ttu-id="570a3-129">Добавьте следующую инструкцию using:</span><span class="sxs-lookup"><span data-stu-id="570a3-129">Add the following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Unity;
3. <span data-ttu-id="570a3-130">Добавьте следующую строку в метод `Start()`.</span><span class="sxs-lookup"><span data-stu-id="570a3-130">Add the following to the `Start()` method</span></span>
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-the-app"></a><span data-ttu-id="570a3-131">Развертывание и запуск приложения</span><span class="sxs-lookup"><span data-stu-id="570a3-131">Deploy and run the app</span></span>
<span data-ttu-id="570a3-132">Прежде чем развертывать это приложение Unity у себя на устройстве, убедитесь, что на компьютере установлен пакет SDK для Android.</span><span class="sxs-lookup"><span data-stu-id="570a3-132">Make sure that you have Android SDK installed on your machine before attempting to deploy this Unity app to your device.</span></span> 

1. <span data-ttu-id="570a3-133">Подключите устройство Android к компьютеру.</span><span class="sxs-lookup"><span data-stu-id="570a3-133">Connect an Android device to your machine.</span></span> 
2. <span data-ttu-id="570a3-134">Откройте **Файл -> Параметры сборки**.</span><span class="sxs-lookup"><span data-stu-id="570a3-134">Open up **File -> Build Settings**</span></span> 
   
    ![][40]
3. <span data-ttu-id="570a3-135">Выберите **Android** и щелкните **Switch Platform** (Переключить платформу).</span><span class="sxs-lookup"><span data-stu-id="570a3-135">Select **Android** and then click on **Switch Platform**</span></span>
   
    ![][51]
   
    ![][52]
4. <span data-ttu-id="570a3-136">Щелкните **Настройка проигрывателя** и укажите допустимый идентификатор пакета.</span><span class="sxs-lookup"><span data-stu-id="570a3-136">Click on **Player settings** and provide a valid Bundle Identifier.</span></span> 
   
    ![][53]
5. <span data-ttu-id="570a3-137">Наконец, нажмите кнопку **Сборка и запуск**</span><span class="sxs-lookup"><span data-stu-id="570a3-137">Finally click on **Build And Run**</span></span>
   
    ![][54]
6. <span data-ttu-id="570a3-138">Возможно, вам потребуется указать имя папки для хранения пакета Android.</span><span class="sxs-lookup"><span data-stu-id="570a3-138">You may be asked to provide a folder name to store the Android package.</span></span> 
7. <span data-ttu-id="570a3-139">Если процесс пройдет успешно и пакет будет развернут на подключенном устройстве, вы увидите игру Unity у себя на телефоне.</span><span class="sxs-lookup"><span data-stu-id="570a3-139">If everything goes fine, then the package will be deployed to your connected device and you should see your Unity game on your phone!</span></span> 

## <span data-ttu-id="570a3-140"><a id="monitor"></a>Подключение приложения с мониторингом в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="570a3-140"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="570a3-141"><a id="integrate-push"></a>Включение push-уведомлений и обмена сообщениями в приложении</span><span class="sxs-lookup"><span data-stu-id="570a3-141"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

### <a name="update-the-engagementconfiguration"></a><span data-ttu-id="570a3-142">Обновление конфигурации EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="570a3-142">Update the EngagementConfiguration</span></span>
1. <span data-ttu-id="570a3-143">В папке пакета SDK откройте файл скрипта **EngagementConfiguration** и обновите **ANDROID\_GOOGLE\_NUMBER** с помощью **номера проекта Google**, полученного ранее на портале разработчиков облака Google.</span><span class="sxs-lookup"><span data-stu-id="570a3-143">Open up the **EngagementConfiguration** script file from the SDK folder and update the **ANDROID\_GOOGLE\_NUMBER** with the **Google Project Number** you obtained earlier from the Google Cloud Developer portal.</span></span> <span data-ttu-id="570a3-144">Это строковое значение, поэтому обязательно заключите его в двойные кавычки.</span><span class="sxs-lookup"><span data-stu-id="570a3-144">This is a string value so make sure to enclose it in double quotes.</span></span> 
   
    ![][75]
2. <span data-ttu-id="570a3-145">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="570a3-145">Save the file.</span></span> 
3. <span data-ttu-id="570a3-146">Щелкните **Файл -> Engagement -> Generate Android Manifest** (Создание манифеста Android).</span><span class="sxs-lookup"><span data-stu-id="570a3-146">Execute **File -> Engagement -> Generate Android Manifest**.</span></span> <span data-ttu-id="570a3-147">Это подключаемый модуль, добавленный в ваш пакет SDK для Служб мобильного взаимодействия. Если его щелкнуть, параметры проекта будут автоматически обновлены.</span><span class="sxs-lookup"><span data-stu-id="570a3-147">This is the plugin added by the Mobile Engagement SDK and clicking on it will automatically update your project settings.</span></span> 
   
    ![][74]

### <a name="configure-the-app-to-receive-notifications"></a><span data-ttu-id="570a3-148">Настройка в приложении получения уведомлений</span><span class="sxs-lookup"><span data-stu-id="570a3-148">Configure the app to receive notifications</span></span>
1. <span data-ttu-id="570a3-149">Откройте сценарий **PlayerController** , вложенный для редактирования в объект Player.</span><span class="sxs-lookup"><span data-stu-id="570a3-149">Open up the **PlayerController** script attached to the Player object for editing.</span></span> 
2. <span data-ttu-id="570a3-150">Добавьте следующую строку в метод `Start()` .</span><span class="sxs-lookup"><span data-stu-id="570a3-150">Add the following to the `Start()` method</span></span>
   
        EngagementReachAgent.Initialize();
3. <span data-ttu-id="570a3-151">Теперь, когда приложение обновлено, разверните и запустите его на устройстве согласно приведенным ниже инструкциям.</span><span class="sxs-lookup"><span data-stu-id="570a3-151">Now that the app is updated, deploy and run the app on a device per the instructions provided below.</span></span> 

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
