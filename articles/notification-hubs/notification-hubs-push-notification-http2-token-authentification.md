---
title: "Проверка подлинности на основе токенов (HTTP/2) для APNS в Центрах уведомлений Azure | Документация Майкрософт"
description: "В этом разделе объясняется, как использовать новую проверку подлинности по токенам для APNS"
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
ms.openlocfilehash: 5a21bcd9f12fc3f96b17a556ba15526c35ababe2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="token-based-http2-authentication-for-apns"></a><span data-ttu-id="7982b-103">Проверка подлинности на основе токенов (HTTP/2) для APNS</span><span class="sxs-lookup"><span data-stu-id="7982b-103">Token-based (HTTP/2) Authentication for APNS</span></span>
## <a name="overview"></a><span data-ttu-id="7982b-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="7982b-104">Overview</span></span>
<span data-ttu-id="7982b-105">В этой статье подробно описывается использование нового протокола APNS, HTTP/2, при проверке подлинности на основе токенов.</span><span class="sxs-lookup"><span data-stu-id="7982b-105">This article details how to use the new APNS HTTP/2 protocol with token based authentication.</span></span>

<span data-ttu-id="7982b-106">Основные преимущества использования нового протокола:</span><span class="sxs-lookup"><span data-stu-id="7982b-106">The key benefits of using the new protocol include:</span></span>
-   <span data-ttu-id="7982b-107">Проще создать токен, чем сертификат.</span><span class="sxs-lookup"><span data-stu-id="7982b-107">Token generation is relatively hassle free (compared to certificates)</span></span>
-   <span data-ttu-id="7982b-108">У токенов отсутствует срок окончания действия. Вы управляете их созданием и отзывом.</span><span class="sxs-lookup"><span data-stu-id="7982b-108">No more expiry dates – you are in control of your authentication tokens and their revocation</span></span>
-   <span data-ttu-id="7982b-109">Полезные данные могут иметь размер до 4 КБ.</span><span class="sxs-lookup"><span data-stu-id="7982b-109">Payloads can now be up to 4 KB</span></span>
- <span data-ttu-id="7982b-110">Синхронная обратная связь.</span><span class="sxs-lookup"><span data-stu-id="7982b-110">Synchronous feedback</span></span>
-   <span data-ttu-id="7982b-111">Используется последняя версия протокола Apple, в то время как сертификаты по-прежнему используют устаревший двоичный протокол.</span><span class="sxs-lookup"><span data-stu-id="7982b-111">You’re on Apple’s latest protocol – certificates still use the binary protocol, which is marked for deprecation</span></span>

<span data-ttu-id="7982b-112">Этот новый механизм можно реализовать в два этапа за несколько минут:</span><span class="sxs-lookup"><span data-stu-id="7982b-112">Using this new mechanism can be done in two steps in a few minutes:</span></span>
1.  <span data-ttu-id="7982b-113">Получите необходимые сведения на портале учетной записи разработчика Apple.</span><span class="sxs-lookup"><span data-stu-id="7982b-113">Obtain the necessary information from the Apple Developer Account portal</span></span>
2.  <span data-ttu-id="7982b-114">Добавьте новые данные в центр уведомлений.</span><span class="sxs-lookup"><span data-stu-id="7982b-114">Configure your notification hub with the new information</span></span>

<span data-ttu-id="7982b-115">Теперь для APNS центры уведомлений будут использовать новую систему проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="7982b-115">Notification Hubs is now all set to use the new authentication system with APNS.</span></span> 

<span data-ttu-id="7982b-116">Если для APNS вы использовали учетные данные сертификата, обратите внимание на следующее:</span><span class="sxs-lookup"><span data-stu-id="7982b-116">Note that if you migrated from using certificate credentials for APNS:</span></span>
- <span data-ttu-id="7982b-117">свойства токена перезапишут сертификат в нашей системе;</span><span class="sxs-lookup"><span data-stu-id="7982b-117">the token properties overwrite your certificate in our system,</span></span>
- <span data-ttu-id="7982b-118">приложение по-прежнему продолжит получать уведомления.</span><span class="sxs-lookup"><span data-stu-id="7982b-118">but your application continues to receive notifications seamlessly.</span></span>

