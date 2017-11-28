---
title: "aaaWindows универсальной дополнительные отчеты с MobileApps Engagement"
description: "Как tooIntegrate Azure Mobile Engagement с универсальные приложения Windows"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: ea5030bf-73ac-49b7-bc3e-c25fc10e945a
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 20968f238ef7ae9dc0b8bb6dac3fb8bdb9bc3a10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-reporting-with-hello-windows-universal-apps-engagement-sdk"></a><span data-ttu-id="067a4-103">Дополнительных отчетов с помощью пакета SDK Engagement универсальных приложений Windows hello</span><span class="sxs-lookup"><span data-stu-id="067a4-103">Advanced Reporting with hello Windows Universal Apps Engagement SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="067a4-104">Универсальная платформа Windows</span><span class="sxs-lookup"><span data-stu-id="067a4-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-reporting.md)
> * [<span data-ttu-id="067a4-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="067a4-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="067a4-106">iOS</span><span class="sxs-lookup"><span data-stu-id="067a4-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="067a4-107">Android</span><span class="sxs-lookup"><span data-stu-id="067a4-107">Android</span></span>](mobile-engagement-android-advanced-reporting.md)
> 
> 

<span data-ttu-id="067a4-108">В этом разделе описаны дополнительные сценарии создания отчетов в универсальном приложении для Windows.</span><span class="sxs-lookup"><span data-stu-id="067a4-108">This topic describes additional reporting scenarios in your Windows Universal application.</span></span> <span data-ttu-id="067a4-109">К таким сценариям относятся параметры, которые вы можете tooapply toohello приложения, созданного в hello [Приступая к работе](mobile-engagement-windows-store-dotnet-get-started.md) учебника.</span><span class="sxs-lookup"><span data-stu-id="067a4-109">These scenarios include options that you can choose tooapply toohello app created in hello [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) tutorial.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="067a4-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="067a4-110">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

<span data-ttu-id="067a4-111">Перед запуском этого учебника, необходимо сначала выполнить hello [Приступая к работе](mobile-engagement-windows-store-dotnet-get-started.md) руководство, в котором намеренно прямой и простой.</span><span class="sxs-lookup"><span data-stu-id="067a4-111">Before starting this tutorial, you must first complete hello [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) tutorial, which is deliberately direct and simple.</span></span> <span data-ttu-id="067a4-112">В этом учебнике рассматриваются дополнительные параметры, доступные для выбора.</span><span class="sxs-lookup"><span data-stu-id="067a4-112">This tutorial covers additional options you can choose from.</span></span>

## <a name="specifying-engagement-configuration-at-runtime"></a><span data-ttu-id="067a4-113">Указание конфигурации Engagement во время выполнения</span><span class="sxs-lookup"><span data-stu-id="067a4-113">Specifying engagement configuration at runtime</span></span>
<span data-ttu-id="067a4-114">централизованный Hello проектной конфигурации в hello `Resources\EngagementConfiguration.xml` файл проекта, где он был задан в hello [Приступая к работе](mobile-engagement-windows-store-dotnet-get-started.md) раздела.</span><span class="sxs-lookup"><span data-stu-id="067a4-114">hello Engagement configuration is centralized in hello `Resources\EngagementConfiguration.xml` file of your project, which is where it was specified in hello [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) topic.</span></span>

<span data-ttu-id="067a4-115">Но также можно указать во время выполнения: вы можете вызвать следующий метод до инициализации агента Engagement hello hello:</span><span class="sxs-lookup"><span data-stu-id="067a4-115">But you can also specify it at runtime: you can call hello following method before hello Engagement agent initialization:</span></span>

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set hello Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);



## <a name="recommended-method-overload-your-page-classes"></a><span data-ttu-id="067a4-116">Рекомендуемый метод: перегрузка классов `Page`</span><span class="sxs-lookup"><span data-stu-id="067a4-116">Recommended method: overload your `Page` classes</span></span>
<span data-ttu-id="067a4-117">tooactivate hello reporting всех журналов hello, необходимых в Engagement toocompute пользователей, сеансы, действия, сбои и технические данные, внести все вашей `Page` вложенные классы наследуют от hello `EngagementPage` классы.</span><span class="sxs-lookup"><span data-stu-id="067a4-117">tooactivate hello reporting of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, make all your `Page` sub-classes inherit from hello `EngagementPage` classes.</span></span>

