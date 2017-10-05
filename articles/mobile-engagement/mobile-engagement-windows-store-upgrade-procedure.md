---
title: "Процедуры обновления SDK универсальных приложений для Windows"
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
ms.openlocfilehash: fe85a99a92fb39082cafe7422b356de1f20f14bd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="windows-universal-apps-sdk-upgrade-procedures"></a><span data-ttu-id="ec678-103">Процедуры обновления SDK универсальных приложений для Windows </span><span class="sxs-lookup"><span data-stu-id="ec678-103">Windows Universal Apps SDK Upgrade Procedures</span></span>
<span data-ttu-id="ec678-104">Если вы уже интегрировали в приложение старую версию службы Engagement, при обновлении пакета SDK необходимо учитывать следующее.</span><span class="sxs-lookup"><span data-stu-id="ec678-104">If you already have integrated an older version of Engagement into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="ec678-105">Если вы пропустили несколько версий пакета SDK, вам понадобиться выполнить несколько процедур.</span><span class="sxs-lookup"><span data-stu-id="ec678-105">You may have to follow several procedures if you missed several versions of the SDK.</span></span> <span data-ttu-id="ec678-106">Например, при миграции с версии 0.10.1 в версию 0.11.0 необходимо сначала выполнить процедуру миграции «с 0.9.0 в 0.10.1», а затем процедуру миграции «с 0.10.1 в 0.11.0».</span><span class="sxs-lookup"><span data-stu-id="ec678-106">For example if you migrate from 0.10.1 to 0.11.0 you have to first follow the "from 0.9.0 to 0.10.1" procedure then the "from 0.10.1 to 0.11.0" procedure.</span></span>

