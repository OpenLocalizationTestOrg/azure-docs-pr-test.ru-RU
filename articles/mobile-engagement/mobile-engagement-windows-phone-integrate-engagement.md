---
title: "aaaWindows Phone Silverlight Engagement SDK-интеграция"
description: "Как tooIntegrate Azure Mobile Engagement с приложениями Silverlight для Windows Phone"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 447fea8d-f4e3-4ad4-8ec0-8e3cf1ad3ab0
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: f65683a62e5256cea469a3a73d99ade4331cb6bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-engagement-sdk-integration"></a><span data-ttu-id="0151b-103">Интеграция пакета SDK Engagement для Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="0151b-103">Windows Phone Silverlight Engagement SDK Integration</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0151b-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="0151b-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md) 
> * [<span data-ttu-id="0151b-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="0151b-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [<span data-ttu-id="0151b-106">iOS</span><span class="sxs-lookup"><span data-stu-id="0151b-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md) 
> * [<span data-ttu-id="0151b-107">Android</span><span class="sxs-lookup"><span data-stu-id="0151b-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md) 
> 
> 

<span data-ttu-id="0151b-108">Эта процедура описывает hello простейший способ tooactivate Azure Mobile Engagement аналитики и наблюдение за функциями в приложении Windows Phone Silverlight.</span><span class="sxs-lookup"><span data-stu-id="0151b-108">This procedure describes hello simplest way tooactivate Azure Mobile Engagement's Analytics and Monitoring functions in your Windows Phone Silverlight application.</span></span>

<span data-ttu-id="0151b-109">следующие шаги Hello — это отчет hello достаточно tooactivate журналов необходимости toocompute все статистические данные о пользователей, сеансы, действия, сбои и Technicals.</span><span class="sxs-lookup"><span data-stu-id="0151b-109">hello following steps are enough tooactivate hello report of logs needed toocompute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="0151b-110">Hello журналов требуется отчет toocompute другие статистические данные, как события, ошибок и задания должны выполняться вручную с помощью hello Engagement API (в разделе [как toouse hello дополнительные теги API в приложения Windows Phone Silverlight мобильного охвата](mobile-engagement-windows-phone-use-engagement-api.md) см. ниже), так как эти статистические данные, зависящие от приложения.</span><span class="sxs-lookup"><span data-stu-id="0151b-110">hello report of logs needed toocompute other statistics like Events, Errors and Jobs must be done manually using hello Engagement API (see [How toouse hello advanced Mobile Engagement tagging API in your Windows Phone Silverlight app](mobile-engagement-windows-phone-use-engagement-api.md) below) since these statistics are application-dependent.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="0151b-111">Поддерживаемые версии</span><span class="sxs-lookup"><span data-stu-id="0151b-111">Supported versions</span></span>
<span data-ttu-id="0151b-112">только Hello SDK Mobile Engagement для Windows Silverlight можно интегрировать в приложения, предназначенные для:</span><span class="sxs-lookup"><span data-stu-id="0151b-112">hello Mobile Engagement SDK for Windows Silverlight can only be integrated into applications targeting :</span></span>

* <span data-ttu-id="0151b-113">Windows Phone 8.0</span><span class="sxs-lookup"><span data-stu-id="0151b-113">Windows Phone 8.0</span></span>
* <span data-ttu-id="0151b-114">Windows Phone 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="0151b-114">Windows Phone 8.1 Silverlight</span></span>

> [!NOTE]
> <span data-ttu-id="0151b-115">Если в качестве цели Windows Phone 8.1 (отличных от Silverlight), а затем ссылаться toohello [Windows универсальной процедуры интеграции](mobile-engagement-windows-store-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="0151b-115">If you are targeting Windows Phone 8.1 (non-Silverlight) then refer toohello [Windows Universal integration procedure](mobile-engagement-windows-store-integrate-engagement.md).</span></span>
> 
> 

## <a name="install-hello-mobile-engagement-silverlight-sdk"></a><span data-ttu-id="0151b-116">Установить пакет SDK Mobile Engagement Silverlight hello</span><span class="sxs-lookup"><span data-stu-id="0151b-116">Install hello Mobile Engagement Silverlight SDK</span></span>
<span data-ttu-id="0151b-117">Hello SDK Mobile Engagement для Windows Silverlight доступен как пакет Nuget вызывается *MicrosoftAzure.MobileEngagement*.</span><span class="sxs-lookup"><span data-stu-id="0151b-117">hello Mobile Engagement SDK for Windows Silverlight is available as a Nuget package called *MicrosoftAzure.MobileEngagement*.</span></span> <span data-ttu-id="0151b-118">Его можно установить из hello диспетчера пакетов Nuget для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0151b-118">You can install it from hello Visual Studio Nuget Package Manager.</span></span> 

## <a name="add-hello-capabilities"></a><span data-ttu-id="0151b-119">Добавление возможностей hello</span><span class="sxs-lookup"><span data-stu-id="0151b-119">Add hello capabilities</span></span>
<span data-ttu-id="0151b-120">Hello Engagement SDK должен некоторые возможности hello пакет SDK для Windows Phone Silverlight в порядке toowork должным образом.</span><span class="sxs-lookup"><span data-stu-id="0151b-120">hello Engagement SDK needs some capabilities of hello Windows Phone Silverlight SDK in order toowork properly.</span></span>

<span data-ttu-id="0151b-121">Откройте ваш `WMAppManifest.xml` файл и убедитесь, что hello следующие возможности, объявляются в hello `Capabilities` панели:</span><span class="sxs-lookup"><span data-stu-id="0151b-121">Open your `WMAppManifest.xml` file and be sure that hello following capabilities are declared in hello `Capabilities` panel:</span></span>

* `ID_CAP_NETWORKING`
* `ID_CAP_IDENTITY_DEVICE`

## <a name="initialize-hello-engagement-sdk"></a><span data-ttu-id="0151b-122">Инициализировать hello Engagement SDK</span><span class="sxs-lookup"><span data-stu-id="0151b-122">Initialize hello Engagement SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="0151b-123">Конфигурация Engagement</span><span class="sxs-lookup"><span data-stu-id="0151b-123">Engagement configuration</span></span>
<span data-ttu-id="0151b-124">централизованный Hello проектной конфигурации в hello `Resources\EngagementConfiguration.xml` файла проекта.</span><span class="sxs-lookup"><span data-stu-id="0151b-124">hello Engagement configuration is centralized in hello `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="0151b-125">Измените этот файл toospecify:</span><span class="sxs-lookup"><span data-stu-id="0151b-125">Edit this file toospecify :</span></span>

* <span data-ttu-id="0151b-126">строку подключения приложения между тегами `<connectionString>` and `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="0151b-126">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="0151b-127">Если требуется, чтобы его во время выполнения вместо этого можно вызвать следующие hello toospecify метод до инициализации агента Engagement hello:</span><span class="sxs-lookup"><span data-stu-id="0151b-127">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization:</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

<span data-ttu-id="0151b-128">Hello строку подключения для приложения отображается на hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="0151b-128">hello connection string for your application is displayed on hello Azure Classic Portal.</span></span>

### <a name="engagement-initialization"></a><span data-ttu-id="0151b-129">Инициализация Engagement</span><span class="sxs-lookup"><span data-stu-id="0151b-129">Engagement initialization</span></span>
<span data-ttu-id="0151b-130">При создании проекта создается файл `App.xaml.cs` .</span><span class="sxs-lookup"><span data-stu-id="0151b-130">When you create a new project, a `App.xaml.cs` file is generated.</span></span> <span data-ttu-id="0151b-131">Этот класс наследуется из `Application` и содержит множество важных методов.</span><span class="sxs-lookup"><span data-stu-id="0151b-131">This class inherits from `Application` and contains many important methods.</span></span> <span data-ttu-id="0151b-132">Он также будет hello используется tooinitialize Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="0151b-132">It will also be used tooinitialize hello Engagement SDK.</span></span>

<span data-ttu-id="0151b-133">Изменение hello `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="0151b-133">Modify hello `App.xaml.cs`:</span></span>

* <span data-ttu-id="0151b-134">Добавить tooyour `using` инструкции:</span><span class="sxs-lookup"><span data-stu-id="0151b-134">Add tooyour `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="0151b-135">Вставить `EngagementAgent.Instance.Init` в hello `Application_Launching` метод:</span><span class="sxs-lookup"><span data-stu-id="0151b-135">Insert `EngagementAgent.Instance.Init` in hello `Application_Launching` method :</span></span>
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
        EngagementAgent.Instance.Init();
      }
* <span data-ttu-id="0151b-136">Вставить `EngagementAgent.Instance.OnActivated` в hello `Application_Activated` метод:</span><span class="sxs-lookup"><span data-stu-id="0151b-136">Insert `EngagementAgent.Instance.OnActivated` in hello `Application_Activated` method :</span></span>
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
      }

> [!WARNING]
> <span data-ttu-id="0151b-137">Настоятельно рекомендуется не вы tooadd hello Engagement инициализации в другом месте приложения.</span><span class="sxs-lookup"><span data-stu-id="0151b-137">We strongly discourage you tooadd hello Engagement initialization in another place of your application.</span></span> <span data-ttu-id="0151b-138">Однако учтите, что hello `EngagementAgent.Instance.Init` метод выполняется в выделенном потоке, а не на hello поток пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="0151b-138">However, be aware that hello `EngagementAgent.Instance.Init` method runs on a dedicated thread, and not on hello UI thread.</span></span>
> 
> 

## <a name="basic-reporting"></a><span data-ttu-id="0151b-139">Упрощенные отчеты</span><span class="sxs-lookup"><span data-stu-id="0151b-139">Basic reporting</span></span>
### <a name="recommended-method--overload-your-phoneapplicationpage-classes"></a><span data-ttu-id="0151b-140">Рекомендуемый метод: перегрузка классов `PhoneApplicationPage`</span><span class="sxs-lookup"><span data-stu-id="0151b-140">Recommended method : overload your `PhoneApplicationPage` classes</span></span>
<span data-ttu-id="0151b-141">В отчете hello tooactivate порядок всех журналов hello, необходимых в Engagement toocompute пользователей, сеансы, действия, сбои и технические данные, можно просто сделать все вашей `PhoneApplicationPage` вложенные классы наследуют от hello `EngagementPage` классы.</span><span class="sxs-lookup"><span data-stu-id="0151b-141">In order tooactivate hello report of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `PhoneApplicationPage` sub-classes inherit from hello `EngagementPage` classes.</span></span>

<span data-ttu-id="0151b-142">Ниже приведен пример того, как toodo это для страницы приложения.</span><span class="sxs-lookup"><span data-stu-id="0151b-142">Here is an example of how toodo this for a page of your application.</span></span> <span data-ttu-id="0151b-143">Можно сделать hello одинаково для всех страниц приложения.</span><span class="sxs-lookup"><span data-stu-id="0151b-143">You can do hello same thing for all pages of your application.</span></span>

#### <a name="c-source-file"></a><span data-ttu-id="0151b-144">Исходный файл на C#</span><span class="sxs-lookup"><span data-stu-id="0151b-144">C# Source file</span></span>
<span data-ttu-id="0151b-145">Измените файл страницы `.xaml.cs` :</span><span class="sxs-lookup"><span data-stu-id="0151b-145">Modify your page `.xaml.cs` file :</span></span>

* <span data-ttu-id="0151b-146">Добавить tooyour `using` инструкции:</span><span class="sxs-lookup"><span data-stu-id="0151b-146">Add tooyour `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="0151b-147">Замените `PhoneApplicationPage` на `EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="0151b-147">Replace `PhoneApplicationPage` with `EngagementPage` :</span></span>

<span data-ttu-id="0151b-148">**Без Engagement:**</span><span class="sxs-lookup"><span data-stu-id="0151b-148">**Without Engagement:**</span></span>

        namespace Example
        {
          public partial class ExamplePage : PhoneApplicationPage
          {
            [...]
          }
        }

<span data-ttu-id="0151b-149">**С Engagement:**</span><span class="sxs-lookup"><span data-stu-id="0151b-149">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!WARNING]
> <span data-ttu-id="0151b-150">Если на странице наследуется от hello `OnNavigatedTo` метод, быть тщательно toolet hello `base.OnNavigatedTo(e)` вызова.</span><span class="sxs-lookup"><span data-stu-id="0151b-150">If your page inherits from hello `OnNavigatedTo` method, be careful toolet hello `base.OnNavigatedTo(e)` call.</span></span> <span data-ttu-id="0151b-151">В противном случае действие hello не будут отображаться.</span><span class="sxs-lookup"><span data-stu-id="0151b-151">Otherwise, hello activity will not be reported.</span></span> <span data-ttu-id="0151b-152">На самом деле hello `EngagementPage` вызывает `StartActivity` внутри hello `OnNavigatedTo` метод.</span><span class="sxs-lookup"><span data-stu-id="0151b-152">Indeed, hello `EngagementPage` is calling `StartActivity` inside hello `OnNavigatedTo` method.</span></span>
> 
> 

#### <a name="xaml-file"></a><span data-ttu-id="0151b-153">XAML-файл</span><span class="sxs-lookup"><span data-stu-id="0151b-153">XAML file</span></span>
<span data-ttu-id="0151b-154">Измените файл страницы `.xaml` :</span><span class="sxs-lookup"><span data-stu-id="0151b-154">Modify your page `.xaml` file :</span></span>

* <span data-ttu-id="0151b-155">Добавьте tooyour объявления пространств имен:</span><span class="sxs-lookup"><span data-stu-id="0151b-155">Add tooyour namespaces declarations :</span></span>
  
      xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
* <span data-ttu-id="0151b-156">Замените `phone:PhoneApplicationPage` на `engagement:EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="0151b-156">Replace `phone:PhoneApplicationPage` with `engagement:EngagementPage` :</span></span>

<span data-ttu-id="0151b-157">**Без Engagement:**</span><span class="sxs-lookup"><span data-stu-id="0151b-157">**Without Engagement:**</span></span>

        <phone:PhoneApplicationPage>
            <!-- layout -->
        </phone:PhoneApplicationPage>

<span data-ttu-id="0151b-158">**С Engagement:**</span><span class="sxs-lookup"><span data-stu-id="0151b-158">**With Engagement:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP">

            <!-- layout -->
        </engagement:EngagementPage >

#### <a name="override-hello-default-behavior"></a><span data-ttu-id="0151b-159">Переопределить поведение по умолчанию hello</span><span class="sxs-lookup"><span data-stu-id="0151b-159">Override hello default behavior</span></span>
<span data-ttu-id="0151b-160">По умолчанию имя класса hello страницы приветствия отображается как имя действия hello с без дополнительных.</span><span class="sxs-lookup"><span data-stu-id="0151b-160">By default, hello class name of hello page is reported as hello activity name, with no extra.</span></span> <span data-ttu-id="0151b-161">Если класс hello использует hello суффикс «Страница», Engagement также удалит ее.</span><span class="sxs-lookup"><span data-stu-id="0151b-161">If hello class uses hello "Page" suffix, Engagement will also remove it.</span></span>

<span data-ttu-id="0151b-162">Если требуется поведение по умолчанию hello toooverride имени hello, просто добавьте следующий код tooyour.</span><span class="sxs-lookup"><span data-stu-id="0151b-162">If you want toooverride hello default behavior for hello name, simply add this tooyour code:</span></span>

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
           /* your code */
           return "new name";
        }

<span data-ttu-id="0151b-163">Если требуется tooreport некоторыми дополнительными сведениями с действием, можно добавить этот код tooyour:</span><span class="sxs-lookup"><span data-stu-id="0151b-163">If you want tooreport some extra information with your activity, you can add this tooyour code:</span></span>

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
           /* your code */
           return extra;
        }

<span data-ttu-id="0151b-164">Эти методы вызываются из внутри hello `OnNavigatedTo` метод страницы.</span><span class="sxs-lookup"><span data-stu-id="0151b-164">These methods are called from within hello `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="0151b-165">Альтернативный метод: вызов `StartActivity()` вручную</span><span class="sxs-lookup"><span data-stu-id="0151b-165">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="0151b-166">Если невозможно или нежелательно toooverload вашей `PhoneApplicationPage` классы, вместо этого можно запустить ваши действия путем вызова `EngagementAgent` методы напрямую.</span><span class="sxs-lookup"><span data-stu-id="0151b-166">If you cannot or do not want toooverload your `PhoneApplicationPage` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="0151b-167">Советуем вызывать `StartActivity` в методе `OnNavigatedTo` класса PhoneApplicationPage.</span><span class="sxs-lookup"><span data-stu-id="0151b-167">We recommend calling `StartActivity` inside your `OnNavigatedTo` method of your PhoneApplicationPage.</span></span>

        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
           base.OnNavigatedTo(e);
           EngagementAgent.Instance.StartActivity("MyPage");
        }

