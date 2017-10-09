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
# <a name="geo-fenced-push-notifications-with-azure-notification-hubs-and-bing-spatial-data"></a>Отправка push-уведомлений с определением геозон с помощью Центров уведомлений Azure и Bing Spatial Data
> [!NOTE]
> toocomplete этого учебника необходимо иметь активную учетную запись Azure. Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут. Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02).
> 
> 

В этом учебнике вы узнаете, как на основе расположения toodeliver извещающих уведомлений с концентраторами уведомлений Azure и Bing пространственными данными из будет применить в приложении универсальной платформы Windows.

## <a name="prerequisites"></a>Предварительные требования
Первое и самое главное необходимо наличие всех hello программного обеспечения и услуг предварительным toomake:

* [Visual Studio 2015 с обновлением 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) или более поздней версии (также подойдет [Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409)); 
* Последнюю версию hello [пакета Azure SDK](https://azure.microsoft.com/downloads/). 
* [учетная запись Центра разработки Карт Bing](https://www.bingmapsportal.com/) (ее можно создать бесплатно и связать с учетной записью Майкрософт). 

## <a name="getting-started"></a>Приступая к работе
Давайте начнем с создания проекта hello. В Visual Studio создайте новый проект типа **Пустое приложение (универсальное приложение Windows)**.

![](./media/notification-hubs-geofence/notification-hubs-create-blank-app.png)

После завершения создания проекта hello должны иметь hello окружение для самого приложения hello. Теперь давайте Установка всех компонентов инфраструктуры геозон hello. Так как мы toouse постоянной службами Bing для этого, есть общедоступную конечную точку REST API, мы сможем кадры tooquery конкретное расположение:

    http://spatial.virtualearth.net/REST/v1/data/

Вам потребуется toospecify hello следующие tooget параметры его работы:

* **Идентификатор источника данных** и **Имя источника данных.** В API Карт Bing источники данных содержат различные сегментированные метаданные, например о местоположении и часах работы. Дополнительные сведения об этих метаданных можно прочесть здесь. 
* **Имя сущности** — hello сущность будет toouse как опорную точку для hello уведомления. 
* **Ключ Bing Maps API** — это ключ hello, полученный ранее при создании учетной записи центра разработчиков Bing hello.

Давайте глубокое погружение в hello установки необходимо сделать для каждого из элементов hello выше.

## <a name="setting-up-hello-data-source"></a>Настройка источника данных hello
Это можно сделать в hello центра разработчиков Bing Maps. Просто щелкните **источники данных** hello навигации в верхней части панели и выберите **Управление источниками данных**.

![](./media/notification-hubs-geofence/bing-maps-manage-data.png)

Если вы не работали с API службы Bing Maps перед, скорее не будет существовать присутствует, источников данных, можно просто создать новые, щелкнув на источнике данных tooa передачи данных. Убедитесь, что заполните все необходимые hello поля:

![](./media/notification-hubs-geofence/bing-maps-create-data.png)

Может возникнуть вопрос, — что такое файл данных hello и что должно загружаете вы? В целях hello этого теста можно просто используйте образец hello основе канала вокруг области waterfront Сан-Франциско hello:

    Bing Spatial Data Services, 1.0, TestBoundaries
    EntityID(Edm.String,primaryKey)|Name(Edm.String)|Longitude(Edm.Double)|Latitude(Edm.Double)|Boundary(Edm.Geography)
    1|SanFranciscoPier|||POLYGON ((-122.389825 37.776598,-122.389438 37.773087,-122.381885 37.771849,-122.382186 37.777022,-122.389825 37.776598))

Hello выше представляет этой сущности.

![](./media/notification-hubs-geofence/bing-maps-geofence.png)

Просто скопируйте и вставьте строку hello выше в новый файл и сохраните его в виде **NotificationHubsGeofence.pipe**и его отправки в центр разработчиков Bing hello.

> [!NOTE]
> Может появиться запрос toospecify новый ключ для hello **главный ключ** , отличается от hello **ключа запроса**. Просто создайте новый ключ по hello панели мониторинга и обновления hello страницу источника данных передачи.
> 
> 

После загрузки файла данных hello потребуется toomake убедитесь, что публикуется hello источника данных. 

Go слишком**Управление источниками данных**, так же, как описано выше, определить источник данных в списке hello и щелкнуть **публикации** в hello **действия** столбца. В немного, вы увидите источника данных в hello **опубликованные источники данных** вкладки:

![](./media/notification-hubs-geofence/bing-maps-published-data.png)

При нажатии кнопки **изменить**, вам будет toosee может быстро каких расположений, мы представили в ней:

![](./media/notification-hubs-geofence/bing-maps-data-details.png)

На этом этапе портал hello не показывает hello границы для geofence hello, мы создали — все, что нам нужно является подтверждением, hello расположение, указанное в правой окружения hello.

Теперь у вас все требования к hello для источника данных hello. Щелкните tooget hello сведения о URL-адрес запроса hello для вызова hello API в центр разработчиков Bing Maps, hello **источники данных** и выберите **источника данных**.

![](./media/notification-hubs-geofence/bing-maps-data-info.png)

Hello **URL-адрес запроса** : у после нее. Это конечная точка hello, для которого можно выполнить запросы toocheck ли hello устройство в настоящий момент в пределах границ hello расположения или нет. это проверить, мы просто необходимо вызвать GET к URL-адрес запроса hello с hello следующие параметры, которые добавляются tooexecute tooperform:

    ?spatialFilter=intersects(%27POINT%20LONGITUDE%20LATITUDE)%27)&$format=json&key=QUERY_KEY

Таким образом задается целевой точки, что мы получаем от устройства hello и Bing Maps автоматически выполнит toosee вычисления hello, является ли она в hello geofence. После своего выполнения hello запроса с помощью браузера (или cURL), вы получите стандартный ответ JSON:

![](./media/notification-hubs-geofence/bing-maps-json.png)

Этот ответ происходит только в том случае, когда точка hello фактически находится в пределах указанных границ hello. Если она находится за пределами, сегмент **results** будет пустым:

![](./media/notification-hubs-geofence/bing-maps-nores.png)

## <a name="setting-up-hello-uwp-application"></a>Настройка приложения UWP hello
Теперь, когда у нас есть источник данных hello готова, мы можем запустить работаете hello приложения UWP, который мы ранее начальной загрузки.

Прежде всего для приложения необходимо включить службы обнаружения местоположения. toodo это, дважды щелкните `Package.appxmanifest` файла в **обозревателе решений**.

![](./media/notification-hubs-geofence/vs-package-manifest.png)

На вкладке Свойства hello пакета, только что открыли, нажмите кнопку **возможности** и убедитесь, что выбрана **расположение**:

![](./media/notification-hubs-geofence/vs-package-location.png)

Как объявлена возможность расположение hello, создайте новую папку с именем решения `Core`и добавьте новый файл в нем вызывается `LocationHelper.cs`:

![](./media/notification-hubs-geofence/vs-location-helper.png)

Hello `LocationHelper` самого класса на этом этапе производится достаточно просто — он осуществляет разрешить нам местонахождения пользователя hello tooobtain через API-Интерфейсу системы hello:

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

Можно прочитать дополнительные сведения о получении hello расположения пользователя в приложениях UWP в официальное hello [документе MSDN](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx).

toocheck, приобретения расположение hello фактически работает, откройте стороне кода hello главной странице (`MainPage.xaml.cs`). Создает новый обработчик событий для hello `Loaded` события в hello `MainPage` конструктор:

    public MainPage()
    {
        this.InitializeComponent();
        this.Loaded += MainPage_Loaded;
    }

Реализация обработчика событий hello Hello выглядит следующим образом:

    private async void MainPage_Loaded(object sender, RoutedEventArgs e)
    {
        var location = await LocationHelper.GetCurrentLocation();

        if (location != null)
        {
            Debug.WriteLine(string.Concat(location.Coordinate.Longitude,
                " ", location.Coordinate.Latitude));
        }
    }

Обратите внимание, что мы объявить обработчик hello асинхронным поскольку `GetCurrentLocation` типа awaitable и поэтому требует toobe, выполняются в контексте async. Кроме того так как при определенных обстоятельствах мы может оказаться, что с пустым местом (hello расположение службы отключены или приложения hello запрещен расположение tooaccess разрешения), нам нужно убедиться, что правильно обрабатываются с помощью проверки null toomake.

Запустите приложение hello. Обязательно разрешите доступ к местоположению:

![](./media/notification-hubs-geofence/notification-hubs-location-access.png)

Один раз Здравствуйте запускает приложение, должен быть координаты hello может toosee hello **вывода** окна:

![](./media/notification-hubs-geofence/notification-hubs-location-output.png)

Теперь вы знаете, что works приобретения расположение — вид обработчик событий теста hello свободного tooremove Loaded так, как мы не будет использоваться его больше.

Hello следующим шагом будет изменение места toocapture. Для этого, давайте рассмотрим задней toohello `LocationHelper` и добавьте обработчик событий hello `PositionChanged`:

    geolocator.PositionChanged += Geolocator_PositionChanged;

Реализация Hello покажет координаты местоположения hello hello **вывода** окна:

    private static async void Geolocator_PositionChanged(Geolocator sender, PositionChangedEventArgs args)
    {
        await CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
        {
            Debug.WriteLine(string.Concat(args.Position.Coordinate.Longitude, " ", args.Position.Coordinate.Latitude));
        });
    }

## <a name="setting-up-hello-backend"></a>Настройка внутреннего hello
Загрузите hello [образец серверной части .NET из GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers). После завершения загрузки Привет открыть hello `NotifyUsers` папки, а затем — hello `NotifyUsers.sln` файла.

Набор hello `AppBackend` проект как hello **запускаемый проект** и запустить его.

![](./media/notification-hubs-geofence/vs-startup-project.png)

Hello проекта, уже настроенные toosend принудительной уведомления tootarget устройства, поэтому нам нужно только две вещи toodo — выгрузить hello правильной строки подключения для концентратора уведомлений hello и добавить toosend hello идентификации границ уведомление, только если hello пользователь входит в hello geofence.

Строка подключения hello tooconfigure в hello `Models` откройте папку `Notifications.cs`. Hello `NotificationHubClient.CreateClientFromConnectionString` функция должна содержать hello сведения о концентраторе уведомлений, которые можно получить в hello [портала Azure](https://portal.azure.com) (обзора hello **политики доступа** колонки в  **Параметры**). Сохраните файл обновленной конфигурации hello.

Теперь нужно toocreate модели для hello результат API службы Bing Maps. Здравствуйте, наиболее простым способом toodo, щелкните правой кнопкой мыши на hello `Models` папке **добавить** > **класса**. Назовите его `GeofenceBoundary.cs`. После завершения копирования hello JSON из ответа hello API, которое мы обсуждали в первом разделе hello и Visual Studio используется **изменить** > **Специальная вставка** > **вставить JSON как классы**. 

Таким образом, мы обеспечиваем hello объекта будут десериализованы точно так, как предполагалось. Итоговый набор классов должен выглядеть следующим образом:

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

Затем откройте `Controllers` > `NotificationsController.cs`. Нужно tootweak hello Post вызов tooaccount для hello целевой широты и долготы. Для этого просто добавьте сигнатуру функции toohello две строки — `latitude` и `longitude`.

    public async Task<HttpResponseMessage> Post(string pns, [FromBody]string message, string to_tag, string latitude, string longitude)

Создайте новый класс в проект с именем hello `ApiHelper.cs` — мы будем использовать tooconnect tooBing toocheck точки границы пересечения. Выполните функцию `IsPointWithinBounds` следующим образом.

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
> Сделайте том конечной hello API toosubstitute hello запроса URL-адрес, полученный ранее из hello центра разработчиков Bing (же применяется toohello API-ключ). 
> 
> 

При наличии запроса toohello результатов, это означает, что hello заданная точка находится в пределах границы hello hello geofence, мы возвращаем `true`. Если ничего не найдено, Bing сообщают, что точка hello находится за пределами кадра подстановки hello, так мы возвращаем `false`.

В `NotificationsController.cs`, создать проверку прямо перед инструкцию switch hello:

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

Таким образом, hello уведомление отправляется только если hello точка находится в пределах границ hello.

## <a name="testing-push-notifications-in-hello-uwp-app"></a>Тестирование push-уведомлений в приложение UWP hello
Вернемся toohello приложения UWP, мы теперь будет может tootest уведомления. В рамках hello `LocationHelper` класса, создайте новую функцию — `SendLocationToBackend`:

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
> Поменять местами hello `POST_URL` toohello расположение развернутого веб-приложения, созданную в предыдущем разделе hello. Сейчас это ОК toorun его локально, но по мере работы по развертыванию общедоступной версии, необходимо будет toohost с помощью внешнего поставщика.
> 
> 

Теперь убедитесь, что необходимо зарегистрировать приложение UWP hello push-уведомления. В Visual Studio щелкнуть **проекта** > **хранения** > **связать приложение с магазином hello**.

![](./media/notification-hubs-geofence/vs-associate-with-store.png)

После входа в учетную запись разработчика tooyour, убедитесь, что выбрать существующее приложение или создайте новый и связать с ним пакет hello. 

Перейдите в центр разработчиков toohello и Привет открыть приложение, которое вы только что создали. Щелкните **Службы** > **Push-уведомления** > **Live Services site** (Сайт служб Live).

![](./media/notification-hubs-geofence/ms-live-services.png)

На сайте hello запишите hello **секрет приложения** и hello **ИД безопасности пакета**. Вам потребуется как hello портал Azure — откройте концентратор уведомлений, щелкнув **параметры** > **служб Notification Services** > **Windows (WNS)**и заполнить hello hello необходимые поля.

![](./media/notification-hubs-geofence/notification-hubs-wns.png)

Щелкните **Save**(Сохранить).

В **обозревателе решений** щелкните правой кнопкой мыши **Ссылки** и выберите **Управление пакетами NuGet**. Нам нужно будет tooadd toohello ссылки **Microsoft Azure Service Bus управляемой библиотеке** — просто поиск `WindowsAzure.Messaging.Managed` и добавить его в проект tooyour.

![](./media/notification-hubs-geofence/vs-nuget.png)

В целях тестирования можно создать hello `MainPage_Loaded` обработчик событий еще раз и добавьте этот tooit фрагмент кода:

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    var hub = new NotificationHub("HUB_NAME", "HUB_LISTEN_CONNECTION_STRING");
    var result = await hub.RegisterNativeAsync(channel.Uri);

    // Displays hello registration ID so you know it was successful
    if (result.RegistrationId != null)
    {
        Debug.WriteLine("Reg successful.");
    }

Hello выше регистрирует приложение hello hello концентратора уведомлений. Вы являетесь toogo Готово! 

В `LocationHelper`, внутри hello `Geolocator_PositionChanged` обработчик, можно добавить фрагмент кода теста, который будет принудительно размещать hello внутри hello geofence:

    await LocationHelper.SendLocationToBackend("wns", "TEST_USER", "TEST", "37.7746", "-122.3858");

Так как мы не проходят hello реальные координаты (которые могут быть в пределах границ hello в момент hello) и используются стандартные тестовые значения, мы увидим, что уведомления отображаются на обновления:

![](./media/notification-hubs-geofence/notification-hubs-test-notification.png)

## <a name="whats-next"></a>Дальнейшие действия
Существует несколько шагов, которые могут потребоваться toofollow в toohello сложения выше toomake убедитесь, что решение hello рабочей среде.

Первое и самое главное может потребоваться tooensure, geofences являются динамическими. Это потребует некоторой дополнительной работы с hello Bing API в порядке toobe может tooupload новые границы в hello существующего источника данных. Обратитесь к hello [документация по интерфейсам API службы Bing пространственных данных](https://msdn.microsoft.com/library/ff701734.aspx) Дополнительные сведения по теме hello.

Во-вторых, как рабочий tooensure, hello доставки выполняется toohello участию, может потребоваться tootarget их через [тегов](notification-hubs-tags-segment-push-message.md).

решение Hello, показанный выше описывает сценарий, в котором могут иметь самые разнообразные целевых платформах, не была ограничена hello зонирование toosystem специальные возможности. С другой стороны, hello универсальной платформы Windows предлагает возможности слишком[обнаружить geofences право out-of--box](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence).

Дополнительные сведения о возможностях Центров уведомлений см. на [портале документации](https://azure.microsoft.com/documentation/services/notification-hubs/).

