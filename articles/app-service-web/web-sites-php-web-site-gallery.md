---
title: "aaaCreate WordPress веб-приложения в службе приложений Azure | Документы Microsoft"
description: "Узнайте, как toocreate новый Azure веб-приложения для hello портал Azure с помощью блога WordPress."
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 193ae094-0d7c-4749-a09b-ff4b1240149e
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 3a95fcb6732c15a8200921ce474b6dde2298dec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-wordpress-web-app-in-azure-app-service"></a><span data-ttu-id="1c5b1-103">Создание веб-приложения WordPress в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="1c5b1-103">Create a WordPress web app in Azure App Service</span></span>
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

<span data-ttu-id="1c5b1-104">В этом учебнике показано, как toodeploy блог WordPress сайта из hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="1c5b1-104">This tutorial shows how toodeploy a WordPress blog site from hello Azure Marketplace.</span></span>

<span data-ttu-id="1c5b1-105">Закончено hello учебника вы получите свой собственный узел блога WordPress вверх и работающих в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="1c5b1-105">When you're done with hello tutorial you'll have your own WordPress blog site up and running in hello cloud.</span></span>

![Сайт WordPress](./media/web-sites-php-web-site-gallery/wpdashboard.png)

<span data-ttu-id="1c5b1-107">Вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="1c5b1-107">You'll learn:</span></span>

* <span data-ttu-id="1c5b1-108">Как toofind шаблоном приложений в Azure Marketplace hello.</span><span class="sxs-lookup"><span data-stu-id="1c5b1-108">How toofind an application template in hello Azure Marketplace.</span></span>
* <span data-ttu-id="1c5b1-109">Как toocreate веб-приложения в приложение Azure службы основан на шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="1c5b1-109">How toocreate a web app in Azure App Service that is based on hello template.</span></span>
* <span data-ttu-id="1c5b1-110">Как параметры службы приложений Azure tooconfigure для hello нового веб-приложения и базы данных.</span><span class="sxs-lookup"><span data-stu-id="1c5b1-110">How tooconfigure Azure App Service settings for hello new web app and database.</span></span>

