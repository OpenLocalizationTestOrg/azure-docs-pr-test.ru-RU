---
title: "aaaToken (HTTP/2) проверка подлинности на основе для APNS в концентраторов уведомлений Azure | Документы Microsoft"
description: "В этом разделе объясняется, как tooleverage hello нового токена проверки подлинности для APNS"
services: notification-hubs
documentationcenter: .net
author: kpiteira
manager: erikre
editor: 
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 05/17/2017
ms.author: kapiteir
ms.openlocfilehash: 3353d7f16033ce0b68edec9ee9aeb98f47faa1fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="token-based-http2-authentication-for-apns"></a><span data-ttu-id="05260-103">Проверка подлинности на основе токенов (HTTP/2) для APNS</span><span class="sxs-lookup"><span data-stu-id="05260-103">Token-based (HTTP/2) Authentication for APNS</span></span>
## <a name="overview"></a><span data-ttu-id="05260-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="05260-104">Overview</span></span>
<span data-ttu-id="05260-105">В этой статье указаны как проверку подлинности на основе протокола hello новый toouse APNS HTTP/2 с маркером.</span><span class="sxs-lookup"><span data-stu-id="05260-105">This article details how toouse hello new APNS HTTP/2 protocol with token based authentication.</span></span>

<span data-ttu-id="05260-106">Hello основные преимущества использования нового протокола hello:</span><span class="sxs-lookup"><span data-stu-id="05260-106">hello key benefits of using hello new protocol include:</span></span>
-   <span data-ttu-id="05260-107">Создания токенов — относительно оскорблять свободного (сравниваемых toocertificates)</span><span class="sxs-lookup"><span data-stu-id="05260-107">Token generation is relatively hassle free (compared toocertificates)</span></span>
-   <span data-ttu-id="05260-108">У токенов отсутствует срок окончания действия. Вы управляете их созданием и отзывом.</span><span class="sxs-lookup"><span data-stu-id="05260-108">No more expiry dates – you are in control of your authentication tokens and their revocation</span></span>
-   <span data-ttu-id="05260-109">Полезные данные теперь можно вверх too4 КБ</span><span class="sxs-lookup"><span data-stu-id="05260-109">Payloads can now be up too4 KB</span></span>
- <span data-ttu-id="05260-110">Синхронная обратная связь.</span><span class="sxs-lookup"><span data-stu-id="05260-110">Synchronous feedback</span></span>
-   <span data-ttu-id="05260-111">Вы используете Apple последнюю протокола — сертификаты по-прежнему использовать двоичный протокол hello, которая помечена для об устаревании</span><span class="sxs-lookup"><span data-stu-id="05260-111">You’re on Apple’s latest protocol – certificates still use hello binary protocol, which is marked for deprecation</span></span>

<span data-ttu-id="05260-112">Этот новый механизм можно реализовать в два этапа за несколько минут:</span><span class="sxs-lookup"><span data-stu-id="05260-112">Using this new mechanism can be done in two steps in a few minutes:</span></span>
1.  <span data-ttu-id="05260-113">Получить hello из портала учетной записи разработчика Apple hello</span><span class="sxs-lookup"><span data-stu-id="05260-113">Obtain hello necessary information from hello Apple Developer Account portal</span></span>
2.  <span data-ttu-id="05260-114">Настройка центра уведомлений с новыми данными hello</span><span class="sxs-lookup"><span data-stu-id="05260-114">Configure your notification hub with hello new information</span></span>

<span data-ttu-id="05260-115">Концентраторы уведомлений сейчас все набор toouse hello новый системой проверки подлинности в APNS.</span><span class="sxs-lookup"><span data-stu-id="05260-115">Notification Hubs is now all set toouse hello new authentication system with APNS.</span></span> 

<span data-ttu-id="05260-116">Если для APNS вы использовали учетные данные сертификата, обратите внимание на следующее:</span><span class="sxs-lookup"><span data-stu-id="05260-116">Note that if you migrated from using certificate credentials for APNS:</span></span>
- <span data-ttu-id="05260-117">свойства токена Hello перезаписать сертификат в нашей системе</span><span class="sxs-lookup"><span data-stu-id="05260-117">hello token properties overwrite your certificate in our system,</span></span>
- <span data-ttu-id="05260-118">но приложение продолжает работать tooreceive уведомления без проблем.</span><span class="sxs-lookup"><span data-stu-id="05260-118">but your application continues tooreceive notifications seamlessly.</span></span>

