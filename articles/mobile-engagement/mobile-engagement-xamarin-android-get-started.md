---
title: "Начало работы со Службами мобильного взаимодействия Azure для Xamarin.Android"
description: "Узнайте, как использовать Службы мобильного взаимодействия Azure с аналитическими функциями и push-уведомлениями для приложений Xamarin.Android."
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
ms.openlocfilehash: 7b3d01b32c2d5a40448fc22861cd45f612238f2f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinandroid-apps"></a><span data-ttu-id="56a0d-103">Начало работы со Службами мобильного взаимодействия Azure для приложений Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="56a0d-103">Get Started with Azure Mobile Engagement for Xamarin.Android Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="56a0d-104">В этой статье показано, как применять Службы мобильного взаимодействия Azure для анализа использования приложения и как отправлять push-уведомления сегментированным пользователям приложения Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="56a0d-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and how to send push notifications to segmented users of a Xamarin.Android application.</span></span>
<span data-ttu-id="56a0d-105">В этом учебнике описывается простой сценарий вещания с использованием Служб мобильного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="56a0d-105">This tutorial demonstrates the simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="56a0d-106">В рассматриваемом сценарии создается пустое приложение Xamarin.Android, которое собирает основные данные и получает push-уведомления с помощью службы Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="56a0d-106">In it, you create a blank Xamarin.Android app that collects basic data and receives push notifications using Google Cloud Messaging (GCM).</span></span>

