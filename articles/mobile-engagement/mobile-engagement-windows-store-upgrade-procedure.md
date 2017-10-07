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
# <a name="windows-universal-apps-sdk-upgrade-procedures"></a>Процедуры обновления SDK универсальных приложений для Windows 
Если уже имеется встроенный более старой версии участия в приложение, у вас есть hello tooconsider при обновлении hello SDK следующие точки.

Вы можете иметь toofollow несколько процедур если пропущены несколько версий пакета SDK для hello. Например, если выполняется миграция из 0.10.1 too0.11.0, у вас есть toofirst выполните hello» из 0.9.0 too0.10.1» процедуры, а затем hello» из 0.10.1 too0.11.0» процедуры.

## <a name="from-330-too340"></a>Из 3.3.0 too3.4.0
### <a name="test-logs"></a>Журналы тестирования
Журналы консоли, созданные hello SDK теперь может быть включен и отключен и фильтруются. toocustomize hello, обновить свойство `EngagementAgent.Instance.TestLogEnabled` tooone hello значения, доступные из hello `EngagementTestLogLevel` перечисления, например:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

### <a name="resources"></a>Ресурсы
Улучшена Hello Reach наложения. Он является частью ресурсы пакета SDK NuGet hello.

При обновлении toohello новую версию пакета SDK для hello можно выбрать, следует tookeep ли существующие файлы из hello наложения папки ресурсов или нет.

* Если предыдущих наложения hello работает для вас или интеграции hello `WebView` элементы вручную, можно определить tookeep для существующих файлов, а затем он будет по-прежнему работать. 
* Если требуется новый наложения toohello tooupdate, просто заменить hello всей `overlay` папку из ресурсов с hello новый из пакета SDK для hello (приложений UWP: после обновления hello можно получить hello наложения папку % USERPROFILE %\\. nuget\ packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).

> [!WARNING]
> С помощью нового наложения hello перезапишет все настройки, произведенные в предыдущей версии hello.
> 
> 

## <a name="from-320-too330"></a>Из 3.2.0 too3.3.0
### <a name="resources"></a>Ресурсы
Этот шаг относится только к настраиваемым ресурсам. Если вы настроили hello ресурсов, предоставляемых на hello SDK (html, изображения, наложения), то у вас есть toobackup их перед обновлением и reapply настройку на обновления ресурсов.

## <a name="from-310-too320"></a>Из 3.1.0 too3.2.0
### <a name="resources"></a>Ресурсы
Этот шаг относится только к настраиваемым ресурсам. Если вы настроили hello ресурсов, предоставляемых на hello SDK (html, изображения, наложения), то у вас есть toobackup их перед обновлением и reapply настройку на обновления ресурсов.

### <a name="webview-integration"></a>Интеграция веб-представления
В этой версии появились некоторые усовершенствования toomatch другое устройство форм-факторов. Убедитесь, что вашей интеграции hello webview соответствуют hello следующие:

На XAML-странице ():

            <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Right" VerticalAlignment="Top"/>
            <WebView x:Name="engagement_announcement_content" Visibility="Collapsed" HorizontalAlignment="Right" VerticalAlignment="Top"/> 

В соответствующем файле CS:

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

## <a name="from-200-too300"></a>Из 2.0.0 too3.0.0
### <a name="resources"></a>Ресурсы
Этот шаг относится только к настраиваемым ресурсам. Если вы настроили hello ресурсов, предоставляемых на hello SDK (html, изображения, наложения), то у вас есть toobackup их перед обновлением и reapply настройку на обновления ресурсов.

## <a name="from-111-too200"></a>Из 1.1.1 too2.0.0
Hello ниже описаны как toomigrate SDK-интеграция с hello обновления Capptain предлагаемых Capptain SAS в приложение на платформе Azure Mobile Engagement. 

> [!IMPORTANT]
> Capptain и мобильного охвата не являются hello и теми же службами и только представленные ниже процедуры hello выделяет как toomigrate hello клиентского приложения. Миграция hello SDK в приложение hello не выполняют миграцию данных из hello Capptain toohello мобильного охвата серверов
> 
> 

При переносе из более ранней версии, обратитесь к веб-сайт toomigrate hello Capptain too1.1.1 сначала затем применить после процедуры hello

### <a name="nuget-package"></a>Пакет NuGet
Замените **Capptain.WindowsPhone** на пакет NuGet **MicrosoftAzure.MobileEngagement**.

