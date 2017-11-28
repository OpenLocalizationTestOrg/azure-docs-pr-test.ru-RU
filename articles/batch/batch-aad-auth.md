---
title: "Аутентификация решений пакетной службы Azure с помощью Azure Active Directory | Документация Майкрософт"
description: "Пакетная служба поддерживает Azure AD для аутентификации из пакетной службы."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/20/2017
ms.author: tamram
ms.openlocfilehash: 9c03bde919c46cd301229255c0b12ee69dda6f78
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-batch-service-solutions-with-active-directory"></a><span data-ttu-id="ba6d6-103">Аутентификация решений пакетной службы с помощью Active Directory</span><span class="sxs-lookup"><span data-stu-id="ba6d6-103">Authenticate Batch service solutions with Active Directory</span></span>

<span data-ttu-id="ba6d6-104">Пакетная служба Azure поддерживает аутентификацию [Azure Active Directory][aad_about] (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ba6d6-104">Azure Batch supports authentication with [Azure Active Directory][aad_about] (Azure AD).</span></span> <span data-ttu-id="ba6d6-105">Azure AD — многопользовательский облачный каталог и служба управления удостоверениями корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-105">Azure AD is Microsoft’s multi-tenant cloud based directory and identity management service.</span></span> <span data-ttu-id="ba6d6-106">Инфраструктура Azure использует Azure AD для аутентификации клиентов, администраторов служб и пользователей организации.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-106">Azure itself uses Azure AD to authenticate its customers, service administrators, and organizational users.</span></span>

<span data-ttu-id="ba6d6-107">Процесс аутентификации Azure AD в пакетной службе Azure можно выполнить двумя способами:</span><span class="sxs-lookup"><span data-stu-id="ba6d6-107">When using Azure AD authentication with Azure Batch, you can authenticate in one of two ways:</span></span>

- <span data-ttu-id="ba6d6-108">Аутентификация пользователя, взаимодействующего с приложением, с использованием **встроенной аутентификации**.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-108">By using **integrated authentication** to authenticate a user that is interacting with the application.</span></span> <span data-ttu-id="ba6d6-109">Приложение, использующее встроенную аутентификацию, собирает учетные данные пользователя и использует их для аутентификации доступа к ресурсам пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-109">An application using integrated authentication gathers a user's credentials and uses those credentials to authenticate access to Batch resources.</span></span>
- <span data-ttu-id="ba6d6-110">Аутентификация автоматического приложения с использованием **субъекта-службы**.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-110">By using a **service principal** to authenticate an unattended application.</span></span> <span data-ttu-id="ba6d6-111">Субъект-служба определяет политику и разрешения приложения, чтобы представить приложение при получении доступа к ресурсам в среде выполнения.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-111">A service principal defines the policy and permissions for an application in order to represent the application when accessing resources at runtime.</span></span>

<span data-ttu-id="ba6d6-112">Дополнительные сведения о службе Azure AD см. в [документации по Azure Active Directory](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="ba6d6-112">To learn more about Azure AD, see the [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span>

## <a name="authentication-and-pool-allocation-mode"></a><span data-ttu-id="ba6d6-113">Режим аутентификации и выделения пула</span><span class="sxs-lookup"><span data-stu-id="ba6d6-113">Authentication and pool allocation mode</span></span>

<span data-ttu-id="ba6d6-114">При создании учетной записи пакетной службы вы можете указать, где должны быть выделены пулы, созданные для этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-114">When you create a Batch account, you can specify where pools created for that account should be allocated.</span></span> <span data-ttu-id="ba6d6-115">Их можно выделить в подписке пакетной службы по умолчанию или подписке пользователя.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-115">You can choose to allocate pools either in the default Batch service subscription or in a user subscription.</span></span> <span data-ttu-id="ba6d6-116">От вашего выбора зависит способ аутентификации доступа к ресурсам в этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-116">Your choice affects how you authenticate access to resources in that account.</span></span>

- <span data-ttu-id="ba6d6-117">**Подписка пакетной службы.**</span><span class="sxs-lookup"><span data-stu-id="ba6d6-117">**Batch service subscription**.</span></span> <span data-ttu-id="ba6d6-118">По умолчанию пулы выделяются в подписке пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-118">By default, Batch pools are allocated in a Batch service subscription.</span></span> <span data-ttu-id="ba6d6-119">При выборе этого варианта аутентификацию доступа к ресурсам в этой учетной записи можно выполнять с помощью [общего ключа](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) или Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-119">If you choose this option, you can authenticate access to resources in that account either with [Shared Key](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) or with Azure AD.</span></span>
- <span data-ttu-id="ba6d6-120">**Подписка пользователя.**</span><span class="sxs-lookup"><span data-stu-id="ba6d6-120">**User subscription.**</span></span> <span data-ttu-id="ba6d6-121">Вы можете выделить пулы пакетной службы в указанной подписке пользователя.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-121">You can choose to allocate Batch pools in a user subscription that you specify.</span></span> <span data-ttu-id="ba6d6-122">Если выбран этот вариант, нужно выполнять проверку подлинности с помощью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-122">If you choose this option, you must authenticate with Azure AD.</span></span>

## <a name="endpoints-for-authentication"></a><span data-ttu-id="ba6d6-123">Конечные точки аутентификации</span><span class="sxs-lookup"><span data-stu-id="ba6d6-123">Endpoints for authentication</span></span>

<span data-ttu-id="ba6d6-124">Чтобы выполнить аутентификацию приложений пакетной службы с помощью Azure AD, необходимо включить некоторые известные конечные точки в код.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-124">To authenticate Batch applications with Azure AD, you need to include some well-known endpoints in your code.</span></span>

### <a name="azure-ad-endpoint"></a><span data-ttu-id="ba6d6-125">Конечная точка Azure AD</span><span class="sxs-lookup"><span data-stu-id="ba6d6-125">Azure AD endpoint</span></span>

<span data-ttu-id="ba6d6-126">Базовая конечная точка авторизации Azure AD:</span><span class="sxs-lookup"><span data-stu-id="ba6d6-126">The base Azure AD authority endpoint is:</span></span>

`https://login.microsoftonline.com/`

<span data-ttu-id="ba6d6-127">Чтобы выполнить аутентификацию с помощью Azure AD, вам потребуется эта конечная точка и идентификатор клиента (идентификатором каталога).</span><span class="sxs-lookup"><span data-stu-id="ba6d6-127">To authenticate with Azure AD, you use this endpoint together with the tenant ID (directory ID).</span></span> <span data-ttu-id="ba6d6-128">Идентификатор клиента определяет клиент Azure AD для аутентификации.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-128">The tenant ID identifies the Azure AD tenant to use for authentication.</span></span> <span data-ttu-id="ba6d6-129">Чтобы получить идентификатор клиента, выполните указания, описанные в разделе [Получение идентификатора клиента для Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="ba6d6-129">To retrieve the tenant ID, follow the steps outlined in [Get the tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

`https://login.microsoftonline.com/<tenant-id>`

> [!NOTE] 
> <span data-ttu-id="ba6d6-130">В процессе аутентификации с использованием субъекта-службы требуется конечная точка определенного клиента.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-130">The tenant-specific endpoint is required when you authenticate using a service principal.</span></span> 
> 
> <span data-ttu-id="ba6d6-131">При аутентификации с помощью встроенной аутентификации эта конечная точка является не обязательной. Тем не менее мы советуем использовать ее.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-131">The tenant-specific endpoint is optional when you authenticate using integrated authentication, but recommended.</span></span> <span data-ttu-id="ba6d6-132">Но вы также можете использовать общую конечную точку Azure AD,</span><span class="sxs-lookup"><span data-stu-id="ba6d6-132">However, you can also use the Azure AD common endpoint.</span></span> <span data-ttu-id="ba6d6-133">которая предоставляет универсальный интерфейс для сбора общих учетных данных в случае отсутствия конкретного клиента.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-133">The common endpoint provides a generic credential gathering interface when a specific tenant is not provided.</span></span> <span data-ttu-id="ba6d6-134">Общая конечная точка выглядит так: `https://login.microsoftonline.com/common`.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-134">The common endpoint is `https://login.microsoftonline.com/common`.</span></span>
>
>

<span data-ttu-id="ba6d6-135">Дополнительные сведения о конечных точках Azure AD см. в статье [Сценарии аутентификации в Azure Active Directory][aad_auth_scenarios].</span><span class="sxs-lookup"><span data-stu-id="ba6d6-135">For more information about Azure AD endpoints, see [Authentication Scenarios for Azure AD][aad_auth_scenarios].</span></span>

### <a name="batch-resource-endpoint"></a><span data-ttu-id="ba6d6-136">Конечная точка ресурса пакетной службы</span><span class="sxs-lookup"><span data-stu-id="ba6d6-136">Batch resource endpoint</span></span>

<span data-ttu-id="ba6d6-137">**Конечная точка ресурса пакетной службы Azure** позволяет получить токен аутентификации запросов для пакетной службы:</span><span class="sxs-lookup"><span data-stu-id="ba6d6-137">Use the **Azure Batch resource endpoint** to acquire a token for authenticating requests to the Batch service:</span></span>

`https://batch.core.windows.net/`

## <a name="register-your-application-with-a-tenant"></a><span data-ttu-id="ba6d6-138">Регистрация приложения в клиенте</span><span class="sxs-lookup"><span data-stu-id="ba6d6-138">Register your application with a tenant</span></span>

<span data-ttu-id="ba6d6-139">При использовании Azure AD для аутентификации в первую очередь необходимо зарегистрировать приложение в клиенте Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-139">The first step in using Azure AD to authenticate is registering your application in an Azure AD tenant.</span></span> <span data-ttu-id="ba6d6-140">Зарегистрировав приложение, вы сможете вызвать [библиотеку аутентификации Azure Active Directory ][aad_adal] (ADAL) из кода.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-140">Registering your application enables you to call the Azure [Active Directory Authentication Library][aad_adal] (ADAL) from your code.</span></span> <span data-ttu-id="ba6d6-141">Эта библиотека предоставляет API для аутентификации с помощью Azure AD в приложении.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-141">The ADAL provides an API for authenticating with Azure AD from your application.</span></span> <span data-ttu-id="ba6d6-142">Регистрация приложения необходима, если вы планируете использовать встроенную аутентификацию или аутентификацию с использованием субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-142">Registering your application is required whether you plan to use integrated authentication or a service principal.</span></span>

<span data-ttu-id="ba6d6-143">При регистрации приложения вы отправляете сведения о приложении в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-143">When you register your application, you supply information about your application to Azure AD.</span></span> <span data-ttu-id="ba6d6-144">После этого служба Azure AD предоставит идентификатор приложения, позволяющий связать с ней приложение во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-144">Azure AD then provides an application ID that you use to associate your application with Azure AD at runtime.</span></span> <span data-ttu-id="ba6d6-145">Дополнительные сведения об идентификаторе приложения см. в статье [Объекты приложения и субъекта-службы в Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="ba6d6-145">To learn more about the application ID, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span>

<span data-ttu-id="ba6d6-146">Чтобы зарегистрировать приложение пакетной службы, выполните инструкции, приведенные в разделе [Добавление приложения](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) статьи [Интеграция приложений с Azure Active Directory][aad_integrate].</span><span class="sxs-lookup"><span data-stu-id="ba6d6-146">To register your Batch application, follow the steps in the [Adding an Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span></span> <span data-ttu-id="ba6d6-147">При регистрации приложения как собственного вы можете указать любой допустимый универсальный код ресурса (URI) в качестве **URI перенаправления**.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-147">If you register your application as a Native Application, you can specify any valid URI for the **Redirect URI**.</span></span> <span data-ttu-id="ba6d6-148">Реальную конечную точку указывать необязательно.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-148">It does not need to be a real endpoint.</span></span>

<span data-ttu-id="ba6d6-149">После регистрации приложения отобразится его идентификатор:</span><span class="sxs-lookup"><span data-stu-id="ba6d6-149">After you've registered your application, you'll see the application ID:</span></span>

![Регистрация приложения пакетной службы в Azure AD](./media/batch-aad-auth/app-registration-data-plane.png)

<span data-ttu-id="ba6d6-151">Дополнительные сведения о регистрации приложения в Azure AD см. в статье [Сценарии аутентификации в Azure Active Directory](../active-directory/develop/active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="ba6d6-151">For more information about registering an application with Azure AD, see [Authentication Scenarios for Azure AD](../active-directory/develop/active-directory-authentication-scenarios.md).</span></span>

## <a name="get-the-tenant-id-for-your-active-directory"></a><span data-ttu-id="ba6d6-152">Получение идентификатора клиента для Active Directory</span><span class="sxs-lookup"><span data-stu-id="ba6d6-152">Get the tenant ID for your Active Directory</span></span>

<span data-ttu-id="ba6d6-153">Идентификатор клиента определяет клиент Azure AD, который предоставляет службы аутентификации приложению.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-153">The tenant ID identifies the Azure AD tenant that provides authentication services to your application.</span></span> <span data-ttu-id="ba6d6-154">Чтобы получить идентификатор клиента, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="ba6d6-154">To get the tenant ID, follow these steps:</span></span>

1. <span data-ttu-id="ba6d6-155">На портале Azure выберите Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-155">In the Azure portal, select your Active Directory.</span></span>
2. <span data-ttu-id="ba6d6-156">Щелкните **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-156">Click **Properties**.</span></span>
3. <span data-ttu-id="ba6d6-157">Скопируйте значение GUID, указанное для идентификатора каталога.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-157">Copy the GUID value provided for the directory ID.</span></span> <span data-ttu-id="ba6d6-158">Это значение также называется идентификатором клиента.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-158">This value is also called the tenant ID.</span></span>

![Копирование идентификатора каталога](./media/batch-aad-auth/aad-directory-id.png)


## <a name="use-integrated-authentication"></a><span data-ttu-id="ba6d6-160">Использование встроенной аутентификации</span><span class="sxs-lookup"><span data-stu-id="ba6d6-160">Use integrated authentication</span></span>

<span data-ttu-id="ba6d6-161">Чтобы выполнить аутентификацию с помощью встроенной аутентификации, необходимо предоставить приложению разрешения на подключение к API пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-161">To authenticate with integrated authentication, you need to grant your application permissions to connect to the Batch service API.</span></span> <span data-ttu-id="ba6d6-162">Это позволит ему выполнить аутентификацию вызовов к API пакетной службы с помощью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-162">This step enables your application to authenticate calls to the Batch service API with Azure AD.</span></span>

<span data-ttu-id="ba6d6-163">Чтобы предоставить приложению доступ к пакетной службе, после [регистрации приложения](#register-your-application-with-an-azure-ad-tenant) выполните следующие действия на портале Azure:</span><span class="sxs-lookup"><span data-stu-id="ba6d6-163">Once you've [registered your application](#register-your-application-with-an-azure-ad-tenant), follow these steps in the Azure portal to grant it access to the Batch service:</span></span>

1. <span data-ttu-id="ba6d6-164">На портале Azure на панели навигации слева выберите **Больше служб**, а затем щелкните **Регистрация приложений**.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-164">In the left-hand navigation pane of the Azure portal, choose **More Services**, click **App Registrations**.</span></span>
2. <span data-ttu-id="ba6d6-165">Найдите имя приложения в списке зарегистрированных приложений:</span><span class="sxs-lookup"><span data-stu-id="ba6d6-165">Search for the name of your application in the list of app registrations:</span></span>

    ![Поиск имени приложения](./media/batch-aad-auth/search-app-registration.png)

3. <span data-ttu-id="ba6d6-167">Откройте колонку **Параметры** приложения.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-167">Open the **Settings** blade for your application.</span></span> <span data-ttu-id="ba6d6-168">В разделе **Доступ через API** выберите **Необходимые разрешения**.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-168">In the **API Access** section, select **Required permissions**.</span></span>
4. <span data-ttu-id="ba6d6-169">В колонке **Необходимые разрешения** нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-169">In the **Required permissions** blade, click the **Add** button.</span></span>
5. <span data-ttu-id="ba6d6-170">На первом шаге выполните поиск API пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-170">In step 1, search for the Batch API.</span></span> <span data-ttu-id="ba6d6-171">Продолжайте поиск для каждой из этих строк, пока не найдете API:</span><span class="sxs-lookup"><span data-stu-id="ba6d6-171">Search for each of these strings until you find the API:</span></span>
    1. <span data-ttu-id="ba6d6-172">**MicrosoftAzureBatch**;</span><span class="sxs-lookup"><span data-stu-id="ba6d6-172">**MicrosoftAzureBatch**.</span></span>
    2. <span data-ttu-id="ba6d6-173">**Microsoft Azure Batch**.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-173">**Microsoft Azure Batch**.</span></span> <span data-ttu-id="ba6d6-174">Более новые клиенты Azure AD могут использовать это имя.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-174">Newer Azure AD tenants may use this name.</span></span>
    3. <span data-ttu-id="ba6d6-175">**ddbf3205-c6bd-46ae-8127-60eb93363864** — это идентификатор API пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-175">**ddbf3205-c6bd-46ae-8127-60eb93363864** is the ID for the Batch API.</span></span> 
6. <span data-ttu-id="ba6d6-176">Когда API-интерфейс пакетной службы будет найден, выберите его и нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-176">Once you find the Batch API, select it and click the **Select** button.</span></span>
6. <span data-ttu-id="ba6d6-177">На шаге 2 установите флажок рядом с параметром **Access Azure Batch Service** (Доступ к пакетной службе Azure) и нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-177">In step 2, select the check box next to **Access Azure Batch Service** and click the **Select** button.</span></span>
7. <span data-ttu-id="ba6d6-178">Нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-178">Click the **Done** button.</span></span>

<span data-ttu-id="ba6d6-179">Теперь в колонке **Необходимые разрешения** показано, что приложение Azure AD имеет доступ к библиотеке ADAL и API пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-179">The **Required Permissions** blade now shows that your Azure AD application has access to both ADAL and the Batch service API.</span></span> <span data-ttu-id="ba6d6-180">Разрешения библиотеке ADAL предоставляются автоматически во время регистрации приложения в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-180">Permissions are granted to ADAL automatically when you first register your app with Azure AD.</span></span>

![Предоставление разрешений API](./media/batch-aad-auth/required-permissions-data-plane.png)

## <a name="use-a-service-principal"></a><span data-ttu-id="ba6d6-182">Использование субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="ba6d6-182">Use a service principal</span></span> 

<span data-ttu-id="ba6d6-183">Чтобы выполнить аутентификацию приложения, которое выполняется автоматически, необходимо использовать субъект-службу.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-183">To authenticate an application that runs unattended, you use a service principal.</span></span> <span data-ttu-id="ba6d6-184">После регистрации приложения выполните приведенные ниже действия на портале Azure, чтобы настроить субъект-службу.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-184">After you've registered your application, follow these steps in the Azure portal to configure a service principal:</span></span>

1. <span data-ttu-id="ba6d6-185">Запросите секретный ключ приложения.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-185">Request a secret key for your application.</span></span>
2. <span data-ttu-id="ba6d6-186">Назначьте приложению роль RBAC.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-186">Assign an RBAC role to your application.</span></span>

### <a name="request-a-secret-key-for-your-application"></a><span data-ttu-id="ba6d6-187">Запрос секретного ключа приложения</span><span class="sxs-lookup"><span data-stu-id="ba6d6-187">Request a secret key for your application</span></span>

<span data-ttu-id="ba6d6-188">При выполнении аутентификации с помощью субъекта-службы приложение отправляет в Azure AD идентификатор приложения и секретный ключ.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-188">When your application authenticates with a service principal, it sends both the application ID and a secret key to Azure AD.</span></span> <span data-ttu-id="ba6d6-189">Вам необходимо создать и скопировать секретный ключ, чтобы использовать его из кода.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-189">You'll need to create and copy the secret key to use from your code.</span></span>

<span data-ttu-id="ba6d6-190">На портале Azure сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="ba6d6-190">Follow these steps in the Azure portal:</span></span>

1. <span data-ttu-id="ba6d6-191">На портале Azure на панели навигации слева выберите **Больше служб**, а затем щелкните **Регистрация приложений**.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-191">In the left-hand navigation pane of the Azure portal, choose **More Services**, click **App Registrations**.</span></span>
2. <span data-ttu-id="ba6d6-192">Найдите имя приложения в списке зарегистрированных приложений.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-192">Search for the name of your application in the list of app registrations.</span></span>
3. <span data-ttu-id="ba6d6-193">Откройте колонку **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-193">Display the **Settings** blade.</span></span> <span data-ttu-id="ba6d6-194">В разделе **Доступ через API** выберите **Ключи**.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-194">In the **API Access** section, select **Keys**.</span></span>
4. <span data-ttu-id="ba6d6-195">Чтобы создать ключ, введите его описание.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-195">To create a key, enter a description for the key.</span></span> <span data-ttu-id="ba6d6-196">Затем выберите срок действия ключа — год или два.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-196">Then select a duration for the key of either one or two years.</span></span> 
5. <span data-ttu-id="ba6d6-197">Нажмите кнопку **Сохранить**, чтобы создать и отобразить ключ.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-197">Click the **Save** button to create and display the key.</span></span> <span data-ttu-id="ba6d6-198">Скопируйте значение ключа в безопасное место, так как у вас больше не будет доступа к нему после закрытия колонки.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-198">Copy the key value to a safe place, as you won't be able to access it again after you leave the blade.</span></span> 

    ![Создание секретного ключа](./media/batch-aad-auth/secret-key.png)

### <a name="assign-an-rbac-role-to-your-application"></a><span data-ttu-id="ba6d6-200">Назначение приложению роли RBAC</span><span class="sxs-lookup"><span data-stu-id="ba6d6-200">Assign an RBAC role to your application</span></span>

<span data-ttu-id="ba6d6-201">Чтобы выполнить аутентификацию с использованием субъекта-службы, вам необходимо назначить приложению роль RBAC.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-201">To authenticate with a service principal, you need to assign an RBAC role to your application.</span></span> <span data-ttu-id="ba6d6-202">Выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-202">Follow these steps:</span></span>

1. <span data-ttu-id="ba6d6-203">На портале Azure перейдите к учетной записи пакетной службы, используемой приложением.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-203">In the Azure portal, navigate to the Batch account used by your application.</span></span>
2. <span data-ttu-id="ba6d6-204">В колонке **Параметры** учетной записи пакетной службы выберите **Управление доступом (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-204">In the **Settings** blade for the Batch account, select **Access Control (IAM)**.</span></span>
3. <span data-ttu-id="ba6d6-205">Нажмите кнопку **Add** (Добавить).</span><span class="sxs-lookup"><span data-stu-id="ba6d6-205">Click the **Add** button.</span></span> 
4. <span data-ttu-id="ba6d6-206">В раскрывающемся списке **Роль** выберите роль приложения — _Участник_ или _Читатель_.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-206">From the **Role** drop-down, choose either the _Contributor_ or _Reader_ role for your application.</span></span> <span data-ttu-id="ba6d6-207">Дополнительные сведения об этих ролях см. в статье [Начало работы с управлением доступом на основе ролей на портале Azure](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="ba6d6-207">For more information on these roles, see [Get started with Role-Based Access Control in the Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>  
5. <span data-ttu-id="ba6d6-208">В поле **Выбрать** введите имя приложения.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-208">In the **Select** field, enter the name of your application.</span></span> <span data-ttu-id="ba6d6-209">Выберите свое приложение в списке, а затем щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-209">Select your application from the list, and click **Save**.</span></span>

<span data-ttu-id="ba6d6-210">После этого приложение с назначенной ролью RBAC должно появиться в параметрах контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-210">Your application should now appear in your access control settings with an RBAC role assigned.</span></span> 

![Назначение приложению роли RBAC](./media/batch-aad-auth/app-rbac-role.png)

### <a name="get-the-tenant-id-for-your-azure-active-directory"></a><span data-ttu-id="ba6d6-212">Получение идентификатора клиента для Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ba6d6-212">Get the tenant ID for your Azure Active Directory</span></span>

<span data-ttu-id="ba6d6-213">Идентификатор клиента определяет клиент Azure AD, который предоставляет службы аутентификации приложению.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-213">The tenant ID identifies the Azure AD tenant that provides authentication services to your application.</span></span> <span data-ttu-id="ba6d6-214">Чтобы получить идентификатор клиента, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="ba6d6-214">To get the tenant ID, follow these steps:</span></span>

1. <span data-ttu-id="ba6d6-215">На портале Azure выберите Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-215">In the Azure portal, select your Active Directory.</span></span>
2. <span data-ttu-id="ba6d6-216">Щелкните **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-216">Click **Properties**.</span></span>
3. <span data-ttu-id="ba6d6-217">Скопируйте значение GUID, указанное для идентификатора каталога.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-217">Copy the GUID value provided for the directory ID.</span></span> <span data-ttu-id="ba6d6-218">Это значение также называется идентификатором клиента.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-218">This value is also called the tenant ID.</span></span>

![Копирование идентификатора каталога](./media/batch-aad-auth/aad-directory-id.png)


## <a name="code-examples"></a><span data-ttu-id="ba6d6-220">Примеры кода</span><span class="sxs-lookup"><span data-stu-id="ba6d6-220">Code examples</span></span>

<span data-ttu-id="ba6d6-221">В примерах кода в этом разделе показано, как выполнить аутентификацию в Azure AD, используя встроенную и субъект-службу.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-221">The code examples in this section show how to authenticate with Azure AD using integrated authentication and with a service principal.</span></span> <span data-ttu-id="ba6d6-222">В этих примерах кода используется .NET, но в целом они актуальны и для других языков.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-222">These code examples use .NET, but the concepts are similar for other languages.</span></span>

> [!NOTE]
> <span data-ttu-id="ba6d6-223">Срок действия маркера проверки подлинности Azure AD истекает через час.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-223">An Azure AD authentication token expires after one hour.</span></span> <span data-ttu-id="ba6d6-224">При использовании долговременного объекта **BatchClient** мы советуем получать маркер из ADAL при каждом запросе, чтобы у вас всегда был допустимый маркер.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-224">When using a long-lived **BatchClient** object, we recommend that you retrieve a token from ADAL on every request to ensure you always have a valid token.</span></span> 
>
>
> <span data-ttu-id="ba6d6-225">Чтобы достичь этого в .NET, напишите метод, который получает маркер из Azure AD, и передайте этот метод в качестве делегата в объект **BatchTokenCredentials**.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-225">To achieve this in .NET, write a method that retrieves the token from Azure AD and pass that method to a **BatchTokenCredentials** object as a delegate.</span></span> <span data-ttu-id="ba6d6-226">Чтобы гарантировать предоставление допустимого маркера, при каждом запросе к пакетной службе вызывается метод делегата.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-226">The delegate method is called on every request to the Batch service to ensure that a valid token is provided.</span></span> <span data-ttu-id="ba6d6-227">По умолчанию ADAL кэширует маркеры, поэтому новый маркер извлекается из Azure AD только при необходимости.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-227">By default ADAL caches tokens, so a new token is retrieved from Azure AD only when necessary.</span></span> <span data-ttu-id="ba6d6-228">Дополнительные сведения о маркерах в Azure AD см. в статье [Сценарии аутентификации в Azure Active Directory][aad_auth_scenarios].</span><span class="sxs-lookup"><span data-stu-id="ba6d6-228">For more information about tokens in Azure AD, see [Authentication Scenarios for Azure AD][aad_auth_scenarios].</span></span>
>
>

### <a name="code-example-using-azure-ad-integrated-authentication-with-batch-net"></a><span data-ttu-id="ba6d6-229">Пример кода. Использование встроенной аутентификации Azure AD с библиотекой .NET для пакетной службы</span><span class="sxs-lookup"><span data-stu-id="ba6d6-229">Code example: Using Azure AD integrated authentication with Batch .NET</span></span>

<span data-ttu-id="ba6d6-230">Чтобы выполнить аутентификацию с использованием встроенной аутентификации из библиотеки .NET для пакетной службы, укажите ссылку на пакет [.NET для пакетной службы Azure](https://www.nuget.org/packages/Azure.Batch/) и пакет [библиотеки ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/).</span><span class="sxs-lookup"><span data-stu-id="ba6d6-230">To authenticate with integrated authentication from Batch .NET, reference the [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) package and the [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) package.</span></span>

<span data-ttu-id="ba6d6-231">Добавьте в код следующие инструкции `using`:</span><span class="sxs-lookup"><span data-stu-id="ba6d6-231">Include the following `using` statements in your code:</span></span>

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="ba6d6-232">Укажите ссылку на конечную точку Azure AD в коде, в том числе идентификатор клиента.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-232">Reference the Azure AD endpoint in your code, including the tenant ID.</span></span> <span data-ttu-id="ba6d6-233">Чтобы получить идентификатор клиента, выполните указания, описанные в разделе [Получение идентификатора клиента для Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="ba6d6-233">To retrieve the tenant ID, follow the steps outlined in [Get the tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

<span data-ttu-id="ba6d6-234">Укажите ссылку на конечную точку ресурса пакетной службы:</span><span class="sxs-lookup"><span data-stu-id="ba6d6-234">Reference the Batch service resource endpoint:</span></span>

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

<span data-ttu-id="ba6d6-235">Укажите ссылку на учетную запись пакетной службы:</span><span class="sxs-lookup"><span data-stu-id="ba6d6-235">Reference your Batch account:</span></span>

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

<span data-ttu-id="ba6d6-236">Укажите идентификатор приложения (идентификатор клиента) для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-236">Specify the application ID (client ID) for your application.</span></span> <span data-ttu-id="ba6d6-237">Идентификатор приложения становится доступен после регистрации приложения на портале Azure:</span><span class="sxs-lookup"><span data-stu-id="ba6d6-237">The application ID is available from your app registration in the Azure portal:</span></span>

```csharp
private const string ClientId = "<application-id>";
```

<span data-ttu-id="ba6d6-238">Скопируйте также URI перенаправления, который вы указали во время процесса регистрации.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-238">Also copy the redirect URI that you specified during the registration process.</span></span> <span data-ttu-id="ba6d6-239">URI перенаправления, указанный в коде, должен соответствовать URI перенаправления, который был указан при регистрации приложения:</span><span class="sxs-lookup"><span data-stu-id="ba6d6-239">The redirect URI specified in your code must match the redirect URI that you provided when you registered the application:</span></span>

```csharp
private const string RedirectUri = "http://mybatchdatasample";
```

<span data-ttu-id="ba6d6-240">Напишите метод обратного вызова, чтобы получить маркер проверки подлинности из Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-240">Write a callback method to acquire the authentication token from Azure AD.</span></span> <span data-ttu-id="ba6d6-241">Приведенный здесь метод обратного вызова **GetAuthenticationTokenAsync** вызывает библиотеку ADAL для аутентификации пользователя, взаимодействующего с приложением.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-241">The **GetAuthenticationTokenAsync** callback method shown here calls ADAL to authenticate a user who is interacting with the application.</span></span> <span data-ttu-id="ba6d6-242">Предоставленный ADAL метод **AcquireTokenAsync** запрашивает учетные данные пользователя. Как только пользователь введет их, приложение продолжит работу (если его учетные данные не кэшированы).</span><span class="sxs-lookup"><span data-stu-id="ba6d6-242">The **AcquireTokenAsync** method provided by ADAL prompts the user for their credentials, and the application proceeds once the user provides them (unless it has already cached credentials):</span></span>

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    var authContext = new AuthenticationContext(AuthorityUri);

    // Acquire the authentication token from Azure AD.
    var authResult = await authContext.AcquireTokenAsync(BatchResourceUri, 
                                                        ClientId, 
                                                        new Uri(RedirectUri), 
                                                        new PlatformParameters(PromptBehavior.Auto));

    return authResult.AccessToken;
}
```

<span data-ttu-id="ba6d6-243">Создайте объект **BatchTokenCredentials**, который принимает делегат в качестве параметра.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-243">Construct a **BatchTokenCredentials** object that takes the delegate as a parameter.</span></span> <span data-ttu-id="ba6d6-244">Используйте эти учетные данные, чтобы открыть объект **BatchClient**.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-244">Use those credentials to open a **BatchClient** object.</span></span> <span data-ttu-id="ba6d6-245">Вы можете использовать объект **BatchClient** для последующих операций в пакетной службе.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-245">You can use that **BatchClient** object for subsequent operations against the Batch service:</span></span>

```csharp
public static async Task PerformBatchOperations()
{
    Func<Task<string>> tokenProvider = () => GetAuthenticationTokenAsync();

    using (var client = await BatchClient.OpenAsync(new BatchTokenCredentials(BatchAccountUrl, tokenProvider)))
    {
        await client.JobOperations.ListJobs().ToListAsync();
    }
}
```

### <a name="code-example-using-an-azure-ad-service-principal-with-batch-net"></a><span data-ttu-id="ba6d6-246">Пример кода. Использование субъекта-службы Azure AD с библиотекой .NET для пакетной службы</span><span class="sxs-lookup"><span data-stu-id="ba6d6-246">Code example: Using an Azure AD service principal with Batch .NET</span></span>

<span data-ttu-id="ba6d6-247">Чтобы выполнить аутентификацию с использованием субъекта-службы из библиотеки .NET для пакетной службы, укажите ссылки на пакет [.NET для пакетной службы Azure](https://www.nuget.org/packages/Azure.Batch/) и пакет [библиотеки ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/).</span><span class="sxs-lookup"><span data-stu-id="ba6d6-247">To authenticate with a service principal from Batch .NET, reference the [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) package and the [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) package.</span></span>

<span data-ttu-id="ba6d6-248">Добавьте в код следующие инструкции `using`:</span><span class="sxs-lookup"><span data-stu-id="ba6d6-248">Include the following `using` statements in your code:</span></span>

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="ba6d6-249">Укажите ссылку на конечную точку Azure AD в коде, в том числе идентификатор клиента.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-249">Reference the Azure AD endpoint in your code, including the tenant ID.</span></span> <span data-ttu-id="ba6d6-250">При использовании субъекта-службы необходимо указать конечную точку определенного клиента.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-250">When using a service principal, you must provide a tenant-specific endpoint.</span></span> <span data-ttu-id="ba6d6-251">Чтобы получить идентификатор клиента, выполните указания, описанные в разделе [Получение идентификатора клиента для Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="ba6d6-251">To retrieve the tenant ID, follow the steps outlined in [Get the tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

<span data-ttu-id="ba6d6-252">Укажите ссылку на конечную точку ресурса пакетной службы:</span><span class="sxs-lookup"><span data-stu-id="ba6d6-252">Reference the Batch service resource endpoint:</span></span>  

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

<span data-ttu-id="ba6d6-253">Укажите ссылку на учетную запись пакетной службы:</span><span class="sxs-lookup"><span data-stu-id="ba6d6-253">Reference your Batch account:</span></span>

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

<span data-ttu-id="ba6d6-254">Укажите идентификатор приложения (идентификатор клиента) для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-254">Specify the application ID (client ID) for your application.</span></span> <span data-ttu-id="ba6d6-255">Идентификатор приложения становится доступен после регистрации приложения на портале Azure:</span><span class="sxs-lookup"><span data-stu-id="ba6d6-255">The application ID is available from your app registration in the Azure portal:</span></span>

```csharp
private const string ClientId = "<application-id>";
```

<span data-ttu-id="ba6d6-256">Укажите секретный ключ, скопированный на портале Azure:</span><span class="sxs-lookup"><span data-stu-id="ba6d6-256">Specify the secret key that you copied from the Azure portal:</span></span>

```csharp
private const string ClientKey = "<secret-key>";
```

<span data-ttu-id="ba6d6-257">Напишите метод обратного вызова, чтобы получить маркер проверки подлинности из Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-257">Write a callback method to acquire the authentication token from Azure AD.</span></span> <span data-ttu-id="ba6d6-258">Приведенный здесь метод обратного вызова **GetAuthenticationTokenAsync** вызывает библиотеку ADAL для автоматической аутентификации:</span><span class="sxs-lookup"><span data-stu-id="ba6d6-258">The **GetAuthenticationTokenAsync** callback method shown here calls ADAL for unattended authentication:</span></span>

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
    AuthenticationResult authResult = await authContext.AcquireTokenAsync(BatchResourceUri, new ClientCredential(ClientId, ClientKey));

    return authResult.AccessToken;
}
```

<span data-ttu-id="ba6d6-259">Создайте объект **BatchTokenCredentials**, который принимает делегат в качестве параметра.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-259">Construct a **BatchTokenCredentials** object that takes the delegate as a parameter.</span></span> <span data-ttu-id="ba6d6-260">Используйте эти учетные данные, чтобы открыть объект **BatchClient**.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-260">Use those credentials to open a **BatchClient** object.</span></span> <span data-ttu-id="ba6d6-261">Затем вы можете использовать объект **BatchClient** для последующих операций в пакетной службе:</span><span class="sxs-lookup"><span data-stu-id="ba6d6-261">You can then use that **BatchClient** object for subsequent operations against the Batch service:</span></span>

```csharp
public static async Task PerformBatchOperations()
{
    Func<Task<string>> tokenProvider = () => GetAuthenticationTokenAsync();

    using (var client = await BatchClient.OpenAsync(new BatchTokenCredentials(BatchAccountUrl, tokenProvider)))
    {
        await client.JobOperations.ListJobs().ToListAsync();
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="ba6d6-262">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ba6d6-262">Next steps</span></span>

<span data-ttu-id="ba6d6-263">Дополнительные сведения о службе Azure AD см. в [документации по Azure Active Directory](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="ba6d6-263">To learn more about Azure AD, see the [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="ba6d6-264">Подробные примеры, показывающие, как использовать ADAL, доступны в библиотеке [примеров кода Azure](https://azure.microsoft.com/resources/samples/?service=active-directory).</span><span class="sxs-lookup"><span data-stu-id="ba6d6-264">In-depth examples showing how to use ADAL are available in the [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=active-directory) library.</span></span>

<span data-ttu-id="ba6d6-265">Дополнительные сведения о субъекте-службе см. в статье [Объекты приложения и субъекта-службы в Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="ba6d6-265">To learn more about service principals, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span> <span data-ttu-id="ba6d6-266">Дополнительные сведения о создании субъекта-службы с помощью портала Azure см. в статье [Создание приложения Azure Active Directory и субъекта-службы с доступом к ресурсам с помощью портала](../resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ba6d6-266">To create a service principal using the Azure portal, see [Use portal to create Active Directory application and service principal that can access resources](../resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="ba6d6-267">Вы также можете создать субъект-службу с помощью PowerShell или Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="ba6d6-267">You can also create a service principal with PowerShell or Azure CLI.</span></span> 

<span data-ttu-id="ba6d6-268">Дополнительные сведения об аутентификации решений по управлению пакетной службой с помощью Azure AD см. в [этой статье](batch-aad-auth-management.md).</span><span class="sxs-lookup"><span data-stu-id="ba6d6-268">To authenticate Batch Management applications using Azure AD, see [Authenticate Batch Management solutions with Active Directory](batch-aad-auth-management.md).</span></span> 

<span data-ttu-id="ba6d6-269">[aad_about]: ../active-directory/active-directory-whatis.md "Что такое Microsoft Azure Active Directory?"</span><span class="sxs-lookup"><span data-stu-id="ba6d6-269">[aad_about]: ../active-directory/active-directory-whatis.md "What is Azure Active Directory?"</span></span>
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
<span data-ttu-id="ba6d6-270">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Сценарии аутентификации в Azure Active Directory"</span><span class="sxs-lookup"><span data-stu-id="ba6d6-270">[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Authentication Scenarios for Azure AD"</span></span>
<span data-ttu-id="ba6d6-271">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Интеграция приложений с Azure Active Directory"</span><span class="sxs-lookup"><span data-stu-id="ba6d6-271">[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrating Applications with Azure Active Directory"</span></span>
[azure_portal]: http://portal.azure.com
