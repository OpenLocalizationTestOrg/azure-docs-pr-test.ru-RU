---
title: "Приобретение имени личного домена для веб-приложений Azure"
description: "Информация о приобретении личного доменного имени для веб-приложения в службе приложение Azure."
services: app-service\web
documentationcenter: 
author: cephalin
manager: cfowler
editor: 
ms.assetid: 70fb0e6e-8727-4cca-ba82-98a4d21586ff
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: cephalin
ms.openlocfilehash: 3cb22b935624041ab51e64028a1b668fd694f9b5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="buy-a-custom-domain-name-for-azure-web-apps"></a><span data-ttu-id="be9ed-103">Приобретение имени личного домена для веб-приложений Azure</span><span class="sxs-lookup"><span data-stu-id="be9ed-103">Buy a custom domain name for Azure Web Apps</span></span>

<span data-ttu-id="be9ed-104">Домены службы приложений (предварительная версия) — это домены верхнего уровня, которые управляются непосредственно в Azure.</span><span class="sxs-lookup"><span data-stu-id="be9ed-104">App Service domains (preview) are top-level domains that are managed directly in Azure.</span></span> <span data-ttu-id="be9ed-105">Они упрощают управление личными доменами для [веб-приложений Azure](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="be9ed-105">They make it easy to manage custom domains for [Azure Web Apps](app-service-web-overview.md).</span></span> <span data-ttu-id="be9ed-106">В этом руководстве показано, как приобрести домен службы веб-приложений и назначить DNS-имена веб-приложениям Azure.</span><span class="sxs-lookup"><span data-stu-id="be9ed-106">This tutorial shows you how to buy an App Service domain and assign DNS names to Azure Web Apps.</span></span>

<span data-ttu-id="be9ed-107">Эта статья предназначена для службы приложений Azure ("Веб-приложения", "Приложения API", "Мобильные приложения", Logic Apps).</span><span class="sxs-lookup"><span data-stu-id="be9ed-107">This article is for Azure App Service (Web Apps, API Apps, Mobile Apps, Logic Apps).</span></span> <span data-ttu-id="be9ed-108">Сведения о виртуальной машине Azure или службе хранилища Azure см. в статье [Assign App Service domain to Azure VM or Azure Storage](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/) (Назначение домена службы приложений виртуальной машине Azure или службе хранилища Azure).</span><span class="sxs-lookup"><span data-stu-id="be9ed-108">For Azure VM or Azure Storage, see [Assign App Service domain to Azure VM or Azure Storage](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/).</span></span> <span data-ttu-id="be9ed-109">Сведения об облачных службах см. в статье [Настройка пользовательского доменного имени для облачной службы Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="be9ed-109">For Cloud Services, see [Configuring a custom domain name for an Azure cloud service](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="be9ed-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="be9ed-110">Prerequisites</span></span>

<span data-ttu-id="be9ed-111">Для работы с этим руководством:</span><span class="sxs-lookup"><span data-stu-id="be9ed-111">To complete this tutorial:</span></span>

* <span data-ttu-id="be9ed-112">[Создайте приложение службы приложений](/azure/app-service/) или используйте приложение, созданное для работы с другим руководством.</span><span class="sxs-lookup"><span data-stu-id="be9ed-112">[Create an App Service app](/azure/app-service/), or use an app that you created for another tutorial.</span></span>

## <a name="prepare-the-app"></a><span data-ttu-id="be9ed-113">Подготовка приложения</span><span class="sxs-lookup"><span data-stu-id="be9ed-113">Prepare the app</span></span>

<span data-ttu-id="be9ed-114">Чтобы использовать пользовательское DNS-имя в веб-приложениях Azure, его уровень [плана службы приложений](https://azure.microsoft.com/pricing/details/app-service/) должен быть платным (**Общий**, **Базовый**, **Стандартный** или **Премиум**).</span><span class="sxs-lookup"><span data-stu-id="be9ed-114">To use custom domains in Azure Web Apps, your web app's [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be a paid tier (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> <span data-ttu-id="be9ed-115">На этом шаге следует убедиться, что веб-приложение находится в поддерживаемой ценовой категории.</span><span class="sxs-lookup"><span data-stu-id="be9ed-115">In this step, you make sure that the web app is in the supported pricing tier.</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="be9ed-116">Вход в Azure</span><span class="sxs-lookup"><span data-stu-id="be9ed-116">Sign in to Azure</span></span>

<span data-ttu-id="be9ed-117">Откройте [портал Azure](https://portal.azure.com) и войдите в систему, используя свою учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="be9ed-117">Open the [Azure portal](https://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="navigate-to-the-app-in-the-azure-portal"></a><span data-ttu-id="be9ed-118">Переход к приложению на портале Azure</span><span class="sxs-lookup"><span data-stu-id="be9ed-118">Navigate to the app in the Azure portal</span></span>

<span data-ttu-id="be9ed-119">В меню слева выберите **Службы приложений**, а затем щелкните имя своего приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="be9ed-119">From the left menu, select **App Services**, and then select the name of the app.</span></span>

![Переход к приложению Azure на портале](./media/app-service-web-tutorial-custom-domain/select-app.png)

<span data-ttu-id="be9ed-121">Откроется страница управления приложением службы приложений.</span><span class="sxs-lookup"><span data-stu-id="be9ed-121">You see the management page of the App Service app.</span></span>  

### <a name="check-the-pricing-tier"></a><span data-ttu-id="be9ed-122">Проверка ценовой категории</span><span class="sxs-lookup"><span data-stu-id="be9ed-122">Check the pricing tier</span></span>

<span data-ttu-id="be9ed-123">В левой области навигации страницы приложения перейдите к разделу **Параметры** и выберите **Увеличить масштаб (план службы приложений)**.</span><span class="sxs-lookup"><span data-stu-id="be9ed-123">In the left navigation of the app page, scroll to the **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Меню увеличения масштаба](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

<span data-ttu-id="be9ed-125">Текущий уровень приложения выделен синей рамкой.</span><span class="sxs-lookup"><span data-stu-id="be9ed-125">The app's current tier is highlighted by a blue border.</span></span> <span data-ttu-id="be9ed-126">Убедитесь, что приложение не находится в ценовой категории **Бесплатный**.</span><span class="sxs-lookup"><span data-stu-id="be9ed-126">Check to make sure that the app is not in the **Free** tier.</span></span> <span data-ttu-id="be9ed-127">Использование личного домена DNS не поддерживается на уровне **Бесплатный**.</span><span class="sxs-lookup"><span data-stu-id="be9ed-127">Custom DNS is not supported in the **Free** tier.</span></span> 

![Проверка ценовой категории](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

<span data-ttu-id="be9ed-129">Если план службы приложений не **бесплатный**, закройте страницу **Выбор ценовой категории** и перейдите к разделу [Приобретение домена](#buy-the-domain).</span><span class="sxs-lookup"><span data-stu-id="be9ed-129">If the App Service plan is not **Free**, close the **Choose your pricing tier** page and skip to [Buy the domain](#buy-the-domain).</span></span>

### <a name="scale-up-the-app-service-plan"></a><span data-ttu-id="be9ed-130">Изменение уровня плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="be9ed-130">Scale up the App Service plan</span></span>

<span data-ttu-id="be9ed-131">Выберите любой из платных уровней (**Общий**, **Базовый**, **Стандартный** или **Премиум**).</span><span class="sxs-lookup"><span data-stu-id="be9ed-131">Select any of the non-free tiers (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> 

<span data-ttu-id="be9ed-132">Нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="be9ed-132">Click **Select**.</span></span>

![Проверка ценовой категории](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

<span data-ttu-id="be9ed-134">Если вы увидите уведомление ниже, значит уровень плана службы приложений изменен.</span><span class="sxs-lookup"><span data-stu-id="be9ed-134">When you see the following notification, the scale operation is complete.</span></span>

![Подтверждение операции масштабирования](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

## <a name="buy-the-domain"></a><span data-ttu-id="be9ed-136">Приобретение домена</span><span class="sxs-lookup"><span data-stu-id="be9ed-136">Buy the domain</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="be9ed-137">Вход в Azure</span><span class="sxs-lookup"><span data-stu-id="be9ed-137">Sign in to Azure</span></span>
<span data-ttu-id="be9ed-138">Откройте [портал Azure](https://portal.azure.com/) и войдите в систему, используя свою учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="be9ed-138">Open the [Azure portal](https://portal.azure.com/) and sign in with your Azure account.</span></span>

### <a name="launch-buy-domains"></a><span data-ttu-id="be9ed-139">Запуск приобретения доменов</span><span class="sxs-lookup"><span data-stu-id="be9ed-139">Launch Buy domains</span></span>
<span data-ttu-id="be9ed-140">На вкладке **Веб-приложения** щелкните имя своего веб-приложения, выберите **Параметры**, а затем — **Личные домены**.</span><span class="sxs-lookup"><span data-stu-id="be9ed-140">In the **Web Apps** tab, click the name of your web app, select **Settings**, and then select **Custom domains**</span></span>
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

<span data-ttu-id="be9ed-141">На странице **Личные домены** щелкните **Купить домены**.</span><span class="sxs-lookup"><span data-stu-id="be9ed-141">In the **Custom domains** page, click **Buy domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-1.png)

### <a name="configure-the-domain-purchase"></a><span data-ttu-id="be9ed-142">Настройка приобретения доменов</span><span class="sxs-lookup"><span data-stu-id="be9ed-142">Configure the domain purchase</span></span>

<span data-ttu-id="be9ed-143">На странице **Домен службы приложений** в текстовом поле **Поиск домена** введите имя домена, которое необходимо приобрести, и введите `Enter`.</span><span class="sxs-lookup"><span data-stu-id="be9ed-143">In the **App Service Domain** page, in the **Search for domain** box, type the domain name you want to buy and type `Enter`.</span></span> <span data-ttu-id="be9ed-144">Под текстовым полем появятся доступные домены.</span><span class="sxs-lookup"><span data-stu-id="be9ed-144">The suggested available domains are shown just below the text box.</span></span> <span data-ttu-id="be9ed-145">Выберите один или несколько доменов, которые вы хотите приобрести.</span><span class="sxs-lookup"><span data-stu-id="be9ed-145">Select one or more domains you want to buy.</span></span> 
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-2.png)

<span data-ttu-id="be9ed-146">Щелкните **Контактные данные** и заполните форму контактных данных домена.</span><span class="sxs-lookup"><span data-stu-id="be9ed-146">Click the **Contact Information** and fill out the domain's contact information form.</span></span> <span data-ttu-id="be9ed-147">По завершении нажмите кнопку **ОК**, чтобы вернуться на страницу домена службы приложений.</span><span class="sxs-lookup"><span data-stu-id="be9ed-147">When finished, click **OK** to return to the App Service Domain page.</span></span>
   
<span data-ttu-id="be9ed-148">Очень важно ввести правильные данные в обязательные поля.</span><span class="sxs-lookup"><span data-stu-id="be9ed-148">It is important that you fill out all required fields with as much accuracy as possible.</span></span> <span data-ttu-id="be9ed-149">Неправильные контактные данные могут препятствовать приобретению доменов.</span><span class="sxs-lookup"><span data-stu-id="be9ed-149">Incorrect data for contact information can result in failure to purchase domains.</span></span> 

<span data-ttu-id="be9ed-150">Затем выберите нужные параметры для вашего домена.</span><span class="sxs-lookup"><span data-stu-id="be9ed-150">Next, select the desired options for your domain.</span></span> <span data-ttu-id="be9ed-151">Примеры см. в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="be9ed-151">See the following table for explanations:</span></span>

| <span data-ttu-id="be9ed-152">Настройка</span><span class="sxs-lookup"><span data-stu-id="be9ed-152">Setting</span></span> | <span data-ttu-id="be9ed-153">Рекомендуемое значение</span><span class="sxs-lookup"><span data-stu-id="be9ed-153">Suggested Value</span></span> | <span data-ttu-id="be9ed-154">Описание</span><span class="sxs-lookup"><span data-stu-id="be9ed-154">Description</span></span> |
|-|-|-|
|<span data-ttu-id="be9ed-155">Автоматическое возобновление</span><span class="sxs-lookup"><span data-stu-id="be9ed-155">Auto renew</span></span> | <span data-ttu-id="be9ed-156">**Включение**</span><span class="sxs-lookup"><span data-stu-id="be9ed-156">**Enable**</span></span> | <span data-ttu-id="be9ed-157">Домен службы приложений автоматически возобновляется каждый год.</span><span class="sxs-lookup"><span data-stu-id="be9ed-157">Renews your App Service Domain automatically every year.</span></span> <span data-ttu-id="be9ed-158">Во время возобновления с вашей кредитной карты снимается та же сумма.</span><span class="sxs-lookup"><span data-stu-id="be9ed-158">Your credit card is charged the same purchase price at the time of renewal.</span></span> |
|<span data-ttu-id="be9ed-159">Защита конфиденциальности</span><span class="sxs-lookup"><span data-stu-id="be9ed-159">Privacy protection</span></span> | <span data-ttu-id="be9ed-160">Включение</span><span class="sxs-lookup"><span data-stu-id="be9ed-160">Enable</span></span> | <span data-ttu-id="be9ed-161">Согласитесь применять защиту личных данных, которая включена в стоимость покупки _бесплатно_ (за исключением доменов верхнего уровня, реестры которых не поддерживают защиту конфиденциальности, например _.co.in_, _.co.uk_ и т. д.).</span><span class="sxs-lookup"><span data-stu-id="be9ed-161">Opt in to "Privacy protection", which is included in the purchase price _for free_ (except for top-level domains whose registry do not support privacy protection, such as _.co.in_, _.co.uk_, and so on).</span></span> |
| <span data-ttu-id="be9ed-162">Назначение имен узлов по умолчанию</span><span class="sxs-lookup"><span data-stu-id="be9ed-162">Assign default hostnames</span></span> | <span data-ttu-id="be9ed-163">**www** и **@**</span><span class="sxs-lookup"><span data-stu-id="be9ed-163">**www** and **@**</span></span> | <span data-ttu-id="be9ed-164">При необходимости выберите нужные привязки имен узлов.</span><span class="sxs-lookup"><span data-stu-id="be9ed-164">Select the desired hostname bindings, if desired.</span></span> <span data-ttu-id="be9ed-165">После завершения операции покупки домена доступ к веб-приложению может осуществляться с помощью выбранных имен узлов.</span><span class="sxs-lookup"><span data-stu-id="be9ed-165">When the domain purchase operation is complete, your web app can be accessed at the selected hostnames.</span></span> <span data-ttu-id="be9ed-166">Если веб-приложение находится за [диспетчером трафика Azure](https://azure.microsoft.com/services/traffic-manager/), вы не увидите пункт назначения корневого домена (@), так как диспетчер трафика не поддерживает записи типа A.</span><span class="sxs-lookup"><span data-stu-id="be9ed-166">If the web app is behind [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/), you don't see the option to assign the root domain (@), because Traffic Manager does not support A records.</span></span> <span data-ttu-id="be9ed-167">После завершения приобретения домена можно внести изменения в назначения имен узлов.</span><span class="sxs-lookup"><span data-stu-id="be9ed-167">You can make changes to the hostname assignments after the domain purchase completes.</span></span> |

### <a name="accept-terms-and-purchase"></a><span data-ttu-id="be9ed-168">Принятие условий и приобретение</span><span class="sxs-lookup"><span data-stu-id="be9ed-168">Accept terms and purchase</span></span>

<span data-ttu-id="be9ed-169">Выберите **Условия использования**, чтобы просмотреть условия использования и тарифы, а затем нажмите кнопку **Купить**.</span><span class="sxs-lookup"><span data-stu-id="be9ed-169">Click **Legal Terms** to review the terms and the charges, then click **Buy**.</span></span>

> [!NOTE]
> <span data-ttu-id="be9ed-170">Домены службы приложений используют Azure DNS для размещения доменов.</span><span class="sxs-lookup"><span data-stu-id="be9ed-170">App Service Domains use Azure DNS to host the domains.</span></span> <span data-ttu-id="be9ed-171">Помимо платы за регистрацию домена взимается плата за использование Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="be9ed-171">In addition to the domain registration fee, usage charges for Azure DNS apply.</span></span> <span data-ttu-id="be9ed-172">Дополнительные сведения см. на странице [цен на Azure DNS](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="be9ed-172">For information, see [Azure DNS Pricing](https://azure.microsoft.com/pricing/details/dns/).</span></span>
>
>

<span data-ttu-id="be9ed-173">На странице **домена службы приложений** нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="be9ed-173">Back in the **App Service Domain** page, click **OK**.</span></span> <span data-ttu-id="be9ed-174">Во время операции появятся следующие уведомления:</span><span class="sxs-lookup"><span data-stu-id="be9ed-174">While the operation is in progress, you see the following notifications:</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-validate.png)

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-purchase-success.png)

### <a name="test-the-hostnames"></a><span data-ttu-id="be9ed-175">Проверка имен узлов</span><span class="sxs-lookup"><span data-stu-id="be9ed-175">Test the hostnames</span></span>

<span data-ttu-id="be9ed-176">Если для веб-приложения вы назначили имена узлов по умолчанию, вы также увидите уведомление о выполнении для каждого выбранного узла.</span><span class="sxs-lookup"><span data-stu-id="be9ed-176">If you have assigned default hostnames to your web app, you also see a success notification for each selected hostname.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

<span data-ttu-id="be9ed-177">Выбранные имена узлов появятся на странице **Личные домены** в разделе **Имена узлов**.</span><span class="sxs-lookup"><span data-stu-id="be9ed-177">You also see the selected hostnames in the **Custom domains** page, in the **Hostnames** section.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added.png)

<span data-ttu-id="be9ed-178">Чтобы проверить имена узлов, перейдите по указанным именам узлов в браузере.</span><span class="sxs-lookup"><span data-stu-id="be9ed-178">To test the hostnames, navigate to the listed hostnames in the browser.</span></span> <span data-ttu-id="be9ed-179">В примере на предыдущем снимке экрана попробуйте перейти к _kontoso.net_ и _www.kontoso.net_.</span><span class="sxs-lookup"><span data-stu-id="be9ed-179">In the example in the preceding screenshot, try navigating to _kontoso.net_ and _www.kontoso.net_.</span></span>

## <a name="assign-hostnames-to-web-app"></a><span data-ttu-id="be9ed-180">Назначение имен узлов для веб-приложения</span><span class="sxs-lookup"><span data-stu-id="be9ed-180">Assign hostnames to web app</span></span>

<span data-ttu-id="be9ed-181">Если вы решили не назначать имена узлов по умолчанию для веб-приложения в процессе покупки или хотите назначить имя узла, которое отсутствует в списке, имя узла можно назначить в любое время.</span><span class="sxs-lookup"><span data-stu-id="be9ed-181">If you choose not to assign one or more default hostnames to your web app during the purchase process, or if you need to assign a hostname not listed, you can assign a hostname at anytime.</span></span>

<span data-ttu-id="be9ed-182">Вы также можете назначить имена узлов в домене службы приложений для любого другого веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="be9ed-182">You can also assign hostnames in the App Service Domain to any other web app.</span></span> <span data-ttu-id="be9ed-183">Дальнейшие шаги зависят от того, принадлежат ли домен службы приложений и веб-приложение к одной подписке.</span><span class="sxs-lookup"><span data-stu-id="be9ed-183">The steps depend on whether the App Service Domain and the web app belong to the same subscription.</span></span>

- <span data-ttu-id="be9ed-184">Другая подписка: сопоставьте пользовательские записи DNS в домене службы приложений с веб-приложением как с приобретенным внешним доменом.</span><span class="sxs-lookup"><span data-stu-id="be9ed-184">Different subscription: Map custom DNS records from the App Service Domain to the web app like an externally purchased domain.</span></span> <span data-ttu-id="be9ed-185">Дополнительные сведения о добавлении пользовательских имен DNS в домен службы приложений см. в статье [Приобретение и настройка имени личного домена для службы приложений Azure](#custom).</span><span class="sxs-lookup"><span data-stu-id="be9ed-185">For information on adding custom DNS names to an App Service Domain, see [Manage custom DNS records](#custom).</span></span> <span data-ttu-id="be9ed-186">Дополнительные сведения о сопоставлении внешнего приобретенного домена с веб-приложением см. в статье [Сопоставление существующего настраиваемого DNS-имени с веб-приложениями Azure](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="be9ed-186">To map an external purchased domain to a web app, see [Map an existing custom DNS name to Azure Web Apps](app-service-web-tutorial-custom-domain.md).</span></span> 
- <span data-ttu-id="be9ed-187">Та же подписка: выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="be9ed-187">Same subscription: Use the following steps.</span></span>

### <a name="launch-add-hostname"></a><span data-ttu-id="be9ed-188">Запуск добавления имени узла</span><span class="sxs-lookup"><span data-stu-id="be9ed-188">Launch add hostname</span></span>
<span data-ttu-id="be9ed-189">На странице **Службы приложений** выберите имя веб-приложения, для которого вы хотите назначить имена узлов, выберите **Параметры**, а затем — **Личные домены**.</span><span class="sxs-lookup"><span data-stu-id="be9ed-189">In the **App Services** page, select the name of your web app that you want to assign hostnames to, select **Settings**, and then select **Custom domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

<span data-ttu-id="be9ed-190">Убедитесь, что приобретенный домен находится в разделе **Домены службы приложений**, но не выбирайте его.</span><span class="sxs-lookup"><span data-stu-id="be9ed-190">Make sure that your purchased domain is listed in the **App Service Domains** section, but don't select it.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-select-domain.png)

> [!NOTE]
> <span data-ttu-id="be9ed-191">Все домены службы приложений в той же подписке отображаются на странице **Личные домены** веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="be9ed-191">All App Service Domains in the same subscription are shown in the web app's **Custom domains** page.</span></span> <span data-ttu-id="be9ed-192">Если домен находится в подписке веб-приложения, но не отображается на странице **Личные домены** веб-приложения, повторно откройте страницу **Личные домены** или обновите веб-страницу.</span><span class="sxs-lookup"><span data-stu-id="be9ed-192">If your domain is in the web app's subscription, but you cannot see it in the web app's **Custom domains** page, try reopening the **Custom domains** page or refresh the webpage.</span></span> <span data-ttu-id="be9ed-193">Также проверьте ход выполнения или наличие сбоев при создании в разделе уведомлений (значок "колокольчик") в верхней части портала Azure.</span><span class="sxs-lookup"><span data-stu-id="be9ed-193">Also, check the notification bell at the top of the Azure portal for progress or creation failures.</span></span>
>
>

<span data-ttu-id="be9ed-194">Выберите **Добавить имя узла**.</span><span class="sxs-lookup"><span data-stu-id="be9ed-194">Select **Add hostname**.</span></span>

### <a name="configure-hostname"></a><span data-ttu-id="be9ed-195">Настройка имени узла</span><span class="sxs-lookup"><span data-stu-id="be9ed-195">Configure hostname</span></span>
<span data-ttu-id="be9ed-196">В диалоговом окне **Добавить имя узла** введите полное доменное имя домена службы приложений или любой поддомен.</span><span class="sxs-lookup"><span data-stu-id="be9ed-196">In the **Add hostname** dialog, type the fully qualified domain name of your App Service Domain or any subdomain.</span></span> <span data-ttu-id="be9ed-197">Например:</span><span class="sxs-lookup"><span data-stu-id="be9ed-197">For example:</span></span>

- <span data-ttu-id="be9ed-198">kontoso.net</span><span class="sxs-lookup"><span data-stu-id="be9ed-198">kontoso.net</span></span>
- <span data-ttu-id="be9ed-199">www.kontoso.net</span><span class="sxs-lookup"><span data-stu-id="be9ed-199">www.kontoso.net</span></span>
- <span data-ttu-id="be9ed-200">abc.kontoso.net</span><span class="sxs-lookup"><span data-stu-id="be9ed-200">abc.kontoso.net</span></span>

<span data-ttu-id="be9ed-201">По завершении выберите **Проверить**.</span><span class="sxs-lookup"><span data-stu-id="be9ed-201">When finished, select **Validate**.</span></span> <span data-ttu-id="be9ed-202">Тип записи имени узла выбирается автоматически.</span><span class="sxs-lookup"><span data-stu-id="be9ed-202">The hostname record type is automatically selected for you.</span></span>

<span data-ttu-id="be9ed-203">Выберите **Добавить имя узла**.</span><span class="sxs-lookup"><span data-stu-id="be9ed-203">Select **Add hostname**.</span></span>

<span data-ttu-id="be9ed-204">После завершения появится уведомление об успешном выполнении операции назначения имени узла.</span><span class="sxs-lookup"><span data-stu-id="be9ed-204">When the operation is complete, you see a success notification for the assigned hostname.</span></span>  

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

### <a name="close-add-hostname"></a><span data-ttu-id="be9ed-205">Закрытие страницы добавления имени узла</span><span class="sxs-lookup"><span data-stu-id="be9ed-205">Close add hostname</span></span>
<span data-ttu-id="be9ed-206">На странице **Добавить имя узла** назначьте любое другое имя узла для веб-приложения в случае необходимости.</span><span class="sxs-lookup"><span data-stu-id="be9ed-206">In the **Add hostname** page, assign any other hostname to your web app, as desired.</span></span> <span data-ttu-id="be9ed-207">После завершения закройте страницу **Добавить имя узла**.</span><span class="sxs-lookup"><span data-stu-id="be9ed-207">When finished, close the **Add hostname** page.</span></span>

<span data-ttu-id="be9ed-208">Вы увидите только что назначенные имена узлов на странице **Личные домены** вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="be9ed-208">You should now see the newly assigned hostname(s) in your app's **Custom domains** page.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added2.png)

### <a name="test-the-hostnames"></a><span data-ttu-id="be9ed-209">Проверка имен узлов</span><span class="sxs-lookup"><span data-stu-id="be9ed-209">Test the hostnames</span></span>

<span data-ttu-id="be9ed-210">Перейдите по указанным именам узлов в браузере.</span><span class="sxs-lookup"><span data-stu-id="be9ed-210">Navigate to the listed hostnames in the browser.</span></span> <span data-ttu-id="be9ed-211">В примере на предыдущем снимке экрана попробуйте перейти к _www.kontoso.net_.</span><span class="sxs-lookup"><span data-stu-id="be9ed-211">In the example in the preceding screenshot, try navigating to _abc.kontoso.net_.</span></span>

<a name="custom" />

## <a name="manage-custom-dns-records"></a><span data-ttu-id="be9ed-212">Управление пользовательскими записями DNS</span><span class="sxs-lookup"><span data-stu-id="be9ed-212">Manage custom DNS records</span></span>

<span data-ttu-id="be9ed-213">В Azure управление записями DNS для домена службы приложений осуществляется с помощью [Azure DNS](https://azure.microsoft.com/services/dns/).</span><span class="sxs-lookup"><span data-stu-id="be9ed-213">In Azure, DNS records for an App Service Domain are managed using [Azure DNS](https://azure.microsoft.com/services/dns/).</span></span> <span data-ttu-id="be9ed-214">Вы можете добавлять, удалять и обновлять записи DNS так же, как для приобретенного внешнего домена.</span><span class="sxs-lookup"><span data-stu-id="be9ed-214">You can add, remove, and update DNS records, just like for an externally purchased domain.</span></span>

### <a name="open-app-service-domain"></a><span data-ttu-id="be9ed-215">Открытие домена службы приложений</span><span class="sxs-lookup"><span data-stu-id="be9ed-215">Open App Service Domain</span></span>

<span data-ttu-id="be9ed-216">На портале Azure в меню слева выберите **Больше служб** > **Домены службы приложений**.</span><span class="sxs-lookup"><span data-stu-id="be9ed-216">In the Azure portal, from the left menu, select **More Services** > **App Service Domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

<span data-ttu-id="be9ed-217">Выберите домен для управления.</span><span class="sxs-lookup"><span data-stu-id="be9ed-217">Select the domain to manage.</span></span> 

### <a name="access-dns-zone"></a><span data-ttu-id="be9ed-218">Доступ к зоне DNS</span><span class="sxs-lookup"><span data-stu-id="be9ed-218">Access DNS zone</span></span>

<span data-ttu-id="be9ed-219">В меню домена слева выберите **Зона DNS**.</span><span class="sxs-lookup"><span data-stu-id="be9ed-219">In the domain's left menu, select **DNS zone**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-dns-zone.png)

<span data-ttu-id="be9ed-220">Открывается страница [Зона DNS](../dns/dns-zones-records.md) вашего домена службы приложений в Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="be9ed-220">This action opens the [DNS zone](../dns/dns-zones-records.md) page of your App Service Domain in Azure DNS.</span></span> <span data-ttu-id="be9ed-221">Сведения о том, как изменять записи DNS, см. в статье [Приобретение и настройка имени личного домена для службы приложений Azure](../dns/dns-operations-dnszones-portal.md).</span><span class="sxs-lookup"><span data-stu-id="be9ed-221">For information on how to edit DNS records, see [How to manage DNS Zones in the Azure portal](../dns/dns-operations-dnszones-portal.md).</span></span>

## <a name="cancel-purchase-delete-domain"></a><span data-ttu-id="be9ed-222">Отмена покупки (удаление домена)</span><span class="sxs-lookup"><span data-stu-id="be9ed-222">Cancel purchase (delete domain)</span></span>

<span data-ttu-id="be9ed-223">Вы можете отменить регистрацию домена службы приложений с полным возмещением в течение 5 дней после даты покупки домена.</span><span class="sxs-lookup"><span data-stu-id="be9ed-223">After you purchase the App Service Domain, you have five days to cancel your purchase for a full refund.</span></span> <span data-ttu-id="be9ed-224">По истечении 5 дней вы сможете удалить домен службы приложений, но не сможете получить полное возмещение.</span><span class="sxs-lookup"><span data-stu-id="be9ed-224">After five days, you can delete the App Service Domain, but cannot receive a refund.</span></span>

### <a name="open-app-service-domain"></a><span data-ttu-id="be9ed-225">Открытие домена службы приложений</span><span class="sxs-lookup"><span data-stu-id="be9ed-225">Open App Service Domain</span></span>

<span data-ttu-id="be9ed-226">На портале Azure в меню слева выберите **Больше служб** > **Домены службы приложений**.</span><span class="sxs-lookup"><span data-stu-id="be9ed-226">In the Azure portal, from the left menu, select **More Services** > **App Service Domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

<span data-ttu-id="be9ed-227">Выберите домен, который вы хотите отменить или удалить.</span><span class="sxs-lookup"><span data-stu-id="be9ed-227">Select the domain to you want to cancel or delete.</span></span> 

### <a name="delete-hostname-bindings"></a><span data-ttu-id="be9ed-228">Удаление привязок имен узлов</span><span class="sxs-lookup"><span data-stu-id="be9ed-228">Delete hostname bindings</span></span>

<span data-ttu-id="be9ed-229">В меню слева для домена выберите **Привязки имен узлов**.</span><span class="sxs-lookup"><span data-stu-id="be9ed-229">In the domain's left menu, select **Hostname bindings**.</span></span> <span data-ttu-id="be9ed-230">Здесь перечислены привязки имен узлов из всех служб Azure.</span><span class="sxs-lookup"><span data-stu-id="be9ed-230">The hostname bindings from all Azure services are listed here.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostname-bindings.png)

<span data-ttu-id="be9ed-231">Вы не можете удалить домен службы приложений, пока не будут удалены все привязки имен узлов.</span><span class="sxs-lookup"><span data-stu-id="be9ed-231">You cannot delete the App Service Domain until all hostname bindings are deleted.</span></span>

<span data-ttu-id="be9ed-232">Удалите каждую привязку имени узла, выбрав **...** > **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="be9ed-232">Delete each hostname binding by selecting **...** > **Delete**.</span></span> <span data-ttu-id="be9ed-233">После удаления всех привязок нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="be9ed-233">After all the bindings are deleted, select **Save**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-delete-hostname-bindings.png)

### <a name="cancel-or-delete"></a><span data-ttu-id="be9ed-234">Отмена или удаление</span><span class="sxs-lookup"><span data-stu-id="be9ed-234">Cancel or delete</span></span>

<span data-ttu-id="be9ed-235">В меню домена слева выберите **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="be9ed-235">In the domain's left menu, select **Overview**.</span></span> 

<span data-ttu-id="be9ed-236">Если период отмены приобретенного домена не истек, выберите **Отменить покупку**.</span><span class="sxs-lookup"><span data-stu-id="be9ed-236">If the cancellation period on the purchased domain has not elapsed, select **Cancel purchase**.</span></span> <span data-ttu-id="be9ed-237">В противном случае вы увидите кнопку **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="be9ed-237">Otherwise, you see a **Delete** button instead.</span></span> <span data-ttu-id="be9ed-238">Чтобы удалить домен без возмещения средств, нажмите кнопку **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="be9ed-238">To delete the domain without a refund, select **Delete**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-cancel.png)

<span data-ttu-id="be9ed-239">Нажмите кнопку **ОК**, чтобы подтвердить операцию.</span><span class="sxs-lookup"><span data-stu-id="be9ed-239">Select **OK** to confirm the operation.</span></span> <span data-ttu-id="be9ed-240">Если вы не хотите продолжать, щелкните в любом месте за пределами диалогового окна подтверждения.</span><span class="sxs-lookup"><span data-stu-id="be9ed-240">If you don't want to proceed, click anywhere outside of the confirmation dialog.</span></span>

<span data-ttu-id="be9ed-241">После завершения операции домен освобождается из подписки, и его снова может купить любой желающий.</span><span class="sxs-lookup"><span data-stu-id="be9ed-241">After the operation is complete, the domain is released from your subscription and available for anyone to purchase again.</span></span> 
