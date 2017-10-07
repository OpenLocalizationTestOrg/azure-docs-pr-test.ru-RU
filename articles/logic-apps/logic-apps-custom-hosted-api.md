---
title: "Вызовите aaaDeploy и пройти проверку подлинности веб-API и REST API для приложения логики Azure | Документы Microsoft"
description: "Развертывание, проверка подлинности и вызов веб-интерфейсов API и интерфейсов REST API в рабочих процессах для интеграции системы с приложениями логики Azure"
keywords: "веб-интерфейсы API, интерфейсы REST API, соединители, рабочие процессы, интеграция системы, проверка подлинности"
services: logic-apps
author: stepsic-microsoft-com
manager: anneta
editor: 
documentationcenter: 
ms.assetid: f113005d-0ba6-496b-8230-c1eadbd6dbb9
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: LADocs; stepsic
ms.openlocfilehash: ca1e4f28196b21f43b7c9ab94029684121e36f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-call-and-authenticate-custom-apis-as-connectors-for-logic-apps"></a><span data-ttu-id="9d485-104">Развертывание, вызов и проверка подлинности пользовательских API в качестве соединителей для приложений логики</span><span class="sxs-lookup"><span data-stu-id="9d485-104">Deploy, call, and authenticate custom APIs as connectors for logic apps</span></span>

