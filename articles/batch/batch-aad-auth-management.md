---
title: "aaaUse Azure Active Directory tooauthenticate пакет управления решения | Документы Microsoft"
description: "Построение приложений с помощью диспетчера ресурсов Azure и поставщик ресурсов пакета hello аутентификации в Azure AD."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/27/2017
ms.author: tamram
ms.openlocfilehash: 192aa9f8d7cbfc0282a4a0c33ab1659f1f351525
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-batch-management-solutions-with-active-directory"></a><span data-ttu-id="9ee68-103">Аутентификация решений по управлению пакетной службой с помощью Active Directory</span><span class="sxs-lookup"><span data-stu-id="9ee68-103">Authenticate Batch Management solutions with Active Directory</span></span>

<span data-ttu-id="9ee68-104">Приложения, вызывающие hello Azure пакета управления службы проверки подлинности в [Azure Active Directory] [ aad_about] (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9ee68-104">Applications that call hello Azure Batch Management service authenticate with [Azure Active Directory][aad_about] (Azure AD).</span></span> <span data-ttu-id="9ee68-105">Azure AD — многопользовательский облачный каталог и служба управления удостоверениями корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="9ee68-105">Azure AD is Microsoft’s multi-tenant cloud based directory and identity management service.</span></span> <span data-ttu-id="9ee68-106">Azure сама использует Azure AD для проверки подлинности hello клиентов, Администраторы служб и пользователей организации.</span><span class="sxs-lookup"><span data-stu-id="9ee68-106">Azure itself uses Azure AD for hello authentication of its customers, service administrators, and organizational users.</span></span>

<span data-ttu-id="9ee68-107">Библиотека пакета управления .NET Hello предоставляет типы для работы с учетными записями, ключи учетной записи, приложения и пакеты приложений пакета.</span><span class="sxs-lookup"><span data-stu-id="9ee68-107">hello Batch Management .NET library exposes types for working with Batch accounts, account keys, applications, and application packages.</span></span> <span data-ttu-id="9ee68-108">Библиотека пакета управления .NET Hello является клиента поставщика ресурсов Azure и используется вместе с [диспетчера ресурсов Azure] [ resman_overview] toomanage эти ресурсы программными средствами.</span><span class="sxs-lookup"><span data-stu-id="9ee68-108">hello Batch Management .NET library is an Azure resource provider client, and is used together with [Azure Resource Manager][resman_overview] toomanage these resources programmatically.</span></span> <span data-ttu-id="9ee68-109">Azure AD — необходимые tooauthenticate запросов, выполненных при помощи любого клиента поставщика ресурсов Azure, включая библиотеку .NET пакета управления hello, а по [диспетчера ресурсов Azure][resman_overview].</span><span class="sxs-lookup"><span data-stu-id="9ee68-109">Azure AD is required tooauthenticate requests made through any Azure resource provider client, including hello Batch Management .NET library, and through [Azure Resource Manager][resman_overview].</span></span>

<span data-ttu-id="9ee68-110">В этой статье мы расскажем, с помощью Azure AD tooauthenticate из приложения, использующие библиотеку hello пакета управления .NET.</span><span class="sxs-lookup"><span data-stu-id="9ee68-110">In this article, we explore using Azure AD tooauthenticate from applications that use hello Batch Management .NET library.</span></span> <span data-ttu-id="9ee68-111">Мы покажем, как tooauthenticate toouse Azure AD администратором подписки или соадминистратором, с помощью встроенной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="9ee68-111">We show how toouse Azure AD tooauthenticate a subscription administrator or co-administrator, using integrated authentication.</span></span> <span data-ttu-id="9ee68-112">Мы используем hello [AccountManagment] [ acct_mgmt_sample] образец проекта, на сайте GitHub, toowalk с помощью Azure AD с библиотекой hello пакета управления .NET.</span><span class="sxs-lookup"><span data-stu-id="9ee68-112">We use hello [AccountManagment][acct_mgmt_sample] sample project, available on GitHub, toowalk through using Azure AD with hello Batch Management .NET library.</span></span>

<span data-ttu-id="9ee68-113">. в разделе toolearn Подробнее об использовании библиотеки пакета управления .NET hello и образец hello AccountManagement [учетные записи пакета управления и квоты с hello пакета управления клиентской библиотеки для .NET](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="9ee68-113">toolearn more about using hello Batch Management .NET library and hello AccountManagement sample, see [Manage Batch accounts and quotas with hello Batch Management client library for .NET](batch-management-dotnet.md).</span></span>

## <a name="register-your-application-with-azure-ad"></a><span data-ttu-id="9ee68-114">Регистрация приложения в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ee68-114">Register your application with Azure AD</span></span>

<span data-ttu-id="9ee68-115">Hello Azure [библиотеку аутентификации Active Directory] [ aad_adal] (ADAL) предоставляет программный интерфейс tooAzure AD для использования в приложениях.</span><span class="sxs-lookup"><span data-stu-id="9ee68-115">hello Azure [Active Directory Authentication Library][aad_adal] (ADAL) provides a programmatic interface tooAzure AD for use within your applications.</span></span> <span data-ttu-id="9ee68-116">toocall ADAL из приложения, необходимо зарегистрировать приложение в клиент Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9ee68-116">toocall ADAL from your application, you must register your application in an Azure AD tenant.</span></span> <span data-ttu-id="9ee68-117">При регистрации приложения вы указываете Azure AD с информацией о приложении, включая ее имя в рамках клиента Azure AD hello.</span><span class="sxs-lookup"><span data-stu-id="9ee68-117">When you register your application, you supply Azure AD with information about your application, including a name for it within hello Azure AD tenant.</span></span> <span data-ttu-id="9ee68-118">Затем Azure AD предоставляет идентификатора приложения используйте tooassociate приложения в Azure AD во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="9ee68-118">Azure AD then provides an application ID that you use tooassociate your application with Azure AD at runtime.</span></span> <span data-ttu-id="9ee68-119">toolearn Дополнительные сведения о идентификатор приложения hello, в разделе [приложений и объектов участника службы в Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="9ee68-119">toolearn more about hello application ID, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span>

<span data-ttu-id="9ee68-120">hello tooregister AccountManagement образец приложения, выполните действия hello в hello [Добавление приложения](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) статьи [интеграция приложений с Azure Active Directory] [ aad_integrate].</span><span class="sxs-lookup"><span data-stu-id="9ee68-120">tooregister hello AccountManagement sample application, follow hello steps in hello [Adding an Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span></span> <span data-ttu-id="9ee68-121">Укажите **собственное клиентское приложение** для типа приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9ee68-121">Specify **Native Client Application** for hello type of application.</span></span> <span data-ttu-id="9ee68-122">Здравствуйте, отрасли стандартного URI OAuth 2.0 для hello **URI перенаправления** — `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="9ee68-122">hello industry standard OAuth 2.0 URI for hello **Redirect URI** is `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="9ee68-123">Тем не менее, можно указать любой допустимый URI (например, `http://myaccountmanagementsample`) для hello **URI перенаправления**, как не обязательно toobe реальные конечной точки:</span><span class="sxs-lookup"><span data-stu-id="9ee68-123">However, you can specify any valid URI (such as `http://myaccountmanagementsample`) for hello **Redirect URI**, as it does not need toobe a real endpoint:</span></span>

![](./media/batch-aad-auth-management/app-registration-management-plane.png)

<span data-ttu-id="9ee68-124">После завершения процесса регистрации hello будет виден идентификатор приложения hello и hello идентификатор объекта (субъекта-службы), указанный для приложения.</span><span class="sxs-lookup"><span data-stu-id="9ee68-124">Once you complete hello registration process, you'll see hello application ID and hello object (service principal) ID listed for your application.</span></span>  

![](./media/batch-aad-auth-management/app-registration-client-id.png)

## <a name="grant-hello-azure-resource-manager-api-access-tooyour-application"></a><span data-ttu-id="9ee68-125">Предоставление доступа tooyour hello API диспетчера ресурсов Azure приложения</span><span class="sxs-lookup"><span data-stu-id="9ee68-125">Grant hello Azure Resource Manager API access tooyour application</span></span>

<span data-ttu-id="9ee68-126">Далее вам понадобятся toodelegate доступа tooyour приложения toohello API диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="9ee68-126">Next, you'll need toodelegate access tooyour application toohello Azure Resource Manager API.</span></span> <span data-ttu-id="9ee68-127">Идентификатор Hello Azure AD для hello API диспетчера ресурсов — **API управления службами Windows Azure**.</span><span class="sxs-lookup"><span data-stu-id="9ee68-127">hello Azure AD identifier for hello Resource Manager API is **Windows Azure Service Management API**.</span></span>

<span data-ttu-id="9ee68-128">Выполните следующие действия в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="9ee68-128">Follow these steps in hello Azure portal:</span></span>

1. <span data-ttu-id="9ee68-129">В области навигации слева hello hello портал Azure, выберите **более служб**, нажмите кнопку **регистрации приложения**и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="9ee68-129">In hello left-hand navigation pane of hello Azure portal, choose **More Services**, click **App Registrations**, and click **Add**.</span></span>
2. <span data-ttu-id="9ee68-130">Найдите имя приложения в списке hello регистраций приложения hello:</span><span class="sxs-lookup"><span data-stu-id="9ee68-130">Search for hello name of your application in hello list of app registrations:</span></span>

    ![Поиск имени приложения](./media/batch-aad-auth-management/search-app-registration.png)

3. <span data-ttu-id="9ee68-132">Экран приветствия **параметры** колонку.</span><span class="sxs-lookup"><span data-stu-id="9ee68-132">Display hello **Settings** blade.</span></span> <span data-ttu-id="9ee68-133">В hello **доступ к API** выберите **требуемые разрешения**.</span><span class="sxs-lookup"><span data-stu-id="9ee68-133">In hello **API Access** section, select **Required permissions**.</span></span>
4. <span data-ttu-id="9ee68-134">Нажмите кнопку **добавить** tooadd новый необходимое разрешение.</span><span class="sxs-lookup"><span data-stu-id="9ee68-134">Click **Add** tooadd a new required permission.</span></span> 
5. <span data-ttu-id="9ee68-135">На шаге 1, введите **API управления службами Windows Azure**, выберите API, который hello список результатов и нажмите кнопку hello **выберите** кнопки.</span><span class="sxs-lookup"><span data-stu-id="9ee68-135">In step 1, enter **Windows Azure Service Management API**, select that API from hello list of results, and click hello **Select** button.</span></span>
6. <span data-ttu-id="9ee68-136">На шаге 2, выберите hello флажок рядом слишком**доступ к Azure классической модели развертывания как пользователи организации**и нажмите кнопку hello **выберите** кнопки.</span><span class="sxs-lookup"><span data-stu-id="9ee68-136">In step 2, select hello check box next too**Access Azure classic deployment model as organization users**, and click hello **Select** button.</span></span>
7. <span data-ttu-id="9ee68-137">Нажмите кнопку hello **сделать** кнопки.</span><span class="sxs-lookup"><span data-stu-id="9ee68-137">Click hello **Done** button.</span></span>

<span data-ttu-id="9ee68-138">Hello **требуемые разрешения** колонке теперь показывает, что приложение tooyour разрешения предоставлены tooboth hello ADAL и API диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9ee68-138">hello **Required Permissions** blade now shows that permissions tooyour application are granted tooboth hello ADAL and Resource Manager APIs.</span></span> <span data-ttu-id="9ee68-139">Разрешения предоставляются tooADAL по умолчанию при первой регистрации приложения в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9ee68-139">Permissions are granted tooADAL by default when you first register your app with Azure AD.</span></span>

![Делегировать разрешения toohello API диспетчера ресурсов Azure](./media/batch-aad-auth-management/required-permissions-management-plane.png)

## <a name="azure-ad-endpoints"></a><span data-ttu-id="9ee68-141">Конечные точки Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ee68-141">Azure AD endpoints</span></span>

<span data-ttu-id="9ee68-142">tooauthenticate решениях пакета управления с Azure AD, вам потребуется два хорошо известных конечных точек.</span><span class="sxs-lookup"><span data-stu-id="9ee68-142">tooauthenticate your Batch Management solutions with Azure AD, you'll need two well-known endpoints.</span></span>

- <span data-ttu-id="9ee68-143">Hello **Обычная конечная точка Azure AD** предоставляет общие сбора интерфейс при конкретных клиентов не указано, как случае hello встроенной проверки подлинности учетные данные:</span><span class="sxs-lookup"><span data-stu-id="9ee68-143">hello **Azure AD common endpoint** provides a generic credential gathering interface when a specific tenant is not provided, as in hello case of integrated authentication:</span></span>

    `https://login.microsoftonline.com/common`

- <span data-ttu-id="9ee68-144">Hello **конечную точку диспетчера ресурсов Azure** является tooacquire используется токен для проверки подлинности службы запросов toohello пакета управления:</span><span class="sxs-lookup"><span data-stu-id="9ee68-144">hello **Azure Resource Manager endpoint** is used tooacquire a token for authenticating requests toohello Batch management service:</span></span>

    `https://management.core.windows.net/`

<span data-ttu-id="9ee68-145">AccountManagement пример приложения Hello определяет константы для этих конечных точек.</span><span class="sxs-lookup"><span data-stu-id="9ee68-145">hello AccountManagement sample application defines constants for these endpoints.</span></span> <span data-ttu-id="9ee68-146">Оставьте их без изменений:</span><span class="sxs-lookup"><span data-stu-id="9ee68-146">Leave these constants unchanged:</span></span>

```csharp
// Azure Active Directory "common" endpoint.
private const string AuthorityUri = "https://login.microsoftonline.com/common";
// Azure Resource Manager endpoint 
private const string ResourceUri = "https://management.core.windows.net/";
```

## <a name="reference-your-application-id"></a><span data-ttu-id="9ee68-147">Ссылка на идентификатор приложения</span><span class="sxs-lookup"><span data-stu-id="9ee68-147">Reference your application ID</span></span> 

<span data-ttu-id="9ee68-148">Клиентское приложение использует tooaccess ID (также назывались tooas hello идентификатор клиента) приложения hello Azure AD во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="9ee68-148">Your client application uses hello application ID (also referred tooas hello client ID) tooaccess Azure AD at runtime.</span></span> <span data-ttu-id="9ee68-149">После регистрации приложения в Azure portal hello обновите идентификатор приложения код toouse hello, предоставляемые Azure AD для зарегистрированного приложения.</span><span class="sxs-lookup"><span data-stu-id="9ee68-149">Once you've registered your application in hello Azure portal, update your code toouse hello application ID provided by Azure AD for your registered application.</span></span> <span data-ttu-id="9ee68-150">В hello AccountManagement образец приложения скопируйте код вашего приложения с подходящей константой hello Azure toohello портала:</span><span class="sxs-lookup"><span data-stu-id="9ee68-150">In hello AccountManagement sample application, copy your application ID from hello Azure portal toohello appropriate constant:</span></span>

```csharp
// Specify hello unique identifier (hello "Client ID") for your application. This is required so that your
// native client application (i.e. this sample) can access hello Microsoft Azure AD Graph API. For information
// about registering an application in Azure Active Directory, please see "Adding an Application" here:
// https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/
private const string ClientId = "<application-id>";
```
<span data-ttu-id="9ee68-151">Кроме того, скопируйте URI, которое определено во время процесса регистрации hello перенаправления hello.</span><span class="sxs-lookup"><span data-stu-id="9ee68-151">Also copy hello redirect URI that you specified during hello registration process.</span></span> <span data-ttu-id="9ee68-152">Здравствуйте, URI, заданный в коде должен соответствовать hello перенаправления, указанный при регистрации приложения hello URI перенаправления.</span><span class="sxs-lookup"><span data-stu-id="9ee68-152">hello redirect URI specified in your code must match hello redirect URI that you provided when you registered hello application.</span></span>

```csharp
// hello URI toowhich Azure AD will redirect in response tooan OAuth 2.0 request. This value is
// specified by you when you register an application with AAD (see ClientId comment). It does not
// need toobe a real endpoint, but must be a valid URI (e.g. https://accountmgmtsampleapp).
private const string RedirectUri = "http://myaccountmanagementsample";
```

## <a name="acquire-an-azure-ad-authentication-token"></a><span data-ttu-id="9ee68-153">Получение маркера проверки подлинности Azure AD</span><span class="sxs-lookup"><span data-stu-id="9ee68-153">Acquire an Azure AD authentication token</span></span>

<span data-ttu-id="9ee68-154">После регистрации примера AccountManagement hello в клиенте Azure AD hello и обновите ваш значениями hello Образец исходного кода, образец hello — Готово tooauthenticate, с помощью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9ee68-154">After you register hello AccountManagement sample in hello Azure AD tenant and update hello sample source code with your values, hello sample is ready tooauthenticate using Azure AD.</span></span> <span data-ttu-id="9ee68-155">При запуске образца hello hello ADAL попыток tooacquire маркер проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="9ee68-155">When you run hello sample, hello ADAL attempts tooacquire an authentication token.</span></span> <span data-ttu-id="9ee68-156">На этом этапе предлагается ввести учетные данные Майкрософт:</span><span class="sxs-lookup"><span data-stu-id="9ee68-156">At this step, it prompts you for your Microsoft credentials:</span></span> 

```csharp
// Obtain an access token using hello "common" AAD resource. This allows hello application
// tooquery AAD for information that lies outside hello application's tenant (such as for
// querying subscription information in your Azure account).
AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
AuthenticationResult authResult = authContext.AcquireToken(ResourceUri,
                                                        ClientId,
                                                        new Uri(RedirectUri),
                                                        PromptBehavior.Auto);
```

<span data-ttu-id="9ee68-157">После ввода учетных данных, пример приложения hello продолжением toohello tooissue проверку подлинности запросов управления пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="9ee68-157">After you provide your credentials, hello sample application can proceed tooissue authenticated requests toohello Batch management service.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9ee68-158">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9ee68-158">Next steps</span></span>

<span data-ttu-id="9ee68-159">Дополнительные сведения о запуске hello [AccountManagement образец приложения][acct_mgmt_sample], в разделе [пакетное управление учетными записями и квоты с hello пакета управления клиентской библиотеки для .NET](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="9ee68-159">For more information on running hello [AccountManagement sample application][acct_mgmt_sample], see [Manage Batch accounts and quotas with hello Batch Management client library for .NET](batch-management-dotnet.md).</span></span>

<span data-ttu-id="9ee68-160">toolearn Дополнительные сведения о Azure AD см. hello [документация Azure Active Directory](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="9ee68-160">toolearn more about Azure AD, see hello [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="9ee68-161">Подробные примеры, показывающие, как toouse ADAL доступны в hello [образцы кода Azure](https://azure.microsoft.com/resources/samples/?service=active-directory) библиотеки.</span><span class="sxs-lookup"><span data-stu-id="9ee68-161">In-depth examples showing how toouse ADAL are available in hello [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=active-directory) library.</span></span>

<span data-ttu-id="9ee68-162">tooauthenticate пакета службы приложения с помощью Azure AD см. [решения службы проверки подлинности пакета с помощью Active Directory](batch-aad-auth.md).</span><span class="sxs-lookup"><span data-stu-id="9ee68-162">tooauthenticate Batch service applications using Azure AD, see [Authenticate Batch service solutions with Active Directory](batch-aad-auth.md).</span></span> 


[aad_about]: ../active-directory/active-directory-whatis.md "Что такое Microsoft Azure Active Directory?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Сценарии аутентификации в Azure Active Directory"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Интеграция приложений с Azure Active Directory"
[acct_mgmt_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/AccountManagement
[azure_portal]: http://portal.azure.com
[resman_overview]: ../azure-resource-manager/resource-group-overview.md
