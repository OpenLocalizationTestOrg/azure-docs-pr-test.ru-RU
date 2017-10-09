---
title: "aaaWindows Phone Silverlight достичь SDK-интеграция"
description: "Как tooIntegrate Azure Mobile Engagement связаться с приложениями Silverlight для Windows Phone"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: d3516a6b-db9f-4cdb-a475-4148edf81af1
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 09c8767216e11963c5c600755ab8d4d11cd92034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-reach-sdk-integration"></a><span data-ttu-id="75311-103">Интеграция пакета SDK Reach для Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="75311-103">Windows Phone Silverlight Reach SDK Integration</span></span>
<span data-ttu-id="75311-104">Необходимо выполнить процедуры интеграции hello, описанной в hello [Windows Phone Silverlight Engagement SDK-Интеграция](mobile-engagement-windows-phone-integrate-engagement.md) до следующего руководства.</span><span class="sxs-lookup"><span data-stu-id="75311-104">You must follow hello integration procedure described in hello [Windows Phone Silverlight Engagement SDK Integration](mobile-engagement-windows-phone-integrate-engagement.md) before following this guide.</span></span>

## <a name="embed-hello-engagement-reach-sdk-into-your-windows-phone-silverlight-project"></a><span data-ttu-id="75311-105">Внедрение hello Engagement Reach SDK в проект Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="75311-105">Embed hello Engagement Reach SDK into your Windows Phone Silverlight project</span></span>
<span data-ttu-id="75311-106">У вас ничего tooadd.</span><span class="sxs-lookup"><span data-stu-id="75311-106">You do not have anything tooadd.</span></span> <span data-ttu-id="75311-107">`EngagementReach` уже включены в проект.</span><span class="sxs-lookup"><span data-stu-id="75311-107">`EngagementReach` references and resources are already in your project.</span></span>

> [!TIP]
> <span data-ttu-id="75311-108">Образы, расположенный в hello можно настраивать `Resources` папки проекта, особенно hello фирменной символики значок (что по умолчанию toohello Engagement).</span><span class="sxs-lookup"><span data-stu-id="75311-108">You can customize images located in hello `Resources` folder of your project, especially hello brand icon (that default toohello Engagement icon).</span></span>
> 
> 

## <a name="add-hello-capabilities"></a><span data-ttu-id="75311-109">Добавление возможностей hello</span><span class="sxs-lookup"><span data-stu-id="75311-109">Add hello capabilities</span></span>
<span data-ttu-id="75311-110">Hello Engagement Reach SDK должен некоторые дополнительные возможности.</span><span class="sxs-lookup"><span data-stu-id="75311-110">hello Engagement Reach SDK needs some additional capabilities.</span></span>

<span data-ttu-id="75311-111">Откройте ваш `WMAppManifest.xml` файл и убедитесь, что объявлены, hello следующие возможности:</span><span class="sxs-lookup"><span data-stu-id="75311-111">Open your `WMAppManifest.xml` file and be sure that hello following capabilities are declared:</span></span>

* `ID_CAP_PUSH_NOTIFICATION`
* `ID_CAP_WEBBROWSERCOMPONENT`

<span data-ttu-id="75311-112">Hello сначала используется один по hello MPNS службы tooallow hello отображение всплывающего уведомления.</span><span class="sxs-lookup"><span data-stu-id="75311-112">hello first one is used by hello MPNS service tooallow hello display of toast notification.</span></span> <span data-ttu-id="75311-113">Hello второе — это используемые tooembed задачу браузера в hello SDK.</span><span class="sxs-lookup"><span data-stu-id="75311-113">hello second one is used tooembed a browser task into hello SDK.</span></span>

<span data-ttu-id="75311-114">Изменить hello `WMAppManifest.xml` и добавьте внутри hello `<Capabilities />` тег:</span><span class="sxs-lookup"><span data-stu-id="75311-114">Edit hello `WMAppManifest.xml` file and add inside hello `<Capabilities />` tag :</span></span>

    <Capability Name="ID_CAP_PUSH_NOTIFICATION" />
    <Capability Name="ID_CAP_WEBBROWSERCOMPONENT" />

