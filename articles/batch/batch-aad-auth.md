---
title: "aaaUse Azure Active Directory tooauthenticate пакетной службы Azure службы решения | Документы Microsoft"
description: "Пакет поддерживает Azure AD для проверки подлинности из hello пакетной службы."
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
ms.openlocfilehash: 6c825c30f1c80bb059a797a2e78367e599acd109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-batch-service-solutions-with-active-directory"></a><span data-ttu-id="346f8-103">Аутентификация решений пакетной службы с помощью Active Directory</span><span class="sxs-lookup"><span data-stu-id="346f8-103">Authenticate Batch service solutions with Active Directory</span></span>

<span data-ttu-id="346f8-104">Пакетная служба Azure поддерживает аутентификацию [Azure Active Directory][aad_about] (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="346f8-104">Azure Batch supports authentication with [Azure Active Directory][aad_about] (Azure AD).</span></span> <span data-ttu-id="346f8-105">Azure AD — многопользовательский облачный каталог и служба управления удостоверениями корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="346f8-105">Azure AD is Microsoft’s multi-tenant cloud based directory and identity management service.</span></span> <span data-ttu-id="346f8-106">Azure сама использует Azure AD tooauthenticate клиентов, Администраторы служб и пользователей организации.</span><span class="sxs-lookup"><span data-stu-id="346f8-106">Azure itself uses Azure AD tooauthenticate its customers, service administrators, and organizational users.</span></span>

<span data-ttu-id="346f8-107">Процесс аутентификации Azure AD в пакетной службе Azure можно выполнить двумя способами:</span><span class="sxs-lookup"><span data-stu-id="346f8-107">When using Azure AD authentication with Azure Batch, you can authenticate in one of two ways:</span></span>

- <span data-ttu-id="346f8-108">С помощью **встроенной проверки подлинности** tooauthenticate пользователя, который взаимодействует с приложением hello.</span><span class="sxs-lookup"><span data-stu-id="346f8-108">By using **integrated authentication** tooauthenticate a user that is interacting with hello application.</span></span> <span data-ttu-id="346f8-109">Приложения с помощью встроенной проверки подлинности собирает учетные данные пользователя и использует эти учетные данные доступа tooauthenticate tooBatch ресурсы.</span><span class="sxs-lookup"><span data-stu-id="346f8-109">An application using integrated authentication gathers a user's credentials and uses those credentials tooauthenticate access tooBatch resources.</span></span>
- <span data-ttu-id="346f8-110">С помощью **участника-службы** tooauthenticate автоматической установки приложения.</span><span class="sxs-lookup"><span data-stu-id="346f8-110">By using a **service principal** tooauthenticate an unattended application.</span></span> <span data-ttu-id="346f8-111">Участника службы определяет политику hello и разрешения для приложения в приложение hello toorepresent заказов, при доступе к ресурсам во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="346f8-111">A service principal defines hello policy and permissions for an application in order toorepresent hello application when accessing resources at runtime.</span></span>

<span data-ttu-id="346f8-112">toolearn Дополнительные сведения о Azure AD см. hello [документация Azure Active Directory](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="346f8-112">toolearn more about Azure AD, see hello [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span>

## <a name="authentication-and-pool-allocation-mode"></a><span data-ttu-id="346f8-113">Режим аутентификации и выделения пула</span><span class="sxs-lookup"><span data-stu-id="346f8-113">Authentication and pool allocation mode</span></span>

<span data-ttu-id="346f8-114">При создании учетной записи пакетной службы вы можете указать, где должны быть выделены пулы, созданные для этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="346f8-114">When you create a Batch account, you can specify where pools created for that account should be allocated.</span></span> <span data-ttu-id="346f8-115">Вы можете tooallocate пулы hello по умолчанию пакетной службы подписки или в подписку пользователя.</span><span class="sxs-lookup"><span data-stu-id="346f8-115">You can choose tooallocate pools either in hello default Batch service subscription or in a user subscription.</span></span> <span data-ttu-id="346f8-116">Выбор влияет на способ проверки подлинности tooresources доступа в такой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="346f8-116">Your choice affects how you authenticate access tooresources in that account.</span></span>

- <span data-ttu-id="346f8-117">**Подписка пакетной службы.**</span><span class="sxs-lookup"><span data-stu-id="346f8-117">**Batch service subscription**.</span></span> <span data-ttu-id="346f8-118">По умолчанию пулы выделяются в подписке пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="346f8-118">By default, Batch pools are allocated in a Batch service subscription.</span></span> <span data-ttu-id="346f8-119">Если этот параметр выбран, можно выполнить проверку подлинности tooresources доступа в такой учетной записи с помощью [Shared Key](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) или с помощью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="346f8-119">If you choose this option, you can authenticate access tooresources in that account either with [Shared Key](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) or with Azure AD.</span></span>
- <span data-ttu-id="346f8-120">**Подписка пользователя.**</span><span class="sxs-lookup"><span data-stu-id="346f8-120">**User subscription.**</span></span> <span data-ttu-id="346f8-121">Вы можете tooallocate пулы пакета в подписки пользователя, указанной вами.</span><span class="sxs-lookup"><span data-stu-id="346f8-121">You can choose tooallocate Batch pools in a user subscription that you specify.</span></span> <span data-ttu-id="346f8-122">Если выбран этот вариант, нужно выполнять проверку подлинности с помощью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="346f8-122">If you choose this option, you must authenticate with Azure AD.</span></span>

## <a name="endpoints-for-authentication"></a><span data-ttu-id="346f8-123">Конечные точки аутентификации</span><span class="sxs-lookup"><span data-stu-id="346f8-123">Endpoints for authentication</span></span>

<span data-ttu-id="346f8-124">tooauthenticate пакета приложений с Azure AD, необходимо tooinclude некоторые хорошо известных конечных точек в коде.</span><span class="sxs-lookup"><span data-stu-id="346f8-124">tooauthenticate Batch applications with Azure AD, you need tooinclude some well-known endpoints in your code.</span></span>

### <a name="azure-ad-endpoint"></a><span data-ttu-id="346f8-125">Конечная точка Azure AD</span><span class="sxs-lookup"><span data-stu-id="346f8-125">Azure AD endpoint</span></span>

<span data-ttu-id="346f8-126">Базовый Hello конечной точки центра Azure AD:</span><span class="sxs-lookup"><span data-stu-id="346f8-126">hello base Azure AD authority endpoint is:</span></span>

`https://login.microsoftonline.com/`

<span data-ttu-id="346f8-127">tooauthenticate с Azure AD, используйте эту конечную точку, вместе с ИД клиента hello (идентификатор каталога).</span><span class="sxs-lookup"><span data-stu-id="346f8-127">tooauthenticate with Azure AD, you use this endpoint together with hello tenant ID (directory ID).</span></span> <span data-ttu-id="346f8-128">Идентификатор клиента Hello определяет hello toouse клиента Azure AD для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="346f8-128">hello tenant ID identifies hello Azure AD tenant toouse for authentication.</span></span> <span data-ttu-id="346f8-129">tooretrieve Здравствуйте ИД клиента, выполните hello действия, описанные в [получить hello ИД клиента для Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="346f8-129">tooretrieve hello tenant ID, follow hello steps outlined in [Get hello tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

`https://login.microsoftonline.com/<tenant-id>`

> [!NOTE] 
> <span data-ttu-id="346f8-130">Hello конечная точка клиента требуется при проверке подлинности с помощью субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="346f8-130">hello tenant-specific endpoint is required when you authenticate using a service principal.</span></span> 
> 
> <span data-ttu-id="346f8-131">Hello клиентская конечная точка является обязательным при проверке подлинности с помощью встроенной проверки подлинности, но рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="346f8-131">hello tenant-specific endpoint is optional when you authenticate using integrated authentication, but recommended.</span></span> <span data-ttu-id="346f8-132">Вы также можете использовать Обычная конечная точка Azure AD hello.</span><span class="sxs-lookup"><span data-stu-id="346f8-132">However, you can also use hello Azure AD common endpoint.</span></span> <span data-ttu-id="346f8-133">Hello Обычная конечная точка представляет собой универсальный учетные данные, сбора интерфейс при конкретного клиента не предоставлен.</span><span class="sxs-lookup"><span data-stu-id="346f8-133">hello common endpoint provides a generic credential gathering interface when a specific tenant is not provided.</span></span> <span data-ttu-id="346f8-134">общую конечную точку Hello `https://login.microsoftonline.com/common`.</span><span class="sxs-lookup"><span data-stu-id="346f8-134">hello common endpoint is `https://login.microsoftonline.com/common`.</span></span>
>
>

<span data-ttu-id="346f8-135">Дополнительные сведения о конечных точках Azure AD см. в статье [Сценарии аутентификации в Azure Active Directory][aad_auth_scenarios].</span><span class="sxs-lookup"><span data-stu-id="346f8-135">For more information about Azure AD endpoints, see [Authentication Scenarios for Azure AD][aad_auth_scenarios].</span></span>

### <a name="batch-resource-endpoint"></a><span data-ttu-id="346f8-136">Конечная точка ресурса пакетной службы</span><span class="sxs-lookup"><span data-stu-id="346f8-136">Batch resource endpoint</span></span>

<span data-ttu-id="346f8-137">Используйте hello **конечной точки ресурсов пакета Azure** toohello пакетная служба запрашивает tooacquire токен для проверки подлинности:</span><span class="sxs-lookup"><span data-stu-id="346f8-137">Use hello **Azure Batch resource endpoint** tooacquire a token for authenticating requests toohello Batch service:</span></span>

`https://batch.core.windows.net/`

## <a name="register-your-application-with-a-tenant"></a><span data-ttu-id="346f8-138">Регистрация приложения в клиенте</span><span class="sxs-lookup"><span data-stu-id="346f8-138">Register your application with a tenant</span></span>

<span data-ttu-id="346f8-139">Hello первый шаг в применении tooauthenticate Azure AD зарегистрировать приложение в клиент Azure AD.</span><span class="sxs-lookup"><span data-stu-id="346f8-139">hello first step in using Azure AD tooauthenticate is registering your application in an Azure AD tenant.</span></span> <span data-ttu-id="346f8-140">Регистрация приложения позволяет toocall hello Azure [библиотеку аутентификации Active Directory] [ aad_adal] (ADAL) в коде.</span><span class="sxs-lookup"><span data-stu-id="346f8-140">Registering your application enables you toocall hello Azure [Active Directory Authentication Library][aad_adal] (ADAL) from your code.</span></span> <span data-ttu-id="346f8-141">Hello ADAL предоставляет API для проверки подлинности в Azure AD из приложения.</span><span class="sxs-lookup"><span data-stu-id="346f8-141">hello ADAL provides an API for authenticating with Azure AD from your application.</span></span> <span data-ttu-id="346f8-142">Регистрация приложения требуется ли планирование встроенной проверки подлинности toouse или субъектом-службой.</span><span class="sxs-lookup"><span data-stu-id="346f8-142">Registering your application is required whether you plan toouse integrated authentication or a service principal.</span></span>

<span data-ttu-id="346f8-143">При регистрации приложения необходимо указать сведения о tooAzure вашего приложения AD.</span><span class="sxs-lookup"><span data-stu-id="346f8-143">When you register your application, you supply information about your application tooAzure AD.</span></span> <span data-ttu-id="346f8-144">Затем Azure AD предоставляет идентификатора приложения используйте tooassociate приложения в Azure AD во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="346f8-144">Azure AD then provides an application ID that you use tooassociate your application with Azure AD at runtime.</span></span> <span data-ttu-id="346f8-145">toolearn Дополнительные сведения о идентификатор приложения hello, в разделе [приложений и объектов участника службы в Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="346f8-145">toolearn more about hello application ID, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span>

<span data-ttu-id="346f8-146">tooregister пакета приложения, повторите шаги hello в hello [Добавление приложения](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) статьи [интеграция приложений с Azure Active Directory][aad_integrate].</span><span class="sxs-lookup"><span data-stu-id="346f8-146">tooregister your Batch application, follow hello steps in hello [Adding an Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span></span> <span data-ttu-id="346f8-147">Если приложение регистрируется как собственное приложение, можно указать любой допустимый URI для hello **URI перенаправления**.</span><span class="sxs-lookup"><span data-stu-id="346f8-147">If you register your application as a Native Application, you can specify any valid URI for hello **Redirect URI**.</span></span> <span data-ttu-id="346f8-148">Не обязательно toobe реальные конечной точки.</span><span class="sxs-lookup"><span data-stu-id="346f8-148">It does not need toobe a real endpoint.</span></span>

<span data-ttu-id="346f8-149">После зарегистрировались приложения, вы увидите, что идентификатор hello приложения:</span><span class="sxs-lookup"><span data-stu-id="346f8-149">After you've registered your application, you'll see hello application ID:</span></span>

![Регистрация приложения пакетной службы в Azure AD](./media/batch-aad-auth/app-registration-data-plane.png)

<span data-ttu-id="346f8-151">Дополнительные сведения о регистрации приложения в Azure AD см. в статье [Сценарии аутентификации в Azure Active Directory](../active-directory/develop/active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="346f8-151">For more information about registering an application with Azure AD, see [Authentication Scenarios for Azure AD](../active-directory/develop/active-directory-authentication-scenarios.md).</span></span>

## <a name="get-hello-tenant-id-for-your-active-directory"></a><span data-ttu-id="346f8-152">Получить идентификатор клиента hello для Active Directory</span><span class="sxs-lookup"><span data-stu-id="346f8-152">Get hello tenant ID for your Active Directory</span></span>

<span data-ttu-id="346f8-153">Идентификатор клиента Hello определяет hello клиента Azure AD, предоставляет приложение tooyour службы проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="346f8-153">hello tenant ID identifies hello Azure AD tenant that provides authentication services tooyour application.</span></span> <span data-ttu-id="346f8-154">tooget Здравствуйте ИД клиента, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="346f8-154">tooget hello tenant ID, follow these steps:</span></span>

1. <span data-ttu-id="346f8-155">В hello портал Azure выберите в Active Directory.</span><span class="sxs-lookup"><span data-stu-id="346f8-155">In hello Azure portal, select your Active Directory.</span></span>
2. <span data-ttu-id="346f8-156">Щелкните **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="346f8-156">Click **Properties**.</span></span>
3. <span data-ttu-id="346f8-157">Скопируйте значение GUID hello, предоставленный для идентификатора hello каталога.</span><span class="sxs-lookup"><span data-stu-id="346f8-157">Copy hello GUID value provided for hello directory ID.</span></span> <span data-ttu-id="346f8-158">Это значение также называется идентификатором hello клиента.</span><span class="sxs-lookup"><span data-stu-id="346f8-158">This value is also called hello tenant ID.</span></span>

![Скопируйте каталог с Идентификатором hello](./media/batch-aad-auth/aad-directory-id.png)


## <a name="use-integrated-authentication"></a><span data-ttu-id="346f8-160">Использование встроенной аутентификации</span><span class="sxs-lookup"><span data-stu-id="346f8-160">Use integrated authentication</span></span>

<span data-ttu-id="346f8-161">tooauthenticate с помощью встроенной проверки подлинности, необходимо toogrant вашей toohello tooconnect разрешения приложения API пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="346f8-161">tooauthenticate with integrated authentication, you need toogrant your application permissions tooconnect toohello Batch service API.</span></span> <span data-ttu-id="346f8-162">Этот шаг включает API приложения tooauthenticate вызовы toohello пакетной службы в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="346f8-162">This step enables your application tooauthenticate calls toohello Batch service API with Azure AD.</span></span>

<span data-ttu-id="346f8-163">После [регистрации приложения](#register-your-application-with-an-azure-ad-tenant), выполните следующие действия в его доступ к toohello пакетная служба Azure портала toogrant hello:</span><span class="sxs-lookup"><span data-stu-id="346f8-163">Once you've [registered your application](#register-your-application-with-an-azure-ad-tenant), follow these steps in hello Azure portal toogrant it access toohello Batch service:</span></span>

1. <span data-ttu-id="346f8-164">В области навигации слева hello hello портал Azure, выберите **более служб**, нажмите кнопку **регистрации приложения**.</span><span class="sxs-lookup"><span data-stu-id="346f8-164">In hello left-hand navigation pane of hello Azure portal, choose **More Services**, click **App Registrations**.</span></span>
2. <span data-ttu-id="346f8-165">Найдите имя приложения в списке hello регистраций приложения hello:</span><span class="sxs-lookup"><span data-stu-id="346f8-165">Search for hello name of your application in hello list of app registrations:</span></span>

    ![Поиск имени приложения](./media/batch-aad-auth/search-app-registration.png)

3. <span data-ttu-id="346f8-167">Откройте hello **параметры** колонку для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="346f8-167">Open hello **Settings** blade for your application.</span></span> <span data-ttu-id="346f8-168">В hello **доступ к API** выберите **требуемые разрешения**.</span><span class="sxs-lookup"><span data-stu-id="346f8-168">In hello **API Access** section, select **Required permissions**.</span></span>
4. <span data-ttu-id="346f8-169">В hello **разрешения, необходимые** колонка, щелкните hello **добавить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="346f8-169">In hello **Required permissions** blade, click hello **Add** button.</span></span>
5. <span data-ttu-id="346f8-170">На первом шаге найдите hello API пакета.</span><span class="sxs-lookup"><span data-stu-id="346f8-170">In step 1, search for hello Batch API.</span></span> <span data-ttu-id="346f8-171">Поиск для каждого из этих строк, пока не найдете hello API:</span><span class="sxs-lookup"><span data-stu-id="346f8-171">Search for each of these strings until you find hello API:</span></span>
    1. <span data-ttu-id="346f8-172">**MicrosoftAzureBatch**;</span><span class="sxs-lookup"><span data-stu-id="346f8-172">**MicrosoftAzureBatch**.</span></span>
    2. <span data-ttu-id="346f8-173">**Microsoft Azure Batch**.</span><span class="sxs-lookup"><span data-stu-id="346f8-173">**Microsoft Azure Batch**.</span></span> <span data-ttu-id="346f8-174">Более новые клиенты Azure AD могут использовать это имя.</span><span class="sxs-lookup"><span data-stu-id="346f8-174">Newer Azure AD tenants may use this name.</span></span>
    3. <span data-ttu-id="346f8-175">**ddbf3205-c6bd-46ae-8127-60eb93363864** идентификатор hello hello API пакета.</span><span class="sxs-lookup"><span data-stu-id="346f8-175">**ddbf3205-c6bd-46ae-8127-60eb93363864** is hello ID for hello Batch API.</span></span> 
6. <span data-ttu-id="346f8-176">Найдя hello API пакета, выберите его и нажмите кнопку hello **выберите** кнопки.</span><span class="sxs-lookup"><span data-stu-id="346f8-176">Once you find hello Batch API, select it and click hello **Select** button.</span></span>
6. <span data-ttu-id="346f8-177">На шаге 2, выберите hello флажок рядом слишком**пакетная служба Azure Access** и нажмите кнопку hello **выберите** кнопки.</span><span class="sxs-lookup"><span data-stu-id="346f8-177">In step 2, select hello check box next too**Access Azure Batch Service** and click hello **Select** button.</span></span>
7. <span data-ttu-id="346f8-178">Нажмите кнопку hello **сделать** кнопки.</span><span class="sxs-lookup"><span data-stu-id="346f8-178">Click hello **Done** button.</span></span>

<span data-ttu-id="346f8-179">Hello **требуемые разрешения** колонке теперь показывают, что у приложения Azure AD, доступ к tooboth ADAL и hello API пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="346f8-179">hello **Required Permissions** blade now shows that your Azure AD application has access tooboth ADAL and hello Batch service API.</span></span> <span data-ttu-id="346f8-180">Разрешения предоставляются tooADAL автоматически при первой регистрации приложения в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="346f8-180">Permissions are granted tooADAL automatically when you first register your app with Azure AD.</span></span>

![Предоставление разрешений API](./media/batch-aad-auth/required-permissions-data-plane.png)

## <a name="use-a-service-principal"></a><span data-ttu-id="346f8-182">Использование субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="346f8-182">Use a service principal</span></span> 

<span data-ttu-id="346f8-183">tooauthenticate приложения, которое выполняется в автоматическом режиме, используйте участника службы.</span><span class="sxs-lookup"><span data-stu-id="346f8-183">tooauthenticate an application that runs unattended, you use a service principal.</span></span> <span data-ttu-id="346f8-184">После зарегистрировались приложения, выполните следующие действия в hello Azure портала tooconfigure участника-службы.</span><span class="sxs-lookup"><span data-stu-id="346f8-184">After you've registered your application, follow these steps in hello Azure portal tooconfigure a service principal:</span></span>

1. <span data-ttu-id="346f8-185">Запросите секретный ключ приложения.</span><span class="sxs-lookup"><span data-stu-id="346f8-185">Request a secret key for your application.</span></span>
2. <span data-ttu-id="346f8-186">Назначение роли tooyour RBAC приложения.</span><span class="sxs-lookup"><span data-stu-id="346f8-186">Assign an RBAC role tooyour application.</span></span>

### <a name="request-a-secret-key-for-your-application"></a><span data-ttu-id="346f8-187">Запрос секретного ключа приложения</span><span class="sxs-lookup"><span data-stu-id="346f8-187">Request a secret key for your application</span></span>

<span data-ttu-id="346f8-188">Когда приложение использует для проверки подлинности субъекта-службы, она отправляет идентификатор приложения hello и секретного ключа tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="346f8-188">When your application authenticates with a service principal, it sends both hello application ID and a secret key tooAzure AD.</span></span> <span data-ttu-id="346f8-189">Вам требуется toocreate и скопируйте hello секретного ключа toouse из кода.</span><span class="sxs-lookup"><span data-stu-id="346f8-189">You'll need toocreate and copy hello secret key toouse from your code.</span></span>

<span data-ttu-id="346f8-190">Выполните следующие действия в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="346f8-190">Follow these steps in hello Azure portal:</span></span>

1. <span data-ttu-id="346f8-191">В области навигации слева hello hello портал Azure, выберите **более служб**, нажмите кнопку **регистрации приложения**.</span><span class="sxs-lookup"><span data-stu-id="346f8-191">In hello left-hand navigation pane of hello Azure portal, choose **More Services**, click **App Registrations**.</span></span>
2. <span data-ttu-id="346f8-192">Найдите имя приложения в списке hello регистраций приложения hello.</span><span class="sxs-lookup"><span data-stu-id="346f8-192">Search for hello name of your application in hello list of app registrations.</span></span>
3. <span data-ttu-id="346f8-193">Экран приветствия **параметры** колонку.</span><span class="sxs-lookup"><span data-stu-id="346f8-193">Display hello **Settings** blade.</span></span> <span data-ttu-id="346f8-194">В hello **доступ к API** выберите **ключей**.</span><span class="sxs-lookup"><span data-stu-id="346f8-194">In hello **API Access** section, select **Keys**.</span></span>
4. <span data-ttu-id="346f8-195">toocreate ключа, введите описание ключа hello.</span><span class="sxs-lookup"><span data-stu-id="346f8-195">toocreate a key, enter a description for hello key.</span></span> <span data-ttu-id="346f8-196">Затем выберите длительность для ключа hello одного или двух лет.</span><span class="sxs-lookup"><span data-stu-id="346f8-196">Then select a duration for hello key of either one or two years.</span></span> 
5. <span data-ttu-id="346f8-197">Нажмите кнопку hello **Сохранить** кнопку toocreate и отобразить ключ hello.</span><span class="sxs-lookup"><span data-stu-id="346f8-197">Click hello **Save** button toocreate and display hello key.</span></span> <span data-ttu-id="346f8-198">Скопируйте hello значение ключа tooa надежном месте, как будет tooaccess может его снова после оставить hello колонку.</span><span class="sxs-lookup"><span data-stu-id="346f8-198">Copy hello key value tooa safe place, as you won't be able tooaccess it again after you leave hello blade.</span></span> 

    ![Создание секретного ключа](./media/batch-aad-auth/secret-key.png)

### <a name="assign-an-rbac-role-tooyour-application"></a><span data-ttu-id="346f8-200">Назначение роли tooyour RBAC приложения</span><span class="sxs-lookup"><span data-stu-id="346f8-200">Assign an RBAC role tooyour application</span></span>

<span data-ttu-id="346f8-201">tooauthenticate с субъектом-службой необходимо tooassign приложения tooyour RBAC роли.</span><span class="sxs-lookup"><span data-stu-id="346f8-201">tooauthenticate with a service principal, you need tooassign an RBAC role tooyour application.</span></span> <span data-ttu-id="346f8-202">Выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="346f8-202">Follow these steps:</span></span>

1. <span data-ttu-id="346f8-203">В hello портал Azure перейдите toohello пакетной учетной записи, используемого приложением.</span><span class="sxs-lookup"><span data-stu-id="346f8-203">In hello Azure portal, navigate toohello Batch account used by your application.</span></span>
2. <span data-ttu-id="346f8-204">В hello **параметры** колонку для hello пакетной учетной записи, выберите **управления доступа (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="346f8-204">In hello **Settings** blade for hello Batch account, select **Access Control (IAM)**.</span></span>
3. <span data-ttu-id="346f8-205">Нажмите кнопку hello **добавить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="346f8-205">Click hello **Add** button.</span></span> 
4. <span data-ttu-id="346f8-206">Из hello **роли** раскрывающийся список, выберите либо hello _участника_ или _чтения_ роли для приложения.</span><span class="sxs-lookup"><span data-stu-id="346f8-206">From hello **Role** drop-down, choose either hello _Contributor_ or _Reader_ role for your application.</span></span> <span data-ttu-id="346f8-207">Дополнительные сведения об этих ролях см. в разделе [приступить к работе с элементом управления доступом на основе ролей в hello портал Azure](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="346f8-207">For more information on these roles, see [Get started with Role-Based Access Control in hello Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>  
5. <span data-ttu-id="346f8-208">В hello **выберите** введите имя приложения hello.</span><span class="sxs-lookup"><span data-stu-id="346f8-208">In hello **Select** field, enter hello name of your application.</span></span> <span data-ttu-id="346f8-209">Выберите приложение из списка hello и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="346f8-209">Select your application from hello list, and click **Save**.</span></span>

<span data-ttu-id="346f8-210">После этого приложение с назначенной ролью RBAC должно появиться в параметрах контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="346f8-210">Your application should now appear in your access control settings with an RBAC role assigned.</span></span> 

![Назначение роли tooyour RBAC приложения](./media/batch-aad-auth/app-rbac-role.png)

### <a name="get-hello-tenant-id-for-your-azure-active-directory"></a><span data-ttu-id="346f8-212">Получить идентификатор клиента hello для Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="346f8-212">Get hello tenant ID for your Azure Active Directory</span></span>

<span data-ttu-id="346f8-213">Идентификатор клиента Hello определяет hello клиента Azure AD, предоставляет приложение tooyour службы проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="346f8-213">hello tenant ID identifies hello Azure AD tenant that provides authentication services tooyour application.</span></span> <span data-ttu-id="346f8-214">tooget Здравствуйте ИД клиента, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="346f8-214">tooget hello tenant ID, follow these steps:</span></span>

1. <span data-ttu-id="346f8-215">В hello портал Azure выберите в Active Directory.</span><span class="sxs-lookup"><span data-stu-id="346f8-215">In hello Azure portal, select your Active Directory.</span></span>
2. <span data-ttu-id="346f8-216">Щелкните **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="346f8-216">Click **Properties**.</span></span>
3. <span data-ttu-id="346f8-217">Скопируйте значение GUID hello, предоставленный для идентификатора hello каталога.</span><span class="sxs-lookup"><span data-stu-id="346f8-217">Copy hello GUID value provided for hello directory ID.</span></span> <span data-ttu-id="346f8-218">Это значение также называется идентификатором hello клиента.</span><span class="sxs-lookup"><span data-stu-id="346f8-218">This value is also called hello tenant ID.</span></span>

![Скопируйте каталог с Идентификатором hello](./media/batch-aad-auth/aad-directory-id.png)


## <a name="code-examples"></a><span data-ttu-id="346f8-220">Примеры кода</span><span class="sxs-lookup"><span data-stu-id="346f8-220">Code examples</span></span>

<span data-ttu-id="346f8-221">Hello в этом разделе примерах кода tooauthenticate с Azure AD с помощью встроенной проверки подлинности, как с субъектом-службой.</span><span class="sxs-lookup"><span data-stu-id="346f8-221">hello code examples in this section show how tooauthenticate with Azure AD using integrated authentication and with a service principal.</span></span> <span data-ttu-id="346f8-222">В этих примерах кода используются .NET, но основные понятия hello аналогичны и для других языков.</span><span class="sxs-lookup"><span data-stu-id="346f8-222">These code examples use .NET, but hello concepts are similar for other languages.</span></span>

> [!NOTE]
> <span data-ttu-id="346f8-223">Срок действия маркера проверки подлинности Azure AD истекает через час.</span><span class="sxs-lookup"><span data-stu-id="346f8-223">An Azure AD authentication token expires after one hour.</span></span> <span data-ttu-id="346f8-224">При использовании долгоживущие **BatchClient** объекта, мы рекомендуем, что можно получить маркер из ADAL на каждый запрос tooensure всегда имеет допустимый токен.</span><span class="sxs-lookup"><span data-stu-id="346f8-224">When using a long-lived **BatchClient** object, we recommend that you retrieve a token from ADAL on every request tooensure you always have a valid token.</span></span> 
>
>
> <span data-ttu-id="346f8-225">tooachieve, в .NET, написать метод, извлекает hello токена из Azure AD и передать этот метод tooa **BatchTokenCredentials** как делегат.</span><span class="sxs-lookup"><span data-stu-id="346f8-225">tooachieve this in .NET, write a method that retrieves hello token from Azure AD and pass that method tooa **BatchTokenCredentials** object as a delegate.</span></span> <span data-ttu-id="346f8-226">Hello делегата метод будет вызван на каждый запрос toohello пакетной службы tooensure, предоставляемого допустимый токен.</span><span class="sxs-lookup"><span data-stu-id="346f8-226">hello delegate method is called on every request toohello Batch service tooensure that a valid token is provided.</span></span> <span data-ttu-id="346f8-227">По умолчанию ADAL кэширует маркеры, поэтому новый маркер извлекается из Azure AD только при необходимости.</span><span class="sxs-lookup"><span data-stu-id="346f8-227">By default ADAL caches tokens, so a new token is retrieved from Azure AD only when necessary.</span></span> <span data-ttu-id="346f8-228">Дополнительные сведения о маркерах в Azure AD см. в статье [Сценарии аутентификации в Azure Active Directory][aad_auth_scenarios].</span><span class="sxs-lookup"><span data-stu-id="346f8-228">For more information about tokens in Azure AD, see [Authentication Scenarios for Azure AD][aad_auth_scenarios].</span></span>
>
>

### <a name="code-example-using-azure-ad-integrated-authentication-with-batch-net"></a><span data-ttu-id="346f8-229">Пример кода. Использование встроенной аутентификации Azure AD с библиотекой .NET для пакетной службы</span><span class="sxs-lookup"><span data-stu-id="346f8-229">Code example: Using Azure AD integrated authentication with Batch .NET</span></span>

<span data-ttu-id="346f8-230">tooauthenticate со встроенной проверкой подлинности из пакета .NET, ссылка hello [пакета Azure .NET](https://www.nuget.org/packages/Azure.Batch/) пакета и hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) пакета.</span><span class="sxs-lookup"><span data-stu-id="346f8-230">tooauthenticate with integrated authentication from Batch .NET, reference hello [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) package and hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) package.</span></span>

<span data-ttu-id="346f8-231">Включить следующие hello `using` инструкций в коде:</span><span class="sxs-lookup"><span data-stu-id="346f8-231">Include hello following `using` statements in your code:</span></span>

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="346f8-232">Ссылка hello Azure AD конечной точки в коде, включая hello клиента идентификатор.</span><span class="sxs-lookup"><span data-stu-id="346f8-232">Reference hello Azure AD endpoint in your code, including hello tenant ID.</span></span> <span data-ttu-id="346f8-233">tooretrieve Здравствуйте ИД клиента, выполните hello действия, описанные в [получить hello ИД клиента для Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="346f8-233">tooretrieve hello tenant ID, follow hello steps outlined in [Get hello tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

<span data-ttu-id="346f8-234">Справочник по hello пакета ресурсов конечной точки службы:</span><span class="sxs-lookup"><span data-stu-id="346f8-234">Reference hello Batch service resource endpoint:</span></span>

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

<span data-ttu-id="346f8-235">Укажите ссылку на учетную запись пакетной службы:</span><span class="sxs-lookup"><span data-stu-id="346f8-235">Reference your Batch account:</span></span>

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

<span data-ttu-id="346f8-236">Укажите идентификатор приложения hello (идентификатор клиента) для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="346f8-236">Specify hello application ID (client ID) for your application.</span></span> <span data-ttu-id="346f8-237">Идентификатор приложения Hello доступен из регистрации вашего приложения в hello портала Azure:</span><span class="sxs-lookup"><span data-stu-id="346f8-237">hello application ID is available from your app registration in hello Azure portal:</span></span>

```csharp
private const string ClientId = "<application-id>";
```

<span data-ttu-id="346f8-238">Кроме того, скопируйте URI, которое определено во время процесса регистрации hello перенаправления hello.</span><span class="sxs-lookup"><span data-stu-id="346f8-238">Also copy hello redirect URI that you specified during hello registration process.</span></span> <span data-ttu-id="346f8-239">Здравствуйте, URI, заданный в коде должен соответствовать hello перенаправления, указанный при регистрации приложения hello URI перенаправления:</span><span class="sxs-lookup"><span data-stu-id="346f8-239">hello redirect URI specified in your code must match hello redirect URI that you provided when you registered hello application:</span></span>

```csharp
private const string RedirectUri = "http://mybatchdatasample";
```

<span data-ttu-id="346f8-240">Запись токена проверки подлинности hello tooacquire метод обратного вызова из Azure AD.</span><span class="sxs-lookup"><span data-stu-id="346f8-240">Write a callback method tooacquire hello authentication token from Azure AD.</span></span> <span data-ttu-id="346f8-241">Hello **GetAuthenticationTokenAsync** метод обратного вызова, показанный здесь вызывает ADAL tooauthenticate пользователь взаимодействует с приложением hello.</span><span class="sxs-lookup"><span data-stu-id="346f8-241">hello **GetAuthenticationTokenAsync** callback method shown here calls ADAL tooauthenticate a user who is interacting with hello application.</span></span> <span data-ttu-id="346f8-242">Hello **AcquireTokenAsync** метод предоставляемых по ADAL приглашения hello свои учетные данные пользователя, после чего приложение hello выполняется один раз hello пользователя предоставляет их (если он уже добавлен в кэш учетных данных):</span><span class="sxs-lookup"><span data-stu-id="346f8-242">hello **AcquireTokenAsync** method provided by ADAL prompts hello user for their credentials, and hello application proceeds once hello user provides them (unless it has already cached credentials):</span></span>

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    var authContext = new AuthenticationContext(AuthorityUri);

    // Acquire hello authentication token from Azure AD.
    var authResult = await authContext.AcquireTokenAsync(BatchResourceUri, 
                                                        ClientId, 
                                                        new Uri(RedirectUri), 
                                                        new PlatformParameters(PromptBehavior.Auto));

    return authResult.AccessToken;
}
```

<span data-ttu-id="346f8-243">Создать **BatchTokenCredentials** объекта, который принимает делегат в качестве параметра hello.</span><span class="sxs-lookup"><span data-stu-id="346f8-243">Construct a **BatchTokenCredentials** object that takes hello delegate as a parameter.</span></span> <span data-ttu-id="346f8-244">Использовать эти учетные данные tooopen **BatchClient** объекта.</span><span class="sxs-lookup"><span data-stu-id="346f8-244">Use those credentials tooopen a **BatchClient** object.</span></span> <span data-ttu-id="346f8-245">Можно использовать этот **BatchClient** объекта для последующих операций, выполняемых hello пакетной службы:</span><span class="sxs-lookup"><span data-stu-id="346f8-245">You can use that **BatchClient** object for subsequent operations against hello Batch service:</span></span>

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

### <a name="code-example-using-an-azure-ad-service-principal-with-batch-net"></a><span data-ttu-id="346f8-246">Пример кода. Использование субъекта-службы Azure AD с библиотекой .NET для пакетной службы</span><span class="sxs-lookup"><span data-stu-id="346f8-246">Code example: Using an Azure AD service principal with Batch .NET</span></span>

<span data-ttu-id="346f8-247">tooauthenticate с субъектом-службой из пакета .NET, ссылка hello [пакета Azure .NET](https://www.nuget.org/packages/Azure.Batch/) пакета и hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) пакета.</span><span class="sxs-lookup"><span data-stu-id="346f8-247">tooauthenticate with a service principal from Batch .NET, reference hello [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) package and hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) package.</span></span>

<span data-ttu-id="346f8-248">Включить следующие hello `using` инструкций в коде:</span><span class="sxs-lookup"><span data-stu-id="346f8-248">Include hello following `using` statements in your code:</span></span>

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="346f8-249">Ссылка hello Azure AD конечной точки в коде, включая hello клиента идентификатор.</span><span class="sxs-lookup"><span data-stu-id="346f8-249">Reference hello Azure AD endpoint in your code, including hello tenant ID.</span></span> <span data-ttu-id="346f8-250">При использовании субъекта-службы необходимо указать конечную точку определенного клиента.</span><span class="sxs-lookup"><span data-stu-id="346f8-250">When using a service principal, you must provide a tenant-specific endpoint.</span></span> <span data-ttu-id="346f8-251">tooretrieve Здравствуйте ИД клиента, выполните hello действия, описанные в [получить hello ИД клиента для Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span><span class="sxs-lookup"><span data-stu-id="346f8-251">tooretrieve hello tenant ID, follow hello steps outlined in [Get hello tenant ID for your Azure Active Directory](#get-the-tenant-id-for-your-active-directory):</span></span>

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

<span data-ttu-id="346f8-252">Справочник по hello пакета ресурсов конечной точки службы:</span><span class="sxs-lookup"><span data-stu-id="346f8-252">Reference hello Batch service resource endpoint:</span></span>  

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

<span data-ttu-id="346f8-253">Укажите ссылку на учетную запись пакетной службы:</span><span class="sxs-lookup"><span data-stu-id="346f8-253">Reference your Batch account:</span></span>

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

<span data-ttu-id="346f8-254">Укажите идентификатор приложения hello (идентификатор клиента) для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="346f8-254">Specify hello application ID (client ID) for your application.</span></span> <span data-ttu-id="346f8-255">Идентификатор приложения Hello доступен из регистрации вашего приложения в hello портала Azure:</span><span class="sxs-lookup"><span data-stu-id="346f8-255">hello application ID is available from your app registration in hello Azure portal:</span></span>

```csharp
private const string ClientId = "<application-id>";
```

<span data-ttu-id="346f8-256">Укажите hello секретного ключа, скопированный из hello портала Azure:</span><span class="sxs-lookup"><span data-stu-id="346f8-256">Specify hello secret key that you copied from hello Azure portal:</span></span>

```csharp
private const string ClientKey = "<secret-key>";
```

<span data-ttu-id="346f8-257">Запись токена проверки подлинности hello tooacquire метод обратного вызова из Azure AD.</span><span class="sxs-lookup"><span data-stu-id="346f8-257">Write a callback method tooacquire hello authentication token from Azure AD.</span></span> <span data-ttu-id="346f8-258">Hello **GetAuthenticationTokenAsync** метод обратного вызова, здесь показаны вызовы ADAL для автоматической проверки подлинности:</span><span class="sxs-lookup"><span data-stu-id="346f8-258">hello **GetAuthenticationTokenAsync** callback method shown here calls ADAL for unattended authentication:</span></span>

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
    AuthenticationResult authResult = await authContext.AcquireTokenAsync(BatchResourceUri, new ClientCredential(ClientId, ClientKey));

    return authResult.AccessToken;
}
```

<span data-ttu-id="346f8-259">Создать **BatchTokenCredentials** объекта, который принимает делегат в качестве параметра hello.</span><span class="sxs-lookup"><span data-stu-id="346f8-259">Construct a **BatchTokenCredentials** object that takes hello delegate as a parameter.</span></span> <span data-ttu-id="346f8-260">Использовать эти учетные данные tooopen **BatchClient** объекта.</span><span class="sxs-lookup"><span data-stu-id="346f8-260">Use those credentials tooopen a **BatchClient** object.</span></span> <span data-ttu-id="346f8-261">Затем можно использовать, **BatchClient** объекта для последующих операций, выполняемых hello пакетной службы:</span><span class="sxs-lookup"><span data-stu-id="346f8-261">You can then use that **BatchClient** object for subsequent operations against hello Batch service:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="346f8-262">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="346f8-262">Next steps</span></span>

<span data-ttu-id="346f8-263">toolearn Дополнительные сведения о Azure AD см. hello [документация Azure Active Directory](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="346f8-263">toolearn more about Azure AD, see hello [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="346f8-264">Подробные примеры, показывающие, как toouse ADAL доступны в hello [образцы кода Azure](https://azure.microsoft.com/resources/samples/?service=active-directory) библиотеки.</span><span class="sxs-lookup"><span data-stu-id="346f8-264">In-depth examples showing how toouse ADAL are available in hello [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=active-directory) library.</span></span>

<span data-ttu-id="346f8-265">toolearn Дополнительные сведения о субъектах, в разделе [приложений и объектов участника службы в Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="346f8-265">toolearn more about service principals, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span> <span data-ttu-id="346f8-266">toocreate участника службы с помощью hello Azure портала, см. в разделе [использовать приложение портала toocreate Active Directory и участника-службы, могут обращаться к ресурсам](../resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="346f8-266">toocreate a service principal using hello Azure portal, see [Use portal toocreate Active Directory application and service principal that can access resources](../resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="346f8-267">Вы также можете создать субъект-службу с помощью PowerShell или Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="346f8-267">You can also create a service principal with PowerShell or Azure CLI.</span></span> 

<span data-ttu-id="346f8-268">приложения tooauthenticate пакета управления, с помощью Azure AD см. [решения для проверки подлинности пакета управления с помощью Active Directory](batch-aad-auth-management.md).</span><span class="sxs-lookup"><span data-stu-id="346f8-268">tooauthenticate Batch Management applications using Azure AD, see [Authenticate Batch Management solutions with Active Directory](batch-aad-auth-management.md).</span></span> 

[aad_about]: ../active-directory/active-directory-whatis.md "Что такое Microsoft Azure Active Directory?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Сценарии аутентификации в Azure Active Directory"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Интеграция приложений с Azure Active Directory"
[azure_portal]: http://portal.azure.com