<span data-ttu-id="9d485-105">По окончании [создавать пользовательские API](./logic-apps-create-api-app.md) , обеспечивающие toouse действий или триггеров в логике приложения рабочих процессов, необходимо развернуть собственные интерфейсы API, прежде чем их можно вызывать.</span><span class="sxs-lookup"><span data-stu-id="9d485-105">After you [create custom APIs](./logic-apps-create-api-app.md) that provide actions or triggers toouse in logic apps workflows, you must deploy your APIs before you can call them.</span></span> <span data-ttu-id="9d485-106">И хотя API-Интерфейс любых можно вызывать из приложения логики, для получения наилучших результатов hello, добавьте [метаданных Swagger](http://swagger.io/specification/) , описывающий операции и параметры вашего API.</span><span class="sxs-lookup"><span data-stu-id="9d485-106">And although you can call any API from a logic app, for hello best experience, add [Swagger metadata](http://swagger.io/specification/) that describes your API's operations and parameters.</span></span> <span data-ttu-id="9d485-107">Этот файл Swagger позволяет улучшить работу API и упростить его интеграцию с приложениями логики.</span><span class="sxs-lookup"><span data-stu-id="9d485-107">This Swagger file helps your API work better and integrate more easily with logic apps.</span></span>

<span data-ttu-id="9d485-108">Интерфейсы API, как можно развернуть [веб-приложений](../app-service-web/app-service-web-overview.md), но следует рассмотреть возможность развертывания интерфейсы API, как [приложения API](../app-service-api/app-service-api-apps-why-best-platform.md), которой может облегчить вашу работу при построении, размещения и использовать интерфейсы API в облаке hello и на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="9d485-108">You can deploy your APIs as [web apps](../app-service-web/app-service-web-overview.md), but consider deploying your APIs as [API apps](../app-service-api/app-service-api-apps-why-best-platform.md), which can make your job easier when you build, host, and consume APIs in hello cloud and on premises.</span></span> <span data-ttu-id="9d485-109">Не нужно toochange любого кода в собственные интерфейсы API — просто развертывания приложения API tooan кода.</span><span class="sxs-lookup"><span data-stu-id="9d485-109">You don't have toochange any code in your APIs -- just deploy your code tooan API app.</span></span> <span data-ttu-id="9d485-110">Собственные интерфейсы API можно разместить на [службе приложений Azure](../app-service/app-service-value-prop-what-is.md), платформа как услуги (PaaS), предоставляющий одним из способов наиболее простым и максимально масштабируемые hello для API размещения.</span><span class="sxs-lookup"><span data-stu-id="9d485-110">You can host your APIs on [Azure App Service](../app-service/app-service-value-prop-what-is.md), a platform-as-a-service (PaaS) offering that provides one of hello best, easiest, and most scalable ways for API hosting.</span></span>

<span data-ttu-id="9d485-111">tooauthenticate вызовы от логики приложения tooyour API-интерфейсы, настройкой Azure Active Directory в hello портал Azure, что избавляет tooupdate кода.</span><span class="sxs-lookup"><span data-stu-id="9d485-111">tooauthenticate calls from logic apps tooyour APIs, you can set up Azure Active Directory in hello Azure portal so you don't have tooupdate your code.</span></span> <span data-ttu-id="9d485-112">Вы можете также применить обязательную проверку подлинности с помощью кода API.</span><span class="sxs-lookup"><span data-stu-id="9d485-112">Or, you can require and enforce authentication through your API's code.</span></span>

## <a name="deploy-your-api-as-a-web-app-or-api-app"></a><span data-ttu-id="9d485-113">Развертывание API в качестве веб-приложения или приложения API</span><span class="sxs-lookup"><span data-stu-id="9d485-113">Deploy your API as a web app or API app</span></span>

<span data-ttu-id="9d485-114">Перед вызовом настраиваемого API из логики приложения, разверните API как веб-приложения или tooAzure приложение API службы приложений.</span><span class="sxs-lookup"><span data-stu-id="9d485-114">Before you can call your custom API from a logic app, deploy your API as a web app or API app tooAzure App Service.</span></span> <span data-ttu-id="9d485-115">Кроме того, toomake Swagger документ для чтения в hello конструктор логики приложения, задайте свойства определения hello API и включите [ресурсов независимо от источника (CORS) для управления доступом](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) для веб-приложения или приложения API.</span><span class="sxs-lookup"><span data-stu-id="9d485-115">Also, toomake your Swagger document readable by hello Logic App Designer, set hello API definition properties and turn on [cross-origin resource sharing (CORS)](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) for your web app or API app.</span></span>

1. <span data-ttu-id="9d485-116">В hello портал Azure выберите веб-приложения или приложения API.</span><span class="sxs-lookup"><span data-stu-id="9d485-116">In hello Azure portal, select your web app or API app.</span></span>

2. <span data-ttu-id="9d485-117">В колонке hello, которое открывается в разделе **API**, выберите **определения API**.</span><span class="sxs-lookup"><span data-stu-id="9d485-117">In hello blade that opens, under **API**, choose **API definition**.</span></span> <span data-ttu-id="9d485-118">Набор hello **расположение определения API** toohello URL-адрес для файла swagger.json.</span><span class="sxs-lookup"><span data-stu-id="9d485-118">Set hello **API definition location** toohello URL for your swagger.json file.</span></span>

   <span data-ttu-id="9d485-119">Как правило hello URL-адрес отображается в следующем формате:`https://{name}.azurewebsites.net/swagger/docs/v1)`</span><span class="sxs-lookup"><span data-stu-id="9d485-119">Usually, hello URL appears in this format: `https://{name}.azurewebsites.net/swagger/docs/v1)`</span></span>

   ![Файл tooSwagger ссылки для настраиваемого API](media/logic-apps-custom-hosted-api/custom-api-swagger-url.png)

3. <span data-ttu-id="9d485-121">В разделе **API** выберите **CORS**.</span><span class="sxs-lookup"><span data-stu-id="9d485-121">Under **API**, choose **CORS**.</span></span> <span data-ttu-id="9d485-122">Задать политику CORS hello для **допускается источников** слишком**"*"** (Разрешить все).</span><span class="sxs-lookup"><span data-stu-id="9d485-122">Set hello CORS policy for **Allowed origins** too**'*'** (allow all).</span></span>

   <span data-ttu-id="9d485-123">Этот параметр разрешает запросы из конструктора приложений логики.</span><span class="sxs-lookup"><span data-stu-id="9d485-123">This setting permits requests from Logic App Designer.</span></span>

   ![Разрешать запросы из пользовательского API tooyour конструктор логику приложения](media/logic-apps-custom-hosted-api/custom-api-cors.png)

<span data-ttu-id="9d485-125">Дополнительные сведения вы найдете в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="9d485-125">For more information, see these articles:</span></span>

* [<span data-ttu-id="9d485-126">Использование метаданных и пользовательского интерфейса API Swagger</span><span class="sxs-lookup"><span data-stu-id="9d485-126">Add Swagger metadata for ASP.NET web APIs</span></span>](../app-service-api/app-service-api-dotnet-get-started.md#use-swagger-api-metadata-and-ui)
* [<span data-ttu-id="9d485-127">Развертывание ASP.NET web API-интерфейсы tooAzure службы приложений</span><span class="sxs-lookup"><span data-stu-id="9d485-127">Deploy ASP.NET web APIs tooAzure App Service</span></span>](../app-service-api/app-service-api-dotnet-get-started.md)

## <a name="call-your-custom-api-from-logic-app-workflows"></a><span data-ttu-id="9d485-128">Вызов настраиваемого API из рабочих процессов приложения логики</span><span class="sxs-lookup"><span data-stu-id="9d485-128">Call your custom API from logic app workflows</span></span>

<span data-ttu-id="9d485-129">После настройки свойств определения hello API и CORS триггеров и действий пользовательского интерфейса API должен быть доступен для tooinclude в рабочем процессе логику приложения.</span><span class="sxs-lookup"><span data-stu-id="9d485-129">After you set up hello API definition properties and CORS, your custom API's triggers and actions should become available for you tooinclude in your logic app workflow.</span></span> 

*  <span data-ttu-id="9d485-130">tooview hello веб-сайты, Swagger URL-адресов, перейдите к веб-сайтам подписки в конструкторе логики приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9d485-130">tooview hello websites that have Swagger URLs, you can browse your subscription websites in hello Logic Apps Designer.</span></span>

*  <span data-ttu-id="9d485-131">Доступные действия tooview и входных данных, указав документ Swagger использовать hello [HTTP + Swagger действие](../connectors/connectors-native-http-swagger.md).</span><span class="sxs-lookup"><span data-stu-id="9d485-131">tooview available actions and inputs by pointing at a Swagger document, use hello [HTTP + Swagger action](../connectors/connectors-native-http-swagger.md).</span></span>

*  <span data-ttu-id="9d485-132">toocall любого API, включая интерфейсы API, которые не имеют или предоставления Swagger документа, всегда можно создать запрос с hello [действия HTTP](../connectors/connectors-native-http.md).</span><span class="sxs-lookup"><span data-stu-id="9d485-132">toocall any API, including APIs that don't have or expose a Swagger document, you can always create a request with hello [HTTP action](../connectors/connectors-native-http.md).</span></span>

## <a name="authenticate-calls-tooyour-custom-api"></a><span data-ttu-id="9d485-133">Проверки подлинности вызовов tooyour настраиваемого API</span><span class="sxs-lookup"><span data-stu-id="9d485-133">Authenticate calls tooyour custom API</span></span>

<span data-ttu-id="9d485-134">Можно защитить tooyour вызывает пользовательский API следующими способами:</span><span class="sxs-lookup"><span data-stu-id="9d485-134">You can secure calls tooyour custom API in these ways:</span></span>

* <span data-ttu-id="9d485-135">[Изменения в коде](#no-code): защита API с [Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) через hello портал Azure, поэтому вы не имеют tooupdate кода или повторно API.</span><span class="sxs-lookup"><span data-stu-id="9d485-135">[No code changes](#no-code): Protect your API with [Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) through hello Azure portal, so you don't have tooupdate your code or redeploy your API.</span></span>

  > [!NOTE]
  > <span data-ttu-id="9d485-136">По умолчанию hello проверки подлинности Azure AD, включите hello портал Azure не предоставляет авторизации разного уровня.</span><span class="sxs-lookup"><span data-stu-id="9d485-136">By default, hello Azure AD authentication that you turn on in hello Azure portal doesn't provide fine-grained authorization.</span></span> <span data-ttu-id="9d485-137">Например эта проверка подлинности блокирует вашей toojust API конкретных клиентов, tooa определенного пользователя или приложения.</span><span class="sxs-lookup"><span data-stu-id="9d485-137">For example, this authentication locks your API toojust a specific tenant, not tooa specific user or app.</span></span> 

* <span data-ttu-id="9d485-138">[Обновление кода API.](#update-code). Защитите API, применив [проверку подлинности на основе сертификата](#certificate), [обычную проверку подлинности](#basic) или [проверку подлинности Azure AD](#azure-ad-code) с помощью кода.</span><span class="sxs-lookup"><span data-stu-id="9d485-138">[Update your API's code](#update-code): Protect your API by enforcing [certificate authentication](#certificate), [basic authentication](#basic), or [Azure AD authentication](#azure-ad-code) through code.</span></span>

<a name="no-code"></a>

### <a name="authenticate-calls-tooyour-api-without-changing-code"></a><span data-ttu-id="9d485-139">Проверки подлинности вызовов API tooyour без изменения кода</span><span class="sxs-lookup"><span data-stu-id="9d485-139">Authenticate calls tooyour API without changing code</span></span>

<span data-ttu-id="9d485-140">Вот hello общие действия для этого метода.</span><span class="sxs-lookup"><span data-stu-id="9d485-140">Here's hello general steps for this method:</span></span>

1. <span data-ttu-id="9d485-141">Создайте два [удостоверения приложений Azure Active Directory (Azure AD)](../app-service-api/app-service-api-dotnet-service-principal-auth.md): одно для приложения логики, а другое — для веб-приложения или приложения API.</span><span class="sxs-lookup"><span data-stu-id="9d485-141">Create two [Azure Active Directory (Azure AD) application identities](../app-service-api/app-service-api-dotnet-service-principal-auth.md): one for your logic app and one for your web app (or API app).</span></span>

2. <span data-ttu-id="9d485-142">tooyour tooauthenticate вызовы API, использовать учетные данные hello (идентификатор клиента и секрет) для hello [участника-службы](../app-service-api/app-service-api-dotnet-service-principal-auth.md) , связанную с hello удостоверение приложения Azure AD для логики приложения.</span><span class="sxs-lookup"><span data-stu-id="9d485-142">tooauthenticate calls tooyour API, use hello credentials (client ID and secret) for hello [service principal](../app-service-api/app-service-api-dotnet-service-principal-auth.md) that's associated with hello Azure AD application identity for your logic app.</span></span>

3. <span data-ttu-id="9d485-143">Включите идентификаторы приложений hello в определении логики приложения.</span><span class="sxs-lookup"><span data-stu-id="9d485-143">Include hello application IDs in your logic app definition.</span></span>

#### <a name="part-1-create-an-azure-ad-application-identity-for-your-logic-app"></a><span data-ttu-id="9d485-144">Часть 1. Создание удостоверения приложения Azure AD для приложения логики</span><span class="sxs-lookup"><span data-stu-id="9d485-144">Part 1: Create an Azure AD application identity for your logic app</span></span>

<span data-ttu-id="9d485-145">Логика приложения использует этот приложения для Azure AD identity tooauthenticate от Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d485-145">Your logic app uses this Azure AD application identity tooauthenticate against Azure AD.</span></span> <span data-ttu-id="9d485-146">Имеется только tooset копирование это удостоверение один раз для вашего каталога.</span><span class="sxs-lookup"><span data-stu-id="9d485-146">You only have tooset up this identity one time for your directory.</span></span> <span data-ttu-id="9d485-147">Например, вы можете toouse hello удостоверением для вашего приложения логики, несмотря на то, что можно создавать уникальные идентификаторы для каждого приложения логики.</span><span class="sxs-lookup"><span data-stu-id="9d485-147">For example, you can choose toouse hello same identity for all your logic apps, even though you can create unique identities for each logic app.</span></span> <span data-ttu-id="9d485-148">Можно настроить эти удостоверения в hello портал Azure [классический портал Azure](#app-identity-logic-classic), или используйте [PowerShell](#powershell).</span><span class="sxs-lookup"><span data-stu-id="9d485-148">You can set up these identities in hello Azure portal, [Azure classic portal](#app-identity-logic-classic), or use [PowerShell](#powershell).</span></span>

<span data-ttu-id="9d485-149">**Создайте удостоверение приложения hello логику приложения в hello портал Azure**</span><span class="sxs-lookup"><span data-stu-id="9d485-149">**Create hello application identity for your logic app in hello Azure portal**</span></span>

1. <span data-ttu-id="9d485-150">В hello [портал Azure](https://portal.azure.com "https://portal.azure.com"), выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9d485-150">In hello [Azure portal](https://portal.azure.com "https://portal.azure.com"), choose **Azure Active Directory**.</span></span> 

2. <span data-ttu-id="9d485-151">Убедитесь, что вы являетесь в hello же каталоге, что веб-приложения или приложения API.</span><span class="sxs-lookup"><span data-stu-id="9d485-151">Confirm that you're in hello same directory as your web app or API app.</span></span>

   > [!TIP]
   > <span data-ttu-id="9d485-152">каталоги tooswitch выберите свой профиль и выберите другой каталог.</span><span class="sxs-lookup"><span data-stu-id="9d485-152">tooswitch directories, click your profile and select another directory.</span></span> <span data-ttu-id="9d485-153">Или выберите **Обзор** > **Переключение каталога**.</span><span class="sxs-lookup"><span data-stu-id="9d485-153">Or, choose **Overview** > **Switch directory**.</span></span>

3. <span data-ttu-id="9d485-154">В меню "directory" hello под **управление**, выберите **регистрации приложения** > **Регистрация нового приложения**.</span><span class="sxs-lookup"><span data-stu-id="9d485-154">On hello directory menu, under **Manage**, choose **App registrations** > **New application registration**.</span></span>

   > [!TIP]
   > <span data-ttu-id="9d485-155">По умолчанию hello приложения регистраций перечислены все регистрации приложения в каталоге.</span><span class="sxs-lookup"><span data-stu-id="9d485-155">By default, hello app registrations list shows all app registrations in your directory.</span></span> <span data-ttu-id="9d485-156">Выберите только ваши приложения регистрации, поискового Далее toohello tooview **Мои приложения**.</span><span class="sxs-lookup"><span data-stu-id="9d485-156">tooview only your app registrations, next toohello search box, select **My apps**.</span></span> 

   ![Создание регистрации приложения](./media/logic-apps-custom-hosted-api/new-app-registration-azure-portal.png)

4. <span data-ttu-id="9d485-158">Присвойте имя вашего удостоверения приложения, оставьте **тип приложения** значение слишком**веб-приложения и API**, укажите уникальный строку в формате домен для **URL-адрес входа**и выберите  **Создание**.</span><span class="sxs-lookup"><span data-stu-id="9d485-158">Give your application identity a name, leave **Application type** set too**Web app / API**, provide a unique string formatted as a domain for **Sign-on URL**, and choose **Create**.</span></span>

   ![Указание имени и URL-адреса входа для удостоверения приложения](./media/logic-apps-custom-hosted-api/logic-app-identity-azure-portal.png)

   <span data-ttu-id="9d485-160">удостоверения приложения Hello, созданный для логики приложения, теперь отображается в списке регистрации приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9d485-160">hello application identity that you created for your logic app now appears in hello app registrations list.</span></span>

   ![Удостоверение приложения логики](./media/logic-apps-custom-hosted-api/logic-app-identity-created.png)

5. <span data-ttu-id="9d485-162">В списке регистрации приложения hello выберите нового удостоверения приложения.</span><span class="sxs-lookup"><span data-stu-id="9d485-162">In hello app registrations list, select your new application identity.</span></span> <span data-ttu-id="9d485-163">Скопируйте и сохраните hello **идентификатор приложения** toouse как Здравствуйте, «идентификатор клиента» для логики приложения в часть 3.</span><span class="sxs-lookup"><span data-stu-id="9d485-163">Copy and save hello **Application ID** toouse as hello "client ID" for your logic app in Part 3.</span></span>

   ![Копирование и сохранение идентификатора приложения для приложения логики](./media/logic-apps-custom-hosted-api/logic-app-application-id.png)

6. <span data-ttu-id="9d485-165">Если параметры удостоверения приложения не отображаются, щелкните **Параметры** или **Все параметры**.</span><span class="sxs-lookup"><span data-stu-id="9d485-165">If your application identity settings aren't visible, choose **Settings** or **All settings**.</span></span>

7. <span data-ttu-id="9d485-166">В разделе **Доступ через API** выберите **Ключи**.</span><span class="sxs-lookup"><span data-stu-id="9d485-166">Under **API Access**, choose **Keys**.</span></span> <span data-ttu-id="9d485-167">В поле **Описание** введите имя для ключа.</span><span class="sxs-lookup"><span data-stu-id="9d485-167">Under **Description**, provide a name for your key.</span></span> <span data-ttu-id="9d485-168">Выберите **срок действия** ключа в соответствующем поле.</span><span class="sxs-lookup"><span data-stu-id="9d485-168">Under **Expires**, select a duration for your key.</span></span>

   <span data-ttu-id="9d485-169">Hello ключ, который вы создаете выступает в качестве удостоверения приложения hello «секретный» или пароль для логики приложения.</span><span class="sxs-lookup"><span data-stu-id="9d485-169">hello key that you're creating acts as hello application identity's "secret" or password for your logic app.</span></span>

   ![Создание ключа для удостоверения приложения логики](./media/logic-apps-custom-hosted-api/create-logic-app-identity-key-secret-password.png)

8. <span data-ttu-id="9d485-171">На панели инструментов hello, выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="9d485-171">On hello toolbar, choose **Save**.</span></span> <span data-ttu-id="9d485-172">Ключ отобразится в разделе **Значение**.</span><span class="sxs-lookup"><span data-stu-id="9d485-172">Under **Value**, your key now appears.</span></span> 
<span data-ttu-id="9d485-173">**Убедитесь, что toocopy и сохраните ключ** для последующего использования так как ключ hello скрыта Если оставить hello ключа колонки.</span><span class="sxs-lookup"><span data-stu-id="9d485-173">**Make sure toocopy and save your key** for later use because hello key is hidden when you leave hello key blade.</span></span>

   <span data-ttu-id="9d485-174">При настройке приложения логики в часть 3, укажите этот ключ как Здравствуйте, «секретный» или пароль.</span><span class="sxs-lookup"><span data-stu-id="9d485-174">When you configure your logic app in Part 3, you specify this key as hello "secret" or password.</span></span>

   ![Копирование и сохранение ключа для дальнейшего использования](./media/logic-apps-custom-hosted-api/logic-app-copy-key-secret-password.png)

<a name="app-identity-logic-classic"></a>

<span data-ttu-id="9d485-176">**Создайте удостоверение приложения hello логику приложения в hello классический портал Azure**</span><span class="sxs-lookup"><span data-stu-id="9d485-176">**Create hello application identity for your logic app in hello Azure classic portal**</span></span>

1. <span data-ttu-id="9d485-177">В hello классический портал Azure, выберите [ **Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span><span class="sxs-lookup"><span data-stu-id="9d485-177">In hello Azure classic portal, choose [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span></span>

2. <span data-ttu-id="9d485-178">Выберите hello же каталоге, который используется для веб-приложения или приложения API.</span><span class="sxs-lookup"><span data-stu-id="9d485-178">Select hello same directory that you use for your web app or API app.</span></span>

3. <span data-ttu-id="9d485-179">На hello **приложений** выберите **добавить** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="9d485-179">On hello **Applications** tab, choose **Add** at hello bottom of hello page.</span></span>

4. <span data-ttu-id="9d485-180">Присвойте удостоверению приложения имя и щелкните **Далее** (стрелка вправо).</span><span class="sxs-lookup"><span data-stu-id="9d485-180">Give your application identity a name, and choose **Next** (right arrow).</span></span>

5. <span data-ttu-id="9d485-181">В разделе **Свойства приложения** укажите уникальную строку в формате домена для параметров **URL-адрес для входа** и **URI кода приложения** и щелкните **Завершено** (значок флажка).</span><span class="sxs-lookup"><span data-stu-id="9d485-181">Under **App properties**, provide a unique string formatted as a domain for **Sign-on URL** and **App ID URI**, and choose **Complete** (checkmark).</span></span>

6. <span data-ttu-id="9d485-182">На hello **Настройка** вкладки, скопируйте и сохраните hello **идентификатор клиента** для вашей toouse приложения логики в часть 3.</span><span class="sxs-lookup"><span data-stu-id="9d485-182">On hello **Configure** tab, copy and save hello **Client ID** for your logic app toouse in Part 3.</span></span>

7. <span data-ttu-id="9d485-183">В разделе **ключей**откройте hello **выберите длительность** списка.</span><span class="sxs-lookup"><span data-stu-id="9d485-183">Under **Keys**, open hello **Select duration** list.</span></span> <span data-ttu-id="9d485-184">Выберите срок действия ключа.</span><span class="sxs-lookup"><span data-stu-id="9d485-184">Select a duration for your key.</span></span>

   <span data-ttu-id="9d485-185">Hello ключ, который вы создаете выступает в качестве удостоверения приложения hello «секретный» или пароль для логики приложения.</span><span class="sxs-lookup"><span data-stu-id="9d485-185">hello key that you're creating acts as hello application identity's "secret" or password for your logic app.</span></span>

8. <span data-ttu-id="9d485-186">Hello нижней части страницы приветствия, выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="9d485-186">At hello bottom of hello page, choose **Save**.</span></span> <span data-ttu-id="9d485-187">Может потребоваться toowait через несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="9d485-187">You might have toowait a few seconds.</span></span>

9. <span data-ttu-id="9d485-188">В разделе **ключей**, убедитесь, что toocopy и сохранить ключ hello, теперь отображается.</span><span class="sxs-lookup"><span data-stu-id="9d485-188">Under **Keys**, make sure toocopy and save hello key that now appears.</span></span> 

   <span data-ttu-id="9d485-189">При настройке приложения логики в часть 3, укажите этот ключ как Здравствуйте, «секретный» или пароль.</span><span class="sxs-lookup"><span data-stu-id="9d485-189">When you configure your logic app in Part 3, you specify this key as hello "secret" or password.</span></span>

<span data-ttu-id="9d485-190">Дополнительные сведения, узнайте, как слишком [Настройка имени входа Azure Active Directory toouse приложения службы приложений](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="9d485-190">For more information, learn how too [configure your App Service application toouse Azure Active Directory login](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span>

<a name="powershell"></a>

<span data-ttu-id="9d485-191">**Создать удостоверение приложения hello логику приложения в PowerShell**</span><span class="sxs-lookup"><span data-stu-id="9d485-191">**Create hello application identity for your logic app in PowerShell**</span></span>

<span data-ttu-id="9d485-192">Эту задачу можно выполнить в Azure Resource Manager с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9d485-192">You can perform this task through Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="9d485-193">Выполните следующие команды в PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9d485-193">In PowerShell, run these commands:</span></span>

1. `Switch-AzureMode AzureResourceManager`

2. `Add-AzureAccount`

3. `New-AzureADApplication -DisplayName "MyLogicAppID" -HomePage "http://mydomain.tld" -IdentifierUris "http://mydomain.tld" -Password "identity-password"`

4. <span data-ttu-id="9d485-194">Убедитесь, что hello toocopy **ИД клиента** hello (идентификатор GUID для клиента Azure AD), **идентификатор приложения**и hello пароль, который использовался.</span><span class="sxs-lookup"><span data-stu-id="9d485-194">Make sure toocopy hello **Tenant ID** (GUID for your Azure AD tenant), hello **Application ID**, and hello password that you used.</span></span>

<span data-ttu-id="9d485-195">Дополнительные сведения, узнайте, как слишком [создать участника службы с ресурсами tooaccess PowerShell](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="9d485-195">For more information, learn how too [create a service principal with PowerShell tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

#### <a name="part-2-create-an-azure-ad-application-identity-for-your-web-app-or-api-app"></a><span data-ttu-id="9d485-196">Часть 2. Создание удостоверения приложения Azure AD для веб-приложения или приложения API</span><span class="sxs-lookup"><span data-stu-id="9d485-196">Part 2: Create an Azure AD application identity for your web app or API app</span></span>

<span data-ttu-id="9d485-197">Если веб-приложения или приложения API уже развернута, можно включить проверку подлинности и создать удостоверение приложения hello в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="9d485-197">If your web app or API app is already deployed, you can turn on authentication and create hello application identity in hello Azure portal.</span></span> <span data-ttu-id="9d485-198">В противном случае вы можете [включить проверку подлинности при развертывании с использованием шаблона Azure Resource Manager](#authen-deploy).</span><span class="sxs-lookup"><span data-stu-id="9d485-198">Otherwise, you can [turn on authentication when you deploy with an Azure Resource Manager template](#authen-deploy).</span></span> 

<span data-ttu-id="9d485-199">**Создайте удостоверение приложения hello и включите проверку подлинности в hello портал Azure для развернутых приложений**</span><span class="sxs-lookup"><span data-stu-id="9d485-199">**Create hello application identity and turn on authentication in hello Azure portal for deployed apps**</span></span>

1. <span data-ttu-id="9d485-200">В hello [портал Azure](https://portal.azure.com "https://portal.azure.com"), найдите и выберите веб-приложения или приложения API.</span><span class="sxs-lookup"><span data-stu-id="9d485-200">In hello [Azure portal](https://portal.azure.com "https://portal.azure.com"), find and select your web app or API app.</span></span> 

2. <span data-ttu-id="9d485-201">В разделе **Параметры** выберите **Аутентификация или авторизация**.</span><span class="sxs-lookup"><span data-stu-id="9d485-201">Under **Settings**, choose **Authentication/Authorization**.</span></span> <span data-ttu-id="9d485-202">В разделе **Проверка подлинности службы приложений** включите проверку подлинности, нажав кнопку **Вкл.**</span><span class="sxs-lookup"><span data-stu-id="9d485-202">Under **App Service Authentication**, turn authentication **On**.</span></span> <span data-ttu-id="9d485-203">В разделе **Поставщики проверки подлинности** щелкните **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9d485-203">Under **Authentication Providers**, choose **Azure Active Directory**.</span></span>

   ![Включение проверки подлинности](./media/logic-apps-custom-hosted-api/custom-web-api-app-authentication.png)

3. <span data-ttu-id="9d485-205">Теперь создайте удостоверение приложения для веб-приложения или приложения API, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="9d485-205">Now create an application identity for your web app or API app as shown here.</span></span> <span data-ttu-id="9d485-206">На hello **параметры Azure Active Directory** задать колонке **режим управления** слишком**Express**.</span><span class="sxs-lookup"><span data-stu-id="9d485-206">On hello **Azure Active Directory Settings** blade, set **Management mode** too**Express**.</span></span> <span data-ttu-id="9d485-207">Щелкните **Создать новое приложение AD**.</span><span class="sxs-lookup"><span data-stu-id="9d485-207">Choose **Create New AD App**.</span></span> <span data-ttu-id="9d485-208">Присвойте удостоверению приложения имя и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9d485-208">Give your application identity a name, and choose **OK**.</span></span> 

   ![Создание удостоверения приложения для веб-приложения или приложения API](./media/logic-apps-custom-hosted-api/custom-api-application-identity.png)

4. <span data-ttu-id="9d485-210">На hello **проверки подлинности и авторизации колонке**, выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="9d485-210">On hello **Authentication / Authorization blade**, choose **Save**.</span></span>

<span data-ttu-id="9d485-211">Теперь необходимо найти идентификатор клиента hello и идентификатор клиента для удостоверения приложения hello, связанный с веб-приложения или приложения API.</span><span class="sxs-lookup"><span data-stu-id="9d485-211">Now you must find hello client ID and tenant ID for hello application identity that's associated with your web app or API app.</span></span> <span data-ttu-id="9d485-212">Используйте эти идентификаторы в части 3.</span><span class="sxs-lookup"><span data-stu-id="9d485-212">You use these IDs in Part 3.</span></span> <span data-ttu-id="9d485-213">Поэтому выполните следующие действия для hello портал Azure или [классический портал Azure](#find-id-classic).</span><span class="sxs-lookup"><span data-stu-id="9d485-213">So continue with these steps for hello Azure portal or [Azure classic portal](#find-id-classic).</span></span>

<span data-ttu-id="9d485-214">**Найти идентификатор клиента удостоверения приложения и идентификатор клиента для веб-приложения или приложения API в hello портал Azure**</span><span class="sxs-lookup"><span data-stu-id="9d485-214">**Find application identity's client ID and tenant ID for your web app or API app in hello Azure portal**</span></span>

1. <span data-ttu-id="9d485-215">В разделе **Поставщики проверки подлинности** щелкните **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9d485-215">Under **Authentication Providers**, choose **Azure Active Directory**.</span></span> 

   ![Выбор элемента Azure Active Directory](./media/logic-apps-custom-hosted-api/custom-api-app-identity-client-id-tenant-id.png)

2. <span data-ttu-id="9d485-217">На hello **параметры Azure Active Directory** задать колонке **режим управления** слишком**Дополнительно**.</span><span class="sxs-lookup"><span data-stu-id="9d485-217">On hello **Azure Active Directory Settings** blade, set **Management mode** too**Advanced**.</span></span>

3. <span data-ttu-id="9d485-218">Копировать hello **идентификатор клиента**и сохраните этот идентификатор GUID для использования в часть 3.</span><span class="sxs-lookup"><span data-stu-id="9d485-218">Copy hello **Client ID**, and save that GUID for use in Part 3.</span></span>

   > [!TIP] 
   > <span data-ttu-id="9d485-219">Если **идентификатор клиента** и **URL-адрес издателя** не отображаются, попробуйте обновить hello портал Azure и повторите шаг 1.</span><span class="sxs-lookup"><span data-stu-id="9d485-219">If **Client ID** and **Issuer Url** don't appear, try refreshing hello Azure portal, and repeat Step 1.</span></span>

4. <span data-ttu-id="9d485-220">В разделе **URL-адрес издателя**, скопируйте и сохраните только hello GUID для часть 3.</span><span class="sxs-lookup"><span data-stu-id="9d485-220">Under **Issuer Url**, copy and save just hello GUID for Part 3.</span></span> <span data-ttu-id="9d485-221">При необходимости вы также можете использовать этот GUID в шаблоне развертывания веб-приложения или приложения API.</span><span class="sxs-lookup"><span data-stu-id="9d485-221">You can also use this GUID in your web app or API app's deployment template, if necessary.</span></span>

   <span data-ttu-id="9d485-222">Этот GUID — идентификатор определенного арендатора (ИД арендатора), который должен отображаться в следующем URL-адресе: `https://sts.windows.net/{GUID}`</span><span class="sxs-lookup"><span data-stu-id="9d485-222">This GUID is your specific tenant's GUID ("tenant ID") and should appear in this URL: `https://sts.windows.net/{GUID}`</span></span>

5. <span data-ttu-id="9d485-223">Без сохранения изменений, закройте hello **параметры Azure Active Directory** колонку.</span><span class="sxs-lookup"><span data-stu-id="9d485-223">Without saving your changes, close hello **Azure Active Directory Settings** blade.</span></span>

<a name="find-id-classic"></a>

<span data-ttu-id="9d485-224">**Найти идентификатор клиента удостоверения приложения и идентификатор клиента для веб-приложения или приложения API в hello классический портал Azure**</span><span class="sxs-lookup"><span data-stu-id="9d485-224">**Find application identity's client ID and tenant ID for your web app or API app in hello Azure classic portal**</span></span>

1. <span data-ttu-id="9d485-225">В hello классический портал Azure, выберите [ **Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span><span class="sxs-lookup"><span data-stu-id="9d485-225">In hello Azure classic portal, choose [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span></span>

2.  <span data-ttu-id="9d485-226">Выберите каталог hello, используемого для веб-приложения или приложения API.</span><span class="sxs-lookup"><span data-stu-id="9d485-226">Select hello directory that you use for your web app or API app.</span></span>

3. <span data-ttu-id="9d485-227">В hello **поиска** , найдите и выберите удостоверение приложения hello для веб-приложения или приложения API.</span><span class="sxs-lookup"><span data-stu-id="9d485-227">In hello **Search** box, find and select hello application identity for your web app or API app.</span></span>

4. <span data-ttu-id="9d485-228">На hello **Настройка** вкладка, hello копирования **идентификатор клиента**и сохраните этот идентификатор GUID для использования в часть 3.</span><span class="sxs-lookup"><span data-stu-id="9d485-228">On hello **Configure** tab, copy hello **Client ID**, and save that GUID for use in Part 3.</span></span>

5. <span data-ttu-id="9d485-229">После получения идентификатора клиента hello, внизу hello hello **Настройка** выберите **просмотреть конечные точки**.</span><span class="sxs-lookup"><span data-stu-id="9d485-229">After you get hello client ID, at hello bottom of hello **Configure** tab, choose **View endpoints**.</span></span>

6. <span data-ttu-id="9d485-230">Скопируйте URL-адрес hello **документа метаданных федерации**и найдите toothat URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="9d485-230">Copy hello URL for **Federation Metadata Document**, and browse toothat URL.</span></span>

7. <span data-ttu-id="9d485-231">В документе метаданных hello, которое открывается, найти корень hello **идентификатор EntityDescriptor** элемент, который имеет **entityID** атрибут в этой форме:`https://sts.windows.net/{GUID}`</span><span class="sxs-lookup"><span data-stu-id="9d485-231">In hello metadata document that opens, find hello root **EntityDescriptor ID** element, which has an **entityID** attribute in this form: `https://sts.windows.net/{GUID}`</span></span> 

      <span data-ttu-id="9d485-232">Hello GUID в этот атрибут представляет идентификатор GUID конкретных клиентов (Идентификатором клиента).</span><span class="sxs-lookup"><span data-stu-id="9d485-232">hello GUID in this attribute is your specific tenant's GUID (tenant ID).</span></span>

8. <span data-ttu-id="9d485-233">Скопируйте идентификатор клиента hello и при необходимости сохранить этот идентификатор для использования в часть 3, а также toouse в веб-приложения или приложения API развертывания шаблона.</span><span class="sxs-lookup"><span data-stu-id="9d485-233">Copy hello tenant ID and save that ID for use in Part 3, and also toouse in your web app or API app's deployment template, if necessary.</span></span>

<span data-ttu-id="9d485-234">Дополнительные сведения см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="9d485-234">For more information, see these topics:</span></span>

* [<span data-ttu-id="9d485-235">Проверка подлинности пользователя для приложений API в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="9d485-235">User authentication for API apps in Azure App Service</span></span>](../app-service-api/app-service-api-dotnet-user-principal-auth.md)
* [<span data-ttu-id="9d485-236">Проверка подлинности и авторизация в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="9d485-236">Authentication and authorization in Azure App Service</span></span>](../app-service/app-service-authentication-overview.md)

<a name="authen-deploy"></a>

<span data-ttu-id="9d485-237">**Проверка подлинности и авторизация в службе приложений Azure**</span><span class="sxs-lookup"><span data-stu-id="9d485-237">**Turn on authentication when you deploy with an Azure Resource Manager template**</span></span>

<span data-ttu-id="9d485-238">По-прежнему необходимо создать удостоверение приложения Azure AD для веб-приложения или приложения API, который отличается от удостоверения приложения hello логику приложения.</span><span class="sxs-lookup"><span data-stu-id="9d485-238">You must still create an Azure AD application identity for your web app or API app that differs from hello app identity for your logic app.</span></span> <span data-ttu-id="9d485-239">удостоверение приложения hello toocreate, выполните hello предыдущих шагов во второй части hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="9d485-239">toocreate hello application identity, follow hello previous steps in Part 2 for hello Azure portal.</span></span> <span data-ttu-id="9d485-240">Вы можно также выполните действия hello в части 1, но необходимо убедиться, что toouse вашего веб-приложения или приложения API фактического `https://{URL}` для **URL-адрес входа** и **URI идентификатора приложения**.</span><span class="sxs-lookup"><span data-stu-id="9d485-240">You can also follow hello steps in Part 1, but make sure toouse your web app or API app's actual `https://{URL}` for **Sign-on URL** and **App ID URI**.</span></span> <span data-ttu-id="9d485-241">Данные этих шагов имеется toosave клиенте hello код и код клиента для использования в шаблон развертывания приложения, а также для часть 3.</span><span class="sxs-lookup"><span data-stu-id="9d485-241">From these steps, you have toosave both hello client ID and tenant ID for use in your app's deployment template and also for Part 3.</span></span>

> [!NOTE]
> <span data-ttu-id="9d485-242">При создании удостоверения приложения hello Azure AD для веб-приложения или приложения API, необходимо использовать портал Azure hello или классический портал Azure, а не в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9d485-242">When you create hello Azure AD application identity for your web app or API app, you must use hello Azure portal or Azure classic portal, rather than PowerShell.</span></span> <span data-ttu-id="9d485-243">командлет PowerShell Hello не Настройка hello необходимых разрешений toosign пользователей в веб-сайт.</span><span class="sxs-lookup"><span data-stu-id="9d485-243">hello PowerShell commandlet doesn't set up hello required permissions toosign users into a website.</span></span>

<span data-ttu-id="9d485-244">После получения идентификатора клиента hello и ИД клиента включить эти идентификаторы subresource вашего веб-приложения или приложения API в шаблон развертывания.</span><span class="sxs-lookup"><span data-stu-id="9d485-244">After you get hello client ID and tenant ID, include these IDs as a subresource of your web app or API app in your deployment template:</span></span>

   ```
   "resources": [
       {
           "apiVersion": "2015-08-01",
           "name": "web",
           "type": "config",
           "dependsOn": ["[concat('Microsoft.Web/sites/','parameters('webAppName'))]"],
           "properties": {
               "siteAuthEnabled": true,
               "siteAuthSettings": {
                 "clientId": "{client-ID}",
                 "issuer": "https://sts.windows.net/{tenant-ID}/",
               }
           }
       }
   ]
   ```

<span data-ttu-id="9d485-245">Развертывание tooautomatically пустой веб-приложения и приложения логики, а также проверки подлинности Azure Active Directory, [hello полный шаблон представления здесь](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json), или нажмите кнопку **развертывание tooAzure** здесь:</span><span class="sxs-lookup"><span data-stu-id="9d485-245">tooautomatically deploy a blank web app and a logic app together with Azure Active Directory authentication, [view hello complete template here](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json), or click **Deploy tooAzure** here:</span></span>

<span data-ttu-id="9d485-246">[![Развертывание tooAzure](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="9d485-246">[![Deploy tooAzure](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)</span></span>

#### <a name="part-3-populate-hello-authorization-section-in-your-logic-app"></a><span data-ttu-id="9d485-247">Часть 3: Заполнение hello раздела авторизации в приложении логики</span><span class="sxs-lookup"><span data-stu-id="9d485-247">Part 3: Populate hello Authorization section in your logic app</span></span>

<span data-ttu-id="9d485-248">Hello предыдущем шаблоне уже есть в этом разделе авторизации, настройки, но при разработке приложения hello логики напрямую, необходимо включить раздел hello полные права.</span><span class="sxs-lookup"><span data-stu-id="9d485-248">hello previous template already has this authorization section set up, but if you are directly authoring hello logic app, you must include hello full authorization section.</span></span>

<span data-ttu-id="9d485-249">Откройте определение приложения логики в представлении кода, последовательно выберите toohello **HTTP** раздел действия, найти hello **авторизации** раздела и включить эту строку:</span><span class="sxs-lookup"><span data-stu-id="9d485-249">Open your logic app definition in code view, go toohello **HTTP** action section, find hello **Authorization** section, and include this line:</span></span>

`{"tenant": "{tenant-ID}", "audience": "{client-ID-from-Part-2-web-app-or-API app}", "clientId": "{client-ID-from-Part-1-logic-app}", "secret": "{key-from-Part-1-logic-app}", "type": "ActiveDirectoryOAuth" }`

| <span data-ttu-id="9d485-250">Элемент</span><span class="sxs-lookup"><span data-stu-id="9d485-250">Element</span></span> | <span data-ttu-id="9d485-251">Описание</span><span class="sxs-lookup"><span data-stu-id="9d485-251">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="9d485-252">tenant</span><span class="sxs-lookup"><span data-stu-id="9d485-252">tenant</span></span> |<span data-ttu-id="9d485-253">Hello GUID для клиента hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d485-253">hello GUID for hello Azure AD tenant</span></span> |
| <span data-ttu-id="9d485-254">audience</span><span class="sxs-lookup"><span data-stu-id="9d485-254">audience</span></span> |<span data-ttu-id="9d485-255">Обязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="9d485-255">Required.</span></span> <span data-ttu-id="9d485-256">Hello GUID для hello целевого ресурса, которые должны tooaccess - hello идентификатор клиента из удостоверения приложения hello для веб-приложения или приложения API</span><span class="sxs-lookup"><span data-stu-id="9d485-256">hello GUID for hello target resource that you want tooaccess - hello client ID from hello application identity for your web app or API app</span></span> |
| <span data-ttu-id="9d485-257">clientid</span><span class="sxs-lookup"><span data-stu-id="9d485-257">clientId</span></span> |<span data-ttu-id="9d485-258">Hello GUID для клиента hello, запрашивающие доступ - hello идентификатор клиента из удостоверения приложения hello логику приложения</span><span class="sxs-lookup"><span data-stu-id="9d485-258">hello GUID for hello client requesting access - hello client ID from hello application identity for your logic app</span></span> |
| <span data-ttu-id="9d485-259">secret</span><span class="sxs-lookup"><span data-stu-id="9d485-259">secret</span></span> |<span data-ttu-id="9d485-260">Обязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="9d485-260">Required.</span></span> <span data-ttu-id="9d485-261">Hello ключ или пароль из удостоверения приложения hello для hello клиента, который запрашивает токен доступа hello</span><span class="sxs-lookup"><span data-stu-id="9d485-261">hello key or password from hello application identity for hello client that's requesting hello access token</span></span> |
| <span data-ttu-id="9d485-262">type</span><span class="sxs-lookup"><span data-stu-id="9d485-262">type</span></span> |<span data-ttu-id="9d485-263">Тип проверки подлинности Hello.</span><span class="sxs-lookup"><span data-stu-id="9d485-263">hello authentication type.</span></span> <span data-ttu-id="9d485-264">Для проверки подлинности activedirectoryoauth используется значение hello — `ActiveDirectoryOAuth`.</span><span class="sxs-lookup"><span data-stu-id="9d485-264">For ActiveDirectoryOAuth authentication, hello value is `ActiveDirectoryOAuth`.</span></span> |

<span data-ttu-id="9d485-265">Например:</span><span class="sxs-lookup"><span data-stu-id="9d485-265">For example:</span></span>

```
{
   ...
   "actions": {
      "some-action": {
         "conditions": [],
         "inputs": {
            "method": "post",
            "uri": "https://your-api-azurewebsites.net/api/your-method",
            "authentication": {
               "tenant": "tenant-ID",
               "audience": "client-ID-from-azure-ad-app-for-web-app-or-api-app",
               "clientId": "client-ID-from-azure-ad-app-for-logic-app",
               "secret": "key-from-azure-ad-app-for-logic-app",
               "type": "ActiveDirectoryOAuth"
            }
         },
      }
   }
}
```

<a name="update-code"></a>

### <a name="secure-api-calls-through-code"></a><span data-ttu-id="9d485-266">Безопасные вызовы API с помощью кода</span><span class="sxs-lookup"><span data-stu-id="9d485-266">Secure API calls through code</span></span>

<a name="certificate"></a>

#### <a name="certificate-authentication"></a><span data-ttu-id="9d485-267">Проверка подлинности на основе сертификата</span><span class="sxs-lookup"><span data-stu-id="9d485-267">Certificate authentication</span></span>

<span data-ttu-id="9d485-268">toovalidate hello входящие запросы от логики приложения tooyour веб-приложения или приложения API, можно использовать клиентские сертификаты.</span><span class="sxs-lookup"><span data-stu-id="9d485-268">toovalidate hello incoming requests from your logic app tooyour web app or API app, you can use client certificates.</span></span> <span data-ttu-id="9d485-269">tooset код, узнайте [как взаимная проверка подлинности TLS tooconfigure](../app-service-web/app-service-web-configure-tls-mutual-auth.md).</span><span class="sxs-lookup"><span data-stu-id="9d485-269">tooset up your code, learn [how tooconfigure TLS mutual authentication](../app-service-web/app-service-web-configure-tls-mutual-auth.md).</span></span>

<span data-ttu-id="9d485-270">В hello **авторизации** статьи, включите эту строку:</span><span class="sxs-lookup"><span data-stu-id="9d485-270">In hello **Authorization** section, include this line:</span></span> 

`{"type": "clientcertificate", "password": "password", "pfx": "long-pfx-key"}`

| <span data-ttu-id="9d485-271">Элемент</span><span class="sxs-lookup"><span data-stu-id="9d485-271">Element</span></span> | <span data-ttu-id="9d485-272">Описание</span><span class="sxs-lookup"><span data-stu-id="9d485-272">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="9d485-273">type</span><span class="sxs-lookup"><span data-stu-id="9d485-273">type</span></span> |<span data-ttu-id="9d485-274">Обязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="9d485-274">Required.</span></span> <span data-ttu-id="9d485-275">Тип проверки подлинности Hello.</span><span class="sxs-lookup"><span data-stu-id="9d485-275">hello authentication type.</span></span> <span data-ttu-id="9d485-276">Для SSL-сертификатов клиента, hello значение должно быть `ClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="9d485-276">For SSL client certificates, hello value must be `ClientCertificate`.</span></span> |
| <span data-ttu-id="9d485-277">пароль</span><span class="sxs-lookup"><span data-stu-id="9d485-277">password</span></span> |<span data-ttu-id="9d485-278">Обязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="9d485-278">Required.</span></span> <span data-ttu-id="9d485-279">Hello пароль для доступа к hello клиентский сертификат (PFX-файла)</span><span class="sxs-lookup"><span data-stu-id="9d485-279">hello password for accessing hello client certificate (PFX file)</span></span> |
| <span data-ttu-id="9d485-280">pfx</span><span class="sxs-lookup"><span data-stu-id="9d485-280">pfx</span></span> |<span data-ttu-id="9d485-281">Обязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="9d485-281">Required.</span></span> <span data-ttu-id="9d485-282">Содержимое base64-кодированном hello клиентский сертификат (PFX-файла)</span><span class="sxs-lookup"><span data-stu-id="9d485-282">Base64-encoded contents of hello client certificate (PFX file)</span></span> |

<a name="basic"></a>

#### <a name="basic-authentication"></a><span data-ttu-id="9d485-283">Обычная аутентификация</span><span class="sxs-lookup"><span data-stu-id="9d485-283">Basic authentication</span></span>

<span data-ttu-id="9d485-284">toovalidate входящие запросы от логики приложения tooyour веб-приложения или приложения API, можно использовать обычную проверку подлинности, такие как имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="9d485-284">toovalidate incoming requests from your logic app tooyour web app or API app, you can use basic authentication, such as a username and password.</span></span> <span data-ttu-id="9d485-285">Обычная проверка подлинности — это общий шаблон и использовании проверки подлинности в любой язык, используемый toobuild веб-приложения или приложения API.</span><span class="sxs-lookup"><span data-stu-id="9d485-285">Basic authentication is a common pattern, and you can use this authentication in any language used toobuild your web app or API app.</span></span>

<span data-ttu-id="9d485-286">В hello **авторизации** статьи, включите эту строку:</span><span class="sxs-lookup"><span data-stu-id="9d485-286">In hello **Authorization** section, include this line:</span></span>

<span data-ttu-id="9d485-287">`{"type": "basic", "username": "username", "password": "password"}`.</span><span class="sxs-lookup"><span data-stu-id="9d485-287">`{"type": "basic", "username": "username", "password": "password"}`.</span></span>

| <span data-ttu-id="9d485-288">Элемент</span><span class="sxs-lookup"><span data-stu-id="9d485-288">Element</span></span> | <span data-ttu-id="9d485-289">Описание</span><span class="sxs-lookup"><span data-stu-id="9d485-289">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9d485-290">type</span><span class="sxs-lookup"><span data-stu-id="9d485-290">type</span></span> |<span data-ttu-id="9d485-291">Обязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="9d485-291">Required.</span></span> <span data-ttu-id="9d485-292">Тип проверки подлинности Hello.</span><span class="sxs-lookup"><span data-stu-id="9d485-292">hello authentication type.</span></span> <span data-ttu-id="9d485-293">Для обычной проверки подлинности должно быть значение hello `Basic`.</span><span class="sxs-lookup"><span data-stu-id="9d485-293">For basic authentication, hello value must be `Basic`.</span></span> |
| <span data-ttu-id="9d485-294">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="9d485-294">username</span></span> |<span data-ttu-id="9d485-295">Обязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="9d485-295">Required.</span></span> <span data-ttu-id="9d485-296">Hello имя пользователя для проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="9d485-296">hello username for authentication</span></span> |
| <span data-ttu-id="9d485-297">пароль</span><span class="sxs-lookup"><span data-stu-id="9d485-297">password</span></span> |<span data-ttu-id="9d485-298">Обязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="9d485-298">Required.</span></span> <span data-ttu-id="9d485-299">Hello пароль для проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="9d485-299">hello password for authentication</span></span> |

<a name="azure-ad-code"></a>

#### <a name="azure-active-directory-authentication-through-code"></a><span data-ttu-id="9d485-300">Проверка подлинности Azure Active Directory с помощью кода</span><span class="sxs-lookup"><span data-stu-id="9d485-300">Azure Active Directory authentication through code</span></span>

<span data-ttu-id="9d485-301">По умолчанию hello проверки подлинности Azure AD, включите hello портал Azure не предоставляет авторизации разного уровня.</span><span class="sxs-lookup"><span data-stu-id="9d485-301">By default, hello Azure AD authentication that you turn on in hello Azure portal doesn't provide fine-grained authorization.</span></span> <span data-ttu-id="9d485-302">Например эта проверка подлинности блокирует вашей toojust API конкретных клиентов, tooa определенного пользователя или приложения.</span><span class="sxs-lookup"><span data-stu-id="9d485-302">For example, this authentication locks your API toojust a specific tenant, not tooa specific user or app.</span></span> 

<span data-ttu-id="9d485-303">приложения логики tooyour toorestrict API-Интерфейс доступа по коду, извлеките hello заголовок, который имеет hello веб-токен JSON (JWT).</span><span class="sxs-lookup"><span data-stu-id="9d485-303">toorestrict API access tooyour logic app through code, extract hello header that has hello JSON web token (JWT).</span></span> <span data-ttu-id="9d485-304">Проверьте hello удостоверение и отклонять запросы, которые не соответствуют друг другу.</span><span class="sxs-lookup"><span data-stu-id="9d485-304">Check hello caller's identity, and reject requests that don't match.</span></span>

<span data-ttu-id="9d485-305">Двигаемся дальше, tooimplement этой проверки подлинности полностью в собственный код и не используйте hello портал Azure, узнайте, как слишком [проверки подлинности в локальной Active Directory в приложении Azure](../app-service-web/web-sites-authentication-authorization.md).</span><span class="sxs-lookup"><span data-stu-id="9d485-305">Going further, tooimplement this authentication entirely in your own code, and not use hello Azure portal, learn how too [authenticate with on-premises Active Directory in your Azure app](../app-service-web/web-sites-authentication-authorization.md).</span></span>

<span data-ttu-id="9d485-306">toocreate удостоверение приложения логики приложения и использовать API, toocall удостоверений, необходимо выполнить предыдущие действия hello.</span><span class="sxs-lookup"><span data-stu-id="9d485-306">toocreate an application identity for your logic app and use that identity toocall your API, you must follow hello previous steps.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d485-307">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9d485-307">Next steps</span></span>

* [<span data-ttu-id="9d485-308">Проверка производительности и включение ведения журналов и оповещений системы диагностики для рабочих процессов в приложениях логики</span><span class="sxs-lookup"><span data-stu-id="9d485-308">Check logic app performance with diagnostic logs and alerts</span></span>](logic-apps-monitor-your-logic-apps.md)