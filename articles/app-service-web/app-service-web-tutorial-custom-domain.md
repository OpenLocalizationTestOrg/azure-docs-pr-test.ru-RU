---
title: "aaaMap существующие пользовательские DNS имя tooAzure веб-приложений | Документы Microsoft"
description: "Узнайте, как tooadd существующий личный домен DNS имя веб-приложения tooa (именного домена), внутреннего сервера мобильного приложения или приложения API в службе приложений Azure."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: dc446e0e-0958-48ea-8d99-441d2b947a7c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 06/23/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 2c4eea3c56c758ca11355554321ffa52dd2c6b9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="map-an-existing-custom-dns-name-tooazure-web-apps"></a><span data-ttu-id="cadc9-103">Сопоставьте существующий пользовательский DNS имя tooAzure веб-приложений</span><span class="sxs-lookup"><span data-stu-id="cadc9-103">Map an existing custom DNS name tooAzure Web Apps</span></span>

<span data-ttu-id="cadc9-104">[Веб-приложения Azure](app-service-web-overview.md) — это служба веб-размещения с самостоятельной установкой исправлений и высоким уровнем масштабируемости.</span><span class="sxs-lookup"><span data-stu-id="cadc9-104">[Azure Web Apps](app-service-web-overview.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="cadc9-105">Этот учебник показывает, как toomap существующие пользовательские DNS имя tooAzure веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="cadc9-105">This tutorial shows you how toomap an existing custom DNS name tooAzure Web Apps.</span></span>

![Приложение портала навигации tooAzure](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

<span data-ttu-id="cadc9-107">Из этого руководства вы узнаете, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="cadc9-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cadc9-108">Сопоставление поддомена (например, `www.contoso.com`) с помощью записи CNAME.</span><span class="sxs-lookup"><span data-stu-id="cadc9-108">Map a subdomain (for example, `www.contoso.com`) by using a CNAME record</span></span>
> * <span data-ttu-id="cadc9-109">Сопоставление корневого домена (например, `contoso.com`) с помощью записи A.</span><span class="sxs-lookup"><span data-stu-id="cadc9-109">Map a root domain (for example, `contoso.com`) by using an A record</span></span>
> * <span data-ttu-id="cadc9-110">Сопоставление домена с подстановочным знаком (например, `*.contoso.com`) с помощью записи CNAME.</span><span class="sxs-lookup"><span data-stu-id="cadc9-110">Map a wildcard domain (for example, `*.contoso.com`) by using a CNAME record</span></span>
> * <span data-ttu-id="cadc9-111">Автоматизация сопоставления доменов с помощью скриптов.</span><span class="sxs-lookup"><span data-stu-id="cadc9-111">Automate domain mapping with scripts</span></span>

<span data-ttu-id="cadc9-112">Можно использовать любой **запись CNAME** или **запись** toomap пользовательские DNS имя tooApp службы.</span><span class="sxs-lookup"><span data-stu-id="cadc9-112">You can use either a **CNAME record** or an **A record** toomap a custom DNS name tooApp Service.</span></span> 

> [!NOTE]
> <span data-ttu-id="cadc9-113">Мы рекомендуем использовать записи CNAME для всех настраиваемых DNS-имен, кроме корневого домена (например, `contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="cadc9-113">We recommend that you use a CNAME for all custom DNS names except a root domain (for example, `contoso.com`).</span></span>

<span data-ttu-id="cadc9-114">toomigrate действующем сайте и его tooApp имя домена DNS службы, см. раздел [миграции active tooAzure имя DNS службы приложений](app-service-custom-domain-name-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="cadc9-114">toomigrate a live site and its DNS domain name tooApp Service, see [Migrate an active DNS name tooAzure App Service](app-service-custom-domain-name-migrate.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cadc9-115">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="cadc9-115">Prerequisites</span></span>

<span data-ttu-id="cadc9-116">toocomplete этого учебника:</span><span class="sxs-lookup"><span data-stu-id="cadc9-116">toocomplete this tutorial:</span></span>

* <span data-ttu-id="cadc9-117">[Создайте приложение службы приложений](/azure/app-service/) или используйте приложение, созданное для работы с другим руководством.</span><span class="sxs-lookup"><span data-stu-id="cadc9-117">[Create an App Service app](/azure/app-service/), or use an app that you created for another tutorial.</span></span>
* <span data-ttu-id="cadc9-118">Приобретите имени домена и убедитесь, что у вас есть доступ toohello DNS реестра поставщику домена (например, GoDaddy).</span><span class="sxs-lookup"><span data-stu-id="cadc9-118">Purchase a domain name and make sure you have access toohello DNS registry for your domain provider (such as GoDaddy).</span></span>

  <span data-ttu-id="cadc9-119">Например, tooadd DNS-записей для `contoso.com` и `www.contoso.com`, должно быть параметров DNS может tooconfigure hello для hello `contoso.com` корневого домена.</span><span class="sxs-lookup"><span data-stu-id="cadc9-119">For example, tooadd DNS entries for `contoso.com` and `www.contoso.com`, you must be able tooconfigure hello DNS settings for hello `contoso.com` root domain.</span></span>

  > [!NOTE]
  > <span data-ttu-id="cadc9-120">Если у вас нет существующего домена имя, рассмотрите возможность [приобретение домена с помощью портала Azure "hello"](custom-dns-web-site-buydomains-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="cadc9-120">If you don't have an existing domain name, consider [purchasing a domain using hello Azure portal](custom-dns-web-site-buydomains-web-app.md).</span></span> 

## <a name="prepare-hello-app"></a><span data-ttu-id="cadc9-121">Подготовка приложения hello</span><span class="sxs-lookup"><span data-stu-id="cadc9-121">Prepare hello app</span></span>

<span data-ttu-id="cadc9-122">toomap пользовательские DNS имя tooa веб-приложения, веб-приложения hello [план служб приложений](https://azure.microsoft.com/pricing/details/app-service/) должен быть платной уровня (**Shared**, **основные**, **Стандартная**, или  **"Премиум"**).</span><span class="sxs-lookup"><span data-stu-id="cadc9-122">toomap a custom DNS name tooa web app, hello web app's [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be a paid tier (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> <span data-ttu-id="cadc9-123">На этом шаге вы убедитесь, что этого приложения службы, используемой в hello hello поддерживается ценовой категории.</span><span class="sxs-lookup"><span data-stu-id="cadc9-123">In this step, you make sure that hello App Service app is in hello supported pricing tier.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="cadc9-124">Войдите в tooAzure</span><span class="sxs-lookup"><span data-stu-id="cadc9-124">Sign in tooAzure</span></span>

<span data-ttu-id="cadc9-125">Откройте hello [портал Azure](https://portal.azure.com) и выполните вход с учетной записью Azure.</span><span class="sxs-lookup"><span data-stu-id="cadc9-125">Open hello [Azure portal](https://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="navigate-toohello-app-in-hello-azure-portal"></a><span data-ttu-id="cadc9-126">Перейдите в приложение toohello в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="cadc9-126">Navigate toohello app in hello Azure portal</span></span>

<span data-ttu-id="cadc9-127">Hello в левом меню, выберите **службы приложений**, а затем выберите имя hello приложение hello.</span><span class="sxs-lookup"><span data-stu-id="cadc9-127">From hello left menu, select **App Services**, and then select hello name of hello app.</span></span>

![Приложение портала навигации tooAzure](./media/app-service-web-tutorial-custom-domain/select-app.png)

<span data-ttu-id="cadc9-129">Вы увидите страницу управления hello объекта hello приложение служб приложений.</span><span class="sxs-lookup"><span data-stu-id="cadc9-129">You see hello management page of hello App Service app.</span></span>  

<a name="checkpricing"></a>

### <a name="check-hello-pricing-tier"></a><span data-ttu-id="cadc9-130">Проверьте hello ценовой категории</span><span class="sxs-lookup"><span data-stu-id="cadc9-130">Check hello pricing tier</span></span>

<span data-ttu-id="cadc9-131">Hello навигации страницы приложения hello слева, прокрутите toohello **параметры** , выберите **масштаб (план службы приложений)**.</span><span class="sxs-lookup"><span data-stu-id="cadc9-131">In hello left navigation of hello app page, scroll toohello **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Меню увеличения масштаба](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

<span data-ttu-id="cadc9-133">приложение Hello текущего уровня, выделяется синей рамкой.</span><span class="sxs-lookup"><span data-stu-id="cadc9-133">hello app's current tier is highlighted by a blue border.</span></span> <span data-ttu-id="cadc9-134">Убедитесь том, что приложение hello не hello toomake **Free** уровня.</span><span class="sxs-lookup"><span data-stu-id="cadc9-134">Check toomake sure that hello app is not in hello **Free** tier.</span></span> <span data-ttu-id="cadc9-135">Пользовательские DNS не поддерживается в hello **Free** уровня.</span><span class="sxs-lookup"><span data-stu-id="cadc9-135">Custom DNS is not supported in hello **Free** tier.</span></span> 

![Проверка ценовой категории](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

<span data-ttu-id="cadc9-137">Если hello план служб приложений не **Free**, закройте hello **выберите ценовую категорию** страницы и пропуска слишком[сопоставить запись CNAME](#cname).</span><span class="sxs-lookup"><span data-stu-id="cadc9-137">If hello App Service plan is not **Free**, close hello **Choose your pricing tier** page and skip too[Map a CNAME record](#cname).</span></span>

<a name="scaleup"></a>

### <a name="scale-up-hello-app-service-plan"></a><span data-ttu-id="cadc9-138">Вертикальное масштабирование hello план служб приложений</span><span class="sxs-lookup"><span data-stu-id="cadc9-138">Scale up hello App Service plan</span></span>

<span data-ttu-id="cadc9-139">Выберите любой из уровней занятых hello (**Shared**, **основные**, **Стандартная**, или **Premium**).</span><span class="sxs-lookup"><span data-stu-id="cadc9-139">Select any of hello non-free tiers (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> 

<span data-ttu-id="cadc9-140">Нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="cadc9-140">Click **Select**.</span></span>

![Проверка ценовой категории](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

<span data-ttu-id="cadc9-142">При появлении hello после уведомления hello шкалы операция завершена.</span><span class="sxs-lookup"><span data-stu-id="cadc9-142">When you see hello following notification, hello scale operation is complete.</span></span>

![Подтверждение операции масштабирования](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

<a name="cname"></a>

## <a name="map-a-cname-record"></a><span data-ttu-id="cadc9-144">Сопоставление записи CNAME</span><span class="sxs-lookup"><span data-stu-id="cadc9-144">Map a CNAME record</span></span>

<span data-ttu-id="cadc9-145">В примере учебника hello, добавьте запись CNAME для hello `www` поддомен (например, `www.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="cadc9-145">In hello tutorial example, you add a CNAME record for hello `www` subdomain (for example, `www.contoso.com`).</span></span>

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-cname-record"></a><span data-ttu-id="cadc9-146">Создайте запись CNAME hello</span><span class="sxs-lookup"><span data-stu-id="cadc9-146">Create hello CNAME record</span></span>

<span data-ttu-id="cadc9-147">Добавление узла по умолчанию приложения toohello поддомен toomap записей CNAME (`<app_name>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="cadc9-147">Add a CNAME record toomap a subdomain toohello app's default hostname (`<app_name>.azurewebsites.net`).</span></span>

<span data-ttu-id="cadc9-148">Для hello `www.contoso.com` пример домена добавьте запись CNAME, которая сопоставляет имя hello `www` слишком`<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="cadc9-148">For hello `www.contoso.com` domain example, add a CNAME record that maps hello name `www` too`<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="cadc9-149">После добавления hello CNAME страницы записей DNS hello выглядит следующим образом hello в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="cadc9-149">After you add hello CNAME, hello DNS records page looks like hello following example:</span></span>

![Приложение портала навигации tooAzure](./media/app-service-web-tutorial-custom-domain/cname-record.png)

### <a name="enable-hello-cname-record-mapping-in-azure"></a><span data-ttu-id="cadc9-151">Разрешить сопоставление запись CNAME hello в Azure</span><span class="sxs-lookup"><span data-stu-id="cadc9-151">Enable hello CNAME record mapping in Azure</span></span>

<span data-ttu-id="cadc9-152">В hello оставшийся навигации страницы приложения hello hello портал Azure, выберите **пользовательские домены**.</span><span class="sxs-lookup"><span data-stu-id="cadc9-152">In hello left navigation of hello app page in hello Azure portal, select **Custom domains**.</span></span> 

![Меню личных доменов](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="cadc9-154">В hello **пользовательские домены** страницы приложения hello, добавьте hello полное доменное имя настраиваемого DNS (`www.contoso.com`) toohello списка.</span><span class="sxs-lookup"><span data-stu-id="cadc9-154">In hello **Custom domains** page of hello app, add hello fully qualified custom DNS name (`www.contoso.com`) toohello list.</span></span>

<span data-ttu-id="cadc9-155">Выберите hello  **+**  значок Далее слишком**добавить имя узла**.</span><span class="sxs-lookup"><span data-stu-id="cadc9-155">Select hello **+** icon next too**Add hostname**.</span></span>

![Добавление имени узла](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="cadc9-157">Полное доменное имя типа hello, добавлена запись CNAME для, таких как `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="cadc9-157">Type hello fully qualified domain name that you added a CNAME record for, such as `www.contoso.com`.</span></span> 

<span data-ttu-id="cadc9-158">Выберите **Проверка**.</span><span class="sxs-lookup"><span data-stu-id="cadc9-158">Select **Validate**.</span></span>

<span data-ttu-id="cadc9-159">Hello **добавить имя узла** кнопка активна.</span><span class="sxs-lookup"><span data-stu-id="cadc9-159">hello **Add hostname** button is activated.</span></span> 

<span data-ttu-id="cadc9-160">Убедитесь, что **тип записи имени узла** задано слишком**CNAME (www.example.com или любого поддомена)**.</span><span class="sxs-lookup"><span data-stu-id="cadc9-160">Make sure that **Hostname record type** is set too**CNAME (www.example.com or any subdomain)**.</span></span>

<span data-ttu-id="cadc9-161">Выберите **Добавить имя узла**.</span><span class="sxs-lookup"><span data-stu-id="cadc9-161">Select **Add hostname**.</span></span>

![Добавить приложение toohello имя DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

<span data-ttu-id="cadc9-163">Он может занять некоторое время для нового узла toobe hello отражаются в приложение hello **пользовательские домены** страницы.</span><span class="sxs-lookup"><span data-stu-id="cadc9-163">It might take some time for hello new hostname toobe reflected in hello app's **Custom domains** page.</span></span> <span data-ttu-id="cadc9-164">Попробуйте обновить tooupdate hello hello обозревателя данных.</span><span class="sxs-lookup"><span data-stu-id="cadc9-164">Try refreshing hello browser tooupdate hello data.</span></span>

![Запись CNAME добавлена](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

<span data-ttu-id="cadc9-166">Если пропущена операция или сделали опечатку. вы Где-либо ранее, отображается ошибка проверки hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="cadc9-166">If you missed a step or made a typo somewhere earlier, you see a verification error at hello bottom of hello page.</span></span>

![Ошибка проверки](./media/app-service-web-tutorial-custom-domain/verification-error-cname.png)

<a name="a"></a>

## <a name="map-an-a-record"></a><span data-ttu-id="cadc9-168">Сопоставление записи A</span><span class="sxs-lookup"><span data-stu-id="cadc9-168">Map an A record</span></span>

<span data-ttu-id="cadc9-169">В примере учебника hello, добавьте запись A для hello корневого домена (например, `contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="cadc9-169">In hello tutorial example, you add an A record for hello root domain (for example, `contoso.com`).</span></span> 

<a name="info"></a>

### <a name="copy-hello-apps-ip-address"></a><span data-ttu-id="cadc9-170">Скопируйте приложение hello IP-адрес</span><span class="sxs-lookup"><span data-stu-id="cadc9-170">Copy hello app's IP address</span></span>

<span data-ttu-id="cadc9-171">запись A toomap необходимо приложение hello внешний IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="cadc9-171">toomap an A record, you need hello app's external IP address.</span></span> <span data-ttu-id="cadc9-172">Этот IP-адрес можно найти в приложение hello **пользовательские домены** страницу приветствия портал Azure.</span><span class="sxs-lookup"><span data-stu-id="cadc9-172">You can find this IP address in hello app's **Custom domains** page in hello Azure portal.</span></span>

<span data-ttu-id="cadc9-173">В hello оставшийся навигации страницы приложения hello hello портал Azure, выберите **пользовательские домены**.</span><span class="sxs-lookup"><span data-stu-id="cadc9-173">In hello left navigation of hello app page in hello Azure portal, select **Custom domains**.</span></span> 

![Меню личных доменов](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="cadc9-175">В hello **пользовательские домены** скопируйте приложение hello IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="cadc9-175">In hello **Custom domains** page, copy hello app's IP address.</span></span>

![Приложение портала навигации tooAzure](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-a-record"></a><span data-ttu-id="cadc9-177">Создание записи hello</span><span class="sxs-lookup"><span data-stu-id="cadc9-177">Create hello A record</span></span>

<span data-ttu-id="cadc9-178">toomap A записей tooan приложения, службы приложений требуется **два** DNS-записей:</span><span class="sxs-lookup"><span data-stu-id="cadc9-178">toomap an A record tooan app, App Service requires **two** DNS records:</span></span>

- <span data-ttu-id="cadc9-179">**A** записи приложения toohello toomap IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="cadc9-179">An **A** record toomap toohello app's IP address.</span></span>
- <span data-ttu-id="cadc9-180">Объект **TXT** записи узла по умолчанию приложения toohello toomap `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="cadc9-180">A **TXT** record toomap toohello app's default hostname `<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="cadc9-181">Службы приложений данная запись используется только во время настройки, tooverify, что вы являетесь владельцем hello пользовательского домена.</span><span class="sxs-lookup"><span data-stu-id="cadc9-181">App Service uses this record only at configuration time, tooverify that you own hello custom domain.</span></span> <span data-ttu-id="cadc9-182">После проверки и настройки личного домена в службе приложений эту TXT-запись можно удалить.</span><span class="sxs-lookup"><span data-stu-id="cadc9-182">After your custom domain is validated and configured in App Service, you can delete this TXT record.</span></span> 

<span data-ttu-id="cadc9-183">Для hello `contoso.com` пример домена создайте hello A- и TXT записи, в соответствии с toohello в следующей таблице (`@` обычно представляет hello корневой домен).</span><span class="sxs-lookup"><span data-stu-id="cadc9-183">For hello `contoso.com` domain example, create hello A and TXT records according toohello following table (`@` typically represents hello root domain).</span></span> 

| <span data-ttu-id="cadc9-184">Тип записи</span><span class="sxs-lookup"><span data-stu-id="cadc9-184">Record type</span></span> | <span data-ttu-id="cadc9-185">Узел</span><span class="sxs-lookup"><span data-stu-id="cadc9-185">Host</span></span> | <span data-ttu-id="cadc9-186">Значение</span><span class="sxs-lookup"><span data-stu-id="cadc9-186">Value</span></span> |
| - | - | - |
| <span data-ttu-id="cadc9-187">A</span><span class="sxs-lookup"><span data-stu-id="cadc9-187">A</span></span> | `@` | <span data-ttu-id="cadc9-188">IP-адрес из [приложение hello копирования IP-адрес](#info)</span><span class="sxs-lookup"><span data-stu-id="cadc9-188">IP address from [Copy hello app's IP address](#info)</span></span> |
| <span data-ttu-id="cadc9-189">TXT</span><span class="sxs-lookup"><span data-stu-id="cadc9-189">TXT</span></span> | `@` | `<app_name>.azurewebsites.net` |

<span data-ttu-id="cadc9-190">При добавлении записей hello, hello страницы записей DNS выглядит как следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="cadc9-190">When hello records are added, hello DNS records page looks like hello following example:</span></span>

![Страница записей DNS](./media/app-service-web-tutorial-custom-domain/a-record.png)

<a name="enable-a"></a>

### <a name="enable-hello-a-record-mapping-in-hello-app"></a><span data-ttu-id="cadc9-192">Включить запись сопоставления в приложение hello hello</span><span class="sxs-lookup"><span data-stu-id="cadc9-192">Enable hello A record mapping in hello app</span></span>

<span data-ttu-id="cadc9-193">Обратно в приложение hello **пользовательские домены** страницы приветствия портал Azure, добавьте hello полное доменное имя настраиваемого DNS (например, `contoso.com`) toohello списка.</span><span class="sxs-lookup"><span data-stu-id="cadc9-193">Back in hello app's **Custom domains** page in hello Azure portal, add hello fully qualified custom DNS name (for example, `contoso.com`) toohello list.</span></span>

<span data-ttu-id="cadc9-194">Выберите hello  **+**  значок Далее слишком**добавить имя узла**.</span><span class="sxs-lookup"><span data-stu-id="cadc9-194">Select hello **+** icon next too**Add hostname**.</span></span>

![Добавление имени узла](./media/app-service-web-tutorial-custom-domain/add-host-name.png)

<span data-ttu-id="cadc9-196">Тип hello полное доменное имя настройки записи hello A, такие как `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="cadc9-196">Type hello fully qualified domain name that you configured hello A record for, such as `contoso.com`.</span></span>

<span data-ttu-id="cadc9-197">Выберите **Проверка**.</span><span class="sxs-lookup"><span data-stu-id="cadc9-197">Select **Validate**.</span></span>

<span data-ttu-id="cadc9-198">Hello **добавить имя узла** кнопка активна.</span><span class="sxs-lookup"><span data-stu-id="cadc9-198">hello **Add hostname** button is activated.</span></span> 

<span data-ttu-id="cadc9-199">Убедитесь, что **тип записи имени узла** задано слишком**записи (example.com)**.</span><span class="sxs-lookup"><span data-stu-id="cadc9-199">Make sure that **Hostname record type** is set too**A record (example.com)**.</span></span>

<span data-ttu-id="cadc9-200">Выберите **Добавить имя узла**.</span><span class="sxs-lookup"><span data-stu-id="cadc9-200">Select **Add hostname**.</span></span>

![Добавить приложение toohello имя DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name.png)

<span data-ttu-id="cadc9-202">Он может занять некоторое время для нового узла toobe hello отражаются в приложение hello **пользовательские домены** страницы.</span><span class="sxs-lookup"><span data-stu-id="cadc9-202">It might take some time for hello new hostname toobe reflected in hello app's **Custom domains** page.</span></span> <span data-ttu-id="cadc9-203">Попробуйте обновить tooupdate hello hello обозревателя данных.</span><span class="sxs-lookup"><span data-stu-id="cadc9-203">Try refreshing hello browser tooupdate hello data.</span></span>

![Запись добавлена](./media/app-service-web-tutorial-custom-domain/a-record-added.png)

<span data-ttu-id="cadc9-205">Если пропущена операция или сделали опечатку. вы Где-либо ранее, отображается ошибка проверки hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="cadc9-205">If you missed a step or made a typo somewhere earlier, you see a verification error at hello bottom of hello page.</span></span>

![Ошибка проверки](./media/app-service-web-tutorial-custom-domain/verification-error.png)

<a name="wildcard"></a>

## <a name="map-a-wildcard-domain"></a><span data-ttu-id="cadc9-207">Сопоставление домена с подстановочными знаками</span><span class="sxs-lookup"><span data-stu-id="cadc9-207">Map a wildcard domain</span></span>

<span data-ttu-id="cadc9-208">В обучающий пример hello, можно сопоставить [подстановочное DNS-имя](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (например, `*.contoso.com`) toohello приложением служб приложений, добавив запись CNAME.</span><span class="sxs-lookup"><span data-stu-id="cadc9-208">In hello tutorial example, you map a [wildcard DNS name](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (for example, `*.contoso.com`) toohello App Service app by adding a CNAME record.</span></span> 

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-cname-record"></a><span data-ttu-id="cadc9-209">Создайте запись CNAME hello</span><span class="sxs-lookup"><span data-stu-id="cadc9-209">Create hello CNAME record</span></span>

<span data-ttu-id="cadc9-210">Добавление узла по умолчанию приложения имя подстановочные toohello toomap записей CNAME (`<app_name>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="cadc9-210">Add a CNAME record toomap a wildcard name toohello app's default hostname (`<app_name>.azurewebsites.net`).</span></span>

<span data-ttu-id="cadc9-211">Для hello `*.contoso.com` пример домена hello запись CNAME будет сопоставить имя hello `*` слишком`<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="cadc9-211">For hello `*.contoso.com` domain example, hello CNAME record will map hello name `*` too`<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="cadc9-212">При добавлении hello CNAME hello страницы записей DNS выглядит как следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="cadc9-212">When hello CNAME is added, hello DNS records page looks like hello following example:</span></span>

![Приложение портала навигации tooAzure](./media/app-service-web-tutorial-custom-domain/cname-record-wildcard.png)

### <a name="enable-hello-cname-record-mapping-in-hello-app"></a><span data-ttu-id="cadc9-214">Разрешить сопоставление запись CNAME hello в приложение hello</span><span class="sxs-lookup"><span data-stu-id="cadc9-214">Enable hello CNAME record mapping in hello app</span></span>

<span data-ttu-id="cadc9-215">Теперь можно добавить любой дочерний домен, который соответствует приложение toohello имя hello подстановочный знак (например, `sub1.contoso.com` и `sub2.contoso.com` соответствует `*.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="cadc9-215">You can now add any subdomain that matches hello wildcard name toohello app (for example, `sub1.contoso.com` and `sub2.contoso.com` match `*.contoso.com`).</span></span> 

<span data-ttu-id="cadc9-216">В hello оставшийся навигации страницы приложения hello hello портал Azure, выберите **пользовательские домены**.</span><span class="sxs-lookup"><span data-stu-id="cadc9-216">In hello left navigation of hello app page in hello Azure portal, select **Custom domains**.</span></span> 

![Меню личных доменов](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="cadc9-218">Выберите hello  **+**  значок Далее слишком**добавить имя узла**.</span><span class="sxs-lookup"><span data-stu-id="cadc9-218">Select hello **+** icon next too**Add hostname**.</span></span>

![Добавление имени узла](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="cadc9-220">Введите полное доменное имя, которое совпадает с именем домена hello подстановочный знак (например, `sub1.contoso.com`), а затем выберите **проверки**.</span><span class="sxs-lookup"><span data-stu-id="cadc9-220">Type a fully qualified domain name that matches hello wildcard domain (for example, `sub1.contoso.com`), and then select **Validate**.</span></span>

<span data-ttu-id="cadc9-221">Hello **добавить имя узла** кнопка активна.</span><span class="sxs-lookup"><span data-stu-id="cadc9-221">hello **Add hostname** button is activated.</span></span> 

<span data-ttu-id="cadc9-222">Убедитесь, что **тип записи имени узла** задано слишком**запись CNAME (www.example.com или любого поддомена)**.</span><span class="sxs-lookup"><span data-stu-id="cadc9-222">Make sure that **Hostname record type** is set too**CNAME record (www.example.com or any subdomain)**.</span></span>

<span data-ttu-id="cadc9-223">Выберите **Добавить имя узла**.</span><span class="sxs-lookup"><span data-stu-id="cadc9-223">Select **Add hostname**.</span></span>

![Добавить приложение toohello имя DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname-wildcard.png)

<span data-ttu-id="cadc9-225">Он может занять некоторое время для нового узла toobe hello отражаются в приложение hello **пользовательские домены** страницы.</span><span class="sxs-lookup"><span data-stu-id="cadc9-225">It might take some time for hello new hostname toobe reflected in hello app's **Custom domains** page.</span></span> <span data-ttu-id="cadc9-226">Попробуйте обновить tooupdate hello hello обозревателя данных.</span><span class="sxs-lookup"><span data-stu-id="cadc9-226">Try refreshing hello browser tooupdate hello data.</span></span>

<span data-ttu-id="cadc9-227">Выберите hello  **+**  значок снова tooadd другого имени узла, которое совпадает с именем домена hello подстановочный знак.</span><span class="sxs-lookup"><span data-stu-id="cadc9-227">Select hello **+** icon again tooadd another hostname that matches hello wildcard domain.</span></span> <span data-ttu-id="cadc9-228">Например, добавьте `sub2.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="cadc9-228">For example, add `sub2.contoso.com`.</span></span>

![Запись CNAME добавлена](./media/app-service-web-tutorial-custom-domain/cname-record-added-wildcard2.png)

## <a name="test-in-browser"></a><span data-ttu-id="cadc9-230">Тестирование в браузере</span><span class="sxs-lookup"><span data-stu-id="cadc9-230">Test in browser</span></span>

<span data-ttu-id="cadc9-231">Обзор DNS-имен toohello ранее (например, `contoso.com`, `www.contoso.com`, `sub1.contoso.com`, и `sub2.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="cadc9-231">Browse toohello DNS name(s) that you configured earlier (for example, `contoso.com`,  `www.contoso.com`, `sub1.contoso.com`, and `sub2.contoso.com`).</span></span>

![Приложение портала навигации tooAzure](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

## <a name="automate-with-scripts"></a><span data-ttu-id="cadc9-233">Автоматизация с помощью сценариев</span><span class="sxs-lookup"><span data-stu-id="cadc9-233">Automate with scripts</span></span>

<span data-ttu-id="cadc9-234">Можно автоматизировать управление пользовательскими доменами с помощью скриптов, с помощью hello [Azure CLI](/cli/azure/install-azure-cli) или [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="cadc9-234">You can automate management of custom domains with scripts, using hello [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span></span> 

### <a name="azure-cli"></a><span data-ttu-id="cadc9-235">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="cadc9-235">Azure CLI</span></span> 

<span data-ttu-id="cadc9-236">Hello, следующая команда добавляет настроенное пользовательские DNS имя tooan приложением служб приложений.</span><span class="sxs-lookup"><span data-stu-id="cadc9-236">hello following command adds a configured custom DNS name tooan App Service app.</span></span> 

```bash 
az appservice web config hostname add \
    --webapp <app_name> \
    --resource-group <resource_group_name> \ 
    --name <fully_qualified_domain_name> 
``` 

<span data-ttu-id="cadc9-237">Дополнительные сведения см. в разделе [карты веб-приложения tooa пользовательского домена](scripts/app-service-cli-configure-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="cadc9-237">For more information, see [Map a custom domain tooa web app](scripts/app-service-cli-configure-custom-domain.md).</span></span> 

### <a name="azure-powershell"></a><span data-ttu-id="cadc9-238">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="cadc9-238">Azure PowerShell</span></span> 

<span data-ttu-id="cadc9-239">Hello, следующая команда добавляет настроенное пользовательские DNS имя tooan приложением служб приложений.</span><span class="sxs-lookup"><span data-stu-id="cadc9-239">hello following command adds a configured custom DNS name tooan App Service app.</span></span> 

```PowerShell  
Set-AzureRmWebApp `
    -Name <app_name> `
    -ResourceGroupName <resource_group_name> ` 
    -HostNames @("<fully_qualified_domain_name>","<app_name>.azurewebsites.net") 
```

<span data-ttu-id="cadc9-240">Дополнительные сведения см. в разделе [назначить веб-приложения пользовательского домена tooa](scripts/app-service-powershell-configure-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="cadc9-240">For more information, see [Assign a custom domain tooa web app](scripts/app-service-powershell-configure-custom-domain.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cadc9-241">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cadc9-241">Next steps</span></span>

<span data-ttu-id="cadc9-242">Из этого руководства вы узнали, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="cadc9-242">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cadc9-243">Сопоставление поддомена с помощью записи CNAME.</span><span class="sxs-lookup"><span data-stu-id="cadc9-243">Map a subdomain by using a CNAME record</span></span>
> * <span data-ttu-id="cadc9-244">Сопоставление корневого домена с помощью записи A.</span><span class="sxs-lookup"><span data-stu-id="cadc9-244">Map a root domain by using an A record</span></span>
> * <span data-ttu-id="cadc9-245">Сопоставление домена с подстановочным знаком с помощью записи CNAME.</span><span class="sxs-lookup"><span data-stu-id="cadc9-245">Map a wildcard domain by using a CNAME record</span></span>
> * <span data-ttu-id="cadc9-246">Автоматизация сопоставления доменов с помощью скриптов.</span><span class="sxs-lookup"><span data-stu-id="cadc9-246">Automate domain mapping with scripts</span></span>

<span data-ttu-id="cadc9-247">Переместить следующий учебник toolearn toohello как toobind пользовательские SSL-сертификат tooa веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="cadc9-247">Advance toohello next tutorial toolearn how toobind a custom SSL certificate tooa web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cadc9-248">Привязать существующий пользовательский SSL сертификат tooAzure веб-приложений</span><span class="sxs-lookup"><span data-stu-id="cadc9-248">Bind an existing custom SSL certificate tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-ssl.md)
