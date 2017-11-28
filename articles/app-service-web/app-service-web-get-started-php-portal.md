---
title: "Развертывание приложения WordPress на портале Azure за пять минут | Документация Майкрософт"
description: "Узнайте, как можно быстро запускать веб-приложения в службе приложений, развернув приложение WordPress. Кроме того, вы сможете быстро просмотреть результаты."
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
ms.openlocfilehash: ef3be9823384bd8dc978c86f5cfde00d1117c4a2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-a-wordpress-app-in-the-azure-portal-in-five-minutes"></a><span data-ttu-id="d1f44-104">Развертывание приложения WordPress на портале Azure за пять минут</span><span class="sxs-lookup"><span data-stu-id="d1f44-104">Deploy a WordPress app in the Azure portal in five minutes</span></span>

<span data-ttu-id="d1f44-105">В этом руководстве показано, как за считанные минуты развернуть свое первое веб-приложение [WordPress](https://wordpress.org/) в [службе приложений Azure](../app-service/app-service-value-prop-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="d1f44-105">This tutorial shows you how to deploy your first [WordPress](https://wordpress.org/) web app to [Azure App Service](../app-service/app-service-value-prop-what-is.md) in minutes.</span></span>

![Сайт WordPress](./media/app-service-web-get-started-php-portal/wpdashboard.png)

## <a name="prerequisites"></a><span data-ttu-id="d1f44-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d1f44-107">Prerequisites</span></span>
<span data-ttu-id="d1f44-108">Вам потребуется учетная запись Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d1f44-108">You need a Microsoft Azure account.</span></span> <span data-ttu-id="d1f44-109">Если у вас нет учетной записи, [подпишитесь на бесплатную пробную версию](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) или [активируйте преимущества для подписчиков Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="d1f44-109">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="d1f44-110">[Пробное использование службы приложений](https://azure.microsoft.com/try/app-service/) возможно даже без учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="d1f44-110">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="d1f44-111">Вы можете создать приложение начального уровня и экспериментировать с ним в течение часа. Для этого вам не нужно указывать данные кредитной карты или брать на себя какие-либо обязательства.</span><span class="sxs-lookup"><span data-stu-id="d1f44-111">Create a starter app and play with it for up to an hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="deploy-the-wordpress-app"></a><span data-ttu-id="d1f44-112">Развертывание приложения WordPress</span><span class="sxs-lookup"><span data-stu-id="d1f44-112">Deploy the WordPress app</span></span>
1. <span data-ttu-id="d1f44-113">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d1f44-113">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="d1f44-114">Откройте страницу [https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress).</span><span class="sxs-lookup"><span data-stu-id="d1f44-114">Open [https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress).</span></span>

    <span data-ttu-id="d1f44-115">Эта ссылка позволит сразу перейти на страницу настройки нового приложения WordPress на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="d1f44-115">This link is a shortcut to immediately configure a new WordPress app in the Azure portal.</span></span>

3. <span data-ttu-id="d1f44-116">В поле **Имя приложения** введите имя веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="d1f44-116">In **App name**, type a web app name.</span></span> <span data-ttu-id="d1f44-117">Если имя является уникальным в домене `azurewebsites.net`, то в поле появится зеленая галочка.</span><span class="sxs-lookup"><span data-stu-id="d1f44-117">You will see a green checkmark in the box if the name is unique in the `azurewebsites.net` domain.</span></span>
   
5. <span data-ttu-id="d1f44-118">В разделе **Группа ресурсов** щелкните **Создать**, чтобы создать [группу ресурсов](../azure-resource-manager/resource-group-overview.md), и введите ее имя.</span><span class="sxs-lookup"><span data-stu-id="d1f44-118">In **Resource Group**, click **Create new** to create a new [resource group](../azure-resource-manager/resource-group-overview.md), then give it a name.</span></span>

6. <span data-ttu-id="d1f44-119">Из списка **Поставщик базы данных** выберите **CleaDB**.</span><span class="sxs-lookup"><span data-stu-id="d1f44-119">In **Database Provider**, select **CleaDB**.</span></span>

7. <span data-ttu-id="d1f44-120">Щелкните **Расположение или план службы приложений** > **Создать**.</span><span class="sxs-lookup"><span data-stu-id="d1f44-120">Click **App Service plan/Location** > **Create New**.</span></span> <span data-ttu-id="d1f44-121">Настройте [план службы приложений](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md), как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="d1f44-121">Configure the [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) as shown:</span></span>

    - <span data-ttu-id="d1f44-122">В поле **План службы приложений** введите требуемое имя.</span><span class="sxs-lookup"><span data-stu-id="d1f44-122">In **App Service plan**, type the desired name.</span></span>
    - <span data-ttu-id="d1f44-123">Из списка **Расположение** выберите расположение для размещения плана.</span><span class="sxs-lookup"><span data-stu-id="d1f44-123">In **Location**, choose a location to host your plan.</span></span>
    - <span data-ttu-id="d1f44-124">Щелкните **Ценовая категория**, а затем выберите **F1 Free** или другую категорию, которая вам подходит. Щелкните **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="d1f44-124">Click **Pricing tier**, then select **F1 Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="d1f44-125">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d1f44-125">Click **OK**.</span></span>

8. <span data-ttu-id="d1f44-126">Щелкните **База данных** > **Создать**.</span><span class="sxs-lookup"><span data-stu-id="d1f44-126">Click **Database** > **Create New**.</span></span> <span data-ttu-id="d1f44-127">Настройте базу данных SQL, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="d1f44-127">Configure the SQL Database as shown:</span></span>

    - <span data-ttu-id="d1f44-128">В поле **Имя базы данных** введите имя базы данных.</span><span class="sxs-lookup"><span data-stu-id="d1f44-128">In **Database Name**, type a database name.</span></span> 
    - <span data-ttu-id="d1f44-129">Из списка **Расположение** выберите то же расположение, что и для плана службы приложений.</span><span class="sxs-lookup"><span data-stu-id="d1f44-129">In **Location**, choose the same location as the App Service plan.</span></span>
    - <span data-ttu-id="d1f44-130">Щелкните **Ценовая категория**, а затем выберите **Mercury** или другую категорию, которая вам подходит. Щелкните **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="d1f44-130">Click **Pricing tier**, then select **Mercury** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="d1f44-131">Выберите **Условия** и щелкните **Приобрести**.</span><span class="sxs-lookup"><span data-stu-id="d1f44-131">Click **Legal Terms** and click **Purchase**.</span></span>
    - <span data-ttu-id="d1f44-132">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d1f44-132">Click **OK**.</span></span>

9. <span data-ttu-id="d1f44-133">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="d1f44-133">Click **Create**.</span></span>

    <span data-ttu-id="d1f44-134">Теперь Azure создаст приложение WordPress на основе выбранной конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d1f44-134">Azure now creates your WordPress app based on your configuration.</span></span> <span data-ttu-id="d1f44-135">Должно появиться уведомление с текстом **Развертывание начато**.</span><span class="sxs-lookup"><span data-stu-id="d1f44-135">You should see a **Deployment started...** notification.</span></span>

    ![Начато развертывание: первое приложение WordPress в службе приложений Azure](./media/app-service-web-get-started-php-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-wordpress-web-app"></a><span data-ttu-id="d1f44-137">Запуск веб-приложения WordPress и управление им</span><span class="sxs-lookup"><span data-stu-id="d1f44-137">Launch and manage your WordPress web app</span></span>

<span data-ttu-id="d1f44-138">Когда Azure завершит развертывание приложения, появится еще одно уведомление.</span><span class="sxs-lookup"><span data-stu-id="d1f44-138">When Azure completes app deployment you see another notification.</span></span>

![Успешное развертывание: первое приложение WordPress в службе приложений Azure](./media/app-service-web-get-started-php-portal/deployment-succeeded.png)

1. <span data-ttu-id="d1f44-140">Щелкните это уведомление.</span><span class="sxs-lookup"><span data-stu-id="d1f44-140">Click the notification.</span></span> <span data-ttu-id="d1f44-141">Если вы пропустили его, то всегда сможете открыть это уведомление, щелкнув значок уведомления (звонок). (![Уведомление внизу: первое приложение WordPress в службе приложений Azure](./media/app-service-web-get-started-dotnet-portal/notification.png).)</span><span class="sxs-lookup"><span data-stu-id="d1f44-141">If you missed it, you can always access it by clicking the notification bell (![Notification bellow - first WordPress in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span></span>

    <span data-ttu-id="d1f44-142">Теперь должна отображаться [колонка](../azure-resource-manager/resource-group-portal.md#manage-resources) управления веб-приложением. (*Колонка*: горизонтальная страница портала.)</span><span class="sxs-lookup"><span data-stu-id="d1f44-142">You should now see your web app's management [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) (*blade*: a portal page that opens horizontally).</span></span>

3. <span data-ttu-id="d1f44-143">В верхней части страницы обзора щелкните **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="d1f44-143">In the top of the Overview page, click **Browse**.</span></span>
   
    ![Обзор: первое приложение WordPress в службе приложений Azure](./media/app-service-web-get-started-php-portal/browse.png)

    <span data-ttu-id="d1f44-145">Теперь вы видите страницу **приветствия** WordPress.</span><span class="sxs-lookup"><span data-stu-id="d1f44-145">Now you see the WordPress **Welcome** page.</span></span> <span data-ttu-id="d1f44-146">Настройте установленное приложение WordPress и поэкспериментируйте с ним.</span><span class="sxs-lookup"><span data-stu-id="d1f44-146">Configure the WordPress installation and start playing with it!</span></span>

    ![Конфигурация WordPress: первое приложение WordPress в службе приложений Azure](./media/app-service-web-get-started-php-portal/wordpress-config.png)
    
## <a name="next-steps"></a><span data-ttu-id="d1f44-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d1f44-148">Next steps</span></span>
* <span data-ttu-id="d1f44-149">[Создание, настройка и развертывание веб-приложения PHP в Azure](app-service-web-php-get-started.md). Изучите базовые навыки, необходимые для запуска любого веб-приложения PHP в Azure, в том числе:</span><span class="sxs-lookup"><span data-stu-id="d1f44-149">[Create, configure, and deploy a Laravel web app to Azure](app-service-web-php-get-started.md) - Learn the basic skills you need to run any PHP web app in Azure, such as:</span></span>

    * <span data-ttu-id="d1f44-150">создание и настройка приложений в Azure с помощью PowerShell и Bash;</span><span class="sxs-lookup"><span data-stu-id="d1f44-150">Create and configure apps in Azure from PowerShell/Bash.</span></span>
    * <span data-ttu-id="d1f44-151">выбор версии PHP;</span><span class="sxs-lookup"><span data-stu-id="d1f44-151">Set PHP version.</span></span>
    * <span data-ttu-id="d1f44-152">использование файла запуска, который находится не в корневом каталоге приложения;</span><span class="sxs-lookup"><span data-stu-id="d1f44-152">Use a start file that is not in the root application directory.</span></span>
    * <span data-ttu-id="d1f44-153">Включение автоматизации Composer.</span><span class="sxs-lookup"><span data-stu-id="d1f44-153">Enable Composer automation.</span></span>
    * <span data-ttu-id="d1f44-154">доступ к переменным конкретной среды;</span><span class="sxs-lookup"><span data-stu-id="d1f44-154">Access environment-specific variables.</span></span>
    * <span data-ttu-id="d1f44-155">устранение распространенных ошибок.</span><span class="sxs-lookup"><span data-stu-id="d1f44-155">Troubleshoot common errors.</span></span>

* <span data-ttu-id="d1f44-156">[Развертывание приложения в службе приложений Azure](web-sites-deploy.md). Узнайте, как развернуть свой код из FTP или репозиториев системы управления версиями.</span><span class="sxs-lookup"><span data-stu-id="d1f44-156">[Deploy your code to Azure App Service](web-sites-deploy.md)- Learn how to deploy from FTP or from source control repositories.</span></span>
* <span data-ttu-id="d1f44-157">[Добавление функциональных возможностей в первое веб-приложение](app-service-web-get-started-2.md). Выведите приложение Azure на следующий уровень.</span><span class="sxs-lookup"><span data-stu-id="d1f44-157">[Add functionality to your first web app](app-service-web-get-started-2.md) - Take your Azure app to the next level.</span></span> <span data-ttu-id="d1f44-158">Проверяйте подлинность пользователей.</span><span class="sxs-lookup"><span data-stu-id="d1f44-158">Authenticate your users.</span></span> <span data-ttu-id="d1f44-159">Масштабируйте приложение в зависимости от потребностей.</span><span class="sxs-lookup"><span data-stu-id="d1f44-159">Scale it based on demand.</span></span> <span data-ttu-id="d1f44-160">Настраивайте оповещения производительности.</span><span class="sxs-lookup"><span data-stu-id="d1f44-160">Set up some performance alerts.</span></span> <span data-ttu-id="d1f44-161">И все это — с помощью нескольких действий.</span><span class="sxs-lookup"><span data-stu-id="d1f44-161">All with a few clicks.</span></span>
