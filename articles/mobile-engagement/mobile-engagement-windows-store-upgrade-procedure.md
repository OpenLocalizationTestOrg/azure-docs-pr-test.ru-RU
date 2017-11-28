---
title: "aaaWindows универсальной процедуры обновления пакета SDK для приложений"
description: "Процедуры обновления пакета SDK универсальных приложений для Windows для Служб мобильного взаимодействия Azure"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 4c898175-2cd6-43db-b350-bb408332f24d
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 95aba5d55cd65d4190aad35737f872414b5ed443
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-sdk-upgrade-procedures"></a><span data-ttu-id="815e1-103">Процедуры обновления SDK универсальных приложений для Windows </span><span class="sxs-lookup"><span data-stu-id="815e1-103">Windows Universal Apps SDK Upgrade Procedures</span></span>
<span data-ttu-id="815e1-104">Если уже имеется встроенный более старой версии участия в приложение, у вас есть hello tooconsider при обновлении hello SDK следующие точки.</span><span class="sxs-lookup"><span data-stu-id="815e1-104">If you already have integrated an older version of Engagement into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="815e1-105">Вы можете иметь toofollow несколько процедур если пропущены несколько версий пакета SDK для hello.</span><span class="sxs-lookup"><span data-stu-id="815e1-105">You may have toofollow several procedures if you missed several versions of hello SDK.</span></span> <span data-ttu-id="815e1-106">Например, если выполняется миграция из 0.10.1 too0.11.0, у вас есть toofirst выполните hello» из 0.9.0 too0.10.1» процедуры, а затем hello» из 0.10.1 too0.11.0» процедуры.</span><span class="sxs-lookup"><span data-stu-id="815e1-106">For example if you migrate from 0.10.1 too0.11.0 you have toofirst follow hello "from 0.9.0 too0.10.1" procedure then hello "from 0.10.1 too0.11.0" procedure.</span></span>

