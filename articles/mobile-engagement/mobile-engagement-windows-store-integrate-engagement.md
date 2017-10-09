---
title: "SDK-интеграция универсальных приложений Engagement aaaWindows"
description: "Как tooIntegrate Azure Mobile Engagement с универсальные приложения Windows"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 71236b68-5ebd-44aa-8c82-c7ca8098ea05
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 18543798099c233dbe55cc387ba0216e369c8596
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-engagement-sdk-integration"></a><span data-ttu-id="19414-103">Интеграция пакета SDK Engagement для универсальных приложений для Windows</span><span class="sxs-lookup"><span data-stu-id="19414-103">Windows Universal Apps Engagement SDK Integration</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="19414-104">Универсальная платформа Windows</span><span class="sxs-lookup"><span data-stu-id="19414-104">Universal Windows</span></span>](mobile-engagement-windows-store-integrate-engagement.md) 
> * [<span data-ttu-id="19414-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="19414-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [<span data-ttu-id="19414-106">iOS</span><span class="sxs-lookup"><span data-stu-id="19414-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md) 
> * [<span data-ttu-id="19414-107">Android</span><span class="sxs-lookup"><span data-stu-id="19414-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md) 
> 
> 

<span data-ttu-id="19414-108">Эта процедура описывает hello простейший способ tooactivate Engagement аналитики и наблюдение за функциями в приложении Windows Universal.</span><span class="sxs-lookup"><span data-stu-id="19414-108">This procedure describes hello simplest way tooactivate Engagement's Analytics and Monitoring functions in your Windows Universal application.</span></span>

<span data-ttu-id="19414-109">следующие шаги Hello — это отчет hello достаточно tooactivate журналов необходимости toocompute все статистические данные о пользователей, сеансы, действия, сбои и Technicals.</span><span class="sxs-lookup"><span data-stu-id="19414-109">hello following steps are enough tooactivate hello report of logs needed toocompute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="19414-110">Hello журналов требуется отчет toocompute другие статистические данные, как события, ошибок и задания должны выполняться вручную с помощью hello Engagement API (в разделе [как toouse hello дополнительные теги API в приложении универсальное приложение для Windows Mobile Engagement](mobile-engagement-windows-store-use-engagement-api.md) с момента Эти статистические данные зависит от приложения.</span><span class="sxs-lookup"><span data-stu-id="19414-110">hello report of logs needed toocompute other statistics like Events, Errors and Jobs must be done manually using hello Engagement API (see [How toouse hello advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="19414-111">Поддерживаемые версии</span><span class="sxs-lookup"><span data-stu-id="19414-111">Supported versions</span></span>
<span data-ttu-id="19414-112">только Hello Mobile Engagement SDK для универсальных приложений Windows можно интегрировать в среды выполнения Windows и приложений универсальной платформы Windows, предназначенных для:</span><span class="sxs-lookup"><span data-stu-id="19414-112">hello Mobile Engagement SDK for Windows Universal Apps can only be integrated into Windows Runtime and Universal Windows Platform applications targeting :</span></span>

* <span data-ttu-id="19414-113">Windows 8</span><span class="sxs-lookup"><span data-stu-id="19414-113">Windows 8</span></span>
* <span data-ttu-id="19414-114">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="19414-114">Windows 8.1</span></span>
* <span data-ttu-id="19414-115">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="19414-115">Windows Phone 8.1</span></span>
* <span data-ttu-id="19414-116">Windows 10 (настольных компьютеров и мобильных устройств)</span><span class="sxs-lookup"><span data-stu-id="19414-116">Windows 10 (desktop and mobile families)</span></span>

> [!NOTE]
> <span data-ttu-id="19414-117">Если в качестве цели Windows Phone Silverlight, а затем ссылаться toohello [процедуры интеграции Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="19414-117">If you are targeting Windows Phone Silverlight then refer toohello [Windows Phone Silverlight integration procedure](mobile-engagement-windows-phone-integrate-engagement.md).</span></span>
> 
> 

## <a name="install-hello-mobile-engagement-universal-apps-sdk"></a><span data-ttu-id="19414-118">Установить пакет SDK Mobile Engagement универсальные приложения hello</span><span class="sxs-lookup"><span data-stu-id="19414-118">Install hello Mobile Engagement Universal Apps SDK</span></span>
### <a name="all-platforms"></a><span data-ttu-id="19414-119">Все платформы</span><span class="sxs-lookup"><span data-stu-id="19414-119">All platforms</span></span>
<span data-ttu-id="19414-120">Mobile Engagement SDK для Windows универсального приложения Hello доступен как пакет Nuget вызывается *MicrosoftAzure.MobileEngagement*.</span><span class="sxs-lookup"><span data-stu-id="19414-120">hello Mobile Engagement SDK for Windows Universal App is available as a Nuget package called *MicrosoftAzure.MobileEngagement*.</span></span> <span data-ttu-id="19414-121">Его можно установить из hello диспетчера пакетов Nuget для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="19414-121">You can install it from hello Visual Studio Nuget Package Manager.</span></span>

### <a name="windows-8x-and-windows-phone-81"></a><span data-ttu-id="19414-122">Windows 8.x и Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="19414-122">Windows 8.x and Windows Phone 8.1</span></span>
<span data-ttu-id="19414-123">NuGet автоматически развертывает ресурсы SDK hello hello `Resources` папки корневого каталога проекта приложения hello.</span><span class="sxs-lookup"><span data-stu-id="19414-123">NuGet automatically deploys hello SDK resources in hello `Resources` folder at hello root of your application project.</span></span>

### <a name="windows-10-universal-windows-platform-applications"></a><span data-ttu-id="19414-124">Универсальные приложения для Windows 10</span><span class="sxs-lookup"><span data-stu-id="19414-124">Windows 10 Universal Windows Platform applications</span></span>
<span data-ttu-id="19414-125">NuGet не развертывает ресурсы SDK hello в приложении UWP еще автоматически.</span><span class="sxs-lookup"><span data-stu-id="19414-125">NuGet does not automatically deploy hello SDK resources in your UWP application yet.</span></span> <span data-ttu-id="19414-126">У вас есть toodo его вручную до развертывания ресурсов возникает снова в NuGet:</span><span class="sxs-lookup"><span data-stu-id="19414-126">You have toodo it manually until resources deployment is reintroduced in NuGet:</span></span>

1. <span data-ttu-id="19414-127">Откройте обозреватель файлов.</span><span class="sxs-lookup"><span data-stu-id="19414-127">Open your File Explorer.</span></span>
2. <span data-ttu-id="19414-128">Перейдите в следующие расположения toohello (**x.x.x** версия hello взаимодействия при установке): *% USERPROFILE %\\.nuget\packages\MicrosoftAzure.MobileEngagement\\*  *x.x.x**\\content\win81*</span><span class="sxs-lookup"><span data-stu-id="19414-128">Navigate toohello following location (**x.x.x** is hello version of Engagement you are installing): *%USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\\**x.x.x**\\content\win81*</span></span>
3. <span data-ttu-id="19414-129">Перетаскивание hello **ресурсов** папку из корня toohello explorer hello файл проекта в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="19414-129">Drag and drop hello **Resources** folder from hello file explorer toohello root of your project in Visual Studio.</span></span>
4. <span data-ttu-id="19414-130">В Visual Studio выберите проект и активировать hello **Показать все файлы** значок поверх hello **обозревателе решений**.</span><span class="sxs-lookup"><span data-stu-id="19414-130">In Visual Studio select your project and activate hello **Show All files** icon on top of hello **Solution Explorer**.</span></span>
5. <span data-ttu-id="19414-131">Некоторые файлы не будут включены в проект hello.</span><span class="sxs-lookup"><span data-stu-id="19414-131">Some files are not included in hello project.</span></span> <span data-ttu-id="19414-132">их за один раз щелкните правой кнопкой мыши hello tooimport **ресурсов** папки, **исключить из проекта** то другой щелкните правой кнопкой мыши hello **ресурсов** папки, **Include в проекте** toore-включить hello всю папку.</span><span class="sxs-lookup"><span data-stu-id="19414-132">tooimport them at once right click on hello **Resources** folder, **Exclude from project** then another right click on hello **Resources** folder, **Include in project** toore-include hello whole folder.</span></span> <span data-ttu-id="19414-133">Все файлы из hello **ресурсов** папки теперь включены в проект.</span><span class="sxs-lookup"><span data-stu-id="19414-133">All files from hello **Resources** folder are now included in your project.</span></span>

## <a name="add-hello-capabilities"></a><span data-ttu-id="19414-134">Добавление возможностей hello</span><span class="sxs-lookup"><span data-stu-id="19414-134">Add hello capabilities</span></span>
<span data-ttu-id="19414-135">Hello Engagement SDK должен некоторые возможности hello пакета SDK для Windows в порядке toowork должным образом.</span><span class="sxs-lookup"><span data-stu-id="19414-135">hello Engagement SDK needs some capabilities of hello Windows SDK in order toowork properly.</span></span>

<span data-ttu-id="19414-136">Откройте ваш `Package.appxmanifest` файл и убедитесь, что объявлены, hello следующие возможности:</span><span class="sxs-lookup"><span data-stu-id="19414-136">Open your `Package.appxmanifest` file and be sure that hello following capabilities are declared:</span></span>

* `Internet (Client)`

## <a name="initialize-hello-engagement-sdk"></a><span data-ttu-id="19414-137">Инициализировать hello Engagement SDK</span><span class="sxs-lookup"><span data-stu-id="19414-137">Initialize hello Engagement SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="19414-138">Конфигурация Engagement</span><span class="sxs-lookup"><span data-stu-id="19414-138">Engagement configuration</span></span>
<span data-ttu-id="19414-139">централизованный Hello проектной конфигурации в hello `Resources\EngagementConfiguration.xml` файла проекта.</span><span class="sxs-lookup"><span data-stu-id="19414-139">hello Engagement configuration is centralized in hello `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="19414-140">Измените этот файл toospecify:</span><span class="sxs-lookup"><span data-stu-id="19414-140">Edit this file toospecify:</span></span>

* <span data-ttu-id="19414-141">строку подключения приложения между тегами `<connectionString>` and `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="19414-141">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="19414-142">Если требуется, чтобы его во время выполнения вместо этого можно вызвать следующие hello toospecify метод до инициализации агента Engagement hello:</span><span class="sxs-lookup"><span data-stu-id="19414-142">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization:</span></span>

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set hello Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);

<span data-ttu-id="19414-143">Hello строку подключения для приложения отображается на hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="19414-143">hello connection string for your application is displayed on hello Azure Classic Portal.</span></span>

### <a name="engagement-initialization"></a><span data-ttu-id="19414-144">Инициализация Engagement</span><span class="sxs-lookup"><span data-stu-id="19414-144">Engagement initialization</span></span>
<span data-ttu-id="19414-145">При создании проекта создается файл `App.xaml.cs` .</span><span class="sxs-lookup"><span data-stu-id="19414-145">When you create a new project, a `App.xaml.cs` file is generated.</span></span> <span data-ttu-id="19414-146">Этот класс наследуется из `Application` и содержит множество важных методов.</span><span class="sxs-lookup"><span data-stu-id="19414-146">This class inherits from `Application` and contains many important methods.</span></span> <span data-ttu-id="19414-147">Он также будет hello используется tooinitialize Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="19414-147">It will also be used tooinitialize hello Engagement SDK.</span></span>

<span data-ttu-id="19414-148">Изменение hello `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="19414-148">Modify hello `App.xaml.cs`:</span></span>

* <span data-ttu-id="19414-149">Добавить tooyour `using` инструкции:</span><span class="sxs-lookup"><span data-stu-id="19414-149">Add tooyour `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="19414-150">Определите инициализации метода tooshare hello Engagement один раз для всех вызовов.</span><span class="sxs-lookup"><span data-stu-id="19414-150">Define a method tooshare hello Engagement initialization once for all calls:</span></span>
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
  
        // or
  
        EngagementAgent.Instance.Init(e, engagementConfiguration);
      }
* <span data-ttu-id="19414-151">Вызовите `InitEngagement` в hello `OnLaunched` метод:</span><span class="sxs-lookup"><span data-stu-id="19414-151">Call `InitEngagement` in hello `OnLaunched` method:</span></span>
  
      protected override void OnLaunched(LaunchActivatedEventArgs e)
      {
        InitEngagement(e);
      }
* <span data-ttu-id="19414-152">При запуске приложения с использованием пользовательской схемы другого приложения или hello командной строки затем hello `OnActivated` вызывается метод.</span><span class="sxs-lookup"><span data-stu-id="19414-152">When your application is launched using a custom scheme, another application or hello command line then hello `OnActivated` method is called.</span></span> <span data-ttu-id="19414-153">Необходимо также tooinitiate hello Engagement SDK при активации приложения.</span><span class="sxs-lookup"><span data-stu-id="19414-153">You also need tooinitiate hello Engagement SDK when your app is activated.</span></span> <span data-ttu-id="19414-154">Таким образом, переопределите toodo `OnActivated` метод:</span><span class="sxs-lookup"><span data-stu-id="19414-154">toodo so, override `OnActivated` method:</span></span>
  
      protected override void OnActivated(IActivatedEventArgs args)
      {
        InitEngagement(args);
      }

> [!IMPORTANT]
> <span data-ttu-id="19414-155">Настоятельно рекомендуется не вы tooadd hello Engagement инициализации в другом месте приложения.</span><span class="sxs-lookup"><span data-stu-id="19414-155">We strongly discourage you tooadd hello Engagement initialization in another place of your application.</span></span>
> 
> 

## <a name="basic-reporting"></a><span data-ttu-id="19414-156">Упрощенные отчеты</span><span class="sxs-lookup"><span data-stu-id="19414-156">Basic reporting</span></span>
### <a name="recommended-method-overload-your-page-classes"></a><span data-ttu-id="19414-157">Рекомендуемый метод: перегрузка классов `Page`</span><span class="sxs-lookup"><span data-stu-id="19414-157">Recommended method: overload your `Page` classes</span></span>
<span data-ttu-id="19414-158">В отчете hello tooactivate порядок всех журналов hello, необходимых в Engagement toocompute пользователей, сеансы, действия, сбои и технические данные, можно просто сделать все вашей `Page` вложенные классы наследуют от hello `EngagementPage` классы.</span><span class="sxs-lookup"><span data-stu-id="19414-158">In order tooactivate hello report of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `Page` sub-classes inherit from hello `EngagementPage` classes.</span></span>

<span data-ttu-id="19414-159">Ниже приведен пример того, как toodo это для страницы приложения.</span><span class="sxs-lookup"><span data-stu-id="19414-159">Here is an example of how toodo this for a page of your application.</span></span> <span data-ttu-id="19414-160">Можно сделать hello одинаково для всех страниц приложения.</span><span class="sxs-lookup"><span data-stu-id="19414-160">You can do hello same thing for all pages of your application.</span></span>

#### <a name="c-source-file"></a><span data-ttu-id="19414-161">Исходный файл на C#</span><span class="sxs-lookup"><span data-stu-id="19414-161">C# Source file</span></span>
<span data-ttu-id="19414-162">Измените файл страницы `.xaml.cs` :</span><span class="sxs-lookup"><span data-stu-id="19414-162">Modify your page `.xaml.cs` file:</span></span>

* <span data-ttu-id="19414-163">Добавить tooyour `using` инструкции:</span><span class="sxs-lookup"><span data-stu-id="19414-163">Add tooyour `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="19414-164">Замените `Page` на `EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="19414-164">Replace `Page` with `EngagementPage`:</span></span>

<span data-ttu-id="19414-165">**Без Engagement:**</span><span class="sxs-lookup"><span data-stu-id="19414-165">**Without Engagement:**</span></span>

        namespace Example
        {
          public sealed partial class ExamplePage : Page
          {
            [...]
          }
        }

<span data-ttu-id="19414-166">**С Engagement:**</span><span class="sxs-lookup"><span data-stu-id="19414-166">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public sealed partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!IMPORTANT]
> <span data-ttu-id="19414-167">Если на странице переопределяет hello `OnNavigatedTo` метода будет убедиться, что toocall `base.OnNavigatedTo(e)`.</span><span class="sxs-lookup"><span data-stu-id="19414-167">If your page overrides hello `OnNavigatedTo` method, be sure toocall `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="19414-168">В противном случае не будет указано действие hello (hello `EngagementPage` вызовы `StartActivity` внутри его `OnNavigatedTo` метода).</span><span class="sxs-lookup"><span data-stu-id="19414-168">Otherwise,  hello activity will not be reported (hello `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span>
> 
> 

#### <a name="xaml-file"></a><span data-ttu-id="19414-169">XAML-файл</span><span class="sxs-lookup"><span data-stu-id="19414-169">XAML file</span></span>
<span data-ttu-id="19414-170">Измените файл страницы `.xaml` :</span><span class="sxs-lookup"><span data-stu-id="19414-170">Modify your page `.xaml` file:</span></span>

* <span data-ttu-id="19414-171">Добавьте tooyour объявления пространств имен:</span><span class="sxs-lookup"><span data-stu-id="19414-171">Add tooyour namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement"
* <span data-ttu-id="19414-172">Замените `Page` на `engagement:EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="19414-172">Replace `Page` with `engagement:EngagementPage`:</span></span>

<span data-ttu-id="19414-173">**Без Engagement:**</span><span class="sxs-lookup"><span data-stu-id="19414-173">**Without Engagement:**</span></span>

        <Page>
            <!-- layout -->
            ...
        </Page>

<span data-ttu-id="19414-174">**С Engagement:**</span><span class="sxs-lookup"><span data-stu-id="19414-174">**With Engagement:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">
            <!-- layout -->
            ...
        </engagement:EngagementPage >

#### <a name="override-hello-default-behaviour"></a><span data-ttu-id="19414-175">Переопределение поведения по умолчанию hello</span><span class="sxs-lookup"><span data-stu-id="19414-175">Override hello default behaviour</span></span>
<span data-ttu-id="19414-176">По умолчанию имя класса hello страницы приветствия отображается как имя действия hello с без дополнительных.</span><span class="sxs-lookup"><span data-stu-id="19414-176">By default, hello class name of hello page is reported as hello activity name, with no extra.</span></span> <span data-ttu-id="19414-177">Если класс hello использует hello суффикс «Страница», Engagement также удалит ее.</span><span class="sxs-lookup"><span data-stu-id="19414-177">If hello class uses hello "Page" suffix, Engagement will also remove it.</span></span>

<span data-ttu-id="19414-178">Если требуется поведение по умолчанию hello toooverride имени hello, просто добавьте следующий код tooyour.</span><span class="sxs-lookup"><span data-stu-id="19414-178">If you want toooverride hello default behaviour for hello name, simply add this tooyour code:</span></span>

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

<span data-ttu-id="19414-179">Если вы хотите tooreport некоторые дополнительные сведения с действием, можно добавить этот код tooyour:</span><span class="sxs-lookup"><span data-stu-id="19414-179">If you want tooreport some extra informations with your activity, you can add this tooyour code:</span></span>

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

<span data-ttu-id="19414-180">Эти методы вызываются из внутри hello `OnNavigatedTo` метод страницы.</span><span class="sxs-lookup"><span data-stu-id="19414-180">These methods are called from within hello `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="19414-181">Альтернативный метод: вызов `StartActivity()` вручную</span><span class="sxs-lookup"><span data-stu-id="19414-181">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="19414-182">Если невозможно или нежелательно toooverload вашей `Page` классы, вместо этого можно запустить ваши действия путем вызова `EngagementAgent` методы напрямую.</span><span class="sxs-lookup"><span data-stu-id="19414-182">If you cannot or do not want toooverload your `Page` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="19414-183">Мы рекомендуем toocall `StartActivity` внутри вашей `OnNavigatedTo` метод страницы.</span><span class="sxs-lookup"><span data-stu-id="19414-183">We recommend toocall `StartActivity` inside your `OnNavigatedTo` method of your Page.</span></span>

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> <span data-ttu-id="19414-184">Убедитесь, что сеанс завершен правильно.</span><span class="sxs-lookup"><span data-stu-id="19414-184">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="19414-185">пакет SDK для Universal Windows Hello автоматически вызывает hello `EndActivity` метод при закрытии приложения hello.</span><span class="sxs-lookup"><span data-stu-id="19414-185">hello Windows Universal SDK automatically calls hello `EndActivity` method when hello application is closed.</span></span> <span data-ttu-id="19414-186">Таким образом, **высокой** рекомендуется toocall hello `StartActivity` метод изменении hello действий пользователя hello и слишком**никогда** hello вызовов `EndActivity` метода, этот метод отправляет tooEngagement сервер, текущий пользователь имеет приложение hello оставьте, именно она влияет на все журналы приложений.</span><span class="sxs-lookup"><span data-stu-id="19414-186">Thus, it is **HIGHLY** recommended toocall hello `StartActivity` method whenever hello activity of hello user change, and too**NEVER** call hello `EndActivity` method, this method sends tooEngagement server that current user has leave hello application, this will impacts all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="19414-187">Расширенные отчеты</span><span class="sxs-lookup"><span data-stu-id="19414-187">Advanced reporting</span></span>
<span data-ttu-id="19414-188">При необходимости вы можете tooreport приложения определенных событий, ошибок и задания, toodo таким образом, использование hello другие методы найдены в hello `EngagementAgent` класса.</span><span class="sxs-lookup"><span data-stu-id="19414-188">Optionally, you may want tooreport application specific events, errors and jobs, toodo so, use hello others methods found in hello `EngagementAgent` class.</span></span> <span data-ttu-id="19414-189">Hello Engagement API позволяет toouse всем Engagement расширенные возможности.</span><span class="sxs-lookup"><span data-stu-id="19414-189">hello Engagement API allows toouse all of Engagement's advanced capabilities.</span></span>

<span data-ttu-id="19414-190">Дополнительные сведения см. в разделе [как toouse hello дополнительные теги API в приложении универсальное приложение для Windows Mobile Engagement](mobile-engagement-windows-store-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="19414-190">For further information, see [How toouse hello advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md).</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="19414-191">Расширенная конфигурация</span><span class="sxs-lookup"><span data-stu-id="19414-191">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="19414-192">Отключение автоматического создания отчетов о сбоях</span><span class="sxs-lookup"><span data-stu-id="19414-192">Disable automatic crash reporting</span></span>
<span data-ttu-id="19414-193">Можно отключить hello аварийного завершения автоматического компонент рвением отчетов.</span><span class="sxs-lookup"><span data-stu-id="19414-193">You can disable hello automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="19414-194">После этого при возникновении необработанного исключения Engagement не будет предпринимать никаких действий.</span><span class="sxs-lookup"><span data-stu-id="19414-194">Then, when an unhandled exception will occur, Engagement won't do anything.</span></span>

> [!WARNING]
> <span data-ttu-id="19414-195">Если планируется toodisable эту функцию, помните, что, когда необработанное сбоя будет появляться в вашем приложении, Engagement не будет отправлять hello аварийного завершения **AND** не закроет сеанс hello и заданий.</span><span class="sxs-lookup"><span data-stu-id="19414-195">If you plan toodisable this feature, be aware that when a unhandled crash will occur in your app, Engagement will not send hello crash **AND** will not close hello session and jobs.</span></span>
> 
> 

<span data-ttu-id="19414-196">автоматического создания отчетов, о сбоях toodisable просто настроить конфигурацию, в зависимости от того, она была объявлена как hello:</span><span class="sxs-lookup"><span data-stu-id="19414-196">toodisable automatic crash reporting, just customize your configuration depending on hello way you declared it:</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="19414-197">Из файла `EngagementConfiguration.xml`</span><span class="sxs-lookup"><span data-stu-id="19414-197">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="19414-198">Отчет набора аварийное завершение работы слишком`false` между `<reportCrash>` и `</reportCrash>` тегов.</span><span class="sxs-lookup"><span data-stu-id="19414-198">Set report crash too`false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="19414-199">Из объекта `EngagementConfiguration` во время выполнения</span><span class="sxs-lookup"><span data-stu-id="19414-199">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="19414-200">Задать toofalse сбоя отчетов с помощью объекта EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="19414-200">Set report crash toofalse using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a><span data-ttu-id="19414-201">Пакетный режим</span><span class="sxs-lookup"><span data-stu-id="19414-201">Burst mode</span></span>
<span data-ttu-id="19414-202">По умолчанию hello Engagement службы отчетов входит в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="19414-202">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="19414-203">Если приложение сообщает журналов производится очень часто, это лучше toobuffer hello журналы и tooreport их все за один раз на обычное время базового (это называется «пакетный режим» hello).</span><span class="sxs-lookup"><span data-stu-id="19414-203">If your application reports logs very frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time base (this is called hello “burst mode”).</span></span>

<span data-ttu-id="19414-204">toodo таким образом, необходимо вызвать метод hello:</span><span class="sxs-lookup"><span data-stu-id="19414-204">toodo so, call hello method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="19414-205">Hello аргумент представляет собой значение в **миллисекунд**.</span><span class="sxs-lookup"><span data-stu-id="19414-205">hello argument is a value in **milliseconds**.</span></span> <span data-ttu-id="19414-206">В любое время Если требуется ведение журнала hello в режиме реального времени для tooreactivate просто вызовите метод hello без какого-либо параметра или со значением hello 0.</span><span class="sxs-lookup"><span data-stu-id="19414-206">At any time, if you want tooreactivate hello real-time logging, just call hello method without any parameter, or with hello 0 value.</span></span>

<span data-ttu-id="19414-207">Hello пакетный режим немного увеличить батареи hello жизни но оказывает влияние на hello монитор Engagement: все сеансы и задания будут скругленными toohello пороговое значение пакетного режима (таким образом, сеансы и задания короче, чем порог повышения hello не могут быть видны).</span><span class="sxs-lookup"><span data-stu-id="19414-207">hello burst mode slightly increase hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration will be rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="19414-208">Это рекомендуется toouse Повышение порогового значения больше чем 30000 (30s).</span><span class="sxs-lookup"><span data-stu-id="19414-208">It is recommended toouse a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="19414-209">Необходимо учитывать, сохраненные журналы являются элементами ограниченный too300 toobe.</span><span class="sxs-lookup"><span data-stu-id="19414-209">You have toobe aware that saved logs are limited too300 items.</span></span> <span data-ttu-id="19414-210">Если отправка занимает слишком много времени, некоторые журналы могут быть потеряны.</span><span class="sxs-lookup"><span data-stu-id="19414-210">If sending is too long you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="19414-211">Порог повышения Hello нельзя настроить период tooa меньше единицы.</span><span class="sxs-lookup"><span data-stu-id="19414-211">hello burst threshold cannot be configured tooa period lesser than 1s.</span></span> <span data-ttu-id="19414-212">При попытке toodo таким образом, hello SDK будет отображать трассировку с ошибкой hello и автоматически сбросить значение по умолчанию toohello, т. е. 0.</span><span class="sxs-lookup"><span data-stu-id="19414-212">If you try toodo so, hello SDK will show a trace with hello error and will automatically reset toohello default value, i.e., 0s.</span></span> <span data-ttu-id="19414-213">Это приведет к началу hello SDK tooreport hello журналы в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="19414-213">This will trigger hello SDK tooreport hello logs in real-time.</span></span>
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview

