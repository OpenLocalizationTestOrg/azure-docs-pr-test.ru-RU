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
# <a name="get-started-with-azure-mobile-engagement-for-xamarinandroid-apps"></a><span data-ttu-id="cc557-103">Начало работы со Службами мобильного взаимодействия Azure для приложений Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="cc557-103">Get Started with Azure Mobile Engagement for Xamarin.Android Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="cc557-104">В этом разделе показано, как Azure Mobile Engagement toounderstand toouse использовании веб-приложения и как toosend push-уведомления пользователей toosegmented Xamarin.Android приложения.</span><span class="sxs-lookup"><span data-stu-id="cc557-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and how toosend push notifications toosegmented users of a Xamarin.Android application.</span></span>
<span data-ttu-id="cc557-105">В этом учебнике показано hello простой широковещательных сценарий с помощью мобильного охвата.</span><span class="sxs-lookup"><span data-stu-id="cc557-105">This tutorial demonstrates hello simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="cc557-106">В рассматриваемом сценарии создается пустое приложение Xamarin.Android, которое собирает основные данные и получает push-уведомления с помощью службы Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="cc557-106">In it, you create a blank Xamarin.Android app that collects basic data and receives push notifications using Google Cloud Messaging (GCM).</span></span>

> [!NOTE]
> <span data-ttu-id="cc557-107">Служба Azure Mobile Engagement Hello будет прекращено 2018 марта и в настоящее время только доступные tooexisting клиентов.</span><span class="sxs-lookup"><span data-stu-id="cc557-107">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="cc557-108">Дополнительные сведения см. на странице [Службы мобильного взаимодействия](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="cc557-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="cc557-109">Этот учебник требует hello следующее:</span><span class="sxs-lookup"><span data-stu-id="cc557-109">This tutorial requires hello following:</span></span>

* <span data-ttu-id="cc557-110">[Xamarin Studio](http://xamarin.com/studio).</span><span class="sxs-lookup"><span data-stu-id="cc557-110">[Xamarin Studio](http://xamarin.com/studio).</span></span> <span data-ttu-id="cc557-111">Вы также можете использовать Visual Studio с расширением Xamarin, но в этом руководстве используется Xamarin Studio.</span><span class="sxs-lookup"><span data-stu-id="cc557-111">You can also use Visual Studio with Xamarin but this tutorial uses Xamarin Studio.</span></span> <span data-ttu-id="cc557-112">Инструкции см. в руководстве по [установке и настройке Visual Studio и Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="cc557-112">For installation instructions, see [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>
* [<span data-ttu-id="cc557-113">пакет Xamarin SDK для Служб мобильного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="cc557-113">Mobile Engagement Xamarin SDK</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> <span data-ttu-id="cc557-114">toocomplete этого учебника необходимо иметь активную учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="cc557-114">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="cc557-115">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="cc557-115">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="cc557-116">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="cc557-116">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started).</span></span>
> 
> 

## <span data-ttu-id="cc557-117"><a id="setup-azme">
            </a>Настройка Служб мобильного взаимодействия для вашего приложения Android</span><span class="sxs-lookup"><span data-stu-id="cc557-117"><a id="setup-azme"></a>Setup Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="cc557-118"><a id="connecting-app"></a>Подключение мобильного охвата toohello внутренний сервер приложений</span><span class="sxs-lookup"><span data-stu-id="cc557-118"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="cc557-119">В этом руководстве содержатся «базовой интеграции», который hello минимальный набор данных требуется toocollect и отправить push-уведомление.</span><span class="sxs-lookup"><span data-stu-id="cc557-119">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> 

<span data-ttu-id="cc557-120">Мы создадим простое приложение с интеграцией hello toodemonstrate Xamarin Studio.</span><span class="sxs-lookup"><span data-stu-id="cc557-120">We will create a basic app with Xamarin Studio toodemonstrate hello integration.</span></span>

### <a name="create-a-new-xamarinandroid-project"></a><span data-ttu-id="cc557-121">Создание нового проекта Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="cc557-121">Create a new Xamarin.Android project</span></span>
1. <span data-ttu-id="cc557-122">Запустите **Xamarin Studio** Go слишком**файл** -> **New** -> **решения**</span><span class="sxs-lookup"><span data-stu-id="cc557-122">Launch **Xamarin Studio** Go too**File** -> **New** -> **Solution**</span></span> 
   
    ![][1]
2. <span data-ttu-id="cc557-123">Выберите **приложения Android** убедитесь, что выбран hello язык — **C#** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="cc557-123">Select **Android App** then make sure hello selected language is **C#** and click **Next**.</span></span>
   
    ![][2]
3. <span data-ttu-id="cc557-124">Заполните hello **имя приложения** и hello **идентификатор организации**.</span><span class="sxs-lookup"><span data-stu-id="cc557-124">Fill in hello **App Name** and hello **Organization Identifier**.</span></span> <span data-ttu-id="cc557-125">Убедитесь, что toocheckmark **службы Google Play** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="cc557-125">Make sure toocheckmark **Google Play Services** and then click **Next**.</span></span> 
   
    ![][3]
4. <span data-ttu-id="cc557-126">Обновление hello **имя проекта**, **имя решения** и **расположение** , если требуется и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="cc557-126">Update hello **Project Name**, **Solution Name** and **Location** if required and click **Create**.</span></span>
   
    ![][4]

<span data-ttu-id="cc557-127">Xamarin Studio создаст приложение hello, в котором будет интегрировать мобильного охвата.</span><span class="sxs-lookup"><span data-stu-id="cc557-127">Xamarin Studio will create hello app in which we will integrate Mobile Engagement.</span></span> 

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="cc557-128">Подключение Engagement tooMobile внутренний сервер приложений</span><span class="sxs-lookup"><span data-stu-id="cc557-128">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="cc557-129">Щелкните правой кнопкой мыши hello **пакетов** папки в windows hello решений и выберите **Добавление пакетов...**</span><span class="sxs-lookup"><span data-stu-id="cc557-129">Right click hello **Packages** folder in hello Solution windows and select **Add Packages...**</span></span>
   
    ![][5]
2. <span data-ttu-id="cc557-130">Поиск hello **Microsoft Azure Mobile Engagement Xamarin SDK** и добавьте его tooyour решения.</span><span class="sxs-lookup"><span data-stu-id="cc557-130">Search for hello **Microsoft Azure Mobile Engagement Xamarin SDK** and add it tooyour solution.</span></span>  
   
    ![][6]
3. <span data-ttu-id="cc557-131">Откройте **MainActivity.cs** и добавьте следующее hello операторы using:</span><span class="sxs-lookup"><span data-stu-id="cc557-131">Open **MainActivity.cs** and add hello following using statements:</span></span>
   
        using Microsoft.Azure.Engagement;
        using Microsoft.Azure.Engagement.Activity;
4. <span data-ttu-id="cc557-132">В hello `OnCreate` метод, добавить следующие tooinitialize hello соединения с внутреннего сервера мобильного охвата hello.</span><span class="sxs-lookup"><span data-stu-id="cc557-132">In hello `OnCreate` method, add hello following tooinitialize hello connection with Mobile Engagement backend.</span></span> <span data-ttu-id="cc557-133">Убедитесь, что tooadd вашей **ConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="cc557-133">Make sure tooadd your **ConnectionString**.</span></span> 
   
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.ConnectionString = "YourConnectionStringFromAzurePortal";
        EngagementAgent.Init(engagementConfiguration);

### <a name="add-permissions-and-a-service-declaration"></a><span data-ttu-id="cc557-134">Добавление разрешений и объявления службы</span><span class="sxs-lookup"><span data-stu-id="cc557-134">Add permissions and a service declaration</span></span>
1. <span data-ttu-id="cc557-135">Откройте hello **Manifest.xml** файл в папке свойства hello.</span><span class="sxs-lookup"><span data-stu-id="cc557-135">Open up hello **Manifest.xml** file under hello Properties folder.</span></span> <span data-ttu-id="cc557-136">Перейдите на вкладку источника, чтобы непосредственного изменения XML-источник hello.</span><span class="sxs-lookup"><span data-stu-id="cc557-136">Select Source tab so that you directly update hello XML source.</span></span>
2. <span data-ttu-id="cc557-137">Добавьте эти разрешения toohello Manifest.xml (который можно найти в разделе hello **свойства** папки) проекта непосредственно перед или после hello `<application>` тег:</span><span class="sxs-lookup"><span data-stu-id="cc557-137">Add these permissions toohello Manifest.xml (which can be found under hello **Properties** folder) of your project immediately before or after hello `<application>` tag:</span></span>
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
3. <span data-ttu-id="cc557-138">Добавьте следующий код hello между hello `<application>` и `</application>` теги toodeclare hello агент службы:</span><span class="sxs-lookup"><span data-stu-id="cc557-138">Add hello following between hello `<application>` and `</application>` tags toodeclare hello agent service:</span></span>
   
        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
4. <span data-ttu-id="cc557-139">В коде hello только что вставленного замените `"<Your application name>"` в метке hello.</span><span class="sxs-lookup"><span data-stu-id="cc557-139">In hello code you just pasted, replace `"<Your application name>"` in hello label.</span></span> <span data-ttu-id="cc557-140">Это отражается в hello **параметры** меню, где пользователи могут видеть службы, работающие на устройстве hello.</span><span class="sxs-lookup"><span data-stu-id="cc557-140">This is displayed in hello **Settings** menu where users can see services running on hello device.</span></span> <span data-ttu-id="cc557-141">Можно добавить слово hello «Служба» в этой метке например.</span><span class="sxs-lookup"><span data-stu-id="cc557-141">You can add hello word "Service" in that label for example.</span></span>

### <a name="send-a-screen-toomobile-engagement"></a><span data-ttu-id="cc557-142">Отправить экрана tooMobile Engagement</span><span class="sxs-lookup"><span data-stu-id="cc557-142">Send a screen tooMobile Engagement</span></span>
<span data-ttu-id="cc557-143">В toostart порядок отправки данных и убедитесь, что пользователи hello активны необходимо отправить по крайней мере один внутреннего сервера мобильного охвата toohello экрана.</span><span class="sxs-lookup"><span data-stu-id="cc557-143">In order toostart sending data and ensuring hello users are active, you must send at least one screen toohello Mobile Engagement backend.</span></span> <span data-ttu-id="cc557-144">Для этого-убедитесь, что hello `MainActivity` наследует от `EngagementActivity` вместо `Activity`.</span><span class="sxs-lookup"><span data-stu-id="cc557-144">For doing this - ensure that hello `MainActivity` inherits from `EngagementActivity` instead of `Activity`.</span></span>

    public class MainActivity : EngagementActivity

<span data-ttu-id="cc557-145">Если наследование от `EngagementActivity` невозможно, необходимо добавить методы `.StartActivity` и `.EndActivity` в `OnResume` и `OnPause` соответственно.</span><span class="sxs-lookup"><span data-stu-id="cc557-145">Alternatively, if you cannot inherit from `EngagementActivity` then you must add `.StartActivity` and `.EndActivity` methods in `OnResume` and `OnPause` respectively.</span></span>  

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

## <span data-ttu-id="cc557-146"><a id="monitor"></a>Подключение приложения с возможностью его отслеживания в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="cc557-146"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="cc557-147"><a id="integrate-push"></a>Включение функции отправки и приема push-уведомлений и обмена сообщениями в приложении</span><span class="sxs-lookup"><span data-stu-id="cc557-147"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="cc557-148">Mobile Engagement позволяет вам toointeract с и доступа пользователей с push-уведомления и сообщения в контексте hello кампаний в приложения.</span><span class="sxs-lookup"><span data-stu-id="cc557-148">Mobile Engagement allows you toointeract with and REACH your users with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="cc557-149">Этот модуль вызывается REACH на портале мобильного охвата hello.</span><span class="sxs-lookup"><span data-stu-id="cc557-149">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="cc557-150">Hello в следующих разделах Настройка вашего приложения tooreceive их.</span><span class="sxs-lookup"><span data-stu-id="cc557-150">hello following sections sets up your app tooreceive them.</span></span>

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
