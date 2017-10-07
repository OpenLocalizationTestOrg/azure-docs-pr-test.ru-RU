---
title: "aaaRegistration управления"
description: "В этом разделе объясняется, как tooregister устройствами с помощью концентраторов уведомлений в порядке tooreceive push-уведомления."
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: fd0ee230-132c-4143-b4f9-65cef7f463a1
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 76471a45c7a0da1614ceed82b73cdb3319979ff7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="registration-management"></a>Управление регистрацией
## <a name="overview"></a>Обзор
В этом разделе объясняется, как tooregister устройствами с помощью концентраторов уведомлений в порядке tooreceive push-уведомления. Hello раздел описывает регистраций на высоком уровне, а затем предоставляет hello двух основных шаблоны для регистрации устройств: регистрация устройства hello непосредственно toohello концентратора уведомлений и регистрация через внутренняя служба приложения. 

## <a name="what-is-device-registration"></a>Регистрация устройств
Регистрация устройств в центре уведомлений осуществляется через **регистрацию** или **установку**.

#### <a name="registrations"></a>Регистрация
Регистрация связывает дескриптор службы уведомлений платформы (PNS) для устройств с тегами и, возможно, шаблон приветствия. Hello дескриптора PNS может быть ChannelURI, маркер устройства или идентификатор регистрации GCM. Теги, используемые tooroute уведомления toohello правильный набор дескрипторов устройства. Дополнительные сведения см. в статье [Маршрутизация и выражения тегов](notification-hubs-tags-segment-push-message.md). Шаблоны — это преобразование используется tooimplement-регистрации. Дополнительные сведения см. в статье [Шаблоны](notification-hubs-templates-cross-platform-push-messages.md).

