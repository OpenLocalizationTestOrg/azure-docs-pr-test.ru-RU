---
title: "защищенные aaaGeo push-уведомлений с концентраторами уведомлений Azure и Bing пространственных данных | Документы Microsoft"
description: "В этом учебнике вы узнаете, как на основе расположения toodeliver извещающих уведомлений с концентраторами уведомлений Azure и Bing пространственных данных."
services: notification-hubs
documentationcenter: windows
keywords: "push-уведомление, push-уведомление"
author: dend
manager: yuaxu
editor: dend
ms.assetid: f41beea1-0d62-4418-9ffc-c9d70607a1b7
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/31/2016
ms.author: dendeli
ms.openlocfilehash: d6efe473537f2159240c53e780741f12619c045d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="geo-fenced-push-notifications-with-azure-notification-hubs-and-bing-spatial-data"></a><span data-ttu-id="6d164-104">Отправка push-уведомлений с определением геозон с помощью Центров уведомлений Azure и Bing Spatial Data</span><span class="sxs-lookup"><span data-stu-id="6d164-104">Geo-fenced push notifications with Azure Notification Hubs and Bing Spatial Data</span></span>
> [!NOTE]
> <span data-ttu-id="6d164-105">toocomplete этого учебника необходимо иметь активную учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="6d164-105">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="6d164-106">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="6d164-106">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="6d164-107">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02).</span><span class="sxs-lookup"><span data-stu-id="6d164-107">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02).</span></span>
> 
> 

<span data-ttu-id="6d164-108">В этом учебнике вы узнаете, как на основе расположения toodeliver извещающих уведомлений с концентраторами уведомлений Azure и Bing пространственными данными из будет применить в приложении универсальной платформы Windows.</span><span class="sxs-lookup"><span data-stu-id="6d164-108">In this tutorial, you will learn how toodeliver location-based push notifications with Azure Notification Hubs and Bing Spatial Data, leveraged from within a Universal Windows Platform application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d164-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6d164-109">Prerequisites</span></span>
<span data-ttu-id="6d164-110">Первое и самое главное необходимо наличие всех hello программного обеспечения и услуг предварительным toomake:</span><span class="sxs-lookup"><span data-stu-id="6d164-110">First and foremost, you need toomake sure that you have all hello software and service pre-requisites:</span></span>

* <span data-ttu-id="6d164-111">[Visual Studio 2015 с обновлением 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) или более поздней версии (также подойдет [Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409));</span><span class="sxs-lookup"><span data-stu-id="6d164-111">[Visual Studio 2015 Update 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) or later ([Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409) will do as well).</span></span> 
* <span data-ttu-id="6d164-112">Последнюю версию hello [пакета Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="6d164-112">Latest version of hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> 
* <span data-ttu-id="6d164-113">[учетная запись Центра разработки Карт Bing](https://www.bingmapsportal.com/) (ее можно создать бесплатно и связать с учетной записью Майкрософт).</span><span class="sxs-lookup"><span data-stu-id="6d164-113">[Bing Maps Dev Center account](https://www.bingmapsportal.com/) (you can create one for free and associate it with your Microsoft account).</span></span> 

## <a name="getting-started"></a><span data-ttu-id="6d164-114">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="6d164-114">Getting Started</span></span>
<span data-ttu-id="6d164-115">Давайте начнем с создания проекта hello.</span><span class="sxs-lookup"><span data-stu-id="6d164-115">Let’s start by creating hello project.</span></span> <span data-ttu-id="6d164-116">В Visual Studio создайте новый проект типа **Пустое приложение (универсальное приложение Windows)**.</span><span class="sxs-lookup"><span data-stu-id="6d164-116">In Visual Studio, start a new project of type **Blank App (Universal Windows)**.</span></span>

![](./media/notification-hubs-geofence/notification-hubs-create-blank-app.png)

<span data-ttu-id="6d164-117">После завершения создания проекта hello должны иметь hello окружение для самого приложения hello.</span><span class="sxs-lookup"><span data-stu-id="6d164-117">Once hello project creation is complete, you should have hello harness for hello app itself.</span></span> <span data-ttu-id="6d164-118">Теперь давайте Установка всех компонентов инфраструктуры геозон hello.</span><span class="sxs-lookup"><span data-stu-id="6d164-118">Now let’s set up everything for hello geo-fencing infrastructure.</span></span> <span data-ttu-id="6d164-119">Так как мы toouse постоянной службами Bing для этого, есть общедоступную конечную точку REST API, мы сможем кадры tooquery конкретное расположение:</span><span class="sxs-lookup"><span data-stu-id="6d164-119">Because we are going toouse Bing services for this, there is a public REST API endpoint that allows us tooquery specific location frames:</span></span>

    http://spatial.virtualearth.net/REST/v1/data/

<span data-ttu-id="6d164-120">Вам потребуется toospecify hello следующие tooget параметры его работы:</span><span class="sxs-lookup"><span data-stu-id="6d164-120">You will need toospecify hello following parameters tooget it working:</span></span>

* <span data-ttu-id="6d164-121">**Идентификатор источника данных** и **Имя источника данных.** В API Карт Bing источники данных содержат различные сегментированные метаданные, например о местоположении и часах работы.</span><span class="sxs-lookup"><span data-stu-id="6d164-121">**Data Source ID** and **Data Source Name** – in Bing Maps API, data sources contain various bucketed metadata, such as locations and business hours of operation.</span></span> <span data-ttu-id="6d164-122">Дополнительные сведения об этих метаданных можно прочесть здесь.</span><span class="sxs-lookup"><span data-stu-id="6d164-122">You can read more about those here.</span></span> 
* <span data-ttu-id="6d164-123">**Имя сущности** — hello сущность будет toouse как опорную точку для hello уведомления.</span><span class="sxs-lookup"><span data-stu-id="6d164-123">**Entity Name** – hello entity you want toouse as a reference point for hello notification.</span></span> 
* <span data-ttu-id="6d164-124">**Ключ Bing Maps API** — это ключ hello, полученный ранее при создании учетной записи центра разработчиков Bing hello.</span><span class="sxs-lookup"><span data-stu-id="6d164-124">**Bing Maps API Key** – this is hello key that you obtained earlier when you created hello Bing Dev Center account.</span></span>

<span data-ttu-id="6d164-125">Давайте глубокое погружение в hello установки необходимо сделать для каждого из элементов hello выше.</span><span class="sxs-lookup"><span data-stu-id="6d164-125">Let’s do a deep-dive on hello setup for each of hello elements above.</span></span>

## <a name="setting-up-hello-data-source"></a><span data-ttu-id="6d164-126">Настройка источника данных hello</span><span class="sxs-lookup"><span data-stu-id="6d164-126">Setting up hello data source</span></span>
<span data-ttu-id="6d164-127">Это можно сделать в hello центра разработчиков Bing Maps.</span><span class="sxs-lookup"><span data-stu-id="6d164-127">You can do it in hello Bing Maps Dev Center.</span></span> <span data-ttu-id="6d164-128">Просто щелкните **источники данных** hello навигации в верхней части панели и выберите **Управление источниками данных**.</span><span class="sxs-lookup"><span data-stu-id="6d164-128">Simply click on **Data sources** in hello top navigation bar and select **Manage Data Sources**.</span></span>

![](./media/notification-hubs-geofence/bing-maps-manage-data.png)

<span data-ttu-id="6d164-129">Если вы не работали с API службы Bing Maps перед, скорее не будет существовать присутствует, источников данных, можно просто создать новые, щелкнув на источнике данных tooa передачи данных.</span><span class="sxs-lookup"><span data-stu-id="6d164-129">If you have not worked with Bing Maps API before, most likely there won’t be any data sources present, so you can just create a new one by clicking on Upload data tooa data source.</span></span> <span data-ttu-id="6d164-130">Убедитесь, что заполните все необходимые hello поля:</span><span class="sxs-lookup"><span data-stu-id="6d164-130">Make sure you fill out all hello required fields:</span></span>

![](./media/notification-hubs-geofence/bing-maps-create-data.png)

<span data-ttu-id="6d164-131">Может возникнуть вопрос, — что такое файл данных hello и что должно загружаете вы?</span><span class="sxs-lookup"><span data-stu-id="6d164-131">You might be wondering – what is hello data file and what should you be uploading?</span></span> <span data-ttu-id="6d164-132">В целях hello этого теста можно просто используйте образец hello основе канала вокруг области waterfront Сан-Франциско hello:</span><span class="sxs-lookup"><span data-stu-id="6d164-132">For hello purposes of this test, we can just use hello sample pipe-based that frames an area of hello San Francisco waterfront:</span></span>

    Bing Spatial Data Services, 1.0, TestBoundaries
    EntityID(Edm.String,primaryKey)|Name(Edm.String)|Longitude(Edm.Double)|Latitude(Edm.Double)|Boundary(Edm.Geography)
    1|SanFranciscoPier|||POLYGON ((-122.389825 37.776598,-122.389438 37.773087,-122.381885 37.771849,-122.382186 37.777022,-122.389825 37.776598))

<span data-ttu-id="6d164-133">Hello выше представляет этой сущности.</span><span class="sxs-lookup"><span data-stu-id="6d164-133">hello above represents this entity:</span></span>

![](./media/notification-hubs-geofence/bing-maps-geofence.png)

<span data-ttu-id="6d164-134">Просто скопируйте и вставьте строку hello выше в новый файл и сохраните его в виде **NotificationHubsGeofence.pipe**и его отправки в центр разработчиков Bing hello.</span><span class="sxs-lookup"><span data-stu-id="6d164-134">Simply copy and paste hello string above into a new file and save it as **NotificationHubsGeofence.pipe**, and upload it in hello Bing Dev Center.</span></span>

> [!NOTE]
> <span data-ttu-id="6d164-135">Может появиться запрос toospecify новый ключ для hello **главный ключ** , отличается от hello **ключа запроса**.</span><span class="sxs-lookup"><span data-stu-id="6d164-135">You might be prompted toospecify a new key for hello **Master Key** that is different from hello **Query Key**.</span></span> <span data-ttu-id="6d164-136">Просто создайте новый ключ по hello панели мониторинга и обновления hello страницу источника данных передачи.</span><span class="sxs-lookup"><span data-stu-id="6d164-136">Simply create a new key through hello dashboard and refresh hello data source upload page.</span></span>
> 
> 

<span data-ttu-id="6d164-137">После загрузки файла данных hello потребуется toomake убедитесь, что публикуется hello источника данных.</span><span class="sxs-lookup"><span data-stu-id="6d164-137">Once you upload hello data file, you will need toomake sure that you publish hello data source.</span></span> 

<span data-ttu-id="6d164-138">Go слишком**Управление источниками данных**, так же, как описано выше, определить источник данных в списке hello и щелкнуть **публикации** в hello **действия** столбца.</span><span class="sxs-lookup"><span data-stu-id="6d164-138">Go too**Manage Data Sources**, just like we did above, find your data source in hello list and click on **Publish** in hello **Actions** column.</span></span> <span data-ttu-id="6d164-139">В немного, вы увидите источника данных в hello **опубликованные источники данных** вкладки:</span><span class="sxs-lookup"><span data-stu-id="6d164-139">In a bit, you should see your data source in hello **Published Data Sources** tab:</span></span>

![](./media/notification-hubs-geofence/bing-maps-published-data.png)

<span data-ttu-id="6d164-140">При нажатии кнопки **изменить**, вам будет toosee может быстро каких расположений, мы представили в ней:</span><span class="sxs-lookup"><span data-stu-id="6d164-140">If you click **Edit**, you will be able toosee at a glance what locations we introduced in it:</span></span>

![](./media/notification-hubs-geofence/bing-maps-data-details.png)

<span data-ttu-id="6d164-141">На этом этапе портал hello не показывает hello границы для geofence hello, мы создали — все, что нам нужно является подтверждением, hello расположение, указанное в правой окружения hello.</span><span class="sxs-lookup"><span data-stu-id="6d164-141">At this point, hello portal does not show you hello boundaries for hello geofence that we created – all we need is a confirmation that hello location specified is in hello right vicinity.</span></span>

<span data-ttu-id="6d164-142">Теперь у вас все требования к hello для источника данных hello.</span><span class="sxs-lookup"><span data-stu-id="6d164-142">Now you have all hello requirements for hello data source.</span></span> <span data-ttu-id="6d164-143">Щелкните tooget hello сведения о URL-адрес запроса hello для вызова hello API в центр разработчиков Bing Maps, hello **источники данных** и выберите **источника данных**.</span><span class="sxs-lookup"><span data-stu-id="6d164-143">tooget hello details on hello request URL for hello API call, in hello Bing Maps Dev Center, click **Data sources** and select **Data Source Information**.</span></span>

![](./media/notification-hubs-geofence/bing-maps-data-info.png)

<span data-ttu-id="6d164-144">Hello **URL-адрес запроса** : у после нее.</span><span class="sxs-lookup"><span data-stu-id="6d164-144">hello **Query URL** is what we’re after here.</span></span> <span data-ttu-id="6d164-145">Это конечная точка hello, для которого можно выполнить запросы toocheck ли hello устройство в настоящий момент в пределах границ hello расположения или нет.</span><span class="sxs-lookup"><span data-stu-id="6d164-145">This is hello endpoint against which we can execute queries toocheck whether hello device is currently within hello boundaries of a location or not.</span></span> <span data-ttu-id="6d164-146">это проверить, мы просто необходимо вызвать GET к URL-адрес запроса hello с hello следующие параметры, которые добавляются tooexecute tooperform:</span><span class="sxs-lookup"><span data-stu-id="6d164-146">tooperform this check, we simply need tooexecute a GET call against hello query URL, with hello following parameters appended:</span></span>

    ?spatialFilter=intersects(%27POINT%20LONGITUDE%20LATITUDE)%27)&$format=json&key=QUERY_KEY

<span data-ttu-id="6d164-147">Таким образом задается целевой точки, что мы получаем от устройства hello и Bing Maps автоматически выполнит toosee вычисления hello, является ли она в hello geofence.</span><span class="sxs-lookup"><span data-stu-id="6d164-147">That way you're specifying a target point that we obtain from hello device and Bing Maps will automatically perform hello calculations toosee whether it is within hello geofence.</span></span> <span data-ttu-id="6d164-148">После своего выполнения hello запроса с помощью браузера (или cURL), вы получите стандартный ответ JSON:</span><span class="sxs-lookup"><span data-stu-id="6d164-148">Once you execute hello request through a browser (or cURL), you will get standard a JSON response:</span></span>

![](./media/notification-hubs-geofence/bing-maps-json.png)

<span data-ttu-id="6d164-149">Этот ответ происходит только в том случае, когда точка hello фактически находится в пределах указанных границ hello.</span><span class="sxs-lookup"><span data-stu-id="6d164-149">This response only happens when hello point is actually within hello designated boundaries.</span></span> <span data-ttu-id="6d164-150">Если она находится за пределами, сегмент **results** будет пустым:</span><span class="sxs-lookup"><span data-stu-id="6d164-150">If it is not, you will get an empty **results** bucket:</span></span>

![](./media/notification-hubs-geofence/bing-maps-nores.png)

## <a name="setting-up-hello-uwp-application"></a><span data-ttu-id="6d164-151">Настройка приложения UWP hello</span><span class="sxs-lookup"><span data-stu-id="6d164-151">Setting up hello UWP application</span></span>
<span data-ttu-id="6d164-152">Теперь, когда у нас есть источник данных hello готова, мы можем запустить работаете hello приложения UWP, который мы ранее начальной загрузки.</span><span class="sxs-lookup"><span data-stu-id="6d164-152">Now that we have hello data source ready, we can start working on hello UWP application that we bootstrapped earlier.</span></span>

<span data-ttu-id="6d164-153">Прежде всего для приложения необходимо включить службы обнаружения местоположения.</span><span class="sxs-lookup"><span data-stu-id="6d164-153">First and foremost, we must enable location services for our application.</span></span> <span data-ttu-id="6d164-154">toodo это, дважды щелкните `Package.appxmanifest` файла в **обозревателе решений**.</span><span class="sxs-lookup"><span data-stu-id="6d164-154">toodo this, double-click on `Package.appxmanifest` file in **Solution Explorer**.</span></span>

![](./media/notification-hubs-geofence/vs-package-manifest.png)

<span data-ttu-id="6d164-155">На вкладке Свойства hello пакета, только что открыли, нажмите кнопку **возможности** и убедитесь, что выбрана **расположение**:</span><span class="sxs-lookup"><span data-stu-id="6d164-155">In hello package properties tab that just opened, click on **Capabilities** and make sure that you select **Location**:</span></span>

![](./media/notification-hubs-geofence/vs-package-location.png)

<span data-ttu-id="6d164-156">Как объявлена возможность расположение hello, создайте новую папку с именем решения `Core`и добавьте новый файл в нем вызывается `LocationHelper.cs`:</span><span class="sxs-lookup"><span data-stu-id="6d164-156">As hello location capability is declared, create a new folder in your solution named `Core`, and add a new file within it, called `LocationHelper.cs`:</span></span>

![](./media/notification-hubs-geofence/vs-location-helper.png)

<span data-ttu-id="6d164-157">Hello `LocationHelper` самого класса на этом этапе производится достаточно просто — он осуществляет разрешить нам местонахождения пользователя hello tooobtain через API-Интерфейсу системы hello:</span><span class="sxs-lookup"><span data-stu-id="6d164-157">hello `LocationHelper` class itself is fairly basic at this point – all it does is allow us tooobtain hello user location through hello system API:</span></span>

    using System;
    using System.Threading.Tasks;
    using Windows.Devices.Geolocation;

    namespace NotificationHubs.Geofence.Core
    {
        public class LocationHelper
        {
            private static readonly uint AppDesiredAccuracyInMeters = 10;

            public async static Task<Geoposition> GetCurrentLocation()
            {
                var accessStatus = await Geolocator.RequestAccessAsync();
                switch (accessStatus)
                {
                    case GeolocationAccessStatus.Allowed:
                        {
                            Geolocator geolocator = new Geolocator { DesiredAccuracyInMeters = AppDesiredAccuracyInMeters };

                            return await geolocator.GetGeopositionAsync();
                        }
                    default:
                        {
                            return null;
                        }
                }
            }

        }
    }

<span data-ttu-id="6d164-158">Можно прочитать дополнительные сведения о получении hello расположения пользователя в приложениях UWP в официальное hello [документе MSDN](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx).</span><span class="sxs-lookup"><span data-stu-id="6d164-158">You can read more about getting hello user’s location in UWP apps in hello official [MSDN document](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx).</span></span>

<span data-ttu-id="6d164-159">toocheck, приобретения расположение hello фактически работает, откройте стороне кода hello главной странице (`MainPage.xaml.cs`).</span><span class="sxs-lookup"><span data-stu-id="6d164-159">toocheck that hello location acquisition is actually working, open hello code side of your main page (`MainPage.xaml.cs`).</span></span> <span data-ttu-id="6d164-160">Создает новый обработчик событий для hello `Loaded` события в hello `MainPage` конструктор:</span><span class="sxs-lookup"><span data-stu-id="6d164-160">Create a new event handler for hello `Loaded` event in hello `MainPage` constructor:</span></span>

    public MainPage()
    {
        this.InitializeComponent();
        this.Loaded += MainPage_Loaded;
    }

<span data-ttu-id="6d164-161">Реализация обработчика событий hello Hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6d164-161">hello implementation of hello event handler is as follows:</span></span>

    private async void MainPage_Loaded(object sender, RoutedEventArgs e)
    {
        var location = await LocationHelper.GetCurrentLocation();

        if (location != null)
        {
            Debug.WriteLine(string.Concat(location.Coordinate.Longitude,
                " ", location.Coordinate.Latitude));
        }
    }

<span data-ttu-id="6d164-162">Обратите внимание, что мы объявить обработчик hello асинхронным поскольку `GetCurrentLocation` типа awaitable и поэтому требует toobe, выполняются в контексте async.</span><span class="sxs-lookup"><span data-stu-id="6d164-162">Notice that we declared hello handler as async because `GetCurrentLocation` is awaitable, and therefore requires toobe executed in an async context.</span></span> <span data-ttu-id="6d164-163">Кроме того так как при определенных обстоятельствах мы может оказаться, что с пустым местом (hello расположение службы отключены или приложения hello запрещен расположение tooaccess разрешения), нам нужно убедиться, что правильно обрабатываются с помощью проверки null toomake.</span><span class="sxs-lookup"><span data-stu-id="6d164-163">Also, because under certain circumstances we might end up with a null location (e.g. hello location services are disabled or hello application was denied permissions tooaccess location), we need toomake sure that it is properly handled with a null check.</span></span>

<span data-ttu-id="6d164-164">Запустите приложение hello.</span><span class="sxs-lookup"><span data-stu-id="6d164-164">Run hello application.</span></span> <span data-ttu-id="6d164-165">Обязательно разрешите доступ к местоположению:</span><span class="sxs-lookup"><span data-stu-id="6d164-165">Make sure you allow location access:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-location-access.png)

<span data-ttu-id="6d164-166">Один раз Здравствуйте запускает приложение, должен быть координаты hello может toosee hello **вывода** окна:</span><span class="sxs-lookup"><span data-stu-id="6d164-166">Once hello application launches, you should be able toosee hello coordinates in hello **Output** window:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-location-output.png)

<span data-ttu-id="6d164-167">Теперь вы знаете, что works приобретения расположение — вид обработчик событий теста hello свободного tooremove Loaded так, как мы не будет использоваться его больше.</span><span class="sxs-lookup"><span data-stu-id="6d164-167">Now you know that location acquisition works – feel free tooremove hello test event handler for Loaded because we won’t be using it anymore.</span></span>

<span data-ttu-id="6d164-168">Hello следующим шагом будет изменение места toocapture.</span><span class="sxs-lookup"><span data-stu-id="6d164-168">hello next step is toocapture location changes.</span></span> <span data-ttu-id="6d164-169">Для этого, давайте рассмотрим задней toohello `LocationHelper` и добавьте обработчик событий hello `PositionChanged`:</span><span class="sxs-lookup"><span data-stu-id="6d164-169">For that, let’s go back toohello `LocationHelper` class and add hello event handler for `PositionChanged`:</span></span>

    geolocator.PositionChanged += Geolocator_PositionChanged;

<span data-ttu-id="6d164-170">Реализация Hello покажет координаты местоположения hello hello **вывода** окна:</span><span class="sxs-lookup"><span data-stu-id="6d164-170">hello implementation will show hello location coordinates in hello **Output** window:</span></span>

    private static async void Geolocator_PositionChanged(Geolocator sender, PositionChangedEventArgs args)
    {
        await CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
        {
            Debug.WriteLine(string.Concat(args.Position.Coordinate.Longitude, " ", args.Position.Coordinate.Latitude));
        });
    }

## <a name="setting-up-hello-backend"></a><span data-ttu-id="6d164-171">Настройка внутреннего hello</span><span class="sxs-lookup"><span data-stu-id="6d164-171">Setting up hello backend</span></span>
<span data-ttu-id="6d164-172">Загрузите hello [образец серверной части .NET из GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span><span class="sxs-lookup"><span data-stu-id="6d164-172">Download hello [.NET Backend Sample from GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span></span> <span data-ttu-id="6d164-173">После завершения загрузки Привет открыть hello `NotifyUsers` папки, а затем — hello `NotifyUsers.sln` файла.</span><span class="sxs-lookup"><span data-stu-id="6d164-173">Once hello download completes, open hello `NotifyUsers` folder, and subsequently – hello `NotifyUsers.sln` file.</span></span>

<span data-ttu-id="6d164-174">Набор hello `AppBackend` проект как hello **запускаемый проект** и запустить его.</span><span class="sxs-lookup"><span data-stu-id="6d164-174">Set hello `AppBackend` project as hello **StartUp Project** and launch it.</span></span>

![](./media/notification-hubs-geofence/vs-startup-project.png)

<span data-ttu-id="6d164-175">Hello проекта, уже настроенные toosend принудительной уведомления tootarget устройства, поэтому нам нужно только две вещи toodo — выгрузить hello правильной строки подключения для концентратора уведомлений hello и добавить toosend hello идентификации границ уведомление, только если hello пользователь входит в hello geofence.</span><span class="sxs-lookup"><span data-stu-id="6d164-175">hello project is already configured toosend push notifications tootarget devices, so we’ll need toodo only two things – swap out hello right connection string for hello notification hub and add boundary identification toosend hello notification only when hello user is within hello geofence.</span></span>

<span data-ttu-id="6d164-176">Строка подключения hello tooconfigure в hello `Models` откройте папку `Notifications.cs`.</span><span class="sxs-lookup"><span data-stu-id="6d164-176">tooconfigure hello connection string, in hello `Models` folder open `Notifications.cs`.</span></span> <span data-ttu-id="6d164-177">Hello `NotificationHubClient.CreateClientFromConnectionString` функция должна содержать hello сведения о концентраторе уведомлений, которые можно получить в hello [портала Azure](https://portal.azure.com) (обзора hello **политики доступа** колонки в  **Параметры**).</span><span class="sxs-lookup"><span data-stu-id="6d164-177">hello `NotificationHubClient.CreateClientFromConnectionString` function should contain hello information about your notification hub that you can get in hello [Azure Portal](https://portal.azure.com) (look inside hello **Access Policies** blade in **Settings**).</span></span> <span data-ttu-id="6d164-178">Сохраните файл обновленной конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="6d164-178">Save hello updated configuration file.</span></span>

<span data-ttu-id="6d164-179">Теперь нужно toocreate модели для hello результат API службы Bing Maps.</span><span class="sxs-lookup"><span data-stu-id="6d164-179">Now we need toocreate a model for hello Bing Maps API result.</span></span> <span data-ttu-id="6d164-180">Здравствуйте, наиболее простым способом toodo, щелкните правой кнопкой мыши на hello `Models` папке **добавить** > **класса**.</span><span class="sxs-lookup"><span data-stu-id="6d164-180">hello easiest way toodo that is right-click on hello `Models` folder, **Add** > **Class**.</span></span> <span data-ttu-id="6d164-181">Назовите его `GeofenceBoundary.cs`.</span><span class="sxs-lookup"><span data-stu-id="6d164-181">Name it `GeofenceBoundary.cs`.</span></span> <span data-ttu-id="6d164-182">После завершения копирования hello JSON из ответа hello API, которое мы обсуждали в первом разделе hello и Visual Studio используется **изменить** > **Специальная вставка** > **вставить JSON как классы**.</span><span class="sxs-lookup"><span data-stu-id="6d164-182">Once done, copy hello JSON from hello API response that we discussed in hello first section and in Visual Studio use **Edit** > **Paste Special** > **Paste JSON as Classes**.</span></span> 

<span data-ttu-id="6d164-183">Таким образом, мы обеспечиваем hello объекта будут десериализованы точно так, как предполагалось.</span><span class="sxs-lookup"><span data-stu-id="6d164-183">That way we ensure that hello object will be deserialized exactly as it was intended.</span></span> <span data-ttu-id="6d164-184">Итоговый набор классов должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6d164-184">Your resulting class set should resemble this:</span></span>

    namespace AppBackend.Models
    {
        public class Rootobject
        {
            public D d { get; set; }
        }

        public class D
        {
            public string __copyright { get; set; }
            public Result[] results { get; set; }
        }

        public class Result
        {
            public __Metadata __metadata { get; set; }
            public string EntityID { get; set; }
            public string Name { get; set; }
            public float Longitude { get; set; }
            public float Latitude { get; set; }
            public string Boundary { get; set; }
            public string Confidence { get; set; }
            public string Locality { get; set; }
            public string AddressLine { get; set; }
            public string AdminDistrict { get; set; }
            public string CountryRegion { get; set; }
            public string PostalCode { get; set; }
        }

        public class __Metadata
        {
            public string uri { get; set; }
        }
    }

<span data-ttu-id="6d164-185">Затем откройте `Controllers` > `NotificationsController.cs`.</span><span class="sxs-lookup"><span data-stu-id="6d164-185">Next, open `Controllers` > `NotificationsController.cs`.</span></span> <span data-ttu-id="6d164-186">Нужно tootweak hello Post вызов tooaccount для hello целевой широты и долготы.</span><span class="sxs-lookup"><span data-stu-id="6d164-186">We need tootweak hello Post call tooaccount for hello target longitude and latitude.</span></span> <span data-ttu-id="6d164-187">Для этого просто добавьте сигнатуру функции toohello две строки — `latitude` и `longitude`.</span><span class="sxs-lookup"><span data-stu-id="6d164-187">For that, simply add two strings toohello function signature – `latitude` and `longitude`.</span></span>

    public async Task<HttpResponseMessage> Post(string pns, [FromBody]string message, string to_tag, string latitude, string longitude)

<span data-ttu-id="6d164-188">Создайте новый класс в проект с именем hello `ApiHelper.cs` — мы будем использовать tooconnect tooBing toocheck точки границы пересечения.</span><span class="sxs-lookup"><span data-stu-id="6d164-188">Create a new class within hello project called `ApiHelper.cs` – we’ll use it tooconnect tooBing toocheck point boundary intersections.</span></span> <span data-ttu-id="6d164-189">Выполните функцию `IsPointWithinBounds` следующим образом.</span><span class="sxs-lookup"><span data-stu-id="6d164-189">Implement a `IsPointWithinBounds` function, like this:</span></span>

    public class ApiHelper
    {
        public static readonly string ApiEndpoint = "{YOUR_QUERY_ENDPOINT}?spatialFilter=intersects(%27POINT%20({0}%20{1})%27)&$format=json&key={2}";
        public static readonly string ApiKey = "{YOUR_API_KEY}";

        public static bool IsPointWithinBounds(string longitude,string latitude)
        {
            var json = new WebClient().DownloadString(string.Format(ApiEndpoint, longitude, latitude, ApiKey));
            var result = JsonConvert.DeserializeObject<Rootobject>(json);
            if (result.d.results != null && result.d.results.Count() > 0)
            {
                return true;
            }
            else
            {
                return false;
            }
        }
    }

> [!NOTE]
> <span data-ttu-id="6d164-190">Сделайте том конечной hello API toosubstitute hello запроса URL-адрес, полученный ранее из hello центра разработчиков Bing (же применяется toohello API-ключ).</span><span class="sxs-lookup"><span data-stu-id="6d164-190">Make sure toosubstitute hello API endpoint with hello query URL that you obtained earlier from hello Bing Dev Center (same applies toohello API key).</span></span> 
> 
> 

<span data-ttu-id="6d164-191">При наличии запроса toohello результатов, это означает, что hello заданная точка находится в пределах границы hello hello geofence, мы возвращаем `true`.</span><span class="sxs-lookup"><span data-stu-id="6d164-191">If there are results toohello query, that means that hello specified point is within hello boundaries of hello geofence, so we return `true`.</span></span> <span data-ttu-id="6d164-192">Если ничего не найдено, Bing сообщают, что точка hello находится за пределами кадра подстановки hello, так мы возвращаем `false`.</span><span class="sxs-lookup"><span data-stu-id="6d164-192">If there are no results, Bing is telling us that hello point is outside hello lookup frame, so we return `false`.</span></span>

<span data-ttu-id="6d164-193">В `NotificationsController.cs`, создать проверку прямо перед инструкцию switch hello:</span><span class="sxs-lookup"><span data-stu-id="6d164-193">Back in `NotificationsController.cs`, create a check right before hello switch statement:</span></span>

    if (ApiHelper.IsPointWithinBounds(longitude, latitude))
    {
        switch (pns.ToLower())
        {
            case "wns":
                //// Windows 8.1 / Windows Phone 8.1
                var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
                            "From " + user + ": " + message + "</text></binding></visual></toast>";
                outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

                // Windows 10 specific Action Center support
                toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
                            "From " + user + ": " + message + "</text></binding></visual></toast>";
                outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

                break;
        }
    }

<span data-ttu-id="6d164-194">Таким образом, hello уведомление отправляется только если hello точка находится в пределах границ hello.</span><span class="sxs-lookup"><span data-stu-id="6d164-194">That way, hello notification is only sent when hello point is within hello boundaries.</span></span>

## <a name="testing-push-notifications-in-hello-uwp-app"></a><span data-ttu-id="6d164-195">Тестирование push-уведомлений в приложение UWP hello</span><span class="sxs-lookup"><span data-stu-id="6d164-195">Testing push notifications in hello UWP app</span></span>
<span data-ttu-id="6d164-196">Вернемся toohello приложения UWP, мы теперь будет может tootest уведомления.</span><span class="sxs-lookup"><span data-stu-id="6d164-196">Going back toohello UWP app, we should now be able tootest notifications.</span></span> <span data-ttu-id="6d164-197">В рамках hello `LocationHelper` класса, создайте новую функцию — `SendLocationToBackend`:</span><span class="sxs-lookup"><span data-stu-id="6d164-197">Within hello `LocationHelper` class, create a new function – `SendLocationToBackend`:</span></span>

    public static async Task SendLocationToBackend(string pns, string userTag, string message, string latitude, string longitude)
    {
        var POST_URL = "http://localhost:8741/api/notifications?pns=" +
            pns + "&to_tag=" + userTag + "&latitude=" + latitude + "&longitude=" + longitude;

        using (var httpClient = new HttpClient())
        {
            try
            {
                await httpClient.PostAsync(POST_URL, new StringContent("\"" + message + "\"",
                    System.Text.Encoding.UTF8, "application/json"));
            }
            catch (Exception ex)
            {
                Debug.WriteLine(ex.Message);
            }
        }
    }

> [!NOTE]
> <span data-ttu-id="6d164-198">Поменять местами hello `POST_URL` toohello расположение развернутого веб-приложения, созданную в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="6d164-198">Swap hello `POST_URL` toohello location of your deployed web application that we created in hello previous section.</span></span> <span data-ttu-id="6d164-199">Сейчас это ОК toorun его локально, но по мере работы по развертыванию общедоступной версии, необходимо будет toohost с помощью внешнего поставщика.</span><span class="sxs-lookup"><span data-stu-id="6d164-199">For now, it’s OK toorun it locally, but as you work on deploying a public version, you will need toohost it with an external provider.</span></span>
> 
> 

<span data-ttu-id="6d164-200">Теперь убедитесь, что необходимо зарегистрировать приложение UWP hello push-уведомления.</span><span class="sxs-lookup"><span data-stu-id="6d164-200">Let’s now make sure that we register hello UWP app for push notifications.</span></span> <span data-ttu-id="6d164-201">В Visual Studio щелкнуть **проекта** > **хранения** > **связать приложение с магазином hello**.</span><span class="sxs-lookup"><span data-stu-id="6d164-201">In Visual Studio, click on **Project** > **Store** > **Associate app with hello store**.</span></span>

![](./media/notification-hubs-geofence/vs-associate-with-store.png)

<span data-ttu-id="6d164-202">После входа в учетную запись разработчика tooyour, убедитесь, что выбрать существующее приложение или создайте новый и связать с ним пакет hello.</span><span class="sxs-lookup"><span data-stu-id="6d164-202">Once you sign in tooyour developer account, make sure you select an existing app or create a new one and associate hello package with it.</span></span> 

<span data-ttu-id="6d164-203">Перейдите в центр разработчиков toohello и Привет открыть приложение, которое вы только что создали.</span><span class="sxs-lookup"><span data-stu-id="6d164-203">Go toohello Dev Center and open hello app that you just created.</span></span> <span data-ttu-id="6d164-204">Щелкните **Службы** > **Push-уведомления** > **Live Services site** (Сайт служб Live).</span><span class="sxs-lookup"><span data-stu-id="6d164-204">Click **Services** > **Push Notifications** > **Live Services site**.</span></span>

![](./media/notification-hubs-geofence/ms-live-services.png)

<span data-ttu-id="6d164-205">На сайте hello запишите hello **секрет приложения** и hello **ИД безопасности пакета**.</span><span class="sxs-lookup"><span data-stu-id="6d164-205">On hello site, take note of hello **Application Secret** and hello **Package SID**.</span></span> <span data-ttu-id="6d164-206">Вам потребуется как hello портал Azure — откройте концентратор уведомлений, щелкнув **параметры** > **служб Notification Services** > **Windows (WNS)**и заполнить hello hello необходимые поля.</span><span class="sxs-lookup"><span data-stu-id="6d164-206">You will need both in hello Azure Portal – open your notification hub, click on **Settings** > **Notification Services** > **Windows (WNS)** and enter hello information in hello required fields.</span></span>

![](./media/notification-hubs-geofence/notification-hubs-wns.png)

<span data-ttu-id="6d164-207">Щелкните **Save**(Сохранить).</span><span class="sxs-lookup"><span data-stu-id="6d164-207">Click on **Save**.</span></span>

<span data-ttu-id="6d164-208">В **обозревателе решений** щелкните правой кнопкой мыши **Ссылки** и выберите **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="6d164-208">Right click on **References** in **Solution Explorer** and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="6d164-209">Нам нужно будет tooadd toohello ссылки **Microsoft Azure Service Bus управляемой библиотеке** — просто поиск `WindowsAzure.Messaging.Managed` и добавить его в проект tooyour.</span><span class="sxs-lookup"><span data-stu-id="6d164-209">We will need tooadd a reference toohello **Microsoft Azure Service Bus managed library** – simply search for `WindowsAzure.Messaging.Managed` and add it tooyour project.</span></span>

![](./media/notification-hubs-geofence/vs-nuget.png)

<span data-ttu-id="6d164-210">В целях тестирования можно создать hello `MainPage_Loaded` обработчик событий еще раз и добавьте этот tooit фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="6d164-210">For testing purposes, we can create hello `MainPage_Loaded` event handler once again, and add this code snippet tooit:</span></span>

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    var hub = new NotificationHub("HUB_NAME", "HUB_LISTEN_CONNECTION_STRING");
    var result = await hub.RegisterNativeAsync(channel.Uri);

    // Displays hello registration ID so you know it was successful
    if (result.RegistrationId != null)
    {
        Debug.WriteLine("Reg successful.");
    }

<span data-ttu-id="6d164-211">Hello выше регистрирует приложение hello hello концентратора уведомлений.</span><span class="sxs-lookup"><span data-stu-id="6d164-211">hello above registers hello app with hello notification hub.</span></span> <span data-ttu-id="6d164-212">Вы являетесь toogo Готово!</span><span class="sxs-lookup"><span data-stu-id="6d164-212">You are ready toogo!</span></span> 

<span data-ttu-id="6d164-213">В `LocationHelper`, внутри hello `Geolocator_PositionChanged` обработчик, можно добавить фрагмент кода теста, который будет принудительно размещать hello внутри hello geofence:</span><span class="sxs-lookup"><span data-stu-id="6d164-213">In `LocationHelper`, inside hello `Geolocator_PositionChanged` handler, you can add a piece of test code that will forcefully put hello location inside hello geofence:</span></span>

    await LocationHelper.SendLocationToBackend("wns", "TEST_USER", "TEST", "37.7746", "-122.3858");

<span data-ttu-id="6d164-214">Так как мы не проходят hello реальные координаты (которые могут быть в пределах границ hello в момент hello) и используются стандартные тестовые значения, мы увидим, что уведомления отображаются на обновления:</span><span class="sxs-lookup"><span data-stu-id="6d164-214">Because we are not passing hello real coordinates (which might not be within hello boundaries at hello moment) and are using predefined test values, we will see a notification show up on update:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-test-notification.png)

## <a name="whats-next"></a><span data-ttu-id="6d164-215">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6d164-215">What’s next?</span></span>
<span data-ttu-id="6d164-216">Существует несколько шагов, которые могут потребоваться toofollow в toohello сложения выше toomake убедитесь, что решение hello рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="6d164-216">There are a couple of steps that you might need toofollow in addition toohello above toomake sure that hello solution is production-ready.</span></span>

<span data-ttu-id="6d164-217">Первое и самое главное может потребоваться tooensure, geofences являются динамическими.</span><span class="sxs-lookup"><span data-stu-id="6d164-217">First and foremost, you might need tooensure that geofences are dynamic.</span></span> <span data-ttu-id="6d164-218">Это потребует некоторой дополнительной работы с hello Bing API в порядке toobe может tooupload новые границы в hello существующего источника данных.</span><span class="sxs-lookup"><span data-stu-id="6d164-218">This will require some extra work with hello Bing API in order toobe able tooupload new boundaries within hello existing data source.</span></span> <span data-ttu-id="6d164-219">Обратитесь к hello [документация по интерфейсам API службы Bing пространственных данных](https://msdn.microsoft.com/library/ff701734.aspx) Дополнительные сведения по теме hello.</span><span class="sxs-lookup"><span data-stu-id="6d164-219">Consult hello [Bing Spatial Data Services API documentation](https://msdn.microsoft.com/library/ff701734.aspx) for more details on hello subject.</span></span>

<span data-ttu-id="6d164-220">Во-вторых, как рабочий tooensure, hello доставки выполняется toohello участию, может потребоваться tootarget их через [тегов](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="6d164-220">Second, as you are working tooensure that hello delivery is done toohello right participants, you might want tootarget them via [tagging](notification-hubs-tags-segment-push-message.md).</span></span>

<span data-ttu-id="6d164-221">решение Hello, показанный выше описывает сценарий, в котором могут иметь самые разнообразные целевых платформах, не была ограничена hello зонирование toosystem специальные возможности.</span><span class="sxs-lookup"><span data-stu-id="6d164-221">hello solution shown above describes a scenario in which you might have a wide variety of target platforms, so we did not limit hello geofencing toosystem-specific capabilities.</span></span> <span data-ttu-id="6d164-222">С другой стороны, hello универсальной платформы Windows предлагает возможности слишком[обнаружить geofences право out-of--box](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence).</span><span class="sxs-lookup"><span data-stu-id="6d164-222">That said, hello Universal Windows Platform offers capabilities too[detect geofences right out-of-the-box](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence).</span></span>

<span data-ttu-id="6d164-223">Дополнительные сведения о возможностях Центров уведомлений см. на [портале документации](https://azure.microsoft.com/documentation/services/notification-hubs/).</span><span class="sxs-lookup"><span data-stu-id="6d164-223">For more details regarding Notification Hubs capabilities, check out our [documentation portal](https://azure.microsoft.com/documentation/services/notification-hubs/).</span></span>