> [!IMPORTANT]
> <span data-ttu-id="0151b-168">Убедитесь, что сеанс завершен правильно.</span><span class="sxs-lookup"><span data-stu-id="0151b-168">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="0151b-169">пакет SDK для Hello автоматически вызывает hello `EndActivity` метод при закрытии приложения hello.</span><span class="sxs-lookup"><span data-stu-id="0151b-169">hello SDK automatically calls hello `EndActivity` method when hello application is closed.</span></span> <span data-ttu-id="0151b-170">Таким образом, **высокой** рекомендуется toocall hello `StartActivity` метод изменении hello действий пользователя hello и слишком**никогда** hello вызовов `EndActivity` метод.</span><span class="sxs-lookup"><span data-stu-id="0151b-170">Thus, it is **HIGHLY** recommended toocall hello `StartActivity` method whenever hello activity of hello user change, and too**NEVER** call hello `EndActivity` method.</span></span> <span data-ttu-id="0151b-171">Этот метод отправляет сообщение сервера Engagement toohello что hello текущий пользователь покинул приложения hello, и это влияет на все журналы приложений.</span><span class="sxs-lookup"><span data-stu-id="0151b-171">This method sends a message toohello Engagement server that hello current user has left hello application and this impacts all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="0151b-172">Расширенные отчеты</span><span class="sxs-lookup"><span data-stu-id="0151b-172">Advanced reporting</span></span>
<span data-ttu-id="0151b-173">При необходимости вы можете tooreport приложения определенных событий, ошибок и задания, toodo таким образом, использование hello другие методы найдены в hello `EngagementAgent` класса.</span><span class="sxs-lookup"><span data-stu-id="0151b-173">Optionally, you may want tooreport application specific events, errors and jobs, toodo so, use hello others methods found in hello `EngagementAgent` class.</span></span> <span data-ttu-id="0151b-174">Hello Engagement API позволяет toouse всем Engagement расширенные возможности.</span><span class="sxs-lookup"><span data-stu-id="0151b-174">hello Engagement API allows toouse all of Engagement's advanced capabilities.</span></span>

