---
title: "Аутентификация пользователей в Data Lake Store с помощью Azure Active Directory | Документация Майкрософт"
description: "Узнайте, как реализовать аутентификацию пользователей в Data Lake Store с помощью Azure Active Directory."
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
ms.openlocfilehash: c20f5c39b00992d801909c8e5de292f3c2f12673
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="end-user-authentication-with-data-lake-store-using-azure-active-directory"></a><span data-ttu-id="dc75a-103">Аутентификация пользователей в Data Lake Store с помощью Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dc75a-103">End-user authentication with Data Lake Store using Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="dc75a-104">Аутентификация между службами</span><span class="sxs-lookup"><span data-stu-id="dc75a-104">Service-to-service authentication</span></span>](data-lake-store-authenticate-using-active-directory.md)
> * [<span data-ttu-id="dc75a-105">Аутентификация пользователей</span><span class="sxs-lookup"><span data-stu-id="dc75a-105">End-user authentication</span></span>](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

<span data-ttu-id="dc75a-106">Azure Data Lake Store использует Azure Active Directory для аутентификации.</span><span class="sxs-lookup"><span data-stu-id="dc75a-106">Azure Data Lake Store uses Azure Active Directory for authentication.</span></span> <span data-ttu-id="dc75a-107">Прежде чем создать приложение, которое работает с Azure Data Lake Store или Azure Data Lake Analytics, необходимо решить, как его следует аутентифицировать посредством Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dc75a-107">Before authoring an application that works with Azure Data Lake Store or Azure Data Lake Analytics, you must first decide how you would like to authenticate your application with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="dc75a-108">Доступно два основных варианта:</span><span class="sxs-lookup"><span data-stu-id="dc75a-108">The two main options available are:</span></span>

* <span data-ttu-id="dc75a-109">Аутентификация пользователей (в этой статье)</span><span class="sxs-lookup"><span data-stu-id="dc75a-109">End-user authentication (this article)</span></span>
* <span data-ttu-id="dc75a-110">Взаимодействие между службами</span><span class="sxs-lookup"><span data-stu-id="dc75a-110">Service-to-service authentication</span></span>

<span data-ttu-id="dc75a-111">Оба этих варианта позволят приложению получить маркер OAuth 2.0, который вкладывается в каждый запрос к Azure Data Lake Store или Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="dc75a-111">Both these options result in your application being provided with an OAuth 2.0 token, which gets attached to each request made to Azure Data Lake Store or Azure Data Lake Analytics.</span></span>

<span data-ttu-id="dc75a-112">Из этой статьи вы узнаете, как создать **собственное приложение Azure AD для аутентификации пользователей**.</span><span class="sxs-lookup"><span data-stu-id="dc75a-112">This article talks about how create an **Azure AD native application for end-user authentication**.</span></span> <span data-ttu-id="dc75a-113">Инструкции по настройке приложения Azure AD для аутентификации между службами см. в статье [Аутентификация между службами в Data Lake Store с помощью Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="dc75a-113">For instructions on Azure AD application configuration for service-to-service authentication see [Service-to-service authentication with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dc75a-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="dc75a-114">Prerequisites</span></span>
* <span data-ttu-id="dc75a-115">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="dc75a-115">An Azure subscription.</span></span> <span data-ttu-id="dc75a-116">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dc75a-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="dc75a-117">Идентификатор подписки.</span><span class="sxs-lookup"><span data-stu-id="dc75a-117">Your subscription ID.</span></span> <span data-ttu-id="dc75a-118">Его можно получить на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="dc75a-118">You can retrieve it from the Azure Portal.</span></span> <span data-ttu-id="dc75a-119">Например, он доступен в колонке учетной записи Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="dc75a-119">For example, it is available from the Data Lake Store account blade.</span></span>
  
    ![Получение идентификатора подписки](./media/data-lake-store-end-user-authenticate-using-active-directory/get-subscription-id.png)

* <span data-ttu-id="dc75a-121">Доменное имя Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc75a-121">Your Azure AD domain name.</span></span> <span data-ttu-id="dc75a-122">Его можно получить, наведя указатель мыши на правый верхний угол страницы портала Azure.</span><span class="sxs-lookup"><span data-stu-id="dc75a-122">You can retrieve it by hovering the mouse in the top-right corner of the Azure Portal.</span></span> <span data-ttu-id="dc75a-123">На приведенном ниже снимке экрана указано имя домена **contoso.onmicrosoft.com**, а идентификатор GUID в скобках — это идентификатор клиента.</span><span class="sxs-lookup"><span data-stu-id="dc75a-123">From the screenshot below, the domain name is **contoso.onmicrosoft.com**, and the GUID within brackets is the tenant ID.</span></span> 
  
    ![Получение домена AAD](./media/data-lake-store-end-user-authenticate-using-active-directory/get-aad-domain.png)

## <a name="end-user-authentication"></a><span data-ttu-id="dc75a-125">Аутентификация пользователей</span><span class="sxs-lookup"><span data-stu-id="dc75a-125">End-user authentication</span></span>
<span data-ttu-id="dc75a-126">Этот подход рекомендуется, если вам нужно, чтобы пользователи входили в приложение с помощью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc75a-126">This is the recommended approach if you want an end-user to log in to your application via Azure AD.</span></span> <span data-ttu-id="dc75a-127">Приложение будет иметь тот же уровень доступа к ресурсам Azure, что и вошедший пользователь.</span><span class="sxs-lookup"><span data-stu-id="dc75a-127">Your application will be able to access Azure resources with the same level of access as the end-user that logged in.</span></span> <span data-ttu-id="dc75a-128">Пользователю понадобится периодически вводить свои учетные данные, чтобы у вашего приложения оставался доступ.</span><span class="sxs-lookup"><span data-stu-id="dc75a-128">Your end-user will need to provide their credentials periodically in order for your application to maintain access.</span></span>

<span data-ttu-id="dc75a-129">В результате входа пользователя приложение получает маркер доступа и маркер обновления.</span><span class="sxs-lookup"><span data-stu-id="dc75a-129">The result of having the end-user log in is that your application is given an access token and a refresh token.</span></span> <span data-ttu-id="dc75a-130">Маркер доступа вкладывается в каждый запрос к Data Lake Store и Data Lake Analytics и по умолчанию действителен в течение одного часа.</span><span class="sxs-lookup"><span data-stu-id="dc75a-130">The access token gets attached to each request made to Data Lake Store or Data Lake Analytics, and it is valid for one hour by default.</span></span> <span data-ttu-id="dc75a-131">Маркер обновления может использоваться для получения нового маркера доступа. По умолчанию он действителен до двух недель, при условии, что используется регулярно.</span><span class="sxs-lookup"><span data-stu-id="dc75a-131">The refresh token can be used to obtain a new access token, and it is valid for up to two weeks by default, if used regularly.</span></span> <span data-ttu-id="dc75a-132">Для входа пользователей можно использовать два разных подхода.</span><span class="sxs-lookup"><span data-stu-id="dc75a-132">You can use two different approaches for end-user log in.</span></span>

### <a name="using-the-oauth-20-pop-up"></a><span data-ttu-id="dc75a-133">Использование всплывающего окна OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="dc75a-133">Using the OAuth 2.0 pop-up</span></span>
<span data-ttu-id="dc75a-134">Приложение может активировать всплывающее окно авторизации OAuth 2.0, в котором пользователь может ввести свои учетные данные.</span><span class="sxs-lookup"><span data-stu-id="dc75a-134">Your application can trigger an OAuth 2.0 authorization pop-up, in which the end-user can enter their credentials.</span></span> <span data-ttu-id="dc75a-135">При необходимости это всплывающее окно также работает с процессом двухфакторной проверки подлинности (2FA) Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc75a-135">This pop-up also works with the Azure AD Two-factor Authentication (2FA) process, if required.</span></span> 

> [!NOTE]
> <span data-ttu-id="dc75a-136">Этот метод еще не поддерживается в библиотеке аутентификации Azure AD (ADAL) для Java или Python.</span><span class="sxs-lookup"><span data-stu-id="dc75a-136">This method is not yet supported in the Azure AD Authentication Library (ADAL) for Python or Java.</span></span>
> 
> 

### <a name="directly-passing-in-user-credentials"></a><span data-ttu-id="dc75a-137">Непосредственная передача учетных данных пользователя</span><span class="sxs-lookup"><span data-stu-id="dc75a-137">Directly passing in user credentials</span></span>
<span data-ttu-id="dc75a-138">Приложение могут напрямую предоставлять Azure AD учетные данные пользователя.</span><span class="sxs-lookup"><span data-stu-id="dc75a-138">Your application can directly provide user credentials to Azure AD.</span></span> <span data-ttu-id="dc75a-139">Этот метод работает только для учетных записей на основе идентификаторов организации. Он не подходит для личных учетных записей пользователей или учетных записей на основе Live ID, включая те, которые заканчиваются на @outlook.com или @live.com.</span><span class="sxs-lookup"><span data-stu-id="dc75a-139">This method only works with organizational ID user accounts; it is not compatible with personal / “live ID” user accounts, including those ending in @outlook.com or @live.com.</span></span> <span data-ttu-id="dc75a-140">Кроме того, данный метод несовместим с учетными записями пользователей, для которых требуется двухфакторная проверка подлинности (2FA) Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc75a-140">Furthermore, this method is not compatible with user accounts that require Azure AD Two-factor Authentication (2FA).</span></span>

### <a name="what-do-i-need-to-use-this-approach"></a><span data-ttu-id="dc75a-141">Что мне нужно для применения этого подхода?</span><span class="sxs-lookup"><span data-stu-id="dc75a-141">What do I need to use this approach?</span></span>
* <span data-ttu-id="dc75a-142">Доменное имя Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc75a-142">Azure AD domain name.</span></span> <span data-ttu-id="dc75a-143">(см. предварительные требования в этой статье).</span><span class="sxs-lookup"><span data-stu-id="dc75a-143">This is already listed in the prerequisite of this article.</span></span>
* <span data-ttu-id="dc75a-144">**Собственное приложение** Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc75a-144">Azure AD **native application**</span></span>
* <span data-ttu-id="dc75a-145">Идентификатор приложения для собственного приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc75a-145">Application ID for the Azure AD native application</span></span>
* <span data-ttu-id="dc75a-146">URI перенаправления для собственного приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc75a-146">Redirect URI for the Azure AD native application</span></span>
* <span data-ttu-id="dc75a-147">Настроенные делегированные разрешения.</span><span class="sxs-lookup"><span data-stu-id="dc75a-147">Set delegated permissions</span></span>


## <a name="step-1-create-an-active-directory-native-application"></a><span data-ttu-id="dc75a-148">Шаг 1. Создание собственного приложения Active Directory</span><span class="sxs-lookup"><span data-stu-id="dc75a-148">Step 1: Create an Active Directory native application</span></span>

<span data-ttu-id="dc75a-149">Создайте и настройте собственное приложение Azure AD для аутентификации пользователей в Azure Data Lake Store с помощью Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="dc75a-149">Create and configure an Azure AD native application for end-user authentication with Azure Data Lake Store using Azure Active Directory.</span></span> <span data-ttu-id="dc75a-150">Инструкции см. в разделе [Создание приложения Azure AD](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="dc75a-150">For instructions, see [Create an Azure AD application](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>

<span data-ttu-id="dc75a-151">При выполнении инструкций по ссылке выше обязательно выберите тип приложения **Собственный**, как показано на следующем снимке экрана.</span><span class="sxs-lookup"><span data-stu-id="dc75a-151">While following the instructions at the above link, make sure you select **Native** for application type, as shown in the screenshot below.</span></span>

<span data-ttu-id="dc75a-152">![Создание веб-приложения](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "Создание собственного приложения")</span><span class="sxs-lookup"><span data-stu-id="dc75a-152">![Create web app](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "Create native app")</span></span>

## <a name="step-2-get-application-id-and-redirect-uri"></a><span data-ttu-id="dc75a-153">Шаг 2. Получение идентификатора приложения и URI перенаправления</span><span class="sxs-lookup"><span data-stu-id="dc75a-153">Step 2: Get application id and redirect URI</span></span>

<span data-ttu-id="dc75a-154">В разделе [Получение идентификатора приложения](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) описывается, как получить идентификатор приложения (также называемый идентификатором клиента на классическом портале Azure) для собственного приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc75a-154">See [Get the application ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) to retrieve the application id (also called the client ID in the Azure classic portal) of the Azure AD native application.</span></span>

<span data-ttu-id="dc75a-155">Чтобы получить универсальный код ресурса (URI) перенаправления, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="dc75a-155">To retrieve the redirect URI, follow the steps below.</span></span>

1. <span data-ttu-id="dc75a-156">На портале Azure выберите **Azure Active Directory**, щелкните **Регистрация приложений**, затем найдите и щелкните только что созданное собственное приложение Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc75a-156">From the Azure Portal, select **Azure Active Directory**, click **App registrations**, and then find and click the Azure AD native application that you just created.</span></span>

2. <span data-ttu-id="dc75a-157">В колонке **Параметры** приложения щелкните **URI перенаправления**.</span><span class="sxs-lookup"><span data-stu-id="dc75a-157">From the **Settings** blade for the application, click **Redirect URIs**.</span></span>

    ![Получение URI перенаправления](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-redirect-uri.png)

3. <span data-ttu-id="dc75a-159">Скопируйте отображенное значение.</span><span class="sxs-lookup"><span data-stu-id="dc75a-159">Copy the value displayed.</span></span>


## <a name="step-3-set-permissions"></a><span data-ttu-id="dc75a-160">Шаг 3. Установка разрешений</span><span class="sxs-lookup"><span data-stu-id="dc75a-160">Step 3: Set permissions</span></span>

1. <span data-ttu-id="dc75a-161">На портале Azure выберите **Azure Active Directory**, щелкните **Регистрация приложений**, затем найдите и щелкните только что созданное собственное приложение Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc75a-161">From the Azure Portal, select **Azure Active Directory**, click **App registrations**, and then find and click the Azure AD native application that you just created.</span></span>

2. <span data-ttu-id="dc75a-162">В колонке **Параметры** приложения щелкните **Необходимые разрешения** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="dc75a-162">From the **Settings** blade for the application, click **Required permissions**, and then click **Add**.</span></span>

    ![Идентификатор клиента](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-1.png)

3. <span data-ttu-id="dc75a-164">В колонке **Добавить доступ через API** щелкните **Выбор API** > **Azure Data Lake** > **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="dc75a-164">In the **Add API Access** blade, click **Select an API**, click **Azure Data Lake**, and then click **Select**.</span></span>

    ![Идентификатор клиента](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-2.png)
 
4.  <span data-ttu-id="dc75a-166">В колонке **Добавить доступ через API** щелкните **Выбор разрешений**, установите флажок, чтобы предоставить **полный доступ к Data Lake Store**, и нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="dc75a-166">In the **Add API Access** blade, click **Select permissions**, select the check box to give **Full access to Data Lake Store**, and then click **Select**.</span></span>

    ![Идентификатор клиента](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-3.png)

    <span data-ttu-id="dc75a-168">Нажмите кнопку **Done**(Готово).</span><span class="sxs-lookup"><span data-stu-id="dc75a-168">Click **Done**.</span></span>

5. <span data-ttu-id="dc75a-169">Повторите последние два шага, чтобы также предоставить разрешения для **API управления службами Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="dc75a-169">Repeat the last two steps to grant permissions for **Windows Azure Service Management API** as well.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="dc75a-170">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dc75a-170">Next steps</span></span>
<span data-ttu-id="dc75a-171">В этой статье мы создали собственное приложение Azure AD и собрали сведения, необходимые в клиентских приложениях, создаваемых с помощью пакетов SDK для .NET, Java, REST API и др. Из следующих статей вы узнаете, как с помощью веб-приложения Azure AD проходить аутентификацию в Data Lake Store, а затем выполнить другие операции в хранилище.</span><span class="sxs-lookup"><span data-stu-id="dc75a-171">In this article you created an Azure AD native application and gathered the information you need in your client applications that you author using .NET SDK, Java SDK, REST API, etc. You can now proceed to the following articles that talk about how to use the Azure AD web application to first authenticate with Data Lake Store and then perform other operations on the store.</span></span>

* [<span data-ttu-id="dc75a-172">Начало работы с хранилищем озера данных Azure с помощью пакета SDK .NET</span><span class="sxs-lookup"><span data-stu-id="dc75a-172">Get started with Azure Data Lake Store using .NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
* [<span data-ttu-id="dc75a-173">Начало работы с хранилищем озера данных Azure с помощью пакета SDK .NET</span><span class="sxs-lookup"><span data-stu-id="dc75a-173">Get started with Azure Data Lake Store using Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
* [<span data-ttu-id="dc75a-174">Начало работы с Azure Data Lake Store с помощью REST API</span><span class="sxs-lookup"><span data-stu-id="dc75a-174">Get started with Azure Data Lake Store using REST API</span></span>](data-lake-store-get-started-rest-api.md)

