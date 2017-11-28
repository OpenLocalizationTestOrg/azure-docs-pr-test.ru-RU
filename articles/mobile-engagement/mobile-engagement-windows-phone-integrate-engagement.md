---
title: "Интеграция пакета SDK Engagement для Windows Phone Silverlight"
description: "Интеграция Служб мобильного взаимодействия Azure с приложениями Windows Phone Silverlight"
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
ms.openlocfilehash: 29b18aecff783cebf617995e2a19f16f0b68b51b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="windows-phone-silverlight-engagement-sdk-integration"></a><span data-ttu-id="3bb42-103">Интеграция пакета SDK Engagement для Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="3bb42-103">Windows Phone Silverlight Engagement SDK Integration</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3bb42-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="3bb42-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md) 
> * [<span data-ttu-id="3bb42-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="3bb42-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [<span data-ttu-id="3bb42-106">iOS</span><span class="sxs-lookup"><span data-stu-id="3bb42-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md) 
> * [<span data-ttu-id="3bb42-107">Android</span><span class="sxs-lookup"><span data-stu-id="3bb42-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md) 
> 
> 

<span data-ttu-id="3bb42-108">Здесь описана самая простая процедура активации функций раздела аналитики и мониторинга Служб мобильного взаимодействия Azure в приложении Windows Phone Silverlight.</span><span class="sxs-lookup"><span data-stu-id="3bb42-108">This procedure describes the simplest way to activate Azure Mobile Engagement's Analytics and Monitoring functions in your Windows Phone Silverlight application.</span></span>

<span data-ttu-id="3bb42-109">Достаточно выполнить следующие шаги, чтобы активировать отчеты по журналам, которые необходимы для вычисления всех статистических данных, касающихся пользователей, сеансов, действий, сбоев и технической информации.</span><span class="sxs-lookup"><span data-stu-id="3bb42-109">The following steps are enough to activate the report of logs needed to compute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="3bb42-110">Отчеты по журналам, необходимые для вычисления других статистических данных (например, касающихся событий, ошибок и заданий), требуется активировать вручную с помощью API Служб мобильного взаимодействия (см. статью [Как использовать API для расширенного добавления тегов Служб мобильного взаимодействия в приложении Windows Phone Silverlight](mobile-engagement-windows-phone-use-engagement-api.md) ниже), так как эти статистические данные зависят от приложения.</span><span class="sxs-lookup"><span data-stu-id="3bb42-110">The report of logs needed to compute other statistics like Events, Errors and Jobs must be done manually using the Engagement API (see [How to use the advanced Mobile Engagement tagging API in your Windows Phone Silverlight app](mobile-engagement-windows-phone-use-engagement-api.md) below) since these statistics are application-dependent.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="3bb42-111">Поддерживаемые версии</span><span class="sxs-lookup"><span data-stu-id="3bb42-111">Supported versions</span></span>
<span data-ttu-id="3bb42-112">Пакет SDK для Служб мобильного взаимодействия для Windows Silverlight можно интегрировать только в приложения, предназначенные для:</span><span class="sxs-lookup"><span data-stu-id="3bb42-112">The Mobile Engagement SDK for Windows Silverlight can only be integrated into applications targeting :</span></span>

* <span data-ttu-id="3bb42-113">Windows Phone 8.0</span><span class="sxs-lookup"><span data-stu-id="3bb42-113">Windows Phone 8.0</span></span>
* <span data-ttu-id="3bb42-114">Windows Phone 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="3bb42-114">Windows Phone 8.1 Silverlight</span></span>

> [!NOTE]
> <span data-ttu-id="3bb42-115">Если вы ориентируетесь на Windows Phone 8.1 (не Silverlight), см. статью [Интеграция пакета SDK Engagement для универсальных приложений для Windows](mobile-engagement-windows-store-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="3bb42-115">If you are targeting Windows Phone 8.1 (non-Silverlight) then refer to the [Windows Universal integration procedure](mobile-engagement-windows-store-integrate-engagement.md).</span></span>
> 
> 

## <a name="install-the-mobile-engagement-silverlight-sdk"></a><span data-ttu-id="3bb42-116">Установка пакета SDK для Служб мобильного взаимодействия для Silverlight</span><span class="sxs-lookup"><span data-stu-id="3bb42-116">Install the Mobile Engagement Silverlight SDK</span></span>
<span data-ttu-id="3bb42-117">Пакет SDK Служб мобильного взаимодействия для Windows Silverlight доступен в виде пакета Nuget, который называется *MicrosoftAzure.MobileEngagement*.</span><span class="sxs-lookup"><span data-stu-id="3bb42-117">The Mobile Engagement SDK for Windows Silverlight is available as a Nuget package called *MicrosoftAzure.MobileEngagement*.</span></span> <span data-ttu-id="3bb42-118">Вы можете установить его из диспетчера пакетов NuGet в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3bb42-118">You can install it from the Visual Studio Nuget Package Manager.</span></span> 

## <a name="add-the-capabilities"></a><span data-ttu-id="3bb42-119">Добавление возможностей</span><span class="sxs-lookup"><span data-stu-id="3bb42-119">Add the capabilities</span></span>
<span data-ttu-id="3bb42-120">Для надлежащей работы пакету SDK для Engagement требуются некоторые возможности пакета SDK для Windows Phone Silverlight.</span><span class="sxs-lookup"><span data-stu-id="3bb42-120">The Engagement SDK needs some capabilities of the Windows Phone Silverlight SDK in order to work properly.</span></span>

<span data-ttu-id="3bb42-121">Откройте файл `WMAppManifest.xml` и убедитесь, что следующие возможности объявлены на панели `Capabilities`:</span><span class="sxs-lookup"><span data-stu-id="3bb42-121">Open your `WMAppManifest.xml` file and be sure that the following capabilities are declared in the `Capabilities` panel:</span></span>

* `ID_CAP_NETWORKING`
* `ID_CAP_IDENTITY_DEVICE`

## <a name="initialize-the-engagement-sdk"></a><span data-ttu-id="3bb42-122">Запуск пакета SDK для Engagement</span><span class="sxs-lookup"><span data-stu-id="3bb42-122">Initialize the Engagement SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="3bb42-123">Конфигурация Engagement</span><span class="sxs-lookup"><span data-stu-id="3bb42-123">Engagement configuration</span></span>
<span data-ttu-id="3bb42-124">Конфигурация Engagement централизована в файле `Resources\EngagementConfiguration.xml` проекта.</span><span class="sxs-lookup"><span data-stu-id="3bb42-124">The Engagement configuration is centralized in the `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="3bb42-125">Измените файл, чтобы указать:</span><span class="sxs-lookup"><span data-stu-id="3bb42-125">Edit this file to specify :</span></span>

* <span data-ttu-id="3bb42-126">строку подключения приложения между тегами `<connectionString>` and `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="3bb42-126">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="3bb42-127">Если вместо этого вам необходимо указать ее во время выполнения, можно вызвать следующий метод до инициализации агента Engagement:</span><span class="sxs-lookup"><span data-stu-id="3bb42-127">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization:</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

<span data-ttu-id="3bb42-128">Строка подключения для приложения отображается на классическом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="3bb42-128">The connection string for your application is displayed on the Azure Classic Portal.</span></span>

### <a name="engagement-initialization"></a><span data-ttu-id="3bb42-129">Инициализация Engagement</span><span class="sxs-lookup"><span data-stu-id="3bb42-129">Engagement initialization</span></span>
<span data-ttu-id="3bb42-130">При создании проекта создается файл `App.xaml.cs` .</span><span class="sxs-lookup"><span data-stu-id="3bb42-130">When you create a new project, a `App.xaml.cs` file is generated.</span></span> <span data-ttu-id="3bb42-131">Этот класс наследуется из `Application` и содержит множество важных методов.</span><span class="sxs-lookup"><span data-stu-id="3bb42-131">This class inherits from `Application` and contains many important methods.</span></span> <span data-ttu-id="3bb42-132">Он также будет использоваться для инициализации пакета SDK для Engagement.</span><span class="sxs-lookup"><span data-stu-id="3bb42-132">It will also be used to initialize the Engagement SDK.</span></span>

<span data-ttu-id="3bb42-133">Измените `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="3bb42-133">Modify the `App.xaml.cs`:</span></span>

* <span data-ttu-id="3bb42-134">Добавьте операторы `using`:</span><span class="sxs-lookup"><span data-stu-id="3bb42-134">Add to your `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="3bb42-135">Вставьте `EngagementAgent.Instance.Init` в метод `Application_Launching`:</span><span class="sxs-lookup"><span data-stu-id="3bb42-135">Insert `EngagementAgent.Instance.Init` in the `Application_Launching` method :</span></span>
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
        EngagementAgent.Instance.Init();
      }
* <span data-ttu-id="3bb42-136">Вставьте `EngagementAgent.Instance.OnActivated` в метод `Application_Activated`:</span><span class="sxs-lookup"><span data-stu-id="3bb42-136">Insert `EngagementAgent.Instance.OnActivated` in the `Application_Activated` method :</span></span>
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
      }

> [!WARNING]
> <span data-ttu-id="3bb42-137">Настоятельно рекомендуем не добавлять инициализацию Engagement в другом расположении приложения.</span><span class="sxs-lookup"><span data-stu-id="3bb42-137">We strongly discourage you to add the Engagement initialization in another place of your application.</span></span> <span data-ttu-id="3bb42-138">Однако учтите, что метод `EngagementAgent.Instance.Init` выполняется в выделенном потоке, а не в потоке пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="3bb42-138">However, be aware that the `EngagementAgent.Instance.Init` method runs on a dedicated thread, and not on the UI thread.</span></span>
> 
> 

## <a name="basic-reporting"></a><span data-ttu-id="3bb42-139">Упрощенные отчеты</span><span class="sxs-lookup"><span data-stu-id="3bb42-139">Basic reporting</span></span>
### <a name="recommended-method--overload-your-phoneapplicationpage-classes"></a><span data-ttu-id="3bb42-140">Рекомендуемый метод: перегрузка классов `PhoneApplicationPage`</span><span class="sxs-lookup"><span data-stu-id="3bb42-140">Recommended method : overload your `PhoneApplicationPage` classes</span></span>
<span data-ttu-id="3bb42-141">Чтобы активировать отчет по всем журналам, необходимым для Engagement при вычислении статистики пользователей, сеансов, действий, сбоев и технической информации, вы можете просто задать для подклассов `PhoneApplicationPage` наследование из классов `EngagementPage`.</span><span class="sxs-lookup"><span data-stu-id="3bb42-141">In order to activate the report of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `PhoneApplicationPage` sub-classes inherit from the `EngagementPage` classes.</span></span>

<span data-ttu-id="3bb42-142">Ниже приведен пример того, как сделать это для страницы приложения.</span><span class="sxs-lookup"><span data-stu-id="3bb42-142">Here is an example of how to do this for a page of your application.</span></span> <span data-ttu-id="3bb42-143">То же самое можно сделать для всех страниц приложения.</span><span class="sxs-lookup"><span data-stu-id="3bb42-143">You can do the same thing for all pages of your application.</span></span>

#### <a name="c-source-file"></a><span data-ttu-id="3bb42-144">Исходный файл на C#</span><span class="sxs-lookup"><span data-stu-id="3bb42-144">C# Source file</span></span>
<span data-ttu-id="3bb42-145">Измените файл страницы `.xaml.cs` :</span><span class="sxs-lookup"><span data-stu-id="3bb42-145">Modify your page `.xaml.cs` file :</span></span>

* <span data-ttu-id="3bb42-146">Добавьте операторы `using`:</span><span class="sxs-lookup"><span data-stu-id="3bb42-146">Add to your `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="3bb42-147">Замените `PhoneApplicationPage` на `EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="3bb42-147">Replace `PhoneApplicationPage` with `EngagementPage` :</span></span>

<span data-ttu-id="3bb42-148">**Без Engagement:**</span><span class="sxs-lookup"><span data-stu-id="3bb42-148">**Without Engagement:**</span></span>

        namespace Example
        {
          public partial class ExamplePage : PhoneApplicationPage
          {
            [...]
          }
        }

<span data-ttu-id="3bb42-149">**С Engagement:**</span><span class="sxs-lookup"><span data-stu-id="3bb42-149">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!WARNING]
> <span data-ttu-id="3bb42-150">Если страница наследуется из метода `OnNavigatedTo`, убедитесь в вызове `base.OnNavigatedTo(e)`.</span><span class="sxs-lookup"><span data-stu-id="3bb42-150">If your page inherits from the `OnNavigatedTo` method, be careful to let the `base.OnNavigatedTo(e)` call.</span></span> <span data-ttu-id="3bb42-151">В противном случае служба не сообщит о действии.</span><span class="sxs-lookup"><span data-stu-id="3bb42-151">Otherwise, the activity will not be reported.</span></span> <span data-ttu-id="3bb42-152">Более того, `EngagementPage` вызывает `StartActivity` в методе `OnNavigatedTo`.</span><span class="sxs-lookup"><span data-stu-id="3bb42-152">Indeed, the `EngagementPage` is calling `StartActivity` inside the `OnNavigatedTo` method.</span></span>
> 
> 

#### <a name="xaml-file"></a><span data-ttu-id="3bb42-153">XAML-файл</span><span class="sxs-lookup"><span data-stu-id="3bb42-153">XAML file</span></span>
<span data-ttu-id="3bb42-154">Измените файл страницы `.xaml` :</span><span class="sxs-lookup"><span data-stu-id="3bb42-154">Modify your page `.xaml` file :</span></span>

* <span data-ttu-id="3bb42-155">Добавьте в объявления пространств имен:</span><span class="sxs-lookup"><span data-stu-id="3bb42-155">Add to your namespaces declarations :</span></span>
  
      xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
* <span data-ttu-id="3bb42-156">Замените `phone:PhoneApplicationPage` на `engagement:EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="3bb42-156">Replace `phone:PhoneApplicationPage` with `engagement:EngagementPage` :</span></span>

<span data-ttu-id="3bb42-157">**Без Engagement:**</span><span class="sxs-lookup"><span data-stu-id="3bb42-157">**Without Engagement:**</span></span>

        <phone:PhoneApplicationPage>
            <!-- layout -->
        </phone:PhoneApplicationPage>

<span data-ttu-id="3bb42-158">**С Engagement:**</span><span class="sxs-lookup"><span data-stu-id="3bb42-158">**With Engagement:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP">

            <!-- layout -->
        </engagement:EngagementPage >

#### <a name="override-the-default-behavior"></a><span data-ttu-id="3bb42-159">Переопределение действия по умолчанию</span><span class="sxs-lookup"><span data-stu-id="3bb42-159">Override the default behavior</span></span>
<span data-ttu-id="3bb42-160">По умолчанию имя класса страницы сообщается как имя действия без дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="3bb42-160">By default, the class name of the page is reported as the activity name, with no extra.</span></span> <span data-ttu-id="3bb42-161">Если класс использует суффикс Page, Engagement также удалит его.</span><span class="sxs-lookup"><span data-stu-id="3bb42-161">If the class uses the "Page" suffix, Engagement will also remove it.</span></span>

<span data-ttu-id="3bb42-162">Если требуется переопределить поведение по умолчанию для имени, просто добавьте в код следующую строку:</span><span class="sxs-lookup"><span data-stu-id="3bb42-162">If you want to override the default behavior for the name, simply add this to your code:</span></span>

        // in the .xaml.cs file
        protected override string GetEngagementPageName()
        {
           /* your code */
           return "new name";
        }

<span data-ttu-id="3bb42-163">Чтобы сообщить дополнительную информацию о действии, добавьте в код следующую строку:</span><span class="sxs-lookup"><span data-stu-id="3bb42-163">If you want to report some extra information with your activity, you can add this to your code:</span></span>

        // in the .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
           /* your code */
           return extra;
        }

<span data-ttu-id="3bb42-164">Эти методы вызываются из метода `OnNavigatedTo` вашей страницы.</span><span class="sxs-lookup"><span data-stu-id="3bb42-164">These methods are called from within the `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="3bb42-165">Альтернативный метод: вызов `StartActivity()` вручную</span><span class="sxs-lookup"><span data-stu-id="3bb42-165">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="3bb42-166">Если вам не удается перегрузить классы `PhoneApplicationPage` или вы не хотите этого делать, запустите действия, вызвав методы `EngagementAgent` напрямую.</span><span class="sxs-lookup"><span data-stu-id="3bb42-166">If you cannot or do not want to overload your `PhoneApplicationPage` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="3bb42-167">Советуем вызывать `StartActivity` в методе `OnNavigatedTo` класса PhoneApplicationPage.</span><span class="sxs-lookup"><span data-stu-id="3bb42-167">We recommend calling `StartActivity` inside your `OnNavigatedTo` method of your PhoneApplicationPage.</span></span>

        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
           base.OnNavigatedTo(e);
           EngagementAgent.Instance.StartActivity("MyPage");
        }