<span data-ttu-id="067a4-118">Ниже приведен пример страницы приложения.</span><span class="sxs-lookup"><span data-stu-id="067a4-118">Here is an example for a page of your application.</span></span> <span data-ttu-id="067a4-119">Можно сделать hello одинаково для всех страниц приложения.</span><span class="sxs-lookup"><span data-stu-id="067a4-119">You can do hello same thing for all pages of your application.</span></span>

### <a name="c-source-file"></a><span data-ttu-id="067a4-120">Исходный файл на C#</span><span class="sxs-lookup"><span data-stu-id="067a4-120">C# Source file</span></span>
<span data-ttu-id="067a4-121">Измените файл страницы `.xaml.cs` :</span><span class="sxs-lookup"><span data-stu-id="067a4-121">Modify your page `.xaml.cs` file:</span></span>

* <span data-ttu-id="067a4-122">Добавить tooyour `using` инструкции:</span><span class="sxs-lookup"><span data-stu-id="067a4-122">Add tooyour `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="067a4-123">Замените `Page` на `EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="067a4-123">Replace `Page` with `EngagementPage`:</span></span>

<span data-ttu-id="067a4-124">**Без Engagement:**</span><span class="sxs-lookup"><span data-stu-id="067a4-124">**Without Engagement:**</span></span>

        namespace Example
        {
          public sealed partial class ExamplePage : Page
          {
            [...]
          }
        }

<span data-ttu-id="067a4-125">**С Engagement:**</span><span class="sxs-lookup"><span data-stu-id="067a4-125">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public sealed partial class ExamplePage : EngagementPage
          {
            [...]
          }
        }

> [!IMPORTANT]
> <span data-ttu-id="067a4-126">Если на странице переопределяет hello `OnNavigatedTo` метода будет убедиться, что toocall `base.OnNavigatedTo(e)`.</span><span class="sxs-lookup"><span data-stu-id="067a4-126">If your page overrides hello `OnNavigatedTo` method, be sure toocall `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="067a4-127">В противном случае действие hello не будут отображаться (hello `EngagementPage` вызовы `StartActivity` внутри его `OnNavigatedTo` метода).</span><span class="sxs-lookup"><span data-stu-id="067a4-127">Otherwise, hello activity is not be reported (hello `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span>
> 
> 

### <a name="xaml-file"></a><span data-ttu-id="067a4-128">XAML-файл</span><span class="sxs-lookup"><span data-stu-id="067a4-128">XAML file</span></span>
<span data-ttu-id="067a4-129">Измените файл страницы `.xaml` :</span><span class="sxs-lookup"><span data-stu-id="067a4-129">Modify your page `.xaml` file:</span></span>