## <a name="from-330-to-340"></a><span data-ttu-id="ec678-107">С 3.3.0 в 3.4.0</span><span class="sxs-lookup"><span data-stu-id="ec678-107">From 3.3.0 to 3.4.0</span></span>
### <a name="test-logs"></a><span data-ttu-id="ec678-108">Журналы тестирования</span><span class="sxs-lookup"><span data-stu-id="ec678-108">Test logs</span></span>
<span data-ttu-id="ec678-109">Теперь журналы консоли, созданные с помощью пакета SDK, можно включать, отключать или фильтровать.</span><span class="sxs-lookup"><span data-stu-id="ec678-109">Console logs produced by the SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="ec678-110">Чтобы настроить это действие, обновите свойство `EngagementAgent.Instance.TestLogEnabled` до одного из значений, доступных в перечислении `EngagementTestLogLevel`, например:</span><span class="sxs-lookup"><span data-stu-id="ec678-110">To customize this, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the value available from the `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

### <a name="resources"></a><span data-ttu-id="ec678-111">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="ec678-111">Resources</span></span>
<span data-ttu-id="ec678-112">Было улучшено наложение Reach.</span><span class="sxs-lookup"><span data-stu-id="ec678-112">The Reach overlay has been improved.</span></span> <span data-ttu-id="ec678-113">Оно входит в состав ресурсов пакета SDK NuGet.</span><span class="sxs-lookup"><span data-stu-id="ec678-113">It is part of the SDK NuGet package resources.</span></span>

<span data-ttu-id="ec678-114">Во время обновления до новой версии пакета SDK можно выбрать возможность сохранения существующих файлов из папки наложения ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ec678-114">While upgrading to the new version of the SDK you can choose whether you want to keep your existing files from the overlay folder of your resources or not:</span></span>

* <span data-ttu-id="ec678-115">Если вы используете предыдущее наложение или интегрируете элементы `WebView` вручную, можно оставить существующие файлы — наложение будет работать.</span><span class="sxs-lookup"><span data-stu-id="ec678-115">If the previous overlay is working for you or you are integrating the `WebView` elements manually then you can decide to keep your exiting files, it will still work.</span></span> 
* <span data-ttu-id="ec678-116">Если вы хотите выполнить обновление до нового наложения, просто замените всю папку `overlay` из ресурсов на новую из пакета SDK (приложения UWP: после обновления можно получить новую папку наложения из %USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span><span class="sxs-lookup"><span data-stu-id="ec678-116">If you want to update to the new overlay, just replace the whole `overlay` folder from your resources with the new one from the SDK package (UWP apps: after the upgrade, you can get the new overlay folder from %USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span></span>

> [!WARNING]
> <span data-ttu-id="ec678-117">Новое наложение перезапишет изменения, внесенные в предыдущую версию.</span><span class="sxs-lookup"><span data-stu-id="ec678-117">Using the new overlay will overwrite any customizations made on the previous version.</span></span>
> 
> 

## <a name="from-320-to-330"></a><span data-ttu-id="ec678-118">С 3.2.0 в 3.3.0</span><span class="sxs-lookup"><span data-stu-id="ec678-118">From 3.2.0 to 3.3.0</span></span>
### <a name="resources"></a><span data-ttu-id="ec678-119">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="ec678-119">Resources</span></span>
<span data-ttu-id="ec678-120">Этот шаг относится только к настраиваемым ресурсам.</span><span class="sxs-lookup"><span data-stu-id="ec678-120">This step concerns customized resources only.</span></span> <span data-ttu-id="ec678-121">Если вы настроили ресурсы, предоставляемые в SDK (HTML-код, изображения, наложения), необходимо создать их резервную копию перед обновлением ресурсов и повторным применением к ним настроек.</span><span class="sxs-lookup"><span data-stu-id="ec678-121">If you have customized the resources provided by the SDK (html, images, overlay) then you have to backup them before upgrading and reapply your customization on upgraded resources.</span></span>

## <a name="from-310-to-320"></a><span data-ttu-id="ec678-122">С 3.1.0 на 3.2.0</span><span class="sxs-lookup"><span data-stu-id="ec678-122">From 3.1.0 to 3.2.0</span></span>
### <a name="resources"></a><span data-ttu-id="ec678-123">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="ec678-123">Resources</span></span>
<span data-ttu-id="ec678-124">Этот шаг относится только к настраиваемым ресурсам.</span><span class="sxs-lookup"><span data-stu-id="ec678-124">This step concerns customized resources only.</span></span> <span data-ttu-id="ec678-125">Если вы настроили ресурсы, предоставляемые в SDK (HTML-код, изображения, наложения), необходимо создать их резервную копию перед обновлением ресурсов и повторным применением к ним настроек.</span><span class="sxs-lookup"><span data-stu-id="ec678-125">If you have customized the resources provided by the SDK (html, images, overlay) then you have to backup them before upgrading and reapply your customization on upgraded resources.</span></span>

### <a name="webview-integration"></a><span data-ttu-id="ec678-126">Интеграция веб-представления</span><span class="sxs-lookup"><span data-stu-id="ec678-126">Webview integration</span></span>
<span data-ttu-id="ec678-127">В этой версии улучшено соответствие форм-факторам различных устройств.</span><span class="sxs-lookup"><span data-stu-id="ec678-127">Some improvements to match different device form factors were introduced in this version.</span></span> <span data-ttu-id="ec678-128">Убедитесь, что интеграция веб-представлений выглядит представленным ниже образом.</span><span class="sxs-lookup"><span data-stu-id="ec678-128">Make sure that your integration of the webview match the following:</span></span>

<span data-ttu-id="ec678-129">На XAML-странице ():</span><span class="sxs-lookup"><span data-stu-id="ec678-129">In your XAML page ():</span></span>

            <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Right" VerticalAlignment="Top"/>
            <WebView x:Name="engagement_announcement_content" Visibility="Collapsed" HorizontalAlignment="Right" VerticalAlignment="Top"/> 

<span data-ttu-id="ec678-130">В соответствующем файле CS:</span><span class="sxs-lookup"><span data-stu-id="ec678-130">And in your associated .cs file:</span></span>

    using Microsoft.Azure.Engagement;
    using System;
    using Windows.ApplicationModel.Core;
    using Windows.UI.ViewManagement;
    using Windows.UI.Xaml;
    using Windows.UI.Xaml.Navigation;

    namespace My.Namespace.Example
    {
            /// <summary>
            /// An empty page that can be used on its own or navigated to within a Frame.
            /// </summary>
            public sealed partial class ExampleEngagementReachPage : EngagementPage
            {
              public ExampleEngagementReachPage()
              {
                this.InitializeComponent();

                /* Set your webview elements to the correct size. */
                SetWebView(width, height);
              }

              #region to implement
              /* Attach events when page is navigated. */
              protected override void OnNavigatedTo(NavigationEventArgs e)
              {
                /* Update the webview when the app window is resized. */
                Window.Current.SizeChanged += DisplayProperties_OrientationChanged;

                /* Update the webview when the app/status bar is resized. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged += DisplayProperties_VisibleBoundsChanged; 
    #endif
                base.OnNavigatedTo(e);
              }

              /* When page is left ensure to detach SizeChanged handler. */
              protected override void OnNavigatedFrom(NavigationEventArgs e)
              {
                Window.Current.SizeChanged -= DisplayProperties_OrientationChanged;
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged -= DisplayProperties_VisibleBoundsChanged;
    #endif
                base.OnNavigatedFrom(e);
              }

              /* "width" and "height" are the current size of your application display. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
              double width = ApplicationView.GetForCurrentView().VisibleBounds.Width;
              double height = ApplicationView.GetForCurrentView().VisibleBounds.Height;
    #else
              double width =  Window.Current.Bounds.Width;
              double height =  Window.Current.Bounds.Height;
    #endif

              /// <summary>
              /// Set your webview elements to the correct size.
              /// </summary>
              /// <param name="width">The width of your current display.</param>
              /// <param name="height">The height of your current display.</param>
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
              /// Handler that takes the Windows.Current.SizeChanged and indicates that webviews have to be resized.
              /// </summary>
              /// <param name="sender">Original event trigger.</param>
              /// <param name="e">Window Size Changed Event arguments.</param>
              private void DisplayProperties_OrientationChanged(object sender, Windows.UI.Core.WindowSizeChangedEventArgs e)
              {
                double width = e.Size.Width;
                double height = e.Size.Height;

                /* Set your webview elements to the correct size. */
                SetWebView(width, height);
              }

    #if WINDOWS_PHONE_APP || WINDOWS_UWP              
              /// <summary>
              /// Handler that takes the ApplicationView.VisibleBoundsChanged and indicates that webviews have to be resized
              /// </summary>
              /// <param name="sender">The related application view.</param>
              /// <param name="e">Related event arguments.</param>
              private void DisplayProperties_VisibleBoundsChanged(ApplicationView sender, Object e)
              {
                double width = sender.VisibleBounds.Width;
                double height = sender.VisibleBounds.Height;

                /* Set your webview elements to the correct size. */
                SetWebView(width, height);
              }
    #endif
              #endregion
            }
    }

## <a name="from-200-to-300"></a><span data-ttu-id="ec678-131">Из версии 2.0.0 в 3.0.0</span><span class="sxs-lookup"><span data-stu-id="ec678-131">From 2.0.0 to 3.0.0</span></span>
### <a name="resources"></a><span data-ttu-id="ec678-132">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="ec678-132">Resources</span></span>
<span data-ttu-id="ec678-133">Этот шаг относится только к настраиваемым ресурсам.</span><span class="sxs-lookup"><span data-stu-id="ec678-133">This step concerns customized resources only.</span></span> <span data-ttu-id="ec678-134">Если вы настроили ресурсы, предоставляемые в SDK (HTML-код, изображения, наложения), необходимо создать их резервную копию перед обновлением ресурсов и повторным применением к ним настроек.</span><span class="sxs-lookup"><span data-stu-id="ec678-134">If you have customized the resources provided by the SDK (html, images, overlay) then you have to backup them before upgrading and reapply your customization on upgraded resources.</span></span>

## <a name="from-111-to-200"></a><span data-ttu-id="ec678-135">От версии 1.1.1 до версии 2.0.0</span><span class="sxs-lookup"><span data-stu-id="ec678-135">From 1.1.1 to 2.0.0</span></span>
<span data-ttu-id="ec678-136">Ниже описан процесс переноса интеграции пакета SDK из службы Capptain от Capptain SAS в приложение Служб мобильного взаимодействия Azure.</span><span class="sxs-lookup"><span data-stu-id="ec678-136">The following describes how to migrate an SDK integration from the Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="ec678-137">Службы Capptain и Служб мобильного взаимодействия Azure отличаются между собой. В представленных ниже процедурах описывается способ переноса только для клиентского приложения.</span><span class="sxs-lookup"><span data-stu-id="ec678-137">Capptain and Mobile Engagement are not the same services and the procedure given below only highlights how to migrate the client app.</span></span> <span data-ttu-id="ec678-138">При переносе пакета SDK в приложение данные НЕ будут перенесены с серверов Capptain на серверы Служб мобильного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="ec678-138">Migrating the SDK in the app will NOT migrate your data from the Capptain servers to the Mobile Engagement servers</span></span>
> 
> 

<span data-ttu-id="ec678-139">При переносе с использованием более ранней версии сначала ознакомьтесь с информацией о переносе в версии 1.1.1 на веб-сайте Capptain, а затем примените следующую процедуру.</span><span class="sxs-lookup"><span data-stu-id="ec678-139">If you are migrating from an earlier version, please consult the Capptain web site to migrate to 1.1.1 first then apply the following procedure</span></span>

### <a name="nuget-package"></a><span data-ttu-id="ec678-140">Пакет NuGet</span><span class="sxs-lookup"><span data-stu-id="ec678-140">Nuget package</span></span>
<span data-ttu-id="ec678-141">Замените **Capptain.WindowsPhone** на пакет NuGet **MicrosoftAzure.MobileEngagement**.</span><span class="sxs-lookup"><span data-stu-id="ec678-141">Replace **Capptain.WindowsPhone** by **MicrosoftAzure.MobileEngagement** Nuget package.</span></span>

### <a name="applying-mobile-engagement"></a><span data-ttu-id="ec678-142">Применение Служб мобильного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="ec678-142">Applying Mobile Engagement</span></span>
<span data-ttu-id="ec678-143">В пакете SDK используется термин `Engagement`,</span><span class="sxs-lookup"><span data-stu-id="ec678-143">The SDK uses the term `Engagement`.</span></span> <span data-ttu-id="ec678-144">поэтому необходимо обновить проект с учетом этого изменения.</span><span class="sxs-lookup"><span data-stu-id="ec678-144">You need to update your project to match this change.</span></span>

<span data-ttu-id="ec678-145">Необходимо удалить текущий пакет NuGet Capptain.</span><span class="sxs-lookup"><span data-stu-id="ec678-145">You need to uninstall your current Capptain nuget package.</span></span> <span data-ttu-id="ec678-146">Советуем удалить все, что было изменено в папке ресурсов Capptain.</span><span class="sxs-lookup"><span data-stu-id="ec678-146">Consider that all your changes in Capptain Resources folder will be removed.</span></span> <span data-ttu-id="ec678-147">Если хотите сохранить эти файлы, скопируйте их в другое место.</span><span class="sxs-lookup"><span data-stu-id="ec678-147">If you want to keep those files then make a copy of them.</span></span>

<span data-ttu-id="ec678-148">После этого установите в проекте новый пакет NuGet для Microsoft Azure Engagement.</span><span class="sxs-lookup"><span data-stu-id="ec678-148">After that, install the new Microsoft Azure Engagement nuget package on your project.</span></span> <span data-ttu-id="ec678-149">Его можно найти непосредственно на [веб-сайте NuGet]</span><span class="sxs-lookup"><span data-stu-id="ec678-149">You can find it directly on [nuget website].</span></span> <span data-ttu-id="ec678-150">или здесь в указателе.</span><span class="sxs-lookup"><span data-stu-id="ec678-150">or here index.</span></span> <span data-ttu-id="ec678-151">В результате выполнения этого действия все файлы ресурсов, используемые Engagement, будут заменены, а в ссылки проекта будет добавлена новая библиотека DLL для Engagement.</span><span class="sxs-lookup"><span data-stu-id="ec678-151">This action replaces all resources files used by Engagement and adds the new Engagement DLL to your project References.</span></span>

<span data-ttu-id="ec678-152">Ссылки проекта необходимо очистить, удалив ссылки на библиотеку DLL Capptain.</span><span class="sxs-lookup"><span data-stu-id="ec678-152">You have to clean your project references by deleting Capptain DLL references.</span></span> <span data-ttu-id="ec678-153">Если этого не сделать, возникнет конфликт с версией Capptain и будут происходить ошибки.</span><span class="sxs-lookup"><span data-stu-id="ec678-153">If you do not make this, the version of Capptain will conflict and errors will happen.</span></span>

<span data-ttu-id="ec678-154">После настройки ресурсов Capptain скопируйте содержимое старых файлов и вставьте его в новые файлы Engagement.</span><span class="sxs-lookup"><span data-stu-id="ec678-154">If you have customized Capptain resources, copy your old files content and paste them in the new Engagement files.</span></span> <span data-ttu-id="ec678-155">Обратите внимание, что XAML- и CS-файлы нужно обновить.</span><span class="sxs-lookup"><span data-stu-id="ec678-155">Please note that both xaml and cs files have to be updated.</span></span>

<span data-ttu-id="ec678-156">После выполнения этих шагов необходимо заменить старые ссылки Capptain на новые ссылки Engagement.</span><span class="sxs-lookup"><span data-stu-id="ec678-156">When those steps are completed you only have to replace old Capptain references by the new Engagement references.</span></span>

1. <span data-ttu-id="ec678-157">Все пространства имен Capptain должны быть обновлены.</span><span class="sxs-lookup"><span data-stu-id="ec678-157">All Capptain namespaces have to be updated.</span></span>
   
    <span data-ttu-id="ec678-158">Перед миграцией:</span><span class="sxs-lookup"><span data-stu-id="ec678-158">Before migration:</span></span>
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    <span data-ttu-id="ec678-159">После миграции:</span><span class="sxs-lookup"><span data-stu-id="ec678-159">After migration:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="ec678-160">Все классы Capptain, содержащие Capptain должны содержать Engagement.</span><span class="sxs-lookup"><span data-stu-id="ec678-160">All Capptain classes that contain "Capptain" should contain "Engagement".</span></span>
   
    <span data-ttu-id="ec678-161">Перед миграцией:</span><span class="sxs-lookup"><span data-stu-id="ec678-161">Before migration:</span></span>
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    <span data-ttu-id="ec678-162">После миграции:</span><span class="sxs-lookup"><span data-stu-id="ec678-162">After migration:</span></span>
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. <span data-ttu-id="ec678-163">Для XAML-файлов изменятся также пространство имен и атрибуты Capptain.</span><span class="sxs-lookup"><span data-stu-id="ec678-163">For xaml files Capptain namespace and attributes also change.</span></span>
   
    <span data-ttu-id="ec678-164">Перед миграцией:</span><span class="sxs-lookup"><span data-stu-id="ec678-164">Before migration:</span></span>
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    <span data-ttu-id="ec678-165">После миграции:</span><span class="sxs-lookup"><span data-stu-id="ec678-165">After migration:</span></span>
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. <span data-ttu-id="ec678-166">Изменяется страница наложения</span><span class="sxs-lookup"><span data-stu-id="ec678-166">Overlay page changes</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="ec678-167">Меняется также и наложение.</span><span class="sxs-lookup"><span data-stu-id="ec678-167">Overlay also changes.</span></span> <span data-ttu-id="ec678-168">Его новым пространство имен является `Microsoft.Azure.Engagement.Overlay`.</span><span class="sxs-lookup"><span data-stu-id="ec678-168">Its new namespace is `Microsoft.Azure.Engagement.Overlay`.</span></span> <span data-ttu-id="ec678-169">Оно должно использоваться в XAML- и CS-файлах.</span><span class="sxs-lookup"><span data-stu-id="ec678-169">It has to be used in both xaml and cs files.</span></span> <span data-ttu-id="ec678-170">Кроме того, `CapptainGrid` будет называться `EngagementGrid`, `capptain_notification_content` — `engagement_notification_content`, а `capptain_announcement_content` — `engagement_announcement_content`.</span><span class="sxs-lookup"><span data-stu-id="ec678-170">Moreover `CapptainGrid` is to be named `EngagementGrid`, `capptain_notification_content` and `capptain_announcement_content` are named `engagement_notification_content` and `engagement_announcement_content`.</span></span>
   > 
   > 
   
    <span data-ttu-id="ec678-171">Для наложения:</span><span class="sxs-lookup"><span data-stu-id="ec678-171">For overlay :</span></span>
   
        <capptain:CapptainPageOverlay
          xmlns:capptain="using:Capptain.Overlay"
          ...
        </capptain:CapptainPageOverlay>
   
    <span data-ttu-id="ec678-172">Это будет выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="ec678-172">It becomes :</span></span>
   
        <EngagementPageOverlay
          engagement="using:Microsoft.Azure.Engagement.Overlay"
          ...
        </engagement:EngagementPageOverlay>
5. <span data-ttu-id="ec678-173">Обратите внимание, что для использования Engagement были переименованы и другие ресурсы, такие как изображения Capptain и HTML-файлы.</span><span class="sxs-lookup"><span data-stu-id="ec678-173">For the other resources like Capptain pictures and HTML files, please note that they also have been renamed to use "Engagement".</span></span>

### <a name="project-declaration"></a><span data-ttu-id="ec678-174">Объявление проекта</span><span class="sxs-lookup"><span data-stu-id="ec678-174">Project declaration</span></span>
<span data-ttu-id="ec678-175">В Package.appxmanifest были обновлены следующие элементы `File Type Associations` :</span><span class="sxs-lookup"><span data-stu-id="ec678-175">On Package.appxmanifest `File Type Associations` has been updated from :</span></span>

* <span data-ttu-id="ec678-176">capptain\_reach\_content to engagement\_reach\_content</span><span class="sxs-lookup"><span data-stu-id="ec678-176">capptain\_reach\_content to engagement\_reach\_content</span></span>
* <span data-ttu-id="ec678-177">capptain\_log\_file to engagement\_log\_file</span><span class="sxs-lookup"><span data-stu-id="ec678-177">capptain\_log\_file to engagement\_log\_file</span></span>

### <a name="application-id--sdk-key"></a><span data-ttu-id="ec678-178">Идентификатор приложения и ключ SDK</span><span class="sxs-lookup"><span data-stu-id="ec678-178">Application ID / SDK Key</span></span>
<span data-ttu-id="ec678-179">Engagement использует строку подключения.</span><span class="sxs-lookup"><span data-stu-id="ec678-179">Engagement uses a connection string.</span></span> <span data-ttu-id="ec678-180">При использовании Служб мобильного взаимодействия не нужно указывать идентификатор приложения и ключ SDK. Достаточно просто задать строку подключения.</span><span class="sxs-lookup"><span data-stu-id="ec678-180">You don't have to specify an application ID and an SDK key with Mobile Engagement, you only have to specify a connection string.</span></span> <span data-ttu-id="ec678-181">Ее можно настроить в файле EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="ec678-181">You can set it up on your EngagementConfiguration file.</span></span>

<span data-ttu-id="ec678-182">Конфигурацию Engagement можно определить в файле `Resources\EngagementConfiguration.xml` проекта.</span><span class="sxs-lookup"><span data-stu-id="ec678-182">The Engagement configuration can be set in your `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="ec678-183">Измените этот файл, чтобы указать:</span><span class="sxs-lookup"><span data-stu-id="ec678-183">Edit this file to specify:</span></span>