### <a name="applying-mobile-engagement"></a>Применение Служб мобильного взаимодействия
Hello SDK использует термин hello `Engagement`. Требуется tooupdate toomatch вашего проекта это изменение.

Необходимо toouninstall текущий пакет nuget Capptain. Советуем удалить все, что было изменено в папке ресурсов Capptain. Если требуется, чтобы tookeep эти файлы затем создается копия их.

После этого установите hello новый пакет nuget Microsoft Azure Engagement для вашего проекта. Его можно найти непосредственно на [веб-сайте NuGet] или здесь в указателе. Это действие заменяет все файлы ресурсов используется охватом и добавляет новые Engagement DLL tooyour hello ссылки на проект.

У вас есть tooclean ссылки проекта, удалив ссылки на библиотеки DLL Capptain. Если этого не сделать, возникнет конфликт Capptain версии hello и будет происходить ошибки.

Если вы настроили Capptain ресурсы, скопируйте старые файлы содержимого и вставьте их в новых файлах Engagement hello. Обратите внимание, xaml и cs-файлы имеют toobe обновить.

После выполнения этих шагов вам достаточно tooreplace старые ссылки Capptain, новые ссылки Engagement hello.

1. Все пространства имен Capptain имеют toobe обновлены.
   
    Перед миграцией:
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    После миграции:
   
        using Microsoft.Azure.Engagement;
2. Все классы Capptain, содержащие Capptain должны содержать Engagement.
   
    Перед миграцией:
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    После миграции:
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. Для XAML-файлов изменятся также пространство имен и атрибуты Capptain.
   
    Перед миграцией:
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    После миграции:
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. Изменяется страница наложения
   
   > [!IMPORTANT]
   > Меняется также и наложение. Его новым пространство имен является `Microsoft.Azure.Engagement.Overlay`. Он имеет toobe, используемых в xaml и cs-файлы. Кроме того `CapptainGrid` называется toobe `EngagementGrid`, `capptain_notification_content` и `capptain_announcement_content` именуются `engagement_notification_content` и `engagement_announcement_content`.
   > 
   > 
   
    Для наложения:
   
        <capptain:CapptainPageOverlay
          xmlns:capptain="using:Capptain.Overlay"
          ...
        </capptain:CapptainPageOverlay>
   
    Это будет выглядеть так:
   
        <EngagementPageOverlay
          engagement="using:Microsoft.Azure.Engagement.Overlay"
          ...
        </engagement:EngagementPageOverlay>
5. Для hello другие ресурсы, такие как Capptain изображений и HTML-файлы, обратите внимание, что они также был переименован toouse «Занят».

### <a name="project-declaration"></a>Объявление проекта
В Package.appxmanifest были обновлены следующие элементы `File Type Associations` :

* capptain\_достичь\_содержимого tooengagement\_достичь\_содержимого
* capptain\_журнала\_файл tooengagement\_журнала\_файла

### <a name="application-id--sdk-key"></a>Идентификатор приложения и ключ SDK
Engagement использует строку подключения. Не нужно toospecify идентификатора приложения и ключ SDK с мобильного охвата, имеется только toospecify строку подключения. Ее можно настроить в файле EngagementConfiguration.

Hello проектной конфигурации может быть задано в вашей `Resources\EngagementConfiguration.xml` файла проекта.

Измените этот файл toospecify:

* строку подключения приложения между тегами `<connectionString>` and `<\connectionString>`.

Если требуется, чтобы его во время выполнения вместо этого можно вызвать следующие hello toospecify метод до инициализации агента Engagement hello:

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(args, engagementConfiguration);

Hello строку подключения для приложения отображается на hello классический портал Azure.

### <a name="items-name-change"></a>Изменение имени элементов
Каждый из элементов с именем *capptain* был переименован на *engagement*. Аналогичным образом, для *Capptain* слишком*Engagement*.

Примеры часто используемых элементов Capptain:

* CapptainConfiguration теперь называется EngagementConfiguration.
* CapptainAgent теперь называется EngagementAgent.
* CapptainReach теперь называется EngagementReach.
* CapptainHttpConfig теперь называется EngagementHttpConfig.
* GetCapptainPageName теперь называется GetEngagementPageName.

Обратите внимание, что переименование также влияет на переопределенные методы.