## <a name="enable-hello-microsoft-push-notification-service"></a><span data-ttu-id="75311-115">Включить hello Microsoft Push Notification Service</span><span class="sxs-lookup"><span data-stu-id="75311-115">Enable hello Microsoft Push Notification Service</span></span>
<span data-ttu-id="75311-116">В порядке hello toouse **Microsoft Push Notification Service** (называемый MPNS) вашего `WMAppManifest.xml` файл должен иметь `<App />` тег с `Publisher` атрибут значение toohello имя проекта.</span><span class="sxs-lookup"><span data-stu-id="75311-116">In order toouse hello **Microsoft Push Notification Service** (referred as MPNS) your `WMAppManifest.xml` file must have an `<App />` tag with a `Publisher` attribute set toohello name of your project.</span></span>

## <a name="initialize-hello-engagement-reach-sdk"></a><span data-ttu-id="75311-117">Инициализировать hello Engagement Reach SDK</span><span class="sxs-lookup"><span data-stu-id="75311-117">Initialize hello Engagement Reach SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="75311-118">Конфигурация Engagement</span><span class="sxs-lookup"><span data-stu-id="75311-118">Engagement configuration</span></span>
<span data-ttu-id="75311-119">централизованный Hello проектной конфигурации в hello `Resources\EngagementConfiguration.xml` файла проекта.</span><span class="sxs-lookup"><span data-stu-id="75311-119">hello Engagement configuration is centralized in hello `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="75311-120">Измените эту настройку reach toospecify файла:</span><span class="sxs-lookup"><span data-stu-id="75311-120">Edit this file toospecify reach configuration :</span></span>

* <span data-ttu-id="75311-121">*Необязательный*, показывают, как активировать hello системных Push-уведомлений (MPNS) или не между `<enableNativePush>` и `</enableNativePush>` теги (`true` по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="75311-121">*Optional*, indicate whether hello native push (MPNS) is activated or not between `<enableNativePush>` and `</enableNativePush>` tags, (`true` by default).</span></span>
* <span data-ttu-id="75311-122">*Необязательный*, указывающей hello hello принудительной канал между `<channelName>` и `</channelName>` теги, предоставляют hello же, что приложение в настоящее время может использовать или оставьте поле пустым.</span><span class="sxs-lookup"><span data-stu-id="75311-122">*Optional*, indicate hello name of hello push channel between `<channelName>` and `</channelName>` tags, provide hello same that your application may currently use or leave it empty.</span></span>

<span data-ttu-id="75311-123">Если требуется, чтобы его во время выполнения вместо этого можно вызвать следующие hello toospecify метод до инициализации агента Engagement hello:</span><span class="sxs-lookup"><span data-stu-id="75311-123">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization :</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    engagementConfiguration.Reach.EnableNativePush = true;                  
    /* [Optional] whether hello native push (MPNS) is activated or not. */

    engagementConfiguration.Reach.ChannelName = "YOUR_PUSH_CHANNEL_NAME";   
    /* [Optional] Provide hello same channel name that your application may currently use. */

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

> [!TIP]
> <span data-ttu-id="75311-124">Можно указать имя hello канала push hello MPNS приложения.</span><span class="sxs-lookup"><span data-stu-id="75311-124">You can specify hello name of hello MPNS push channel of your application.</span></span> <span data-ttu-id="75311-125">По умолчанию Engagement создает имя, основанное на hello appId.</span><span class="sxs-lookup"><span data-stu-id="75311-125">By default, Engagement creates a name based on hello appId.</span></span> <span data-ttu-id="75311-126">У вас нет необходимости toospecify hello имя самостоятельно, за исключением того, если планируется канала push hello toouse за пределами обязательств.</span><span class="sxs-lookup"><span data-stu-id="75311-126">You have no need toospecify hello name yourself, except if you plan toouse hello push channel outside of Engagement.</span></span>
> 
> 

### <a name="engagement-initialization"></a><span data-ttu-id="75311-127">Инициализация Engagement</span><span class="sxs-lookup"><span data-stu-id="75311-127">Engagement initialization</span></span>
<span data-ttu-id="75311-128">Изменение hello `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="75311-128">Modify hello `App.xaml.cs`:</span></span>

