---
title: "aaaWindows универсальных приложений достичь интеграции пакета SDK"
description: "Как tooIntegrate Azure Mobile Engagement связаться с помощью универсальных приложений Windows"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a31ca1d6-856f-4aec-898a-07969ae5f7ec
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: af311c65940014083333853875a00173b8d6783e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-reach-sdk-integration"></a><span data-ttu-id="25641-103">Интеграция пакета SDK Reach для универсальных приложений для Windows</span><span class="sxs-lookup"><span data-stu-id="25641-103">Windows Universal Apps Reach SDK Integration</span></span>
<span data-ttu-id="25641-104">Необходимо выполнить процедуры интеграции hello, описанной в hello [интеграции пакета SDK Windows универсальной Engagement](mobile-engagement-windows-store-integrate-engagement.md) до следующего руководства.</span><span class="sxs-lookup"><span data-stu-id="25641-104">You must follow hello integration procedure described in hello [Windows Universal Engagement SDK Integration](mobile-engagement-windows-store-integrate-engagement.md) before following this guide.</span></span>

## <a name="embed-hello-engagement-reach-sdk-into-your-windows-universal-project"></a><span data-ttu-id="25641-105">Внедрение hello Engagement Reach SDK в проект Windows Universal.</span><span class="sxs-lookup"><span data-stu-id="25641-105">Embed hello Engagement Reach SDK into your Windows Universal project</span></span>
<span data-ttu-id="25641-106">У вас ничего tooadd.</span><span class="sxs-lookup"><span data-stu-id="25641-106">You do not have anything tooadd.</span></span> <span data-ttu-id="25641-107">`EngagementReach` уже включены в проект.</span><span class="sxs-lookup"><span data-stu-id="25641-107">`EngagementReach` references and resources are already in your project.</span></span>

> [!TIP]
> <span data-ttu-id="25641-108">Образы, расположенный в hello можно настраивать `Resources` папки проекта, особенно hello фирменной символики значок (что по умолчанию toohello Engagement).</span><span class="sxs-lookup"><span data-stu-id="25641-108">You can customize images located in hello `Resources` folder of your project, especially hello brand icon (that default toohello Engagement icon).</span></span> <span data-ttu-id="25641-109">Для универсальных приложений также можно перемещать hello `Resources` папку на ваш tooshare общего проекта, его содержимое между приложениями, но будет иметь tookeep hello `Resources\EngagementConfiguration.xml` файлов на расположение по умолчанию, поскольку это зависит от используемой платформы.</span><span class="sxs-lookup"><span data-stu-id="25641-109">On Universal Apps you can also move hello `Resources` folder on your shared project tooshare its content between apps, but you will have tookeep hello `Resources\EngagementConfiguration.xml` file on its default location as it is platform dependent.</span></span>
> 
> 

## <a name="enable-hello-windows-notification-service"></a><span data-ttu-id="25641-110">Включить службу уведомлений Windows hello</span><span class="sxs-lookup"><span data-stu-id="25641-110">Enable hello Windows Notification Service</span></span>
### <a name="windows-8x-and-windows-phone-81-only"></a><span data-ttu-id="25641-111">Только для Windows 8.x и Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="25641-111">Windows 8.x and Windows Phone 8.1 only</span></span>
<span data-ttu-id="25641-112">В порядке hello toouse **службы уведомлений Windows** (называемый WNS) в вашей `Package.appxmanifest` файлов на `Application UI` щелкните `All Image Assets` в поле слева роботов hello.</span><span class="sxs-lookup"><span data-stu-id="25641-112">In order toouse hello **Windows Notification Service** (referred as WNS) in your `Package.appxmanifest` file on `Application UI` click on `All Image Assets` in hello left bot box.</span></span> <span data-ttu-id="25641-113">В hello справа от поля hello в `Notifications`, изменить `toast capable` из `(not set)` слишком`(Yes)`.</span><span class="sxs-lookup"><span data-stu-id="25641-113">At hello right of hello box in `Notifications`, change `toast capable` from `(not set)` too`(Yes)`.</span></span>