## <a name="from-330-too340"></a><span data-ttu-id="815e1-107">Из 3.3.0 too3.4.0</span><span class="sxs-lookup"><span data-stu-id="815e1-107">From 3.3.0 too3.4.0</span></span>
### <a name="test-logs"></a><span data-ttu-id="815e1-108">Журналы тестирования</span><span class="sxs-lookup"><span data-stu-id="815e1-108">Test logs</span></span>
<span data-ttu-id="815e1-109">Журналы консоли, созданные hello SDK теперь может быть включен и отключен и фильтруются.</span><span class="sxs-lookup"><span data-stu-id="815e1-109">Console logs produced by hello SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="815e1-110">toocustomize hello, обновить свойство `EngagementAgent.Instance.TestLogEnabled` tooone hello значения, доступные из hello `EngagementTestLogLevel` перечисления, например:</span><span class="sxs-lookup"><span data-stu-id="815e1-110">toocustomize this, update hello property `EngagementAgent.Instance.TestLogEnabled` tooone of hello value available from hello `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

### <a name="resources"></a><span data-ttu-id="815e1-111">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="815e1-111">Resources</span></span>
<span data-ttu-id="815e1-112">Улучшена Hello Reach наложения.</span><span class="sxs-lookup"><span data-stu-id="815e1-112">hello Reach overlay has been improved.</span></span> <span data-ttu-id="815e1-113">Он является частью ресурсы пакета SDK NuGet hello.</span><span class="sxs-lookup"><span data-stu-id="815e1-113">It is part of hello SDK NuGet package resources.</span></span>

<span data-ttu-id="815e1-114">При обновлении toohello новую версию пакета SDK для hello можно выбрать, следует tookeep ли существующие файлы из hello наложения папки ресурсов или нет.</span><span class="sxs-lookup"><span data-stu-id="815e1-114">While upgrading toohello new version of hello SDK you can choose whether you want tookeep your existing files from hello overlay folder of your resources or not:</span></span>

* <span data-ttu-id="815e1-115">Если предыдущих наложения hello работает для вас или интеграции hello `WebView` элементы вручную, можно определить tookeep для существующих файлов, а затем он будет по-прежнему работать.</span><span class="sxs-lookup"><span data-stu-id="815e1-115">If hello previous overlay is working for you or you are integrating hello `WebView` elements manually then you can decide tookeep your exiting files, it will still work.</span></span> 
* <span data-ttu-id="815e1-116">Если требуется новый наложения toohello tooupdate, просто заменить hello всей `overlay` папку из ресурсов с hello новый из пакета SDK для hello (приложений UWP: после обновления hello можно получить hello наложения папку % USERPROFILE %\\. nuget\ packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span><span class="sxs-lookup"><span data-stu-id="815e1-116">If you want tooupdate toohello new overlay, just replace hello whole `overlay` folder from your resources with hello new one from hello SDK package (UWP apps: after hello upgrade, you can get hello new overlay folder from %USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span></span>

> [!WARNING]
> <span data-ttu-id="815e1-117">С помощью нового наложения hello перезапишет все настройки, произведенные в предыдущей версии hello.</span><span class="sxs-lookup"><span data-stu-id="815e1-117">Using hello new overlay will overwrite any customizations made on hello previous version.</span></span>
> 
> 

## <a name="from-320-too330"></a><span data-ttu-id="815e1-118">Из 3.2.0 too3.3.0</span><span class="sxs-lookup"><span data-stu-id="815e1-118">From 3.2.0 too3.3.0</span></span>
### <a name="resources"></a><span data-ttu-id="815e1-119">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="815e1-119">Resources</span></span>
<span data-ttu-id="815e1-120">Этот шаг относится только к настраиваемым ресурсам.</span><span class="sxs-lookup"><span data-stu-id="815e1-120">This step concerns customized resources only.</span></span> <span data-ttu-id="815e1-121">Если вы настроили hello ресурсов, предоставляемых на hello SDK (html, изображения, наложения), то у вас есть toobackup их перед обновлением и reapply настройку на обновления ресурсов.</span><span class="sxs-lookup"><span data-stu-id="815e1-121">If you have customized hello resources provided by hello SDK (html, images, overlay) then you have toobackup them before upgrading and reapply your customization on upgraded resources.</span></span>

## <a name="from-310-too320"></a><span data-ttu-id="815e1-122">Из 3.1.0 too3.2.0</span><span class="sxs-lookup"><span data-stu-id="815e1-122">From 3.1.0 too3.2.0</span></span>
### <a name="resources"></a><span data-ttu-id="815e1-123">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="815e1-123">Resources</span></span>
<span data-ttu-id="815e1-124">Этот шаг относится только к настраиваемым ресурсам.</span><span class="sxs-lookup"><span data-stu-id="815e1-124">This step concerns customized resources only.</span></span> <span data-ttu-id="815e1-125">Если вы настроили hello ресурсов, предоставляемых на hello SDK (html, изображения, наложения), то у вас есть toobackup их перед обновлением и reapply настройку на обновления ресурсов.</span><span class="sxs-lookup"><span data-stu-id="815e1-125">If you have customized hello resources provided by hello SDK (html, images, overlay) then you have toobackup them before upgrading and reapply your customization on upgraded resources.</span></span>

### <a name="webview-integration"></a><span data-ttu-id="815e1-126">Интеграция веб-представления</span><span class="sxs-lookup"><span data-stu-id="815e1-126">Webview integration</span></span>
<span data-ttu-id="815e1-127">В этой версии появились некоторые усовершенствования toomatch другое устройство форм-факторов.</span><span class="sxs-lookup"><span data-stu-id="815e1-127">Some improvements toomatch different device form factors were introduced in this version.</span></span> <span data-ttu-id="815e1-128">Убедитесь, что вашей интеграции hello webview соответствуют hello следующие:</span><span class="sxs-lookup"><span data-stu-id="815e1-128">Make sure that your integration of hello webview match hello following:</span></span>

<span data-ttu-id="815e1-129">На XAML-странице ():</span><span class="sxs-lookup"><span data-stu-id="815e1-129">In your XAML page ():</span></span>

            <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Right" VerticalAlignment="Top"/>
            <WebView x:Name="engagement_announcement_content" Visibility="Collapsed" HorizontalAlignment="Right" VerticalAlignment="Top"/> 

<span data-ttu-id="815e1-130">В соответствующем файле CS:</span><span class="sxs-lookup"><span data-stu-id="815e1-130">And in your associated .cs file:</span></span>

    using Microsoft.Azure.Engagement;
    using System;
    using Windows.ApplicationModel.Core;
    using Windows.UI.ViewManagement;
    using Windows.UI.Xaml;
    using Windows.UI.Xaml.Navigation;

    namespace My.Namespace.Example
    {
            /// <summary>
            /// An empty page that can be used on its own or navigated toowithin a Frame.
            /// </summary>
            public sealed partial class ExampleEngagementReachPage : EngagementPage
            {
              public ExampleEngagementReachPage()
              {
                this.InitializeComponent();

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }

              #region tooimplement
              /* Attach events when page is navigated. */
              protected override void OnNavigatedTo(NavigationEventArgs e)
              {
                /* Update hello webview when hello app window is resized. */
                Window.Current.SizeChanged += DisplayProperties_OrientationChanged;

                /* Update hello webview when hello app/status bar is resized. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged += DisplayProperties_VisibleBoundsChanged; 
    #endif
                base.OnNavigatedTo(e);
              }

              /* When page is left ensure toodetach SizeChanged handler. */
              protected override void OnNavigatedFrom(NavigationEventArgs e)
              {
                Window.Current.SizeChanged -= DisplayProperties_OrientationChanged;
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged -= DisplayProperties_VisibleBoundsChanged;
    #endif
                base.OnNavigatedFrom(e);
              }

              /* "width" and "height" are hello current size of your application display. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
              double width = ApplicationView.GetForCurrentView().VisibleBounds.Width;
              double height = ApplicationView.GetForCurrentView().VisibleBounds.Height;
    #else
              double width =  Window.Current.Bounds.Width;
              double height =  Window.Current.Bounds.Height;
    #endif

              /// <summary>
              /// Set your webview elements toohello correct size.
              /// </summary>
              /// <param name="width">hello width of your current display.</param>
              /// <param name="height">hello height of your current display.</param>
              private void SetWebView(double width, double height)
              {
                #pragma warning disable 4014
                CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(Windows.UI.Core.CoreDispatcherPriority.Normal,
                        () =>
                        {
                          this.engagement_notification_content.Width = width;
                          this.engagement_announcement_content.Width = width;
                          this.engagement_announcement_content.Height = height;
                        });
              }

              /// <summary>
              /// Handler that takes hello Windows.Current.SizeChanged and indicates that webviews have toobe resized.
              /// </summary>
              /// <param name="sender">Original event trigger.</param>
              /// <param name="e">Window Size Changed Event arguments.</param>
              private void DisplayProperties_OrientationChanged(object sender, Windows.UI.Core.WindowSizeChangedEventArgs e)
              {
                double width = e.Size.Width;
                double height = e.Size.Height;

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }

    #if WINDOWS_PHONE_APP || WINDOWS_UWP              
              /// <summary>
              /// Handler that takes hello ApplicationView.VisibleBoundsChanged and indicates that webviews have toobe resized
              /// </summary>
              /// <param name="sender">hello related application view.</param>
              /// <param name="e">Related event arguments.</param>
              private void DisplayProperties_VisibleBoundsChanged(ApplicationView sender, Object e)
              {
                double width = sender.VisibleBounds.Width;
                double height = sender.VisibleBounds.Height;

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }
    #endif
              #endregion
            }
    }

## <a name="from-200-too300"></a><span data-ttu-id="815e1-131">Из 2.0.0 too3.0.0</span><span class="sxs-lookup"><span data-stu-id="815e1-131">From 2.0.0 too3.0.0</span></span>
### <a name="resources"></a><span data-ttu-id="815e1-132">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="815e1-132">Resources</span></span>
<span data-ttu-id="815e1-133">Этот шаг относится только к настраиваемым ресурсам.</span><span class="sxs-lookup"><span data-stu-id="815e1-133">This step concerns customized resources only.</span></span> <span data-ttu-id="815e1-134">Если вы настроили hello ресурсов, предоставляемых на hello SDK (html, изображения, наложения), то у вас есть toobackup их перед обновлением и reapply настройку на обновления ресурсов.</span><span class="sxs-lookup"><span data-stu-id="815e1-134">If you have customized hello resources provided by hello SDK (html, images, overlay) then you have toobackup them before upgrading and reapply your customization on upgraded resources.</span></span>

## <a name="from-111-too200"></a><span data-ttu-id="815e1-135">Из 1.1.1 too2.0.0</span><span class="sxs-lookup"><span data-stu-id="815e1-135">From 1.1.1 too2.0.0</span></span>
<span data-ttu-id="815e1-136">Hello ниже описаны как toomigrate SDK-интеграция с hello обновления Capptain предлагаемых Capptain SAS в приложение на платформе Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="815e1-136">hello following describes how toomigrate an SDK integration from hello Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="815e1-137">Capptain и мобильного охвата не являются hello и теми же службами и только представленные ниже процедуры hello выделяет как toomigrate hello клиентского приложения.</span><span class="sxs-lookup"><span data-stu-id="815e1-137">Capptain and Mobile Engagement are not hello same services and hello procedure given below only highlights how toomigrate hello client app.</span></span> <span data-ttu-id="815e1-138">Миграция hello SDK в приложение hello не выполняют миграцию данных из hello Capptain toohello мобильного охвата серверов</span><span class="sxs-lookup"><span data-stu-id="815e1-138">Migrating hello SDK in hello app will NOT migrate your data from hello Capptain servers toohello Mobile Engagement servers</span></span>
> 
> 

<span data-ttu-id="815e1-139">При переносе из более ранней версии, обратитесь к веб-сайт toomigrate hello Capptain too1.1.1 сначала затем применить после процедуры hello</span><span class="sxs-lookup"><span data-stu-id="815e1-139">If you are migrating from an earlier version, please consult hello Capptain web site toomigrate too1.1.1 first then apply hello following procedure</span></span>

### <a name="nuget-package"></a><span data-ttu-id="815e1-140">Пакет NuGet</span><span class="sxs-lookup"><span data-stu-id="815e1-140">Nuget package</span></span>
<span data-ttu-id="815e1-141">Замените **Capptain.WindowsPhone** на пакет NuGet **MicrosoftAzure.MobileEngagement**.</span><span class="sxs-lookup"><span data-stu-id="815e1-141">Replace **Capptain.WindowsPhone** by **MicrosoftAzure.MobileEngagement** Nuget package.</span></span>

### <a name="applying-mobile-engagement"></a><span data-ttu-id="815e1-142">Применение Служб мобильного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="815e1-142">Applying Mobile Engagement</span></span>
<span data-ttu-id="815e1-143">Hello SDK использует термин hello `Engagement`.</span><span class="sxs-lookup"><span data-stu-id="815e1-143">hello SDK uses hello term `Engagement`.</span></span> <span data-ttu-id="815e1-144">Требуется tooupdate toomatch вашего проекта это изменение.</span><span class="sxs-lookup"><span data-stu-id="815e1-144">You need tooupdate your project toomatch this change.</span></span>

<span data-ttu-id="815e1-145">Необходимо toouninstall текущий пакет nuget Capptain.</span><span class="sxs-lookup"><span data-stu-id="815e1-145">You need toouninstall your current Capptain nuget package.</span></span> <span data-ttu-id="815e1-146">Советуем удалить все, что было изменено в папке ресурсов Capptain.</span><span class="sxs-lookup"><span data-stu-id="815e1-146">Consider that all your changes in Capptain Resources folder will be removed.</span></span> <span data-ttu-id="815e1-147">Если требуется, чтобы tookeep эти файлы затем создается копия их.</span><span class="sxs-lookup"><span data-stu-id="815e1-147">If you want tookeep those files then make a copy of them.</span></span>

<span data-ttu-id="815e1-148">После этого установите hello новый пакет nuget Microsoft Azure Engagement для вашего проекта.</span><span class="sxs-lookup"><span data-stu-id="815e1-148">After that, install hello new Microsoft Azure Engagement nuget package on your project.</span></span> <span data-ttu-id="815e1-149">Его можно найти непосредственно на [веб-сайте NuGet]</span><span class="sxs-lookup"><span data-stu-id="815e1-149">You can find it directly on [nuget website].</span></span> <span data-ttu-id="815e1-150">или здесь в указателе.</span><span class="sxs-lookup"><span data-stu-id="815e1-150">or here index.</span></span> <span data-ttu-id="815e1-151">Это действие заменяет все файлы ресурсов используется охватом и добавляет новые Engagement DLL tooyour hello ссылки на проект.</span><span class="sxs-lookup"><span data-stu-id="815e1-151">This action replaces all resources files used by Engagement and adds hello new Engagement DLL tooyour project References.</span></span>

<span data-ttu-id="815e1-152">У вас есть tooclean ссылки проекта, удалив ссылки на библиотеки DLL Capptain.</span><span class="sxs-lookup"><span data-stu-id="815e1-152">You have tooclean your project references by deleting Capptain DLL references.</span></span> <span data-ttu-id="815e1-153">Если этого не сделать, возникнет конфликт Capptain версии hello и будет происходить ошибки.</span><span class="sxs-lookup"><span data-stu-id="815e1-153">If you do not make this, hello version of Capptain will conflict and errors will happen.</span></span>

<span data-ttu-id="815e1-154">Если вы настроили Capptain ресурсы, скопируйте старые файлы содержимого и вставьте их в новых файлах Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="815e1-154">If you have customized Capptain resources, copy your old files content and paste them in hello new Engagement files.</span></span> <span data-ttu-id="815e1-155">Обратите внимание, xaml и cs-файлы имеют toobe обновить.</span><span class="sxs-lookup"><span data-stu-id="815e1-155">Please note that both xaml and cs files have toobe updated.</span></span>

<span data-ttu-id="815e1-156">После выполнения этих шагов вам достаточно tooreplace старые ссылки Capptain, новые ссылки Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="815e1-156">When those steps are completed you only have tooreplace old Capptain references by hello new Engagement references.</span></span>

1. <span data-ttu-id="815e1-157">Все пространства имен Capptain имеют toobe обновлены.</span><span class="sxs-lookup"><span data-stu-id="815e1-157">All Capptain namespaces have toobe updated.</span></span>
   
    <span data-ttu-id="815e1-158">Перед миграцией:</span><span class="sxs-lookup"><span data-stu-id="815e1-158">Before migration:</span></span>
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    <span data-ttu-id="815e1-159">После миграции:</span><span class="sxs-lookup"><span data-stu-id="815e1-159">After migration:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="815e1-160">Все классы Capptain, содержащие Capptain должны содержать Engagement.</span><span class="sxs-lookup"><span data-stu-id="815e1-160">All Capptain classes that contain "Capptain" should contain "Engagement".</span></span>
   
    <span data-ttu-id="815e1-161">Перед миграцией:</span><span class="sxs-lookup"><span data-stu-id="815e1-161">Before migration:</span></span>
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    <span data-ttu-id="815e1-162">После миграции:</span><span class="sxs-lookup"><span data-stu-id="815e1-162">After migration:</span></span>
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. <span data-ttu-id="815e1-163">Для XAML-файлов изменятся также пространство имен и атрибуты Capptain.</span><span class="sxs-lookup"><span data-stu-id="815e1-163">For xaml files Capptain namespace and attributes also change.</span></span>
   
    <span data-ttu-id="815e1-164">Перед миграцией:</span><span class="sxs-lookup"><span data-stu-id="815e1-164">Before migration:</span></span>
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    <span data-ttu-id="815e1-165">После миграции:</span><span class="sxs-lookup"><span data-stu-id="815e1-165">After migration:</span></span>
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. <span data-ttu-id="815e1-166">Изменяется страница наложения</span><span class="sxs-lookup"><span data-stu-id="815e1-166">Overlay page changes</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="815e1-167">Меняется также и наложение.</span><span class="sxs-lookup"><span data-stu-id="815e1-167">Overlay also changes.</span></span> <span data-ttu-id="815e1-168">Его новым пространство имен является `Microsoft.Azure.Engagement.Overlay`.</span><span class="sxs-lookup"><span data-stu-id="815e1-168">Its new namespace is `Microsoft.Azure.Engagement.Overlay`.</span></span> <span data-ttu-id="815e1-169">Он имеет toobe, используемых в xaml и cs-файлы.</span><span class="sxs-lookup"><span data-stu-id="815e1-169">It has toobe used in both xaml and cs files.</span></span> <span data-ttu-id="815e1-170">Кроме того `CapptainGrid` называется toobe `EngagementGrid`, `capptain_notification_content` и `capptain_announcement_content` именуются `engagement_notification_content` и `engagement_announcement_content`.</span><span class="sxs-lookup"><span data-stu-id="815e1-170">Moreover `CapptainGrid` is toobe named `EngagementGrid`, `capptain_notification_content` and `capptain_announcement_content` are named `engagement_notification_content` and `engagement_announcement_content`.</span></span>
   > 
   > 
   
    <span data-ttu-id="815e1-171">Для наложения:</span><span class="sxs-lookup"><span data-stu-id="815e1-171">For overlay :</span></span>
   
        <capptain:CapptainPageOverlay
          xmlns:capptain="using:Capptain.Overlay"
          ...
        </capptain:CapptainPageOverlay>
   
    <span data-ttu-id="815e1-172">Это будет выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="815e1-172">It becomes :</span></span>
   
        <EngagementPageOverlay
          engagement="using:Microsoft.Azure.Engagement.Overlay"
          ...
        </engagement:EngagementPageOverlay>
5. <span data-ttu-id="815e1-173">Для hello другие ресурсы, такие как Capptain изображений и HTML-файлы, обратите внимание, что они также был переименован toouse «Занят».</span><span class="sxs-lookup"><span data-stu-id="815e1-173">For hello other resources like Capptain pictures and HTML files, please note that they also have been renamed toouse "Engagement".</span></span>

### <a name="project-declaration"></a><span data-ttu-id="815e1-174">Объявление проекта</span><span class="sxs-lookup"><span data-stu-id="815e1-174">Project declaration</span></span>
<span data-ttu-id="815e1-175">В Package.appxmanifest были обновлены следующие элементы `File Type Associations` :</span><span class="sxs-lookup"><span data-stu-id="815e1-175">On Package.appxmanifest `File Type Associations` has been updated from :</span></span>

* <span data-ttu-id="815e1-176">capptain\_достичь\_содержимого tooengagement\_достичь\_содержимого</span><span class="sxs-lookup"><span data-stu-id="815e1-176">capptain\_reach\_content tooengagement\_reach\_content</span></span>
* <span data-ttu-id="815e1-177">capptain\_журнала\_файл tooengagement\_журнала\_файла</span><span class="sxs-lookup"><span data-stu-id="815e1-177">capptain\_log\_file tooengagement\_log\_file</span></span>

### <a name="application-id--sdk-key"></a><span data-ttu-id="815e1-178">Идентификатор приложения и ключ SDK</span><span class="sxs-lookup"><span data-stu-id="815e1-178">Application ID / SDK Key</span></span>
<span data-ttu-id="815e1-179">Engagement использует строку подключения.</span><span class="sxs-lookup"><span data-stu-id="815e1-179">Engagement uses a connection string.</span></span> <span data-ttu-id="815e1-180">Не нужно toospecify идентификатора приложения и ключ SDK с мобильного охвата, имеется только toospecify строку подключения.</span><span class="sxs-lookup"><span data-stu-id="815e1-180">You don't have toospecify an application ID and an SDK key with Mobile Engagement, you only have toospecify a connection string.</span></span> <span data-ttu-id="815e1-181">Ее можно настроить в файле EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="815e1-181">You can set it up on your EngagementConfiguration file.</span></span>

<span data-ttu-id="815e1-182">Hello проектной конфигурации может быть задано в вашей `Resources\EngagementConfiguration.xml` файла проекта.</span><span class="sxs-lookup"><span data-stu-id="815e1-182">hello Engagement configuration can be set in your `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="815e1-183">Измените этот файл toospecify:</span><span class="sxs-lookup"><span data-stu-id="815e1-183">Edit this file toospecify:</span></span>

