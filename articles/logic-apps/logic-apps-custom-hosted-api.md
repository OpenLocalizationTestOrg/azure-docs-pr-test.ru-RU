---
title: "Развертывание, вызов и проверка подлинности веб-интерфейсов API и интерфейсов REST API для приложений логики Azure | Документация Майкрософт"
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
ms.openlocfilehash: 88c62d5ab046d8cf4bce5d23b776e517bb0e1d87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-call-and-authenticate-custom-apis-as-connectors-for-logic-apps"></a><span data-ttu-id="bf55c-104">Развертывание, вызов и проверка подлинности пользовательских API в качестве соединителей для приложений логики</span><span class="sxs-lookup"><span data-stu-id="bf55c-104">Deploy, call, and authenticate custom APIs as connectors for logic apps</span></span>

<span data-ttu-id="bf55c-105">После [создания пользовательских API](./logic-apps-create-api-app.md), которые предоставляют действия или триггеры, используемые в рабочих процессах приложений логики, необходимо развернуть эти API, прежде чем их вызывать.</span><span class="sxs-lookup"><span data-stu-id="bf55c-105">After you [create custom APIs](./logic-apps-create-api-app.md) that provide actions or triggers to use in logic apps workflows, you must deploy your APIs before you can call them.</span></span> <span data-ttu-id="bf55c-106">Хотя из приложения логики можно вызвать любой API, для получения наилучших результатов добавьте [метаданные Swagger](http://swagger.io/specification/), которые описывают операции и параметры вашего API.</span><span class="sxs-lookup"><span data-stu-id="bf55c-106">And although you can call any API from a logic app, for the best experience, add [Swagger metadata](http://swagger.io/specification/) that describes your API's operations and parameters.</span></span> <span data-ttu-id="bf55c-107">Этот файл Swagger позволяет улучшить работу API и упростить его интеграцию с приложениями логики.</span><span class="sxs-lookup"><span data-stu-id="bf55c-107">This Swagger file helps your API work better and integrate more easily with logic apps.</span></span>

<span data-ttu-id="bf55c-108">API-интерфейсы можно развернуть в качестве [веб-приложений](../app-service-web/app-service-web-overview.md), но лучше их развернуть в качестве [приложений API](../app-service-api/app-service-api-apps-why-best-platform.md), что облегчит создание, размещение и использование API-интерфейсов как в облаке, так и в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="bf55c-108">You can deploy your APIs as [web apps](../app-service-web/app-service-web-overview.md), but consider deploying your APIs as [API apps](../app-service-api/app-service-api-apps-why-best-platform.md), which can make your job easier when you build, host, and consume APIs in the cloud and on premises.</span></span> <span data-ttu-id="bf55c-109">Не нужно изменять код в API-интерфейсах, просто разверните свой код в приложении API.</span><span class="sxs-lookup"><span data-stu-id="bf55c-109">You don't have to change any code in your APIs -- just deploy your code to an API app.</span></span> <span data-ttu-id="bf55c-110">API-интерфейсы можно разместить в [службе приложений Azure](../app-service/app-service-value-prop-what-is.md). Это служба PaaS (платформа как услуга), предоставляющая один из лучших и самых удобных способов размещения API с максимальным уровнем масштабирования.</span><span class="sxs-lookup"><span data-stu-id="bf55c-110">You can host your APIs on [Azure App Service](../app-service/app-service-value-prop-what-is.md), a platform-as-a-service (PaaS) offering that provides one of the best, easiest, and most scalable ways for API hosting.</span></span>

<span data-ttu-id="bf55c-111">Для проверки подлинности вызовов из приложений логики к API-интерфейсам настройте Azure Active Directory на портале Azure, чтобы не обновлять код.</span><span class="sxs-lookup"><span data-stu-id="bf55c-111">To authenticate calls from logic apps to your APIs, you can set up Azure Active Directory in the Azure portal so you don't have to update your code.</span></span> <span data-ttu-id="bf55c-112">Вы можете также применить обязательную проверку подлинности с помощью кода API.</span><span class="sxs-lookup"><span data-stu-id="bf55c-112">Or, you can require and enforce authentication through your API's code.</span></span>

## <a name="deploy-your-api-as-a-web-app-or-api-app"></a><span data-ttu-id="bf55c-113">Развертывание API в качестве веб-приложения или приложения API</span><span class="sxs-lookup"><span data-stu-id="bf55c-113">Deploy your API as a web app or API app</span></span>

<span data-ttu-id="bf55c-114">Прежде чем вызвать настраиваемый API из приложения логики, разверните его в качестве веб-приложения или приложения API в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="bf55c-114">Before you can call your custom API from a logic app, deploy your API as a web app or API app to Azure App Service.</span></span> <span data-ttu-id="bf55c-115">Также задайте свойства определения API и включите [общий доступ к ресурсам независимо от источника (CORS)](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) для веб-приложения или приложения API, чтобы конструктор приложений логики мог считать документ Swagger.</span><span class="sxs-lookup"><span data-stu-id="bf55c-115">Also, to make your Swagger document readable by the Logic App Designer, set the API definition properties and turn on [cross-origin resource sharing (CORS)](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) for your web app or API app.</span></span>

1. <span data-ttu-id="bf55c-116">На портале Azure выберите веб-приложение или приложение API.</span><span class="sxs-lookup"><span data-stu-id="bf55c-116">In the Azure portal, select your web app or API app.</span></span>

2. <span data-ttu-id="bf55c-117">В открывшейся колонке в разделе **API** выберите **Определение API**.</span><span class="sxs-lookup"><span data-stu-id="bf55c-117">In the blade that opens, under **API**, choose **API definition**.</span></span> <span data-ttu-id="bf55c-118">Задайте в качестве значения параметра **Расположение определения API** URL-адрес файла swagger.json.</span><span class="sxs-lookup"><span data-stu-id="bf55c-118">Set the **API definition location** to the URL for your swagger.json file.</span></span>

   <span data-ttu-id="bf55c-119">Как правило, URL-адрес отображается в таком формате: `https://{name}.azurewebsites.net/swagger/docs/v1)`</span><span class="sxs-lookup"><span data-stu-id="bf55c-119">Usually, the URL appears in this format: `https://{name}.azurewebsites.net/swagger/docs/v1)`</span></span>

   ![Ссылка на файл Swagger для настраиваемого API](media/logic-apps-custom-hosted-api/custom-api-swagger-url.png)

3. <span data-ttu-id="bf55c-121">В разделе **API** выберите **CORS**.</span><span class="sxs-lookup"><span data-stu-id="bf55c-121">Under **API**, choose **CORS**.</span></span> <span data-ttu-id="bf55c-122">Задайте для параметра **Разрешенные источники** политики CORS значение **"*"** (разрешить все).</span><span class="sxs-lookup"><span data-stu-id="bf55c-122">Set the CORS policy for **Allowed origins** to **'*'** (allow all).</span></span>

   <span data-ttu-id="bf55c-123">Этот параметр разрешает запросы из конструктора приложений логики.</span><span class="sxs-lookup"><span data-stu-id="bf55c-123">This setting permits requests from Logic App Designer.</span></span>

   ![Разрешение запросов из конструктора приложений логики для настраиваемого API](media/logic-apps-custom-hosted-api/custom-api-cors.png)

<span data-ttu-id="bf55c-125">Дополнительные сведения вы найдете в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="bf55c-125">For more information, see these articles:</span></span>

* [<span data-ttu-id="bf55c-126">Использование метаданных и пользовательского интерфейса API Swagger</span><span class="sxs-lookup"><span data-stu-id="bf55c-126">Add Swagger metadata for ASP.NET web APIs</span></span>](../app-service-api/app-service-api-dotnet-get-started.md#use-swagger-api-metadata-and-ui)
* [<span data-ttu-id="bf55c-127">Приступая к работе с приложениями API, ASP.NET и Swagger в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="bf55c-127">Deploy ASP.NET web APIs to Azure App Service</span></span>](../app-service-api/app-service-api-dotnet-get-started.md)

## <a name="call-your-custom-api-from-logic-app-workflows"></a><span data-ttu-id="bf55c-128">Вызов настраиваемого API из рабочих процессов приложения логики</span><span class="sxs-lookup"><span data-stu-id="bf55c-128">Call your custom API from logic app workflows</span></span>

<span data-ttu-id="bf55c-129">После настройки CORS и свойств определения API триггеры и действия в пользовательском API должны стать доступными, чтобы вы могли включить их в рабочий процесс приложения логики.</span><span class="sxs-lookup"><span data-stu-id="bf55c-129">After you set up the API definition properties and CORS, your custom API's triggers and actions should become available for you to include in your logic app workflow.</span></span> 

*  <span data-ttu-id="bf55c-130">Чтобы просмотреть веб-сайты с URL-адресом Swagger, просмотрите веб-сайты, относящиеся к вашей подписке, в конструкторе приложений логики.</span><span class="sxs-lookup"><span data-stu-id="bf55c-130">To view the websites that have Swagger URLs, you can browse your subscription websites in the Logic Apps Designer.</span></span>

*  <span data-ttu-id="bf55c-131">Чтобы просмотреть доступные действия и входные данные, указав документ Swagger, используйте действие [HTTP и Swagger](../connectors/connectors-native-http-swagger.md).</span><span class="sxs-lookup"><span data-stu-id="bf55c-131">To view available actions and inputs by pointing at a Swagger document, use the [HTTP + Swagger action](../connectors/connectors-native-http-swagger.md).</span></span>

*  <span data-ttu-id="bf55c-132">Чтобы вызвать любой API, даже тот, который не имеет документа Swagger или не предоставляет его, всегда можно создать запрос с помощью [действия HTTP](../connectors/connectors-native-http.md).</span><span class="sxs-lookup"><span data-stu-id="bf55c-132">To call any API, including APIs that don't have or expose a Swagger document, you can always create a request with the [HTTP action](../connectors/connectors-native-http.md).</span></span>

## <a name="authenticate-calls-to-your-custom-api"></a><span data-ttu-id="bf55c-133">Проверка подлинности вызовов к настраиваемому API</span><span class="sxs-lookup"><span data-stu-id="bf55c-133">Authenticate calls to your custom API</span></span>

<span data-ttu-id="bf55c-134">Защитить вызовы к настраиваемому API можно следующими способами:</span><span class="sxs-lookup"><span data-stu-id="bf55c-134">You can secure calls to your custom API in these ways:</span></span>

* <span data-ttu-id="bf55c-135">[Без изменения кода.](#no-code) Защитите API с помощью [Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) на портале Azure, чтобы не обновлять код и не развертывать API повторно.</span><span class="sxs-lookup"><span data-stu-id="bf55c-135">[No code changes](#no-code): Protect your API with [Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) through the Azure portal, so you don't have to update your code or redeploy your API.</span></span>

  > [!NOTE]
  > <span data-ttu-id="bf55c-136">По умолчанию проверка подлинности Azure AD, которую можно включить на портале Azure, не обеспечивает детального уровня авторизации.</span><span class="sxs-lookup"><span data-stu-id="bf55c-136">By default, the Azure AD authentication that you turn on in the Azure portal doesn't provide fine-grained authorization.</span></span> <span data-ttu-id="bf55c-137">Например, при такой проверке подлинности API блокируется только для конкретного арендатора, а не для определенного пользователя или приложения.</span><span class="sxs-lookup"><span data-stu-id="bf55c-137">For example, this authentication locks your API to just a specific tenant, not to a specific user or app.</span></span> 

* <span data-ttu-id="bf55c-138">[Обновление кода API.](#update-code). Защитите API, применив [проверку подлинности на основе сертификата](#certificate), [обычную проверку подлинности](#basic) или [проверку подлинности Azure AD](#azure-ad-code) с помощью кода.</span><span class="sxs-lookup"><span data-stu-id="bf55c-138">[Update your API's code](#update-code): Protect your API by enforcing [certificate authentication](#certificate), [basic authentication](#basic), or [Azure AD authentication](#azure-ad-code) through code.</span></span>

<a name="no-code"></a>

### <a name="authenticate-calls-to-your-api-without-changing-code"></a><span data-ttu-id="bf55c-139">Проверка подлинности вызовов к API без изменения кода</span><span class="sxs-lookup"><span data-stu-id="bf55c-139">Authenticate calls to your API without changing code</span></span>

<span data-ttu-id="bf55c-140">Вот основные действия для применения этого метода:</span><span class="sxs-lookup"><span data-stu-id="bf55c-140">Here's the general steps for this method:</span></span>

1. <span data-ttu-id="bf55c-141">Создайте два [удостоверения приложений Azure Active Directory (Azure AD)](../app-service-api/app-service-api-dotnet-service-principal-auth.md): одно для приложения логики, а другое — для веб-приложения или приложения API.</span><span class="sxs-lookup"><span data-stu-id="bf55c-141">Create two [Azure Active Directory (Azure AD) application identities](../app-service-api/app-service-api-dotnet-service-principal-auth.md): one for your logic app and one for your web app (or API app).</span></span>

2. <span data-ttu-id="bf55c-142">Чтобы проверить подлинность вызовов к API, используйте учетные данные (идентификатор и секрет клиента) [субъекта-службы](../app-service-api/app-service-api-dotnet-service-principal-auth.md), связанного с удостоверением приложения Azure AD для приложения логики.</span><span class="sxs-lookup"><span data-stu-id="bf55c-142">To authenticate calls to your API, use the credentials (client ID and secret) for the [service principal](../app-service-api/app-service-api-dotnet-service-principal-auth.md) that's associated with the Azure AD application identity for your logic app.</span></span>

3. <span data-ttu-id="bf55c-143">Добавьте идентификаторы приложений в определение приложения логики.</span><span class="sxs-lookup"><span data-stu-id="bf55c-143">Include the application IDs in your logic app definition.</span></span>

#### <a name="part-1-create-an-azure-ad-application-identity-for-your-logic-app"></a><span data-ttu-id="bf55c-144">Часть 1. Создание удостоверения приложения Azure AD для приложения логики</span><span class="sxs-lookup"><span data-stu-id="bf55c-144">Part 1: Create an Azure AD application identity for your logic app</span></span>

<span data-ttu-id="bf55c-145">Приложение логики использует это удостоверение приложения Azure AD для проверки подлинности в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bf55c-145">Your logic app uses this Azure AD application identity to authenticate against Azure AD.</span></span> <span data-ttu-id="bf55c-146">Для вашего каталога это удостоверение необходимо настроить только один раз.</span><span class="sxs-lookup"><span data-stu-id="bf55c-146">You only have to set up this identity one time for your directory.</span></span> <span data-ttu-id="bf55c-147">Например, вы можете использовать одно удостоверение для всех приложений логики или создать отдельные удостоверения для каждого из них.</span><span class="sxs-lookup"><span data-stu-id="bf55c-147">For example, you can choose to use the same identity for all your logic apps, even though you can create unique identities for each logic app.</span></span> <span data-ttu-id="bf55c-148">Эти удостоверения можно настроить на портале Azure, на [классическом портале Azure](#app-identity-logic-classic) или с помощью [PowerShell](#powershell).</span><span class="sxs-lookup"><span data-stu-id="bf55c-148">You can set up these identities in the Azure portal, [Azure classic portal](#app-identity-logic-classic), or use [PowerShell](#powershell).</span></span>

<span data-ttu-id="bf55c-149">**Создание удостоверения для приложения логики на портале Azure**</span><span class="sxs-lookup"><span data-stu-id="bf55c-149">**Create the application identity for your logic app in the Azure portal**</span></span>

1. <span data-ttu-id="bf55c-150">На [портале Azure](https://portal.azure.com "https://portal.azure.com") выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bf55c-150">In the [Azure portal](https://portal.azure.com "https://portal.azure.com"), choose **Azure Active Directory**.</span></span> 

2. <span data-ttu-id="bf55c-151">Убедитесь, что вы открыли каталог своего веб-приложения или приложения API.</span><span class="sxs-lookup"><span data-stu-id="bf55c-151">Confirm that you're in the same directory as your web app or API app.</span></span>

   > [!TIP]
   > <span data-ttu-id="bf55c-152">Для перехода между каталогами щелкните свой профиль и выберите другой каталог.</span><span class="sxs-lookup"><span data-stu-id="bf55c-152">To switch directories, click your profile and select another directory.</span></span> <span data-ttu-id="bf55c-153">Или выберите **Обзор** > **Переключение каталога**.</span><span class="sxs-lookup"><span data-stu-id="bf55c-153">Or, choose **Overview** > **Switch directory**.</span></span>

3. <span data-ttu-id="bf55c-154">В разделе **Управление** в меню каталога выберите **Регистрация приложений** > **Регистрация нового приложения**.</span><span class="sxs-lookup"><span data-stu-id="bf55c-154">On the directory menu, under **Manage**, choose **App registrations** > **New application registration**.</span></span>

   > [!TIP]
   > <span data-ttu-id="bf55c-155">По умолчанию в списке регистрации приложений отображаются записи о регистрации всех приложений в каталоге.</span><span class="sxs-lookup"><span data-stu-id="bf55c-155">By default, the app registrations list shows all app registrations in your directory.</span></span> <span data-ttu-id="bf55c-156">Чтобы просмотреть записи о регистрации только своих приложений, рядом с полем поиска выберите **Мои приложения**.</span><span class="sxs-lookup"><span data-stu-id="bf55c-156">To view only your app registrations, next to the search box, select **My apps**.</span></span> 

   ![Создание регистрации приложения](./media/logic-apps-custom-hosted-api/new-app-registration-azure-portal.png)

4. <span data-ttu-id="bf55c-158">Присвойте имя удостоверению приложения, оставьте для параметра **Тип приложения** значение **Веб-приложение или API**, укажите уникальную строку в формате домена в поле **URL-адрес для входа** и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="bf55c-158">Give your application identity a name, leave **Application type** set to **Web app / API**, provide a unique string formatted as a domain for **Sign-on URL**, and choose **Create**.</span></span>

   ![Указание имени и URL-адреса входа для удостоверения приложения](./media/logic-apps-custom-hosted-api/logic-app-identity-azure-portal.png)

   <span data-ttu-id="bf55c-160">Удостоверение приложения, созданное для приложения логики, теперь отображается в списке регистрации приложений.</span><span class="sxs-lookup"><span data-stu-id="bf55c-160">The application identity that you created for your logic app now appears in the app registrations list.</span></span>

   ![Удостоверение приложения логики](./media/logic-apps-custom-hosted-api/logic-app-identity-created.png)

5. <span data-ttu-id="bf55c-162">В списке регистрации приложений выберите новое удостоверение приложения.</span><span class="sxs-lookup"><span data-stu-id="bf55c-162">In the app registrations list, select your new application identity.</span></span> <span data-ttu-id="bf55c-163">Скопируйте и сохраните **идентификатор приложения**, чтобы использовать его в качестве идентификатора клиента для приложения логики в части 3.</span><span class="sxs-lookup"><span data-stu-id="bf55c-163">Copy and save the **Application ID** to use as the "client ID" for your logic app in Part 3.</span></span>

   ![Копирование и сохранение идентификатора приложения для приложения логики](./media/logic-apps-custom-hosted-api/logic-app-application-id.png)

6. <span data-ttu-id="bf55c-165">Если параметры удостоверения приложения не отображаются, щелкните **Параметры** или **Все параметры**.</span><span class="sxs-lookup"><span data-stu-id="bf55c-165">If your application identity settings aren't visible, choose **Settings** or **All settings**.</span></span>

7. <span data-ttu-id="bf55c-166">В разделе **Доступ через API** выберите **Ключи**.</span><span class="sxs-lookup"><span data-stu-id="bf55c-166">Under **API Access**, choose **Keys**.</span></span> <span data-ttu-id="bf55c-167">В поле **Описание** введите имя для ключа.</span><span class="sxs-lookup"><span data-stu-id="bf55c-167">Under **Description**, provide a name for your key.</span></span> <span data-ttu-id="bf55c-168">Выберите **срок действия** ключа в соответствующем поле.</span><span class="sxs-lookup"><span data-stu-id="bf55c-168">Under **Expires**, select a duration for your key.</span></span>

   <span data-ttu-id="bf55c-169">Ключ, который вы создаете, выступает в качестве "секрета" или пароля для удостоверения приложения логики.</span><span class="sxs-lookup"><span data-stu-id="bf55c-169">The key that you're creating acts as the application identity's "secret" or password for your logic app.</span></span>

   ![Создание ключа для удостоверения приложения логики](./media/logic-apps-custom-hosted-api/create-logic-app-identity-key-secret-password.png)

8. <span data-ttu-id="bf55c-171">На панели инструментов нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="bf55c-171">On the toolbar, choose **Save**.</span></span> <span data-ttu-id="bf55c-172">Ключ отобразится в разделе **Значение**.</span><span class="sxs-lookup"><span data-stu-id="bf55c-172">Under **Value**, your key now appears.</span></span> 
<span data-ttu-id="bf55c-173">**Скопируйте и сохраните ключ** для дальнейшего использования, так как он будет скрыт, если вы выйдете из колонки ключа.</span><span class="sxs-lookup"><span data-stu-id="bf55c-173">**Make sure to copy and save your key** for later use because the key is hidden when you leave the key blade.</span></span>

   <span data-ttu-id="bf55c-174">При настройке приложения логики в части 3 потребуется указать этот ключ в качестве "секрета" или пароля.</span><span class="sxs-lookup"><span data-stu-id="bf55c-174">When you configure your logic app in Part 3, you specify this key as the "secret" or password.</span></span>

   ![Копирование и сохранение ключа для дальнейшего использования](./media/logic-apps-custom-hosted-api/logic-app-copy-key-secret-password.png)

<a name="app-identity-logic-classic"></a>

<span data-ttu-id="bf55c-176">**Создание удостоверения приложения логики на классическом портале Azure**</span><span class="sxs-lookup"><span data-stu-id="bf55c-176">**Create the application identity for your logic app in the Azure classic portal**</span></span>

1. <span data-ttu-id="bf55c-177">На классическом портале Azure перейдите в раздел [**Azure Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span><span class="sxs-lookup"><span data-stu-id="bf55c-177">In the Azure classic portal, choose [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span></span>

2. <span data-ttu-id="bf55c-178">Выберите каталог, который используется для веб-приложения или приложения API.</span><span class="sxs-lookup"><span data-stu-id="bf55c-178">Select the same directory that you use for your web app or API app.</span></span>

3. <span data-ttu-id="bf55c-179">На вкладке **Приложения** щелкните **Добавить** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="bf55c-179">On the **Applications** tab, choose **Add** at the bottom of the page.</span></span>

4. <span data-ttu-id="bf55c-180">Присвойте удостоверению приложения имя и щелкните **Далее** (стрелка вправо).</span><span class="sxs-lookup"><span data-stu-id="bf55c-180">Give your application identity a name, and choose **Next** (right arrow).</span></span>

5. <span data-ttu-id="bf55c-181">В разделе **Свойства приложения** укажите уникальную строку в формате домена для параметров **URL-адрес для входа** и **URI кода приложения** и щелкните **Завершено** (значок флажка).</span><span class="sxs-lookup"><span data-stu-id="bf55c-181">Under **App properties**, provide a unique string formatted as a domain for **Sign-on URL** and **App ID URI**, and choose **Complete** (checkmark).</span></span>

6. <span data-ttu-id="bf55c-182">На вкладке **Настройка** скопируйте и сохраните **идентификатор клиента**, чтобы использовать его для приложения логики в части 3.</span><span class="sxs-lookup"><span data-stu-id="bf55c-182">On the **Configure** tab, copy and save the **Client ID** for your logic app to use in Part 3.</span></span>

7. <span data-ttu-id="bf55c-183">В разделе **Ключи** откройте список **Выбрать длительность**.</span><span class="sxs-lookup"><span data-stu-id="bf55c-183">Under **Keys**, open the **Select duration** list.</span></span> <span data-ttu-id="bf55c-184">Выберите срок действия ключа.</span><span class="sxs-lookup"><span data-stu-id="bf55c-184">Select a duration for your key.</span></span>

   <span data-ttu-id="bf55c-185">Ключ, который вы создаете, выступает в качестве "секрета" или пароля для удостоверения приложения логики.</span><span class="sxs-lookup"><span data-stu-id="bf55c-185">The key that you're creating acts as the application identity's "secret" or password for your logic app.</span></span>

8. <span data-ttu-id="bf55c-186">В нижней части страницы нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="bf55c-186">At the bottom of the page, choose **Save**.</span></span> <span data-ttu-id="bf55c-187">Возможно, потребуется подождать несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="bf55c-187">You might have to wait a few seconds.</span></span>

9. <span data-ttu-id="bf55c-188">Скопируйте и сохраните ключ, который отображается в разделе **Ключи**.</span><span class="sxs-lookup"><span data-stu-id="bf55c-188">Under **Keys**, make sure to copy and save the key that now appears.</span></span> 

   <span data-ttu-id="bf55c-189">При настройке приложения логики в части 3 потребуется указать этот ключ в качестве "секрета" или пароля.</span><span class="sxs-lookup"><span data-stu-id="bf55c-189">When you configure your logic app in Part 3, you specify this key as the "secret" or password.</span></span>

<span data-ttu-id="bf55c-190">Дополнительные сведения см. в статье [Настройка приложения службы приложений для использования службы входа Azure Active Directory](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="bf55c-190">For more information, learn how to [configure your App Service application to use Azure Active Directory login](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span>

<a name="powershell"></a>

<span data-ttu-id="bf55c-191">**Создание удостоверения приложения логики в PowerShell**</span><span class="sxs-lookup"><span data-stu-id="bf55c-191">**Create the application identity for your logic app in PowerShell**</span></span>

<span data-ttu-id="bf55c-192">Эту задачу можно выполнить в Azure Resource Manager с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bf55c-192">You can perform this task through Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="bf55c-193">Выполните следующие команды в PowerShell:</span><span class="sxs-lookup"><span data-stu-id="bf55c-193">In PowerShell, run these commands:</span></span>

1. `Switch-AzureMode AzureResourceManager`

2. `Add-AzureAccount`

3. `New-AzureADApplication -DisplayName "MyLogicAppID" -HomePage "http://mydomain.tld" -IdentifierUris "http://mydomain.tld" -Password "identity-password"`

4. <span data-ttu-id="bf55c-194">Скопируйте использованные ранее **идентификатор клиента** (GUID для клиента Azure AD), **идентификатор приложения** и пароль.</span><span class="sxs-lookup"><span data-stu-id="bf55c-194">Make sure to copy the **Tenant ID** (GUID for your Azure AD tenant), the **Application ID**, and the password that you used.</span></span>

<span data-ttu-id="bf55c-195">Дополнительные сведения см. в статье [Использование Azure PowerShell для создания субъекта-службы и доступа к ресурсам](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="bf55c-195">For more information, learn how to [create a service principal with PowerShell to access resources](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

#### <a name="part-2-create-an-azure-ad-application-identity-for-your-web-app-or-api-app"></a><span data-ttu-id="bf55c-196">Часть 2. Создание удостоверения приложения Azure AD для веб-приложения или приложения API</span><span class="sxs-lookup"><span data-stu-id="bf55c-196">Part 2: Create an Azure AD application identity for your web app or API app</span></span>

<span data-ttu-id="bf55c-197">Если веб-приложение или приложение API уже развернуты, можно включить проверку подлинности и создать удостоверение приложения на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="bf55c-197">If your web app or API app is already deployed, you can turn on authentication and create the application identity in the Azure portal.</span></span> <span data-ttu-id="bf55c-198">В противном случае вы можете [включить проверку подлинности при развертывании с использованием шаблона Azure Resource Manager](#authen-deploy).</span><span class="sxs-lookup"><span data-stu-id="bf55c-198">Otherwise, you can [turn on authentication when you deploy with an Azure Resource Manager template](#authen-deploy).</span></span> 

<span data-ttu-id="bf55c-199">**Создание удостоверения приложения и включение проверки подлинности для развернутых приложений на портале Azure**</span><span class="sxs-lookup"><span data-stu-id="bf55c-199">**Create the application identity and turn on authentication in the Azure portal for deployed apps**</span></span>

1. <span data-ttu-id="bf55c-200">На [портале Azure](https://portal.azure.com "https://portal.azure.com") найдите и выберите свое веб-приложение или приложение API.</span><span class="sxs-lookup"><span data-stu-id="bf55c-200">In the [Azure portal](https://portal.azure.com "https://portal.azure.com"), find and select your web app or API app.</span></span> 

2. <span data-ttu-id="bf55c-201">В разделе **Параметры** выберите **Аутентификация или авторизация**.</span><span class="sxs-lookup"><span data-stu-id="bf55c-201">Under **Settings**, choose **Authentication/Authorization**.</span></span> <span data-ttu-id="bf55c-202">В разделе **Проверка подлинности службы приложений** включите проверку подлинности, нажав кнопку **Вкл.**</span><span class="sxs-lookup"><span data-stu-id="bf55c-202">Under **App Service Authentication**, turn authentication **On**.</span></span> <span data-ttu-id="bf55c-203">В разделе **Поставщики проверки подлинности** щелкните **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bf55c-203">Under **Authentication Providers**, choose **Azure Active Directory**.</span></span>

   ![Включение проверки подлинности](./media/logic-apps-custom-hosted-api/custom-web-api-app-authentication.png)

3. <span data-ttu-id="bf55c-205">Теперь создайте удостоверение приложения для веб-приложения или приложения API, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="bf55c-205">Now create an application identity for your web app or API app as shown here.</span></span> <span data-ttu-id="bf55c-206">В колонке **Параметры Azure Active Directory** для параметра **Режим управления** установите значение **Экспресс**.</span><span class="sxs-lookup"><span data-stu-id="bf55c-206">On the **Azure Active Directory Settings** blade, set **Management mode** to **Express**.</span></span> <span data-ttu-id="bf55c-207">Щелкните **Создать новое приложение AD**.</span><span class="sxs-lookup"><span data-stu-id="bf55c-207">Choose **Create New AD App**.</span></span> <span data-ttu-id="bf55c-208">Присвойте удостоверению приложения имя и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="bf55c-208">Give your application identity a name, and choose **OK**.</span></span> 

   ![Создание удостоверения приложения для веб-приложения или приложения API](./media/logic-apps-custom-hosted-api/custom-api-application-identity.png)

4. <span data-ttu-id="bf55c-210">В колонке **Проверка подлинности/авторизация** нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="bf55c-210">On the **Authentication / Authorization blade**, choose **Save**.</span></span>

<span data-ttu-id="bf55c-211">Теперь необходимо найти идентификаторы клиента и арендатора для удостоверения приложения, связанного с веб-приложением или приложением API.</span><span class="sxs-lookup"><span data-stu-id="bf55c-211">Now you must find the client ID and tenant ID for the application identity that's associated with your web app or API app.</span></span> <span data-ttu-id="bf55c-212">Используйте эти идентификаторы в части 3.</span><span class="sxs-lookup"><span data-stu-id="bf55c-212">You use these IDs in Part 3.</span></span> <span data-ttu-id="bf55c-213">Выполните следующие шаги на портале Azure или на [классическом портале Azure](#find-id-classic).</span><span class="sxs-lookup"><span data-stu-id="bf55c-213">So continue with these steps for the Azure portal or [Azure classic portal](#find-id-classic).</span></span>

<span data-ttu-id="bf55c-214">**Поиск идентификаторов клиента и арендатора удостоверения для веб-приложения или приложения API на портале Azure**</span><span class="sxs-lookup"><span data-stu-id="bf55c-214">**Find application identity's client ID and tenant ID for your web app or API app in the Azure portal**</span></span>

1. <span data-ttu-id="bf55c-215">В разделе **Поставщики проверки подлинности** щелкните **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bf55c-215">Under **Authentication Providers**, choose **Azure Active Directory**.</span></span> 

   ![Выбор элемента Azure Active Directory](./media/logic-apps-custom-hosted-api/custom-api-app-identity-client-id-tenant-id.png)

2. <span data-ttu-id="bf55c-217">В колонке **Параметры Azure Active Directory** для параметра **Режим управления** установите значение **Расширенный**.</span><span class="sxs-lookup"><span data-stu-id="bf55c-217">On the **Azure Active Directory Settings** blade, set **Management mode** to **Advanced**.</span></span>

3. <span data-ttu-id="bf55c-218">Скопируйте **идентификатор клиента** и сохраните этот GUID для использования в части 3.</span><span class="sxs-lookup"><span data-stu-id="bf55c-218">Copy the **Client ID**, and save that GUID for use in Part 3.</span></span>

   > [!TIP] 
   > <span data-ttu-id="bf55c-219">Если **идентификатор клиента** и **URL-адрес издателя** не отображаются, обновите портал Azure и повторите шаг 1.</span><span class="sxs-lookup"><span data-stu-id="bf55c-219">If **Client ID** and **Issuer Url** don't appear, try refreshing the Azure portal, and repeat Step 1.</span></span>

4. <span data-ttu-id="bf55c-220">В разделе **URL-адрес издателя** скопируйте и сохраните только GUID для части 3.</span><span class="sxs-lookup"><span data-stu-id="bf55c-220">Under **Issuer Url**, copy and save just the GUID for Part 3.</span></span> <span data-ttu-id="bf55c-221">При необходимости вы также можете использовать этот GUID в шаблоне развертывания веб-приложения или приложения API.</span><span class="sxs-lookup"><span data-stu-id="bf55c-221">You can also use this GUID in your web app or API app's deployment template, if necessary.</span></span>

   <span data-ttu-id="bf55c-222">Этот GUID — идентификатор определенного арендатора (ИД арендатора), который должен отображаться в следующем URL-адресе: `https://sts.windows.net/{GUID}`</span><span class="sxs-lookup"><span data-stu-id="bf55c-222">This GUID is your specific tenant's GUID ("tenant ID") and should appear in this URL: `https://sts.windows.net/{GUID}`</span></span>

5. <span data-ttu-id="bf55c-223">Не сохраняя изменений, закройте колонку **Параметры Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bf55c-223">Without saving your changes, close the **Azure Active Directory Settings** blade.</span></span>

<a name="find-id-classic"></a>

<span data-ttu-id="bf55c-224">**Поиск идентификаторов клиента и арендатора удостоверения для веб-приложения или приложения API на классическом портале Azure**</span><span class="sxs-lookup"><span data-stu-id="bf55c-224">**Find application identity's client ID and tenant ID for your web app or API app in the Azure classic portal**</span></span>

1. <span data-ttu-id="bf55c-225">На классическом портале Azure перейдите в раздел [**Azure Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span><span class="sxs-lookup"><span data-stu-id="bf55c-225">In the Azure classic portal, choose [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span></span>

2.  <span data-ttu-id="bf55c-226">Выберите каталог, используемый для веб-приложения или приложения API.</span><span class="sxs-lookup"><span data-stu-id="bf55c-226">Select the directory that you use for your web app or API app.</span></span>

3. <span data-ttu-id="bf55c-227">В поле **поиска** найдите и выберите удостоверение для веб-приложения или приложения API.</span><span class="sxs-lookup"><span data-stu-id="bf55c-227">In the **Search** box, find and select the application identity for your web app or API app.</span></span>

4. <span data-ttu-id="bf55c-228">На вкладке **Настройка** скопируйте **идентификатор клиента** и сохраните этот GUID для использования в части 3.</span><span class="sxs-lookup"><span data-stu-id="bf55c-228">On the **Configure** tab, copy the **Client ID**, and save that GUID for use in Part 3.</span></span>

5. <span data-ttu-id="bf55c-229">Получив идентификатор клиента, в нижней части вкладки **Настройка** щелкните **Просмотр конечных точек**.</span><span class="sxs-lookup"><span data-stu-id="bf55c-229">After you get the client ID, at the bottom of the **Configure** tab, choose **View endpoints**.</span></span>

6. <span data-ttu-id="bf55c-230">Скопируйте URL-адрес **документа метаданных федерации** и перейдите по этому адресу.</span><span class="sxs-lookup"><span data-stu-id="bf55c-230">Copy the URL for **Federation Metadata Document**, and browse to that URL.</span></span>

7. <span data-ttu-id="bf55c-231">В открывшемся документе метаданных найдите корневой элемент **EntityDescriptor ID** с атрибутом **entityID** в таком формате: `https://sts.windows.net/{GUID}`</span><span class="sxs-lookup"><span data-stu-id="bf55c-231">In the metadata document that opens, find the root **EntityDescriptor ID** element, which has an **entityID** attribute in this form: `https://sts.windows.net/{GUID}`</span></span> 

      <span data-ttu-id="bf55c-232">GUID в этом атрибуте — идентификатор определенного арендатора (ИД арендатора).</span><span class="sxs-lookup"><span data-stu-id="bf55c-232">The GUID in this attribute is your specific tenant's GUID (tenant ID).</span></span>

8. <span data-ttu-id="bf55c-233">Скопируйте ИД арендатора и сохраните его для использования в части 3, а также в шаблоне развертывания веб-приложения или приложения API (при необходимости).</span><span class="sxs-lookup"><span data-stu-id="bf55c-233">Copy the tenant ID and save that ID for use in Part 3, and also to use in your web app or API app's deployment template, if necessary.</span></span>

<span data-ttu-id="bf55c-234">Дополнительные сведения см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="bf55c-234">For more information, see these topics:</span></span>

* [<span data-ttu-id="bf55c-235">Проверка подлинности пользователя для приложений API в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="bf55c-235">User authentication for API apps in Azure App Service</span></span>](../app-service-api/app-service-api-dotnet-user-principal-auth.md)
* [<span data-ttu-id="bf55c-236">Проверка подлинности и авторизация в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="bf55c-236">Authentication and authorization in Azure App Service</span></span>](../app-service/app-service-authentication-overview.md)

<a name="authen-deploy"></a>

<span data-ttu-id="bf55c-237">**Проверка подлинности и авторизация в службе приложений Azure**</span><span class="sxs-lookup"><span data-stu-id="bf55c-237">**Turn on authentication when you deploy with an Azure Resource Manager template**</span></span>

<span data-ttu-id="bf55c-238">Вам все же потребуется создать удостоверение приложения Azure AD для веб-приложения или приложения API, которое отличается от удостоверения приложения логики.</span><span class="sxs-lookup"><span data-stu-id="bf55c-238">You must still create an Azure AD application identity for your web app or API app that differs from the app identity for your logic app.</span></span> <span data-ttu-id="bf55c-239">Чтобы создать удостоверение приложения, выполните шаги на портале Azure, приведенные в части 2.</span><span class="sxs-lookup"><span data-stu-id="bf55c-239">To create the application identity, follow the previous steps in Part 2 for the Azure portal.</span></span> <span data-ttu-id="bf55c-240">Вы также можете выполнить шаги, приведенные в части 1, но при этом обязательно укажите фактическое значение `https://{URL}` веб-приложения или приложения API для параметров **URL-адрес для входа** и **URI кода приложения**.</span><span class="sxs-lookup"><span data-stu-id="bf55c-240">You can also follow the steps in Part 1, but make sure to use your web app or API app's actual `https://{URL}` for **Sign-on URL** and **App ID URI**.</span></span> <span data-ttu-id="bf55c-241">В этих шагах необходимо сохранить идентификаторы клиента и арендатора, чтобы использовать их в шаблоне развертывания приложения и в части 3.</span><span class="sxs-lookup"><span data-stu-id="bf55c-241">From these steps, you have to save both the client ID and tenant ID for use in your app's deployment template and also for Part 3.</span></span>

> [!NOTE]
> <span data-ttu-id="bf55c-242">При создании удостоверения приложения Azure AD для веб-приложения или приложения API необходимо использовать портал Azure или классический портал Azure, а не PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bf55c-242">When you create the Azure AD application identity for your web app or API app, you must use the Azure portal or Azure classic portal, rather than PowerShell.</span></span> <span data-ttu-id="bf55c-243">Командлет PowerShell не поддерживает настройку необходимых разрешений для входа пользователей на веб-сайт.</span><span class="sxs-lookup"><span data-stu-id="bf55c-243">The PowerShell commandlet doesn't set up the required permissions to sign users into a website.</span></span>

<span data-ttu-id="bf55c-244">Получив идентификаторы клиента и арендатора, добавьте их в шаблон развертывания в качестве подресурса веб-приложения или приложения API.</span><span class="sxs-lookup"><span data-stu-id="bf55c-244">After you get the client ID and tenant ID, include these IDs as a subresource of your web app or API app in your deployment template:</span></span>

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

<span data-ttu-id="bf55c-245">Чтобы автоматически развернуть пустое веб-приложение и приложение логики и включить проверку подлинности с помощью Azure Active Directory, просмотрите полный шаблон [здесь](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json) или щелкните **Развертывание в Azure**:</span><span class="sxs-lookup"><span data-stu-id="bf55c-245">To automatically deploy a blank web app and a logic app together with Azure Active Directory authentication, [view the complete template here](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json), or click **Deploy to Azure** here:</span></span>

<span data-ttu-id="bf55c-246">[![Развертывание в Azure](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="bf55c-246">[![Deploy to Azure](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)</span></span>

#### <a name="part-3-populate-the-authorization-section-in-your-logic-app"></a><span data-ttu-id="bf55c-247">Часть 3. Заполнение раздела авторизации в приложении логики</span><span class="sxs-lookup"><span data-stu-id="bf55c-247">Part 3: Populate the Authorization section in your logic app</span></span>

<span data-ttu-id="bf55c-248">В предыдущем шаблоне этот раздел авторизации уже настроен. Но если вы разрабатываете приложение логики полностью самостоятельно, вам потребуется включить весь раздел авторизации.</span><span class="sxs-lookup"><span data-stu-id="bf55c-248">The previous template already has this authorization section set up, but if you are directly authoring the logic app, you must include the full authorization section.</span></span>

<span data-ttu-id="bf55c-249">Откройте определение приложения логики в представлении кода, перейдите к разделу действия **HTTP**, найдите раздел **Авторизация** и добавьте следующую строку:</span><span class="sxs-lookup"><span data-stu-id="bf55c-249">Open your logic app definition in code view, go to the **HTTP** action section, find the **Authorization** section, and include this line:</span></span>

`{"tenant": "{tenant-ID}", "audience": "{client-ID-from-Part-2-web-app-or-API app}", "clientId": "{client-ID-from-Part-1-logic-app}", "secret": "{key-from-Part-1-logic-app}", "type": "ActiveDirectoryOAuth" }`

| <span data-ttu-id="bf55c-250">Элемент</span><span class="sxs-lookup"><span data-stu-id="bf55c-250">Element</span></span> | <span data-ttu-id="bf55c-251">Описание</span><span class="sxs-lookup"><span data-stu-id="bf55c-251">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="bf55c-252">tenant</span><span class="sxs-lookup"><span data-stu-id="bf55c-252">tenant</span></span> |<span data-ttu-id="bf55c-253">GUID для арендатора Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bf55c-253">The GUID for the Azure AD tenant</span></span> |
| <span data-ttu-id="bf55c-254">audience</span><span class="sxs-lookup"><span data-stu-id="bf55c-254">audience</span></span> |<span data-ttu-id="bf55c-255">обязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="bf55c-255">Required.</span></span> <span data-ttu-id="bf55c-256">GUID целевого ресурса, к которому требуется доступ, — идентификатор клиента из удостоверения приложения для веб-приложения или приложения API.</span><span class="sxs-lookup"><span data-stu-id="bf55c-256">The GUID for the target resource that you want to access - the client ID from the application identity for your web app or API app</span></span> |
| <span data-ttu-id="bf55c-257">clientid</span><span class="sxs-lookup"><span data-stu-id="bf55c-257">clientId</span></span> |<span data-ttu-id="bf55c-258">GUID клиента, запрашивающего доступ, — идентификатор клиента из удостоверения приложения логики.</span><span class="sxs-lookup"><span data-stu-id="bf55c-258">The GUID for the client requesting access - the client ID from the application identity for your logic app</span></span> |
| <span data-ttu-id="bf55c-259">secret</span><span class="sxs-lookup"><span data-stu-id="bf55c-259">secret</span></span> |<span data-ttu-id="bf55c-260">обязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="bf55c-260">Required.</span></span> <span data-ttu-id="bf55c-261">Ключ или пароль из удостоверения приложения для клиента, который запрашивает маркер доступа.</span><span class="sxs-lookup"><span data-stu-id="bf55c-261">The key or password from the application identity for the client that's requesting the access token</span></span> |
| <span data-ttu-id="bf55c-262">Тип</span><span class="sxs-lookup"><span data-stu-id="bf55c-262">type</span></span> |<span data-ttu-id="bf55c-263">Тип проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="bf55c-263">The authentication type.</span></span> <span data-ttu-id="bf55c-264">Для аутентификации ActiveDirectoryOAuth это значение равно `ActiveDirectoryOAuth`.</span><span class="sxs-lookup"><span data-stu-id="bf55c-264">For ActiveDirectoryOAuth authentication, the value is `ActiveDirectoryOAuth`.</span></span> |

<span data-ttu-id="bf55c-265">Например:</span><span class="sxs-lookup"><span data-stu-id="bf55c-265">For example:</span></span>

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

### <a name="secure-api-calls-through-code"></a><span data-ttu-id="bf55c-266">Безопасные вызовы API с помощью кода</span><span class="sxs-lookup"><span data-stu-id="bf55c-266">Secure API calls through code</span></span>

<a name="certificate"></a>

#### <a name="certificate-authentication"></a><span data-ttu-id="bf55c-267">Проверка подлинности на основе сертификата</span><span class="sxs-lookup"><span data-stu-id="bf55c-267">Certificate authentication</span></span>

<span data-ttu-id="bf55c-268">Вы можете использовать сертификаты клиента для проверки входящих запросов из приложения логики к веб-приложению или приложению API.</span><span class="sxs-lookup"><span data-stu-id="bf55c-268">To validate the incoming requests from your logic app to your web app or API app, you can use client certificates.</span></span> <span data-ttu-id="bf55c-269">Чтобы узнать, как настроить код, см. статью о [настройке взаимной проверки подлинности TLS](../app-service-web/app-service-web-configure-tls-mutual-auth.md).</span><span class="sxs-lookup"><span data-stu-id="bf55c-269">To set up your code, learn [how to configure TLS mutual authentication](../app-service-web/app-service-web-configure-tls-mutual-auth.md).</span></span>

<span data-ttu-id="bf55c-270">В разделе **Авторизация** добавьте следующую строку:</span><span class="sxs-lookup"><span data-stu-id="bf55c-270">In the **Authorization** section, include this line:</span></span> 

`{"type": "clientcertificate", "password": "password", "pfx": "long-pfx-key"}`

| <span data-ttu-id="bf55c-271">Элемент</span><span class="sxs-lookup"><span data-stu-id="bf55c-271">Element</span></span> | <span data-ttu-id="bf55c-272">Описание</span><span class="sxs-lookup"><span data-stu-id="bf55c-272">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="bf55c-273">type</span><span class="sxs-lookup"><span data-stu-id="bf55c-273">type</span></span> |<span data-ttu-id="bf55c-274">обязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="bf55c-274">Required.</span></span> <span data-ttu-id="bf55c-275">Тип проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="bf55c-275">The authentication type.</span></span> <span data-ttu-id="bf55c-276">Для SSL-сертификатов клиента используйте значение `ClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="bf55c-276">For SSL client certificates, the value must be `ClientCertificate`.</span></span> |
| <span data-ttu-id="bf55c-277">пароль</span><span class="sxs-lookup"><span data-stu-id="bf55c-277">password</span></span> |<span data-ttu-id="bf55c-278">обязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="bf55c-278">Required.</span></span> <span data-ttu-id="bf55c-279">Пароль для доступа к сертификату клиента (PFX-файл).</span><span class="sxs-lookup"><span data-stu-id="bf55c-279">The password for accessing the client certificate (PFX file)</span></span> |
| <span data-ttu-id="bf55c-280">pfx</span><span class="sxs-lookup"><span data-stu-id="bf55c-280">pfx</span></span> |<span data-ttu-id="bf55c-281">обязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="bf55c-281">Required.</span></span> <span data-ttu-id="bf55c-282">Содержимое сертификата клиента в кодировке Base64 (PFX-файл).</span><span class="sxs-lookup"><span data-stu-id="bf55c-282">Base64-encoded contents of the client certificate (PFX file)</span></span> |

<a name="basic"></a>

#### <a name="basic-authentication"></a><span data-ttu-id="bf55c-283">Обычная аутентификация</span><span class="sxs-lookup"><span data-stu-id="bf55c-283">Basic authentication</span></span>

<span data-ttu-id="bf55c-284">Для проверки входящих запросов из приложения логики к веб-приложениям или приложениям API можно использовать обычную проверку подлинности: имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="bf55c-284">To validate incoming requests from your logic app to your web app or API app, you can use basic authentication, such as a username and password.</span></span> <span data-ttu-id="bf55c-285">Обычная проверка подлинности — это универсальный вариант, который подходит для веб-приложений и приложений API, написанных на любых языках программирования.</span><span class="sxs-lookup"><span data-stu-id="bf55c-285">Basic authentication is a common pattern, and you can use this authentication in any language used to build your web app or API app.</span></span>

<span data-ttu-id="bf55c-286">В разделе **Авторизация** добавьте следующую строку:</span><span class="sxs-lookup"><span data-stu-id="bf55c-286">In the **Authorization** section, include this line:</span></span>

<span data-ttu-id="bf55c-287">`{"type": "basic", "username": "username", "password": "password"}`.</span><span class="sxs-lookup"><span data-stu-id="bf55c-287">`{"type": "basic", "username": "username", "password": "password"}`.</span></span>

| <span data-ttu-id="bf55c-288">Элемент</span><span class="sxs-lookup"><span data-stu-id="bf55c-288">Element</span></span> | <span data-ttu-id="bf55c-289">Описание</span><span class="sxs-lookup"><span data-stu-id="bf55c-289">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bf55c-290">type</span><span class="sxs-lookup"><span data-stu-id="bf55c-290">type</span></span> |<span data-ttu-id="bf55c-291">обязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="bf55c-291">Required.</span></span> <span data-ttu-id="bf55c-292">Тип проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="bf55c-292">The authentication type.</span></span> <span data-ttu-id="bf55c-293">Для обычной проверки подлинности используйте значение `Basic`.</span><span class="sxs-lookup"><span data-stu-id="bf55c-293">For basic authentication, the value must be `Basic`.</span></span> |
| <span data-ttu-id="bf55c-294">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="bf55c-294">username</span></span> |<span data-ttu-id="bf55c-295">обязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="bf55c-295">Required.</span></span> <span data-ttu-id="bf55c-296">Имя пользователя для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="bf55c-296">The username for authentication</span></span> |
| <span data-ttu-id="bf55c-297">пароль</span><span class="sxs-lookup"><span data-stu-id="bf55c-297">password</span></span> |<span data-ttu-id="bf55c-298">обязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="bf55c-298">Required.</span></span> <span data-ttu-id="bf55c-299">Пароль для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="bf55c-299">The password for authentication</span></span> |

<a name="azure-ad-code"></a>

#### <a name="azure-active-directory-authentication-through-code"></a><span data-ttu-id="bf55c-300">Проверка подлинности Azure Active Directory с помощью кода</span><span class="sxs-lookup"><span data-stu-id="bf55c-300">Azure Active Directory authentication through code</span></span>

<span data-ttu-id="bf55c-301">По умолчанию проверка подлинности Azure AD, которую можно включить на портале Azure, не обеспечивает детального уровня авторизации.</span><span class="sxs-lookup"><span data-stu-id="bf55c-301">By default, the Azure AD authentication that you turn on in the Azure portal doesn't provide fine-grained authorization.</span></span> <span data-ttu-id="bf55c-302">Например, при такой проверке подлинности API блокируется только для конкретного арендатора, а не для определенного пользователя или приложения.</span><span class="sxs-lookup"><span data-stu-id="bf55c-302">For example, this authentication locks your API to just a specific tenant, not to a specific user or app.</span></span> 

<span data-ttu-id="bf55c-303">Чтобы ограничить доступ через API к приложению логики с помощью кода, извлеките заголовок, который содержит маркер JSON Web Token (JWT).</span><span class="sxs-lookup"><span data-stu-id="bf55c-303">To restrict API access to your logic app through code, extract the header that has the JSON web token (JWT).</span></span> <span data-ttu-id="bf55c-304">Проверяйте удостоверение вызывающей стороны и отклоняйте запросы, не отвечающие требованиям.</span><span class="sxs-lookup"><span data-stu-id="bf55c-304">Check the caller's identity, and reject requests that don't match.</span></span>

<span data-ttu-id="bf55c-305">Чтобы реализовать проверку подлинности полностью в коде, не используя портал Azure, ознакомьтесь со статьей [Проверка подлинности в приложении Azure с помощью локального каталога Active Directory](../app-service-web/web-sites-authentication-authorization.md).</span><span class="sxs-lookup"><span data-stu-id="bf55c-305">Going further, to implement this authentication entirely in your own code, and not use the Azure portal, learn how to [authenticate with on-premises Active Directory in your Azure app](../app-service-web/web-sites-authentication-authorization.md).</span></span>

<span data-ttu-id="bf55c-306">Чтобы создать удостоверение для приложения логики и с его помощью вызвать API, вам потребуется выполнить приведенные выше шаги.</span><span class="sxs-lookup"><span data-stu-id="bf55c-306">To create an application identity for your logic app and use that identity to call your API, you must follow the previous steps.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bf55c-307">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bf55c-307">Next steps</span></span>

* [<span data-ttu-id="bf55c-308">Проверка производительности и включение ведения журналов и оповещений системы диагностики для рабочих процессов в приложениях логики</span><span class="sxs-lookup"><span data-stu-id="bf55c-308">Check logic app performance with diagnostic logs and alerts</span></span>](logic-apps-monitor-your-logic-apps.md)