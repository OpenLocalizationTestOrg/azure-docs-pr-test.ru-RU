---
title: "Аутентификация решений по управлению пакетной службой с помощью Azure Active Directory | Документация Майкрософт"
description: "Аутентификация приложений, созданных с помощью Azure Resource Manager и поставщика ресурсов пакетной службы, выполняется с использование Azure AD."
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
ms.openlocfilehash: 26d4adf4f74f9aacc4cf8cf24be293ebdb4d63c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-batch-management-solutions-with-active-directory"></a><span data-ttu-id="90fd6-103">Аутентификация решений по управлению пакетной службой с помощью Active Directory</span><span class="sxs-lookup"><span data-stu-id="90fd6-103">Authenticate Batch Management solutions with Active Directory</span></span>

<span data-ttu-id="90fd6-104">Аутентификация приложений, вызывающих службу управления пакетной службой Azure, выполняется с помощью [Azure Active Directory][aad_about] (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="90fd6-104">Applications that call the Azure Batch Management service authenticate with [Azure Active Directory][aad_about] (Azure AD).</span></span> <span data-ttu-id="90fd6-105">Azure AD — многопользовательский облачный каталог и служба управления удостоверениями корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="90fd6-105">Azure AD is Microsoft’s multi-tenant cloud based directory and identity management service.</span></span> <span data-ttu-id="90fd6-106">Инфраструктура Azure уже использует Azure AD для проверки подлинности клиентов, администраторов служб и пользователей организации.</span><span class="sxs-lookup"><span data-stu-id="90fd6-106">Azure itself uses Azure AD for the authentication of its customers, service administrators, and organizational users.</span></span>

<span data-ttu-id="90fd6-107">Библиотека .NET для управления пакетной службой предоставляет типы для работы с учетными записями пакетной службы, ключами учетной записи, приложениями и пакетами приложений.</span><span class="sxs-lookup"><span data-stu-id="90fd6-107">The Batch Management .NET library exposes types for working with Batch accounts, account keys, applications, and application packages.</span></span> <span data-ttu-id="90fd6-108">Данная библиотека является клиентом поставщика ресурсов Azure и используется совместно с [Azure Resource Manager][resman_overview] для программного управления этими ресурсами.</span><span class="sxs-lookup"><span data-stu-id="90fd6-108">The Batch Management .NET library is an Azure resource provider client, and is used together with [Azure Resource Manager][resman_overview] to manage these resources programmatically.</span></span> <span data-ttu-id="90fd6-109">Служба Azure AD необходима для аутентификации запросов, выполненных с помощью любого клиента поставщика ресурсов Azure, а также библиотеки .NET для управления пакетной службой и [Azure Resource Manager][resman_overview].</span><span class="sxs-lookup"><span data-stu-id="90fd6-109">Azure AD is required to authenticate requests made through any Azure resource provider client, including the Batch Management .NET library, and through [Azure Resource Manager][resman_overview].</span></span>

<span data-ttu-id="90fd6-110">В этой статье рассматривается выполнение аутентификации в приложениях, применяющих библиотеку .NET для управления пакетной службой, с помощью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="90fd6-110">In this article, we explore using Azure AD to authenticate from applications that use the Batch Management .NET library.</span></span> <span data-ttu-id="90fd6-111">Мы покажем, как использовать Azure AD для аутентификации администратора или соадминистратора подписки с помощью встроенной аутентификации.</span><span class="sxs-lookup"><span data-stu-id="90fd6-111">We show how to use Azure AD to authenticate a subscription administrator or co-administrator, using integrated authentication.</span></span> <span data-ttu-id="90fd6-112">Чтобы изучить использование Azure AD с библиотекой .NET для управления пакетной службой, мы используем пример проекта [AccountManagment][acct_mgmt_sample], который доступен на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="90fd6-112">We use the [AccountManagment][acct_mgmt_sample] sample project, available on GitHub, to walk through using Azure AD with the Batch Management .NET library.</span></span>

<span data-ttu-id="90fd6-113">Дополнительные сведения об использовании библиотеки .NET для управления пакетной службой и примера AccountManagement см. в статье [Управление учетными записями и квотами пакетной службы с помощью клиентской библиотеки .NET для управления пакетной службой](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="90fd6-113">To learn more about using the Batch Management .NET library and the AccountManagement sample, see [Manage Batch accounts and quotas with the Batch Management client library for .NET](batch-management-dotnet.md).</span></span>

## <a name="register-your-application-with-azure-ad"></a><span data-ttu-id="90fd6-114">Регистрация приложения в Azure AD</span><span class="sxs-lookup"><span data-stu-id="90fd6-114">Register your application with Azure AD</span></span>

<span data-ttu-id="90fd6-115">[Библиотека проверки подлинности Azure Active Directory][aad_adal] (ADAL) предоставляет программный интерфейс Azure AD для использования в приложениях.</span><span class="sxs-lookup"><span data-stu-id="90fd6-115">The Azure [Active Directory Authentication Library][aad_adal] (ADAL) provides a programmatic interface to Azure AD for use within your applications.</span></span> <span data-ttu-id="90fd6-116">Чтобы вызвать ADAL в приложении, необходимо зарегистрировать приложение в клиенте Azure AD.</span><span class="sxs-lookup"><span data-stu-id="90fd6-116">To call ADAL from your application, you must register your application in an Azure AD tenant.</span></span> <span data-ttu-id="90fd6-117">При регистрации приложения в клиенте Azure AD нужно предоставить Azure AD сведения о приложении, включая его имя.</span><span class="sxs-lookup"><span data-stu-id="90fd6-117">When you register your application, you supply Azure AD with information about your application, including a name for it within the Azure AD tenant.</span></span> <span data-ttu-id="90fd6-118">После этого служба Azure AD предоставит идентификатор приложения, позволяющий связать с ней приложение во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="90fd6-118">Azure AD then provides an application ID that you use to associate your application with Azure AD at runtime.</span></span> <span data-ttu-id="90fd6-119">Дополнительные сведения об идентификаторе приложения см. в статье [Объекты приложения и субъекта-службы в Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="90fd6-119">To learn more about the application ID, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span>

<span data-ttu-id="90fd6-120">Чтобы зарегистрировать пример приложения AccountManagement, выполните инструкции, приведенные в разделе [Добавление приложения](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) статьи [Интеграция приложений с Azure Active Directory][aad_integrate].</span><span class="sxs-lookup"><span data-stu-id="90fd6-120">To register the AccountManagement sample application, follow the steps in the [Adding an Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span></span> <span data-ttu-id="90fd6-121">Укажите в качестве типа приложения **собственное клиентское приложение**.</span><span class="sxs-lookup"><span data-stu-id="90fd6-121">Specify **Native Client Application** for the type of application.</span></span> <span data-ttu-id="90fd6-122">`urn:ietf:wg:oauth:2.0:oob` — это стандартный отраслевой универсальный код ресурса (URI) OAuth 2.0, используемый в качестве **URI перенаправления**.</span><span class="sxs-lookup"><span data-stu-id="90fd6-122">The industry standard OAuth 2.0 URI for the **Redirect URI** is `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="90fd6-123">Тем не менее в качестве **URI перенаправления** можно указать любой допустимый универсальный код ресурса (URI) (например, `http://myaccountmanagementsample`). Реальную конечную точку указывать необязательно.</span><span class="sxs-lookup"><span data-stu-id="90fd6-123">However, you can specify any valid URI (such as `http://myaccountmanagementsample`) for the **Redirect URI**, as it does not need to be a real endpoint:</span></span>

![](./media/batch-aad-auth-management/app-registration-management-plane.png)

<span data-ttu-id="90fd6-124">После завершения процесса регистрации отобразится указанный для вашего приложения идентификатор приложения и объекта (субъекта-службы).</span><span class="sxs-lookup"><span data-stu-id="90fd6-124">Once you complete the registration process, you'll see the application ID and the object (service principal) ID listed for your application.</span></span>  

![](./media/batch-aad-auth-management/app-registration-client-id.png)

## <a name="grant-the-azure-resource-manager-api-access-to-your-application"></a><span data-ttu-id="90fd6-125">Предоставление доступа API Azure Resource Manager к приложению</span><span class="sxs-lookup"><span data-stu-id="90fd6-125">Grant the Azure Resource Manager API access to your application</span></span>

<span data-ttu-id="90fd6-126">Теперь необходимо делегировать доступ к приложению для API Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="90fd6-126">Next, you'll need to delegate access to your application to the Azure Resource Manager API.</span></span> <span data-ttu-id="90fd6-127">Идентификатором Azure AD для API Resource Manager является **API управления службами Windows Azure**.</span><span class="sxs-lookup"><span data-stu-id="90fd6-127">The Azure AD identifier for the Resource Manager API is **Windows Azure Service Management API**.</span></span>

<span data-ttu-id="90fd6-128">На портале Azure сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="90fd6-128">Follow these steps in the Azure portal:</span></span>

1. <span data-ttu-id="90fd6-129">В левой области навигации портала Azure выберите **Больше служб**, щелкните **Регистрация приложений**, а затем нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="90fd6-129">In the left-hand navigation pane of the Azure portal, choose **More Services**, click **App Registrations**, and click **Add**.</span></span>
2. <span data-ttu-id="90fd6-130">Найдите имя приложения в списке зарегистрированных приложений:</span><span class="sxs-lookup"><span data-stu-id="90fd6-130">Search for the name of your application in the list of app registrations:</span></span>

    ![Поиск имени приложения](./media/batch-aad-auth-management/search-app-registration.png)

3. <span data-ttu-id="90fd6-132">Откройте колонку **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="90fd6-132">Display the **Settings** blade.</span></span> <span data-ttu-id="90fd6-133">В разделе **Доступ через API** выберите **Необходимые разрешения**.</span><span class="sxs-lookup"><span data-stu-id="90fd6-133">In the **API Access** section, select **Required permissions**.</span></span>
4. <span data-ttu-id="90fd6-134">Щелкните **Добавить** для добавления нового необходимого разрешения.</span><span class="sxs-lookup"><span data-stu-id="90fd6-134">Click **Add** to add a new required permission.</span></span> 
5. <span data-ttu-id="90fd6-135">На шаге 1 введите **API управления службами Windows Azure**, выберите этот API в списке результатов и нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="90fd6-135">In step 1, enter **Windows Azure Service Management API**, select that API from the list of results, and click the **Select** button.</span></span>
6. <span data-ttu-id="90fd6-136">На шаге 2 установите флажок рядом с параметром **Access Azure classic deployment model as organization users** (Доступ к классической модели развертывания Azure от имени пользователей организации) и нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="90fd6-136">In step 2, select the check box next to **Access Azure classic deployment model as organization users**, and click the **Select** button.</span></span>
7. <span data-ttu-id="90fd6-137">Нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="90fd6-137">Click the **Done** button.</span></span>

<span data-ttu-id="90fd6-138">Теперь в колонке **Необходимые разрешения** показано, что разрешения на доступ к приложению предоставлены и интерфейсам API Resource Manager, и ADAL.</span><span class="sxs-lookup"><span data-stu-id="90fd6-138">The **Required Permissions** blade now shows that permissions to your application are granted to both the ADAL and Resource Manager APIs.</span></span> <span data-ttu-id="90fd6-139">Разрешения ADAL предоставляются по умолчанию во время регистрации приложения в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="90fd6-139">Permissions are granted to ADAL by default when you first register your app with Azure AD.</span></span>

![Делегирование разрешений для API Azure Resource Manager](./media/batch-aad-auth-management/required-permissions-management-plane.png)

## <a name="azure-ad-endpoints"></a><span data-ttu-id="90fd6-141">Конечные точки Azure AD</span><span class="sxs-lookup"><span data-stu-id="90fd6-141">Azure AD endpoints</span></span>

<span data-ttu-id="90fd6-142">Чтобы выполнить аутентификацию решений по управлению пакетной службой с помощью Azure AD, необходимо иметь две известные конечные точки.</span><span class="sxs-lookup"><span data-stu-id="90fd6-142">To authenticate your Batch Management solutions with Azure AD, you'll need two well-known endpoints.</span></span>

- <span data-ttu-id="90fd6-143">**Общая конечная точка Azure AD** предоставляет универсальный интерфейс для сбора учетных данных при отсутствии конкретного клиента (как в случае со встроенной аутентификацией):</span><span class="sxs-lookup"><span data-stu-id="90fd6-143">The **Azure AD common endpoint** provides a generic credential gathering interface when a specific tenant is not provided, as in the case of integrated authentication:</span></span>

    `https://login.microsoftonline.com/common`

- <span data-ttu-id="90fd6-144">**Конечная точка Azure Resource Manager** используется для получения токена для аутентификации запросов к службе управления пакетной службой:</span><span class="sxs-lookup"><span data-stu-id="90fd6-144">The **Azure Resource Manager endpoint** is used to acquire a token for authenticating requests to the Batch management service:</span></span>

    `https://management.core.windows.net/`

<span data-ttu-id="90fd6-145">Пример приложения AccountManagement определяет константы для этих конечных точек.</span><span class="sxs-lookup"><span data-stu-id="90fd6-145">The AccountManagement sample application defines constants for these endpoints.</span></span> <span data-ttu-id="90fd6-146">Оставьте их без изменений:</span><span class="sxs-lookup"><span data-stu-id="90fd6-146">Leave these constants unchanged:</span></span>

```csharp
// Azure Active Directory "common" endpoint.
private const string AuthorityUri = "https://login.microsoftonline.com/common";
// Azure Resource Manager endpoint 
private const string ResourceUri = "https://management.core.windows.net/";
```

## <a name="reference-your-application-id"></a><span data-ttu-id="90fd6-147">Ссылка на идентификатор приложения</span><span class="sxs-lookup"><span data-stu-id="90fd6-147">Reference your application ID</span></span> 

<span data-ttu-id="90fd6-148">Клиентское приложение использует идентификатор приложения (также называемый идентификатором клиента) для доступа к Azure AD во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="90fd6-148">Your client application uses the application ID (also referred to as the client ID) to access Azure AD at runtime.</span></span> <span data-ttu-id="90fd6-149">После регистрации приложения на портале Azure обновите код, указав в нем идентификатор приложения, предоставленный Azure AD для зарегистрированного приложения.</span><span class="sxs-lookup"><span data-stu-id="90fd6-149">Once you've registered your application in the Azure portal, update your code to use the application ID provided by Azure AD for your registered application.</span></span> <span data-ttu-id="90fd6-150">В примере приложения AccountManagement скопируйте идентификатор приложения из портала Azure в соответствующую константу:</span><span class="sxs-lookup"><span data-stu-id="90fd6-150">In the AccountManagement sample application, copy your application ID from the Azure portal to the appropriate constant:</span></span>

```csharp
// Specify the unique identifier (the "Client ID") for your application. This is required so that your
// native client application (i.e. this sample) can access the Microsoft Azure AD Graph API. For information
// about registering an application in Azure Active Directory, please see "Adding an Application" here:
// https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/
private const string ClientId = "<application-id>";
```
<span data-ttu-id="90fd6-151">Скопируйте также URI перенаправления, который вы указали во время процесса регистрации.</span><span class="sxs-lookup"><span data-stu-id="90fd6-151">Also copy the redirect URI that you specified during the registration process.</span></span> <span data-ttu-id="90fd6-152">URI перенаправления, указанный в коде, должен соответствовать URI перенаправления, который был указан при регистрации приложения.</span><span class="sxs-lookup"><span data-stu-id="90fd6-152">The redirect URI specified in your code must match the redirect URI that you provided when you registered the application.</span></span>

```csharp
// The URI to which Azure AD will redirect in response to an OAuth 2.0 request. This value is
// specified by you when you register an application with AAD (see ClientId comment). It does not
// need to be a real endpoint, but must be a valid URI (e.g. https://accountmgmtsampleapp).
private const string RedirectUri = "http://myaccountmanagementsample";
```

## <a name="acquire-an-azure-ad-authentication-token"></a><span data-ttu-id="90fd6-153">Получение маркера проверки подлинности Azure AD</span><span class="sxs-lookup"><span data-stu-id="90fd6-153">Acquire an Azure AD authentication token</span></span>

<span data-ttu-id="90fd6-154">После регистрации приложения AccountManagement в клиенте Azure AD и добавления собственных значений в пример исходного кода этот пример можно использовать для аутентификации с помощью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="90fd6-154">After you register the AccountManagement sample in the Azure AD tenant and update the sample source code with your values, the sample is ready to authenticate using Azure AD.</span></span> <span data-ttu-id="90fd6-155">При запуске примера ADAL пытается получить маркер проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="90fd6-155">When you run the sample, the ADAL attempts to acquire an authentication token.</span></span> <span data-ttu-id="90fd6-156">На этом этапе предлагается ввести учетные данные Майкрософт:</span><span class="sxs-lookup"><span data-stu-id="90fd6-156">At this step, it prompts you for your Microsoft credentials:</span></span> 

```csharp
// Obtain an access token using the "common" AAD resource. This allows the application
// to query AAD for information that lies outside the application's tenant (such as for
// querying subscription information in your Azure account).
AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
AuthenticationResult authResult = authContext.AcquireToken(ResourceUri,
                                                        ClientId,
                                                        new Uri(RedirectUri),
                                                        PromptBehavior.Auto);
```

<span data-ttu-id="90fd6-157">После указания учетных данных пример приложения может отправлять запросы, прошедшие проверку подлинности, к службе управления пакетами.</span><span class="sxs-lookup"><span data-stu-id="90fd6-157">After you provide your credentials, the sample application can proceed to issue authenticated requests to the Batch management service.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="90fd6-158">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="90fd6-158">Next steps</span></span>

<span data-ttu-id="90fd6-159">Дополнительные сведения о выполнении [примера приложения AccountManagement][acct_mgmt_sample] см. в статье [Управление учетными записями и квотами пакетной службы с помощью клиентской библиотеки .NET для управления пакетной службой](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="90fd6-159">For more information on running the [AccountManagement sample application][acct_mgmt_sample], see [Manage Batch accounts and quotas with the Batch Management client library for .NET](batch-management-dotnet.md).</span></span>

<span data-ttu-id="90fd6-160">Дополнительные сведения о службе Azure AD см. в [документации по Azure Active Directory](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="90fd6-160">To learn more about Azure AD, see the [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="90fd6-161">Подробные примеры, показывающие, как использовать ADAL, доступны в библиотеке [примеров кода Azure](https://azure.microsoft.com/resources/samples/?service=active-directory).</span><span class="sxs-lookup"><span data-stu-id="90fd6-161">In-depth examples showing how to use ADAL are available in the [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=active-directory) library.</span></span>

<span data-ttu-id="90fd6-162">Дополнительные сведения об аутентификации приложений пакетной службы с помощью Azure AD см. в статье [Аутентификация решений пакетной службы с помощью Active Directory](batch-aad-auth.md).</span><span class="sxs-lookup"><span data-stu-id="90fd6-162">To authenticate Batch service applications using Azure AD, see [Authenticate Batch service solutions with Active Directory](batch-aad-auth.md).</span></span> 


<span data-ttu-id="90fd6-163">[aad_about]: ../active-directory/active-directory-whatis.md "Что такое Microsoft Azure Active Directory?"</span><span class="sxs-lookup"><span data-stu-id="90fd6-163">[aad_about]: ../active-directory/active-directory-whatis.md "What is Azure Active Directory?"</span></span>
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
<span data-ttu-id="90fd6-164">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Сценарии аутентификации в Azure Active Directory"</span><span class="sxs-lookup"><span data-stu-id="90fd6-164">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Authentication Scenarios for Azure AD"</span></span>
<span data-ttu-id="90fd6-165">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Интеграция приложений с Azure Active Directory"</span><span class="sxs-lookup"><span data-stu-id="90fd6-165">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrating Applications with Azure Active Directory"</span></span>
[acct_mgmt_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/AccountManagement
[azure_portal]: http://portal.azure.com
[resman_overview]: ../azure-resource-manager/resource-group-overview.md
