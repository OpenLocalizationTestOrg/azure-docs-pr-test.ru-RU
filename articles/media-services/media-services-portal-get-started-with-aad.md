---
title: "aaaGet к выполнению проверки подлинности Azure AD с помощью hello портал Azure | Документы Microsoft"
description: "Узнайте, как toouse hello Azure портала tooaccess tooconsume проверки подлинности Azure Active Directory (Azure AD) hello API служб мультимедиа Azure."
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
ms.openlocfilehash: 497ad1806b3fd1262802adefb6e12b65ee9f2d61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-ad-authentication-by-using-hello-azure-portal"></a><span data-ttu-id="ea249-103">Начало работы с проверкой подлинности Azure AD с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="ea249-103">Get started with Azure AD authentication by using hello Azure portal</span></span>

<span data-ttu-id="ea249-104">Узнайте, как toouse hello Azure tooaccess портала Azure Active Directory (Azure AD) для проверки подлинности tooaccess hello API служб мультимедиа Azure.</span><span class="sxs-lookup"><span data-stu-id="ea249-104">Learn how toouse hello Azure portal tooaccess Azure Active Directory (Azure AD) authentication tooaccess hello Azure Media Services API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ea249-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ea249-105">Prerequisites</span></span>

- <span data-ttu-id="ea249-106">Учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="ea249-106">An Azure account.</span></span> <span data-ttu-id="ea249-107">Если у вас нет учетной записи Azure, начните с получения [бесплатной пробной версии](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ea249-107">If you don't have an account, start with an [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="ea249-108">Учетная запись служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="ea249-108">A Media Services account.</span></span> <span data-ttu-id="ea249-109">Дополнительные сведения см. в разделе [создать учетную запись служб мультимедиа Azure с помощью портала Azure hello](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="ea249-109">For more information, see [Create an Azure Media Services account by using hello Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="ea249-110">Обязательно изучите hello [доступ к Azure API служб мультимедиа с обзор проверки подлинности Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="ea249-110">Make sure you review hello [Accessing Azure Media Services API with Azure AD authentication overview](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

<span data-ttu-id="ea249-111">При использовании аутентификации Azure AD со службами мультимедиа Azure доступны два метода аутентификации.</span><span class="sxs-lookup"><span data-stu-id="ea249-111">When you use Azure AD authentication with Azure Media Services, you have two authentication options:</span></span>

- <span data-ttu-id="ea249-112">**Аутентификация пользователя**.</span><span class="sxs-lookup"><span data-stu-id="ea249-112">**User authentication**.</span></span> <span data-ttu-id="ea249-113">Проверка подлинности пользователя, работающего с toointeract приложения hello с ресурсами службы мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="ea249-113">Authenticate a person who is using hello app toointeract with Media Services resources.</span></span> <span data-ttu-id="ea249-114">интерактивные приложения Hello должен сначала запросить учетные данные пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="ea249-114">hello interactive application should first prompt hello user for credentials.</span></span> <span data-ttu-id="ea249-115">Пример — приложение консоли управления, используемые заданий кодирования toomonitor авторизованных пользователей или динамической потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="ea249-115">An example is a management console app used by authorized users toomonitor encoding jobs or live streaming.</span></span> 
- <span data-ttu-id="ea249-116">**Аутентификация субъекта-службы**.</span><span class="sxs-lookup"><span data-stu-id="ea249-116">**Service principal authentication**.</span></span> <span data-ttu-id="ea249-117">Аутентификация службы.</span><span class="sxs-lookup"><span data-stu-id="ea249-117">Authenticate a service.</span></span> <span data-ttu-id="ea249-118">Этот метод аутентификации обычно используют приложения, которые выполняют службы управляющей программы, службы среднего уровня или запланированные задания: веб-приложения, приложения-функции, приложения логики, интерфейсы API или микрослужбы.</span><span class="sxs-lookup"><span data-stu-id="ea249-118">Applications that commonly use this authentication method are apps that run daemon services, middle-tier services, or scheduled jobs: web apps, function apps, logic apps, APIs, or a microservice.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ea249-119">В настоящее время службы мультимедиа поддерживают модель проверки подлинности службы контроля доступа Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ea249-119">Currently, Media Services supports hello Azure Access Control service authentication model.</span></span> <span data-ttu-id="ea249-120">Тем не менее авторизация посредством службы контроля доступа будет объявлена устаревшей 1 июня 2018 года.</span><span class="sxs-lookup"><span data-stu-id="ea249-120">However, Access Control authorization will be deprecated on June 1, 2018.</span></span> <span data-ttu-id="ea249-121">Рекомендуется как можно быстрее перейти модель проверки подлинности toohello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ea249-121">We recommend that you migrate toohello Azure AD authentication model as soon as possible.</span></span>

## <a name="select-hello-authentication-method"></a><span data-ttu-id="ea249-122">Выберите метод проверки подлинности hello</span><span class="sxs-lookup"><span data-stu-id="ea249-122">Select hello authentication method</span></span>

1. <span data-ttu-id="ea249-123">В hello [портал Azure](https://portal.azure.com/), выберите учетную запись служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="ea249-123">In hello [Azure portal](https://portal.azure.com/), select your Media Services account.</span></span>
2. <span data-ttu-id="ea249-124">Выбор метода tooconnect toohello API служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="ea249-124">Select how tooconnect toohello Media Services API.</span></span>

    ![Страница выбора способа подключения](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started01.png)

## <a name="user-authentication"></a><span data-ttu-id="ea249-126">Аутентификация пользователей</span><span class="sxs-lookup"><span data-stu-id="ea249-126">User authentication</span></span>

<span data-ttu-id="ea249-127">toohello tooconnect API служб мультимедиа с помощью hello вариант проверки подлинности пользователя, клиентское приложение hello должен toorequest маркера Azure AD, который имеет hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="ea249-127">tooconnect toohello Media Services API by using hello user authentication option, hello client app needs toorequest an Azure AD token that has hello following parameters:</span></span>  

* <span data-ttu-id="ea249-128">Конечная точка клиента Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ea249-128">Azure AD tenant endpoint</span></span>
* <span data-ttu-id="ea249-129">Универсальный код ресурса (URI) для ресурса служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="ea249-129">Media Services resource URI</span></span>
* <span data-ttu-id="ea249-130">Идентификатор клиента (собственного) приложения служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="ea249-130">Media Services (native) application client ID</span></span> 
* <span data-ttu-id="ea249-131">Универсальный код ресурса (URI) перенаправления (собственного) приложения служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="ea249-131">Media Services (native) application redirect URI</span></span> 
* <span data-ttu-id="ea249-132">Универсальный код ресурса (URI) для ресурса REST служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="ea249-132">Resource URI for REST Media Services</span></span>

<span data-ttu-id="ea249-133">Вы можете получить hello значения для этих параметров на hello **API служб мультимедиа с проверкой подлинности пользователя** страницы.</span><span class="sxs-lookup"><span data-stu-id="ea249-133">You can get hello values for these parameters on hello **Media Services API with user authentication** page.</span></span> 

![Страница подключения с помощью аутентификации пользователя](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started02.png)

<span data-ttu-id="ea249-135">При подключении toohello API служб мультимедиа с помощью Media Services Microsoft .NET SDK hello hello необходимых значений tooyou доступны как часть пакета SDK для hello.</span><span class="sxs-lookup"><span data-stu-id="ea249-135">If you connect toohello Media Services API by using hello Media Services Microsoft .NET SDK, hello required values are available tooyou as part of hello SDK.</span></span> <span data-ttu-id="ea249-136">Дополнительные сведения см. в разделе [tooaccess проверки подлинности используют Azure AD hello API служб мультимедиа Azure в .NET Framework](media-services-dotnet-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="ea249-136">For more information, see [Use Azure AD authentication tooaccess hello Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span>

<span data-ttu-id="ea249-137">Если вы не используете пакет SDK для клиента .NET служб мультимедиа hello, необходимо вручную создать запрос токена Azure AD с помощью параметров hello уже было сказано ранее.</span><span class="sxs-lookup"><span data-stu-id="ea249-137">If you're not using hello Media Services .NET client SDK, you must manually create an Azure AD token request by using hello parameters discussed earlier.</span></span> <span data-ttu-id="ea249-138">Дополнительные сведения см. в разделе [как tooget библиотеки проверки подлинности Azure AD hello toouse hello Azure AD токен](../active-directory/develop/active-directory-authentication-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="ea249-138">For more information, see [How toouse hello Azure AD Authentication Library tooget hello Azure AD token](../active-directory/develop/active-directory-authentication-libraries.md).</span></span>

## <a name="service-principal-authentication"></a><span data-ttu-id="ea249-139">Проверка подлинности субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="ea249-139">Service principal authentication</span></span>

<span data-ttu-id="ea249-140">toohello tooconnect API служб мультимедиа с помощью hello параметр участника службы, приложения среднего уровня (веб-API или веб-приложение) должен toorequest маркера Azure AD, который имеет hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="ea249-140">tooconnect toohello Media Services API by using hello service principal option, your middle-tier app (web API or web application) needs toorequest an Azure AD token that has hello following parameters:</span></span>  

* <span data-ttu-id="ea249-141">Конечная точка клиента Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ea249-141">Azure AD tenant endpoint</span></span>
* <span data-ttu-id="ea249-142">Универсальный код ресурса (URI) для ресурса служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="ea249-142">Media Services resource URI</span></span> 
* <span data-ttu-id="ea249-143">Универсальный код ресурса (URI) для ресурса REST служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="ea249-143">Resource URI for REST Media Services</span></span>
* <span data-ttu-id="ea249-144">Значения приложения Azure AD: hello **идентификатор клиента** и **секрет клиента**</span><span class="sxs-lookup"><span data-stu-id="ea249-144">Azure AD application values: hello **client ID** and **client secret**</span></span>

<span data-ttu-id="ea249-145">Вы можете получить hello значения для этих параметров на hello **подключения tooMedia API служб с субъектом-службой** страницы.</span><span class="sxs-lookup"><span data-stu-id="ea249-145">You can get hello values for these parameters on hello **Connect tooMedia Services API with service principal** page.</span></span> <span data-ttu-id="ea249-146">Использование этой страницы toocreate новый Azure AD приложения или tooselect уже существующий.</span><span class="sxs-lookup"><span data-stu-id="ea249-146">Use this page toocreate a new Azure AD application or tooselect an existing one.</span></span> <span data-ttu-id="ea249-147">После выбора приложения hello Azure AD можно получить идентификатор клиента hello (идентификатор приложения) и создать секрет (ключ) значениями hello клиента.</span><span class="sxs-lookup"><span data-stu-id="ea249-147">After you select hello Azure AD app, you can get hello client ID (Application ID) and generate hello client secret (key) values.</span></span> 

![Страница подключения с помощью субъекта-службы](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started04.png)

<span data-ttu-id="ea249-149">Здравствуйте, когда **участника-службы** открывает колонку, выбран первый Azure AD приложения hello, отвечающего hello следующие условия:</span><span class="sxs-lookup"><span data-stu-id="ea249-149">When hello **Service Principal** blade opens, hello first Azure AD application that meets hello following criteria is selected:</span></span>

- <span data-ttu-id="ea249-150">оно зарегистрировано в Azure AD;</span><span class="sxs-lookup"><span data-stu-id="ea249-150">It is a registered Azure AD application.</span></span>
- <span data-ttu-id="ea249-151">Он имеет разрешения участника или Owner Role-Based управления доступом для hello учетной записи.</span><span class="sxs-lookup"><span data-stu-id="ea249-151">It has Contributor or Owner Role-Based Access Control permissions on hello account.</span></span>

<span data-ttu-id="ea249-152">После создания или выбора приложения Azure AD, можно создать и скопируйте секрет клиента (ключ) и hello идентификатор клиента (идентификатор приложения).</span><span class="sxs-lookup"><span data-stu-id="ea249-152">After you create or select an Azure AD app, you can create and copy a client secret (key) and hello client ID (Application ID).</span></span> <span data-ttu-id="ea249-153">Идентификатор секрета и клиент клиента Hello, маркер доступа требуется tooget hello в этом сценарии.</span><span class="sxs-lookup"><span data-stu-id="ea249-153">hello client secret and client ID are required tooget hello access token in this scenario.</span></span>

<span data-ttu-id="ea249-154">При отсутствии приложения Azure AD toocreate разрешений в вашем домене, не отображаются элементы управления приложения Azure AD hello колонка hello и выводится предупреждающее сообщение.</span><span class="sxs-lookup"><span data-stu-id="ea249-154">If you don't have permissions toocreate Azure AD apps in your domain, hello Azure AD app controls of hello blade are not shown, and a warning message is displayed.</span></span>

<span data-ttu-id="ea249-155">При подключении toohello API служб мультимедиа с помощью Media Services .NET SDK hello. в разделе [tooaccess проверки подлинности используют Azure AD hello API служб мультимедиа Azure в .NET Framework](media-services-dotnet-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="ea249-155">If you connect toohello Media Services API by using hello Media Services .NET SDK, see [Use Azure AD authentication tooaccess hello Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span>

<span data-ttu-id="ea249-156">Если не используется пакет SDK для клиента .NET служб мультимедиа hello, необходимо вручную создать запрос токена Azure AD с помощью параметров hello уже было сказано ранее.</span><span class="sxs-lookup"><span data-stu-id="ea249-156">If you are not using hello Media Services .NET client SDK, you must manually create an Azure AD token request using hello parameters discussed earlier.</span></span> <span data-ttu-id="ea249-157">Дополнительные сведения см. в разделе [как tooget библиотеки проверки подлинности Azure AD hello toouse hello Azure AD токен](../active-directory/develop/active-directory-authentication-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="ea249-157">For more information, see [How toouse hello Azure AD Authentication Library tooget hello Azure AD token](../active-directory/develop/active-directory-authentication-libraries.md).</span></span>

### <a name="get-hello-client-id-and-client-secret"></a><span data-ttu-id="ea249-158">Получить идентификатор и секрет клиента приветствия клиента</span><span class="sxs-lookup"><span data-stu-id="ea249-158">Get hello client ID and client secret</span></span>

<span data-ttu-id="ea249-159">После выбора существующего приложения Azure AD или выберите hello параметр toocreate новый, отображаются hello следующие кнопки:</span><span class="sxs-lookup"><span data-stu-id="ea249-159">After you select an existing Azure AD app or select hello option toocreate a new one, hello following buttons appear:</span></span>

![Кнопки "Управление разрешениями" и "Управление приложением"](./media/media-services-portal-get-started-with-aad/media-services-portal-manage.png)

<span data-ttu-id="ea249-161">hello tooopen колонке приложения Azure AD щелкните **управления приложением**.</span><span class="sxs-lookup"><span data-stu-id="ea249-161">tooopen hello Azure AD application blade, click **Manage application**.</span></span> <span data-ttu-id="ea249-162">На hello **управления приложением** колонки, можно получить идентификатор клиента приложения hello (идентификатор приложения).</span><span class="sxs-lookup"><span data-stu-id="ea249-162">On hello **Manage application** blade, you can get hello app's client ID (Application ID).</span></span> <span data-ttu-id="ea249-163">секрет клиента (ключ), выберите toogenerate **ключей**.</span><span class="sxs-lookup"><span data-stu-id="ea249-163">toogenerate a client secret (key), select **Keys**.</span></span>

![Параметр "Ключи" в колонке "Управление приложением"](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started06.png) 

### <a name="manage-permissions-and-hello-application"></a><span data-ttu-id="ea249-165">Управление разрешениями и приложения hello</span><span class="sxs-lookup"><span data-stu-id="ea249-165">Manage permissions and hello application</span></span>

<span data-ttu-id="ea249-166">После выбора приложения hello Azure AD, вы можете управлять приложения hello и разрешения.</span><span class="sxs-lookup"><span data-stu-id="ea249-166">After you select hello Azure AD application, you can manage hello application and permissions.</span></span> <span data-ttu-id="ea249-167">tooset копирование вашего tooaccess приложения Azure AD щелкните другие приложения **Управление разрешениями**.</span><span class="sxs-lookup"><span data-stu-id="ea249-167">tooset up your Azure AD application tooaccess other applications, click **Manage permissions**.</span></span> <span data-ttu-id="ea249-168">Для задач управления, таких как изменение ключей и URL-адреса ответа и манифест приложения hello tooedit, нажмите кнопку **управления приложением**.</span><span class="sxs-lookup"><span data-stu-id="ea249-168">For management tasks, such as changing keys and reply URLs, or tooedit hello application’s manifest, click **Manage application**.</span></span>

### <a name="edit-hello-apps-settings-or-manifest"></a><span data-ttu-id="ea249-169">Изменить параметры приложения hello или манифеста</span><span class="sxs-lookup"><span data-stu-id="ea249-169">Edit hello app's settings or manifest</span></span>

<span data-ttu-id="ea249-170">параметры или манифест, приложение hello tooedit щелкните **управления приложением**.</span><span class="sxs-lookup"><span data-stu-id="ea249-170">tooedit hello app's settings or manifest, click **Manage application**.</span></span>

![Страница "Управление приложением"](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started05.png)

## <a name="next-steps"></a><span data-ttu-id="ea249-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ea249-172">Next steps</span></span>

<span data-ttu-id="ea249-173">Приступая к работе с [передача файлов учетная запись tooyour](media-services-portal-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="ea249-173">Get started with [uploading files tooyour account](media-services-portal-upload-files.md).</span></span>