<span data-ttu-id="1c5b1-111">Hello Azure Marketplace делает доступными широкий ряд популярных веб-приложений, разработанных корпорацией Майкрософт, сторонних компаний и инициативы по открытым исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="1c5b1-111">hello Azure Marketplace makes available a wide range of popular web apps developed by Microsoft, third party companies, and open source software initiatives.</span></span> <span data-ttu-id="1c5b1-112">веб-приложения Hello построены на широкий набор наиболее популярных платформ, таких как [PHP](/develop/nodejs/) в этом примере WordPress [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/), и [Python](/develop/python/), tooname несколько.</span><span class="sxs-lookup"><span data-stu-id="1c5b1-112">hello web apps are built on a wide range of popular frameworks, such as [PHP](/develop/nodejs/) in this WordPress example, [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/), and [Python](/develop/python/), tooname a few.</span></span> <span data-ttu-id="1c5b1-113">веб-приложение из Azure Marketplace hello только необходимого программного обеспечения является hello браузера, используемого для hello hello toocreate [портала Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1c5b1-113">toocreate a web app from hello Azure Marketplace hello only software you need is hello browser that you use for hello [Azure Portal](https://portal.azure.com/).</span></span> 

<span data-ttu-id="1c5b1-114">Hello сайта WordPress, развертываемые в этом учебнике используется MySQL для hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="1c5b1-114">hello WordPress site that you deploy in this tutorial uses MySQL for hello database.</span></span> <span data-ttu-id="1c5b1-115">При необходимости используйте tooinstead базы данных SQL для базы данных hello. в разделе [Nami проекта](http://projectnami.org/).</span><span class="sxs-lookup"><span data-stu-id="1c5b1-115">If you wish tooinstead use SQL Database for hello database, see [Project Nami](http://projectnami.org/).</span></span> <span data-ttu-id="1c5b1-116">**Проект Nami** также доступна через hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="1c5b1-116">**Project Nami** is also available through hello Marketplace.</span></span>

> [!NOTE]
> <span data-ttu-id="1c5b1-117">toocomplete этого учебника необходима учетная запись Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="1c5b1-117">toocomplete this tutorial, you need a Microsoft Azure account.</span></span> <span data-ttu-id="1c5b1-118">Если у вас нет учетной записи, можно [активировать преимущества для подписчиков Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) или [подписаться на бесплатную пробную версию](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="1c5b1-118">If you don't have an account, you can [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) or [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
> 
> <span data-ttu-id="1c5b1-119">Tooget к работе со службой приложения Azure, прежде чем выполнить вход для учетной записи Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/).</span><span class="sxs-lookup"><span data-stu-id="1c5b1-119">If you want tooget started with Azure App Service before you sign up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/).</span></span> <span data-ttu-id="1c5b1-120">Там вы сможете немедленно создать кратковременное начальное веб-приложение в службе приложений. Для этого не потребуется ни кредитная карта, ни какие-либо обязательства.</span><span class="sxs-lookup"><span data-stu-id="1c5b1-120">There, you can immediately create a short-lived starter web app in App Service—no credit card required, and no commitments.</span></span>
> 
> 

## <a name="select-wordpress-and-configure-for-azure-app-service"></a><span data-ttu-id="1c5b1-121">Выбор WordPress и настройка для службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="1c5b1-121">Select WordPress and configure for Azure App Service</span></span>
1. <span data-ttu-id="1c5b1-122">Войдите в toohello [портала Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1c5b1-122">Log in toohello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="1c5b1-123">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="1c5b1-123">Click **New**.</span></span>
   
    ![Создать][5]
3. <span data-ttu-id="1c5b1-125">Выполните поиск по запросу **WordPress**, а затем щелкните приложение **WordPress**.</span><span class="sxs-lookup"><span data-stu-id="1c5b1-125">Search for **WordPress**, and then click **WordPress**.</span></span> <span data-ttu-id="1c5b1-126">При желании toouse базы данных SQL вместо MySQL поиск **Nami проекта**.</span><span class="sxs-lookup"><span data-stu-id="1c5b1-126">If you wish toouse SQL Database instead of MySQL, search for **Project Nami**.</span></span>
   
    ![WordPress из списка][7]
4. <span data-ttu-id="1c5b1-128">Прочитав описание hello приложение hello WordPress, нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="1c5b1-128">After reading hello description of hello WordPress app, click **Create**.</span></span>
   
    ![Создание](./media/web-sites-php-web-site-gallery/create.png)
5. <span data-ttu-id="1c5b1-130">Введите имя для веб-приложения hello в hello **веб-приложение** поле.</span><span class="sxs-lookup"><span data-stu-id="1c5b1-130">Enter a name for hello web app in hello **Web app** box.</span></span>
   
    <span data-ttu-id="1c5b1-131">Это имя должно быть уникальным в домене azurewebsites.net hello, так как hello URL-адрес веб-приложения hello {имя}. azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="1c5b1-131">This name must be unique in hello azurewebsites.net domain because hello URL of hello web app will be {name}.azurewebsites.net.</span></span> <span data-ttu-id="1c5b1-132">Если вы вводите имя hello не является уникальным, в текстовом поле hello отображается красный восклицательный знак.</span><span class="sxs-lookup"><span data-stu-id="1c5b1-132">If hello name you enter isn't unique, a red exclamation mark appears in hello text box.</span></span>
6. <span data-ttu-id="1c5b1-133">Если у вас несколько подписок, выберите hello один требуется toouse.</span><span class="sxs-lookup"><span data-stu-id="1c5b1-133">If you have more than one subscription, choose hello one you want toouse.</span></span> 
7. <span data-ttu-id="1c5b1-134">Выберите **группу ресурсов** или создайте новую.</span><span class="sxs-lookup"><span data-stu-id="1c5b1-134">Select a **Resource Group** or create a new one.</span></span>
   
    <span data-ttu-id="1c5b1-135">Дополнительные сведения о группах ресурсов см. в статье [Общие сведения об Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1c5b1-135">For more information about resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
8. <span data-ttu-id="1c5b1-136">Выберите или создайте **план службы приложений или расположение** .</span><span class="sxs-lookup"><span data-stu-id="1c5b1-136">Select an **App Service plan/Location** or create a new one.</span></span>
   
    <span data-ttu-id="1c5b1-137">Дополнительные сведения о планах службы приложений см. в [подробном обзоре планов службы приложений Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1c5b1-137">For more information about App Service plans, see [Azure App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)</span></span>    
9. <span data-ttu-id="1c5b1-138">Нажмите кнопку **базы данных**, а затем в hello **новую базу данных MySQL** колонке предоставляют hello необходимые значения для настройки базы данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="1c5b1-138">Click **Database**, and then in hello **New MySQL Database** blade provide hello required values for configuring your MySQL database.</span></span>
   
    <span data-ttu-id="1c5b1-139">а.</span><span class="sxs-lookup"><span data-stu-id="1c5b1-139">a.</span></span> <span data-ttu-id="1c5b1-140">Введите новое имя или оставьте имя по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="1c5b1-140">Enter a new name or leave hello default name.</span></span>
   
    <span data-ttu-id="1c5b1-141">b.</span><span class="sxs-lookup"><span data-stu-id="1c5b1-141">b.</span></span> <span data-ttu-id="1c5b1-142">Оставьте hello **тип базы данных** значение слишком**Shared**.</span><span class="sxs-lookup"><span data-stu-id="1c5b1-142">Leave hello **Database Type** set too**Shared**.</span></span>
   
    <span data-ttu-id="1c5b1-143">c.</span><span class="sxs-lookup"><span data-stu-id="1c5b1-143">c.</span></span> <span data-ttu-id="1c5b1-144">Выберите местоположения, как и в случае hello, с которой вы выбрали для веб-приложения hello приветствия.</span><span class="sxs-lookup"><span data-stu-id="1c5b1-144">Choose hello same location as hello one you chose for hello web app.</span></span>
   
    <span data-ttu-id="1c5b1-145">d.</span><span class="sxs-lookup"><span data-stu-id="1c5b1-145">d.</span></span> <span data-ttu-id="1c5b1-146">Выберите ценовую категорию.</span><span class="sxs-lookup"><span data-stu-id="1c5b1-146">Choose a pricing tier.</span></span> <span data-ttu-id="1c5b1-147">Для этого учебника подходит «Меркурий» (бесплатно с минимумом разрешенных подключений и места на диске).</span><span class="sxs-lookup"><span data-stu-id="1c5b1-147">Mercury (free with minimal allowed connections and disk space) is fine for this tutorial.</span></span>
10. <span data-ttu-id="1c5b1-148">В hello **новую базу данных MySQL** колонка, щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="1c5b1-148">In hello **New MySQL Database** blade, click **OK**.</span></span> 
11. <span data-ttu-id="1c5b1-149">В hello **WordPress** колонки, примите условия hello и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="1c5b1-149">In hello **WordPress** blade, accept hello legal terms, and then click **Create**.</span></span> 
    
     ![Настройка веб-приложения](./media/web-sites-php-web-site-gallery/configure.png)
    
     <span data-ttu-id="1c5b1-151">Служба приложений Azure создает веб-приложения hello, обычно меньше, чем через минуту.</span><span class="sxs-lookup"><span data-stu-id="1c5b1-151">Azure App Service creates hello web app, typically in less than a minute.</span></span> <span data-ttu-id="1c5b1-152">Можно отслеживать ход выполнения hello, щелкнув значок колокольчика hello hello верхней части страницы портала hello.</span><span class="sxs-lookup"><span data-stu-id="1c5b1-152">You can watch hello progress by clicking hello bell icon at hello top of hello portal page.</span></span>
    
     ![Индикатор хода выполнения](./media/web-sites-php-web-site-gallery/progress.png)

## <a name="launch-and-manage-your-wordpress-web-app"></a><span data-ttu-id="1c5b1-154">Запуск веб-приложения WordPress и управление им</span><span class="sxs-lookup"><span data-stu-id="1c5b1-154">Launch and manage your WordPress web app</span></span>
1. <span data-ttu-id="1c5b1-155">После завершения создания приложения hello web перейдите в группе ресурсов Azure Portal toohello hello в которой вы создали приложение hello, и вы увидите hello веб-приложения и базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="1c5b1-155">When hello web app creation is finished, navigate in hello Azure Portal toohello resource group in which you created hello application, and you can see hello web app and hello database.</span></span>
   
    <span data-ttu-id="1c5b1-156">Hello дополнительных ресурсов с использованием значок лампочки hello — [Application Insights](/services/application-insights/), который предоставляет службы мониторинга для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="1c5b1-156">hello extra resource with hello light bulb icon is [Application Insights](/services/application-insights/), which provides monitoring services for your web app.</span></span>
2. <span data-ttu-id="1c5b1-157">В hello **группы ресурсов** колонка, щелкните строку приложения hello web.</span><span class="sxs-lookup"><span data-stu-id="1c5b1-157">In hello **Resource group** blade, click hello web app line.</span></span>
   
    ![Настройка веб-приложения](./media/web-sites-php-web-site-gallery/resourcegroup.png)
3. <span data-ttu-id="1c5b1-159">В колонке приложения hello Web щелкните **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="1c5b1-159">In hello Web app blade, click **Browse**.</span></span>
   
    ![URL-адрес сайта][browse]
4. <span data-ttu-id="1c5b1-161">В hello WordPress **приветствия** введите hello данные конфигурации, необходимые WordPress и нажмите кнопку **Установка WordPress**.</span><span class="sxs-lookup"><span data-stu-id="1c5b1-161">In hello WordPress **Welcome** page, enter hello configuration information required by WordPress, and then click **Install WordPress**.</span></span>
   
    ![Настройка WordPress](./media/web-sites-php-web-site-gallery/wpconfigure.png)
5. <span data-ttu-id="1c5b1-163">Вход с использованием учетных данных hello, вы создали на hello **приветствия** страницы.</span><span class="sxs-lookup"><span data-stu-id="1c5b1-163">Log in using hello credentials you created on hello **Welcome** page.</span></span>  
6. <span data-ttu-id="1c5b1-164">Откроется страница панели мониторинга вашего сайта.</span><span class="sxs-lookup"><span data-stu-id="1c5b1-164">Your site Dashboard page opens.</span></span>    
   
    ![Сайт WordPress](./media/web-sites-php-web-site-gallery/wpdashboard.png)

## <a name="next-steps"></a><span data-ttu-id="1c5b1-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1c5b1-166">Next steps</span></span>
<span data-ttu-id="1c5b1-167">Вы знаете, как toocreate и развертывать веб-приложения PHP из галереи hello.</span><span class="sxs-lookup"><span data-stu-id="1c5b1-167">You've seen how toocreate and deploy a PHP web app from hello gallery.</span></span> <span data-ttu-id="1c5b1-168">Дополнительные сведения об использовании PHP в Azure см. в разделе hello [Центр разработчика PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="1c5b1-168">For more information about using PHP in Azure, see hello [PHP Developer Center](/develop/php/).</span></span>

<span data-ttu-id="1c5b1-169">Дополнительные сведения о том, как toowork для приложения службы веб-приложений, см. ссылки hello hello левая сторона страницы приветствия (для широкого обозревателя windows) или в начале hello страницы приветствия (для обычных обозревателя windows).</span><span class="sxs-lookup"><span data-stu-id="1c5b1-169">For more information about how toowork with App Service Web Apps, see hello links on hello left side of hello page (for wide browser windows) or at hello top of hello page (for narrow browser windows).</span></span> 

## <a name="whats-changed"></a><span data-ttu-id="1c5b1-170">Изменения</span><span class="sxs-lookup"><span data-stu-id="1c5b1-170">What's changed</span></span>
* <span data-ttu-id="1c5b1-171">Руководство по toohello изменений из tooApp веб-сайтов службы, см. [службе приложений Azure и ее влияние на существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="1c5b1-171">For a guide toohello change from Websites tooApp Service, see [Azure App Service and its impact on existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

[5]: ./media/web-sites-php-web-site-gallery/startmarketplace.png
[7]: ./media/web-sites-php-web-site-gallery/search-web-app.png
[browse]: ./media/web-sites-php-web-site-gallery/browse-web.png