## <a name="obtaining-authentication-information-from-apple"></a><span data-ttu-id="7982b-119">Получение сведений о проверке подлинности от Apple</span><span class="sxs-lookup"><span data-stu-id="7982b-119">Obtaining authentication information from Apple</span></span>
<span data-ttu-id="7982b-120">Чтобы включить проверку подлинности на основе токенов, необходимы следующие свойства вашей учетной записи разработчика Apple:</span><span class="sxs-lookup"><span data-stu-id="7982b-120">To enable token-based authentication, you need the following properties from your Apple Developer Account:</span></span>
### <a name="key-identifier"></a><span data-ttu-id="7982b-121">Идентификатор ключа</span><span class="sxs-lookup"><span data-stu-id="7982b-121">Key Identifier</span></span>
<span data-ttu-id="7982b-122">Идентификатор ключа можно получить на странице "Ключи" в учетной записи разработчика Apple.</span><span class="sxs-lookup"><span data-stu-id="7982b-122">The key identifier can be obtained from the "Keys" page in your Apple Developer Account</span></span>

![](./media/notification-hubs-push-notification-http2-token-authentification/obtaining-auth-information-from-apple.png)

### <a name="application-identifier--application-name"></a><span data-ttu-id="7982b-123">Идентификатор и имя приложения</span><span class="sxs-lookup"><span data-stu-id="7982b-123">Application Identifier & Application Name</span></span>
<span data-ttu-id="7982b-124">Имя приложения доступно на странице идентификаторов приложений в учетной записи разработчика.</span><span class="sxs-lookup"><span data-stu-id="7982b-124">The application name is available via the App IDs page in the Developer Account.</span></span> 
![](./media/notification-hubs-push-notification-http2-token-authentification/app-name.png)

<span data-ttu-id="7982b-125">Идентификатор приложения доступен на странице сведений о членстве в учетной записи разработчика.</span><span class="sxs-lookup"><span data-stu-id="7982b-125">The application identifier is available via the membership details page in the Developer Account.</span></span>
![](./media/notification-hubs-push-notification-http2-token-authentification/app-id.png)


### <a name="authentication-token"></a><span data-ttu-id="7982b-126">Токен проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="7982b-126">Authentication token</span></span>
<span data-ttu-id="7982b-127">После создания токена приложения можно скачать токен проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="7982b-127">The authentication token can be downloaded after you generate a token for your application.</span></span> <span data-ttu-id="7982b-128">Дополнительные сведения о создании этого токена см. в [документации для разработчиков Apple](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65).</span><span class="sxs-lookup"><span data-stu-id="7982b-128">For details on how to generate this token, refer to [Apple’s Developer documentation](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65).</span></span>

## <a name="configuring-your-notification-hub-to-use-token-based-authentication"></a><span data-ttu-id="7982b-129">Настройка центра уведомлений для использования проверки подлинности на основе токенов</span><span class="sxs-lookup"><span data-stu-id="7982b-129">Configuring your notification hub to use token-based authentication</span></span>
### <a name="configure-via-the-azure-portal"></a><span data-ttu-id="7982b-130">Настройка на портале Azure</span><span class="sxs-lookup"><span data-stu-id="7982b-130">Configure via the Azure portal</span></span>
<span data-ttu-id="7982b-131">Чтобы включить проверку подлинности на основе токенов, войдите на портал Azure и перейдите на панель "Концентратор уведомлений > Службы уведомлений > APNS".</span><span class="sxs-lookup"><span data-stu-id="7982b-131">To enable token based authentication in the portal, log in to the Azure portal and go to your Notification Hub > Notification Services > APNS panel.</span></span> 

<span data-ttu-id="7982b-132">Там есть новое свойство *Режим проверки подлинности*.</span><span class="sxs-lookup"><span data-stu-id="7982b-132">There is a new property – *Authentication Mode*.</span></span> <span data-ttu-id="7982b-133">Выберите "Токен", чтобы обновить все соответствующие свойства токенов в концентраторе.</span><span class="sxs-lookup"><span data-stu-id="7982b-133">Selecting Token allows you to update your hub with all the relevant token properties.</span></span>

![](./media/notification-hubs-push-notification-http2-token-authentification/azure-portal-apns-settings.png)

- <span data-ttu-id="7982b-134">Введите свойства, полученные из учетной записи разработчика Apple.</span><span class="sxs-lookup"><span data-stu-id="7982b-134">Enter the properties you retrieved from your Apple developer account,</span></span> 
- <span data-ttu-id="7982b-135">Выберите режим приложения (Production (Рабочий) или Sandbox (Песочница)).</span><span class="sxs-lookup"><span data-stu-id="7982b-135">choose your application mode (Production or Sandbox)</span></span> 
- <span data-ttu-id="7982b-136">Щелкните Save (Сохранить), чтобы обновить учетные данные APNS.</span><span class="sxs-lookup"><span data-stu-id="7982b-136">click Save to update your APNS credentials.</span></span> 