### <a name="all-platforms"></a><span data-ttu-id="25641-114">Все платформы</span><span class="sxs-lookup"><span data-stu-id="25641-114">All platforms</span></span>
<span data-ttu-id="25641-115">Необходимо toosynchronize вашего приложения tooyour Microsoft учетной записи и toohello платформа для взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="25641-115">You need toosynchronize your app tooyour Microsoft account and toohello engagement platform.</span></span> <span data-ttu-id="25641-116">Для этого требуется toocreate учетную запись или войдите в систему [центра разработчиков windows](https://dev.windows.com).</span><span class="sxs-lookup"><span data-stu-id="25641-116">For this you need toocreate an account or log on [windows dev center](https://dev.windows.com).</span></span> <span data-ttu-id="25641-117">После того, создайте новое приложение и найти hello SID и секретный ключ.</span><span class="sxs-lookup"><span data-stu-id="25641-117">After that create a new application and find hello SID and secret key.</span></span> <span data-ttu-id="25641-118">На сервере переднего плана engagement hello, перейдите на параметры приложения в `native push` и вставьте свои учетные данные.</span><span class="sxs-lookup"><span data-stu-id="25641-118">On hello engagement frontend, go on your app setting in `native push` and paste your credentials.</span></span> <span data-ttu-id="25641-119">После этого щелкните правой кнопкой мыши проект и выберите `store` и `Associate App with hello Store...`.</span><span class="sxs-lookup"><span data-stu-id="25641-119">After that, right click on your project, select `store` and `Associate App with hello Store...`.</span></span> <span data-ttu-id="25641-120">Необходимо просто приложения hello tooselect имеют перед toosynchronize ее создании.</span><span class="sxs-lookup"><span data-stu-id="25641-120">You just need tooselect hello application you have create before toosynchronize it.</span></span>

## <a name="initialize-hello-engagement-reach-sdk"></a><span data-ttu-id="25641-121">Инициализировать hello Engagement Reach SDK</span><span class="sxs-lookup"><span data-stu-id="25641-121">Initialize hello Engagement Reach SDK</span></span>
<span data-ttu-id="25641-122">Изменение hello `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="25641-122">Modify hello `App.xaml.cs`:</span></span>

* <span data-ttu-id="25641-123">Вставьте `EngagementReach.Instance.Init` сразу после `EngagementAgent.Instance.Init` в методе `InitEngagement`:</span><span class="sxs-lookup"><span data-stu-id="25641-123">Insert `EngagementReach.Instance.Init` just after `EngagementAgent.Instance.Init` in your `InitEngagement` method:</span></span>
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
        EngagementReach.Instance.Init(e);
      }
  
  <span data-ttu-id="25641-124">Hello `EngagementReach.Instance.Init` выполняется в выделенном потоке.</span><span class="sxs-lookup"><span data-stu-id="25641-124">hello `EngagementReach.Instance.Init` runs in a dedicated thread.</span></span> <span data-ttu-id="25641-125">У вас toodo его самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="25641-125">You do not have toodo it yourself.</span></span>

> [!NOTE]
> <span data-ttu-id="25641-126">Если вы используете push-уведомлений в другом месте в приложении, то у вас слишком[совместно используют канал принудительной](#push-channel-sharing) с Engagement Reach.</span><span class="sxs-lookup"><span data-stu-id="25641-126">If you are using push notifications elsewhere in your application then you have too[share your push channel](#push-channel-sharing) with Engagement Reach.</span></span>
> 
> 

## <a name="integration"></a><span data-ttu-id="25641-127">Интеграция</span><span class="sxs-lookup"><span data-stu-id="25641-127">Integration</span></span>
<span data-ttu-id="25641-128">Engagement предоставляет два способа tooadd hello Reach в приложении ленты и interstitial представления для объявлений и для опросов в приложении: hello наложения интеграции и вручную интеграции hello web представления.</span><span class="sxs-lookup"><span data-stu-id="25641-128">Engagement provides two ways tooadd hello Reach in-app banners and interstitial views for announcements and polls in your application: hello overlay integration and hello web views manual integration.</span></span> <span data-ttu-id="25641-129">Не следует сочетать оба подхода hello одной страницы.</span><span class="sxs-lookup"><span data-stu-id="25641-129">You should not combine both approach on hello same page.</span></span>

<span data-ttu-id="25641-130">Таким образом может описать Hello Выбор между двумя интеграции hello.</span><span class="sxs-lookup"><span data-stu-id="25641-130">hello choice between hello two integration could be summarized this way:</span></span>

* <span data-ttu-id="25641-131">Может выбрать интеграции наложения hello, если на страницах уже наследует от hello агента `EngagementPage`, он является лишь замены `EngagementPage` по `EngagementPageOverlay` и `xmlns:engagement="using:Microsoft.Azure.Engagement"` по `xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"` на страницах.</span><span class="sxs-lookup"><span data-stu-id="25641-131">You may choose hello overlay integration if your pages already inherits from hello Agent `EngagementPage`, it's just a matter of replacing `EngagementPage` by `EngagementPageOverlay` and `xmlns:engagement="using:Microsoft.Azure.Engagement"` by `xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"` in your pages.</span></span>
* <span data-ttu-id="25641-132">Вы можете вручную интеграции hello web представления tooprecisely месте hello достичь пользовательского интерфейса внутри страницы или если вы не хотите tooadd другой страницы уровня tooyour наследования.</span><span class="sxs-lookup"><span data-stu-id="25641-132">You may choose hello web views manual integration if you want tooprecisely place hello Reach UI within your pages or if you don't want tooadd another inheritance level tooyour pages.</span></span> 

### <a name="overlay-integration"></a><span data-ttu-id="25641-133">Интеграции наложения</span><span class="sxs-lookup"><span data-stu-id="25641-133">Overlay integration</span></span>
<span data-ttu-id="25641-134">наложение Engagement Hello динамически добавляет элементы пользовательского интерфейса hello используемых кампаниями Reach toodisplay на странице.</span><span class="sxs-lookup"><span data-stu-id="25641-134">hello Engagement overlay dynamically adds hello UI elements used toodisplay Reach campaigns in your page.</span></span> <span data-ttu-id="25641-135">Если макет не подходит для наложения hello следует hello веб-представления вручную интеграции вместо.</span><span class="sxs-lookup"><span data-stu-id="25641-135">If hello overlay doesn't suit your layout you should consider hello web views manual integration instead.</span></span>

<span data-ttu-id="25641-136">В изменения файла .xaml `EngagementPage` слишком ссылки`EngagementPageOverlay`</span><span class="sxs-lookup"><span data-stu-id="25641-136">In your .xaml file change `EngagementPage` reference too`EngagementPageOverlay`</span></span>

* <span data-ttu-id="25641-137">Добавьте tooyour объявления пространств имен:</span><span class="sxs-lookup"><span data-stu-id="25641-137">Add tooyour namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"
* <span data-ttu-id="25641-138">Замените `engagement:EngagementPage` на `engagement:EngagementPageOverlay`:</span><span class="sxs-lookup"><span data-stu-id="25641-138">Replace `engagement:EngagementPage` with `engagement:EngagementPageOverlay`:</span></span>

<span data-ttu-id="25641-139">**EngagementPage:**</span><span class="sxs-lookup"><span data-stu-id="25641-139">**With EngagementPage:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">

            <!-- Your layout -->
        </engagement:EngagementPage>

<span data-ttu-id="25641-140">**EngagementPageOverlay:**</span><span class="sxs-lookup"><span data-stu-id="25641-140">**With EngagementPageOverlay:**</span></span>

        <engagement:EngagementPageOverlay 
            xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay">

            <!-- Your layout -->
        </engagement:EngagementPageOverlay>

<span data-ttu-id="25641-141">Затем в CS-файле пометьте страницу тегом `EngagementPageOverlay`, а не `EngagementPage`, и импортируйте `Microsoft.Azure.Engagement.Overlay`.</span><span class="sxs-lookup"><span data-stu-id="25641-141">Then in your .cs file tag your page in `EngagementPageOverlay` instead of `EngagementPage` and import `Microsoft.Azure.Engagement.Overlay`.</span></span>

            using Microsoft.Azure.Engagement.Overlay;

* <span data-ttu-id="25641-142">Замените `EngagementPage` на `EngagementPageOverlay`:</span><span class="sxs-lookup"><span data-stu-id="25641-142">Replace `EngagementPage` with `EngagementPageOverlay`:</span></span>

<span data-ttu-id="25641-143">**EngagementPage:**</span><span class="sxs-lookup"><span data-stu-id="25641-143">**With EngagementPage:**</span></span>

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPage
              {
                [...]
              }
            }

<span data-ttu-id="25641-144">**EngagementPageOverlay:**</span><span class="sxs-lookup"><span data-stu-id="25641-144">**With EngagementPageOverlay:**</span></span>

            using Microsoft.Azure.Engagement.Overlay;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPageOverlay 
              {
                [...]
              }
            }


<span data-ttu-id="25641-145">Hello наложения Engagement добавляет `Grid` элемент поверх страницы состоит из макета и hello двух `WebView` элементы один для hello banner и другую переменную, чтобы представление interstitial hello hello.</span><span class="sxs-lookup"><span data-stu-id="25641-145">hello Engagement overlay adds a `Grid` element on top of your page composed of your layout and hello two `WebView` elements one for hello banner and hello other one for hello interstitial view.</span></span>

<span data-ttu-id="25641-146">Можно настраивать элементы наложения hello непосредственно в hello `EngagementPageOverlay.cs` файла.</span><span class="sxs-lookup"><span data-stu-id="25641-146">You can customize hello overlay elements directly in hello `EngagementPageOverlay.cs` file.</span></span>

### <a name="web-views-manual-integration"></a><span data-ttu-id="25641-147">Интеграция веб-представлений вручную</span><span class="sxs-lookup"><span data-stu-id="25641-147">Web views manual integration</span></span>
<span data-ttu-id="25641-148">Reach будет искать на страницах hello двух `WebView` отвечает за отображение баннера hello и hello interstitial представление элементов.</span><span class="sxs-lookup"><span data-stu-id="25641-148">Reach will be searching your pages for hello two `WebView` elements responsible for displaying hello banner and hello interstitial view.</span></span> <span data-ttu-id="25641-149">Здравствуйте, только что toodo tooadd этих двух `WebView` элементы где-нибудь на страницах, ниже приведен пример:</span><span class="sxs-lookup"><span data-stu-id="25641-149">hello only thing you have toodo is tooadd those two `WebView` elements somewhere in your pages, here is an example:</span></span>

    <Grid x:Name="engagementGrid">

      <!-- Your layout -->

      <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Stretch" VerticalAlignment="Top"/>
      <WebView x:Name="engagement_announcement_content" Visibility="Collapsed"  HorizontalAlignment="Stretch"  VerticalAlignment="Stretch"/>
    </Grid>


<span data-ttu-id="25641-150">В этом примере hello `WebView` элементы являются растяжением toofit их контейнер, который автоматически размеров их повторно в случае изменения размера экрана поворот или окна.</span><span class="sxs-lookup"><span data-stu-id="25641-150">In this example hello `WebView` elements are stretched toofit their container which automatically re-sizes them in case of screen rotation or window size change.</span></span>

> [!WARNING]
> <span data-ttu-id="25641-151">Очень важно tookeep hello же именования `engagement_notification_content` и `engagement_announcement_content` для hello `WebView` элементов.</span><span class="sxs-lookup"><span data-stu-id="25641-151">It is important tookeep hello same naming `engagement_notification_content` and `engagement_announcement_content` for hello `WebView` elements.</span></span> <span data-ttu-id="25641-152">Reach определяет элементы по имени.</span><span class="sxs-lookup"><span data-stu-id="25641-152">Reach is identifying them by their name.</span></span> 
> 
> 

## <a name="handle-datapush-optional"></a><span data-ttu-id="25641-153">Обработка отправленных данных (необязательно)</span><span class="sxs-lookup"><span data-stu-id="25641-153">Handle datapush (optional)</span></span>
<span data-ttu-id="25641-154">Если требуется вашего приложения toobe может tooreceive Reach данных Push-уведомлений, имеется tooimplement двумя событиями hello EngagementReach класса:</span><span class="sxs-lookup"><span data-stu-id="25641-154">If you want your application toobe able tooreceive Reach data pushes, you have tooimplement two events of hello EngagementReach class:</span></span>

<span data-ttu-id="25641-155">Добавьте в App.xaml.cs в конструкторе App() hello.</span><span class="sxs-lookup"><span data-stu-id="25641-155">In App.xaml.cs in hello App() constructor add:</span></span>

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

<span data-ttu-id="25641-156">Вы увидите ответного вызова hello каждый метод возвращает логическое значение.</span><span class="sxs-lookup"><span data-stu-id="25641-156">You can see that hello callback of each method returns a boolean.</span></span> <span data-ttu-id="25641-157">Engagement отправляет отзыв tooits внутренней после отправки hello Принудительная отправка данных.</span><span class="sxs-lookup"><span data-stu-id="25641-157">Engagement sends a feedback tooits back-end after dispatching hello data push.</span></span> <span data-ttu-id="25641-158">Если hello обратный вызов возвращает значение false, hello `exit` отзыв будет отправлено.</span><span class="sxs-lookup"><span data-stu-id="25641-158">If hello callback returns false, hello `exit` feedback will be send.</span></span> <span data-ttu-id="25641-159">В противном случае отправляется `action`.</span><span class="sxs-lookup"><span data-stu-id="25641-159">Otherwise, it will be `action`.</span></span> <span data-ttu-id="25641-160">Если обратный вызов не имеет значение для событий hello, hello `drop` отзыв будет возвращаться tooEngagement.</span><span class="sxs-lookup"><span data-stu-id="25641-160">If no callback is set for hello events, hello `drop` feedback will be returned tooEngagement.</span></span>

> [!WARNING]
> <span data-ttu-id="25641-161">Engagement не может tooreceive кратные отзывы для принудительной отправки данных.</span><span class="sxs-lookup"><span data-stu-id="25641-161">Engagement is not able tooreceive multiples feedbacks for a data push.</span></span> <span data-ttu-id="25641-162">Если вы планируете tooset несколько обработчиков событий, имейте в виду, что hello отзыв будет соответствовать toohello отправлено последним.</span><span class="sxs-lookup"><span data-stu-id="25641-162">If you plan tooset several handlers on an event, be aware that hello feedback will correspond toohello last one sent.</span></span> <span data-ttu-id="25641-163">В этом случае рекомендуется tooalways возвращает hello же tooavoid значение с путаницу отзывы на hello переднего плана.</span><span class="sxs-lookup"><span data-stu-id="25641-163">In this case, we recommend tooalways returns hello same value tooavoid having confusing feedback on hello front-end.</span></span>
> 
> 

## <a name="customize-ui-optional"></a><span data-ttu-id="25641-164">Настройка пользовательского интерфейса (необязательно)</span><span class="sxs-lookup"><span data-stu-id="25641-164">Customize UI (optional)</span></span>
### <a name="first-step"></a><span data-ttu-id="25641-165">Первый шаг</span><span class="sxs-lookup"><span data-stu-id="25641-165">First step</span></span>
<span data-ttu-id="25641-166">Мы даем reach hello toocustomize пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="25641-166">We allow you toocustomize hello reach UI.</span></span>

<span data-ttu-id="25641-167">toodo таким образом, у вас есть toocreate подкласс hello `EngagementReachHandler` класса.</span><span class="sxs-lookup"><span data-stu-id="25641-167">toodo so, you have toocreate a subclass of hello `EngagementReachHandler` class.</span></span>

<span data-ttu-id="25641-168">**Пример кода:**</span><span class="sxs-lookup"><span data-stu-id="25641-168">**Sample Code :**</span></span>

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              internal class ExampleReachHandler : EngagementReachHandler
              {
               // Override EngagementReachHandler methods depending on your needs
              }
            }

<span data-ttu-id="25641-169">Задайте содержимое hello hello `EngagementReach.Instance.Handler` пользовательского объекта в поле вашего `App.xaml.cs` класс внутри hello `App()` метод.</span><span class="sxs-lookup"><span data-stu-id="25641-169">Then, set hello content of hello `EngagementReach.Instance.Handler` field with your custom object in your `App.xaml.cs` class within hello `App()` method.</span></span>

<span data-ttu-id="25641-170">**Пример кода:**</span><span class="sxs-lookup"><span data-stu-id="25641-170">**Sample Code :**</span></span>

            protected override void OnLaunched(LaunchActivatedEventArgs args)
            {
              // your app initialization 
              EngagementReach.Instance.Handler = new ExampleReachHandler();
              // Engagement Agent and Reach initialization
            }

> [!NOTE]
> <span data-ttu-id="25641-171">По умолчанию Engagement использует собственную реализацию `EngagementReachHandler`.</span><span class="sxs-lookup"><span data-stu-id="25641-171">By default, Engagement uses its own implementation of `EngagementReachHandler`.</span></span>
> <span data-ttu-id="25641-172">Нет toocreate собственный, и при этом, у вас нет toooverride каждого метода.</span><span class="sxs-lookup"><span data-stu-id="25641-172">You don't have toocreate your own, and if you do so, you don't have toooverride every method.</span></span> <span data-ttu-id="25641-173">поведение по умолчанию Hello — tooselect hello Engagement базовый объект.</span><span class="sxs-lookup"><span data-stu-id="25641-173">hello default behavior is tooselect hello Engagement base object.</span></span>
> 
> 

### <a name="web-view"></a><span data-ttu-id="25641-174">Веб-представление</span><span class="sxs-lookup"><span data-stu-id="25641-174">Web View</span></span>
<span data-ttu-id="25641-175">По умолчанию Reach будет использовать hello внедренные ресурсы hello DLL toodisplay hello уведомлений и страниц.</span><span class="sxs-lookup"><span data-stu-id="25641-175">By default, Reach will use hello embedded resources of hello DLL toodisplay hello notifications and pages.</span></span>

<span data-ttu-id="25641-176">tooprovide полной возможности настройки, воспользуемся веб-представление.</span><span class="sxs-lookup"><span data-stu-id="25641-176">tooprovide a full customization possibilities we only use web view.</span></span> <span data-ttu-id="25641-177">Если toocustomize макеты, переопределите непосредственно файлы ресурсов hello `EngagementAnnouncement.html` и `EngagementNotification.html`.</span><span class="sxs-lookup"><span data-stu-id="25641-177">If you want toocustomize layouts, override directly hello resources files `EngagementAnnouncement.html` and `EngagementNotification.html`.</span></span> <span data-ttu-id="25641-178">Engagement должен весь код в `<body></body>` toorun правильно.</span><span class="sxs-lookup"><span data-stu-id="25641-178">Engagement needs all code in `<body></body>` toorun correctly.</span></span> <span data-ttu-id="25641-179">Однако можно добавить тег снаружи `engagement_webview_area`.</span><span class="sxs-lookup"><span data-stu-id="25641-179">But you can add tag outer `engagement_webview_area`.</span></span>

<span data-ttu-id="25641-180">Однако можно решить toouse собственные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="25641-180">However, you can decide toouse your own resources.</span></span>

<span data-ttu-id="25641-181">Можно переопределить `EngagementReachHandler` методы в ваш подкласс tootell Engagement toouse макеты, но принимают механизм engagement hello tooembedded осторожность:</span><span class="sxs-lookup"><span data-stu-id="25641-181">You can override `EngagementReachHandler` methods in your subclass tootell Engagement toouse your layouts, but take care tooembedded hello engagement mechanism:</span></span>

<span data-ttu-id="25641-182">**Пример кода:**</span><span class="sxs-lookup"><span data-stu-id="25641-182">**Sample Code :**</span></span>

            // In your subclass of EngagementReachHandler

            public override string GetAnnouncementHTML()
            {
              return base.GetAnnouncementHTML();
            }
            public override string GetAnnouncementName()
            {
              return base.GetAnnouncementName();
            }
            public override string GetNotfificationHTML()
            {
              return base.GetNotfificationHTML();
            }
            public override string GetNotfificationName()
            {
              return base.GetNotfificationName();
            }


<span data-ttu-id="25641-183">По умолчанию AnnouncementHTML — это `ms-appx-web:///Resources/EngagementAnnouncement.html`.</span><span class="sxs-lookup"><span data-stu-id="25641-183">By default, AnnouncementHTML is `ms-appx-web:///Resources/EngagementAnnouncement.html`.</span></span> <span data-ttu-id="25641-184">Он представляет hello HTML-файл, разрабатывать hello содержимое сообщения push (текст объявления, Web anoucement и объявления опроса).</span><span class="sxs-lookup"><span data-stu-id="25641-184">It represents hello html file that design hello content of a push message (Text announcement, Web anoucement and Poll announcement).</span></span> <span data-ttu-id="25641-185">AnnouncementName — `engagement_announcement_content`.</span><span class="sxs-lookup"><span data-stu-id="25641-185">AnnouncementName is `engagement_announcement_content`.</span></span> <span data-ttu-id="25641-186">Это имя hello hello проектирования webview в xaml-страницы.</span><span class="sxs-lookup"><span data-stu-id="25641-186">It is hello name of hello webview design in your xaml page.</span></span>

<span data-ttu-id="25641-187">NotfificationHTML — `ms-appx-web:///Resources/EngagementNotification.html`.</span><span class="sxs-lookup"><span data-stu-id="25641-187">NotfificationHTML is `ms-appx-web:///Resources/EngagementNotification.html`.</span></span> <span data-ttu-id="25641-188">Он представляет hello HTML-файл, создать уведомление о push-сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="25641-188">It represents hello html file that design hello notification of a push message.</span></span> <span data-ttu-id="25641-189">NotfificationName — `engagement_notification_content`.</span><span class="sxs-lookup"><span data-stu-id="25641-189">NotfificationName is `engagement_notification_content`.</span></span> <span data-ttu-id="25641-190">Это имя hello hello проектирования webview в xaml-страницы.</span><span class="sxs-lookup"><span data-stu-id="25641-190">It is hello name of hello webview design in your xaml page.</span></span>

### <a name="customization"></a><span data-ttu-id="25641-191">Настройка</span><span class="sxs-lookup"><span data-stu-id="25641-191">Customization</span></span>
<span data-ttu-id="25641-192">Вы можете настроить необходимое веб-представление уведомлений и объявлений, если сохраните объект Engagement.</span><span class="sxs-lookup"><span data-stu-id="25641-192">You can customize notification and announcement web view has you want if you preserve Engagement object.</span></span> <span data-ttu-id="25641-193">Будьте внимательны, веб-представление объекта описан три раза — hello первый раз в xaml, второй раз в CS-файл в методе «setwebview()» hello и третий раз в HTML-файле hello.</span><span class="sxs-lookup"><span data-stu-id="25641-193">Take care that webview object is described three times - hello first time in your xaml, second time in your .cs file in hello "setwebview()" method, and third time in hello html file.</span></span>

* <span data-ttu-id="25641-194">В коде xaml описывают hello текущего компонента webview графическом макете.</span><span class="sxs-lookup"><span data-stu-id="25641-194">In your xaml you describe hello current graphical layout webview component.</span></span>
* <span data-ttu-id="25641-195">В CS-файл можно определить «setwebview()», в котором заданы hello измерение hello два веб-представление (уведомления, объявления).</span><span class="sxs-lookup"><span data-stu-id="25641-195">In your .cs file you can define "setwebview()" in which you set hello dimension of hello two webview (notification, announcement).</span></span> <span data-ttu-id="25641-196">Он является весьма эффективным, когда меняет размер приложения hello.</span><span class="sxs-lookup"><span data-stu-id="25641-196">It is very effective when hello application is resizing.</span></span>
* <span data-ttu-id="25641-197">В HTML-файле Engagement hello описывают hello webview содержимого, разработки и hello позиций элементов друг с другом.</span><span class="sxs-lookup"><span data-stu-id="25641-197">In hello Engagement html file we describe hello webview content, design and hello elements positions between each other.</span></span>

### <a name="launch-message"></a><span data-ttu-id="25641-198">Запуск сообщения</span><span class="sxs-lookup"><span data-stu-id="25641-198">Launch message</span></span>
<span data-ttu-id="25641-199">Когда пользователь щелкает Системное уведомление (всплывающее уведомление), Engagement запускает приложение hello, содержимое hello нагрузки hello отправляют сообщения и отображения страницы приветствия для соответствующей кампании hello.</span><span class="sxs-lookup"><span data-stu-id="25641-199">When a user clicks on a system notification (a toast), Engagement launches hello application, load hello content of hello push messages, and display hello page for hello corresponding campaign.</span></span>

<span data-ttu-id="25641-200">Возникает задержка между запуска hello hello приложения и hello отображения страницы приветствия (в зависимости от скорости сети hello).</span><span class="sxs-lookup"><span data-stu-id="25641-200">There is a delay between hello launch of hello application and hello display of hello page (depending on hello speed of your network).</span></span>

<span data-ttu-id="25641-201">пользователь toohello tooindicate, что-то загружается, необходимо предоставить visual сведения, например, индикатор выполнения или индикатор хода выполнения.</span><span class="sxs-lookup"><span data-stu-id="25641-201">tooindicate toohello user that something is loading, you should provide a visual information, like a progress bar or a progress indicator.</span></span> <span data-ttu-id="25641-202">Engagement не может обработать ее самостоятельно, но предоставляет несколько обработчиков, которыми вы можете воспользоваться.</span><span class="sxs-lookup"><span data-stu-id="25641-202">Engagement cannot handle that itself, but provides a few handlers for you.</span></span>

<span data-ttu-id="25641-203">Добавление обратного вызова hello tooimplement в App.xaml.cs в «{} открытый App()»:</span><span class="sxs-lookup"><span data-stu-id="25641-203">tooimplement hello callback, in App.xaml.cs in "Public App(){}" add:</span></span>

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

<span data-ttu-id="25641-204">Hello обратного вызова можно задать в методе «Открытый App() {}» из вашей `App.xaml.cs` файла предпочтительно перед hello `EngagementReach.Instance.Init()` вызова.</span><span class="sxs-lookup"><span data-stu-id="25641-204">You can set hello callback in your "Public App(){}" method of your `App.xaml.cs` file, preferably before hello `EngagementReach.Instance.Init()` call.</span></span>

> [!TIP]
> <span data-ttu-id="25641-205">Каждый обработчик вызывается hello потока пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="25641-205">Each handler is called by hello UI Thread.</span></span> <span data-ttu-id="25641-206">У вас tooworry при использовании MessageBox или что-нибудь связанные с Пользовательским интерфейсом.</span><span class="sxs-lookup"><span data-stu-id="25641-206">You do not have tooworry when using a MessageBox or something UI-related.</span></span>
> 
> 

## <span data-ttu-id="25641-207"><a id="push-channel-sharing"></a> Общий доступ к каналу push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="25641-207"><a id="push-channel-sharing"></a> Push channel sharing</span></span>
<span data-ttu-id="25641-208">При использовании push-уведомлений для других целей в приложении есть toouse hello принудительной канала функции hello Engagement SDK общего доступа.</span><span class="sxs-lookup"><span data-stu-id="25641-208">If you are using push notifications for another purpose in your application then you have toouse hello push channel sharing feature of hello Engagement SDK.</span></span> <span data-ttu-id="25641-209">Это tooavoid пропущенных push.</span><span class="sxs-lookup"><span data-stu-id="25641-209">This is tooavoid missed push.</span></span>

* <span data-ttu-id="25641-210">Вы можете предоставить свои собственные push toohello Engagement Reach инициализации канала.</span><span class="sxs-lookup"><span data-stu-id="25641-210">You can provide your own push channel toohello Engagement Reach initialization.</span></span> <span data-ttu-id="25641-211">Hello SDK будет использовать его вместо нового запроса.</span><span class="sxs-lookup"><span data-stu-id="25641-211">hello SDK will use it instead of requesting a new one.</span></span>

<span data-ttu-id="25641-212">Обновить hello Engagement Reach инициализации канала push в hello `InitEngagement` метод hello `App.xaml.cs` файла:</span><span class="sxs-lookup"><span data-stu-id="25641-212">Update hello Engagement Reach initialization with your push channel in hello `InitEngagement` method from hello `App.xaml.cs` file:</span></span>

    /* Your own push channel logic... */
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    /*...Engagement initialization */
    EngagementAgent.Instance.Init(e);
    EngagementReach.Instance.Init(e,pushChannel);

* <span data-ttu-id="25641-213">Кроме того Если необходимо просто tooconsume hello push канала после инициализации Reach hello обратного вызова можно задать на Engagement Reach канала push tooget hello после его создания, пакет SDK для hello.</span><span class="sxs-lookup"><span data-stu-id="25641-213">Alternatively, if you just want tooconsume hello push channel after hello Reach initialization then you can set a callback on Engagement Reach tooget hello push channel once it is created by hello SDK.</span></span>

<span data-ttu-id="25641-214">Задать обратного вызова в любом месте **после** hello Reach инициализации:</span><span class="sxs-lookup"><span data-stu-id="25641-214">Set your callback at any place **after** hello Reach initialization :</span></span>

    /* Set action on hello SDK push channel. */
    EngagementReach.Instance.SetActionOnPushChannel((PushNotificationChannel channel) => 
    {
      /* hello forwarded channel can be null if its creation fails for any reason. */
      if (channel != null)
      {
        /* Your own push channel logic... */
      });
    }

## <a name="custom-scheme-tip"></a><span data-ttu-id="25641-215">Совет по настраиваемой схеме</span><span class="sxs-lookup"><span data-stu-id="25641-215">Custom scheme tip</span></span>
<span data-ttu-id="25641-216">Мы предоставляем возможность использования настраиваемой схемы.</span><span class="sxs-lookup"><span data-stu-id="25641-216">We provide custom scheme use.</span></span> <span data-ttu-id="25641-217">Можно отправить другой тип URI из toobe engagement переднего плана, в приложении обязательств.</span><span class="sxs-lookup"><span data-stu-id="25641-217">You can send different type of URI from engagement frontend toobe used in your engagement application.</span></span> <span data-ttu-id="25641-218">Управление схемой по умолчанию, например `http, ftp, ...`, осуществляет операционная система Windows. Если на устройстве не установлено приложение по умолчанию, появится окно с запросом.</span><span class="sxs-lookup"><span data-stu-id="25641-218">Default scheme like `http, ftp, ...` are manage by Windows, a window will prompt if they are no default application installed on device.</span></span> <span data-ttu-id="25641-219">Также можно создать собственную настраиваемую схему для своего приложения.</span><span class="sxs-lookup"><span data-stu-id="25641-219">You can also create your own custom scheme for your application.</span></span>

<span data-ttu-id="25641-220">простой способ Hello tooset пользовательской схемы в приложении является tooopen вашей `Package.appxmanifest` перейдите в `Declarations` панель.</span><span class="sxs-lookup"><span data-stu-id="25641-220">hello simple way tooset a custom scheme in your application is tooopen your `Package.appxmanifest` go in `Declarations` panel.</span></span> <span data-ttu-id="25641-221">Выберите `Protocol` в прокрутите доступные объявления hello и добавить его.</span><span class="sxs-lookup"><span data-stu-id="25641-221">Select `Protocol` in hello Available Declarations scroll box and add it.</span></span> <span data-ttu-id="25641-222">Изменить hello `Name` имя требуемого поля с вашего нового протокола.</span><span class="sxs-lookup"><span data-stu-id="25641-222">Edit hello `Name` field with your new protocol desired name.</span></span>

<span data-ttu-id="25641-223">Теперь toouse этот протокол изменить ваш `App.xaml.cs` с hello `OnActivated` метод и также не забывайте tooinitialize engagement здесь:</span><span class="sxs-lookup"><span data-stu-id="25641-223">Now toouse this protocol, edit your `App.xaml.cs` with hello `OnActivated` method, and don't forget tooinitialize engagement here also:</span></span>

            /// <summary>
            /// Enter point when app his called by another way than user click
            /// </summary>
            /// <param name="args">Activation args</param>
            protected override void OnActivated(IActivatedEventArgs args)
            {
              /* Init engagement like it was launch by a custom uri scheme */
              EngagementAgent.Instance.Init(args);
              EngagementReach.Instance.Init(args);

              //TODO design action toodo when app is launch

              #region Custom scheme use
              if (args.Kind == ActivationKind.Protocol)
              {
                ProtocolActivatedEventArgs myProtocol = (ProtocolActivatedEventArgs)args;

                if (myProtocol.Uri.Scheme.Equals("protocolName"))
                {
                  string path = myProtocol.Uri.AbsolutePath;
                }
              }
              #endregion

