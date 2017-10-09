---
title: "aaaDeploy — приложение WordPress на портал Azure в течение пяти минут hello | Документы Microsoft"
description: "Узнайте, как просто можно toorun веб-приложений в службе приложений, развернув приложение WordPress. Кроме того, вы сможете быстро просмотреть результаты."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 6feac128-c728-4491-8b79-962da9a40788
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: cephalin
ms.openlocfilehash: 4cd26bbacf89657997847ded1284e472288ddebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-wordpress-app-in-hello-azure-portal-in-five-minutes"></a><span data-ttu-id="ca4bb-104">Развертывание приложения WordPress в hello портал Azure в течение пяти минут</span><span class="sxs-lookup"><span data-stu-id="ca4bb-104">Deploy a WordPress app in hello Azure portal in five minutes</span></span>

<span data-ttu-id="ca4bb-105">В этом учебнике показано как toodeploy первого [WordPress](https://wordpress.org/) веб-приложения слишком[службе приложений Azure](../app-service/app-service-value-prop-what-is.md) в минутах.</span><span class="sxs-lookup"><span data-stu-id="ca4bb-105">This tutorial shows you how toodeploy your first [WordPress](https://wordpress.org/) web app too[Azure App Service](../app-service/app-service-value-prop-what-is.md) in minutes.</span></span>

![Сайт WordPress](./media/app-service-web-get-started-php-portal/wpdashboard.png)

## <a name="prerequisites"></a><span data-ttu-id="ca4bb-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ca4bb-107">Prerequisites</span></span>
<span data-ttu-id="ca4bb-108">Вам потребуется учетная запись Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="ca4bb-108">You need a Microsoft Azure account.</span></span> <span data-ttu-id="ca4bb-109">Если у вас нет учетной записи, [подпишитесь на бесплатную пробную версию](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) или [активируйте преимущества для подписчиков Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="ca4bb-109">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="ca4bb-110">[Пробное использование службы приложений](https://azure.microsoft.com/try/app-service/) возможно даже без учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="ca4bb-110">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="ca4bb-111">Создание начального приложения и воспроизведение к ней до часа tooan--без кредитной карты требуется, не обязательства.</span><span class="sxs-lookup"><span data-stu-id="ca4bb-111">Create a starter app and play with it for up tooan hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="deploy-hello-wordpress-app"></a><span data-ttu-id="ca4bb-112">Развернуть приложение hello WordPress</span><span class="sxs-lookup"><span data-stu-id="ca4bb-112">Deploy hello WordPress app</span></span>
1. <span data-ttu-id="ca4bb-113">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ca4bb-113">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="ca4bb-114">Откройте страницу [https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress).</span><span class="sxs-lookup"><span data-stu-id="ca4bb-114">Open [https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress).</span></span>

    <span data-ttu-id="ca4bb-115">Указывает tooimmediately ярлык настроить новое приложение WordPress в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ca4bb-115">This link is a shortcut tooimmediately configure a new WordPress app in hello Azure portal.</span></span>

3. <span data-ttu-id="ca4bb-116">В поле **Имя приложения** введите имя веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="ca4bb-116">In **App name**, type a web app name.</span></span> <span data-ttu-id="ca4bb-117">Если вы увидите зеленый флажок в поле hello hello имя является уникальным в hello `azurewebsites.net` домена.</span><span class="sxs-lookup"><span data-stu-id="ca4bb-117">You will see a green checkmark in hello box if hello name is unique in hello `azurewebsites.net` domain.</span></span>
   
5. <span data-ttu-id="ca4bb-118">В **группы ресурсов**, нажмите кнопку **создать новый** toocreate новый [группы ресурсов](../azure-resource-manager/resource-group-overview.md), присвойте ему имя.</span><span class="sxs-lookup"><span data-stu-id="ca4bb-118">In **Resource Group**, click **Create new** toocreate a new [resource group](../azure-resource-manager/resource-group-overview.md), then give it a name.</span></span>

6. <span data-ttu-id="ca4bb-119">Из списка **Поставщик базы данных** выберите **CleaDB**.</span><span class="sxs-lookup"><span data-stu-id="ca4bb-119">In **Database Provider**, select **CleaDB**.</span></span>

7. <span data-ttu-id="ca4bb-120">Щелкните **Расположение или план службы приложений** > **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ca4bb-120">Click **App Service plan/Location** > **Create New**.</span></span> <span data-ttu-id="ca4bb-121">Настройка hello [план служб приложений](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) следующим:</span><span class="sxs-lookup"><span data-stu-id="ca4bb-121">Configure hello [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) as shown:</span></span>

    - <span data-ttu-id="ca4bb-122">В **план служб приложений**, требуемое имя типа hello.</span><span class="sxs-lookup"><span data-stu-id="ca4bb-122">In **App Service plan**, type hello desired name.</span></span>
    - <span data-ttu-id="ca4bb-123">В **расположение**, выбрать план toohost расположение.</span><span class="sxs-lookup"><span data-stu-id="ca4bb-123">In **Location**, choose a location toohost your plan.</span></span>
    - <span data-ttu-id="ca4bb-124">Щелкните **Ценовая категория**, а затем выберите **F1 Free** или другую категорию, которая вам подходит. Щелкните **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="ca4bb-124">Click **Pricing tier**, then select **F1 Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="ca4bb-125">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ca4bb-125">Click **OK**.</span></span>

8. <span data-ttu-id="ca4bb-126">Щелкните **База данных** > **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ca4bb-126">Click **Database** > **Create New**.</span></span> <span data-ttu-id="ca4bb-127">Настройте hello базы данных SQL, как показано.</span><span class="sxs-lookup"><span data-stu-id="ca4bb-127">Configure hello SQL Database as shown:</span></span>

    - <span data-ttu-id="ca4bb-128">В поле **Имя базы данных** введите имя базы данных.</span><span class="sxs-lookup"><span data-stu-id="ca4bb-128">In **Database Name**, type a database name.</span></span> 
    - <span data-ttu-id="ca4bb-129">В **расположение**, выберите hello местоположения hello план служб приложений.</span><span class="sxs-lookup"><span data-stu-id="ca4bb-129">In **Location**, choose hello same location as hello App Service plan.</span></span>
    - <span data-ttu-id="ca4bb-130">Щелкните **Ценовая категория**, а затем выберите **Mercury** или другую категорию, которая вам подходит. Щелкните **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="ca4bb-130">Click **Pricing tier**, then select **Mercury** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="ca4bb-131">Выберите **Условия** и щелкните **Приобрести**.</span><span class="sxs-lookup"><span data-stu-id="ca4bb-131">Click **Legal Terms** and click **Purchase**.</span></span>
    - <span data-ttu-id="ca4bb-132">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ca4bb-132">Click **OK**.</span></span>

9. <span data-ttu-id="ca4bb-133">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ca4bb-133">Click **Create**.</span></span>

    <span data-ttu-id="ca4bb-134">Теперь Azure создаст приложение WordPress на основе выбранной конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ca4bb-134">Azure now creates your WordPress app based on your configuration.</span></span> <span data-ttu-id="ca4bb-135">Должно появиться уведомление с текстом **Развертывание начато**.</span><span class="sxs-lookup"><span data-stu-id="ca4bb-135">You should see a **Deployment started...** notification.</span></span>

    ![Начато развертывание: первое приложение WordPress в службе приложений Azure](./media/app-service-web-get-started-php-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-wordpress-web-app"></a><span data-ttu-id="ca4bb-137">Запуск веб-приложения WordPress и управление им</span><span class="sxs-lookup"><span data-stu-id="ca4bb-137">Launch and manage your WordPress web app</span></span>

<span data-ttu-id="ca4bb-138">Когда Azure завершит развертывание приложения, появится еще одно уведомление.</span><span class="sxs-lookup"><span data-stu-id="ca4bb-138">When Azure completes app deployment you see another notification.</span></span>

![Успешное развертывание: первое приложение WordPress в службе приложений Azure](./media/app-service-web-get-started-php-portal/deployment-succeeded.png)

1. <span data-ttu-id="ca4bb-140">Щелкните уведомление hello.</span><span class="sxs-lookup"><span data-stu-id="ca4bb-140">Click hello notification.</span></span> <span data-ttu-id="ca4bb-141">Если вы пропустили всегда доступен, щелкнув hello уведомления колокольчика (![ниже уведомления - первый WordPress в службе приложений Azure](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span><span class="sxs-lookup"><span data-stu-id="ca4bb-141">If you missed it, you can always access it by clicking hello notification bell (![Notification bellow - first WordPress in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span></span>

    <span data-ttu-id="ca4bb-142">Теперь должна отображаться [колонка](../azure-resource-manager/resource-group-portal.md#manage-resources) управления веб-приложением. (*Колонка*: горизонтальная страница портала.)</span><span class="sxs-lookup"><span data-stu-id="ca4bb-142">You should now see your web app's management [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) (*blade*: a portal page that opens horizontally).</span></span>

3. <span data-ttu-id="ca4bb-143">В hello вверху страницы обзора hello щелкните **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="ca4bb-143">In hello top of hello Overview page, click **Browse**.</span></span>
   
    ![Обзор: первое приложение WordPress в службе приложений Azure](./media/app-service-web-get-started-php-portal/browse.png)

    <span data-ttu-id="ca4bb-145">Теперь вы видите hello WordPress **приветствия** страницы.</span><span class="sxs-lookup"><span data-stu-id="ca4bb-145">Now you see hello WordPress **Welcome** page.</span></span> <span data-ttu-id="ca4bb-146">Настройка установки WordPress hello и начать воспроизведение с ним!</span><span class="sxs-lookup"><span data-stu-id="ca4bb-146">Configure hello WordPress installation and start playing with it!</span></span>

    ![Конфигурация WordPress: первое приложение WordPress в службе приложений Azure](./media/app-service-web-get-started-php-portal/wordpress-config.png)
    
## <a name="next-steps"></a><span data-ttu-id="ca4bb-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ca4bb-148">Next steps</span></span>
* <span data-ttu-id="ca4bb-149">[Создавать, настраивать и развертывать приложения tooAzure Laravel web](app-service-web-php-get-started.md) -овладеть основными навыками работы hello необходимо toorun любой PHP веб-приложения в Azure, такие как:</span><span class="sxs-lookup"><span data-stu-id="ca4bb-149">[Create, configure, and deploy a Laravel web app tooAzure](app-service-web-php-get-started.md) - Learn hello basic skills you need toorun any PHP web app in Azure, such as:</span></span>

    * <span data-ttu-id="ca4bb-150">создание и настройка приложений в Azure с помощью PowerShell и Bash;</span><span class="sxs-lookup"><span data-stu-id="ca4bb-150">Create and configure apps in Azure from PowerShell/Bash.</span></span>
    * <span data-ttu-id="ca4bb-151">выбор версии PHP;</span><span class="sxs-lookup"><span data-stu-id="ca4bb-151">Set PHP version.</span></span>
    * <span data-ttu-id="ca4bb-152">Используйте начальный файл, который не находится в корневом каталоге приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ca4bb-152">Use a start file that is not in hello root application directory.</span></span>
    * <span data-ttu-id="ca4bb-153">Включение автоматизации Composer.</span><span class="sxs-lookup"><span data-stu-id="ca4bb-153">Enable Composer automation.</span></span>
    * <span data-ttu-id="ca4bb-154">доступ к переменным конкретной среды;</span><span class="sxs-lookup"><span data-stu-id="ca4bb-154">Access environment-specific variables.</span></span>
    * <span data-ttu-id="ca4bb-155">устранение распространенных ошибок.</span><span class="sxs-lookup"><span data-stu-id="ca4bb-155">Troubleshoot common errors.</span></span>

* <span data-ttu-id="ca4bb-156">[Развертывание tooAzure ваш код приложения службы](web-sites-deploy.md)-Узнайте, как toodeploy из FTP или источника контролировать репозиториев.</span><span class="sxs-lookup"><span data-stu-id="ca4bb-156">[Deploy your code tooAzure App Service](web-sites-deploy.md)- Learn how toodeploy from FTP or from source control repositories.</span></span>
* <span data-ttu-id="ca4bb-157">[Добавление функциональности tooyour первого веб-приложения](app-service-web-get-started-2.md) -занять вашего приложения Azure toohello Далее уровня.</span><span class="sxs-lookup"><span data-stu-id="ca4bb-157">[Add functionality tooyour first web app](app-service-web-get-started-2.md) - Take your Azure app toohello next level.</span></span> <span data-ttu-id="ca4bb-158">Проверяйте подлинность пользователей.</span><span class="sxs-lookup"><span data-stu-id="ca4bb-158">Authenticate your users.</span></span> <span data-ttu-id="ca4bb-159">Масштабируйте приложение в зависимости от потребностей.</span><span class="sxs-lookup"><span data-stu-id="ca4bb-159">Scale it based on demand.</span></span> <span data-ttu-id="ca4bb-160">Настраивайте оповещения производительности.</span><span class="sxs-lookup"><span data-stu-id="ca4bb-160">Set up some performance alerts.</span></span> <span data-ttu-id="ca4bb-161">И все это — с помощью нескольких действий.</span><span class="sxs-lookup"><span data-stu-id="ca4bb-161">All with a few clicks.</span></span>