* <span data-ttu-id="75311-129">Добавить tooyour `using` инструкции:</span><span class="sxs-lookup"><span data-stu-id="75311-129">Add tooyour `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="75311-130">Вставьте `EngagementReach.Instance.Init` сразу `EngagementAgent.Instance.Init` после в `Application_Launching`:</span><span class="sxs-lookup"><span data-stu-id="75311-130">Insert `EngagementReach.Instance.Init` just after `EngagementAgent.Instance.Init` in `Application_Launching` :</span></span>
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
         EngagementAgent.Instance.Init();
         EngagementReach.Instance.Init();
      }
* <span data-ttu-id="75311-131">Вставить `EngagementReach.Instance.OnActivated` в hello `Application_Activated` метод:</span><span class="sxs-lookup"><span data-stu-id="75311-131">Insert `EngagementReach.Instance.OnActivated` in hello `Application_Activated` method :</span></span>
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
         EngagementReach.Instance.OnActivated(e);
      }

> [!IMPORTANT]
> <span data-ttu-id="75311-132">Hello `EngagementReach.Instance.Init` выполняется в выделенном потоке.</span><span class="sxs-lookup"><span data-stu-id="75311-132">hello `EngagementReach.Instance.Init` runs in a dedicated thread.</span></span> <span data-ttu-id="75311-133">У вас toodo его самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="75311-133">You do not have toodo it yourself.</span></span>
> 
> 

## <a name="app-store-submission-considerations"></a><span data-ttu-id="75311-134">Замечания по отправке приложений в Магазин</span><span class="sxs-lookup"><span data-stu-id="75311-134">App store submission considerations</span></span>
<span data-ttu-id="75311-135">Microsoft накладывает некоторые правила, при использовании hello push-уведомлений:</span><span class="sxs-lookup"><span data-stu-id="75311-135">Microsoft imposes some rules when using hello push notifications:</span></span>

<span data-ttu-id="75311-136">Из hello Microsoft [политики применения] документации, разделе 2.9:</span><span class="sxs-lookup"><span data-stu-id="75311-136">From hello Microsoft [Application Policies] documentation, section 2.9:</span></span>

1) <span data-ttu-id="75311-137">Должно попросите hello пользователя tooaccept tooreceive push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="75311-137">You must ask hello user tooaccept tooreceive push notifications.</span></span> <span data-ttu-id="75311-138">В параметрах, добавьте способом toodisable hello push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="75311-138">Then, in your settings, add a way toodisable hello push notifications.</span></span>

<span data-ttu-id="75311-139">Объект EngagementReach Hello предоставляет два методы toomanage hello в/opt отказаться, `EnableNativePush()` и `DisableNativePush()`.</span><span class="sxs-lookup"><span data-stu-id="75311-139">hello EngagementReach object provides two methods toomanage hello opt-in/opt-out, `EnableNativePush()` and `DisableNativePush()`.</span></span> <span data-ttu-id="75311-140">Например, невозможно создать параметр в параметрах hello с toodisable переключателя или включить MPNS.</span><span class="sxs-lookup"><span data-stu-id="75311-140">You could, for example, create an option in hello settings with a toggle toodisable or enable MPNS.</span></span>

<span data-ttu-id="75311-141">Можно также toodeactivate MPNS через конфигурацию hello Engagement\<windows phone-sdk-reach конфигурации\>.</span><span class="sxs-lookup"><span data-stu-id="75311-141">You can also decide toodeactivate MPNS through hello Engagement configuration\<windows-phone-sdk-reach-configuration\>.</span></span>

> <span data-ttu-id="75311-142">2.9.1) приложения hello сначала необходимо описать предоставленный toobe уведомления hello и **получения явного разрешения пользователя hello (opt-in)**, и **необходимо предоставить механизм, посредством которой hello пользователя можно отказаться от получения Push-уведомления**.</span><span class="sxs-lookup"><span data-stu-id="75311-142">2.9.1) hello application must first describe hello notifications toobe provided and **obtain hello user’s express permission (opt-in)**, and **must provide a mechanism through which hello user can opt out of receiving push notifications**.</span></span> <span data-ttu-id="75311-143">Все уведомления с помощью hello Microsoft Push Notification Service должны быть согласованы с пользователем toohello описание hello и должны соблюдать все применимые [политики применения] [ Content Policies]и [Дополнительные требования для конкретного приложения типов].</span><span class="sxs-lookup"><span data-stu-id="75311-143">All notifications provided using hello Microsoft Push Notification Service must be consistent with hello description provided toohello user and must comply with all applicable [Application Policies][Content Policies] and [Additional Requirements for Specific Application Types].</span></span>
> 
> 

2) <span data-ttu-id="75311-144">Не следует использовать слишком много push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="75311-144">You should not use too many push notifications.</span></span> <span data-ttu-id="75311-145">Управлять уведомлениями будет Engagement.</span><span class="sxs-lookup"><span data-stu-id="75311-145">Engagement will handle notifications for you.</span></span>

> <span data-ttu-id="75311-146">2.9.2) приложение hello и ее использование hello Microsoft Push Notification Service должен не слишком пропускной способности сети или пропускной способности hello Microsoft Push Notification Service, а в противном случае происходит чрезмерного обременять Windows Phone или другие устройства Microsoft или службы с чрезмерным push-уведомления, по определению корпорации Майкрософт по ее обоснованному усмотрению и не должно нанести вред или помешать любой сетей Майкрософт или серверов или все серверы сторонних производителей или toohello подключенной сети служба Push-уведомлений Microsoft.</span><span class="sxs-lookup"><span data-stu-id="75311-146">2.9.2) hello application and its use of hello Microsoft Push Notification Service must not excessively use network capacity or bandwidth of hello Microsoft Push Notification Service, or otherwise unduly burden a Windows Phone or other Microsoft device or service with excessive push notifications, as determined by Microsoft in its reasonable discretion, and must not harm or interfere with any Microsoft networks or servers or any third party servers or networks connected toohello Microsoft Push Notification Service.</span></span>
> 
> 

3) <span data-ttu-id="75311-147">Не следует полагаться на MPNS toosend criticals сведения.</span><span class="sxs-lookup"><span data-stu-id="75311-147">Do not rely on MPNS toosend criticals information.</span></span> <span data-ttu-id="75311-148">Engagement использует MPNS, поэтому это правило также применяется для кампаний hello, созданный внутри hello Engagement переднего плана.</span><span class="sxs-lookup"><span data-stu-id="75311-148">Engagement uses MPNS, so this rule also applies for hello campaigns created inside hello Engagement front-end.</span></span>

> <span data-ttu-id="75311-149">2.9.3) hello Microsoft Push Notification Service не может быть используется toosend уведомлений, которые являются критически важных или иным образом может повлиять на вопросы и ответы жизни или смерти, включая без ограничения критических уведомлений связанные tooa Медицинские устройства или условий.</span><span class="sxs-lookup"><span data-stu-id="75311-149">2.9.3) hello Microsoft Push Notification Service may not be used toosend notifications that are mission critical or otherwise could affect matters of life or death, including without limitation critical notifications related tooa medical device or condition.</span></span> <span data-ttu-id="75311-150">Майкрософт ПРЯМО отказывается от ANY никаких гарантий, hello используйте из hello MICROSOFT PUSH уведомления службы или ДОСТАВКИ из MICROSOFT PUSH-УВЕДОМЛЕНИЙ службы уведомления будет быть без ПЕРЕРЫВА, ошибка свободного или, в противном случае ГАРАНТИРУЕТСЯ tooOCCUR ON в реальном времени ОТДЕЛЬНО.</span><span class="sxs-lookup"><span data-stu-id="75311-150">MICROSOFT EXPRESSLY DISCLAIMS ANY WARRANTIES THAT hello USE OF hello MICROSOFT PUSH NOTIFICATION SERVICE OR DELIVERY OF MICROSOFT PUSH NOTIFICATION SERVICE NOTIFICATIONS WILL BE UNINTERRUPTED, ERROR FREE, OR OTHERWISE GUARANTEED tooOCCUR ON A REAL-TIME BASIS.</span></span>
> 
> 

<span data-ttu-id="75311-151">**Мы не можем гарантировать, приложение передаст hello процесса проверки, если вы не влияют на следующие рекомендации.**</span><span class="sxs-lookup"><span data-stu-id="75311-151">**We cannot guarantee that your application will pass hello validation process if you do not respect these recommendations.**</span></span>

## <a name="handle-data-push-optional"></a><span data-ttu-id="75311-152">Обработка отправленных данных (необязательно)</span><span class="sxs-lookup"><span data-stu-id="75311-152">Handle data push (optional)</span></span>
<span data-ttu-id="75311-153">Если требуется вашего приложения toobe может tooreceive Reach данных Push-уведомлений, имеется tooimplement двумя событиями hello EngagementReach класса:</span><span class="sxs-lookup"><span data-stu-id="75311-153">If you want your application toobe able tooreceive Reach data pushes, you have tooimplement two events of hello EngagementReach class:</span></span>

    EngagementReach.Instance.DataPushStringReceived += (body) =>
    {
       Debug.WriteLine("String data push message received: " + body);
       return true;
    };

    EngagementReach.Instance.DataPushBase64Received += (decodedBody, encodedBody) =>
    {
       Debug.WriteLine("Base64 data push message received: " + encodedBody);
       // Do something useful with decodedBody like updating an image view
       return true;
    };

<span data-ttu-id="75311-154">Вы увидите ответного вызова hello каждый метод возвращает логическое значение.</span><span class="sxs-lookup"><span data-stu-id="75311-154">You can see that hello callback of each method returns a boolean.</span></span> <span data-ttu-id="75311-155">Engagement отправляет отзыв tooits внутренней после отправки hello Принудительная отправка данных.</span><span class="sxs-lookup"><span data-stu-id="75311-155">Engagement sends a feedback tooits back-end after dispatching hello data push.</span></span> <span data-ttu-id="75311-156">Если hello обратный вызов возвращает значение false, hello `exit` отзыв будет отправлено.</span><span class="sxs-lookup"><span data-stu-id="75311-156">If hello callback returns false, hello `exit` feedback will be send.</span></span> <span data-ttu-id="75311-157">В противном случае отправляется `action`.</span><span class="sxs-lookup"><span data-stu-id="75311-157">Otherwise, it will be `action`.</span></span> <span data-ttu-id="75311-158">Если обратный вызов не имеет значение для событий hello, hello `drop` отзыв будет возвращаться tooEngagement.</span><span class="sxs-lookup"><span data-stu-id="75311-158">If no callback is set for hello events, hello `drop` feedback will be returned tooEngagement.</span></span>

> [!WARNING]
> <span data-ttu-id="75311-159">Engagement не может tooreceive кратные отзывы для принудительной отправки данных.</span><span class="sxs-lookup"><span data-stu-id="75311-159">Engagement is not able tooreceive multiples feedbacks for a data push.</span></span> <span data-ttu-id="75311-160">Если вы планируете tooset несколько обработчиков событий, имейте в виду, что hello отзыв будет соответствовать toohello отправлено последним.</span><span class="sxs-lookup"><span data-stu-id="75311-160">If you plan tooset several handlers on an event, be aware that hello feedback will correspond toohello last one sent.</span></span> <span data-ttu-id="75311-161">В этом случае рекомендуется tooalways возвращает hello же tooavoid значение с путаницу отзывы на hello переднего плана.</span><span class="sxs-lookup"><span data-stu-id="75311-161">In this case, we recommend tooalways returns hello same value tooavoid having confusing feedback on hello front-end.</span></span>
> 
> 

## <a name="customize-ui-optional"></a><span data-ttu-id="75311-162">Настройка пользовательского интерфейса (необязательно)</span><span class="sxs-lookup"><span data-stu-id="75311-162">Customize UI (optional)</span></span>
### <a name="first-step"></a><span data-ttu-id="75311-163">Первый шаг</span><span class="sxs-lookup"><span data-stu-id="75311-163">First step</span></span>
<span data-ttu-id="75311-164">Мы даем reach hello toocustomize пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="75311-164">We allow you toocustomize hello reach UI.</span></span>

<span data-ttu-id="75311-165">toodo таким образом, у вас есть toocreate подкласс hello `EngagementReachHandler` класса.</span><span class="sxs-lookup"><span data-stu-id="75311-165">toodo so, you have toocreate a subclass of hello `EngagementReachHandler` class.</span></span>

<span data-ttu-id="75311-166">**Пример кода:**</span><span class="sxs-lookup"><span data-stu-id="75311-166">**Sample Code :**</span></span>

    using Microsoft.Azure.Engagement;

    namespace Example
    {
       internal class ExampleReachHandler : EngagementReachHandler
       {
          // Override EngagementReachHandler methods depending on your needs
       }
    }

<span data-ttu-id="75311-167">Задайте содержимое hello hello `EngagementReach.Instance.Handler` пользовательского объекта в поле вашего `App.xaml.cs` класс внутри hello `Application_Launching` метод.</span><span class="sxs-lookup"><span data-stu-id="75311-167">Then, set hello content of hello `EngagementReach.Instance.Handler` field with your custom object in your `App.xaml.cs` class within hello `Application_Launching` method.</span></span>

<span data-ttu-id="75311-168">**Пример кода:**</span><span class="sxs-lookup"><span data-stu-id="75311-168">**Sample Code :**</span></span>

    private void Application_Launching(object sender, LaunchingEventArgs e)
    {
       // your app initialization 
       EngagementReach.Instance.Handler = new ExampleReachHandler();
       // Engagement Agent and Reach initialization
    }

> [!NOTE]
> <span data-ttu-id="75311-169">По умолчанию Engagement использует собственную реализацию `EngagementReachHandler`.</span><span class="sxs-lookup"><span data-stu-id="75311-169">By default, Engagement uses its own implementation of `EngagementReachHandler`.</span></span> <span data-ttu-id="75311-170">Нет toocreate собственный, и при этом, у вас нет toooverride каждого метода.</span><span class="sxs-lookup"><span data-stu-id="75311-170">You don't have toocreate your own, and if you do so, you don't have toooverride every method.</span></span> <span data-ttu-id="75311-171">поведение по умолчанию Hello — tooselect hello Engagement базовый объект.</span><span class="sxs-lookup"><span data-stu-id="75311-171">hello default behavior is tooselect hello Engagement base object.</span></span>
> 
> 

### <a name="layouts"></a><span data-ttu-id="75311-172">Макеты</span><span class="sxs-lookup"><span data-stu-id="75311-172">Layouts</span></span>
<span data-ttu-id="75311-173">По умолчанию Reach будет использовать hello внедренные ресурсы hello DLL toodisplay hello уведомлений и страниц.</span><span class="sxs-lookup"><span data-stu-id="75311-173">By default, Reach will use hello embedded resources of hello DLL toodisplay hello notifications and pages.</span></span>

<span data-ttu-id="75311-174">Тем не менее, вы можете toouse собственные ресурсы tooreflect фирменного стиля в этих компонентах.</span><span class="sxs-lookup"><span data-stu-id="75311-174">However, you can decide toouse your own resources tooreflect your brand in these components.</span></span>

<span data-ttu-id="75311-175">Можно переопределить `EngagementReachHandler` методы в ваш подкласс tootell Engagement toouse макеты:</span><span class="sxs-lookup"><span data-stu-id="75311-175">You can override `EngagementReachHandler` methods in your subclass tootell Engagement toouse your layouts :</span></span>

<span data-ttu-id="75311-176">**Пример кода:**</span><span class="sxs-lookup"><span data-stu-id="75311-176">**Sample Code :**</span></span>

    // In your subclass of EngagementReachHandler

    public override string GetTextViewAnnouncementUri()
    {
       // return hello path of your own xaml
    }

    public override string GetWebViewAnnouncementUri()
    {
       // return hello path of your own xaml
    }

    public override string GetPollUri()
    {
       // return hello path of your own xaml
    }

    public override EngagementNotificationView CreateNotification(EngagementNotificationViewModel viewModel)
    {
       // return a new instance of your own notification
    }

> [!TIP]
> <span data-ttu-id="75311-177">Hello `CreateNotification` метод может возвращать значение null.</span><span class="sxs-lookup"><span data-stu-id="75311-177">hello `CreateNotification` method can return null.</span></span> <span data-ttu-id="75311-178">Hello уведомления не будут отображаться и кампании reach hello, будут удалены.</span><span class="sxs-lookup"><span data-stu-id="75311-178">hello notification won't be displayed and hello reach campaign will be dropped.</span></span>
> 
> 

<span data-ttu-id="75311-179">toosimplify реализация макета, мы также предоставляем нашим собственным xaml, который можно использовать в качестве основы для кода.</span><span class="sxs-lookup"><span data-stu-id="75311-179">toosimplify your layout implementation, we also provide our own xaml which can serve as a basis for your code.</span></span> <span data-ttu-id="75311-180">Они находятся в архиве Engagement SDK hello (/ src/reach /).</span><span class="sxs-lookup"><span data-stu-id="75311-180">They are located in hello Engagement SDK archive (/src/reach/).</span></span>

> [!WARNING]
> <span data-ttu-id="75311-181">Hello источники, которые мы предоставляем hello точное используются те же, которые мы используем.</span><span class="sxs-lookup"><span data-stu-id="75311-181">hello sources that we provide are hello exact same ones that we use.</span></span> <span data-ttu-id="75311-182">Поэтому при необходимости toomodify их напрямую, не забыть toochange приветствия имен и hello имя.</span><span class="sxs-lookup"><span data-stu-id="75311-182">So if you want toomodify them directly, don't forget toochange hello namespace and hello name.</span></span>
> 
> 

### <a name="notification-position"></a><span data-ttu-id="75311-183">Расположение уведомлений</span><span class="sxs-lookup"><span data-stu-id="75311-183">Notification position</span></span>
<span data-ttu-id="75311-184">По умолчанию уведомление в приложении отображается в нижней левой hello приложения hello.</span><span class="sxs-lookup"><span data-stu-id="75311-184">By default, an in-app notification is displayed at hello bottom left side of hello application.</span></span> <span data-ttu-id="75311-185">Это поведение можно изменить путем переопределения hello `GetNotificationPosition` метод hello `EngagementReachHandler` объекта.</span><span class="sxs-lookup"><span data-stu-id="75311-185">You can change this behavior by overriding hello `GetNotificationPosition` method of hello `EngagementReachHandler` object.</span></span>

    // In your subclass of EngagementReachHandler

    public override EngagementReachHandler.NotificationPosition GetNotificationPosition(EngagementNotificationViewModel viewModel)
    {
       // return a value of hello EngagementReachHandler.NotificationPosition enum (TOP or BOTTOM)
    }

<span data-ttu-id="75311-186">В настоящее время можно выбрать между hello `BOTTOM` (по умолчанию) и `TOP` позиций.</span><span class="sxs-lookup"><span data-stu-id="75311-186">Currently, you can choose between hello `BOTTOM` (default) and `TOP` positions.</span></span>

### <a name="launch-message"></a><span data-ttu-id="75311-187">Запуск сообщения</span><span class="sxs-lookup"><span data-stu-id="75311-187">Launch message</span></span>
<span data-ttu-id="75311-188">При щелчке Системное уведомление (всплывающее уведомление) запускает Engagement hello приложения, содержимое hello нагрузки hello отправляют сообщения и отображения страницы приветствия для hello соответствующий кампании.</span><span class="sxs-lookup"><span data-stu-id="75311-188">When a user clicks on a system notification (a toast), Engagement launches hello app, load hello content of hello push messages, and display hello page for hello corresponding campaign.</span></span>

<span data-ttu-id="75311-189">Возникает задержка между запуска hello hello приложения и hello отображения страницы приветствия (в зависимости от скорости сети hello).</span><span class="sxs-lookup"><span data-stu-id="75311-189">There is a delay between hello launch of hello application and hello display of hello page (depending on hello speed of your network).</span></span>

<span data-ttu-id="75311-190">пользователь toohello tooindicate, что-то загружается, необходимо предоставить visual сведения, например, индикатор выполнения или индикатор хода выполнения.</span><span class="sxs-lookup"><span data-stu-id="75311-190">tooindicate toohello user that something is loading, you should provide a visual information, like a progress bar or a progress indicator.</span></span> <span data-ttu-id="75311-191">Engagement не может обработать ее самостоятельно, но предоставляет несколько обработчиков, которыми вы можете воспользоваться.</span><span class="sxs-lookup"><span data-stu-id="75311-191">Engagement cannot handle that itself, but provides a few handlers for you.</span></span>

<span data-ttu-id="75311-192">tooimplement hello обратного вызова, выполните действия.</span><span class="sxs-lookup"><span data-stu-id="75311-192">tooimplement hello callback, do:</span></span>

    /* hello application has launched and hello content is loading.
     * You should display an indicator here.
     */
    EngagementReach.Instance.RetrieveLaunchMessageStarted += () => { [...] };

    /* hello application has finished loading hello content and hello page
     * is about toobe displayed.
     * You should hide hello indicator here.
     */
    EngagementReach.Instance.RetrieveLaunchMessageCompleted += () => { [...] };

    /* hello content has been loaded, but an error has occurred.
     * You can provide an information toohello user.
     * You should hide hello indicator here.
     */
    EngagementReach.Instance.RetrieveLaunchMessageFailed += () => { [...] };

<span data-ttu-id="75311-193">Hello обратного вызова можно задать в вашей `Application_Launching` метод вашей `App.xaml.cs` файла предпочтительно перед hello `EngagementReach.Instance.Init()` вызова.</span><span class="sxs-lookup"><span data-stu-id="75311-193">You can set hello callback in your `Application_Launching` method of your `App.xaml.cs` file, preferably before hello `EngagementReach.Instance.Init()` call.</span></span>

> [!TIP]
> <span data-ttu-id="75311-194">Каждый обработчик вызывается hello потока пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="75311-194">Each handler is called by hello UI Thread.</span></span> <span data-ttu-id="75311-195">У вас tooworry при использовании MessageBox или что-нибудь связанные с Пользовательским интерфейсом.</span><span class="sxs-lookup"><span data-stu-id="75311-195">You do not have tooworry when using a MessageBox or something UI-related.</span></span>
> 
> 

[политики применения]:http://msdn.microsoft.com/library/windows/apps/hh184841(v=vs.105).aspx
[Content Policies]:http://msdn.microsoft.com/library/windows/apps/hh184842(v=vs.105).aspx
[Дополнительные требования для конкретного приложения типов]:http://msdn.microsoft.com/library/windows/apps/hh184838(v=vs.105).aspx