* <span data-ttu-id="ec678-184">строку подключения приложения между тегами `<connectionString>` and `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="ec678-184">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="ec678-185">Если вместо этого вам необходимо указать ее во время выполнения, можно вызвать следующий метод до инициализации агента Engagement:</span><span class="sxs-lookup"><span data-stu-id="ec678-185">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization:</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(args, engagementConfiguration);

<span data-ttu-id="ec678-186">Строка подключения для приложения отображается на классическом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="ec678-186">The connection string for your application is displayed on the Azure Classic Portal.</span></span>

### <a name="items-name-change"></a><span data-ttu-id="ec678-187">Изменение имени элементов</span><span class="sxs-lookup"><span data-stu-id="ec678-187">Items name change</span></span>
<span data-ttu-id="ec678-188">Каждый из элементов с именем *capptain* был переименован на *engagement*.</span><span class="sxs-lookup"><span data-stu-id="ec678-188">All items named *capptain* have been named *engagement*.</span></span> <span data-ttu-id="ec678-189">Аналогичным образом имя *Capptain* изменилось на *Engagement*.</span><span class="sxs-lookup"><span data-stu-id="ec678-189">Similarly for *Capptain* to *Engagement*.</span></span>

<span data-ttu-id="ec678-190">Примеры часто используемых элементов Capptain:</span><span class="sxs-lookup"><span data-stu-id="ec678-190">Examples of commonly used Capptain items :</span></span>

* <span data-ttu-id="ec678-191">CapptainConfiguration теперь называется EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="ec678-191">CapptainConfiguration now named EngagementConfiguration</span></span>
* <span data-ttu-id="ec678-192">CapptainAgent теперь называется EngagementAgent.</span><span class="sxs-lookup"><span data-stu-id="ec678-192">CapptainAgent now named EngagementAgent</span></span>
* <span data-ttu-id="ec678-193">CapptainReach теперь называется EngagementReach.</span><span class="sxs-lookup"><span data-stu-id="ec678-193">CapptainReach now named EngagementReach</span></span>
* <span data-ttu-id="ec678-194">CapptainHttpConfig теперь называется EngagementHttpConfig.</span><span class="sxs-lookup"><span data-stu-id="ec678-194">CapptainHttpConfig now named EngagementHttpConfig</span></span>
* <span data-ttu-id="ec678-195">GetCapptainPageName теперь называется GetEngagementPageName.</span><span class="sxs-lookup"><span data-stu-id="ec678-195">GetCapptainPageName now named GetEngagementPageName</span></span>

<span data-ttu-id="ec678-196">Обратите внимание, что переименование также влияет на переопределенные методы.</span><span class="sxs-lookup"><span data-stu-id="ec678-196">Note that rename also affects overridden methods.</span></span>