#### <a name="installations"></a>Установка
Установка — это расширенная регистрация, включающая набор свойств, связанных с push-уведомлениями. Это hello последние и лучший подход tooregistering устройств. Однако в настоящее время он не поддерживается пакетом SDK .NET на стороне клиента ([пакетом SDK концентратора уведомлений для серверных операций](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)).  Это означает, что при регистрации из hello клиентское устройство будет иметь toouse hello [API REST концентраторов уведомлений](https://msdn.microsoft.com/library/mt621153.aspx) подход toosupport установок. При использовании серверной службы, необходимо будет toouse [SDK концентратора уведомления для внутренних операций](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).

Hello ниже приведены некоторые ключевые преимущества toousing установки.

* Создание или обновление установки является полностью идемпотентной операцией. Поэтому его можно повторять, не заботясь о дублирующихся регистрациях.
* модель установки Hello позволяет легко toodo отдельных Push-уведомлений - предназначенные для конкретного устройства. В каждую регистрацию через установку автоматически добавляется системный тег **"$InstallationId:[installationId]"** . Поэтому вы можете вызвать tootarget тега toothis отправки конкретного устройства без необходимости toodo дополнительное программирование.
* С помощью установки также позволяет вам toodo регистрации частичного обновления. Hello частичное обновление установки запрашивается с помощью метода PATCH, с помощью hello [стандарт JSON-Patch](https://tools.ietf.org/html/rfc6902). Это особенно полезно при необходимости теги tooupdate hello при регистрации. Нет toopull работу всего регистрации hello и затем повторно отправьте все предыдущие теги hello.

Установка может содержать следующие свойства hello hello. Полный список см. свойства установки hello, [создавать или перезаписывать установки с помощью REST API](https://msdn.microsoft.com/library/azure/mt621153.aspx) или [свойства установки](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx) для hello.

    // Example installation format tooshow some supported properties
    {
        installationId: "",
        expirationTime: "",
        tags: [],
        platform: "",
        pushChannel: "",
        ………
        templates: {
            "templateName1" : {
                body: "",
                tags: [] },
            "templateName2" : {
                body: "",
                // Headers are for Windows Store only
                headers: {
                    "X-WNS-Type": "wns/tile" }
                tags: [] }
        },
        secondaryTiles: {
            "tileId1": {
                pushChannel: "",
                tags: [],
                templates: {
                    "otherTemplate": {
                        bodyTemplate: "",
                        headers: {
                            ... }
                        tags: [] }
                }
            }
        }
    }



Это важные toonote, регистрации и установки по умолчанию больше не истекает.

Регистрации и установки должны содержать действительный дескриптор PNS для каждого устройства или канала. Поскольку дескрипторов PNS может быть получен только в клиентском приложении на устройстве hello, одним из шаблонов является tooregister непосредственно на этом устройстве hello клиентского приложения. На hello другие руки, вопросы безопасности и бизнес-логики, касающиеся tootags может потребоваться toomanage регистрацию устройств в серверной части приложения hello. 

#### <a name="templates"></a>Шаблоны
Если требуется, чтобы toouse [шаблоны](notification-hubs-templates-cross-platform-push-messages.md), установка устройства hello также содержать все шаблоны, связанные с устройством в JSON (см. пример выше). Hello имена шаблонов направить различные шаблоны для hello одного устройства.

Обратите внимание, что имя каждого шаблона соответствует tooa тела шаблона и дополнительный набор тегов. Кроме того, каждая платформа может иметь дополнительные свойства шаблонов. Для магазина Windows (с помощью WNS) и Windows Phone 8 (с помощью MPNS) дополнительный набор заголовков, может быть частью шаблона hello. В случае hello APN tooeither свойство срока действия можно задать выражение константы или tooa шаблона. Полный список см. свойства установки hello, [создавать или перезаписывать установки с ОСТАЛЬНОЙ](https://msdn.microsoft.com/library/azure/mt621153.aspx) раздела.

#### <a name="secondary-tiles-for-windows-store-apps"></a>Вспомогательные плитки для приложений из Магазина Windows
Для клиентских приложений для магазина Windows отправку уведомлений — toosecondary плитки hello же, как отправлять им toohello первичной. Это также поддерживается в установках. Обратите внимание, что вторичной плитки различных ChannelUri, какие hello SDK на клиентское приложение обрабатывает прозрачно.

использует словарь SecondaryTiles Hello hello же TileId, используемые toocreate hello SecondaryTiles объекта в приложении магазина Windows.
Как и с hello основной ChannelUri, идентификаторы Channeluri получателей плиток можно изменить в любой момент. В порядке tookeep hello установок в концентратор уведомлений hello обновлен hello устройства необходимо обновить их с hello текущего идентификаторов Channeluri hello получателей плиток.

## <a name="registration-management-from-hello-device"></a>Управление регистрацией с устройства hello
При управлении регистрацию устройств из клиентских приложений, сервер hello только отвечает за отправку уведомлений. Клиентские приложения сохранить дескрипторов PNS копирование toodate и зарегистрируйте тегов. Hello следующий рисунок иллюстрирует этот шаблон.

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-device.png)

устройство Hello сначала получает приветствия PNS обработки из hello PNS, а затем регистрирует напрямую с концентратором уведомлений hello. После успешной регистрации hello внутреннего сервера приложения hello можно отправить уведомление, предназначенных для этой регистрации. Дополнительные сведения о том, как уведомления toosend разделе [маршрутизации и выражения с тегами](notification-hubs-tags-segment-push-message.md).
Обратите внимание, что в этом случае используется только для прослушивания tooaccess права концентраторов уведомлений с устройства hello. Дополнительные сведения см. в статье [Безопасность](notification-hubs-push-notification-security.md).

Регистрация устройства hello hello проще, но имеет некоторые недостатки.
Hello первый недостатком является то, что клиентского приложения можно обновить только его теги при активном приложение hello. Например если пользователь имеет два устройства, которые регистрируют теги связанные toosport команд, при регистрации первого устройства hello для дополнительных тега (например, Seahawks), второе устройство hello не будут получать hello уведомления о hello Seahawks до приложение hello на hello Второе устройство выполняется еще раз. В общем случае если теги влияют на нескольких устройствах, управление теги из внутреннего hello является предпочтительным решением.
второй недостаток Hello управления регистрацией из клиентского приложения hello —, так как приложения могут быть объектом вредоносной атаки, защита регистрации hello теги toospecific требует особой осторожности как описано в разделе hello «безопасность на уровне тег».

#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-an-installation"></a>Пример кода tooregister с концентратором уведомлений с использованием установки устройства
В настоящее время поддерживается только с помощью hello [API REST концентраторов уведомлений](https://msdn.microsoft.com/library/mt621153.aspx).

Можно также использовать метод PATCH hello, с помощью hello [стандарт JSON-Patch](https://tools.ietf.org/html/rfc6902) обновления установки hello.

    class DeviceInstallation
    {
        public string installationId { get; set; }
        public string platform { get; set; }
        public string pushChannel { get; set; }
        public string[] tags { get; set; }
    }

    private async Task<HttpStatusCode> CreateOrUpdateInstallationAsync(DeviceInstallation deviceInstallation,
         string hubName, string listenConnectionString)
    {
        if (deviceInstallation.installationId == null)
            return HttpStatusCode.BadRequest;

        // Parse connection string (https://msdn.microsoft.com/library/azure/dn495627.aspx)
        ConnectionStringUtility connectionSaSUtil = new ConnectionStringUtility(listenConnectionString);
        string hubResource = "installations/" + deviceInstallation.installationId + "?";
        string apiVersion = "api-version=2015-04";

        // Determine hello targetUri that we will sign
        string uri = connectionSaSUtil.Endpoint + hubName + "/" + hubResource + apiVersion;

        //=== Generate SaS Security Token for Authorization header ===
        // See, https://msdn.microsoft.com/library/azure/dn495627.aspx
        string SasToken = connectionSaSUtil.getSaSToken(uri, 60);

        using (var httpClient = new HttpClient())
        {
            string json = JsonConvert.SerializeObject(deviceInstallation);

            httpClient.DefaultRequestHeaders.Add("Authorization", SasToken);

            var response = await httpClient.PutAsync(uri, new StringContent(json, System.Text.Encoding.UTF8, "application/json"));
            return response.StatusCode;
        }
    }

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    string installationId = null;
    var settings = ApplicationData.Current.LocalSettings.Values;

    // If we have not stored a installation id in application data, create and store as application data.
    if (!settings.ContainsKey("__NHInstallationId"))
    {
        installationId = Guid.NewGuid().ToString();
        settings.Add("__NHInstallationId", installationId);
    }

    installationId = (string)settings["__NHInstallationId"];

    var deviceInstallation = new DeviceInstallation
    {
        installationId = installationId,
        platform = "wns",
        pushChannel = channel.Uri,
        //tags = tags.ToArray<string>()
    };

    var statusCode = await CreateOrUpdateInstallationAsync(deviceInstallation, 
                        "<HUBNAME>", "<SHARED LISTEN CONNECTION STRING>");

    if (statusCode != HttpStatusCode.Accepted)
    {
        var dialog = new MessageDialog(statusCode.ToString(), "Registration failed. Installation Id : " + installationId);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
    else
    {
        var dialog = new MessageDialog("Registration successful using installation Id : " + installationId);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }



#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-a-registration"></a>Пример кода tooregister с концентратором уведомлений на устройстве с регистрацией
Эти методы, создание или обновление регистрации для hello устройства, на котором они вызываются. Это означает, что в порядке tooupdate hello дескриптор или hello тегов, переписывает всю регистрации hello. Помните, что регистраций являются временными, поэтому следует всегда иметь надежного хранилища с тегами текущего hello, необходимые для конкретного устройства.

    // Initialize hello Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // hello Device id from hello PNS
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // If you are registering from hello client itself, then store this registration id in device
    // storage. Then when hello app starts, you can check if a registration id already exists or not before
    // creating.
    var settings = ApplicationData.Current.LocalSettings.Values;

    // If we have not stored a registration id in application data, store in application data.
    if (!settings.ContainsKey("__NHRegistrationId"))
    {
        // make sure there are no existing registrations for this push handle (used for iOS and Android)    
        string newRegistrationId = null;
        var registrations = await hub.GetRegistrationsByChannelAsync(pushChannel.Uri, 100);
        foreach (RegistrationDescription registration in registrations)
        {
            if (newRegistrationId == null)
            {
                newRegistrationId = registration.RegistrationId;
            }
            else
            {
                await hub.DeleteRegistrationAsync(registration);
            }
        }

        newRegistrationId = await hub.CreateRegistrationIdAsync();

        settings.Add("__NHRegistrationId", newRegistrationId);
    }

    string regId = (string)settings["__NHRegistrationId"];

    RegistrationDescription registration = new WindowsRegistrationDescription(pushChannel.Uri);
    registration.RegistrationId = regId;
    registration.Tags = new HashSet<string>(YourTags);

    try
    {
        await hub.CreateOrUpdateRegistrationAsync(registration);
    }
    catch (Microsoft.WindowsAzure.Messaging.RegistrationGoneException e)
    {
        settings.Remove("__NHRegistrationId");
    }


## <a name="registration-management-from-a-backend"></a>Управление регистрацией из серверной части
Управление регистраций из внутреннего hello требуется написать дополнительный код. приложение Hello hello устройства необходимо предоставить hello обновленные серверной toohello дескриптора PNS, каждый раз при запуске приложение hello (вместе с тегами и шаблонов), и серверной hello необходимо обновить этот дескриптор в концентраторе уведомлений hello. Hello следующий рисунок иллюстрирует этот проект.

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-backend.png)

Hello управление регистраций из внутреннего hello преимущества теги hello возможности toomodify tooregistrations даже в том случае, если соответствующие приложение hello на устройстве hello неактивна и клиентское приложение hello tooauthenticate перед добавлением регистрации tooits тег.

#### <a name="example-code-tooregister-with-a-notification-hub-from-a-backend-using-an-installation"></a>Пример кода tooregister с концентратором уведомлений из базы данных, с помощью установки
как и раньше Hello клиентского устройства по-прежнему возвращает его дескриптора PNS и установки соответствующих свойств и вызывает пользовательский API hello серверную часть, могут выполнить регистрацию hello и авторизацию теги серверной hello и т.д. можно воспользоваться hello [SDK концентратора уведомлений внутренних операций](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).

Можно также использовать метод PATCH hello, с помощью hello [стандарт JSON-Patch](https://tools.ietf.org/html/rfc6902) обновления установки hello.

    // Initialize hello Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // Custom API on hello backend
    public async Task<HttpResponseMessage> Put(DeviceInstallation deviceUpdate)
    {

        Installation installation = new Installation();
        installation.InstallationId = deviceUpdate.InstallationId;
        installation.PushChannel = deviceUpdate.Handle;
        installation.Tags = deviceUpdate.Tags;

        switch (deviceUpdate.Platform)
        {
            case "mpns":
                installation.Platform = NotificationPlatform.Mpns;
                break;
            case "wns":
                installation.Platform = NotificationPlatform.Wns;
                break;
            case "apns":
                installation.Platform = NotificationPlatform.Apns;
                break;
            case "gcm":
                installation.Platform = NotificationPlatform.Gcm;
                break;
            default:
                throw new HttpResponseException(HttpStatusCode.BadRequest);
        }


        // In hello backend we can control if a user is allowed tooadd tags
        //installation.Tags = new List<string>(deviceUpdate.Tags);
        //installation.Tags.Add("username:" + username);

        await hub.CreateOrUpdateInstallationAsync(installation);

        return Request.CreateResponse(HttpStatusCode.OK);
    }


#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-a-registration-id"></a>Пример кода tooregister с концентратором уведомлений на устройстве с код регистрации
Из серверной части приложения с регистрациями можно выполнять основные операции CRUDS. Например:

    var hub = NotificationHubClient.CreateClientFromConnectionString("{connectionString}", "hubName");

    // create a registration description object of hello correct type, e.g.
    var reg = new WindowsRegistrationDescription(channelUri, tags);

    // Create
    await hub.CreateRegistrationAsync(reg);

    // Get by id
    var r = await hub.GetRegistrationAsync<RegistrationDescription>("id");

    // update
    r.Tags.Add("myTag");

    // update on hub
    await hub.UpdateRegistrationAsync(r);

    // delete
    await hub.DeleteRegistrationAsync(r);


Серверная часть Hello должен обрабатывать параллелизма между обновлениями регистрации. Служебная шина предоставляет управление оптимистичным параллелизмом для управления регистрациями. На уровне hello HTTP это реализуется с использованием hello ETag на операции управления регистрации. Эта функция автоматически используется в пакетах Microsoft SDK, которые выдают исключение, если обновление отклоняется по причинам параллелизма. внутреннего сервера приложения Hello отвечает за обработку этих исключений и повторная попытка обновления hello, при необходимости.

