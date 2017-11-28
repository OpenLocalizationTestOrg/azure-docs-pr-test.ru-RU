---
title: "aaaAdd tooan CDN службе приложений Azure | Документы Microsoft"
description: "Добавьте toocache службе приложений Azure tooan сети доставки содержимого (CDN) и подготовить статические файлы с серверов закрыть tooyour клиентам по всему Здравствуй, мир."
services: app-service\web
author: syntaxc4
ms.author: cfowler
ms.date: 05/31/2017
ms.topic: tutorial
ms.service: app-service-web
manager: erikre
ms.workload: web
ms.custom: mvc
ms.openlocfilehash: 88b7fd884517279064472b804a6d1dc2921cbd24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-content-delivery-network-cdn-tooan-azure-app-service"></a><span data-ttu-id="24843-103">Добавление сети доставки содержимого (CDN) tooan службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="24843-103">Add a Content Delivery Network (CDN) tooan Azure App Service</span></span>

<span data-ttu-id="24843-104">[Azure сеть доставки содержимого (CDN)](../cdn/cdn-overview.md) кэширует статического веб-содержимого в стратегически расположенных пунктах tooprovide максимальную пропускную способность для доставки содержимого toousers.</span><span class="sxs-lookup"><span data-stu-id="24843-104">[Azure Content Delivery Network (CDN)](../cdn/cdn-overview.md) caches static web content at strategically placed locations tooprovide maximum throughput for delivering content toousers.</span></span> <span data-ttu-id="24843-105">Hello CDN также уменьшает нагрузку на сервер на веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="24843-105">hello CDN also decreases server load on your web app.</span></span> <span data-ttu-id="24843-106">В этом учебнике показано как Azure CDN tooa tooadd [веб-приложения в службе приложений Azure](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="24843-106">This tutorial shows how tooadd Azure CDN tooa [web app in Azure App Service](app-service-web-overview.md).</span></span> 

<span data-ttu-id="24843-107">Вот hello Домашняя страница hello образец статических HTML узла, который вы будете работать с:</span><span class="sxs-lookup"><span data-stu-id="24843-107">Here's hello home page of hello sample static HTML site that you'll work with:</span></span>

![Домашняя страница примера приложения](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page.png)

<span data-ttu-id="24843-109">Из этого руководства вы узнаете, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="24843-109">What you'll learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="24843-110">создание конечной точки CDN;</span><span class="sxs-lookup"><span data-stu-id="24843-110">Create a CDN endpoint.</span></span>
> * <span data-ttu-id="24843-111">обновление кэшированных ресурсов;</span><span class="sxs-lookup"><span data-stu-id="24843-111">Refresh cached assets.</span></span>
> * <span data-ttu-id="24843-112">Использовать запрос строк в кэше toocontrol версии.</span><span class="sxs-lookup"><span data-stu-id="24843-112">Use query strings toocontrol cached versions.</span></span>
> * <span data-ttu-id="24843-113">Используйте настраиваемый домен для конечной точки CDN hello.</span><span class="sxs-lookup"><span data-stu-id="24843-113">Use a custom domain for hello CDN endpoint.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24843-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="24843-114">Prerequisites</span></span>

<span data-ttu-id="24843-115">toocomplete этого учебника:</span><span class="sxs-lookup"><span data-stu-id="24843-115">toocomplete this tutorial:</span></span>

- <span data-ttu-id="24843-116">[установите Git](https://git-scm.com/);</span><span class="sxs-lookup"><span data-stu-id="24843-116">[Install Git](https://git-scm.com/)</span></span>
- <span data-ttu-id="24843-117">[Установите Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="24843-117">[Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-hello-web-app"></a><span data-ttu-id="24843-118">Создать веб-приложение hello</span><span class="sxs-lookup"><span data-stu-id="24843-118">Create hello web app</span></span>

<span data-ttu-id="24843-119">toocreate hello веб-приложение, вы будете работать с hello выполните [статических HTML краткое руководство](app-service-web-get-started-html.md) через hello **toohello приложения обзора** шаг.</span><span class="sxs-lookup"><span data-stu-id="24843-119">toocreate hello web app that you'll work with, follow hello [static HTML quickstart](app-service-web-get-started-html.md) through hello **Browse toohello app** step.</span></span>

### <a name="have-a-custom-domain-ready"></a><span data-ttu-id="24843-120">Подготовка личного домена</span><span class="sxs-lookup"><span data-stu-id="24843-120">Have a custom domain ready</span></span>

<span data-ttu-id="24843-121">шаг настраиваемого домена hello toocomplete этого учебника требуется tooown пользовательского домена и иметь доступ tooyour DNS реестра для поставщика домена (например, GoDaddy).</span><span class="sxs-lookup"><span data-stu-id="24843-121">toocomplete hello custom domain step of this tutorial, you need tooown a custom domain and have access tooyour DNS registry for your domain provider (such as GoDaddy).</span></span> <span data-ttu-id="24843-122">Например, tooadd DNS-записей для `contoso.com` и `www.contoso.com`, должен иметь параметры доступа tooconfigure hello DNS для hello `contoso.com` корневого домена.</span><span class="sxs-lookup"><span data-stu-id="24843-122">For example, tooadd DNS entries for `contoso.com` and `www.contoso.com`, you must have access tooconfigure hello DNS settings for hello `contoso.com` root domain.</span></span>

<span data-ttu-id="24843-123">Если у вас еще нет имени домена, попробуйте выполнить hello [учебника домена службы приложений](custom-dns-web-site-buydomains-web-app.md) toopurchase домена с помощью hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="24843-123">If you don't already have a domain name, consider following hello [App Service domain tutorial](custom-dns-web-site-buydomains-web-app.md) toopurchase a domain using hello Azure portal.</span></span> 

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="24843-124">Войдите в toohello портал Azure</span><span class="sxs-lookup"><span data-stu-id="24843-124">Log in toohello Azure portal</span></span>

<span data-ttu-id="24843-125">Откройте браузер и перейдите toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="24843-125">Open a browser and navigate toohello [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-a-cdn-profile-and-endpoint"></a><span data-ttu-id="24843-126">Создание профиля CDN и конечной точки</span><span class="sxs-lookup"><span data-stu-id="24843-126">Create a CDN profile and endpoint</span></span>

<span data-ttu-id="24843-127">В hello навигации слева, выберите **службы приложений**и выберите приложение hello, созданную в hello [статических HTML краткое руководство](app-service-web-get-started-html.md).</span><span class="sxs-lookup"><span data-stu-id="24843-127">In hello left navigation, select **App Services**, and then select hello app that you created in hello [static HTML quickstart](app-service-web-get-started-html.md).</span></span>

![Выберите приложение служб приложений портала hello](media/app-service-web-tutorial-content-delivery-network/portal-select-app-services.png)

<span data-ttu-id="24843-129">В hello **службы приложений** страницы в hello **параметры** выберите **сетевые подключения > Настройка Azure CDN для вашего приложения**.</span><span class="sxs-lookup"><span data-stu-id="24843-129">In hello **App Service** page, in hello **Settings** section, select **Networking > Configure Azure CDN for your app**.</span></span>

![Выберите CDN hello портала](media/app-service-web-tutorial-content-delivery-network/portal-select-cdn.png)

<span data-ttu-id="24843-131">В hello **сети доставки содержимого Azure** укажите hello **новую конечную точку** параметры, как указано в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="24843-131">In hello **Azure Content Delivery Network** page, provide hello **New endpoint** settings as specified in hello table.</span></span>

![Создание профиля и конечной точки на портале hello](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint.png)

| <span data-ttu-id="24843-133">Настройка</span><span class="sxs-lookup"><span data-stu-id="24843-133">Setting</span></span> | <span data-ttu-id="24843-134">Рекомендуемое значение</span><span class="sxs-lookup"><span data-stu-id="24843-134">Suggested value</span></span> | <span data-ttu-id="24843-135">Описание</span><span class="sxs-lookup"><span data-stu-id="24843-135">Description</span></span> |
| ------- | --------------- | ----------- |
| <span data-ttu-id="24843-136">**Профиль CDN**</span><span class="sxs-lookup"><span data-stu-id="24843-136">**CDN profile**</span></span> | <span data-ttu-id="24843-137">myCDNProfile</span><span class="sxs-lookup"><span data-stu-id="24843-137">myCDNProfile</span></span> | <span data-ttu-id="24843-138">Выберите **создать новый** toocreate профиля CDN.</span><span class="sxs-lookup"><span data-stu-id="24843-138">Select **Create new** toocreate a CDN profile.</span></span> <span data-ttu-id="24843-139">Профиль CDN-это набор конечных точек CDN с hello же ценовой категории.</span><span class="sxs-lookup"><span data-stu-id="24843-139">A CDN profile is a collection of CDN endpoints with hello same pricing tier.</span></span> |
| <span data-ttu-id="24843-140">**Ценовая категория**</span><span class="sxs-lookup"><span data-stu-id="24843-140">**Pricing tier**</span></span> | <span data-ttu-id="24843-141">Akamai уровня "Стандартный"</span><span class="sxs-lookup"><span data-stu-id="24843-141">Standard Akamai</span></span> | <span data-ttu-id="24843-142">Hello [ценовой категории](../cdn/cdn-overview.md#azure-cdn-features) указывает hello поставщика и новых возможностей.</span><span class="sxs-lookup"><span data-stu-id="24843-142">hello [pricing tier](../cdn/cdn-overview.md#azure-cdn-features) specifies hello provider and available features.</span></span> <span data-ttu-id="24843-143">В этом руководстве используется ценовая категория Akamai уровня "Стандартный".</span><span class="sxs-lookup"><span data-stu-id="24843-143">In this tutorial, we are using Standard Akamai.</span></span> |
| <span data-ttu-id="24843-144">**Имя конечной точки CDN**</span><span class="sxs-lookup"><span data-stu-id="24843-144">**CDN endpoint name**</span></span> | <span data-ttu-id="24843-145">Любое имя, которое является уникальным в домене azureedge.net hello</span><span class="sxs-lookup"><span data-stu-id="24843-145">Any name that is unique in hello azureedge.net domain</span></span> | <span data-ttu-id="24843-146">Доступ кэшированные ресурсы в домене hello  *\<endpointname >. azureedge.net*.</span><span class="sxs-lookup"><span data-stu-id="24843-146">You access your cached resources at hello domain *\<endpointname>.azureedge.net*.</span></span>

<span data-ttu-id="24843-147">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="24843-147">Select **Create**.</span></span>

<span data-ttu-id="24843-148">Azure создает профиль hello и конечной точки.</span><span class="sxs-lookup"><span data-stu-id="24843-148">Azure creates hello profile and endpoint.</span></span> <span data-ttu-id="24843-149">появляется новая конечная точка Hello в hello **конечные точки** списке hello одной странице, и при его подготовке hello состояние **под управлением**.</span><span class="sxs-lookup"><span data-stu-id="24843-149">hello new endpoint appears in hello **Endpoints** list on hello same page, and when it's provisioned hello status is **Running**.</span></span>

![Новая конечная точка в списке](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint-in-list.png)

### <a name="test-hello-cdn-endpoint"></a><span data-ttu-id="24843-151">Тест hello конечной точки CDN</span><span class="sxs-lookup"><span data-stu-id="24843-151">Test hello CDN endpoint</span></span>

<span data-ttu-id="24843-152">Если выбрать ценовую категорию Verizon, распространение конечной точки может занять около 90 минут.</span><span class="sxs-lookup"><span data-stu-id="24843-152">If you selected Verizon pricing tier, it typically takes about 90 minutes for endpoint propagation.</span></span> <span data-ttu-id="24843-153">В ценовой категории Akamai распространение длится несколько минут.</span><span class="sxs-lookup"><span data-stu-id="24843-153">For Akamai, it takes a couple minutes for propagation</span></span>

<span data-ttu-id="24843-154">содержит пример приложения Hello `index.html` файла и *css*, *img*, и *js* папки, содержащие другие статические активы.</span><span class="sxs-lookup"><span data-stu-id="24843-154">hello sample app has an `index.html` file and *css*, *img*, and *js* folders that contain other static assets.</span></span> <span data-ttu-id="24843-155">Hello содержимого, что пути для всех этих файлов являются одинаковыми hello в конечной точке CDN hello.</span><span class="sxs-lookup"><span data-stu-id="24843-155">hello content paths for all of these files are hello same at hello CDN endpoint.</span></span> <span data-ttu-id="24843-156">Например, обе следующие URL-адреса hello доступ hello *bootstrap.css* файла в hello *css* папки:</span><span class="sxs-lookup"><span data-stu-id="24843-156">For example, both of hello following URLs access hello *bootstrap.css* file in hello *css* folder:</span></span>

```
http://<appname>.azurewebsites.net/css/bootstrap.css
```

```
http://<endpointname>.azureedge.net/css/bootstrap.css
```

<span data-ttu-id="24843-157">Найдите toohello браузера, URL-адреса:</span><span class="sxs-lookup"><span data-stu-id="24843-157">Navigate a browser toohello following URL:</span></span>

```
http://<endpointname>.azureedge.net/index.html
```

![Домашняя страница примера приложения, которая передается из CDN](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page-cdn.png)

 <span data-ttu-id="24843-159">Вы увидите hello же страницу, что вы выполняли ранее в Azure веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="24843-159">You see hello same page that you ran earlier in an Azure web app.</span></span> <span data-ttu-id="24843-160">Azure CDN извлеченные активы hello источника веб-приложения и обслуживает их из конечной точки CDN hello</span><span class="sxs-lookup"><span data-stu-id="24843-160">Azure CDN has retrieved hello origin web app's assets and is serving them from hello CDN endpoint</span></span>

<span data-ttu-id="24843-161">tooensure, что эта страница кэшируется в hello CDN, обновите страницу приветствия.</span><span class="sxs-lookup"><span data-stu-id="24843-161">tooensure that this page is cached in hello CDN, refresh hello page.</span></span> <span data-ttu-id="24843-162">Два запросах hello одного средства необходимы иногда для hello CDN toocache hello запрошенного содержимого.</span><span class="sxs-lookup"><span data-stu-id="24843-162">Two requests for hello same asset are sometimes required for hello CDN toocache hello requested content.</span></span>

<span data-ttu-id="24843-163">Дополнительные сведения о создании профилей и конечных точек Azure CDN см. в статье [Начало работы с Azure CDN](../cdn/cdn-create-new-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="24843-163">For more information about creating Azure CDN profiles and endpoints, see [Getting started with Azure CDN](../cdn/cdn-create-new-endpoint.md).</span></span>

## <a name="purge-hello-cdn"></a><span data-ttu-id="24843-164">Очистка hello CDN</span><span class="sxs-lookup"><span data-stu-id="24843-164">Purge hello CDN</span></span>

<span data-ttu-id="24843-165">Hello CDN периодически обновляет его ресурсы из hello источника веб-приложения на основе hello срока жизни (TTL) конфигурации.</span><span class="sxs-lookup"><span data-stu-id="24843-165">hello CDN periodically refreshes its resources from hello origin web app based on hello time-to-live (TTL) configuration.</span></span> <span data-ttu-id="24843-166">TTL по умолчанию Hello составляет семь дней.</span><span class="sxs-lookup"><span data-stu-id="24843-166">hello default TTL is seven days.</span></span>

<span data-ttu-id="24843-167">В некоторых случаях может потребоваться toorefresh hello CDN перед hello TTL истечение срока действия — например, при развертывании обновленного toohello содержимого веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="24843-167">At times you might need toorefresh hello CDN before hello TTL expiration -- for example, when you deploy updated content toohello web app.</span></span> <span data-ttu-id="24843-168">tootrigger обновления можно вручную очистить ресурсы CDN hello.</span><span class="sxs-lookup"><span data-stu-id="24843-168">tootrigger a refresh, you can manually purge hello CDN resources.</span></span> 

<span data-ttu-id="24843-169">В этом разделе учебника hello развертывание веб-приложения toohello изменений и очистка hello CDN tootrigger hello CDN toorefresh свой кэш.</span><span class="sxs-lookup"><span data-stu-id="24843-169">In this section of hello tutorial, you deploy a change toohello web app and purge hello CDN tootrigger hello CDN toorefresh its cache.</span></span>

### <a name="deploy-a-change-toohello-web-app"></a><span data-ttu-id="24843-170">Развертывание изменений toohello веб-приложения</span><span class="sxs-lookup"><span data-stu-id="24843-170">Deploy a change toohello web app</span></span>

<span data-ttu-id="24843-171">Откройте hello `index.html` и добавьте «-V2 «заголовок toohello H1, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="24843-171">Open hello `index.html` file and add "- V2" toohello H1 heading, as shown in hello following example:</span></span> 

```
<h1>Azure App Service - Sample Static HTML Site - V2</h1>
```

<span data-ttu-id="24843-172">Зафиксировать внесенные изменения и развернуть ее toohello веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="24843-172">Commit your change and deploy it toohello web app.</span></span>

```bash
git commit -am "version 2"
git push azure master
```

<span data-ttu-id="24843-173">После завершения развертывания обзора toohello URL-адрес приложения отобразится изменить hello.</span><span class="sxs-lookup"><span data-stu-id="24843-173">Once deployment has completed, browse toohello web app URL and you see hello change.</span></span>

```
http://<appname>.azurewebsites.net/index.html
```

![Элемент "V2" в заголовке веб-приложения](media/app-service-web-tutorial-content-delivery-network/v2-in-web-app-title.png)

<span data-ttu-id="24843-175">Обзор toohello конечной точки CDN URL-адрес для домашней страницы приветствия и вы не видите hello изменить, так как кэшированная версия hello в hello CDN еще не истек.</span><span class="sxs-lookup"><span data-stu-id="24843-175">Browse toohello CDN endpoint URL for hello home page and you don't see hello change because hello cached version in hello CDN hasn't expired yet.</span></span> 

```
http://<endpointname>.azureedge.net/index.html
```

![В заголовке в CDN нет элемента "V2"](media/app-service-web-tutorial-content-delivery-network/no-v2-in-cdn-title.png)

### <a name="purge-hello-cdn-in-hello-portal"></a><span data-ttu-id="24843-177">Очистка hello CDN hello портала</span><span class="sxs-lookup"><span data-stu-id="24843-177">Purge hello CDN in hello portal</span></span>

<span data-ttu-id="24843-178">tootrigger hello его кэшированная версия CDN tooupdate, удалите hello CDN.</span><span class="sxs-lookup"><span data-stu-id="24843-178">tootrigger hello CDN tooupdate its cached version, purge hello CDN.</span></span>

<span data-ttu-id="24843-179">Hello портала левой навигационной панели, выберите **групп ресурсов**, а затем выберите группу ресурсов hello, созданный для веб-приложения (myResourceGroup).</span><span class="sxs-lookup"><span data-stu-id="24843-179">In hello portal left navigation, select **Resource groups**, and then select hello resource group that you created for your web app (myResourceGroup).</span></span>

![Выбор группы ресурсов](media/app-service-web-tutorial-content-delivery-network/portal-select-group.png)

<span data-ttu-id="24843-181">Выберите конечную точку CDN hello списка ресурсов.</span><span class="sxs-lookup"><span data-stu-id="24843-181">In hello list of resources, select your CDN endpoint.</span></span>

![Выбор конечной точки](media/app-service-web-tutorial-content-delivery-network/portal-select-endpoint.png)

<span data-ttu-id="24843-183">Вверху hello hello **конечной точки** щелкните **очистки**.</span><span class="sxs-lookup"><span data-stu-id="24843-183">At hello top of hello **Endpoint** page, click **Purge**.</span></span>

![Нажатие кнопки "Очистить"](media/app-service-web-tutorial-content-delivery-network/portal-select-purge.png)

<span data-ttu-id="24843-185">Ввод пути к содержимому hello, нужно toopurge.</span><span class="sxs-lookup"><span data-stu-id="24843-185">Enter hello content paths you wish toopurge.</span></span> <span data-ttu-id="24843-186">Можно передать toopurge полный путь файла по отдельности или toopurge сегмента пути и обновить все содержимое в папке.</span><span class="sxs-lookup"><span data-stu-id="24843-186">You can pass a complete file path toopurge an individual file, or a path segment toopurge and refresh all content in a folder.</span></span> <span data-ttu-id="24843-187">Поскольку вы изменили `index.html`, убедитесь, что это один из путей hello.</span><span class="sxs-lookup"><span data-stu-id="24843-187">Since you changed `index.html`, make sure that is one of hello paths.</span></span>

<span data-ttu-id="24843-188">Hello нижней части страницы приветствия, выберите **очистки**.</span><span class="sxs-lookup"><span data-stu-id="24843-188">At hello bottom of hello page, select **Purge**.</span></span>

![Страница очистки](media/app-service-web-tutorial-content-delivery-network/app-service-web-purge-cdn.png)

### <a name="verify-that-hello-cdn-is-updated"></a><span data-ttu-id="24843-190">Убедитесь, что hello обновления CDN</span><span class="sxs-lookup"><span data-stu-id="24843-190">Verify that hello CDN is updated</span></span>

<span data-ttu-id="24843-191">Подождите, пока запрос очистку hello завершает обработку, обычно за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="24843-191">Wait until hello purge request finishes processing, typically a couple of minutes.</span></span> <span data-ttu-id="24843-192">toosee hello текущее состояние, выберите hello значок колокольчика вверху hello страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="24843-192">toosee hello current status, select hello bell icon at hello top of hello page.</span></span> 

![Уведомление об очистке](media/app-service-web-tutorial-content-delivery-network/portal-purge-notification.png)

<span data-ttu-id="24843-194">Обзор URL-адрес конечной точки CDN toohello для `index.html`, и вы увидите hello V2, что добавлен заголовок toohello на домашней странице приветствия.</span><span class="sxs-lookup"><span data-stu-id="24843-194">Browse toohello CDN endpoint URL for `index.html`, and now you see hello V2 that you added toohello title on hello home page.</span></span> <span data-ttu-id="24843-195">Это значит, что обновления кэша CDN hello.</span><span class="sxs-lookup"><span data-stu-id="24843-195">This shows that hello CDN cache has been refreshed.</span></span>

```
http://<endpointname>.azureedge.net/index.html
```

!["V2" в заголовке в CDN](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title.png)

<span data-ttu-id="24843-197">Дополнительные сведения см. в статье [Очистка конечной точки сети CDN Azure](../cdn/cdn-purge-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="24843-197">For more information, see [Purge an Azure CDN endpoint](../cdn/cdn-purge-endpoint.md).</span></span> 

## <a name="use-query-strings-tooversion-content"></a><span data-ttu-id="24843-198">Использование содержимого tooversion строки запроса</span><span class="sxs-lookup"><span data-stu-id="24843-198">Use query strings tooversion content</span></span>

<span data-ttu-id="24843-199">Hello Azure CDN предлагает следующие варианты кэширования поведение hello.</span><span class="sxs-lookup"><span data-stu-id="24843-199">hello Azure CDN offers hello following caching behavior options:</span></span>

* <span data-ttu-id="24843-200">игнорировать строки запросов;</span><span class="sxs-lookup"><span data-stu-id="24843-200">Ignore query strings</span></span>
* <span data-ttu-id="24843-201">обходить кэширование для строк запросов;</span><span class="sxs-lookup"><span data-stu-id="24843-201">Bypass caching for query strings</span></span>
* <span data-ttu-id="24843-202">кэшировать все уникальные URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="24843-202">Cache every unique URL</span></span> 

<span data-ttu-id="24843-203">Здравствуйте, сначала из них — по умолчанию hello, то есть только один кэшированная версия актива независимо от hello строки запроса в URL-адрес hello.</span><span class="sxs-lookup"><span data-stu-id="24843-203">hello first of these is hello default, which means there is only one cached version of an asset regardless of hello query string in hello URL.</span></span> 

<span data-ttu-id="24843-204">В этом разделе учебника hello изменить hello кэширование toocache поведение каждый уникальный URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="24843-204">In this section of hello tutorial, you change hello caching behavior toocache every unique URL.</span></span>

### <a name="change-hello-cache-behavior"></a><span data-ttu-id="24843-205">Изменить поведение кэширования hello</span><span class="sxs-lookup"><span data-stu-id="24843-205">Change hello cache behavior</span></span>

<span data-ttu-id="24843-206">В hello портал Azure **конечной точки CDN** выберите **кэша**.</span><span class="sxs-lookup"><span data-stu-id="24843-206">In hello Azure portal **CDN Endpoint** page, select **Cache**.</span></span>

<span data-ttu-id="24843-207">Выберите **кэшировать каждый уникальный URL-адрес** из hello **режим кэширования строк запросов** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="24843-207">Select **Cache every unique URL** from hello **Query string caching behavior** drop-down list.</span></span>

<span data-ttu-id="24843-208">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="24843-208">Select **Save**.</span></span>

![Выбор режима кэширования строки запроса](media/app-service-web-tutorial-content-delivery-network/portal-select-caching-behavior.png)

### <a name="verify-that-unique-urls-are-cached-separately"></a><span data-ttu-id="24843-210">Проверка кэширования уникальных URL-адресов по отдельности</span><span class="sxs-lookup"><span data-stu-id="24843-210">Verify that unique URLs are cached separately</span></span>

<span data-ttu-id="24843-211">В браузере перейдите на домашнюю страницу toohello в конечной точке CDN hello, но включать строки запроса:</span><span class="sxs-lookup"><span data-stu-id="24843-211">In a browser, navigate toohello home page at hello CDN endpoint, but include a query string:</span></span> 

```
http://<endpointname>.azureedge.net/index.html?q=1
```

<span data-ttu-id="24843-212">Hello CDN возвращает hello текущего веб-приложения содержимого, включая «Версии 2» в заголовке hello.</span><span class="sxs-lookup"><span data-stu-id="24843-212">hello CDN returns hello current web app content, which includes "V2" in hello heading.</span></span> 

<span data-ttu-id="24843-213">tooensure, что эта страница кэшируется в hello CDN, обновите страницу приветствия.</span><span class="sxs-lookup"><span data-stu-id="24843-213">tooensure that this page is cached in hello CDN, refresh hello page.</span></span> 

<span data-ttu-id="24843-214">Откройте `index.html` и измените «Версии 2», слишком «V3» и развернуть изменение hello.</span><span class="sxs-lookup"><span data-stu-id="24843-214">Open `index.html` and change "V2" too"V3", and deploy hello change.</span></span> 

```bash
git commit -am "version 3"
git push azure master
```

<span data-ttu-id="24843-215">В браузере перейдите URL-адрес конечной точки CDN toohello с новой строки запроса, такие как `q=2`.</span><span class="sxs-lookup"><span data-stu-id="24843-215">In a browser, go toohello CDN endpoint URL with a new query string such as `q=2`.</span></span> <span data-ttu-id="24843-216">Hello CDN возвращает текущий hello `index.html` и отображает «V3».</span><span class="sxs-lookup"><span data-stu-id="24843-216">hello CDN gets hello current `index.html` file and displays "V3".</span></span>  <span data-ttu-id="24843-217">Однако после перехода конечной точки CDN toohello с hello `q=1` строка запроса отображается «V2».</span><span class="sxs-lookup"><span data-stu-id="24843-217">But if you navigate toohello CDN endpoint with hello `q=1` query string, you see "V2".</span></span>

```
http://<endpointname>.azureedge.net/index.html?q=2
```

!["V3" в заголовке CDN, строка запроса 2](media/app-service-web-tutorial-content-delivery-network/v3-in-cdn-title-qs2.png)

```
http://<endpointname>.azureedge.net/index.html?q=1
```

!["V2" в заголовке CDN, строка запроса 1](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title-qs1.png)

<span data-ttu-id="24843-220">Этот результат показывает, что каждая строка запроса обрабатывается по-разному:</span><span class="sxs-lookup"><span data-stu-id="24843-220">This output shows that each query string is treated differently:</span></span>

* <span data-ttu-id="24843-221">строка "q=1" использовалась ранее, поэтому возвращается кэшированное содержимое (V2);</span><span class="sxs-lookup"><span data-stu-id="24843-221">q=1 was used before, so cached contents are returned (V2).</span></span>
* <span data-ttu-id="24843-222">q = 2 является новым, поэтому содержимое приложения web последнюю hello, извлекаются и возвращается (V3).</span><span class="sxs-lookup"><span data-stu-id="24843-222">q=2 is new, so hello latest web app contents are retrieved and returned (V3).</span></span>

<span data-ttu-id="24843-223">Дополнительные сведения см. в статье [Управление режимом кэширования Azure CDN с помощью строк запросов](../cdn/cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="24843-223">For more information, see [Control Azure CDN caching behavior with query strings](../cdn/cdn-query-string.md).</span></span>

## <a name="map-a-custom-domain-tooa-cdn-endpoint"></a><span data-ttu-id="24843-224">Сопоставить конечную точку CDN tooa пользовательского домена</span><span class="sxs-lookup"><span data-stu-id="24843-224">Map a custom domain tooa CDN endpoint</span></span>

<span data-ttu-id="24843-225">Необходимо сопоставить ваш пользовательский домен tooyour конечной точки CDN, создав запись CNAME.</span><span class="sxs-lookup"><span data-stu-id="24843-225">You'll map your custom domain tooyour CDN Endpoint by creating a CNAME record.</span></span> <span data-ttu-id="24843-226">Запись CNAME является функцией DNS, которая сопоставляет исходный домен tooa целевой домен.</span><span class="sxs-lookup"><span data-stu-id="24843-226">A CNAME record is a DNS feature that maps a source domain tooa destination domain.</span></span> <span data-ttu-id="24843-227">Например, можно сопоставить `cdn.contoso.com` или `static.contoso.com` слишком`contoso.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="24843-227">For example, you might map `cdn.contoso.com` or `static.contoso.com` too`contoso.azureedge.net`.</span></span>

<span data-ttu-id="24843-228">Если настраиваемый домен отсутствует, попробуйте выполнить hello [учебника домена службы приложений](custom-dns-web-site-buydomains-web-app.md) toopurchase домена с помощью hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="24843-228">If you don't have a custom domain, consider following hello [App Service domain tutorial](custom-dns-web-site-buydomains-web-app.md) toopurchase a domain using hello Azure portal.</span></span> 

### <a name="find-hello-hostname-toouse-with-hello-cname"></a><span data-ttu-id="24843-229">Найти hello toouse имя узла с hello CNAME</span><span class="sxs-lookup"><span data-stu-id="24843-229">Find hello hostname toouse with hello CNAME</span></span>

<span data-ttu-id="24843-230">В hello портал Azure **конечной точки** убедитесь, что **Обзор** выбран hello оставить навигации и выберите hello **+ пользовательский домен** кнопку вверху hello страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="24843-230">In hello Azure portal **Endpoint** page, make sure **Overview** is selected in hello left navigation, and then select hello **+ Custom Domain** button at hello top of hello page.</span></span>

![Нажатие кнопки добавления личного домена](media/app-service-web-tutorial-content-delivery-network/portal-select-add-domain.png)

<span data-ttu-id="24843-232">В hello **добавить пользовательский домен** страницы, вы видите toouse имя узла hello конечной точки при создании записи CNAME.</span><span class="sxs-lookup"><span data-stu-id="24843-232">In hello **Add a custom domain** page, you see hello endpoint host name toouse in creating a CNAME record.</span></span> <span data-ttu-id="24843-233">Имя узла Hello является производным от URL-адрес конечной точки CDN:  **&lt;EndpointName >. azureedge.net**.</span><span class="sxs-lookup"><span data-stu-id="24843-233">hello host name is derived from your CDN endpoint URL: **&lt;EndpointName>.azureedge.net**.</span></span> 

![Страница добавления домена](media/app-service-web-tutorial-content-delivery-network/portal-add-domain.png)

### <a name="configure-hello-cname-with-your-domain-registrar"></a><span data-ttu-id="24843-235">Настройка hello CNAME с помощью регистратора доменных имен</span><span class="sxs-lookup"><span data-stu-id="24843-235">Configure hello CNAME with your domain registrar</span></span>

<span data-ttu-id="24843-236">Перейдите на веб-сайте регистратора домена tooyour и найдите раздел hello создания записей DNS.</span><span class="sxs-lookup"><span data-stu-id="24843-236">Navigate tooyour domain registrar's web site, and locate hello section for creating DNS records.</span></span> <span data-ttu-id="24843-237">Это может быть такой раздел, как **Доменное имя**, **DNS** или **Управление сервером доменных имен**.</span><span class="sxs-lookup"><span data-stu-id="24843-237">You might find this in a section such as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>

<span data-ttu-id="24843-238">Найдите раздел hello управления записями CNAME.</span><span class="sxs-lookup"><span data-stu-id="24843-238">Find hello section for managing CNAMEs.</span></span> <span data-ttu-id="24843-239">Могут содержать дополнительные параметры страницы toogo tooan и искать слова hello CNAME, псевдонима или поддомены.</span><span class="sxs-lookup"><span data-stu-id="24843-239">You may have toogo tooan advanced settings page and look for hello words CNAME, Alias, or Subdomains.</span></span>

<span data-ttu-id="24843-240">Создайте запись CNAME, которая сопоставляет выбранный вами поддомен (например, **статических** или **cdn**) toohello **имя узла конечной точки** показанный выше в портал hello.</span><span class="sxs-lookup"><span data-stu-id="24843-240">Create a CNAME record that maps your chosen subdomain (for example, **static** or **cdn**) toohello **Endpoint host name** shown earlier in hello portal.</span></span> 

### <a name="enter-hello-custom-domain-in-azure"></a><span data-ttu-id="24843-241">Введите пользовательский домен hello в Azure</span><span class="sxs-lookup"><span data-stu-id="24843-241">Enter hello custom domain in Azure</span></span>

<span data-ttu-id="24843-242">Вернуть toohello **добавить пользовательский домен** страницы и введите свой домен, включая поддомен hello в диалоговое окно «hello».</span><span class="sxs-lookup"><span data-stu-id="24843-242">Return toohello **Add a custom domain** page, and enter your custom domain, including hello subdomain, in hello dialog box.</span></span> <span data-ttu-id="24843-243">Например, введите `cdn.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="24843-243">For example, enter `cdn.contoso.com`.</span></span>   
   
<span data-ttu-id="24843-244">Azure проверяет наличие записи CNAME hello для hello доменное имя, которое вы ввели.</span><span class="sxs-lookup"><span data-stu-id="24843-244">Azure verifies that hello CNAME record exists for hello domain name you have entered.</span></span> <span data-ttu-id="24843-245">Если правильно hello CNAME, проверяется вашего домена.</span><span class="sxs-lookup"><span data-stu-id="24843-245">If hello CNAME is correct, your custom domain is validated.</span></span>

<span data-ttu-id="24843-246">Для серверов tooname toopropagate записей CNAME hello на hello Интернет занимает время.</span><span class="sxs-lookup"><span data-stu-id="24843-246">It can take time for hello CNAME record toopropagate tooname servers on hello Internet.</span></span> <span data-ttu-id="24843-247">Если домен не проверяется сразу, подождите несколько минут и повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="24843-247">If your domain is not validated immediately, wait a few minutes and try again.</span></span>

### <a name="test-hello-custom-domain"></a><span data-ttu-id="24843-248">Пользовательский домен hello теста</span><span class="sxs-lookup"><span data-stu-id="24843-248">Test hello custom domain</span></span>

<span data-ttu-id="24843-249">В браузере перейдите toohello `index.html` текстовый файл с помощью личного домена (например, `cdn.contoso.com/index.html`) tooverify, результат hello Здравствуйте таким же, как при переходе непосредственно слишком`<endpointname>azureedge.net/index.html`.</span><span class="sxs-lookup"><span data-stu-id="24843-249">In a browser, navigate toohello `index.html` file using your custom domain (for example, `cdn.contoso.com/index.html`) tooverify that hello result is hello same as when you go directly too`<endpointname>azureedge.net/index.html`.</span></span>

![Домашняя страница примера приложения по URL-адресу с личным доменом](media/app-service-web-tutorial-content-delivery-network/home-page-custom-domain.png)

<span data-ttu-id="24843-251">Дополнительные сведения см. в разделе [личный домен CDN Azure карты содержимого tooa](../cdn/cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="24843-251">For more information, see [Map Azure CDN content tooa custom domain](../cdn/cdn-map-content-to-custom-domain.md).</span></span>

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="24843-252">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="24843-252">Next steps</span></span>

<span data-ttu-id="24843-253">Вы научились выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="24843-253">What you learned:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="24843-254">создание конечной точки CDN;</span><span class="sxs-lookup"><span data-stu-id="24843-254">Create a CDN endpoint.</span></span>
> * <span data-ttu-id="24843-255">обновление кэшированных ресурсов;</span><span class="sxs-lookup"><span data-stu-id="24843-255">Refresh cached assets.</span></span>
> * <span data-ttu-id="24843-256">Использовать запрос строк в кэше toocontrol версии.</span><span class="sxs-lookup"><span data-stu-id="24843-256">Use query strings toocontrol cached versions.</span></span>
> * <span data-ttu-id="24843-257">Используйте настраиваемый домен для конечной точки CDN hello.</span><span class="sxs-lookup"><span data-stu-id="24843-257">Use a custom domain for hello CDN endpoint.</span></span>

<span data-ttu-id="24843-258">Узнайте, как производительность CDN toooptimize hello следующие статьи:</span><span class="sxs-lookup"><span data-stu-id="24843-258">Learn how toooptimize CDN performance in hello following articles:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="24843-259">Повышение производительности за счет сжатия файлов в Azure CDN</span><span class="sxs-lookup"><span data-stu-id="24843-259">Improve performance by compressing files in Azure CDN</span></span>](../cdn/cdn-improve-performance.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="24843-260">Предварительная загрузка ресурсов на конечной точке CDN Azure</span><span class="sxs-lookup"><span data-stu-id="24843-260">Pre-load assets on an Azure CDN endpoint</span></span>](../cdn/cdn-preload-endpoint.md)
