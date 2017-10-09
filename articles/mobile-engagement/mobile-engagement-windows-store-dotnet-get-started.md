---
title: "aaaGet к работе с Windows универсальных приложений Azure Mobile Engagement"
description: "Узнайте, как toouse Azure Mobile Engagement с анализа и отправка уведомлений для универсальных приложений Windows."
services: mobile-engagement
documentationcenter: windows
author: piyushjo
manager: erikre
editor: 
ms.assetid: 48103867-7f64-4646-b019-42bd797d38e2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 8224a6d3789cfe4784bbc9472005f9eddb94a8b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-universal-apps"></a><span data-ttu-id="6720f-103">Приступая к работе со Службами мобильного взаимодействия Azure для универсальных приложений для Windows</span><span class="sxs-lookup"><span data-stu-id="6720f-103">Get started with Azure Mobile Engagement for Windows Universal Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="6720f-104">В этом разделе показано, как Azure Mobile Engagement toounderstand toouse использования приложений и отправлять push-уведомления пользователей toosegmented универсальное приложение для Windows приложения.</span><span class="sxs-lookup"><span data-stu-id="6720f-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users of a Windows Universal application.</span></span>
<span data-ttu-id="6720f-105">В этом учебнике показано hello простой широковещательных сценарий с помощью мобильного охвата.</span><span class="sxs-lookup"><span data-stu-id="6720f-105">This tutorial demonstrates hello simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="6720f-106">Вы создадите пустое универсальное приложение для Windows, которое будет собирать основные данные об использовании приложений и получать push-уведомления, используя службу push-уведомлений Windows (WNS).</span><span class="sxs-lookup"><span data-stu-id="6720f-106">You create a blank Windows Universal App that collects basic app usage data and receives push notifications using Windows Notification Service (WNS).</span></span>