## <a name="obtaining-authentication-information-from-apple"></a><span data-ttu-id="05260-119">Получение сведений о проверке подлинности от Apple</span><span class="sxs-lookup"><span data-stu-id="05260-119">Obtaining authentication information from Apple</span></span>
<span data-ttu-id="05260-120">tooenable маркер проверки подлинности на основе необходимые hello следующие свойства из вашей учетной записи разработчика Apple.</span><span class="sxs-lookup"><span data-stu-id="05260-120">tooenable token-based authentication, you need hello following properties from your Apple Developer Account:</span></span>
### <a name="key-identifier"></a><span data-ttu-id="05260-121">Идентификатор ключа</span><span class="sxs-lookup"><span data-stu-id="05260-121">Key Identifier</span></span>
<span data-ttu-id="05260-122">Идентификатор ключа Hello можно получить на странице «Ключи» hello в учетной записи разработчика Apple</span><span class="sxs-lookup"><span data-stu-id="05260-122">hello key identifier can be obtained from hello "Keys" page in your Apple Developer Account</span></span>

![](./media/notification-hubs-push-notification-http2-token-authentification/obtaining-auth-information-from-apple.png)

### <a name="application-identifier--application-name"></a><span data-ttu-id="05260-123">Идентификатор и имя приложения</span><span class="sxs-lookup"><span data-stu-id="05260-123">Application Identifier & Application Name</span></span>
<span data-ttu-id="05260-124">Имя приложения Hello доступна через страницу идентификаторы приложений hello в hello учетную запись разработчика.</span><span class="sxs-lookup"><span data-stu-id="05260-124">hello application name is available via hello App IDs page in hello Developer Account.</span></span> 
![](./media/notification-hubs-push-notification-http2-token-authentification/app-name.png)

<span data-ttu-id="05260-125">Идентификатор приложения Hello доступна через hello страница сведений членства в hello учетную запись разработчика.</span><span class="sxs-lookup"><span data-stu-id="05260-125">hello application identifier is available via hello membership details page in hello Developer Account.</span></span>
![](./media/notification-hubs-push-notification-http2-token-authentification/app-id.png)


### <a name="authentication-token"></a><span data-ttu-id="05260-126">Токен проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="05260-126">Authentication token</span></span>
<span data-ttu-id="05260-127">После создания маркера для приложения можно скачать Hello токена проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="05260-127">hello authentication token can be downloaded after you generate a token for your application.</span></span> <span data-ttu-id="05260-128">Подробнее о как toogenerate это маркер, см. в слишком[документации разработчика Apple](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65).</span><span class="sxs-lookup"><span data-stu-id="05260-128">For details on how toogenerate this token, refer too[Apple’s Developer documentation](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65).</span></span>

## <a name="configuring-your-notification-hub-toouse-token-based-authentication"></a><span data-ttu-id="05260-129">Настройка аутентификация токены toouse концентратора уведомлений</span><span class="sxs-lookup"><span data-stu-id="05260-129">Configuring your notification hub toouse token-based authentication</span></span>
### <a name="configure-via-hello-azure-portal"></a><span data-ttu-id="05260-130">Настройка с использованием hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="05260-130">Configure via hello Azure portal</span></span>
<span data-ttu-id="05260-131">tooenable маркер проверки подлинности hello портала вход toohello портал Azure на основе и перейти tooyour концентратора уведомлений > служб Notification Services > Панель APNS.</span><span class="sxs-lookup"><span data-stu-id="05260-131">tooenable token based authentication in hello portal, log in toohello Azure portal and go tooyour Notification Hub > Notification Services > APNS panel.</span></span> 

<span data-ttu-id="05260-132">Там есть новое свойство *Режим проверки подлинности*.</span><span class="sxs-lookup"><span data-stu-id="05260-132">There is a new property – *Authentication Mode*.</span></span> <span data-ttu-id="05260-133">При выборе маркер позволяет tooupdate концентратор с hello соответствующих токенов свойств.</span><span class="sxs-lookup"><span data-stu-id="05260-133">Selecting Token allows you tooupdate your hub with all hello relevant token properties.</span></span>

![](./media/notification-hubs-push-notification-http2-token-authentification/azure-portal-apns-settings.png)

- <span data-ttu-id="05260-134">Введите свойства hello, полученный от учетной записи разработчика Apple</span><span class="sxs-lookup"><span data-stu-id="05260-134">Enter hello properties you retrieved from your Apple developer account,</span></span> 
- <span data-ttu-id="05260-135">Выберите режим приложения (Production (Рабочий) или Sandbox (Песочница)).</span><span class="sxs-lookup"><span data-stu-id="05260-135">choose your application mode (Production or Sandbox)</span></span> 
- <span data-ttu-id="05260-136">Нажмите кнопку Сохранить tooupdate APNS учетные данные.</span><span class="sxs-lookup"><span data-stu-id="05260-136">click Save tooupdate your APNS credentials.</span></span> 

### <a name="configure-via-management-api-rest"></a><span data-ttu-id="05260-137">Настройка с помощью API управления (REST)</span><span class="sxs-lookup"><span data-stu-id="05260-137">Configure via Management API (REST)</span></span>

