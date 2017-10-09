---
title: "Аутентификация пользователей в Data Lake Store с помощью Azure Active Directory | Документация Майкрософт"
description: "Узнайте, как проверка подлинности для конечных пользователей tooachieve с хранилища Озера данных с помощью Azure Active Directory"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ec586ecd-1b42-459e-b600-fadbb7b80a9b
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: fd58f4f2d8fc915b8bc51d9e5b040d2cee34047e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="end-user-authentication-with-data-lake-store-using-azure-active-directory"></a><span data-ttu-id="a97cb-103">Аутентификация пользователей в Data Lake Store с помощью Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a97cb-103">End-user authentication with Data Lake Store using Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a97cb-104">Аутентификация между службами</span><span class="sxs-lookup"><span data-stu-id="a97cb-104">Service-to-service authentication</span></span>](data-lake-store-authenticate-using-active-directory.md)
> * [<span data-ttu-id="a97cb-105">Аутентификация пользователей</span><span class="sxs-lookup"><span data-stu-id="a97cb-105">End-user authentication</span></span>](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

<span data-ttu-id="a97cb-106">Azure Data Lake Store использует Azure Active Directory для аутентификации.</span><span class="sxs-lookup"><span data-stu-id="a97cb-106">Azure Data Lake Store uses Azure Active Directory for authentication.</span></span> <span data-ttu-id="a97cb-107">До создания приложения, которое работает с хранилища Озера данных Azure и аналитики Озера данных Azure, сначала необходимо решить, как tooauthenticate приложения с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a97cb-107">Before authoring an application that works with Azure Data Lake Store or Azure Data Lake Analytics, you must first decide how you would like tooauthenticate your application with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="a97cb-108">Hello основные возможные варианты:</span><span class="sxs-lookup"><span data-stu-id="a97cb-108">hello two main options available are:</span></span>

* <span data-ttu-id="a97cb-109">Аутентификация пользователей (в этой статье)</span><span class="sxs-lookup"><span data-stu-id="a97cb-109">End-user authentication (this article)</span></span>
* <span data-ttu-id="a97cb-110">Взаимодействие между службами</span><span class="sxs-lookup"><span data-stu-id="a97cb-110">Service-to-service authentication</span></span>

<span data-ttu-id="a97cb-111">Оба этих параметра привести приложение, предоставляемой с токеном OAuth 2.0, который получает tooeach вложенного запроса, выполняемого tooAzure хранилища Озера данных или аналитики Озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="a97cb-111">Both these options result in your application being provided with an OAuth 2.0 token, which gets attached tooeach request made tooAzure Data Lake Store or Azure Data Lake Analytics.</span></span>

<span data-ttu-id="a97cb-112">Из этой статьи вы узнаете, как создать **собственное приложение Azure AD для аутентификации пользователей**.</span><span class="sxs-lookup"><span data-stu-id="a97cb-112">This article talks about how create an **Azure AD native application for end-user authentication**.</span></span> <span data-ttu-id="a97cb-113">Инструкции по настройке приложения Azure AD для аутентификации между службами см. в статье [Аутентификация между службами в Data Lake Store с помощью Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="a97cb-113">For instructions on Azure AD application configuration for service-to-service authentication see [Service-to-service authentication with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a97cb-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a97cb-114">Prerequisites</span></span>
* <span data-ttu-id="a97cb-115">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="a97cb-115">An Azure subscription.</span></span> <span data-ttu-id="a97cb-116">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a97cb-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="a97cb-117">Идентификатор подписки.</span><span class="sxs-lookup"><span data-stu-id="a97cb-117">Your subscription ID.</span></span> <span data-ttu-id="a97cb-118">Его можно получить из hello портала Azure.</span><span class="sxs-lookup"><span data-stu-id="a97cb-118">You can retrieve it from hello Azure Portal.</span></span> <span data-ttu-id="a97cb-119">Например он доступен из колонки учетной записи хранилища Озера данных hello.</span><span class="sxs-lookup"><span data-stu-id="a97cb-119">For example, it is available from hello Data Lake Store account blade.</span></span>
  
    ![Получение идентификатора подписки](./media/data-lake-store-end-user-authenticate-using-active-directory/get-subscription-id.png)

* <span data-ttu-id="a97cb-121">Доменное имя Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a97cb-121">Your Azure AD domain name.</span></span> <span data-ttu-id="a97cb-122">Его можно получить путем наведения указателя мыши hello в правом верхнем углу hello hello портала Azure.</span><span class="sxs-lookup"><span data-stu-id="a97cb-122">You can retrieve it by hovering hello mouse in hello top-right corner of hello Azure Portal.</span></span> <span data-ttu-id="a97cb-123">Из hello снимке hello доменное имя — **contoso.onmicrosoft.com**, и hello GUID внутри скобок является идентификатором hello клиента.</span><span class="sxs-lookup"><span data-stu-id="a97cb-123">From hello screenshot below, hello domain name is **contoso.onmicrosoft.com**, and hello GUID within brackets is hello tenant ID.</span></span> 
  
    ![Получение домена AAD](./media/data-lake-store-end-user-authenticate-using-active-directory/get-aad-domain.png)

## <a name="end-user-authentication"></a><span data-ttu-id="a97cb-125">Аутентификация пользователей</span><span class="sxs-lookup"><span data-stu-id="a97cb-125">End-user authentication</span></span>
<span data-ttu-id="a97cb-126">Это рекомендованный подход, если требуется, чтобы toolog конечным пользователем в приложении tooyour через Azure AD hello.</span><span class="sxs-lookup"><span data-stu-id="a97cb-126">This is hello recommended approach if you want an end-user toolog in tooyour application via Azure AD.</span></span> <span data-ttu-id="a97cb-127">Приложение будет подвергаться может tooaccess ресурсы Azure с hello таким же уровнем доступа как hello конечного пользователя, который вход.</span><span class="sxs-lookup"><span data-stu-id="a97cb-127">Your application will be able tooaccess Azure resources with hello same level of access as hello end-user that logged in.</span></span> <span data-ttu-id="a97cb-128">Конечному пользователю потребуется tooprovide свои учетные данные периодически toomaintain приложению доступ.</span><span class="sxs-lookup"><span data-stu-id="a97cb-128">Your end-user will need tooprovide their credentials periodically in order for your application toomaintain access.</span></span>

<span data-ttu-id="a97cb-129">Hello с конечным пользователем hello вход образом, приложение получает токен доступа и токена обновления.</span><span class="sxs-lookup"><span data-stu-id="a97cb-129">hello result of having hello end-user log in is that your application is given an access token and a refresh token.</span></span> <span data-ttu-id="a97cb-130">маркер доступа Hello получает запрос tooeach вложенное хранилище Озера tooData или аналитики Озера данных и действителен в течение одного часа, по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a97cb-130">hello access token gets attached tooeach request made tooData Lake Store or Data Lake Analytics, and it is valid for one hour by default.</span></span> <span data-ttu-id="a97cb-131">токен обновления Hello может быть используется tooobtain новый маркер доступа, который действителен для копии недель tootwo по умолчанию, если используется регулярно.</span><span class="sxs-lookup"><span data-stu-id="a97cb-131">hello refresh token can be used tooobtain a new access token, and it is valid for up tootwo weeks by default, if used regularly.</span></span> <span data-ttu-id="a97cb-132">Для входа пользователей можно использовать два разных подхода.</span><span class="sxs-lookup"><span data-stu-id="a97cb-132">You can use two different approaches for end-user log in.</span></span>

### <a name="using-hello-oauth-20-pop-up"></a><span data-ttu-id="a97cb-133">С помощью всплывающего окна hello OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="a97cb-133">Using hello OAuth 2.0 pop-up</span></span>
<span data-ttu-id="a97cb-134">Приложение может вызывать всплывающих авторизации OAuth 2.0, в которых hello для конечных пользователей можно вводить свои учетные данные.</span><span class="sxs-lookup"><span data-stu-id="a97cb-134">Your application can trigger an OAuth 2.0 authorization pop-up, in which hello end-user can enter their credentials.</span></span> <span data-ttu-id="a97cb-135">Это всплывающее окно также работает с процессом hello Azure AD, двухфакторной проверки подлинности (2FA), при необходимости.</span><span class="sxs-lookup"><span data-stu-id="a97cb-135">This pop-up also works with hello Azure AD Two-factor Authentication (2FA) process, if required.</span></span> 

> [!NOTE]
> <span data-ttu-id="a97cb-136">Этот метод не еще поддерживается в hello библиотеки проверки подлинности Azure AD (ADAL) для Python или Java.</span><span class="sxs-lookup"><span data-stu-id="a97cb-136">This method is not yet supported in hello Azure AD Authentication Library (ADAL) for Python or Java.</span></span>
> 
> 

### <a name="directly-passing-in-user-credentials"></a><span data-ttu-id="a97cb-137">Непосредственная передача учетных данных пользователя</span><span class="sxs-lookup"><span data-stu-id="a97cb-137">Directly passing in user credentials</span></span>
<span data-ttu-id="a97cb-138">Приложение может предоставлять непосредственно tooAzure учетные данные пользователя AD.</span><span class="sxs-lookup"><span data-stu-id="a97cb-138">Your application can directly provide user credentials tooAzure AD.</span></span> <span data-ttu-id="a97cb-139">Этот метод работает только для учетных записей на основе идентификаторов организации. Он не подходит для личных учетных записей пользователей или учетных записей на основе Live ID, включая те, которые заканчиваются на @outlook.com или @live.com. Кроме того, данный метод несовместим с учетными записями пользователей, для которых требуется двухфакторная проверка подлинности (2FA) Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a97cb-139">This method only works with organizational ID user accounts; it is not compatible with personal / “live ID” user accounts, including those ending in @outlook.com or @live.com. Furthermore, this method is not compatible with user accounts that require Azure AD Two-factor Authentication (2FA).</span></span>

### <a name="what-do-i-need-toouse-this-approach"></a><span data-ttu-id="a97cb-140">Что делать мне toouse этот подход?</span><span class="sxs-lookup"><span data-stu-id="a97cb-140">What do I need toouse this approach?</span></span>
* <span data-ttu-id="a97cb-141">Доменное имя Azure AD</span><span class="sxs-lookup"><span data-stu-id="a97cb-141">Azure AD domain name.</span></span> <span data-ttu-id="a97cb-142">Уже есть в необходимом компоненте hello данной статьи.</span><span class="sxs-lookup"><span data-stu-id="a97cb-142">This is already listed in hello prerequisite of this article.</span></span>
* <span data-ttu-id="a97cb-143">**Собственное приложение** Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a97cb-143">Azure AD **native application**</span></span>
* <span data-ttu-id="a97cb-144">Идентификатор приложения для собственного приложения hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a97cb-144">Application ID for hello Azure AD native application</span></span>
* <span data-ttu-id="a97cb-145">URI перенаправления для hello собственное приложение Azure AD</span><span class="sxs-lookup"><span data-stu-id="a97cb-145">Redirect URI for hello Azure AD native application</span></span>
* <span data-ttu-id="a97cb-146">Настроенные делегированные разрешения.</span><span class="sxs-lookup"><span data-stu-id="a97cb-146">Set delegated permissions</span></span>


## <a name="step-1-create-an-active-directory-native-application"></a><span data-ttu-id="a97cb-147">Шаг 1. Создание собственного приложения Active Directory</span><span class="sxs-lookup"><span data-stu-id="a97cb-147">Step 1: Create an Active Directory native application</span></span>

<span data-ttu-id="a97cb-148">Создайте и настройте собственное приложение Azure AD для аутентификации пользователей в Azure Data Lake Store с помощью Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a97cb-148">Create and configure an Azure AD native application for end-user authentication with Azure Data Lake Store using Azure Active Directory.</span></span> <span data-ttu-id="a97cb-149">Инструкции см. в разделе [Создание приложения Azure AD](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a97cb-149">For instructions, see [Create an Azure AD application](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>

<span data-ttu-id="a97cb-150">Придерживаясь инструкциям hello в hello выше ссылку, обязательно выберите **собственного** для типа приложения, как показано на следующем снимке экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="a97cb-150">While following hello instructions at hello above link, make sure you select **Native** for application type, as shown in hello screenshot below.</span></span>

<span data-ttu-id="a97cb-151">![Создание веб-приложения](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "Создание собственного приложения")</span><span class="sxs-lookup"><span data-stu-id="a97cb-151">![Create web app](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "Create native app")</span></span>

## <a name="step-2-get-application-id-and-redirect-uri"></a><span data-ttu-id="a97cb-152">Шаг 2. Получение идентификатора приложения и URI перенаправления</span><span class="sxs-lookup"><span data-stu-id="a97cb-152">Step 2: Get application id and redirect URI</span></span>

<span data-ttu-id="a97cb-153">В разделе [получить идентификатор приложения hello](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) tooretrieve hello идентификатор приложения (также называется hello идентификатор клиента в hello классический портал Azure) собственного приложения hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a97cb-153">See [Get hello application ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) tooretrieve hello application id (also called hello client ID in hello Azure classic portal) of hello Azure AD native application.</span></span>

<span data-ttu-id="a97cb-154">tooretrieve hello URI перенаправления, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="a97cb-154">tooretrieve hello redirect URI, follow hello steps below.</span></span>

1. <span data-ttu-id="a97cb-155">Hello портал Azure, выберите **Azure Active Directory**, нажмите кнопку **регистрации приложения**, затем найдите и выберите только что созданный собственное приложение hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a97cb-155">From hello Azure Portal, select **Azure Active Directory**, click **App registrations**, and then find and click hello Azure AD native application that you just created.</span></span>

2. <span data-ttu-id="a97cb-156">Из hello **параметры** щелкните колонку для приложения hello **URI перенаправления**.</span><span class="sxs-lookup"><span data-stu-id="a97cb-156">From hello **Settings** blade for hello application, click **Redirect URIs**.</span></span>

    ![Получение URI перенаправления](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-redirect-uri.png)

3. <span data-ttu-id="a97cb-158">Скопируйте отображаемое значение hello.</span><span class="sxs-lookup"><span data-stu-id="a97cb-158">Copy hello value displayed.</span></span>


## <a name="step-3-set-permissions"></a><span data-ttu-id="a97cb-159">Шаг 3. Установка разрешений</span><span class="sxs-lookup"><span data-stu-id="a97cb-159">Step 3: Set permissions</span></span>

1. <span data-ttu-id="a97cb-160">Hello портал Azure, выберите **Azure Active Directory**, нажмите кнопку **регистрации приложения**, затем найдите и выберите только что созданный собственное приложение hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a97cb-160">From hello Azure Portal, select **Azure Active Directory**, click **App registrations**, and then find and click hello Azure AD native application that you just created.</span></span>

2. <span data-ttu-id="a97cb-161">Из hello **параметры** щелкните колонку для приложения hello **разрешения, необходимые**и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="a97cb-161">From hello **Settings** blade for hello application, click **Required permissions**, and then click **Add**.</span></span>

    ![Идентификатор клиента](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-1.png)

3. <span data-ttu-id="a97cb-163">В hello **Добавление доступа к API** колонке нажмите кнопку **выберите API**, нажмите кнопку **Озера данных Azure**, а затем нажмите кнопку **выберите**.</span><span class="sxs-lookup"><span data-stu-id="a97cb-163">In hello **Add API Access** blade, click **Select an API**, click **Azure Data Lake**, and then click **Select**.</span></span>

    ![Идентификатор клиента](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-2.png)
 
4.  <span data-ttu-id="a97cb-165">В hello **Добавление доступа к API** колонке нажмите кнопку **разрешений Select**, выберите hello флажок toogive **полного доступа к хранилищу Озера tooData**и нажмите кнопку **выберите** .</span><span class="sxs-lookup"><span data-stu-id="a97cb-165">In hello **Add API Access** blade, click **Select permissions**, select hello check box toogive **Full access tooData Lake Store**, and then click **Select**.</span></span>

    ![Идентификатор клиента](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-3.png)

    <span data-ttu-id="a97cb-167">Нажмите кнопку **Done**(Готово).</span><span class="sxs-lookup"><span data-stu-id="a97cb-167">Click **Done**.</span></span>

5. <span data-ttu-id="a97cb-168">Повторите hello последние два шага toogrant разрешения для **API управления службами Windows Azure** также.</span><span class="sxs-lookup"><span data-stu-id="a97cb-168">Repeat hello last two steps toogrant permissions for **Windows Azure Service Management API** as well.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="a97cb-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a97cb-169">Next steps</span></span>
<span data-ttu-id="a97cb-170">В этой статье создания собственного приложения Azure AD и собрать информацию о hello в клиентские приложения, создаваемые с помощью пакета SDK для .NET, Java SDK, REST API, и т. д. Теперь можно перейти toohello следующие статьи, в которых расскажем, как проверка подлинности приложения web toofirst для toouse hello Azure AD с хранилища Озера данных и затем выполнить другие операции в хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="a97cb-170">In this article you created an Azure AD native application and gathered hello information you need in your client applications that you author using .NET SDK, Java SDK, REST API, etc. You can now proceed toohello following articles that talk about how toouse hello Azure AD web application toofirst authenticate with Data Lake Store and then perform other operations on hello store.</span></span>

* [<span data-ttu-id="a97cb-171">Начало работы с хранилищем озера данных Azure с помощью пакета SDK .NET</span><span class="sxs-lookup"><span data-stu-id="a97cb-171">Get started with Azure Data Lake Store using .NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
* [<span data-ttu-id="a97cb-172">Начало работы с хранилищем озера данных Azure с помощью пакета SDK .NET</span><span class="sxs-lookup"><span data-stu-id="a97cb-172">Get started with Azure Data Lake Store using Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
* [<span data-ttu-id="a97cb-173">Начало работы с Azure Data Lake Store с помощью REST API</span><span class="sxs-lookup"><span data-stu-id="a97cb-173">Get started with Azure Data Lake Store using REST API</span></span>](data-lake-store-get-started-rest-api.md)