* <span data-ttu-id="815e1-184">строку подключения приложения между тегами `<connectionString>` and `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="815e1-184">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="815e1-185">Если требуется, чтобы его во время выполнения вместо этого можно вызвать следующие hello toospecify метод до инициализации агента Engagement hello:</span><span class="sxs-lookup"><span data-stu-id="815e1-185">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization:</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(args, engagementConfiguration);

<span data-ttu-id="815e1-186">Hello строку подключения для приложения отображается на hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="815e1-186">hello connection string for your application is displayed on hello Azure Classic Portal.</span></span>

### <a name="items-name-change"></a><span data-ttu-id="815e1-187">Изменение имени элементов</span><span class="sxs-lookup"><span data-stu-id="815e1-187">Items name change</span></span>
<span data-ttu-id="815e1-188">Каждый из элементов с именем *capptain* был переименован на *engagement*.</span><span class="sxs-lookup"><span data-stu-id="815e1-188">All items named *capptain* have been named *engagement*.</span></span> <span data-ttu-id="815e1-189">Аналогичным образом, для *Capptain* слишком*Engagement*.</span><span class="sxs-lookup"><span data-stu-id="815e1-189">Similarly for *Capptain* too*Engagement*.</span></span>

<span data-ttu-id="815e1-190">Примеры часто используемых элементов Capptain:</span><span class="sxs-lookup"><span data-stu-id="815e1-190">Examples of commonly used Capptain items :</span></span>

* <span data-ttu-id="815e1-191">CapptainConfiguration теперь называется EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="815e1-191">CapptainConfiguration now named EngagementConfiguration</span></span>
* <span data-ttu-id="815e1-192">CapptainAgent теперь называется EngagementAgent.</span><span class="sxs-lookup"><span data-stu-id="815e1-192">CapptainAgent now named EngagementAgent</span></span>
* <span data-ttu-id="815e1-193">CapptainReach теперь называется EngagementReach.</span><span class="sxs-lookup"><span data-stu-id="815e1-193">CapptainReach now named EngagementReach</span></span>
* <span data-ttu-id="815e1-194">CapptainHttpConfig теперь называется EngagementHttpConfig.</span><span class="sxs-lookup"><span data-stu-id="815e1-194">CapptainHttpConfig now named EngagementHttpConfig</span></span>
* <span data-ttu-id="815e1-195">GetCapptainPageName теперь называется GetEngagementPageName.</span><span class="sxs-lookup"><span data-stu-id="815e1-195">GetCapptainPageName now named GetEngagementPageName</span></span>

<span data-ttu-id="815e1-196">Обратите внимание, что переименование также влияет на переопределенные методы.</span><span class="sxs-lookup"><span data-stu-id="815e1-196">Note that rename also affects overridden methods.</span></span>

