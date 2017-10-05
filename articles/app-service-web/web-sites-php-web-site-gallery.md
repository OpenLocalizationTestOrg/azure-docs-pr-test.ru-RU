---
title: "Создание веб-приложения WordPress в службе приложений Azure | Документация Майкрософт"
description: "Узнайте, как создать новое веб-приложение Azure для блога WordPress с помощью портала Azure."
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
ms.openlocfilehash: 460afdabed947fb4018a9ea8a7a5bc7dc5bc89c7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-wordpress-web-app-in-azure-app-service"></a><span data-ttu-id="0063c-103">Создание веб-приложения WordPress в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="0063c-103">Create a WordPress web app in Azure App Service</span></span>
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

<span data-ttu-id="0063c-104">В этом руководстве объясняется, как развернуть сайт блога WordPress в Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="0063c-104">This tutorial shows how to deploy a WordPress blog site from the Azure Marketplace.</span></span>

<span data-ttu-id="0063c-105">После завершения работы с учебником ваш собственный блог WordPress будет работать в облаке.</span><span class="sxs-lookup"><span data-stu-id="0063c-105">When you're done with the tutorial you'll have your own WordPress blog site up and running in the cloud.</span></span>

![Сайт WordPress](./media/web-sites-php-web-site-gallery/wpdashboard.png)

<span data-ttu-id="0063c-107">Вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="0063c-107">You'll learn:</span></span>

* <span data-ttu-id="0063c-108">Как найти шаблон приложения в магазине Azure.</span><span class="sxs-lookup"><span data-stu-id="0063c-108">How to find an application template in the Azure Marketplace.</span></span>
* <span data-ttu-id="0063c-109">Как создать веб-приложение в службе приложений Azure на основе шаблона.</span><span class="sxs-lookup"><span data-stu-id="0063c-109">How to create a web app in Azure App Service that is based on the template.</span></span>
* <span data-ttu-id="0063c-110">Как настроить параметры службы приложений Azure для нового веб-приложения и базы данных.</span><span class="sxs-lookup"><span data-stu-id="0063c-110">How to configure Azure App Service settings for the new web app and database.</span></span>

