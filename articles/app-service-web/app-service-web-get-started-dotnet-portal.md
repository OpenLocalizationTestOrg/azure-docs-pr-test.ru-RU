---
title: "веб-приложение Umbraco в hello портал Azure в течение пяти минут aaaDeploy | Документы Microsoft"
description: "Узнайте, как просто можно toorun веб-приложений в службе приложений путем развертывания пример приложения ASP.NET. Кроме того, вы сможете быстро просмотреть результаты."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: b1e6bd58-48d1-4007-9d6c-53fd6db061e3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: cephalin
ms.openlocfilehash: 6da45f99b3043a3684e3d99c14e6443d597b5212
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-umbraco-web-app-in-hello-azure-portal-in-five-minutes"></a><span data-ttu-id="d9b11-104">Развертывание веб-приложение Umbraco в hello портал Azure в течение пяти минут</span><span class="sxs-lookup"><span data-stu-id="d9b11-104">Deploy an Umbraco web app in hello Azure portal in five minutes</span></span>

<span data-ttu-id="d9b11-105">Этот учебник поможет вам развернуть n [Umbraco](https://our.umbraco.org/) веб-приложения слишком[службе приложений Azure](../app-service/app-service-value-prop-what-is.md) в минутах.</span><span class="sxs-lookup"><span data-stu-id="d9b11-105">This tutorial helps you deploy n [Umbraco](https://our.umbraco.org/) web app too[Azure App Service](../app-service/app-service-value-prop-what-is.md) in minutes.</span></span>

![Приложение Umbraco](./media/app-service-web-get-started-dotnet-portal/defaultpage.png)

## <a name="prerequisites"></a><span data-ttu-id="d9b11-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d9b11-107">Prerequisites</span></span>
<span data-ttu-id="d9b11-108">Вам потребуется учетная запись Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d9b11-108">You need a Microsoft Azure account.</span></span> <span data-ttu-id="d9b11-109">Если у вас нет учетной записи, [подпишитесь на бесплатную пробную версию](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) или [активируйте преимущества для подписчиков Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="d9b11-109">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="d9b11-110">[Пробное использование службы приложений](https://azure.microsoft.com/try/app-service/) возможно даже без учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="d9b11-110">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="d9b11-111">Создание начального приложения и воспроизведение к ней до часа tooan--без кредитной карты требуется, не обязательства.</span><span class="sxs-lookup"><span data-stu-id="d9b11-111">Create a starter app and play with it for up tooan hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="deploy-hello-aspnet-app"></a><span data-ttu-id="d9b11-112">Развертывание приложения ASP.NET hello</span><span class="sxs-lookup"><span data-stu-id="d9b11-112">Deploy hello ASP.NET app</span></span>
1. <span data-ttu-id="d9b11-113">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d9b11-113">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="d9b11-114">Откройте страницу [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS).</span><span class="sxs-lookup"><span data-stu-id="d9b11-114">Open [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS).</span></span>

    <span data-ttu-id="d9b11-115">Указывает tooimmediately ярлык настроить новое приложение Umbraco в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d9b11-115">This link is a shortcut tooimmediately configure a new Umbraco app in hello Azure portal.</span></span>

3. <span data-ttu-id="d9b11-116">В поле **Имя приложения** введите имя веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="d9b11-116">In **App name**, type a web app name.</span></span> <span data-ttu-id="d9b11-117">Если вы увидите зеленый флажок в поле hello hello имя является уникальным в hello `azurewebsites.net` домена.</span><span class="sxs-lookup"><span data-stu-id="d9b11-117">You will see a green checkmark in hello box if hello name is unique in hello `azurewebsites.net` domain.</span></span>
   
5. <span data-ttu-id="d9b11-118">В **группы ресурсов**, нажмите кнопку **создать новый** toocreate новый [группы ресурсов](../azure-resource-manager/resource-group-overview.md), присвойте ему имя.</span><span class="sxs-lookup"><span data-stu-id="d9b11-118">In **Resource Group**, click **Create new** toocreate a new [resource group](../azure-resource-manager/resource-group-overview.md), then give it a name.</span></span>

7. <span data-ttu-id="d9b11-119">Щелкните **Расположение или план службы приложений** > **Создать**.</span><span class="sxs-lookup"><span data-stu-id="d9b11-119">Click **App Service plan/Location** > **Create New**.</span></span> <span data-ttu-id="d9b11-120">Настройка hello [план служб приложений](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) следующим:</span><span class="sxs-lookup"><span data-stu-id="d9b11-120">Configure hello [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) as shown:</span></span>

    - <span data-ttu-id="d9b11-121">В **план служб приложений**, требуемое имя типа hello.</span><span class="sxs-lookup"><span data-stu-id="d9b11-121">In **App Service plan**, type hello desired name.</span></span>
    - <span data-ttu-id="d9b11-122">В **расположение**, выбрать план toohost расположение.</span><span class="sxs-lookup"><span data-stu-id="d9b11-122">In **Location**, choose a location toohost your plan.</span></span>
    - <span data-ttu-id="d9b11-123">Щелкните **Ценовая категория**, а затем выберите **F1 Free** или другую категорию, которая вам подходит. Щелкните **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="d9b11-123">Click **Pricing tier**, then select **F1 Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="d9b11-124">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d9b11-124">Click **OK**.</span></span>

    <span data-ttu-id="d9b11-125">Конфигурация Umbraco CMS теперь должен выглядеть, как следующий снимок экрана приветствия:</span><span class="sxs-lookup"><span data-stu-id="d9b11-125">Your Umbraco CMS configuration should now look like hello following screenshot:</span></span>

    ![Настройка конфигурации: первое приложение Umbraco в службе приложений Azure](./media/app-service-web-get-started-dotnet-portal/configure-in-progress.png)

12. <span data-ttu-id="d9b11-127">Щелкните **База данных SQL** > **Создать новую базу данных**.</span><span class="sxs-lookup"><span data-stu-id="d9b11-127">Click **SQL Database** > **Create a new database**.</span></span> <span data-ttu-id="d9b11-128">Настройте hello базы данных SQL, как показано.</span><span class="sxs-lookup"><span data-stu-id="d9b11-128">Configure hello SQL Database as shown:</span></span>

    - <span data-ttu-id="d9b11-129">В поле **Имя** введите имя, например **myDB**.</span><span class="sxs-lookup"><span data-stu-id="d9b11-129">In **Name**, type a name, such as **myDB**.</span></span>
    - <span data-ttu-id="d9b11-130">Щелкните **Ценовая категория**, а затем выберите **F1 Free** или другую категорию, которая вам подходит. Щелкните **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="d9b11-130">Click **Pricing tier**, then select **F Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="d9b11-131">Щелкните **Целевой сервер** > **Создать сервер**.</span><span class="sxs-lookup"><span data-stu-id="d9b11-131">Click **Target server** > **Create a new server**.</span></span> <span data-ttu-id="d9b11-132">Настройка сервера базы данных hello, как показано:</span><span class="sxs-lookup"><span data-stu-id="d9b11-132">Configure hello database server as shown:</span></span>

        - <span data-ttu-id="d9b11-133">В поле **Имя сервера** введите имя сервера.</span><span class="sxs-lookup"><span data-stu-id="d9b11-133">In **Server name**, type a server name.</span></span> <span data-ttu-id="d9b11-134">Если вы увидите зеленый флажок в поле hello hello имя является уникальным в hello `.database.windows.net` домена.</span><span class="sxs-lookup"><span data-stu-id="d9b11-134">You will see a green checkmark in hello box if hello name is unique in hello `.database.windows.net` domain.</span></span>
        - <span data-ttu-id="d9b11-135">В **имя входа администратора сервера**, имя пользователя администратора требуемого типа hello.</span><span class="sxs-lookup"><span data-stu-id="d9b11-135">In **Server admin login**, type hello desired admininistrator username.</span></span>
        - <span data-ttu-id="d9b11-136">В **пароль** и **подтверждение пароля**, введите нужный пароль hello.</span><span class="sxs-lookup"><span data-stu-id="d9b11-136">In **Password** and **Confirm password**, type hello desired password.</span></span>
        - <span data-ttu-id="d9b11-137">В расположении выберите hello того же расположения, используемого для веб-приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d9b11-137">In Location, select hello same location you use for hello web app.</span></span>
        - <span data-ttu-id="d9b11-138">Убедитесь, что **tooaccess сервера разрешить службам azure** выбран.</span><span class="sxs-lookup"><span data-stu-id="d9b11-138">Make sure **Allow azure services tooaccess server** is selected.</span></span>
        - <span data-ttu-id="d9b11-139">Нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="d9b11-139">Click **Select**.</span></span>
    
    - <span data-ttu-id="d9b11-140">Нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="d9b11-140">Click **Select**.</span></span>

13. <span data-ttu-id="d9b11-141">Нажмите кнопку **веб-параметров приложения**, укажите имя пользователя базы данных hello и пароль и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d9b11-141">Click **Web app settings**, specify hello database username and password, and click **OK**.</span></span>

    <span data-ttu-id="d9b11-142">Конфигурация Umbraco CMS теперь должен выглядеть, как следующий снимок экрана приветствия:</span><span class="sxs-lookup"><span data-stu-id="d9b11-142">Your Umbraco CMS configuration should now look like hello following screenshot:</span></span>

    ![Настройка конфигурации завершена: первое приложение Umbraco в службе приложений Azure](./media/app-service-web-get-started-dotnet-portal/configure-complete.png)

14. <span data-ttu-id="d9b11-144">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="d9b11-144">Click **Create**.</span></span>
    
    <span data-ttu-id="d9b11-145">Теперь Azure создаст приложение Umbraco на основе выбранной конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d9b11-145">Azure now creates your Umbraco app based on your configuration.</span></span> <span data-ttu-id="d9b11-146">Должно появиться уведомление с текстом **Развертывание начато**.</span><span class="sxs-lookup"><span data-stu-id="d9b11-146">You should see a **Deployment started...** notification.</span></span>

    ![Успешное развертывание: первое приложение Umbraco в службе приложений Azure](./media/app-service-web-get-started-dotnet-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-umrbaco-web-app"></a><span data-ttu-id="d9b11-148">Запуск веб-приложения Umrbaco и управление им</span><span class="sxs-lookup"><span data-stu-id="d9b11-148">Launch and manage your Umrbaco web app</span></span>

<span data-ttu-id="d9b11-149">Когда Azure завершит развертывание приложения, появится еще одно уведомление.</span><span class="sxs-lookup"><span data-stu-id="d9b11-149">When Azure completes app deployment you see another notification.</span></span>

![Успешное развертывание: первое приложение Umbraco в службе приложений Azure](./media/app-service-web-get-started-dotnet-portal/deployment-succeeded.png)

1. <span data-ttu-id="d9b11-151">Щелкните уведомление hello.</span><span class="sxs-lookup"><span data-stu-id="d9b11-151">Click hello notification.</span></span> <span data-ttu-id="d9b11-152">Если вы пропустили всегда доступен, щелкнув hello уведомления колокольчика (![ниже уведомления - первый Umbraco в службе приложений Azure](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span><span class="sxs-lookup"><span data-stu-id="d9b11-152">If you missed it, you can always access it by clicking hello notification bell (![Notification bellow - first Umbraco in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span></span>

    <span data-ttu-id="d9b11-153">Теперь должна отображаться [колонка](../azure-resource-manager/resource-group-portal.md#manage-resources) управления веб-приложением. (*Колонка*: горизонтальная страница портала.)</span><span class="sxs-lookup"><span data-stu-id="d9b11-153">You should now see your web app's management [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) (*blade*: a portal page that opens horizontally).</span></span>

3. <span data-ttu-id="d9b11-154">В hello вверху страницы обзора hello щелкните **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="d9b11-154">In hello top of hello Overview page, click **Browse**.</span></span>
   
    ![Обзор: первое приложение Umbraco в службе приложений Azure](./media/app-service-web-get-started-dotnet-portal/browse.png)

    <span data-ttu-id="d9b11-156">Теперь вы видите hello Umbraco **приветствия** страницы.</span><span class="sxs-lookup"><span data-stu-id="d9b11-156">Now you see hello Umbraco **Welcome** page.</span></span> <span data-ttu-id="d9b11-157">Настройте установку Umbraco hello и начать воспроизведение с ним!</span><span class="sxs-lookup"><span data-stu-id="d9b11-157">Configure hello Umbraco installation and start playing with it!</span></span>

    ![Конфигурация Umbraco: первое приложение Umbraco в службе приложений Azure](./media/app-service-web-get-started-dotnet-portal/umbraco-config.png)
    
## <a name="next-steps"></a><span data-ttu-id="d9b11-159">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d9b11-159">Next steps</span></span>
* <span data-ttu-id="d9b11-160">[Развертывание ASP.NET tooAzure приложения web службу приложений, с помощью Visual Studio](app-service-web-get-started-dotnet.md) -Узнайте, как toocreate новый веб-приложение Azure из Visual Studio, используя любой из hello включены шаблоны приложений.</span><span class="sxs-lookup"><span data-stu-id="d9b11-160">[Deploy an ASP.NET web app tooAzure App Service, using Visual Studio](app-service-web-get-started-dotnet.md) - Learn how toocreate a new Azure web app from Visual Studio, using any one of hello included application templates.</span></span>
* <span data-ttu-id="d9b11-161">[Развертывание tooAzure ваш код приложения службы](web-sites-deploy.md)-Узнайте, как toodeploy из FTP или источника контролировать репозиториев.</span><span class="sxs-lookup"><span data-stu-id="d9b11-161">[Deploy your code tooAzure App Service](web-sites-deploy.md)- Learn how toodeploy from FTP or from source control repositories.</span></span>
* <span data-ttu-id="d9b11-162">[Добавление функциональности tooyour первого веб-приложения](app-service-web-get-started-2.md) -занять вашего приложения Azure toohello Далее уровня.</span><span class="sxs-lookup"><span data-stu-id="d9b11-162">[Add functionality tooyour first web app](app-service-web-get-started-2.md) - Take your Azure app toohello next level.</span></span> <span data-ttu-id="d9b11-163">Проверяйте подлинность пользователей.</span><span class="sxs-lookup"><span data-stu-id="d9b11-163">Authenticate your users.</span></span> <span data-ttu-id="d9b11-164">Масштабируйте приложение в зависимости от потребностей.</span><span class="sxs-lookup"><span data-stu-id="d9b11-164">Scale it based on demand.</span></span> <span data-ttu-id="d9b11-165">Настраивайте оповещения производительности.</span><span class="sxs-lookup"><span data-stu-id="d9b11-165">Set up some performance alerts.</span></span> <span data-ttu-id="d9b11-166">И все это — с помощью нескольких действий.</span><span class="sxs-lookup"><span data-stu-id="d9b11-166">All with a few clicks.</span></span>