<span data-ttu-id="05260-138">Можно использовать наши [API-интерфейсы управления](https://msdn.microsoft.com/library/azure/dn495827.aspx) tooupdate аутентификация токены toouse концентратора уведомлений.</span><span class="sxs-lookup"><span data-stu-id="05260-138">You can use our [management APIs](https://msdn.microsoft.com/library/azure/dn495827.aspx) tooupdate your notification hub toouse token-based authentication.</span></span>
<span data-ttu-id="05260-139">В зависимости от приложения hello, которую вы настраиваете "песочницы" производственного приложения или (указанный в учетной записи разработчика Apple) используйте один из hello соответствующие конечные точки.</span><span class="sxs-lookup"><span data-stu-id="05260-139">Depending on whether hello application you’re configuring is a Sandbox or Production app (specified in your Apple Developer Account), use one of hello corresponding endpoints:</span></span>

- <span data-ttu-id="05260-140">Конечная точка для "песочницы": [https://api.development.push.apple.com:443/3/device](https://api.development.push.apple.com:443/3/device).</span><span class="sxs-lookup"><span data-stu-id="05260-140">Sandbox Endpoint: [https://api.development.push.apple.com:443/3/device](https://api.development.push.apple.com:443/3/device)</span></span>
- <span data-ttu-id="05260-141">Конечная точка рабочего приложения: [https://api.push.apple.com:443/3/device](https://api.push.apple.com:443/3/device).</span><span class="sxs-lookup"><span data-stu-id="05260-141">Production Endpoint: [https://api.push.apple.com:443/3/device](https://api.push.apple.com:443/3/device)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="05260-142">Для проверки подлинности на основе токенов требуется версия API **2017-04 или более поздняя**.</span><span class="sxs-lookup"><span data-stu-id="05260-142">Token-based authentication requires an API version of: **2017-04 or later**.</span></span>
> 
> 

<span data-ttu-id="05260-143">Ниже приведен пример tooupdate запрос PUT концентратора с проверкой подлинности на основе маркеров:</span><span class="sxs-lookup"><span data-stu-id="05260-143">Here’s an example of a PUT request tooupdate a hub with token-based authentication:</span></span>


        PUT https://{namespace}.servicebus.windows.net/{Notification Hub}?api-version=2017-04
          "Properties": {
            "ApnsCredential": {
              "Properties": {
                "KeyId": "<Your Key Id>",
                "Token": "<Your Authentication Token>",
                "AppName": "<Your Application Name>",
                "AppId": "<Your Application Id>",
                "Endpoint":"<Sandbox/Production Endpoint>"
              }
            }
          }
        

### <a name="configure-via-hello-net-sdk"></a><span data-ttu-id="05260-144">Настройка с использованием hello .NET SDK</span><span class="sxs-lookup"><span data-stu-id="05260-144">Configure via hello .NET SDK</span></span>
<span data-ttu-id="05260-145">Можно настроить на токена проверки подлинности на основе toouse концентратора с помощью наших [последнюю версию пакета SDK для клиента](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8).</span><span class="sxs-lookup"><span data-stu-id="05260-145">You can configure your hub toouse token based authentication using our [latest client SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8).</span></span> 

<span data-ttu-id="05260-146">Ниже приведен пример кода, иллюстрирующие правильное использование hello.</span><span class="sxs-lookup"><span data-stu-id="05260-146">Here’s a code sample illustrating hello correct usage:</span></span>


        NamespaceManager nm = NamespaceManager.CreateFromConnectionString(_endpoint);
        string token = "YOUR TOKEN HERE";
        string keyId = "YOUR KEY ID HERE";
        string appName = "YOUR APP NAME HERE";
        string appId = "YOUR APP ID HERE";
        NotificationHubDescription desc = new NotificationHubDescription("PATH tooYOUR HUB");
        desc.ApnsCredential = new ApnsCredential(token, keyId, appId, appName);
        desc.ApnsCredential.Endpoint = @"https://api.development.push.apple.com:443/3/device";
        nm.UpdateNotificationHubAsync(desc);

## <a name="reverting-toousing-certificate-based-authentication"></a><span data-ttu-id="05260-147">Возврат toousing сертификат проверки подлинности на основе</span><span class="sxs-lookup"><span data-stu-id="05260-147">Reverting toousing certificate-based authentication</span></span>
<span data-ttu-id="05260-148">Можно вернуться в любое время toousing сертификат проверки подлинности на основе с помощью любого предыдущего сертификата hello метода и передача вместо свойства токена hello.</span><span class="sxs-lookup"><span data-stu-id="05260-148">You can revert at any time toousing certificate-based authentication by using any preceding method and passing hello certificate instead of hello token properties.</span></span> <span data-ttu-id="05260-149">Ранее, действие перезаписывает hello сохраненные учетные данные.</span><span class="sxs-lookup"><span data-stu-id="05260-149">That action overwrites hello previously stored credentials.</span></span>