<span data-ttu-id="0063c-111">Azure Marketplace предоставляет широкий спектр популярных веб-приложений, разработанных нами, сторонними компаниями и группами разработки программного обеспечения с открытым исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="0063c-111">The Azure Marketplace makes available a wide range of popular web apps developed by Microsoft, third party companies, and open source software initiatives.</span></span> <span data-ttu-id="0063c-112">Веб-приложения создаются на основе разных популярных платформ, включая [PHP](/develop/nodejs/) (в нашем примере с WordPress), [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/), [Python](/develop/python/) и др.</span><span class="sxs-lookup"><span data-stu-id="0063c-112">The web apps are built on a wide range of popular frameworks, such as [PHP](/develop/nodejs/) in this WordPress example, [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/), and [Python](/develop/python/), to name a few.</span></span> <span data-ttu-id="0063c-113">Единственное программное обеспечение, которое понадобится для создания веб-приложения из магазина Azure, — это браузер, который вы будете использовать для входа на [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0063c-113">To create a web app from the Azure Marketplace the only software you need is the browser that you use for the [Azure Portal](https://portal.azure.com/).</span></span> 

<span data-ttu-id="0063c-114">Сайт WordPress, развертываемый в этом руководстве, использует MySQL для базы данных.</span><span class="sxs-lookup"><span data-stu-id="0063c-114">The WordPress site that you deploy in this tutorial uses MySQL for the database.</span></span> <span data-ttu-id="0063c-115">Если вы хотите использовать в качестве базы данных базу данных SQL, см. сайт [проекта Nami](http://projectnami.org/).</span><span class="sxs-lookup"><span data-stu-id="0063c-115">If you wish to instead use SQL Database for the database, see [Project Nami](http://projectnami.org/).</span></span> <span data-ttu-id="0063c-116">**Проект Nami** также доступен в Marketplace.</span><span class="sxs-lookup"><span data-stu-id="0063c-116">**Project Nami** is also available through the Marketplace.</span></span>

> [!NOTE]
> <span data-ttu-id="0063c-117">Для работы с этим учебником необходимо использовать учетную запись Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="0063c-117">To complete this tutorial, you need a Microsoft Azure account.</span></span> <span data-ttu-id="0063c-118">Если у вас нет учетной записи, можно [активировать преимущества для подписчиков Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) или [подписаться на бесплатную пробную версию](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="0063c-118">If you don't have an account, you can [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) or [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
> 
> <span data-ttu-id="0063c-119">Чтобы приступить к работе со службой приложений Azure до регистрации и получения учетной записи Azure, перейдите на страницу [пробного использования службы приложений](https://azure.microsoft.com/try/app-service/).</span><span class="sxs-lookup"><span data-stu-id="0063c-119">If you want to get started with Azure App Service before you sign up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/).</span></span> <span data-ttu-id="0063c-120">Там вы сможете немедленно создать кратковременное начальное веб-приложение в службе приложений. Для этого не потребуется ни кредитная карта, ни какие-либо обязательства.</span><span class="sxs-lookup"><span data-stu-id="0063c-120">There, you can immediately create a short-lived starter web app in App Service—no credit card required, and no commitments.</span></span>
> 
> 

## <a name="select-wordpress-and-configure-for-azure-app-service"></a><span data-ttu-id="0063c-121">Выбор WordPress и настройка для службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="0063c-121">Select WordPress and configure for Azure App Service</span></span>
1. <span data-ttu-id="0063c-122">Войдите на [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0063c-122">Log in to the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="0063c-123">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="0063c-123">Click **New**.</span></span>
   
    ![Создать][5]
3. <span data-ttu-id="0063c-125">Выполните поиск по запросу **WordPress**, а затем щелкните приложение **WordPress**.</span><span class="sxs-lookup"><span data-stu-id="0063c-125">Search for **WordPress**, and then click **WordPress**.</span></span> <span data-ttu-id="0063c-126">Если вы хотите использовать базу данных SQL вместо MySQL, выполните поиск по запросу **Project Nami**.</span><span class="sxs-lookup"><span data-stu-id="0063c-126">If you wish to use SQL Database instead of MySQL, search for **Project Nami**.</span></span>
   
    ![WordPress из списка][7]
4. <span data-ttu-id="0063c-128">После прочтения описания приложения WordPress нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="0063c-128">After reading the description of the WordPress app, click **Create**.</span></span>
   
    ![Создать](./media/web-sites-php-web-site-gallery/create.png)
5. <span data-ttu-id="0063c-130">Введите имя для веб-приложения в поле **Веб-приложение** .</span><span class="sxs-lookup"><span data-stu-id="0063c-130">Enter a name for the web app in the **Web app** box.</span></span>
   
    <span data-ttu-id="0063c-131">Это имя должно быть уникальным в домене azurewebsites.net, так как URL-адрес веб-приложения будет иметь такой формат: {имя}. azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="0063c-131">This name must be unique in the azurewebsites.net domain because the URL of the web app will be {name}.azurewebsites.net.</span></span> <span data-ttu-id="0063c-132">Если введенное имя не является уникальным, в текстовом поле отображается красный восклицательный знак.</span><span class="sxs-lookup"><span data-stu-id="0063c-132">If the name you enter isn't unique, a red exclamation mark appears in the text box.</span></span>
6. <span data-ttu-id="0063c-133">Если у вас есть несколько подписок, выберите ту, которую будете использовать.</span><span class="sxs-lookup"><span data-stu-id="0063c-133">If you have more than one subscription, choose the one you want to use.</span></span> 
7. <span data-ttu-id="0063c-134">Выберите **группу ресурсов** или создайте новую.</span><span class="sxs-lookup"><span data-stu-id="0063c-134">Select a **Resource Group** or create a new one.</span></span>
   
    <span data-ttu-id="0063c-135">Дополнительные сведения о группах ресурсов см. в статье [Общие сведения об Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0063c-135">For more information about resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
8. <span data-ttu-id="0063c-136">Выберите или создайте **план службы приложений или расположение** .</span><span class="sxs-lookup"><span data-stu-id="0063c-136">Select an **App Service plan/Location** or create a new one.</span></span>
   
    <span data-ttu-id="0063c-137">Дополнительные сведения о планах службы приложений см. в [подробном обзоре планов службы приложений Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0063c-137">For more information about App Service plans, see [Azure App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)</span></span>    
9. <span data-ttu-id="0063c-138">Щелкните элемент **База данных** и укажите в колонке **Новая база данных MySQL** значения для настройки базы данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="0063c-138">Click **Database**, and then in the **New MySQL Database** blade provide the required values for configuring your MySQL database.</span></span>
   
    <span data-ttu-id="0063c-139">а.</span><span class="sxs-lookup"><span data-stu-id="0063c-139">a.</span></span> <span data-ttu-id="0063c-140">Введите новое имя или оставьте имя по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="0063c-140">Enter a new name or leave the default name.</span></span>
   
    <span data-ttu-id="0063c-141">b.</span><span class="sxs-lookup"><span data-stu-id="0063c-141">b.</span></span> <span data-ttu-id="0063c-142">Оставьте в поле **Тип базы данных** значение **Общая**.</span><span class="sxs-lookup"><span data-stu-id="0063c-142">Leave the **Database Type** set to **Shared**.</span></span>
   
    <span data-ttu-id="0063c-143">c.</span><span class="sxs-lookup"><span data-stu-id="0063c-143">c.</span></span> <span data-ttu-id="0063c-144">Выберите то же расположение, которое выбрано для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="0063c-144">Choose the same location as the one you chose for the web app.</span></span>
   
    <span data-ttu-id="0063c-145">г)</span><span class="sxs-lookup"><span data-stu-id="0063c-145">d.</span></span> <span data-ttu-id="0063c-146">Выберите ценовую категорию.</span><span class="sxs-lookup"><span data-stu-id="0063c-146">Choose a pricing tier.</span></span> <span data-ttu-id="0063c-147">Для этого учебника подходит «Меркурий» (бесплатно с минимумом разрешенных подключений и места на диске).</span><span class="sxs-lookup"><span data-stu-id="0063c-147">Mercury (free with minimal allowed connections and disk space) is fine for this tutorial.</span></span>
10. <span data-ttu-id="0063c-148">В колонке **Новая база данных MySQL** нажмите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="0063c-148">In the **New MySQL Database** blade, click **OK**.</span></span> 
11. <span data-ttu-id="0063c-149">В колонке **WordPress** примите условия использования и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="0063c-149">In the **WordPress** blade, accept the legal terms, and then click **Create**.</span></span> 
    
     ![Настройка веб-приложения](./media/web-sites-php-web-site-gallery/configure.png)
    
     <span data-ttu-id="0063c-151">Служба приложений Azure создаст веб-приложение (обычно это занимает меньше минуты).</span><span class="sxs-lookup"><span data-stu-id="0063c-151">Azure App Service creates the web app, typically in less than a minute.</span></span> <span data-ttu-id="0063c-152">Можно отслеживать ход выполнения, щелкнув значок колокольчика в верхней части страницы портала.</span><span class="sxs-lookup"><span data-stu-id="0063c-152">You can watch the progress by clicking the bell icon at the top of the portal page.</span></span>
    
     ![Индикатор хода выполнения](./media/web-sites-php-web-site-gallery/progress.png)

## <a name="launch-and-manage-your-wordpress-web-app"></a><span data-ttu-id="0063c-154">Запуск веб-приложения WordPress и управление им</span><span class="sxs-lookup"><span data-stu-id="0063c-154">Launch and manage your WordPress web app</span></span>
1. <span data-ttu-id="0063c-155">После завершения создания веб-приложения перейдите на портале Azure к группе ресурсов, в которой было создано приложение, и вы увидите веб-приложение и базу данных.</span><span class="sxs-lookup"><span data-stu-id="0063c-155">When the web app creation is finished, navigate in the Azure Portal to the resource group in which you created the application, and you can see the web app and the database.</span></span>
   
    <span data-ttu-id="0063c-156">Дополнительный ресурс со значком лампочки — надстройка [Application Insights](/services/application-insights/), которая предоставляет службы мониторинга для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="0063c-156">The extra resource with the light bulb icon is [Application Insights](/services/application-insights/), which provides monitoring services for your web app.</span></span>
2. <span data-ttu-id="0063c-157">В колонке **Группа ресурсов** щелкните строку веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="0063c-157">In the **Resource group** blade, click the web app line.</span></span>
   
    ![Настройка веб-приложения](./media/web-sites-php-web-site-gallery/resourcegroup.png)
3. <span data-ttu-id="0063c-159">В колонке веб-приложения нажмите кнопку **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="0063c-159">In the Web app blade, click **Browse**.</span></span>
   
    ![URL-адрес сайта][browse]
4. <span data-ttu-id="0063c-161">На странице **приветствия** WordPress введите параметры, которые требуются WordPress, после чего нажмите кнопку **Установить WordPress**.</span><span class="sxs-lookup"><span data-stu-id="0063c-161">In the WordPress **Welcome** page, enter the configuration information required by WordPress, and then click **Install WordPress**.</span></span>
   
    ![Настройка WordPress](./media/web-sites-php-web-site-gallery/wpconfigure.png)
5. <span data-ttu-id="0063c-163">Войдите, используя учетные данные, созданные на странице **приветствия** .</span><span class="sxs-lookup"><span data-stu-id="0063c-163">Log in using the credentials you created on the **Welcome** page.</span></span>  
6. <span data-ttu-id="0063c-164">Откроется страница панели мониторинга вашего сайта.</span><span class="sxs-lookup"><span data-stu-id="0063c-164">Your site Dashboard page opens.</span></span>    
   
    ![Сайт WordPress](./media/web-sites-php-web-site-gallery/wpdashboard.png)

## <a name="next-steps"></a><span data-ttu-id="0063c-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0063c-166">Next steps</span></span>
<span data-ttu-id="0063c-167">Вы уже знаете, как создать и развернуть веб-приложение PHP из коллекции.</span><span class="sxs-lookup"><span data-stu-id="0063c-167">You've seen how to create and deploy a PHP web app from the gallery.</span></span> <span data-ttu-id="0063c-168">Дополнительные сведения об использовании PHP в Azure см. в [центре разработчиков PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="0063c-168">For more information about using PHP in Azure, see the [PHP Developer Center](/develop/php/).</span></span>

<span data-ttu-id="0063c-169">Дополнительные сведения о работе с веб-приложениями службы приложений см. по ссылкам в левой части страницы (для широких окон браузера) или в верхней части страницы (для узких окон браузера).</span><span class="sxs-lookup"><span data-stu-id="0063c-169">For more information about how to work with App Service Web Apps, see the links on the left side of the page (for wide browser windows) or at the top of the page (for narrow browser windows).</span></span> 

## <a name="whats-changed"></a><span data-ttu-id="0063c-170">Изменения</span><span class="sxs-lookup"><span data-stu-id="0063c-170">What's changed</span></span>
* <span data-ttu-id="0063c-171">Руководство по переходу от веб-сайтов к службе приложений см. в статье [Служба приложений Azure и существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="0063c-171">For a guide to the change from Websites to App Service, see [Azure App Service and its impact on existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

[5]: ./media/web-sites-php-web-site-gallery/startmarketplace.png
[7]: ./media/web-sites-php-web-site-gallery/search-web-app.png
[browse]: ./media/web-sites-php-web-site-gallery/browse-web.png
