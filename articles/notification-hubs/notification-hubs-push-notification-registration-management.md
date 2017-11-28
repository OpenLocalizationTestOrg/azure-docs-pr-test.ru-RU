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
# <a name="registration-management"></a><span data-ttu-id="53cb1-103">Управление регистрацией</span><span class="sxs-lookup"><span data-stu-id="53cb1-103">Registration management</span></span>
## <a name="overview"></a><span data-ttu-id="53cb1-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="53cb1-104">Overview</span></span>
<span data-ttu-id="53cb1-105">В этом разделе объясняется, как tooregister устройствами с помощью концентраторов уведомлений в порядке tooreceive push-уведомления.</span><span class="sxs-lookup"><span data-stu-id="53cb1-105">This topic explains how tooregister devices with notification hubs in order tooreceive push notifications.</span></span> <span data-ttu-id="53cb1-106">Hello раздел описывает регистраций на высоком уровне, а затем предоставляет hello двух основных шаблоны для регистрации устройств: регистрация устройства hello непосредственно toohello концентратора уведомлений и регистрация через внутренняя служба приложения.</span><span class="sxs-lookup"><span data-stu-id="53cb1-106">hello topic describes registrations at a high level, then introduces hello two main patterns for registering devices: registering from hello device directly toohello notification hub, and registering through an application backend.</span></span> 

## <a name="what-is-device-registration"></a><span data-ttu-id="53cb1-107">Регистрация устройств</span><span class="sxs-lookup"><span data-stu-id="53cb1-107">What is device registration</span></span>
<span data-ttu-id="53cb1-108">Регистрация устройств в центре уведомлений осуществляется через **регистрацию** или **установку**.</span><span class="sxs-lookup"><span data-stu-id="53cb1-108">Device registration with a Notification Hub is accomplished using a **Registration** or **Installation**.</span></span>

