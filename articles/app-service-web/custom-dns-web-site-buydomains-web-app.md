---
title: "aaaBuy пользовательское доменное имя для веб-приложений Azure"
description: "Узнайте, как имя toobuy пользовательский домен с веб-приложения в службе приложений Azure."
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
ms.openlocfilehash: 2ff61a3f27020516c917fe105ece99eb2a5754b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="buy-a-custom-domain-name-for-azure-web-apps"></a><span data-ttu-id="a18a5-103">Приобретение имени личного домена для веб-приложений Azure</span><span class="sxs-lookup"><span data-stu-id="a18a5-103">Buy a custom domain name for Azure Web Apps</span></span>

<span data-ttu-id="a18a5-104">Домены службы приложений (предварительная версия) — это домены верхнего уровня, которые управляются непосредственно в Azure.</span><span class="sxs-lookup"><span data-stu-id="a18a5-104">App Service domains (preview) are top-level domains that are managed directly in Azure.</span></span> <span data-ttu-id="a18a5-105">Они позволяют легко toomanage пользовательских доменов [веб-приложениях Azure](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a18a5-105">They make it easy toomanage custom domains for [Azure Web Apps](app-service-web-overview.md).</span></span> <span data-ttu-id="a18a5-106">Этот учебник показывает, как toobuy домен приложения службы и назначьте DNS имена tooAzure веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="a18a5-106">This tutorial shows you how toobuy an App Service domain and assign DNS names tooAzure Web Apps.</span></span>

<span data-ttu-id="a18a5-107">Эта статья предназначена для службы приложений Azure ("Веб-приложения", "Приложения API", "Мобильные приложения", Logic Apps).</span><span class="sxs-lookup"><span data-stu-id="a18a5-107">This article is for Azure App Service (Web Apps, API Apps, Mobile Apps, Logic Apps).</span></span> <span data-ttu-id="a18a5-108">Для хранилища Azure или виртуальной Машине Azure в разделе [tooAzure домена назначение приложения службы виртуальных Машин или хранилище Azure](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/).</span><span class="sxs-lookup"><span data-stu-id="a18a5-108">For Azure VM or Azure Storage, see [Assign App Service domain tooAzure VM or Azure Storage](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/).</span></span> <span data-ttu-id="a18a5-109">Сведения об облачных службах см. в статье [Настройка пользовательского доменного имени для облачной службы Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a18a5-109">For Cloud Services, see [Configuring a custom domain name for an Azure cloud service](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a18a5-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a18a5-110">Prerequisites</span></span>

<span data-ttu-id="a18a5-111">toocomplete этого учебника:</span><span class="sxs-lookup"><span data-stu-id="a18a5-111">toocomplete this tutorial:</span></span>

* <span data-ttu-id="a18a5-112">[Создайте приложение службы приложений](/azure/app-service/) или используйте приложение, созданное для работы с другим руководством.</span><span class="sxs-lookup"><span data-stu-id="a18a5-112">[Create an App Service app](/azure/app-service/), or use an app that you created for another tutorial.</span></span>

## <a name="prepare-hello-app"></a><span data-ttu-id="a18a5-113">Подготовка приложения hello</span><span class="sxs-lookup"><span data-stu-id="a18a5-113">Prepare hello app</span></span>

<span data-ttu-id="a18a5-114">toouse пользовательских доменов в Azure веб-приложений, веб-приложения [план служб приложений](https://azure.microsoft.com/pricing/details/app-service/) должен быть платной уровня (**Shared**, **основные**, **Стандартная**, или **Premium**).</span><span class="sxs-lookup"><span data-stu-id="a18a5-114">toouse custom domains in Azure Web Apps, your web app's [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be a paid tier (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> <span data-ttu-id="a18a5-115">На этом шаге вы убедитесь, что веб-приложения hello в hello поддерживается ценовой категории.</span><span class="sxs-lookup"><span data-stu-id="a18a5-115">In this step, you make sure that hello web app is in hello supported pricing tier.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="a18a5-116">Войдите в tooAzure</span><span class="sxs-lookup"><span data-stu-id="a18a5-116">Sign in tooAzure</span></span>

<span data-ttu-id="a18a5-117">Откройте hello [портал Azure](https://portal.azure.com) и выполните вход с учетной записью Azure.</span><span class="sxs-lookup"><span data-stu-id="a18a5-117">Open hello [Azure portal](https://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="navigate-toohello-app-in-hello-azure-portal"></a><span data-ttu-id="a18a5-118">Перейдите в приложение toohello в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="a18a5-118">Navigate toohello app in hello Azure portal</span></span>

<span data-ttu-id="a18a5-119">Hello в левом меню, выберите **службы приложений**, а затем выберите имя hello приложение hello.</span><span class="sxs-lookup"><span data-stu-id="a18a5-119">From hello left menu, select **App Services**, and then select hello name of hello app.</span></span>

![Приложение портала навигации tooAzure](./media/app-service-web-tutorial-custom-domain/select-app.png)

<span data-ttu-id="a18a5-121">Вы увидите страницу управления hello объекта hello приложение служб приложений.</span><span class="sxs-lookup"><span data-stu-id="a18a5-121">You see hello management page of hello App Service app.</span></span>  

### <a name="check-hello-pricing-tier"></a><span data-ttu-id="a18a5-122">Проверьте hello ценовой категории</span><span class="sxs-lookup"><span data-stu-id="a18a5-122">Check hello pricing tier</span></span>

<span data-ttu-id="a18a5-123">Hello навигации страницы приложения hello слева, прокрутите toohello **параметры** , выберите **масштаб (план службы приложений)**.</span><span class="sxs-lookup"><span data-stu-id="a18a5-123">In hello left navigation of hello app page, scroll toohello **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Меню увеличения масштаба](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

<span data-ttu-id="a18a5-125">приложение Hello текущего уровня, выделяется синей рамкой.</span><span class="sxs-lookup"><span data-stu-id="a18a5-125">hello app's current tier is highlighted by a blue border.</span></span> <span data-ttu-id="a18a5-126">Убедитесь том, что приложение hello не hello toomake **Free** уровня.</span><span class="sxs-lookup"><span data-stu-id="a18a5-126">Check toomake sure that hello app is not in hello **Free** tier.</span></span> <span data-ttu-id="a18a5-127">Пользовательские DNS не поддерживается в hello **Free** уровня.</span><span class="sxs-lookup"><span data-stu-id="a18a5-127">Custom DNS is not supported in hello **Free** tier.</span></span> 

![Проверка ценовой категории](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

<span data-ttu-id="a18a5-129">Если hello план служб приложений не **Free**, закройте hello **выберите ценовую категорию** страницы и пропуска слишком[домена hello Покупка](#buy-the-domain).</span><span class="sxs-lookup"><span data-stu-id="a18a5-129">If hello App Service plan is not **Free**, close hello **Choose your pricing tier** page and skip too[Buy hello domain](#buy-the-domain).</span></span>

### <a name="scale-up-hello-app-service-plan"></a><span data-ttu-id="a18a5-130">Вертикальное масштабирование hello план служб приложений</span><span class="sxs-lookup"><span data-stu-id="a18a5-130">Scale up hello App Service plan</span></span>

<span data-ttu-id="a18a5-131">Выберите любой из уровней занятых hello (**Shared**, **основные**, **Стандартная**, или **Premium**).</span><span class="sxs-lookup"><span data-stu-id="a18a5-131">Select any of hello non-free tiers (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> 

<span data-ttu-id="a18a5-132">Нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="a18a5-132">Click **Select**.</span></span>

![Проверка ценовой категории](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

<span data-ttu-id="a18a5-134">При появлении hello после уведомления hello шкалы операция завершена.</span><span class="sxs-lookup"><span data-stu-id="a18a5-134">When you see hello following notification, hello scale operation is complete.</span></span>

![Подтверждение операции масштабирования](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

## <a name="buy-hello-domain"></a><span data-ttu-id="a18a5-136">Приобретение hello домена</span><span class="sxs-lookup"><span data-stu-id="a18a5-136">Buy hello domain</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="a18a5-137">Войдите в tooAzure</span><span class="sxs-lookup"><span data-stu-id="a18a5-137">Sign in tooAzure</span></span>
<span data-ttu-id="a18a5-138">Откройте hello [портал Azure](https://portal.azure.com/) и выполните вход с учетной записью Azure.</span><span class="sxs-lookup"><span data-stu-id="a18a5-138">Open hello [Azure portal](https://portal.azure.com/) and sign in with your Azure account.</span></span>

### <a name="launch-buy-domains"></a><span data-ttu-id="a18a5-139">Запуск приобретения доменов</span><span class="sxs-lookup"><span data-stu-id="a18a5-139">Launch Buy domains</span></span>
<span data-ttu-id="a18a5-140">В hello **веб-приложений** щелкните имя веб-приложения, выберите hello **параметры**, а затем выберите **пользовательские домены**</span><span class="sxs-lookup"><span data-stu-id="a18a5-140">In hello **Web Apps** tab, click hello name of your web app, select **Settings**, and then select **Custom domains**</span></span>
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

<span data-ttu-id="a18a5-141">В hello **пользовательские домены** щелкните **купить домены**.</span><span class="sxs-lookup"><span data-stu-id="a18a5-141">In hello **Custom domains** page, click **Buy domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-1.png)

### <a name="configure-hello-domain-purchase"></a><span data-ttu-id="a18a5-142">Настройка домена покупки hello</span><span class="sxs-lookup"><span data-stu-id="a18a5-142">Configure hello domain purchase</span></span>

<span data-ttu-id="a18a5-143">В hello **домен приложения службы** страницы в hello **поиск домена** введите имя домена на hello toobuy и тип `Enter`.</span><span class="sxs-lookup"><span data-stu-id="a18a5-143">In hello **App Service Domain** page, in hello **Search for domain** box, type hello domain name you want toobuy and type `Enter`.</span></span> <span data-ttu-id="a18a5-144">Hello предлагаемые доступных доменов отображаются под hello текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="a18a5-144">hello suggested available domains are shown just below hello text box.</span></span> <span data-ttu-id="a18a5-145">Выберите один или несколько доменов, которые вы хотите toobuy.</span><span class="sxs-lookup"><span data-stu-id="a18a5-145">Select one or more domains you want toobuy.</span></span> 
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-2.png)

<span data-ttu-id="a18a5-146">Нажмите кнопку hello **контактные данные** и заполните форму hello домена контактные данные.</span><span class="sxs-lookup"><span data-stu-id="a18a5-146">Click hello **Contact Information** and fill out hello domain's contact information form.</span></span> <span data-ttu-id="a18a5-147">По завершении нажмите кнопку **ОК** tooreturn toohello домен приложения службы страницы.</span><span class="sxs-lookup"><span data-stu-id="a18a5-147">When finished, click **OK** tooreturn toohello App Service Domain page.</span></span>
   
<span data-ttu-id="a18a5-148">Очень важно ввести правильные данные в обязательные поля.</span><span class="sxs-lookup"><span data-stu-id="a18a5-148">It is important that you fill out all required fields with as much accuracy as possible.</span></span> <span data-ttu-id="a18a5-149">Неверные данные для получения контактной информации может привести к toopurchase домены сбоя.</span><span class="sxs-lookup"><span data-stu-id="a18a5-149">Incorrect data for contact information can result in failure toopurchase domains.</span></span> 

<span data-ttu-id="a18a5-150">Затем выберите параметры hello требуемого для своего домена.</span><span class="sxs-lookup"><span data-stu-id="a18a5-150">Next, select hello desired options for your domain.</span></span> <span data-ttu-id="a18a5-151">См. в следующей таблице для объяснения hello.</span><span class="sxs-lookup"><span data-stu-id="a18a5-151">See hello following table for explanations:</span></span>

| <span data-ttu-id="a18a5-152">Настройка</span><span class="sxs-lookup"><span data-stu-id="a18a5-152">Setting</span></span> | <span data-ttu-id="a18a5-153">Рекомендуемое значение</span><span class="sxs-lookup"><span data-stu-id="a18a5-153">Suggested Value</span></span> | <span data-ttu-id="a18a5-154">Описание</span><span class="sxs-lookup"><span data-stu-id="a18a5-154">Description</span></span> |
|-|-|-|
|<span data-ttu-id="a18a5-155">Автоматическое возобновление</span><span class="sxs-lookup"><span data-stu-id="a18a5-155">Auto renew</span></span> | <span data-ttu-id="a18a5-156">**Включение**</span><span class="sxs-lookup"><span data-stu-id="a18a5-156">**Enable**</span></span> | <span data-ttu-id="a18a5-157">Домен службы приложений автоматически возобновляется каждый год.</span><span class="sxs-lookup"><span data-stu-id="a18a5-157">Renews your App Service Domain automatically every year.</span></span> <span data-ttu-id="a18a5-158">Плата вашей кредитной карты hello одной цене покупки во время обновления hello.</span><span class="sxs-lookup"><span data-stu-id="a18a5-158">Your credit card is charged hello same purchase price at hello time of renewal.</span></span> |
|<span data-ttu-id="a18a5-159">Защита конфиденциальности</span><span class="sxs-lookup"><span data-stu-id="a18a5-159">Privacy protection</span></span> | <span data-ttu-id="a18a5-160">Включение</span><span class="sxs-lookup"><span data-stu-id="a18a5-160">Enable</span></span> | <span data-ttu-id="a18a5-161">Соглашаться слишком «Защита личных», который включается в цены покупки hello _бесплатно_ (за исключением доменов верхнего уровня, реестр которого не поддерживают защиты конфиденциальности, таких как _. co.in_, _. CO.uk_и так далее).</span><span class="sxs-lookup"><span data-stu-id="a18a5-161">Opt in too"Privacy protection", which is included in hello purchase price _for free_ (except for top-level domains whose registry do not support privacy protection, such as _.co.in_, _.co.uk_, and so on).</span></span> |
| <span data-ttu-id="a18a5-162">Назначение имен узлов по умолчанию</span><span class="sxs-lookup"><span data-stu-id="a18a5-162">Assign default hostnames</span></span> | <span data-ttu-id="a18a5-163">**www** и **@**</span><span class="sxs-lookup"><span data-stu-id="a18a5-163">**www** and **@**</span></span> | <span data-ttu-id="a18a5-164">Выберите hello требуемого привязки имени узла, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="a18a5-164">Select hello desired hostname bindings, if desired.</span></span> <span data-ttu-id="a18a5-165">По завершении операции покупки hello домена веб-приложения может осуществляться в hello выбранные имена узлов.</span><span class="sxs-lookup"><span data-stu-id="a18a5-165">When hello domain purchase operation is complete, your web app can be accessed at hello selected hostnames.</span></span> <span data-ttu-id="a18a5-166">Если веб-приложение hello находится за [диспетчера трафика Azure](https://azure.microsoft.com/services/traffic-manager/), вы не видите hello параметр tooassign hello корневого домена (@), так как поддержка записи A не диспетчера трафика.</span><span class="sxs-lookup"><span data-stu-id="a18a5-166">If hello web app is behind [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/), you don't see hello option tooassign hello root domain (@), because Traffic Manager does not support A records.</span></span> <span data-ttu-id="a18a5-167">Можно изменять имя узла назначения toohello после завершения покупки домена hello.</span><span class="sxs-lookup"><span data-stu-id="a18a5-167">You can make changes toohello hostname assignments after hello domain purchase completes.</span></span> |

### <a name="accept-terms-and-purchase"></a><span data-ttu-id="a18a5-168">Принятие условий и приобретение</span><span class="sxs-lookup"><span data-stu-id="a18a5-168">Accept terms and purchase</span></span>

<span data-ttu-id="a18a5-169">Нажмите кнопку **условия** tooreview hello термины и hello накладные расходы, нажмите кнопку **купить**.</span><span class="sxs-lookup"><span data-stu-id="a18a5-169">Click **Legal Terms** tooreview hello terms and hello charges, then click **Buy**.</span></span>

> [!NOTE]
> <span data-ttu-id="a18a5-170">Домены приложений службы используйте домены hello toohost Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="a18a5-170">App Service Domains use Azure DNS toohost hello domains.</span></span> <span data-ttu-id="a18a5-171">Кроме плата регистрации домена toohello, взимается плата за использование для Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="a18a5-171">In addition toohello domain registration fee, usage charges for Azure DNS apply.</span></span> <span data-ttu-id="a18a5-172">Дополнительные сведения см. на странице [цен на Azure DNS](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="a18a5-172">For information, see [Azure DNS Pricing](https://azure.microsoft.com/pricing/details/dns/).</span></span>
>
>

<span data-ttu-id="a18a5-173">Вернитесь в hello **домен приложения службы** щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a18a5-173">Back in hello **App Service Domain** page, click **OK**.</span></span> <span data-ttu-id="a18a5-174">Во время операции hello появляется hello следующие уведомления:</span><span class="sxs-lookup"><span data-stu-id="a18a5-174">While hello operation is in progress, you see hello following notifications:</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-validate.png)

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-purchase-success.png)

### <a name="test-hello-hostnames"></a><span data-ttu-id="a18a5-175">Имена узлов hello теста</span><span class="sxs-lookup"><span data-stu-id="a18a5-175">Test hello hostnames</span></span>

<span data-ttu-id="a18a5-176">Если вы назначили по умолчанию имена узлов tooyour веб-приложения, также будет показано уведомление об успехе для каждого выбранного имени узла.</span><span class="sxs-lookup"><span data-stu-id="a18a5-176">If you have assigned default hostnames tooyour web app, you also see a success notification for each selected hostname.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

<span data-ttu-id="a18a5-177">Появится hello выбранные имена узлов в hello **пользовательские домены** страницы в hello **имена узлов** раздела.</span><span class="sxs-lookup"><span data-stu-id="a18a5-177">You also see hello selected hostnames in hello **Custom domains** page, in hello **Hostnames** section.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added.png)

<span data-ttu-id="a18a5-178">tootest приветствия имен узлов, перейдите в списке toohello имена узлов в браузере hello.</span><span class="sxs-lookup"><span data-stu-id="a18a5-178">tootest hello hostnames, navigate toohello listed hostnames in hello browser.</span></span> <span data-ttu-id="a18a5-179">В примере hello в hello предшествующий экрана, повторите перемещение too_kontoso.net_ и _www.kontoso.net_.</span><span class="sxs-lookup"><span data-stu-id="a18a5-179">In hello example in hello preceding screenshot, try navigating too_kontoso.net_ and _www.kontoso.net_.</span></span>

## <a name="assign-hostnames-tooweb-app"></a><span data-ttu-id="a18a5-180">Назначение приложения tooweb имена узлов</span><span class="sxs-lookup"><span data-stu-id="a18a5-180">Assign hostnames tooweb app</span></span>

<span data-ttu-id="a18a5-181">Если выбирается не tooassign одно или несколько веб-приложения tooyour по умолчанию имена узлов во время hello приобрести процесса, или если не требуется tooassign имени узла в списке, можно назначить имя узла в любое время.</span><span class="sxs-lookup"><span data-stu-id="a18a5-181">If you choose not tooassign one or more default hostnames tooyour web app during hello purchase process, or if you need tooassign a hostname not listed, you can assign a hostname at anytime.</span></span>

<span data-ttu-id="a18a5-182">Можно также назначить имена узлов в домен приложения службы tooany hello другие веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="a18a5-182">You can also assign hostnames in hello App Service Domain tooany other web app.</span></span> <span data-ttu-id="a18a5-183">Hello действия зависят от ли hello домен приложения службы и веб-приложения hello принадлежат toohello одной подписке.</span><span class="sxs-lookup"><span data-stu-id="a18a5-183">hello steps depend on whether hello App Service Domain and hello web app belong toohello same subscription.</span></span>

- <span data-ttu-id="a18a5-184">Другой подписке: сопоставить пользовательские записи DNS из веб-приложения toohello hello домен приложения службы как извне приобретенных домен.</span><span class="sxs-lookup"><span data-stu-id="a18a5-184">Different subscription: Map custom DNS records from hello App Service Domain toohello web app like an externally purchased domain.</span></span> <span data-ttu-id="a18a5-185">Сведения о добавлении пользовательских DNS-имена tooan домен приложения службы, см. в разделе [управление пользовательские записи DNS](#custom).</span><span class="sxs-lookup"><span data-stu-id="a18a5-185">For information on adding custom DNS names tooan App Service Domain, see [Manage custom DNS records](#custom).</span></span> <span data-ttu-id="a18a5-186">toomap внешнего домена приобретенных tooa веб-приложение, в разделе [сопоставления существующих пользовательских DNS имя tooAzure веб-приложений](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="a18a5-186">toomap an external purchased domain tooa web app, see [Map an existing custom DNS name tooAzure Web Apps](app-service-web-tutorial-custom-domain.md).</span></span> 
- <span data-ttu-id="a18a5-187">Одной подписке: hello используйте следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="a18a5-187">Same subscription: Use hello following steps.</span></span>

### <a name="launch-add-hostname"></a><span data-ttu-id="a18a5-188">Запуск добавления имени узла</span><span class="sxs-lookup"><span data-stu-id="a18a5-188">Launch add hostname</span></span>
<span data-ttu-id="a18a5-189">В hello **службы приложений** страницу, выберите hello имя веб-приложения, должны tooassign имен узлов, выберите **параметры**, а затем выберите **пользовательские домены**.</span><span class="sxs-lookup"><span data-stu-id="a18a5-189">In hello **App Services** page, select hello name of your web app that you want tooassign hostnames to, select **Settings**, and then select **Custom domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

<span data-ttu-id="a18a5-190">Убедитесь, что указано приобретенных домена в hello **доменов приложения службы** статьи, но не его выбрать.</span><span class="sxs-lookup"><span data-stu-id="a18a5-190">Make sure that your purchased domain is listed in hello **App Service Domains** section, but don't select it.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-select-domain.png)

> [!NOTE]
> <span data-ttu-id="a18a5-191">Все домены приложения службы в одной подписке отображаются в веб-приложения hello hello **пользовательские домены** страницы.</span><span class="sxs-lookup"><span data-stu-id="a18a5-191">All App Service Domains in hello same subscription are shown in hello web app's **Custom domains** page.</span></span> <span data-ttu-id="a18a5-192">Если домен находится в подписке hello веб-приложения, но он не отображается в веб-приложения hello **пользовательские домены** страницы, повторите попытку открытия hello **пользовательские домены** страницы или обновить веб-страницу приветствия.</span><span class="sxs-lookup"><span data-stu-id="a18a5-192">If your domain is in hello web app's subscription, but you cannot see it in hello web app's **Custom domains** page, try reopening hello **Custom domains** page or refresh hello webpage.</span></span> <span data-ttu-id="a18a5-193">Кроме того проверьте колокольчика уведомления hello вверху hello hello портал Azure для создания или выполнения сбоев.</span><span class="sxs-lookup"><span data-stu-id="a18a5-193">Also, check hello notification bell at hello top of hello Azure portal for progress or creation failures.</span></span>
>
>

<span data-ttu-id="a18a5-194">Выберите **Добавить имя узла**.</span><span class="sxs-lookup"><span data-stu-id="a18a5-194">Select **Add hostname**.</span></span>

### <a name="configure-hostname"></a><span data-ttu-id="a18a5-195">Настройка имени узла</span><span class="sxs-lookup"><span data-stu-id="a18a5-195">Configure hostname</span></span>
<span data-ttu-id="a18a5-196">В hello **добавить имя узла** диалогового окна, hello полное доменное имя типа службы домена приложения или любой дочерний домен.</span><span class="sxs-lookup"><span data-stu-id="a18a5-196">In hello **Add hostname** dialog, type hello fully qualified domain name of your App Service Domain or any subdomain.</span></span> <span data-ttu-id="a18a5-197">Например:</span><span class="sxs-lookup"><span data-stu-id="a18a5-197">For example:</span></span>

- <span data-ttu-id="a18a5-198">kontoso.net</span><span class="sxs-lookup"><span data-stu-id="a18a5-198">kontoso.net</span></span>
- <span data-ttu-id="a18a5-199">www.kontoso.net</span><span class="sxs-lookup"><span data-stu-id="a18a5-199">www.kontoso.net</span></span>
- <span data-ttu-id="a18a5-200">abc.kontoso.net</span><span class="sxs-lookup"><span data-stu-id="a18a5-200">abc.kontoso.net</span></span>

<span data-ttu-id="a18a5-201">По завершении выберите **Проверить**.</span><span class="sxs-lookup"><span data-stu-id="a18a5-201">When finished, select **Validate**.</span></span> <span data-ttu-id="a18a5-202">Тип записи имени узла Hello выбирается автоматически.</span><span class="sxs-lookup"><span data-stu-id="a18a5-202">hello hostname record type is automatically selected for you.</span></span>

<span data-ttu-id="a18a5-203">Выберите **Добавить имя узла**.</span><span class="sxs-lookup"><span data-stu-id="a18a5-203">Select **Add hostname**.</span></span>

<span data-ttu-id="a18a5-204">По завершении операции hello появится уведомление об успехе для hello, назначенный имени узла.</span><span class="sxs-lookup"><span data-stu-id="a18a5-204">When hello operation is complete, you see a success notification for hello assigned hostname.</span></span>  

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

### <a name="close-add-hostname"></a><span data-ttu-id="a18a5-205">Закрытие страницы добавления имени узла</span><span class="sxs-lookup"><span data-stu-id="a18a5-205">Close add hostname</span></span>
<span data-ttu-id="a18a5-206">В hello **добавить имя узла** назначьте любое имя узла tooyour веб-приложения, в случае необходимости.</span><span class="sxs-lookup"><span data-stu-id="a18a5-206">In hello **Add hostname** page, assign any other hostname tooyour web app, as desired.</span></span> <span data-ttu-id="a18a5-207">После завершения закройте hello **добавить имя узла** страницы.</span><span class="sxs-lookup"><span data-stu-id="a18a5-207">When finished, close hello **Add hostname** page.</span></span>

<span data-ttu-id="a18a5-208">Вы увидите hostname(s) hello новые назначенные в вашем приложении **пользовательские домены** страницы.</span><span class="sxs-lookup"><span data-stu-id="a18a5-208">You should now see hello newly assigned hostname(s) in your app's **Custom domains** page.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added2.png)

### <a name="test-hello-hostnames"></a><span data-ttu-id="a18a5-209">Имена узлов hello теста</span><span class="sxs-lookup"><span data-stu-id="a18a5-209">Test hello hostnames</span></span>

<span data-ttu-id="a18a5-210">Перейдите в списке toohello имена узлов в браузере hello.</span><span class="sxs-lookup"><span data-stu-id="a18a5-210">Navigate toohello listed hostnames in hello browser.</span></span> <span data-ttu-id="a18a5-211">В примере перед экрана приветствия hello попробуйте too_abc.kontoso.net_ навигации.</span><span class="sxs-lookup"><span data-stu-id="a18a5-211">In hello example in hello preceding screenshot, try navigating too_abc.kontoso.net_.</span></span>

<a name="custom" />

## <a name="manage-custom-dns-records"></a><span data-ttu-id="a18a5-212">Управление пользовательскими записями DNS</span><span class="sxs-lookup"><span data-stu-id="a18a5-212">Manage custom DNS records</span></span>

<span data-ttu-id="a18a5-213">В Azure управление записями DNS для домена службы приложений осуществляется с помощью [Azure DNS](https://azure.microsoft.com/services/dns/).</span><span class="sxs-lookup"><span data-stu-id="a18a5-213">In Azure, DNS records for an App Service Domain are managed using [Azure DNS](https://azure.microsoft.com/services/dns/).</span></span> <span data-ttu-id="a18a5-214">Вы можете добавлять, удалять и обновлять записи DNS так же, как для приобретенного внешнего домена.</span><span class="sxs-lookup"><span data-stu-id="a18a5-214">You can add, remove, and update DNS records, just like for an externally purchased domain.</span></span>

### <a name="open-app-service-domain"></a><span data-ttu-id="a18a5-215">Открытие домена службы приложений</span><span class="sxs-lookup"><span data-stu-id="a18a5-215">Open App Service Domain</span></span>

<span data-ttu-id="a18a5-216">В hello hello левого меню портала Azure выберите **более служб** > **доменов приложения службы**.</span><span class="sxs-lookup"><span data-stu-id="a18a5-216">In hello Azure portal, from hello left menu, select **More Services** > **App Service Domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

<span data-ttu-id="a18a5-217">Выберите домен toomanage hello.</span><span class="sxs-lookup"><span data-stu-id="a18a5-217">Select hello domain toomanage.</span></span> 

### <a name="access-dns-zone"></a><span data-ttu-id="a18a5-218">Доступ к зоне DNS</span><span class="sxs-lookup"><span data-stu-id="a18a5-218">Access DNS zone</span></span>

<span data-ttu-id="a18a5-219">В левом меню hello домена, выберите **зоны DNS**.</span><span class="sxs-lookup"><span data-stu-id="a18a5-219">In hello domain's left menu, select **DNS zone**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-dns-zone.png)

<span data-ttu-id="a18a5-220">Это действие открывает hello [зоны DNS](../dns/dns-zones-records.md) страницы службы домена приложения в Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="a18a5-220">This action opens hello [DNS zone](../dns/dns-zones-records.md) page of your App Service Domain in Azure DNS.</span></span> <span data-ttu-id="a18a5-221">Сведения о том, как tooedit DNS-записи, в разделе [как toomanage зоны DNS в hello портал Azure](../dns/dns-operations-dnszones-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a18a5-221">For information on how tooedit DNS records, see [How toomanage DNS Zones in hello Azure portal](../dns/dns-operations-dnszones-portal.md).</span></span>

## <a name="cancel-purchase-delete-domain"></a><span data-ttu-id="a18a5-222">Отмена покупки (удаление домена)</span><span class="sxs-lookup"><span data-stu-id="a18a5-222">Cancel purchase (delete domain)</span></span>

<span data-ttu-id="a18a5-223">После приобретения hello домен приложения службы, у вас есть пять дней toocancel покупки для возмещение.</span><span class="sxs-lookup"><span data-stu-id="a18a5-223">After you purchase hello App Service Domain, you have five days toocancel your purchase for a full refund.</span></span> <span data-ttu-id="a18a5-224">Через пять дней можно удалить hello домен приложения службы, но не может получить возмещение.</span><span class="sxs-lookup"><span data-stu-id="a18a5-224">After five days, you can delete hello App Service Domain, but cannot receive a refund.</span></span>

### <a name="open-app-service-domain"></a><span data-ttu-id="a18a5-225">Открытие домена службы приложений</span><span class="sxs-lookup"><span data-stu-id="a18a5-225">Open App Service Domain</span></span>

<span data-ttu-id="a18a5-226">В hello hello левого меню портала Azure выберите **более служб** > **доменов приложения службы**.</span><span class="sxs-lookup"><span data-stu-id="a18a5-226">In hello Azure portal, from hello left menu, select **More Services** > **App Service Domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

<span data-ttu-id="a18a5-227">Выберите hello tooyou домена требуется toocancel или удалить.</span><span class="sxs-lookup"><span data-stu-id="a18a5-227">Select hello domain tooyou want toocancel or delete.</span></span> 

### <a name="delete-hostname-bindings"></a><span data-ttu-id="a18a5-228">Удаление привязок имен узлов</span><span class="sxs-lookup"><span data-stu-id="a18a5-228">Delete hostname bindings</span></span>

<span data-ttu-id="a18a5-229">В левом меню hello домена, выберите **привязки имени узла**.</span><span class="sxs-lookup"><span data-stu-id="a18a5-229">In hello domain's left menu, select **Hostname bindings**.</span></span> <span data-ttu-id="a18a5-230">Здесь перечислены привязки имени узла Hello из всех служб Azure.</span><span class="sxs-lookup"><span data-stu-id="a18a5-230">hello hostname bindings from all Azure services are listed here.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostname-bindings.png)

<span data-ttu-id="a18a5-231">Не удается удалить hello домен приложения службы, пока не будут удалены все привязки имени узла.</span><span class="sxs-lookup"><span data-stu-id="a18a5-231">You cannot delete hello App Service Domain until all hostname bindings are deleted.</span></span>

<span data-ttu-id="a18a5-232">Удалите каждую привязку имени узла, выбрав **...** > **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="a18a5-232">Delete each hostname binding by selecting **...** > **Delete**.</span></span> <span data-ttu-id="a18a5-233">После удаления всех привязок hello выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="a18a5-233">After all hello bindings are deleted, select **Save**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-delete-hostname-bindings.png)

### <a name="cancel-or-delete"></a><span data-ttu-id="a18a5-234">Отмена или удаление</span><span class="sxs-lookup"><span data-stu-id="a18a5-234">Cancel or delete</span></span>

<span data-ttu-id="a18a5-235">В левом меню hello домена, выберите **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="a18a5-235">In hello domain's left menu, select **Overview**.</span></span> 

<span data-ttu-id="a18a5-236">Если hello отмены в домене приобретенных hello не истекло, выберите **отменить покупку**.</span><span class="sxs-lookup"><span data-stu-id="a18a5-236">If hello cancellation period on hello purchased domain has not elapsed, select **Cancel purchase**.</span></span> <span data-ttu-id="a18a5-237">В противном случае вы увидите кнопку **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="a18a5-237">Otherwise, you see a **Delete** button instead.</span></span> <span data-ttu-id="a18a5-238">домен hello toodelete без возврата, выберите **удалить**.</span><span class="sxs-lookup"><span data-stu-id="a18a5-238">toodelete hello domain without a refund, select **Delete**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-cancel.png)

<span data-ttu-id="a18a5-239">Выберите **ОК** tooconfirm hello операции.</span><span class="sxs-lookup"><span data-stu-id="a18a5-239">Select **OK** tooconfirm hello operation.</span></span> <span data-ttu-id="a18a5-240">Если вы не хотите tooproceed, щелкните за пределами hello диалоговое окно подтверждения.</span><span class="sxs-lookup"><span data-stu-id="a18a5-240">If you don't want tooproceed, click anywhere outside of hello confirmation dialog.</span></span>

<span data-ttu-id="a18a5-241">По завершении операции hello домена hello выпущено из подписки и доступна для тех, кто toopurchase еще раз.</span><span class="sxs-lookup"><span data-stu-id="a18a5-241">After hello operation is complete, hello domain is released from your subscription and available for anyone toopurchase again.</span></span> 