> [!NOTE]
> <span data-ttu-id="6720f-107">Служба Azure Mobile Engagement Hello будет прекращено 2018 марта и в настоящее время только доступные tooexisting клиентов.</span><span class="sxs-lookup"><span data-stu-id="6720f-107">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="6720f-108">Дополнительные сведения см. на странице [Службы мобильного взаимодействия](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="6720f-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6720f-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6720f-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="set-up-mobile-engagement-for-your-windows-universal-app"></a><span data-ttu-id="6720f-110">Настройка Служб мобильного взаимодействия для универсального приложения для Windows</span><span class="sxs-lookup"><span data-stu-id="6720f-110">Set up Mobile Engagement for your Windows Universal app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="6720f-111"><a id="connecting-app"></a>Подключение мобильного охвата toohello внутренний сервер приложений</span><span class="sxs-lookup"><span data-stu-id="6720f-111"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="6720f-112">В этом руководстве содержатся «базовой интеграции служб, «hello минимальный набор данных требуется toocollect и отправить push-уведомление.</span><span class="sxs-lookup"><span data-stu-id="6720f-112">This tutorial presents a "basic integration," which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="6720f-113">Hello полной интеграции документацию можно найти в hello [интеграции Windows Mobile Engagement SDK универсальной](mobile-engagement-windows-store-sdk-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6720f-113">hello complete integration documentation can be found in hello [Mobile Engagement Windows Universal SDK integration](mobile-engagement-windows-store-sdk-overview.md).</span></span>

<span data-ttu-id="6720f-114">Создать простое приложение с помощью Visual Studio toodemonstrate hello интеграции.</span><span class="sxs-lookup"><span data-stu-id="6720f-114">You create a basic app with Visual Studio toodemonstrate hello integration.</span></span>

### <a name="create-a-windows-universal-app-project"></a><span data-ttu-id="6720f-115">Создание проекта универсального приложения для Windows</span><span class="sxs-lookup"><span data-stu-id="6720f-115">Create a Windows Universal App project</span></span>
<span data-ttu-id="6720f-116">Hello следующие шаги предполагают использование Visual Studio 2015 hello хотя hello действия схожи в более ранних версиях Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6720f-116">hello following steps assume hello use of Visual Studio 2015 though hello steps are similar in earlier versions of Visual Studio.</span></span>

1. <span data-ttu-id="6720f-117">Запустите Visual Studio и в hello **Главная** выберите **новый проект**.</span><span class="sxs-lookup"><span data-stu-id="6720f-117">Start Visual Studio, and in hello **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="6720f-118">Во всплывающем hello выберите **Windows** -> **универсальной** -> **пустое приложение (универсальные приложения Windows)**.</span><span class="sxs-lookup"><span data-stu-id="6720f-118">In hello pop-up, select **Windows** -> **Universal** -> **Blank App (Universal Windows)**.</span></span> <span data-ttu-id="6720f-119">Заполните приложение hello **имя** и **имя решения**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="6720f-119">Fill in hello app **Name** and **Solution name**, and then click **OK**.</span></span>

    ![][1]

<span data-ttu-id="6720f-120">Вы создали проект универсального приложения Windows, в которую затем интегрировать hello Azure Mobile Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="6720f-120">You have now created a Windows Universal App project into which you next integrate hello Azure Mobile Engagement SDK.</span></span>

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="6720f-121">Подключение Engagement tooMobile внутренний сервер приложений</span><span class="sxs-lookup"><span data-stu-id="6720f-121">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="6720f-122">Установка hello [MicrosoftAzure.MobileEngagement] пакета Nuget в проекте.</span><span class="sxs-lookup"><span data-stu-id="6720f-122">Install hello [MicrosoftAzure.MobileEngagement] Nuget package in your project.</span></span> <span data-ttu-id="6720f-123">Если вы используете платформ Windows и Windows Phone, toodo это необходимо для обоих проектов.</span><span class="sxs-lookup"><span data-stu-id="6720f-123">If you are targeting both Windows and Windows Phone platforms, you need toodo this for both projects.</span></span> <span data-ttu-id="6720f-124">Для Windows 8.x и Windows Phone 8.1, hello те же Nuget пакета местах hello правильный платформой двоичные файлы в каждом проекте.</span><span class="sxs-lookup"><span data-stu-id="6720f-124">For Windows 8.x and Windows Phone 8.1, hello same Nuget package places hello correct platform-specific binaries in each project.</span></span>
2. <span data-ttu-id="6720f-125">Откройте **Package.appxmanifest** и убедитесь, что существует добавлено, hello следующие возможности:</span><span class="sxs-lookup"><span data-stu-id="6720f-125">Open **Package.appxmanifest** and make sure that hello following capability is added there:</span></span>

        Internet (Client)

    ![][2]
3. <span data-ttu-id="6720f-126">Теперь скопируйте строку подключения hello, скопированное ранее для приложения Mobile Engagement и вставьте его в hello `Resources\EngagementConfiguration.xml` файла между hello `<connectionString>` и `</connectionString>` теги:</span><span class="sxs-lookup"><span data-stu-id="6720f-126">Now copy hello connection string that you copied earlier for your Mobile Engagement App and paste it in hello `Resources\EngagementConfiguration.xml` file, between hello `<connectionString>` and `</connectionString>` tags:</span></span>

    ![][3]

    > [!TIP]
    > <span data-ttu-id="6720f-127">Если приложение рассчитано как на платформу Windows, так и на Windows Phone, то следует создать два приложения Служб мобильного взаимодействия (по одному для каждой из поддерживаемых платформ).</span><span class="sxs-lookup"><span data-stu-id="6720f-127">If your App targets both Windows and Windows Phone platforms, you should still create two Mobile Engagement Applications - one for each supported platform.</span></span> <span data-ttu-id="6720f-128">Наличие двух приложений обеспечивает можно создать правильный сегментации hello аудитории и может отправлять соответствующие целевые уведомления для каждой платформы.</span><span class="sxs-lookup"><span data-stu-id="6720f-128">Having two apps ensures that you can create correct segmentation of hello audience and can send appropriately targeted notifications for each platform.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="6720f-129">NuGet не копирует автоматически ресурсов SDK hello в приложении Windows 10 UWP.</span><span class="sxs-lookup"><span data-stu-id="6720f-129">NuGet does not automatically copy hello SDK resources in your Windows 10 UWP application.</span></span> <span data-ttu-id="6720f-130">У вас есть toodo его вручную после hello шаги, которые отображаются при установке пакета Nuget hello (readme.txt).</span><span class="sxs-lookup"><span data-stu-id="6720f-130">You have toodo it manually following hello steps which show up (readme.txt) when hello Nuget package is installed.</span></span>  

1. <span data-ttu-id="6720f-131">В hello `App.xaml.cs` файла:</span><span class="sxs-lookup"><span data-stu-id="6720f-131">In hello `App.xaml.cs` file:</span></span>

    <span data-ttu-id="6720f-132">а.</span><span class="sxs-lookup"><span data-stu-id="6720f-132">a.</span></span> <span data-ttu-id="6720f-133">Добавить hello `using` инструкции:</span><span class="sxs-lookup"><span data-stu-id="6720f-133">Add hello `using` statement:</span></span>

            using Microsoft.Azure.Engagement;

    <span data-ttu-id="6720f-134">b.</span><span class="sxs-lookup"><span data-stu-id="6720f-134">b.</span></span> <span data-ttu-id="6720f-135">Добавьте метод, который инициализирует hello участия:</span><span class="sxs-lookup"><span data-stu-id="6720f-135">Add a method that initializes hello Engagement:</span></span>

           private void InitEngagement(IActivatedEventArgs e)
           {
             EngagementAgent.Instance.Init(e);

             //... rest of hello code
           }

    <span data-ttu-id="6720f-136">c.</span><span class="sxs-lookup"><span data-stu-id="6720f-136">c.</span></span> <span data-ttu-id="6720f-137">Инициализировать hello SDK в hello **OnLaunched** метод:</span><span class="sxs-lookup"><span data-stu-id="6720f-137">Initialize hello SDK in hello **OnLaunched** method:</span></span>

            protected override void OnLaunched(LaunchActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of hello code
            }

    <span data-ttu-id="6720f-138">c.</span><span class="sxs-lookup"><span data-stu-id="6720f-138">c.</span></span> <span data-ttu-id="6720f-139">Вставьте следующие hello в hello **OnActivated** метода и добавьте метод hello в том случае, если он еще не:</span><span class="sxs-lookup"><span data-stu-id="6720f-139">Insert hello following in hello **OnActivated** method and add hello method if it is not already present:</span></span>

            protected override void OnActivated(IActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of hello code
            }

## <span data-ttu-id="6720f-140"><a id="monitor"></a>Включение мониторинга в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="6720f-140"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="6720f-141">toostart отправляет данные и обеспечить hello пользователей активны, необходимо отправить по крайней мере один внутреннего сервера мобильного охвата toohello экрана (действие).</span><span class="sxs-lookup"><span data-stu-id="6720f-141">toostart sending data and ensuring that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="6720f-142">В hello **MainPage.xaml.cs**, добавьте следующее hello `using` инструкции:</span><span class="sxs-lookup"><span data-stu-id="6720f-142">In hello **MainPage.xaml.cs**, add hello following `using` statement:</span></span>

    <span data-ttu-id="6720f-143">с помощью Microsoft.Azure.Engagement.Overlay.</span><span class="sxs-lookup"><span data-stu-id="6720f-143">using Microsoft.Azure.Engagement.Overlay;</span></span>
2. <span data-ttu-id="6720f-144">Измените базовый класс hello объекта **MainPage** из **страницы** слишком**EngagementPageOverlay**:</span><span class="sxs-lookup"><span data-stu-id="6720f-144">Change hello base class of **MainPage** from **Page** too**EngagementPageOverlay**:</span></span>

        class MainPage : EngagementPageOverlay
3. <span data-ttu-id="6720f-145">В hello `MainPage.xaml` файла:</span><span class="sxs-lookup"><span data-stu-id="6720f-145">In hello `MainPage.xaml` file:</span></span>

    <span data-ttu-id="6720f-146">а.</span><span class="sxs-lookup"><span data-stu-id="6720f-146">a.</span></span> <span data-ttu-id="6720f-147">Добавьте tooyour объявления пространств имен:</span><span class="sxs-lookup"><span data-stu-id="6720f-147">Add tooyour namespaces declarations:</span></span>

        xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"

    <span data-ttu-id="6720f-148">b.</span><span class="sxs-lookup"><span data-stu-id="6720f-148">b.</span></span> <span data-ttu-id="6720f-149">Замените hello **страницы** в имени XML-тега hello с **engagement: EngagementPageOverlay**</span><span class="sxs-lookup"><span data-stu-id="6720f-149">Replace hello **Page** in hello XML tag name with **engagement:EngagementPageOverlay**</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6720f-150">Если на странице переопределяет hello `OnNavigatedTo` метода будет убедиться, что toocall `base.OnNavigatedTo(e)`.</span><span class="sxs-lookup"><span data-stu-id="6720f-150">If your page overrides hello `OnNavigatedTo` method, be sure toocall `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="6720f-151">В противном случае hello не выводятся `EngagementPage` вызовы `StartActivity` внутри его `OnNavigatedTo` метода).</span><span class="sxs-lookup"><span data-stu-id="6720f-151">Otherwise, hello activity is not reported `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span> <span data-ttu-id="6720f-152">Это особенно важно в проекте Windows Phone, где есть шаблон по умолчанию hello `OnNavigatedTo` метод.</span><span class="sxs-lookup"><span data-stu-id="6720f-152">This is especially important in a Windows Phone project where hello default template has an `OnNavigatedTo` method.</span></span>
>
> <span data-ttu-id="6720f-153">Для **универсальных приложений Windows 10**, метод hello в hello рекомендуется использовать» рекомендуется использовать метод: перегружать классов страницы «раздел [Advanced отчетов с помощью пакета SDK Engagement универсальных приложений Windows hello](mobile-engagement-windows-store-advanced-reporting.md) , вместо того чтобы hello упомянутым выше.</span><span class="sxs-lookup"><span data-stu-id="6720f-153">For **Windows 10 Universal apps**, use hello method recommended in hello "Recommended method: overload your Page classes" section of [Advanced Reporting with hello Windows Universal Apps Engagement SDK](mobile-engagement-windows-store-advanced-reporting.md), rather than hello one mentioned above.</span></span>

## <span data-ttu-id="6720f-154"><a id="monitor"></a>Подключение приложения с возможностью его отслеживания в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="6720f-154"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="6720f-155"><a id="integrate-push"></a>Включение функции отправки и приема push-уведомлений и обмена сообщениями в приложении</span><span class="sxs-lookup"><span data-stu-id="6720f-155"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="6720f-156">Mobile Engagement позволяет вам toointeract и доступа пользователей с push-уведомления и сообщения в контексте hello кампаний в приложения.</span><span class="sxs-lookup"><span data-stu-id="6720f-156">Mobile Engagement allows you toointeract and reach your users with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="6720f-157">Этот модуль вызывается REACH на портале мобильного охвата hello.</span><span class="sxs-lookup"><span data-stu-id="6720f-157">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="6720f-158">Hello следующих разделах Настройка вашего приложения tooreceive их.</span><span class="sxs-lookup"><span data-stu-id="6720f-158">hello following sections set up your app tooreceive them.</span></span>

### <a name="enable-your-app-tooreceive-wns-push-notifications"></a><span data-ttu-id="6720f-159">Включить вашего приложения tooreceive Push-уведомления WNS</span><span class="sxs-lookup"><span data-stu-id="6720f-159">Enable your app tooreceive WNS Push Notifications</span></span>
1. <span data-ttu-id="6720f-160">В hello `Package.appxmanifest` файла в hello **приложения** в разделе **уведомления**, задайте **всплывающие уведомления:** слишком**Да**</span><span class="sxs-lookup"><span data-stu-id="6720f-160">In hello `Package.appxmanifest` file, in hello **Application** tab, under **Notifications**, set **Toast capable:** too**Yes**</span></span>

    ![][5]

### <a name="initialize-hello-reach-sdk"></a><span data-ttu-id="6720f-161">Инициализировать hello пакет SDK для REACH</span><span class="sxs-lookup"><span data-stu-id="6720f-161">Initialize hello REACH SDK</span></span>
<span data-ttu-id="6720f-162">В `App.xaml.cs`, вызовите **EngagementReach.Instance.Init(e);** в hello **InitEngagement** функция сразу же после инициализации агента hello:</span><span class="sxs-lookup"><span data-stu-id="6720f-162">In `App.xaml.cs`, call **EngagementReach.Instance.Init(e);** in hello **InitEngagement** function right after hello agent initialization:</span></span>

        private void InitEngagement(IActivatedEventArgs e)
        {
           EngagementAgent.Instance.Init(e);
           EngagementReach.Instance.Init(e);
        }

<span data-ttu-id="6720f-163">Теперь вы готовы toosend всплывающее уведомление.</span><span class="sxs-lookup"><span data-stu-id="6720f-163">You're ready toosend a toast.</span></span> <span data-ttu-id="6720f-164">Теперь убедимся, что базовая интеграция выполнена правильно.</span><span class="sxs-lookup"><span data-stu-id="6720f-164">Next we verify that you have correctly carried out this basic integration.</span></span>

### <a name="grant-access-toomobile-engagement-toosend-notifications"></a><span data-ttu-id="6720f-165">Предоставление доступа к tooMobile Engagement toosend уведомления</span><span class="sxs-lookup"><span data-stu-id="6720f-165">Grant access tooMobile Engagement toosend notifications</span></span>
1. <span data-ttu-id="6720f-166">Откройте в веб-браузере [Центр разработки Магазина Windows] , войдите и при необходимости создайте учетную запись.</span><span class="sxs-lookup"><span data-stu-id="6720f-166">Open [Windows Store Dev Center] in your web browser, login, and create an account if necessary.</span></span>
2. <span data-ttu-id="6720f-167">Нажмите кнопку **мониторинга** справа вверху hello углу, а затем нажмите кнопку **создайте новое приложение** hello левой панели меню.</span><span class="sxs-lookup"><span data-stu-id="6720f-167">Click **Dashboard** at hello top right corner and then click **Create a new app** from hello left panel menu.</span></span>

    ![][9]
3. <span data-ttu-id="6720f-168">Создайте приложение, резервируя его имя.</span><span class="sxs-lookup"><span data-stu-id="6720f-168">Create your app by reserving its name.</span></span>

    ![][10]
4. <span data-ttu-id="6720f-169">После создания приложения hello перейдите слишком**службы -> Push-уведомления** из меню слева hello.</span><span class="sxs-lookup"><span data-stu-id="6720f-169">Once hello app has been created, navigate too**Services -> Push notifications** from hello left menu.</span></span>

    ![][11]
5. <span data-ttu-id="6720f-170">В hello Push-уведомления, нажмите кнопку hello **узла службы Live** ссылку.</span><span class="sxs-lookup"><span data-stu-id="6720f-170">In hello Push notifications section, click hello **Live Services site** link.</span></span>

    ![][12]
6. <span data-ttu-id="6720f-171">Переместитесь раздел учетных данных toohello Push.</span><span class="sxs-lookup"><span data-stu-id="6720f-171">You navigate toohello Push credentials section.</span></span> <span data-ttu-id="6720f-172">Убедитесь, что вы находитесь в hello **параметры приложения** статьи и скопируйте вашей **ИД безопасности пакета** и **секрет клиента**</span><span class="sxs-lookup"><span data-stu-id="6720f-172">Make sure you are in hello **App Settings** section and then copy your **Package SID** and **Client secret**</span></span>

    ![][13]
7. <span data-ttu-id="6720f-173">Перейдите toohello **параметры** из порталу мобильного охвата и нажмите кнопку hello **системные Push-уведомления** раздел слева hello.</span><span class="sxs-lookup"><span data-stu-id="6720f-173">Navigate toohello **Settings** of your Mobile Engagement portal, and click hello **Native Push** section on hello left.</span></span> <span data-ttu-id="6720f-174">Нажмите кнопку hello **изменить** tooenter кнопку вашей **пакета идентификатор безопасности (SID)** и **секретный ключ** как показано:</span><span class="sxs-lookup"><span data-stu-id="6720f-174">Then, click hello **Edit** button tooenter your **Package security identifier (SID)** and your **Secret Key** as shown:</span></span>

    ![][6]
8. <span data-ttu-id="6720f-175">Наконец убедитесь, что с помощью этого приложения, созданного в магазине приложений hello связаны приложения Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6720f-175">Finally make sure that you have associated your Visual Studio app with this created app in hello App store.</span></span> <span data-ttu-id="6720f-176">В Visual Studio щелкните **Associate App with Store** (Связать приложение с магазином).</span><span class="sxs-lookup"><span data-stu-id="6720f-176">Click **Associate App with Store** in Visual Studio.</span></span>

    ![][7]

## <span data-ttu-id="6720f-177"><a id="send"></a>Отправить уведомление о tooyour приложение</span><span class="sxs-lookup"><span data-stu-id="6720f-177"><a id="send"></a>Send a notification tooyour app</span></span>
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

<span data-ttu-id="6720f-178">Если приложение hello работает, может появиться уведомление в приложении.</span><span class="sxs-lookup"><span data-stu-id="6720f-178">If hello app is running, you see an in-app notification.</span></span> <span data-ttu-id="6720f-179">в противном случае приложение hello закрыт, вы увидите всплывающее уведомление.</span><span class="sxs-lookup"><span data-stu-id="6720f-179">otherwise if hello app is closed, you see a toast notification.</span></span>
<span data-ttu-id="6720f-180">Если вы видите уведомление в приложении, но не всплывающее уведомление и выполнении приложение hello в режиме отладки в Visual Studio, затем повторите **события жизненного цикла -> Suspend** в tooensure инструментов hello приостанавливается, приложение hello.</span><span class="sxs-lookup"><span data-stu-id="6720f-180">If you see an in-app notification but not a toast notification, and you are running hello app in debug mode in Visual Studio, then try **Lifecycle events -> Suspend** in hello toolbar tooensure that hello app is suspended.</span></span> <span data-ttu-id="6720f-181">Если была нажата кнопка домашней hello во время отладки приложения hello в Visual Studio, затем он не всегда была приостановлена и во время уведомления hello вы увидите, как в приложении, он не отображается в виде всплывающих уведомлений.</span><span class="sxs-lookup"><span data-stu-id="6720f-181">If you clicked hello Home button while debugging hello application in Visual Studio, then it doesn't always get suspended and while you see hello notification as in-app, it doesn't show up as a toast notification.</span></span>  

![][8]

<!-- URLs. -->
[Mobile Engagement Windows Universal SDK documentation]: ../mobile-engagement-windows-store-integrate-engagement/
[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9864592
[Центр разработки Магазина Windows]: https://dev.windows.com
[Windows Universal Apps - Overlay integration]: ../mobile-engagement-windows-store-integrate-engagement-reach/#overlay-integration

<!-- Images. -->
[1]: ./media/mobile-engagement-windows-store-dotnet-get-started/universal-app-creation.png
[2]: ./media/mobile-engagement-windows-store-dotnet-get-started/manifest-capabilities.png
[3]: ./media/mobile-engagement-windows-store-dotnet-get-started/add-connection-info.png
[5]: ./media/mobile-engagement-windows-store-dotnet-get-started/manifest-toast.png
[6]: ./media/mobile-engagement-windows-store-dotnet-get-started/enter-credentials.png
[7]: ./media/mobile-engagement-windows-store-dotnet-get-started/associate-app-store.png
[8]: ./media/mobile-engagement-windows-store-dotnet-get-started/vs-suspend.png
[9]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_create_app.png
[10]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_app_name.png
[11]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push.png
[12]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push_1.png
[13]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push_creds.png