<span data-ttu-id="0151b-175">Дополнительные сведения см. в разделе [как toouse hello дополнительные теги API в приложения Windows Phone Silverlight мобильного охвата](mobile-engagement-windows-phone-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="0151b-175">For further information, see [How toouse hello advanced Mobile Engagement tagging API in your Windows Phone Silverlight app](mobile-engagement-windows-phone-use-engagement-api.md).</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="0151b-176">Расширенная конфигурация</span><span class="sxs-lookup"><span data-stu-id="0151b-176">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="0151b-177">Отключение автоматического создания отчетов о сбоях</span><span class="sxs-lookup"><span data-stu-id="0151b-177">Disable automatic crash reporting</span></span>
<span data-ttu-id="0151b-178">Можно отключить hello аварийного завершения автоматического компонент рвением отчетов.</span><span class="sxs-lookup"><span data-stu-id="0151b-178">You can disable hello automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="0151b-179">После этого при возникновении необработанного исключения Engagement не будет предпринимать никаких действий.</span><span class="sxs-lookup"><span data-stu-id="0151b-179">Then, when an unhandled exception will occur, Engagement won't do anything.</span></span>

> [!WARNING]
> <span data-ttu-id="0151b-180">Если планируется toodisable эту функцию, помните, что, когда необработанное сбоя будет появляться в вашем приложении, Engagement не будет отправлять hello аварийного завершения **AND** не закроет сеанс hello и заданий.</span><span class="sxs-lookup"><span data-stu-id="0151b-180">If you plan toodisable this feature, be aware that when a unhandled crash will occur in your app, Engagement will not send hello crash **AND** it will not close hello session and jobs.</span></span>
> 
> 

<span data-ttu-id="0151b-181">автоматического создания отчетов, о сбоях toodisable просто настроить конфигурацию, в зависимости от того, она была объявлена как hello:</span><span class="sxs-lookup"><span data-stu-id="0151b-181">toodisable automatic crash reporting, just customize your configuration depending on hello way you declared it :</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="0151b-182">Из файла `EngagementConfiguration.xml`</span><span class="sxs-lookup"><span data-stu-id="0151b-182">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="0151b-183">Отчет набора аварийное завершение работы слишком`false` между `<reportCrash>` и `</reportCrash>` тегов.</span><span class="sxs-lookup"><span data-stu-id="0151b-183">Set report crash too`false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="0151b-184">Из объекта `EngagementConfiguration` во время выполнения</span><span class="sxs-lookup"><span data-stu-id="0151b-184">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="0151b-185">Задать toofalse сбоя отчетов с помощью объекта EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="0151b-185">Set report crash toofalse using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration(); engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";
        /\* Disable Engagement crash reporting. \*/ engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a><span data-ttu-id="0151b-186">Пакетный режим</span><span class="sxs-lookup"><span data-stu-id="0151b-186">Burst mode</span></span>
<span data-ttu-id="0151b-187">По умолчанию hello Engagement службы отчетов входит в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="0151b-187">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="0151b-188">Если приложение сообщает журналов производится очень часто, это лучше toobuffer hello журналы и tooreport их все за один раз на обычное время базового (это называется «пакетный режим» hello).</span><span class="sxs-lookup"><span data-stu-id="0151b-188">If your application reports logs very frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time base (this is called hello “burst mode”).</span></span>

<span data-ttu-id="0151b-189">toodo таким образом, необходимо вызвать метод hello:</span><span class="sxs-lookup"><span data-stu-id="0151b-189">toodo so, call hello method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="0151b-190">Hello аргумент представляет собой значение в **миллисекунд**.</span><span class="sxs-lookup"><span data-stu-id="0151b-190">hello argument is a value in **milliseconds**.</span></span> <span data-ttu-id="0151b-191">В любое время Если требуется ведение журнала hello в режиме реального времени для tooreactivate просто вызовите метод hello без какого-либо параметра или со значением hello 0.</span><span class="sxs-lookup"><span data-stu-id="0151b-191">At any time, if you want tooreactivate hello real-time logging, just call hello method without any parameter, or with hello 0 value.</span></span>

<span data-ttu-id="0151b-192">Hello пакетный режим немного увеличить батареи hello жизни но оказывает влияние на hello монитор Engagement: все сеансы и задания будут скругленными toohello пороговое значение пакетного режима (таким образом, сеансы и задания короче, чем порог повышения hello не могут быть видны).</span><span class="sxs-lookup"><span data-stu-id="0151b-192">hello burst mode slightly increase hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration will be rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="0151b-193">Это рекомендуется toouse Повышение порогового значения больше чем 30000 (30s).</span><span class="sxs-lookup"><span data-stu-id="0151b-193">It is recommended toouse a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="0151b-194">Необходимо учитывать, сохраненные журналы являются элементами ограниченный too300 toobe.</span><span class="sxs-lookup"><span data-stu-id="0151b-194">You have toobe aware that saved logs are limited too300 items.</span></span> <span data-ttu-id="0151b-195">Если отправка занимает слишком много времени, некоторые журналы могут быть потеряны.</span><span class="sxs-lookup"><span data-stu-id="0151b-195">If sending is too long you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="0151b-196">Hello пороговое значение пакета не может быть настроен меньший период tooa одного раза в секунду.</span><span class="sxs-lookup"><span data-stu-id="0151b-196">hello burst threshold cannot be configured tooa period lesser than one second.</span></span> <span data-ttu-id="0151b-197">При попытке toodo таким образом, hello SDK будет отображать трассировку с ошибкой hello и автоматически сбросить toohello значение по умолчанию, то есть, ноль секунд.</span><span class="sxs-lookup"><span data-stu-id="0151b-197">If you try toodo so, hello SDK will show a trace with hello error and will automatically reset toohello default value, that is, zero seconds.</span></span> <span data-ttu-id="0151b-198">Это приведет к началу hello SDK tooreport hello журналы в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="0151b-198">This will trigger hello SDK tooreport hello logs in real-time.</span></span>
> 
> 

