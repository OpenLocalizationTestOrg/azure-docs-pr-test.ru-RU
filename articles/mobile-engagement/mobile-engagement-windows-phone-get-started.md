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
# <a name="get-started-with-azure-mobile-engagement-for-windows-phone-silverlight-apps"></a><span data-ttu-id="a23b9-103">Приступая к работе со Службами мобильного взаимодействия Azure для приложений Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="a23b9-103">Get started with Azure Mobile Engagement for Windows Phone Silverlight apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="a23b9-104">В этом разделе показано, как Azure Mobile Engagement toounderstand toouse использования приложений и отправлять push-уведомления пользователей toosegmented приложения Windows Phone Silverlight.</span><span class="sxs-lookup"><span data-stu-id="a23b9-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users of a Windows Phone Silverlight application.</span></span>
<span data-ttu-id="a23b9-105">В этом учебнике показано hello простой широковещательных сценарий с помощью мобильного охвата.</span><span class="sxs-lookup"><span data-stu-id="a23b9-105">This tutorial demonstrates hello simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="a23b9-106">Здесь вы создадите пустое приложение Windows Phone Silverlight, которое будет собирать основные данные и получать push-уведомления, используя службу push-уведомлений (Майкрософт) (MPNS).</span><span class="sxs-lookup"><span data-stu-id="a23b9-106">In it, you create a blank Windows Phone Silverlight app that collects basic data and receives push notifications using Microsoft Push Notification Service (MPNS).</span></span>