#### <a name="registrations"></a><span data-ttu-id="53cb1-109">Регистрация</span><span class="sxs-lookup"><span data-stu-id="53cb1-109">Registrations</span></span>
<span data-ttu-id="53cb1-110">Регистрация связывает дескриптор службы уведомлений платформы (PNS) для устройств с тегами и, возможно, шаблон приветствия.</span><span class="sxs-lookup"><span data-stu-id="53cb1-110">A registration associates hello Platform Notification Service (PNS) handle for a device with tags and possibly a template.</span></span> <span data-ttu-id="53cb1-111">Hello дескриптора PNS может быть ChannelURI, маркер устройства или идентификатор регистрации GCM. Теги, используемые tooroute уведомления toohello правильный набор дескрипторов устройства.</span><span class="sxs-lookup"><span data-stu-id="53cb1-111">hello PNS handle could be a ChannelURI, device token, or GCM registration id. Tags are used tooroute notifications toohello correct set of device handles.</span></span> <span data-ttu-id="53cb1-112">Дополнительные сведения см. в статье [Маршрутизация и выражения тегов](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="53cb1-112">For more information, see [Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span> <span data-ttu-id="53cb1-113">Шаблоны — это преобразование используется tooimplement-регистрации.</span><span class="sxs-lookup"><span data-stu-id="53cb1-113">Templates are used tooimplement per-registration transformation.</span></span> <span data-ttu-id="53cb1-114">Дополнительные сведения см. в статье [Шаблоны](notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="53cb1-114">For more information, see [Templates](notification-hubs-templates-cross-platform-push-messages.md).</span></span>

#### <a name="installations"></a><span data-ttu-id="53cb1-115">Установка</span><span class="sxs-lookup"><span data-stu-id="53cb1-115">Installations</span></span>
<span data-ttu-id="53cb1-116">Установка — это расширенная регистрация, включающая набор свойств, связанных с push-уведомлениями.</span><span class="sxs-lookup"><span data-stu-id="53cb1-116">An Installation is an enhanced registration that includes a bag of push related properties.</span></span> <span data-ttu-id="53cb1-117">Это hello последние и лучший подход tooregistering устройств.</span><span class="sxs-lookup"><span data-stu-id="53cb1-117">It is hello latest and best approach tooregistering your devices.</span></span> <span data-ttu-id="53cb1-118">Однако в настоящее время он не поддерживается пакетом SDK .NET на стороне клиента ([пакетом SDK концентратора уведомлений для серверных операций](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)).</span><span class="sxs-lookup"><span data-stu-id="53cb1-118">However, it is not supported by client side .NET SDK ([Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)) as of yet.</span></span>  <span data-ttu-id="53cb1-119">Это означает, что при регистрации из hello клиентское устройство будет иметь toouse hello [API REST концентраторов уведомлений](https://msdn.microsoft.com/library/mt621153.aspx) подход toosupport установок.</span><span class="sxs-lookup"><span data-stu-id="53cb1-119">This means if you are registering from hello client device itself, you would have toouse hello [Notification Hubs REST API](https://msdn.microsoft.com/library/mt621153.aspx) approach toosupport installations.</span></span> <span data-ttu-id="53cb1-120">При использовании серверной службы, необходимо будет toouse [SDK концентратора уведомления для внутренних операций](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="53cb1-120">If you are using a backend service, you should be able toouse [Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="53cb1-121">Hello ниже приведены некоторые ключевые преимущества toousing установки.</span><span class="sxs-lookup"><span data-stu-id="53cb1-121">hello following are some key advantages toousing installations:</span></span>

* <span data-ttu-id="53cb1-122">Создание или обновление установки является полностью идемпотентной операцией.</span><span class="sxs-lookup"><span data-stu-id="53cb1-122">Creating or updating an installation is fully idempotent.</span></span> <span data-ttu-id="53cb1-123">Поэтому его можно повторять, не заботясь о дублирующихся регистрациях.</span><span class="sxs-lookup"><span data-stu-id="53cb1-123">So you can retry it without any concerns about duplicate registrations.</span></span>
* <span data-ttu-id="53cb1-124">модель установки Hello позволяет легко toodo отдельных Push-уведомлений - предназначенные для конкретного устройства.</span><span class="sxs-lookup"><span data-stu-id="53cb1-124">hello installation model makes it easy toodo individual pushes - targeting specific device.</span></span> <span data-ttu-id="53cb1-125">В каждую регистрацию через установку автоматически добавляется системный тег **"$InstallationId:[installationId]"** .</span><span class="sxs-lookup"><span data-stu-id="53cb1-125">A system tag **"$InstallationId:[installationId]"** is automatically added with each installation based registration.</span></span> <span data-ttu-id="53cb1-126">Поэтому вы можете вызвать tootarget тега toothis отправки конкретного устройства без необходимости toodo дополнительное программирование.</span><span class="sxs-lookup"><span data-stu-id="53cb1-126">So you can call a send toothis tag tootarget a specific device without having toodo any additional coding.</span></span>
* <span data-ttu-id="53cb1-127">С помощью установки также позволяет вам toodo регистрации частичного обновления.</span><span class="sxs-lookup"><span data-stu-id="53cb1-127">Using installations also enables you toodo partial registration updates.</span></span> <span data-ttu-id="53cb1-128">Hello частичное обновление установки запрашивается с помощью метода PATCH, с помощью hello [стандарт JSON-Patch](https://tools.ietf.org/html/rfc6902).</span><span class="sxs-lookup"><span data-stu-id="53cb1-128">hello partial update of an installation is requested with a PATCH method using hello [JSON-Patch standard](https://tools.ietf.org/html/rfc6902).</span></span> <span data-ttu-id="53cb1-129">Это особенно полезно при необходимости теги tooupdate hello при регистрации.</span><span class="sxs-lookup"><span data-stu-id="53cb1-129">This is particularly useful when you want tooupdate tags on hello registration.</span></span> <span data-ttu-id="53cb1-130">Нет toopull работу всего регистрации hello и затем повторно отправьте все предыдущие теги hello.</span><span class="sxs-lookup"><span data-stu-id="53cb1-130">You don't have toopull down hello entire registration and then resend all hello previous tags again.</span></span>

<span data-ttu-id="53cb1-131">Установка может содержать следующие свойства hello hello.</span><span class="sxs-lookup"><span data-stu-id="53cb1-131">An installation can contain hello hello following properties.</span></span> <span data-ttu-id="53cb1-132">Полный список см. свойства установки hello, [создавать или перезаписывать установки с помощью REST API](https://msdn.microsoft.com/library/azure/mt621153.aspx) или [свойства установки](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx) для hello.</span><span class="sxs-lookup"><span data-stu-id="53cb1-132">For a complete listing of hello installation properties see, [Create or Overwrite an Installation with REST API](https://msdn.microsoft.com/library/azure/mt621153.aspx) or [Installation Properties](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx) for hello .</span></span>

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



<span data-ttu-id="53cb1-133">Это важные toonote, регистрации и установки по умолчанию больше не истекает.</span><span class="sxs-lookup"><span data-stu-id="53cb1-133">It is important toonote that registrations and installations by default no longer expire.</span></span>

<span data-ttu-id="53cb1-134">Регистрации и установки должны содержать действительный дескриптор PNS для каждого устройства или канала.</span><span class="sxs-lookup"><span data-stu-id="53cb1-134">Registrations and installations must contain a valid PNS handle for each device/channel.</span></span> <span data-ttu-id="53cb1-135">Поскольку дескрипторов PNS может быть получен только в клиентском приложении на устройстве hello, одним из шаблонов является tooregister непосредственно на этом устройстве hello клиентского приложения.</span><span class="sxs-lookup"><span data-stu-id="53cb1-135">Because PNS handles can only be obtained in a client app on hello device, one pattern is tooregister directly on that device with hello client app.</span></span> <span data-ttu-id="53cb1-136">На hello другие руки, вопросы безопасности и бизнес-логики, касающиеся tootags может потребоваться toomanage регистрацию устройств в серверной части приложения hello.</span><span class="sxs-lookup"><span data-stu-id="53cb1-136">On hello other hand, security considerations and business logic related tootags might require you toomanage device registration in hello app back-end.</span></span> 

#### <a name="templates"></a><span data-ttu-id="53cb1-137">Шаблоны</span><span class="sxs-lookup"><span data-stu-id="53cb1-137">Templates</span></span>
<span data-ttu-id="53cb1-138">Если требуется, чтобы toouse [шаблоны](notification-hubs-templates-cross-platform-push-messages.md), установка устройства hello также содержать все шаблоны, связанные с устройством в JSON (см. пример выше).</span><span class="sxs-lookup"><span data-stu-id="53cb1-138">If you want toouse [Templates](notification-hubs-templates-cross-platform-push-messages.md), hello device installation also hold all templates associated with that device in a JSON format (see sample above).</span></span> <span data-ttu-id="53cb1-139">Hello имена шаблонов направить различные шаблоны для hello одного устройства.</span><span class="sxs-lookup"><span data-stu-id="53cb1-139">hello template names help target different templates for hello same device.</span></span>

<span data-ttu-id="53cb1-140">Обратите внимание, что имя каждого шаблона соответствует tooa тела шаблона и дополнительный набор тегов.</span><span class="sxs-lookup"><span data-stu-id="53cb1-140">Note that each template name maps tooa template body and an optional set of tags.</span></span> <span data-ttu-id="53cb1-141">Кроме того, каждая платформа может иметь дополнительные свойства шаблонов.</span><span class="sxs-lookup"><span data-stu-id="53cb1-141">Moreover, each platform can have additional template properties.</span></span> <span data-ttu-id="53cb1-142">Для магазина Windows (с помощью WNS) и Windows Phone 8 (с помощью MPNS) дополнительный набор заголовков, может быть частью шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="53cb1-142">For Windows Store (using WNS) and Windows Phone 8 (using MPNS), an additional set of headers can be part of hello template.</span></span> <span data-ttu-id="53cb1-143">В случае hello APN tooeither свойство срока действия можно задать выражение константы или tooa шаблона.</span><span class="sxs-lookup"><span data-stu-id="53cb1-143">In hello case of APNs, you can set an expiry property tooeither a constant or tooa template expression.</span></span> <span data-ttu-id="53cb1-144">Полный список см. свойства установки hello, [создавать или перезаписывать установки с ОСТАЛЬНОЙ](https://msdn.microsoft.com/library/azure/mt621153.aspx) раздела.</span><span class="sxs-lookup"><span data-stu-id="53cb1-144">For a complete listing of hello installation properties see, [Create or Overwrite an Installation with REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) topic.</span></span>

#### <a name="secondary-tiles-for-windows-store-apps"></a><span data-ttu-id="53cb1-145">Вспомогательные плитки для приложений из Магазина Windows</span><span class="sxs-lookup"><span data-stu-id="53cb1-145">Secondary Tiles for Windows Store Apps</span></span>
<span data-ttu-id="53cb1-146">Для клиентских приложений для магазина Windows отправку уведомлений — toosecondary плитки hello же, как отправлять им toohello первичной.</span><span class="sxs-lookup"><span data-stu-id="53cb1-146">For Windows Store client applications, sending notifications toosecondary tiles is hello same as sending them toohello primary one.</span></span> <span data-ttu-id="53cb1-147">Это также поддерживается в установках.</span><span class="sxs-lookup"><span data-stu-id="53cb1-147">This is also supported in installations.</span></span> <span data-ttu-id="53cb1-148">Обратите внимание, что вторичной плитки различных ChannelUri, какие hello SDK на клиентское приложение обрабатывает прозрачно.</span><span class="sxs-lookup"><span data-stu-id="53cb1-148">Note that secondary tiles have a different ChannelUri, which hello SDK on your client app handles transparently.</span></span>

<span data-ttu-id="53cb1-149">использует словарь SecondaryTiles Hello hello же TileId, используемые toocreate hello SecondaryTiles объекта в приложении магазина Windows.</span><span class="sxs-lookup"><span data-stu-id="53cb1-149">hello SecondaryTiles dictionary uses hello same TileId that is used toocreate hello SecondaryTiles object in your Windows Store app.</span></span>
<span data-ttu-id="53cb1-150">Как и с hello основной ChannelUri, идентификаторы Channeluri получателей плиток можно изменить в любой момент.</span><span class="sxs-lookup"><span data-stu-id="53cb1-150">As with hello primary ChannelUri, ChannelUris of secondary tiles can change at any moment.</span></span> <span data-ttu-id="53cb1-151">В порядке tookeep hello установок в концентратор уведомлений hello обновлен hello устройства необходимо обновить их с hello текущего идентификаторов Channeluri hello получателей плиток.</span><span class="sxs-lookup"><span data-stu-id="53cb1-151">In order tookeep hello installations in hello notification hub updated, hello device must refresh them with hello current ChannelUris of hello secondary tiles.</span></span>

## <a name="registration-management-from-hello-device"></a><span data-ttu-id="53cb1-152">Управление регистрацией с устройства hello</span><span class="sxs-lookup"><span data-stu-id="53cb1-152">Registration management from hello device</span></span>
<span data-ttu-id="53cb1-153">При управлении регистрацию устройств из клиентских приложений, сервер hello только отвечает за отправку уведомлений.</span><span class="sxs-lookup"><span data-stu-id="53cb1-153">When managing device registration from client apps, hello backend is only responsible for sending notifications.</span></span> <span data-ttu-id="53cb1-154">Клиентские приложения сохранить дескрипторов PNS копирование toodate и зарегистрируйте тегов.</span><span class="sxs-lookup"><span data-stu-id="53cb1-154">Client apps keep PNS handles up toodate, and register tags.</span></span> <span data-ttu-id="53cb1-155">Hello следующий рисунок иллюстрирует этот шаблон.</span><span class="sxs-lookup"><span data-stu-id="53cb1-155">hello following picture illustrates this pattern.</span></span>

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-device.png)

<span data-ttu-id="53cb1-156">устройство Hello сначала получает приветствия PNS обработки из hello PNS, а затем регистрирует напрямую с концентратором уведомлений hello.</span><span class="sxs-lookup"><span data-stu-id="53cb1-156">hello device first retrieves hello PNS handle from hello PNS, then registers with hello notification hub directly.</span></span> <span data-ttu-id="53cb1-157">После успешной регистрации hello внутреннего сервера приложения hello можно отправить уведомление, предназначенных для этой регистрации.</span><span class="sxs-lookup"><span data-stu-id="53cb1-157">After hello registration is successful, hello app backend can send a notification targeting that registration.</span></span> <span data-ttu-id="53cb1-158">Дополнительные сведения о том, как уведомления toosend разделе [маршрутизации и выражения с тегами](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="53cb1-158">For more information about how toosend notifications, see [Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>
<span data-ttu-id="53cb1-159">Обратите внимание, что в этом случае используется только для прослушивания tooaccess права концентраторов уведомлений с устройства hello.</span><span class="sxs-lookup"><span data-stu-id="53cb1-159">Note that in this case, you will use only Listen rights tooaccess your notification hubs from hello device.</span></span> <span data-ttu-id="53cb1-160">Дополнительные сведения см. в статье [Безопасность](notification-hubs-push-notification-security.md).</span><span class="sxs-lookup"><span data-stu-id="53cb1-160">For more information, see [Security](notification-hubs-push-notification-security.md).</span></span>

<span data-ttu-id="53cb1-161">Регистрация устройства hello hello проще, но имеет некоторые недостатки.</span><span class="sxs-lookup"><span data-stu-id="53cb1-161">Registering from hello device is hello simplest method, but it has some drawbacks.</span></span>
<span data-ttu-id="53cb1-162">Hello первый недостатком является то, что клиентского приложения можно обновить только его теги при активном приложение hello.</span><span class="sxs-lookup"><span data-stu-id="53cb1-162">hello first drawback is that a client app can only update its tags when hello app is active.</span></span> <span data-ttu-id="53cb1-163">Например если пользователь имеет два устройства, которые регистрируют теги связанные toosport команд, при регистрации первого устройства hello для дополнительных тега (например, Seahawks), второе устройство hello не будут получать hello уведомления о hello Seahawks до приложение hello на hello Второе устройство выполняется еще раз.</span><span class="sxs-lookup"><span data-stu-id="53cb1-163">For example, if a user has two devices that register tags related toosport teams, when hello first device registers for an additional tag (for example, Seahawks), hello second device will not receive hello notifications about hello Seahawks until hello app on hello second device is executed a second time.</span></span> <span data-ttu-id="53cb1-164">В общем случае если теги влияют на нескольких устройствах, управление теги из внутреннего hello является предпочтительным решением.</span><span class="sxs-lookup"><span data-stu-id="53cb1-164">More generally, when tags are affected by multiple devices, managing tags from hello backend is a desirable option.</span></span>
<span data-ttu-id="53cb1-165">второй недостаток Hello управления регистрацией из клиентского приложения hello —, так как приложения могут быть объектом вредоносной атаки, защита регистрации hello теги toospecific требует особой осторожности как описано в разделе hello «безопасность на уровне тег».</span><span class="sxs-lookup"><span data-stu-id="53cb1-165">hello second drawback of registration management from hello client app is that, since apps can be hacked, securing hello registration toospecific tags requires extra care, as explained in hello section “Tag-level security.”</span></span>

#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-an-installation"></a><span data-ttu-id="53cb1-166">Пример кода tooregister с концентратором уведомлений с использованием установки устройства</span><span class="sxs-lookup"><span data-stu-id="53cb1-166">Example code tooregister with a notification hub from a device using an installation</span></span>
<span data-ttu-id="53cb1-167">В настоящее время поддерживается только с помощью hello [API REST концентраторов уведомлений](https://msdn.microsoft.com/library/mt621153.aspx).</span><span class="sxs-lookup"><span data-stu-id="53cb1-167">At this time, this is only supported using hello [Notification Hubs REST API](https://msdn.microsoft.com/library/mt621153.aspx).</span></span>

<span data-ttu-id="53cb1-168">Можно также использовать метод PATCH hello, с помощью hello [стандарт JSON-Patch](https://tools.ietf.org/html/rfc6902) обновления установки hello.</span><span class="sxs-lookup"><span data-stu-id="53cb1-168">You can also use hello PATCH method using hello [JSON-Patch standard](https://tools.ietf.org/html/rfc6902) for updating hello installation.</span></span>

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



#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-a-registration"></a><span data-ttu-id="53cb1-169">Пример кода tooregister с концентратором уведомлений на устройстве с регистрацией</span><span class="sxs-lookup"><span data-stu-id="53cb1-169">Example code tooregister with a notification hub from a device using a registration</span></span>
<span data-ttu-id="53cb1-170">Эти методы, создание или обновление регистрации для hello устройства, на котором они вызываются.</span><span class="sxs-lookup"><span data-stu-id="53cb1-170">These methods create or update a registration for hello device on which they are called.</span></span> <span data-ttu-id="53cb1-171">Это означает, что в порядке tooupdate hello дескриптор или hello тегов, переписывает всю регистрации hello.</span><span class="sxs-lookup"><span data-stu-id="53cb1-171">This means that in order tooupdate hello handle or hello tags, you must overwrite hello entire registration.</span></span> <span data-ttu-id="53cb1-172">Помните, что регистраций являются временными, поэтому следует всегда иметь надежного хранилища с тегами текущего hello, необходимые для конкретного устройства.</span><span class="sxs-lookup"><span data-stu-id="53cb1-172">Remember that registrations are transient, so you should always have a reliable store with hello current tags that a specific device needs.</span></span>

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


## <a name="registration-management-from-a-backend"></a><span data-ttu-id="53cb1-173">Управление регистрацией из серверной части</span><span class="sxs-lookup"><span data-stu-id="53cb1-173">Registration management from a backend</span></span>
<span data-ttu-id="53cb1-174">Управление регистраций из внутреннего hello требуется написать дополнительный код.</span><span class="sxs-lookup"><span data-stu-id="53cb1-174">Managing registrations from hello backend requires writing additional code.</span></span> <span data-ttu-id="53cb1-175">приложение Hello hello устройства необходимо предоставить hello обновленные серверной toohello дескриптора PNS, каждый раз при запуске приложение hello (вместе с тегами и шаблонов), и серверной hello необходимо обновить этот дескриптор в концентраторе уведомлений hello.</span><span class="sxs-lookup"><span data-stu-id="53cb1-175">hello app from hello device must provide hello updated PNS handle toohello backend every time hello app starts (along with tags and templates), and hello backend must update this handle on hello notification hub.</span></span> <span data-ttu-id="53cb1-176">Hello следующий рисунок иллюстрирует этот проект.</span><span class="sxs-lookup"><span data-stu-id="53cb1-176">hello following picture illustrates this design.</span></span>

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-backend.png)

<span data-ttu-id="53cb1-177">Hello управление регистраций из внутреннего hello преимущества теги hello возможности toomodify tooregistrations даже в том случае, если соответствующие приложение hello на устройстве hello неактивна и клиентское приложение hello tooauthenticate перед добавлением регистрации tooits тег.</span><span class="sxs-lookup"><span data-stu-id="53cb1-177">hello advantages of managing registrations from hello backend include hello ability toomodify tags tooregistrations even when hello corresponding app on hello device is inactive, and tooauthenticate hello client app before adding a tag tooits registration.</span></span>

#### <a name="example-code-tooregister-with-a-notification-hub-from-a-backend-using-an-installation"></a><span data-ttu-id="53cb1-178">Пример кода tooregister с концентратором уведомлений из базы данных, с помощью установки</span><span class="sxs-lookup"><span data-stu-id="53cb1-178">Example code tooregister with a notification hub from a backend using an installation</span></span>
<span data-ttu-id="53cb1-179">как и раньше Hello клиентского устройства по-прежнему возвращает его дескриптора PNS и установки соответствующих свойств и вызывает пользовательский API hello серверную часть, могут выполнить регистрацию hello и авторизацию теги серверной hello и т.д. можно воспользоваться hello [SDK концентратора уведомлений внутренних операций](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="53cb1-179">hello client device still gets its PNS handle and relevant installation properties as before and calls a custom API on hello backend that can perform hello registration and authorize tags etc. hello backend can leverage hello [Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="53cb1-180">Можно также использовать метод PATCH hello, с помощью hello [стандарт JSON-Patch](https://tools.ietf.org/html/rfc6902) обновления установки hello.</span><span class="sxs-lookup"><span data-stu-id="53cb1-180">You can also use hello PATCH method using hello [JSON-Patch standard](https://tools.ietf.org/html/rfc6902) for updating hello installation.</span></span>

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


#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-a-registration-id"></a><span data-ttu-id="53cb1-181">Пример кода tooregister с концентратором уведомлений на устройстве с код регистрации</span><span class="sxs-lookup"><span data-stu-id="53cb1-181">Example code tooregister with a notification hub from a device using a registration id</span></span>
<span data-ttu-id="53cb1-182">Из серверной части приложения с регистрациями можно выполнять основные операции CRUDS.</span><span class="sxs-lookup"><span data-stu-id="53cb1-182">From your app backend, you can perform basic CRUDS operations on registrations.</span></span> <span data-ttu-id="53cb1-183">Например:</span><span class="sxs-lookup"><span data-stu-id="53cb1-183">For example:</span></span>

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


<span data-ttu-id="53cb1-184">Серверная часть Hello должен обрабатывать параллелизма между обновлениями регистрации.</span><span class="sxs-lookup"><span data-stu-id="53cb1-184">hello backend must handle concurrency between registration updates.</span></span> <span data-ttu-id="53cb1-185">Служебная шина предоставляет управление оптимистичным параллелизмом для управления регистрациями.</span><span class="sxs-lookup"><span data-stu-id="53cb1-185">Service Bus offers optimistic concurrency control for registration management.</span></span> <span data-ttu-id="53cb1-186">На уровне hello HTTP это реализуется с использованием hello ETag на операции управления регистрации.</span><span class="sxs-lookup"><span data-stu-id="53cb1-186">At hello HTTP level, this is implemented with hello use of ETag on registration management operations.</span></span> <span data-ttu-id="53cb1-187">Эта функция автоматически используется в пакетах Microsoft SDK, которые выдают исключение, если обновление отклоняется по причинам параллелизма.</span><span class="sxs-lookup"><span data-stu-id="53cb1-187">This feature is transparently used by Microsoft SDKs, which throw an exception if an update is rejected for concurrency reasons.</span></span> <span data-ttu-id="53cb1-188">внутреннего сервера приложения Hello отвечает за обработку этих исключений и повторная попытка обновления hello, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="53cb1-188">hello app backend is responsible for handling these exceptions and retrying hello update if required.</span></span>