### <a name="configure-via-management-api-rest"></a><span data-ttu-id="7982b-137">Настройка с помощью API управления (REST)</span><span class="sxs-lookup"><span data-stu-id="7982b-137">Configure via Management API (REST)</span></span>

<span data-ttu-id="7982b-138">Чтобы настроить центр уведомлений для использования проверки подлинности на основе токенов, вы можете воспользоваться нашими [API-интерфейсами управления](https://msdn.microsoft.com/library/azure/dn495827.aspx).</span><span class="sxs-lookup"><span data-stu-id="7982b-138">You can use our [management APIs](https://msdn.microsoft.com/library/azure/dn495827.aspx) to update your notification hub to use token-based authentication.</span></span>
<span data-ttu-id="7982b-139">В зависимости от выбранного режима для настраиваемого приложения (Sandbox (Песочница) или Production (Рабочее)) (указано в учетной записи разработчика Apple), используйте одну из соответствующих конечных точек.</span><span class="sxs-lookup"><span data-stu-id="7982b-139">Depending on whether the application you’re configuring is a Sandbox or Production app (specified in your Apple Developer Account), use one of the corresponding endpoints:</span></span>

- <span data-ttu-id="7982b-140">Конечная точка для "песочницы": [https://api.development.push.apple.com:443/3/device](https://api.development.push.apple.com:443/3/device).</span><span class="sxs-lookup"><span data-stu-id="7982b-140">Sandbox Endpoint: [https://api.development.push.apple.com:443/3/device](https://api.development.push.apple.com:443/3/device)</span></span>
- <span data-ttu-id="7982b-141">Конечная точка рабочего приложения: [https://api.push.apple.com:443/3/device](https://api.push.apple.com:443/3/device).</span><span class="sxs-lookup"><span data-stu-id="7982b-141">Production Endpoint: [https://api.push.apple.com:443/3/device](https://api.push.apple.com:443/3/device)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7982b-142">Для проверки подлинности на основе токенов требуется версия API **2017-04 или более поздняя**.</span><span class="sxs-lookup"><span data-stu-id="7982b-142">Token-based authentication requires an API version of: **2017-04 or later**.</span></span>
> 
> 

<span data-ttu-id="7982b-143">Ниже приведен пример запроса PUT, с помощью которого можно настроить центр для использования проверки подлинности на основе токенов:</span><span class="sxs-lookup"><span data-stu-id="7982b-143">Here’s an example of a PUT request to update a hub with token-based authentication:</span></span>


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
        

### <a name="configure-via-the-net-sdk"></a><span data-ttu-id="7982b-144">Настройка с использованием пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="7982b-144">Configure via the .NET SDK</span></span>
<span data-ttu-id="7982b-145">Центр можно настроить для использования проверки подлинности на основе токенов с помощью нашего [клиентского пакета SDK последней версии](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8).</span><span class="sxs-lookup"><span data-stu-id="7982b-145">You can configure your hub to use token based authentication using our [latest client SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8).</span></span> 

<span data-ttu-id="7982b-146">Ниже приведен пример кода, который иллюстрирует правильное использование.</span><span class="sxs-lookup"><span data-stu-id="7982b-146">Here’s a code sample illustrating the correct usage:</span></span>


        NamespaceManager nm = NamespaceManager.CreateFromConnectionString(_endpoint);
        string token = "YOUR TOKEN HERE";
        string keyId = "YOUR KEY ID HERE";
        string appName = "YOUR APP NAME HERE";
        string appId = "YOUR APP ID HERE";
        NotificationHubDescription desc = new NotificationHubDescription("PATH TO YOUR HUB");
        desc.ApnsCredential = new ApnsCredential(token, keyId, appId, appName);
        desc.ApnsCredential.Endpoint = @"https://api.development.push.apple.com:443/3/device";
        nm.UpdateNotificationHubAsync(desc);

## <a name="reverting-to-using-certificate-based-authentication"></a><span data-ttu-id="7982b-147">Восстановление проверки подлинности на основе сертификатов</span><span class="sxs-lookup"><span data-stu-id="7982b-147">Reverting to using certificate-based authentication</span></span>
<span data-ttu-id="7982b-148">С помощью любого предыдущего метода можно в любое время вернуться к использованию проверки подлинности на основе сертификатов и передавать сертификат вместо свойств токена.</span><span class="sxs-lookup"><span data-stu-id="7982b-148">You can revert at any time to using certificate-based authentication by using any preceding method and passing the certificate instead of the token properties.</span></span> <span data-ttu-id="7982b-149">Это действие перезаписывает ранее сохраненные учетные данные.</span><span class="sxs-lookup"><span data-stu-id="7982b-149">That action overwrites the previously stored credentials.</span></span>