> [!NOTE]
> <span data-ttu-id="a23b9-107">Служба Azure Mobile Engagement Hello будет прекращено 2018 марта и в настоящее время только доступные tooexisting клиентов.</span><span class="sxs-lookup"><span data-stu-id="a23b9-107">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="a23b9-108">Дополнительные сведения см. на странице [Службы мобильного взаимодействия](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="a23b9-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

> [!NOTE]
> <span data-ttu-id="a23b9-109">Проекты для версии Windows Phone 8.1 и более ранних версий не поддерживаются в Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="a23b9-109">Windows Phone 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="a23b9-110">Дополнительные сведения см. в статье [Целевая платформа и совместимость для Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="a23b9-110">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

> [!NOTE]
> <span data-ttu-id="a23b9-111">Если вы используете Windows Phone 8.1 (отличных от Silverlight), см. toohello [Windows Universal учебника](mobile-engagement-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a23b9-111">If you are targeting Windows Phone 8.1 (non-Silverlight), refer toohello [Windows Universal tutorial](mobile-engagement-windows-store-dotnet-get-started.md).</span></span>
> 
> 

<span data-ttu-id="a23b9-112">Этот учебник требует hello следующее:</span><span class="sxs-lookup"><span data-stu-id="a23b9-112">This tutorial requires hello following:</span></span>

* <span data-ttu-id="a23b9-113">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="a23b9-113">Visual Studio 2013</span></span>
* <span data-ttu-id="a23b9-114">[MicrosoftAzure.MobileEngagement] </span><span class="sxs-lookup"><span data-stu-id="a23b9-114">[MicrosoftAzure.MobileEngagement] Nuget package</span></span>

> [!NOTE]
> <span data-ttu-id="a23b9-115">toocomplete этого учебника необходимо иметь активную учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="a23b9-115">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="a23b9-116">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="a23b9-116">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="a23b9-117">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-windows-phone-get-started).</span><span class="sxs-lookup"><span data-stu-id="a23b9-117">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-windows-phone-get-started).</span></span>
> 
> 

## <span data-ttu-id="a23b9-118"><a id="setup-azme">
            </a>Настройка Служб мобильного взаимодействия для приложения Windows Phone</span><span class="sxs-lookup"><span data-stu-id="a23b9-118"><a id="setup-azme"></a>Setup Mobile Engagement for your Windows Phone app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="a23b9-119"><a id="connecting-app"></a>Подключение мобильного охвата toohello внутренний сервер приложений</span><span class="sxs-lookup"><span data-stu-id="a23b9-119"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="a23b9-120">В этом руководстве содержатся «базовой интеграции», который hello минимальный набор данных требуется toocollect и отправить push-уведомление.</span><span class="sxs-lookup"><span data-stu-id="a23b9-120">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="a23b9-121">Hello полной интеграции документацию можно найти в hello [интеграции пакета SDK для Windows Phone Mobile Engagement](mobile-engagement-windows-phone-sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="a23b9-121">hello complete integration documentation can be found in hello [Mobile Engagement Windows Phone SDK integration](mobile-engagement-windows-phone-sdk-overview.md)</span></span>

<span data-ttu-id="a23b9-122">Мы создадим простое приложение с помощью Visual Studio toodemonstrate hello интеграции.</span><span class="sxs-lookup"><span data-stu-id="a23b9-122">We will create a basic app with Visual Studio toodemonstrate hello integration.</span></span>

### <a name="create-a-new-windows-phone-silverlight-project"></a><span data-ttu-id="a23b9-123">Создание проекта для Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="a23b9-123">Create a new Windows Phone Silverlight project</span></span>
<span data-ttu-id="a23b9-124">Hello следующие шаги предполагают использование Visual Studio 2015 hello хотя hello действия схожи в более ранних версиях Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a23b9-124">hello following steps assume hello use of Visual Studio 2015 though hello steps are similar in earlier versions of Visual Studio.</span></span> 

1. <span data-ttu-id="a23b9-125">Запустите Visual Studio и в hello **Главная** выберите **новый проект**.</span><span class="sxs-lookup"><span data-stu-id="a23b9-125">Start Visual Studio, and in hello **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="a23b9-126">Во всплывающем hello выберите **Windows 8** -> **Windows Phone** -> **пустое приложение (Windows Phone Silverlight)**.</span><span class="sxs-lookup"><span data-stu-id="a23b9-126">In hello pop-up, select **Windows 8** -> **Windows Phone** -> **Blank App (Windows Phone Silverlight)**.</span></span> <span data-ttu-id="a23b9-127">Заполните приложение hello **имя** и **имя решения**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a23b9-127">Fill in hello app **Name** and **Solution name**, and then click **OK**.</span></span>
   
    ![][1]
3. <span data-ttu-id="a23b9-128">Можно выбрать либо tootarget **Windows Phone 8.0** или **Windows Phone 8.1**.</span><span class="sxs-lookup"><span data-stu-id="a23b9-128">You can choose tootarget either **Windows Phone 8.0** or **Windows Phone 8.1**.</span></span>

<span data-ttu-id="a23b9-129">Вы создали нового приложения Windows Phone Silverlight, в которую будет интегрировать hello Azure Mobile Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="a23b9-129">You have now created a new Windows Phone Silverlight app into which we will integrate hello Azure Mobile Engagement SDK.</span></span>

### <a name="connect-your-app-toohello-mobile-engagement-backend"></a><span data-ttu-id="a23b9-130">Подключение мобильного охвата toohello внутренний сервер приложений</span><span class="sxs-lookup"><span data-stu-id="a23b9-130">Connect your app toohello Mobile Engagement backend</span></span>
1. <span data-ttu-id="a23b9-131">Установка hello [MicrosoftAzure.MobileEngagement] пакета nuget в проекте.</span><span class="sxs-lookup"><span data-stu-id="a23b9-131">Install hello [MicrosoftAzure.MobileEngagement] nuget package in your project.</span></span>
2. <span data-ttu-id="a23b9-132">Откройте `WMAppManifest.xml` (папке hello свойства) и убедитесь, что объявлены следующие hello (добавить их, если они не являются) в hello `<Capabilities />` тег:</span><span class="sxs-lookup"><span data-stu-id="a23b9-132">Open `WMAppManifest.xml` (under hello Properties folder) and make sure hello following are declared (add them if they are not) in hello `<Capabilities />` tag:</span></span>
   
        <Capability Name="ID_CAP_NETWORKING" />
        <Capability Name="ID_CAP_IDENTITY_DEVICE" />
   
    ![][2]
3. <span data-ttu-id="a23b9-133">Теперь вставьте строку подключения hello, скопированное ранее для приложения Mobile Engagement и вставьте его в hello `Resources\EngagementConfiguration.xml` файла между hello `<connectionString>` и `</connectionString>` теги:</span><span class="sxs-lookup"><span data-stu-id="a23b9-133">Now paste hello connection string that you copied earlier for your Mobile Engagement app and paste it in hello `Resources\EngagementConfiguration.xml` file, between hello `<connectionString>` and `</connectionString>` tags:</span></span>
   
    ![][3]
4. <span data-ttu-id="a23b9-134">В hello `App.xaml.cs` файла:</span><span class="sxs-lookup"><span data-stu-id="a23b9-134">In hello `App.xaml.cs` file:</span></span>
   
    <span data-ttu-id="a23b9-135">а.</span><span class="sxs-lookup"><span data-stu-id="a23b9-135">a.</span></span> <span data-ttu-id="a23b9-136">Добавить hello `using` инструкции:</span><span class="sxs-lookup"><span data-stu-id="a23b9-136">Add hello `using` statement:</span></span>
   
            using Microsoft.Azure.Engagement;
   
    <span data-ttu-id="a23b9-137">b.</span><span class="sxs-lookup"><span data-stu-id="a23b9-137">b.</span></span> <span data-ttu-id="a23b9-138">Инициализировать hello SDK в hello `Application_Launching` метод:</span><span class="sxs-lookup"><span data-stu-id="a23b9-138">Initialize hello SDK in hello `Application_Launching` method:</span></span>
   
            private void Application_Launching(object sender, LaunchingEventArgs e)
            {
              EngagementAgent.Instance.Init();
            }
   
    <span data-ttu-id="a23b9-139">c.</span><span class="sxs-lookup"><span data-stu-id="a23b9-139">c.</span></span> <span data-ttu-id="a23b9-140">Вставьте следующие hello в hello `Application_Activated`:</span><span class="sxs-lookup"><span data-stu-id="a23b9-140">Insert hello following in hello `Application_Activated`:</span></span>
   
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
               EngagementAgent.Instance.OnActivated(e);
            }

## <span data-ttu-id="a23b9-141"><a id="monitor"></a>Включение мониторинга в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="a23b9-141"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="a23b9-142">В toostart порядок отправки данных и убедитесь, что пользователи hello active необходимо отправить по крайней мере один внутреннего сервера мобильного охвата toohello экрана (действие).</span><span class="sxs-lookup"><span data-stu-id="a23b9-142">In order toostart sending data and ensuring that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="a23b9-143">Добавьте в hello MainPage.xaml.cs hello `using` инструкции:</span><span class="sxs-lookup"><span data-stu-id="a23b9-143">In hello MainPage.xaml.cs, add hello `using` statement:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="a23b9-144">Замените hello базовый класс **MainPage**, который предшествует **PhoneApplicationPage**, с **EngagementPage**.</span><span class="sxs-lookup"><span data-stu-id="a23b9-144">Replace hello base class of **MainPage**, which is before **PhoneApplicationPage**, with **EngagementPage**.</span></span>
   
        class MainPage : EngagementPage 
3. <span data-ttu-id="a23b9-145">В файле `MainPage.xml`:</span><span class="sxs-lookup"><span data-stu-id="a23b9-145">In your `MainPage.xml` file:</span></span>
   
    <span data-ttu-id="a23b9-146">а.</span><span class="sxs-lookup"><span data-stu-id="a23b9-146">a.</span></span> <span data-ttu-id="a23b9-147">Добавьте tooyour объявления пространств имен:</span><span class="sxs-lookup"><span data-stu-id="a23b9-147">Add tooyour namespaces declarations:</span></span>
   
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
   
    <span data-ttu-id="a23b9-148">b.</span><span class="sxs-lookup"><span data-stu-id="a23b9-148">b.</span></span> <span data-ttu-id="a23b9-149">Замените `phone:PhoneApplicationPage` в имени XML-тега hello с `engagement:EngagementPage`.</span><span class="sxs-lookup"><span data-stu-id="a23b9-149">Replace `phone:PhoneApplicationPage` in hello XML tag name with `engagement:EngagementPage`.</span></span>

## <span data-ttu-id="a23b9-150"><a id="monitor"></a>Подключение приложения с возможностью его отслеживания в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="a23b9-150"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="a23b9-151"><a id="integrate-push"></a>Включение функции отправки и приема push-уведомлений и обмена сообщениями в приложении</span><span class="sxs-lookup"><span data-stu-id="a23b9-151"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="a23b9-152">Mobile Engagement позволяет вам toointeract и доступа пользователей с Push-уведомления и обмен сообщениями в приложении в контексте hello кампаний.</span><span class="sxs-lookup"><span data-stu-id="a23b9-152">Mobile Engagement allows you toointeract and reach your users with Push Notifications and in-app Messaging in hello context of campaigns.</span></span> <span data-ttu-id="a23b9-153">Этот модуль вызывается REACH на портале мобильного охвата hello.</span><span class="sxs-lookup"><span data-stu-id="a23b9-153">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="a23b9-154">Hello следующих разделах Настройка вашего приложения tooreceive их.</span><span class="sxs-lookup"><span data-stu-id="a23b9-154">hello following sections set up your app tooreceive them.</span></span>

### <a name="enable-your-app-tooreceive-mpns-push-notifications"></a><span data-ttu-id="a23b9-155">Включить вашего приложения tooreceive Push-уведомления MPNS</span><span class="sxs-lookup"><span data-stu-id="a23b9-155">Enable your app tooreceive MPNS Push Notifications</span></span>
<span data-ttu-id="a23b9-156">Добавить новые возможности tooyour `WMAppManifest.xml` файла:</span><span class="sxs-lookup"><span data-stu-id="a23b9-156">Add new Capabilities tooyour `WMAppManifest.xml` file:</span></span>

        ID_CAP_PUSH_NOTIFICATION
        ID_CAP_WEBBROWSERCOMPONENT

   ![][5]

### <a name="initialize-hello-reach-sdk"></a><span data-ttu-id="a23b9-157">Инициализировать hello пакет SDK для REACH</span><span class="sxs-lookup"><span data-stu-id="a23b9-157">Initialize hello REACH SDK</span></span>
1. <span data-ttu-id="a23b9-158">В `App.xaml.cs`, вызовите `EngagementReach.Instance.Init();` в hello **Application_Launching** функция сразу же после инициализации агента hello:</span><span class="sxs-lookup"><span data-stu-id="a23b9-158">In `App.xaml.cs`, call `EngagementReach.Instance.Init();` in hello **Application_Launching** function, right after hello agent initialization:</span></span>
   
        private void Application_Launching(object sender, LaunchingEventArgs e)
        {
           EngagementAgent.Instance.Init();
           EngagementReach.Instance.Init();
        }
2. <span data-ttu-id="a23b9-159">В `App.xaml.cs`, вызовите `EngagementReach.Instance.OnActivated(e);` в hello **Application_Activated** функция сразу же после инициализации агента hello:</span><span class="sxs-lookup"><span data-stu-id="a23b9-159">In `App.xaml.cs`, call `EngagementReach.Instance.OnActivated(e);` in hello **Application_Activated** function, right after hello agent initialization:</span></span>
   
        private void Application_Activated(object sender, ActivatedEventArgs e)
        {
           EngagementAgent.Instance.OnActivated(e);
           EngagementReach.Instance.OnActivated(e);
        }

<span data-ttu-id="a23b9-160">Все готово.</span><span class="sxs-lookup"><span data-stu-id="a23b9-160">You're all set.</span></span> <span data-ttu-id="a23b9-161">Теперь убедимся, что базовая интеграция выполнена правильно.</span><span class="sxs-lookup"><span data-stu-id="a23b9-161">Now we will verify that you have correctly cried out this basic integration.</span></span>

## <span data-ttu-id="a23b9-162"><a id="send"></a>Отправить уведомление о tooyour приложение</span><span class="sxs-lookup"><span data-stu-id="a23b9-162"><a id="send"></a>Send a notification tooyour app</span></span>
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

<span data-ttu-id="a23b9-163">Вы увидите уведомление на вашем устройстве, на котором будут отображаться как уведомление в приложении Если приложение hello еще открыт, в противном случае значение в виде всплывающих уведомлений hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a23b9-163">You should now see a notification on your device which will show up as an in-app notification if hello app is open otherwise as a toast notification like hello following:</span></span> 

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