> [!IMPORTANT]
> <span data-ttu-id="3bb42-168">Убедитесь, что сеанс завершен правильно.</span><span class="sxs-lookup"><span data-stu-id="3bb42-168">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="3bb42-169">Пакет SDK автоматически вызывает метод `EndActivity` при закрытии приложения.</span><span class="sxs-lookup"><span data-stu-id="3bb42-169">The SDK automatically calls the `EndActivity` method when the application is closed.</span></span> <span data-ttu-id="3bb42-170">Поэтому мы **настоятельно** рекомендуем вызывать метод `StartActivity` при каждом изменении действия пользователя и **никогда** не вызывать метод `EndActivity`.</span><span class="sxs-lookup"><span data-stu-id="3bb42-170">Thus, it is **HIGHLY** recommended to call the `StartActivity` method whenever the activity of the user change, and to **NEVER** call the `EndActivity` method.</span></span> <span data-ttu-id="3bb42-171">Этот метод отправляет на сервер Engagement сообщение о том, что текущий пользователь вышел из приложения, и это отражается во всех журналах приложений.</span><span class="sxs-lookup"><span data-stu-id="3bb42-171">This method sends a message to the Engagement server that the current user has left the application and this impacts all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="3bb42-172">Расширенные отчеты</span><span class="sxs-lookup"><span data-stu-id="3bb42-172">Advanced reporting</span></span>
<span data-ttu-id="3bb42-173">При желании можно также сообщать об определенных событиях, ошибках и заданиях приложения. Это можно сделать с помощью других методов в классе `EngagementAgent`.</span><span class="sxs-lookup"><span data-stu-id="3bb42-173">Optionally, you may want to report application specific events, errors and jobs, to do so, use the others methods found in the `EngagementAgent` class.</span></span> <span data-ttu-id="3bb42-174">Engagement API позволяет использовать все дополнительные возможности Engagement.</span><span class="sxs-lookup"><span data-stu-id="3bb42-174">The Engagement API allows to use all of Engagement's advanced capabilities.</span></span>