* <span data-ttu-id="067a4-130">Добавьте tooyour объявления пространств имен:</span><span class="sxs-lookup"><span data-stu-id="067a4-130">Add tooyour namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement"
* <span data-ttu-id="067a4-131">Замените `Page` на `engagement:EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="067a4-131">Replace `Page` with `engagement:EngagementPage`:</span></span>

<span data-ttu-id="067a4-132">**Без Engagement:**</span><span class="sxs-lookup"><span data-stu-id="067a4-132">**Without Engagement:**</span></span>

        <Page>
            <!-- layout -->
            ...
        </Page>

<span data-ttu-id="067a4-133">**С Engagement:**</span><span class="sxs-lookup"><span data-stu-id="067a4-133">**With Engagement:**</span></span>

        <engagement:EngagementPage
            xmlns:engagement="using:Microsoft.Azure.Engagement">
            <!-- layout -->
            ...
        </engagement:EngagementPage >

### <a name="override-hello-default-behaviour"></a><span data-ttu-id="067a4-134">Переопределение поведения по умолчанию hello</span><span class="sxs-lookup"><span data-stu-id="067a4-134">Override hello default behaviour</span></span>
<span data-ttu-id="067a4-135">По умолчанию имя класса hello страницы приветствия отображается как имя действия hello с без дополнительных.</span><span class="sxs-lookup"><span data-stu-id="067a4-135">By default, hello class name of hello page is reported as hello activity name, with no extra.</span></span> <span data-ttu-id="067a4-136">Если класс hello использует hello суффикс «Страница», Engagement удаляет его.</span><span class="sxs-lookup"><span data-stu-id="067a4-136">If hello class uses hello "Page" suffix, Engagement removes it.</span></span>

<span data-ttu-id="067a4-137">поведение по умолчанию hello toooverride имени hello, добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="067a4-137">toooverride hello default behavior for hello name, add this code:</span></span>

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

<span data-ttu-id="067a4-138">tooreport дополнительных сведений с действием, добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="067a4-138">tooreport extra information with your activity, add this code:</span></span>

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

<span data-ttu-id="067a4-139">Эти методы вызываются из внутри hello `OnNavigatedTo` метод страницы.</span><span class="sxs-lookup"><span data-stu-id="067a4-139">These methods are called from within hello `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="067a4-140">Альтернативный метод: вызов `StartActivity()` вручную</span><span class="sxs-lookup"><span data-stu-id="067a4-140">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="067a4-141">Если невозможно или нежелательно toooverload вашей `Page` классы, вместо этого можно запустить ваши действия путем вызова `EngagementAgent` методы напрямую.</span><span class="sxs-lookup"><span data-stu-id="067a4-141">If you cannot or do not want toooverload your `Page` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="067a4-142">Рекомендуем вызывать `StartActivity` внутри метода `OnNavigatedTo` своей страницы.</span><span class="sxs-lookup"><span data-stu-id="067a4-142">We recommend calling `StartActivity` inside your `OnNavigatedTo` method of your Page.</span></span>

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> <span data-ttu-id="067a4-143">Убедитесь, что сеанс завершен правильно.</span><span class="sxs-lookup"><span data-stu-id="067a4-143">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="067a4-144">пакет SDK для Universal Windows Hello автоматически вызывает hello `EndActivity` метод при закрытии приложения hello.</span><span class="sxs-lookup"><span data-stu-id="067a4-144">hello Windows Universal SDK automatically calls hello `EndActivity` method when hello application is closed.</span></span> <span data-ttu-id="067a4-145">Таким образом, **высокой** рекомендуется toocall hello `StartActivity` метод изменении hello действий пользователя hello и слишком**никогда** hello вызовов `EndActivity` метод.</span><span class="sxs-lookup"><span data-stu-id="067a4-145">Thus, it is **HIGHLY** recommended toocall hello `StartActivity` method whenever hello activity of hello user change, and too**NEVER** call hello `EndActivity` method.</span></span> <span data-ttu-id="067a4-146">Этот метод уведомляет сервер занят hello что hello текущий пользователь покинул приложения hello, что повлияет на все журналы приложений.</span><span class="sxs-lookup"><span data-stu-id="067a4-146">This method notifies hello Engagement server that hello current user has left hello application, which will impact all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="067a4-147">Расширенные отчеты</span><span class="sxs-lookup"><span data-stu-id="067a4-147">Advanced reporting</span></span>
<span data-ttu-id="067a4-148">При необходимости вы можете tooreport события конкретного приложения, ошибок и задания, toodo таким образом, использование hello другие методы найдены в hello `EngagementAgent` класса.</span><span class="sxs-lookup"><span data-stu-id="067a4-148">Optionally, you may want tooreport application-specific events, errors and jobs, toodo so, use hello others methods found in hello `EngagementAgent` class.</span></span> <span data-ttu-id="067a4-149">Hello Engagement API позволяет использовать расширенные возможности всех обязательств.</span><span class="sxs-lookup"><span data-stu-id="067a4-149">hello Engagement API allows use of all Engagement's advanced capabilities.</span></span>

<span data-ttu-id="067a4-150">Дополнительные сведения см. в разделе [как toouse hello дополнительные теги API в приложении универсальное приложение для Windows Mobile Engagement](mobile-engagement-windows-store-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="067a4-150">For further information, see [How toouse hello advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md).</span></span>