> [!NOTE]
> <span data-ttu-id="56a0d-107">Мы прекратим использование Служб мобильного взаимодействия Azure в марте 2018 г. Сейчас они доступны только существующим клиентам.</span><span class="sxs-lookup"><span data-stu-id="56a0d-107">The Azure Mobile Engagement service will be retired March 2018 and is currently only available to existing customers.</span></span> <span data-ttu-id="56a0d-108">Дополнительные сведения см. на странице [Службы мобильного взаимодействия](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="56a0d-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="56a0d-109">Для работы с данным учебником требуется следующее:</span><span class="sxs-lookup"><span data-stu-id="56a0d-109">This tutorial requires the following:</span></span>

* <span data-ttu-id="56a0d-110">[Xamarin Studio](http://xamarin.com/studio).</span><span class="sxs-lookup"><span data-stu-id="56a0d-110">[Xamarin Studio](http://xamarin.com/studio).</span></span> <span data-ttu-id="56a0d-111">Вы также можете использовать Visual Studio с расширением Xamarin, но в этом руководстве используется Xamarin Studio.</span><span class="sxs-lookup"><span data-stu-id="56a0d-111">You can also use Visual Studio with Xamarin but this tutorial uses Xamarin Studio.</span></span> <span data-ttu-id="56a0d-112">Инструкции см. в руководстве по [установке и настройке Visual Studio и Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="56a0d-112">For installation instructions, see [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>
* [<span data-ttu-id="56a0d-113">пакет Xamarin SDK для Служб мобильного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="56a0d-113">Mobile Engagement Xamarin SDK</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> <span data-ttu-id="56a0d-114">Для работы с этим учебником необходима активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="56a0d-114">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="56a0d-115">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="56a0d-115">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="56a0d-116">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="56a0d-116">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started).</span></span>
> 
> 

## <span data-ttu-id="56a0d-117"><a id="setup-azme"></a>Настройка Служб мобильного взаимодействия для вашего приложения Android</span><span class="sxs-lookup"><span data-stu-id="56a0d-117"><a id="setup-azme"></a>Setup Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="56a0d-118"><a id="connecting-app"></a>Подключение приложения к серверной части Служб мобильного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="56a0d-118"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="56a0d-119">В этом руководстве описаны действия по базовой интеграции, т. е. минимум, необходимый для сбора данных и отправки push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="56a0d-119">This tutorial presents a "basic integration", which is the minimal set required to collect data and send a push notification.</span></span> 

<span data-ttu-id="56a0d-120">Мы создадим базовое приложение в Xamarin Studio, чтобы продемонстрировать интеграцию.</span><span class="sxs-lookup"><span data-stu-id="56a0d-120">We will create a basic app with Xamarin Studio to demonstrate the integration.</span></span>

### <a name="create-a-new-xamarinandroid-project"></a><span data-ttu-id="56a0d-121">Создание нового проекта Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="56a0d-121">Create a new Xamarin.Android project</span></span>
1. <span data-ttu-id="56a0d-122">Запустите **Xamarin Studio**. Щелкните **File** -> **New** -> **Solution** (Файл -> Создать -> Решение).</span><span class="sxs-lookup"><span data-stu-id="56a0d-122">Launch **Xamarin Studio** Go to **File** -> **New** -> **Solution**</span></span> 
   
    ![][1]
2. <span data-ttu-id="56a0d-123">Выберите **Android App** (Приложение Android), а затем выберите язык **C#** и нажмите кнопку **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="56a0d-123">Select **Android App** then make sure the selected language is **C#** and click **Next**.</span></span>
   
    ![][2]
3. <span data-ttu-id="56a0d-124">Заполните поля **App Name** (Имя приложения) и **Organization Identifier** (Идентификатор организации).</span><span class="sxs-lookup"><span data-stu-id="56a0d-124">Fill in the **App Name** and the **Organization Identifier**.</span></span> <span data-ttu-id="56a0d-125">Установите флажок **Google Play Services** (Службы Google Play) и нажмите кнопку **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="56a0d-125">Make sure to checkmark **Google Play Services** and then click **Next**.</span></span> 
   
    ![][3]
4. <span data-ttu-id="56a0d-126">Если требуется, обновите значения в полях **Project Name** (Имя проекта), **Solution Name** (Имя решения) и **Location** (Расположение), а затем нажмите кнопку **Create** (Создать).</span><span class="sxs-lookup"><span data-stu-id="56a0d-126">Update the **Project Name**, **Solution Name** and **Location** if required and click **Create**.</span></span>
   
    ![][4]

<span data-ttu-id="56a0d-127">Xamarin Studio создаст приложение, в которое мы интегрируем Службы мобильного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="56a0d-127">Xamarin Studio will create the app in which we will integrate Mobile Engagement.</span></span> 

### <a name="connect-your-app-to-mobile-engagement-backend"></a><span data-ttu-id="56a0d-128">Подключение приложения к серверной части Служб мобильного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="56a0d-128">Connect your app to Mobile Engagement backend</span></span>
1. <span data-ttu-id="56a0d-129">В окне решения правой кнопкой мыши щелкните папку **Packages** (Пакеты) и выберите пункт **Add Packages...** (Добавить пакеты).</span><span class="sxs-lookup"><span data-stu-id="56a0d-129">Right click the **Packages** folder in the Solution windows and select **Add Packages...**</span></span>
   
    ![][5]
2. <span data-ttu-id="56a0d-130">Найдите пакет **Xamarin SDK для Служб мобильного взаимодействия Microsoft Azure** и добавьте его в свое решение.</span><span class="sxs-lookup"><span data-stu-id="56a0d-130">Search for the **Microsoft Azure Mobile Engagement Xamarin SDK** and add it to your solution.</span></span>  
   
    ![][6]
3. <span data-ttu-id="56a0d-131">Откройте файл **MainActivity.cs** и добавьте следующие инструкции using:</span><span class="sxs-lookup"><span data-stu-id="56a0d-131">Open **MainActivity.cs** and add the following using statements:</span></span>
   
        using Microsoft.Azure.Engagement;
        using Microsoft.Azure.Engagement.Activity;
4. <span data-ttu-id="56a0d-132">В метод `OnCreate` добавьте следующую команду, чтобы инициализировать подключение к внутреннему серверу Служб мобильного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="56a0d-132">In the `OnCreate` method, add the following to initialize the connection with Mobile Engagement backend.</span></span> <span data-ttu-id="56a0d-133">Обязательно добавьте **строку подключения**.</span><span class="sxs-lookup"><span data-stu-id="56a0d-133">Make sure to add your **ConnectionString**.</span></span> 
   
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.ConnectionString = "YourConnectionStringFromAzurePortal";
        EngagementAgent.Init(engagementConfiguration);

### <a name="add-permissions-and-a-service-declaration"></a><span data-ttu-id="56a0d-134">Добавление разрешений и объявления службы</span><span class="sxs-lookup"><span data-stu-id="56a0d-134">Add permissions and a service declaration</span></span>
1. <span data-ttu-id="56a0d-135">Откройте файл **Manifest.xml** в папке Properties (Свойства).</span><span class="sxs-lookup"><span data-stu-id="56a0d-135">Open up the **Manifest.xml** file under the Properties folder.</span></span> <span data-ttu-id="56a0d-136">Перейдите на вкладку Source (Источник), чтобы напрямую обновить источник XML.</span><span class="sxs-lookup"><span data-stu-id="56a0d-136">Select Source tab so that you directly update the XML source.</span></span>
2. <span data-ttu-id="56a0d-137">Добавьте эти разрешения в файл Manifest.xml (который можно найти в папке **Properties** (Свойства)) проекта непосредственно перед тегом `<application>` или после него:</span><span class="sxs-lookup"><span data-stu-id="56a0d-137">Add these permissions to the Manifest.xml (which can be found under the **Properties** folder) of your project immediately before or after the `<application>` tag:</span></span>
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
3. <span data-ttu-id="56a0d-138">Добавьте следующий код между тегами `<application>` и `</application>`, чтобы объявить службу агента:</span><span class="sxs-lookup"><span data-stu-id="56a0d-138">Add the following between the `<application>` and `</application>` tags to declare the agent service:</span></span>
   
        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
4. <span data-ttu-id="56a0d-139">В только что вставленном коде замените `"<Your application name>"` в метке фактическим значением.</span><span class="sxs-lookup"><span data-stu-id="56a0d-139">In the code you just pasted, replace `"<Your application name>"` in the label.</span></span> <span data-ttu-id="56a0d-140">Это имя появится в меню **Параметры** , где отображены службы, работающие на устройстве пользователя.</span><span class="sxs-lookup"><span data-stu-id="56a0d-140">This is displayed in the **Settings** menu where users can see services running on the device.</span></span> <span data-ttu-id="56a0d-141">Вы можете добавить в метку слово, например Service (служба).</span><span class="sxs-lookup"><span data-stu-id="56a0d-141">You can add the word "Service" in that label for example.</span></span>

### <a name="send-a-screen-to-mobile-engagement"></a><span data-ttu-id="56a0d-142">Отправка экрана в Службы мобильного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="56a0d-142">Send a screen to Mobile Engagement</span></span>
<span data-ttu-id="56a0d-143">Чтобы начать отправку данных и убедиться, что пользователи активны, отправьте по крайней мере один экран на внутренний сервер Служб мобильного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="56a0d-143">In order to start sending data and ensuring the users are active, you must send at least one screen to the Mobile Engagement backend.</span></span> <span data-ttu-id="56a0d-144">Для этого убедитесь, что `MainActivity` наследуется от `EngagementActivity`, а не от `Activity`.</span><span class="sxs-lookup"><span data-stu-id="56a0d-144">For doing this - ensure that the `MainActivity` inherits from `EngagementActivity` instead of `Activity`.</span></span>

    public class MainActivity : EngagementActivity

<span data-ttu-id="56a0d-145">Если наследование от `EngagementActivity` невозможно, необходимо добавить методы `.StartActivity` и `.EndActivity` в `OnResume` и `OnPause` соответственно.</span><span class="sxs-lookup"><span data-stu-id="56a0d-145">Alternatively, if you cannot inherit from `EngagementActivity` then you must add `.StartActivity` and `.EndActivity` methods in `OnResume` and `OnPause` respectively.</span></span>  

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

## <span data-ttu-id="56a0d-146"><a id="monitor"></a>Подключение приложения с возможностью его отслеживания в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="56a0d-146"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="56a0d-147"><a id="integrate-push"></a>Включение push-уведомлений и обмена сообщениями в приложении</span><span class="sxs-lookup"><span data-stu-id="56a0d-147"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="56a0d-148">Службы мобильного взаимодействия позволяют взаимодействовать и СВЯЗЫВАТЬСЯ с пользователями с помощью push-уведомлений и сообщений в приложении в контексте кампаний.</span><span class="sxs-lookup"><span data-stu-id="56a0d-148">Mobile Engagement allows you to interact with and REACH your users with push notifications and in-app messaging in the context of campaigns.</span></span> <span data-ttu-id="56a0d-149">На портале Служб мобильного взаимодействия этот модуль называется МОДУЛЕМ ОБРАБОТКИ РЕКЛАМНЫХ КАМПАНИЙ.</span><span class="sxs-lookup"><span data-stu-id="56a0d-149">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="56a0d-150">В следующих разделах показано, как настроить приложение для приема уведомлений и сообщений.</span><span class="sxs-lookup"><span data-stu-id="56a0d-150">The following sections sets up your app to receive them.</span></span>

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