<span data-ttu-id="3bb42-175">Дополнительные сведения см. в статье [Как использовать API Служб мобильного взаимодействия в Windows Phone Silverlight](mobile-engagement-windows-phone-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="3bb42-175">For further information, see [How to use the advanced Mobile Engagement tagging API in your Windows Phone Silverlight app](mobile-engagement-windows-phone-use-engagement-api.md).</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="3bb42-176">Расширенная конфигурация</span><span class="sxs-lookup"><span data-stu-id="3bb42-176">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="3bb42-177">Отключение автоматического создания отчетов о сбоях</span><span class="sxs-lookup"><span data-stu-id="3bb42-177">Disable automatic crash reporting</span></span>
<span data-ttu-id="3bb42-178">Вы можете отключить функцию автоматического создания отчетов о сбоях в Engagement.</span><span class="sxs-lookup"><span data-stu-id="3bb42-178">You can disable the automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="3bb42-179">После этого при возникновении необработанного исключения Engagement не будет предпринимать никаких действий.</span><span class="sxs-lookup"><span data-stu-id="3bb42-179">Then, when an unhandled exception will occur, Engagement won't do anything.</span></span>

> [!WARNING]
> <span data-ttu-id="3bb42-180">Если вы планируете отключить эту функцию, учтите, что при возникновении необработанного сбоя в приложении Engagement не будет отправлять уведомление о сбое **И** не закроет сеанс и задания.</span><span class="sxs-lookup"><span data-stu-id="3bb42-180">If you plan to disable this feature, be aware that when a unhandled crash will occur in your app, Engagement will not send the crash **AND** it will not close the session and jobs.</span></span>
> 
> 

<span data-ttu-id="3bb42-181">Чтобы отключить автоматическое создание отчетов о сбоях, просто настройте конфигурацию в зависимости от того, как она была объявлена:</span><span class="sxs-lookup"><span data-stu-id="3bb42-181">To disable automatic crash reporting, just customize your configuration depending on the way you declared it :</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="3bb42-182">Из файла `EngagementConfiguration.xml`</span><span class="sxs-lookup"><span data-stu-id="3bb42-182">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="3bb42-183">Задайте для параметра уведомления о сбоях значение `false` между тегами `<reportCrash>` и `</reportCrash>`.</span><span class="sxs-lookup"><span data-stu-id="3bb42-183">Set report crash to `false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="3bb42-184">Из объекта `EngagementConfiguration` во время выполнения</span><span class="sxs-lookup"><span data-stu-id="3bb42-184">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="3bb42-185">Задайте для параметра уведомления о сбоях значение false с помощью объекта EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="3bb42-185">Set report crash to false using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration(); engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";
        /\* Disable Engagement crash reporting. \*/ engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a><span data-ttu-id="3bb42-186">Пакетный режим</span><span class="sxs-lookup"><span data-stu-id="3bb42-186">Burst mode</span></span>
<span data-ttu-id="3bb42-187">По умолчанию служба Engagement ведет отчеты по журналам в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="3bb42-187">By default, the Engagement service reports logs in real time.</span></span> <span data-ttu-id="3bb42-188">Если приложение создает отчеты по журналам очень часто, лучше поместить журналы в буфер и создавать отчеты по всем журналам одновременно через регулярные промежутки времени (это называется «пакетный режим»).</span><span class="sxs-lookup"><span data-stu-id="3bb42-188">If your application reports logs very frequently, it is better to buffer the logs and to report them all at once on a regular time base (this is called the “burst mode”).</span></span>

<span data-ttu-id="3bb42-189">Для этого вызовите следующий метод:</span><span class="sxs-lookup"><span data-stu-id="3bb42-189">To do so, call the method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="3bb42-190">Значение аргумента задается в **миллисекундах**.</span><span class="sxs-lookup"><span data-stu-id="3bb42-190">The argument is a value in **milliseconds**.</span></span> <span data-ttu-id="3bb42-191">Если вам в любое время потребуется повторно активировать ведение журнала в реальном времени, просто вызовите метод без каких-либо параметров или со значением 0.</span><span class="sxs-lookup"><span data-stu-id="3bb42-191">At any time, if you want to reactivate the real-time logging, just call the method without any parameter, or with the 0 value.</span></span>

<span data-ttu-id="3bb42-192">Пакетный режим немного продлевает время работы батареи, но влияет на Engagement Monitor: время выполнения всех сеансов и заданий будет округляться до порогового значения пакета (таким образом, сеансы и задания, время выполнения которых короче, чем пороговое значение пакета, могут не отображаться).</span><span class="sxs-lookup"><span data-stu-id="3bb42-192">The burst mode slightly increase the battery life but has an impact on the Engagement Monitor: all sessions and jobs duration will be rounded to the burst threshold (thus, sessions and jobs shorter than the burst threshold may not be visible).</span></span> <span data-ttu-id="3bb42-193">Мы советуем использовать пороговое значение пакета не более чем 30 000 (30 с).</span><span class="sxs-lookup"><span data-stu-id="3bb42-193">It is recommended to use a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="3bb42-194">Следует иметь в виду, что в сохраняемых журналах может быть не более 300 элементов.</span><span class="sxs-lookup"><span data-stu-id="3bb42-194">You have to be aware that saved logs are limited to 300 items.</span></span> <span data-ttu-id="3bb42-195">Если отправка занимает слишком много времени, некоторые журналы могут быть потеряны.</span><span class="sxs-lookup"><span data-stu-id="3bb42-195">If sending is too long you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="3bb42-196">Для порогового значения пакета нельзя настроить период менее одной секунды.</span><span class="sxs-lookup"><span data-stu-id="3bb42-196">The burst threshold cannot be configured to a period lesser than one second.</span></span> <span data-ttu-id="3bb42-197">При попытке задать значение менее одной секунды трассировка в пакете SDK отобразится с ошибкой, и будет автоматически восстановлено значения по умолчанию, т. е. ноль секунд.</span><span class="sxs-lookup"><span data-stu-id="3bb42-197">If you try to do so, the SDK will show a trace with the error and will automatically reset to the default value, that is, zero seconds.</span></span> <span data-ttu-id="3bb42-198">Это приведет к тому, что пакет SDK начнет создавать отчеты по журналам в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="3bb42-198">This will trigger the SDK to report the logs in real-time.</span></span>
> 
> 

