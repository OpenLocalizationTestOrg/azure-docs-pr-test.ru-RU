---
title: "Приступая к работе с аутентификацией Azure AD с помощью портала Azure | Документация Майкрософт"
description: "Узнайте, как использовать аутентификацию Azure Active Directory (Azure AD) для работы с API служб мультимедиа Azure с помощью портала Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: 829e0759f8aeb8758f6b8895b88b60b66ffb22ed
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-ad-authentication-by-using-the-azure-portal"></a><span data-ttu-id="89910-103">Приступая к работе с аутентификацией Azure AD с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="89910-103">Get started with Azure AD authentication by using the Azure portal</span></span>

<span data-ttu-id="89910-104">Узнайте, как использовать аутентификацию Azure Active Directory (Azure AD) для доступа к API служб мультимедиа Azure с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="89910-104">Learn how to use the Azure portal to access Azure Active Directory (Azure AD) authentication to access the Azure Media Services API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89910-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="89910-105">Prerequisites</span></span>

- <span data-ttu-id="89910-106">Учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="89910-106">An Azure account.</span></span> <span data-ttu-id="89910-107">Если у вас нет учетной записи Azure, начните с получения [бесплатной пробной версии](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="89910-107">If you don't have an account, start with an [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="89910-108">Учетная запись служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="89910-108">A Media Services account.</span></span> <span data-ttu-id="89910-109">Дополнительные сведения см. в статье [Создание учетной записи служб мультимедиа Azure с помощью портала Azure](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="89910-109">For more information, see [Create an Azure Media Services account by using the Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="89910-110">Обязательно ознакомьтесь с разделом [Доступ к API служб мультимедиа Azure с помощью аутентификации Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="89910-110">Make sure you review the [Accessing Azure Media Services API with Azure AD authentication overview](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

<span data-ttu-id="89910-111">При использовании аутентификации Azure AD со службами мультимедиа Azure доступны два метода аутентификации.</span><span class="sxs-lookup"><span data-stu-id="89910-111">When you use Azure AD authentication with Azure Media Services, you have two authentication options:</span></span>

- <span data-ttu-id="89910-112">**Аутентификация пользователя**.</span><span class="sxs-lookup"><span data-stu-id="89910-112">**User authentication**.</span></span> <span data-ttu-id="89910-113">Аутентификация пользователя, который использует приложение для взаимодействия с ресурсами служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="89910-113">Authenticate a person who is using the app to interact with Media Services resources.</span></span> <span data-ttu-id="89910-114">Интерактивное приложение должно сначала запросить у пользователя учетные данные.</span><span class="sxs-lookup"><span data-stu-id="89910-114">The interactive application should first prompt the user for credentials.</span></span> <span data-ttu-id="89910-115">Примером может послужить приложение консоли управления, которое используется авторизованными пользователями для мониторинга заданий кодирования или потоковой трансляции.</span><span class="sxs-lookup"><span data-stu-id="89910-115">An example is a management console app used by authorized users to monitor encoding jobs or live streaming.</span></span> 
- <span data-ttu-id="89910-116">**Аутентификация субъекта-службы**.</span><span class="sxs-lookup"><span data-stu-id="89910-116">**Service principal authentication**.</span></span> <span data-ttu-id="89910-117">Аутентификация службы.</span><span class="sxs-lookup"><span data-stu-id="89910-117">Authenticate a service.</span></span> <span data-ttu-id="89910-118">Этот метод аутентификации обычно используют приложения, которые выполняют службы управляющей программы, службы среднего уровня или запланированные задания: веб-приложения, приложения-функции, приложения логики, интерфейсы API или микрослужбы.</span><span class="sxs-lookup"><span data-stu-id="89910-118">Applications that commonly use this authentication method are apps that run daemon services, middle-tier services, or scheduled jobs: web apps, function apps, logic apps, APIs, or a microservice.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="89910-119">Службы мультимедиа в настоящее время поддерживают модель аутентификации с помощью службы контроля доступа Azure.</span><span class="sxs-lookup"><span data-stu-id="89910-119">Currently, Media Services supports the Azure Access Control service authentication model.</span></span> <span data-ttu-id="89910-120">Тем не менее авторизация посредством службы контроля доступа будет объявлена устаревшей 1 июня 2018 года.</span><span class="sxs-lookup"><span data-stu-id="89910-120">However, Access Control authorization will be deprecated on June 1, 2018.</span></span> <span data-ttu-id="89910-121">Мы рекомендуем как можно быстрее перейти на использование модели аутентификации Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89910-121">We recommend that you migrate to the Azure AD authentication model as soon as possible.</span></span>

## <a name="select-the-authentication-method"></a><span data-ttu-id="89910-122">Выбор метода аутентификации</span><span class="sxs-lookup"><span data-stu-id="89910-122">Select the authentication method</span></span>

1. <span data-ttu-id="89910-123">На [портале Azure](https://portal.azure.com/) выберите свою учетную запись служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="89910-123">In the [Azure portal](https://portal.azure.com/), select your Media Services account.</span></span>
2. <span data-ttu-id="89910-124">Выберите способ подключения к API служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="89910-124">Select how to connect to the Media Services API.</span></span>

    ![Страница выбора способа подключения](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started01.png)

## <a name="user-authentication"></a><span data-ttu-id="89910-126">Аутентификация пользователей</span><span class="sxs-lookup"><span data-stu-id="89910-126">User authentication</span></span>

<span data-ttu-id="89910-127">Для подключения к API служб мультимедиа с помощью аутентификации пользователя клиентскому приложению требуется запросить маркер Azure AD со следующими параметрами:</span><span class="sxs-lookup"><span data-stu-id="89910-127">To connect to the Media Services API by using the user authentication option, the client app needs to request an Azure AD token that has the following parameters:</span></span>  

* <span data-ttu-id="89910-128">Конечная точка клиента Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89910-128">Azure AD tenant endpoint</span></span>
* <span data-ttu-id="89910-129">Универсальный код ресурса (URI) для ресурса служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="89910-129">Media Services resource URI</span></span>
* <span data-ttu-id="89910-130">Идентификатор клиента (собственного) приложения служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="89910-130">Media Services (native) application client ID</span></span> 
* <span data-ttu-id="89910-131">Универсальный код ресурса (URI) перенаправления (собственного) приложения служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="89910-131">Media Services (native) application redirect URI</span></span> 
* <span data-ttu-id="89910-132">Универсальный код ресурса (URI) для ресурса REST служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="89910-132">Resource URI for REST Media Services</span></span>

<span data-ttu-id="89910-133">Значения этих параметров можно получить на странице **Подключение к API служб мультимедиа с помощью проверки подлинности пользователя**.</span><span class="sxs-lookup"><span data-stu-id="89910-133">You can get the values for these parameters on the **Media Services API with user authentication** page.</span></span> 

![Страница подключения с помощью аутентификации пользователя](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started02.png)

<span data-ttu-id="89910-135">При подключении к API служб мультимедиа с помощью пакета SDK служб мультимедиа для Microsoft .NET требуемые значения доступны в самом пакете SDK.</span><span class="sxs-lookup"><span data-stu-id="89910-135">If you connect to the Media Services API by using the Media Services Microsoft .NET SDK, the required values are available to you as part of the SDK.</span></span> <span data-ttu-id="89910-136">Дополнительные сведения см. в разделе [Использование аутентификации Azure AD для доступа к API служб мультимедиа Azure с помощью .NET](media-services-dotnet-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="89910-136">For more information, see [Use Azure AD authentication to access the Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span>

<span data-ttu-id="89910-137">Если вы не используете клиентский пакет SDK служб мультимедиа для .NET, то вам необходимо вручную создать запрос маркера Azure AD, указав параметры, описанные ранее.</span><span class="sxs-lookup"><span data-stu-id="89910-137">If you're not using the Media Services .NET client SDK, you must manually create an Azure AD token request by using the parameters discussed earlier.</span></span> <span data-ttu-id="89910-138">Дополнительные сведения см. в разделе [Библиотеки проверки подлинности Azure Active Directory](../active-directory/develop/active-directory-authentication-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="89910-138">For more information, see [How to use the Azure AD Authentication Library to get the Azure AD token](../active-directory/develop/active-directory-authentication-libraries.md).</span></span>

## <a name="service-principal-authentication"></a><span data-ttu-id="89910-139">Проверка подлинности субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="89910-139">Service principal authentication</span></span>

<span data-ttu-id="89910-140">Для подключения к API служб мультимедиа в режиме аутентификации субъекта-службы приложению среднего уровня (веб-API или веб-приложению) требуется запросить маркер Azure AD со следующими параметрами:</span><span class="sxs-lookup"><span data-stu-id="89910-140">To connect to the Media Services API by using the service principal option, your middle-tier app (web API or web application) needs to request an Azure AD token that has the following parameters:</span></span>  

* <span data-ttu-id="89910-141">Конечная точка клиента Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89910-141">Azure AD tenant endpoint</span></span>
* <span data-ttu-id="89910-142">Универсальный код ресурса (URI) для ресурса служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="89910-142">Media Services resource URI</span></span> 
* <span data-ttu-id="89910-143">Универсальный код ресурса (URI) для ресурса REST служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="89910-143">Resource URI for REST Media Services</span></span>
* <span data-ttu-id="89910-144">Значения приложения Azure AD: **идентификатор клиента** и **секрет клиента**.</span><span class="sxs-lookup"><span data-stu-id="89910-144">Azure AD application values: the **client ID** and **client secret**</span></span>

<span data-ttu-id="89910-145">Значения этих параметров можно получить на странице **Подключение к API служб мультимедиа с помощью субъекта-службы**.</span><span class="sxs-lookup"><span data-stu-id="89910-145">You can get the values for these parameters on the **Connect to Media Services API with service principal** page.</span></span> <span data-ttu-id="89910-146">На этой странице создайте новое приложение Azure AD или выберите существующее.</span><span class="sxs-lookup"><span data-stu-id="89910-146">Use this page to create a new Azure AD application or to select an existing one.</span></span> <span data-ttu-id="89910-147">После выбора приложения Azure AD можно получить идентификатор клиента (идентификатор приложения) и сформировать значения секрета клиента (ключа).</span><span class="sxs-lookup"><span data-stu-id="89910-147">After you select the Azure AD app, you can get the client ID (Application ID) and generate the client secret (key) values.</span></span> 

![Страница подключения с помощью субъекта-службы](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started04.png)

<span data-ttu-id="89910-149">Когда откроется колонка **Субъект-служба**, в ней будет выбрано первое приложение Azure AD, которое удовлетворяет следующим требованиям:</span><span class="sxs-lookup"><span data-stu-id="89910-149">When the **Service Principal** blade opens, the first Azure AD application that meets the following criteria is selected:</span></span>

- <span data-ttu-id="89910-150">оно зарегистрировано в Azure AD;</span><span class="sxs-lookup"><span data-stu-id="89910-150">It is a registered Azure AD application.</span></span>
- <span data-ttu-id="89910-151">ему назначены разрешения участника или владельца для учетной записи (управление доступом на основе ролей).</span><span class="sxs-lookup"><span data-stu-id="89910-151">It has Contributor or Owner Role-Based Access Control permissions on the account.</span></span>

<span data-ttu-id="89910-152">После создания или выбора приложения Azure AD можно создать и скопировать секрет клиента (ключ) и идентификатор клиента (идентификатор приложения).</span><span class="sxs-lookup"><span data-stu-id="89910-152">After you create or select an Azure AD app, you can create and copy a client secret (key) and the client ID (Application ID).</span></span> <span data-ttu-id="89910-153">Для получения маркера доступа в этом сценарии требуются секрет клиента и идентификатор клиента.</span><span class="sxs-lookup"><span data-stu-id="89910-153">The client secret and client ID are required to get the access token in this scenario.</span></span>

<span data-ttu-id="89910-154">Если разрешения на создание приложений Azure AD в вашем домене отсутствуют, элементы управления приложением Azure AD в колонке не отображаются и выводится предупреждающее сообщение.</span><span class="sxs-lookup"><span data-stu-id="89910-154">If you don't have permissions to create Azure AD apps in your domain, the Azure AD app controls of the blade are not shown, and a warning message is displayed.</span></span>

<span data-ttu-id="89910-155">Подключение к API служб мультимедиа с помощью пакета SDK служб мультимедиа для .NET описывается в разделе [Использование аутентификации Azure AD для доступа к API служб мультимедиа Azure с помощью .NET](media-services-dotnet-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="89910-155">If you connect to the Media Services API by using the Media Services .NET SDK, see [Use Azure AD authentication to access the Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span>

<span data-ttu-id="89910-156">Если вы не используете клиентский пакет SDK служб мультимедиа для .NET, то вам необходимо вручную создать запрос маркера Azure AD, указав параметры, описанные ранее.</span><span class="sxs-lookup"><span data-stu-id="89910-156">If you are not using the Media Services .NET client SDK, you must manually create an Azure AD token request using the parameters discussed earlier.</span></span> <span data-ttu-id="89910-157">Дополнительные сведения см. в разделе [Библиотеки проверки подлинности Azure Active Directory](../active-directory/develop/active-directory-authentication-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="89910-157">For more information, see [How to use the Azure AD Authentication Library to get the Azure AD token](../active-directory/develop/active-directory-authentication-libraries.md).</span></span>

### <a name="get-the-client-id-and-client-secret"></a><span data-ttu-id="89910-158">Получение идентификатора клиента и секрета клиента</span><span class="sxs-lookup"><span data-stu-id="89910-158">Get the client ID and client secret</span></span>

<span data-ttu-id="89910-159">После выбора существующего приложения Azure AD или параметра для создания нового приложения отображаются показанные ниже кнопки.</span><span class="sxs-lookup"><span data-stu-id="89910-159">After you select an existing Azure AD app or select the option to create a new one, the following buttons appear:</span></span>

![Кнопки "Управление разрешениями" и "Управление приложением"](./media/media-services-portal-get-started-with-aad/media-services-portal-manage.png)

<span data-ttu-id="89910-161">Чтобы открыть колонку приложения Azure AD, нажмите кнопку **Управление приложением**.</span><span class="sxs-lookup"><span data-stu-id="89910-161">To open the Azure AD application blade, click **Manage application**.</span></span> <span data-ttu-id="89910-162">В колонке **Управление приложением** можно получить идентификатор клиента для приложения (идентификатор приложения).</span><span class="sxs-lookup"><span data-stu-id="89910-162">On the **Manage application** blade, you can get the app's client ID (Application ID).</span></span> <span data-ttu-id="89910-163">Чтобы создать секрет клиента (ключ), щелкните **Ключи**.</span><span class="sxs-lookup"><span data-stu-id="89910-163">To generate a client secret (key), select **Keys**.</span></span>

![Параметр "Ключи" в колонке "Управление приложением"](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started06.png) 

### <a name="manage-permissions-and-the-application"></a><span data-ttu-id="89910-165">Управление разрешениями и приложением</span><span class="sxs-lookup"><span data-stu-id="89910-165">Manage permissions and the application</span></span>

<span data-ttu-id="89910-166">После выбора приложения Azure AD можно управлять им и разрешениями.</span><span class="sxs-lookup"><span data-stu-id="89910-166">After you select the Azure AD application, you can manage the application and permissions.</span></span> <span data-ttu-id="89910-167">Чтобы настроить приложение Azure AD для доступа к другим приложениям, нажмите кнопку **Управление разрешениями**.</span><span class="sxs-lookup"><span data-stu-id="89910-167">To set up your Azure AD application to access other applications, click **Manage permissions**.</span></span> <span data-ttu-id="89910-168">Чтобы выполнить такие задачи управления, как изменение ключей, URL-адресов ответа или манифеста приложения, нажмите кнопку **Управление приложением**.</span><span class="sxs-lookup"><span data-stu-id="89910-168">For management tasks, such as changing keys and reply URLs, or to edit the application’s manifest, click **Manage application**.</span></span>

### <a name="edit-the-apps-settings-or-manifest"></a><span data-ttu-id="89910-169">Изменение параметров или манифеста приложения</span><span class="sxs-lookup"><span data-stu-id="89910-169">Edit the app's settings or manifest</span></span>

<span data-ttu-id="89910-170">Чтобы изменить параметры или манифест приложения, нажмите кнопку **Управление приложением**.</span><span class="sxs-lookup"><span data-stu-id="89910-170">To edit the app's settings or manifest, click **Manage application**.</span></span>

![Страница "Управление приложением"](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started05.png)

## <a name="next-steps"></a><span data-ttu-id="89910-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="89910-172">Next steps</span></span>

<span data-ttu-id="89910-173">Приступите к [передаче файлов в учетную запись](media-services-portal-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="89910-173">Get started with [uploading files to your account](media-services-portal-upload-files.md).</span></span>
