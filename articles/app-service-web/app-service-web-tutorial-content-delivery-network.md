---
title: "Добавление сети доставки содержимого в службу приложений Azure | Документация Майкрософт"
description: "Добавление сети доставки содержимого (CDN) в службу приложений Azure для кэширования и доставки статических файлов с ближайших к вашим клиентам серверов по всему миру."
services: app-service\web
author: syntaxc4
ms.author: cfowler
ms.date: 05/31/2017
ms.topic: tutorial
ms.service: app-service-web
manager: erikre
ms.workload: web
ms.custom: mvc
ms.openlocfilehash: 257b75d01f3904661c1a188a2d53ffcb74f48f06
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="add-a-content-delivery-network-cdn-to-an-azure-app-service"></a><span data-ttu-id="febb0-103">Добавление сети доставки содержимого (CDN) в службу приложений Azure</span><span class="sxs-lookup"><span data-stu-id="febb0-103">Add a Content Delivery Network (CDN) to an Azure App Service</span></span>

<span data-ttu-id="febb0-104">[Сеть доставки содержимого (CDN) Azure](../cdn/cdn-overview.md) кэширует статическое веб-содержимое в стратегически расположенных точках. Это позволяет обеспечить максимальную пропускную способность для доставки содержимого пользователям.</span><span class="sxs-lookup"><span data-stu-id="febb0-104">[Azure Content Delivery Network (CDN)](../cdn/cdn-overview.md) caches static web content at strategically placed locations to provide maximum throughput for delivering content to users.</span></span> <span data-ttu-id="febb0-105">CDN также уменьшает нагрузку сервера веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="febb0-105">The CDN also decreases server load on your web app.</span></span> <span data-ttu-id="febb0-106">В этом руководстве показано, как добавить Azure CDN в [веб-приложение службы приложений Azure](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="febb0-106">This tutorial shows how to add Azure CDN to a [web app in Azure App Service](app-service-web-overview.md).</span></span> 

<span data-ttu-id="febb0-107">Это домашняя страница примера статического HTML-сайта, с которым вы будете работать:</span><span class="sxs-lookup"><span data-stu-id="febb0-107">Here's the home page of the sample static HTML site that you'll work with:</span></span>

![Домашняя страница примера приложения](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page.png)

<span data-ttu-id="febb0-109">Из этого руководства вы узнаете, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="febb0-109">What you'll learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="febb0-110">создание конечной точки CDN;</span><span class="sxs-lookup"><span data-stu-id="febb0-110">Create a CDN endpoint.</span></span>
> * <span data-ttu-id="febb0-111">обновление кэшированных ресурсов;</span><span class="sxs-lookup"><span data-stu-id="febb0-111">Refresh cached assets.</span></span>
> * <span data-ttu-id="febb0-112">использование строк запросов для управления кэшированными версиями;</span><span class="sxs-lookup"><span data-stu-id="febb0-112">Use query strings to control cached versions.</span></span>
> * <span data-ttu-id="febb0-113">использование личного домена для конечной точки CDN.</span><span class="sxs-lookup"><span data-stu-id="febb0-113">Use a custom domain for the CDN endpoint.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="febb0-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="febb0-114">Prerequisites</span></span>

<span data-ttu-id="febb0-115">Для работы с этим руководством:</span><span class="sxs-lookup"><span data-stu-id="febb0-115">To complete this tutorial:</span></span>

- <span data-ttu-id="febb0-116">[установите Git](https://git-scm.com/);</span><span class="sxs-lookup"><span data-stu-id="febb0-116">[Install Git](https://git-scm.com/)</span></span>
- <span data-ttu-id="febb0-117">[Установите Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="febb0-117">[Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-the-web-app"></a><span data-ttu-id="febb0-118">Создание веб-приложения</span><span class="sxs-lookup"><span data-stu-id="febb0-118">Create the web app</span></span>

<span data-ttu-id="febb0-119">Чтобы создать веб-приложение, с которым вы будете работать, следуйте инструкциям в разделе **Переход в приложение** статьи [Создание статического веб-приложения HTML в Azure](app-service-web-get-started-html.md).</span><span class="sxs-lookup"><span data-stu-id="febb0-119">To create the web app that you'll work with, follow the [static HTML quickstart](app-service-web-get-started-html.md) through the **Browse to the app** step.</span></span>

### <a name="have-a-custom-domain-ready"></a><span data-ttu-id="febb0-120">Подготовка личного домена</span><span class="sxs-lookup"><span data-stu-id="febb0-120">Have a custom domain ready</span></span>

<span data-ttu-id="febb0-121">Чтобы подготовить личный домен, вам необходимо быть его владельцем, а также нужен доступ к реестру DNS поставщика домена (например, GoDaddy).</span><span class="sxs-lookup"><span data-stu-id="febb0-121">To complete the custom domain step of this tutorial, you need to own a custom domain and have access to your DNS registry for your domain provider (such as GoDaddy).</span></span> <span data-ttu-id="febb0-122">Например, чтобы добавить записи DNS для `contoso.com` и `www.contoso.com`, необходим доступ для настройки параметров DNS для корневого домена `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="febb0-122">For example, to add DNS entries for `contoso.com` and `www.contoso.com`, you must have access to configure the DNS settings for the `contoso.com` root domain.</span></span>

<span data-ttu-id="febb0-123">Если у вас еще нет доменного имени, ознакомьтесь с [руководством по домену службы приложений](custom-dns-web-site-buydomains-web-app.md), чтобы узнать, как приобрести домен с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="febb0-123">If you don't already have a domain name, consider following the [App Service domain tutorial](custom-dns-web-site-buydomains-web-app.md) to purchase a domain using the Azure portal.</span></span> 

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="febb0-124">Войдите на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="febb0-124">Log in to the Azure portal</span></span>

<span data-ttu-id="febb0-125">Откройте браузер и перейдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="febb0-125">Open a browser and navigate to the [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-a-cdn-profile-and-endpoint"></a><span data-ttu-id="febb0-126">Создание профиля CDN и конечной точки</span><span class="sxs-lookup"><span data-stu-id="febb0-126">Create a CDN profile and endpoint</span></span>

<span data-ttu-id="febb0-127">В области навигации слева выберите раздел **Службы приложений**, а затем и выберите приложение, созданное в соответствии с инструкциями по [созданию статического веб-приложения HTML](app-service-web-get-started-html.md).</span><span class="sxs-lookup"><span data-stu-id="febb0-127">In the left navigation, select **App Services**, and then select the app that you created in the [static HTML quickstart](app-service-web-get-started-html.md).</span></span>

![Выбор службы приложений на портале](media/app-service-web-tutorial-content-delivery-network/portal-select-app-services.png)

<span data-ttu-id="febb0-129">На странице **Служба приложений** в разделе **Параметры** выберите **Сеть > Настроить сеть доставки содержимого Azure для приложения**.</span><span class="sxs-lookup"><span data-stu-id="febb0-129">In the **App Service** page, in the **Settings** section, select **Networking > Configure Azure CDN for your app**.</span></span>

![Выбор CDN на портале](media/app-service-web-tutorial-content-delivery-network/portal-select-cdn.png)

<span data-ttu-id="febb0-131">На странице **Сеть доставки содержимого Azure** выберите параметры **новой конечной точки** параметры, как указано в таблице.</span><span class="sxs-lookup"><span data-stu-id="febb0-131">In the **Azure Content Delivery Network** page, provide the **New endpoint** settings as specified in the table.</span></span>

![Создание профиля и конечной точки на портале](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint.png)

| <span data-ttu-id="febb0-133">Настройка</span><span class="sxs-lookup"><span data-stu-id="febb0-133">Setting</span></span> | <span data-ttu-id="febb0-134">Рекомендуемое значение</span><span class="sxs-lookup"><span data-stu-id="febb0-134">Suggested value</span></span> | <span data-ttu-id="febb0-135">Описание</span><span class="sxs-lookup"><span data-stu-id="febb0-135">Description</span></span> |
| ------- | --------------- | ----------- |
| <span data-ttu-id="febb0-136">**Профиль CDN**</span><span class="sxs-lookup"><span data-stu-id="febb0-136">**CDN profile**</span></span> | <span data-ttu-id="febb0-137">myCDNProfile</span><span class="sxs-lookup"><span data-stu-id="febb0-137">myCDNProfile</span></span> | <span data-ttu-id="febb0-138">Выберите **Создать**, чтобы создать профиль CDN.</span><span class="sxs-lookup"><span data-stu-id="febb0-138">Select **Create new** to create a CDN profile.</span></span> <span data-ttu-id="febb0-139">Профиль CDN представляет собой коллекцию конечных точек сети CDN из одной ценовой категории.</span><span class="sxs-lookup"><span data-stu-id="febb0-139">A CDN profile is a collection of CDN endpoints with the same pricing tier.</span></span> |
| <span data-ttu-id="febb0-140">**Ценовая категория**</span><span class="sxs-lookup"><span data-stu-id="febb0-140">**Pricing tier**</span></span> | <span data-ttu-id="febb0-141">Akamai уровня "Стандартный"</span><span class="sxs-lookup"><span data-stu-id="febb0-141">Standard Akamai</span></span> | <span data-ttu-id="febb0-142">От [ценовой категории](../cdn/cdn-overview.md#azure-cdn-features) зависят поставщик и доступные возможности.</span><span class="sxs-lookup"><span data-stu-id="febb0-142">The [pricing tier](../cdn/cdn-overview.md#azure-cdn-features) specifies the provider and available features.</span></span> <span data-ttu-id="febb0-143">В этом руководстве используется ценовая категория Akamai уровня "Стандартный".</span><span class="sxs-lookup"><span data-stu-id="febb0-143">In this tutorial, we are using Standard Akamai.</span></span> |
| <span data-ttu-id="febb0-144">**Имя конечной точки CDN**</span><span class="sxs-lookup"><span data-stu-id="febb0-144">**CDN endpoint name**</span></span> | <span data-ttu-id="febb0-145">Любое имя, которое является уникальным в домене azureedge.net</span><span class="sxs-lookup"><span data-stu-id="febb0-145">Any name that is unique in the azureedge.net domain</span></span> | <span data-ttu-id="febb0-146">Вы можете обращаться к кэшированным ресурсам в домене *\<имя_конечной_точки>. azureedge.net*.</span><span class="sxs-lookup"><span data-stu-id="febb0-146">You access your cached resources at the domain *\<endpointname>.azureedge.net*.</span></span>

<span data-ttu-id="febb0-147">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="febb0-147">Select **Create**.</span></span>

<span data-ttu-id="febb0-148">Azure создаст профиль и конечную точку.</span><span class="sxs-lookup"><span data-stu-id="febb0-148">Azure creates the profile and endpoint.</span></span> <span data-ttu-id="febb0-149">Новая конечная точка появится в списке **Конечные точки** на той же странице. Когда она будет готова, ее состояние изменится на **Выполняется**.</span><span class="sxs-lookup"><span data-stu-id="febb0-149">The new endpoint appears in the **Endpoints** list on the same page, and when it's provisioned the status is **Running**.</span></span>

![Новая конечная точка в списке](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint-in-list.png)

### <a name="test-the-cdn-endpoint"></a><span data-ttu-id="febb0-151">Тестирование конечной точки сети CDN</span><span class="sxs-lookup"><span data-stu-id="febb0-151">Test the CDN endpoint</span></span>

<span data-ttu-id="febb0-152">Если выбрать ценовую категорию Verizon, распространение конечной точки может занять около 90 минут.</span><span class="sxs-lookup"><span data-stu-id="febb0-152">If you selected Verizon pricing tier, it typically takes about 90 minutes for endpoint propagation.</span></span> <span data-ttu-id="febb0-153">В ценовой категории Akamai распространение длится несколько минут.</span><span class="sxs-lookup"><span data-stu-id="febb0-153">For Akamai, it takes a couple minutes for propagation</span></span>

<span data-ttu-id="febb0-154">Пример приложения содержит файл `index.html` и папки *css*, *img* и *js*, в которых находятся другие статические ресурсы.</span><span class="sxs-lookup"><span data-stu-id="febb0-154">The sample app has an `index.html` file and *css*, *img*, and *js* folders that contain other static assets.</span></span> <span data-ttu-id="febb0-155">Пути содержимого для всех этих файлов совпадают с путями конечной точки CDN.</span><span class="sxs-lookup"><span data-stu-id="febb0-155">The content paths for all of these files are the same at the CDN endpoint.</span></span> <span data-ttu-id="febb0-156">Например, оба URL-адреса в примерах ниже обращаются к файлу *bootstrap.css* в папке *css*:</span><span class="sxs-lookup"><span data-stu-id="febb0-156">For example, both of the following URLs access the *bootstrap.css* file in the *css* folder:</span></span>

```
http://<appname>.azurewebsites.net/css/bootstrap.css
```

```
http://<endpointname>.azureedge.net/css/bootstrap.css
```

<span data-ttu-id="febb0-157">Откройте браузер и перейдите по следующему URL-адресу:</span><span class="sxs-lookup"><span data-stu-id="febb0-157">Navigate a browser to the following URL:</span></span>

```
http://<endpointname>.azureedge.net/index.html
```

![Домашняя страница примера приложения, которая передается из CDN](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page-cdn.png)

 <span data-ttu-id="febb0-159">Вы увидите ту же страницу, которая отображалась раньше в веб-приложении.</span><span class="sxs-lookup"><span data-stu-id="febb0-159">You see the same page that you ran earlier in an Azure web app.</span></span> <span data-ttu-id="febb0-160">Сеть доставки содержимого Azure извлекла ресурсы исходного веб-приложения и передает их из конечной точки CDN.</span><span class="sxs-lookup"><span data-stu-id="febb0-160">Azure CDN has retrieved the origin web app's assets and is serving them from the CDN endpoint</span></span>

<span data-ttu-id="febb0-161">Чтобы убедиться, что эта страница кэшируется в CDN, обновите страницу.</span><span class="sxs-lookup"><span data-stu-id="febb0-161">To ensure that this page is cached in the CDN, refresh the page.</span></span> <span data-ttu-id="febb0-162">Иногда для кэширования запрошенного содержимого в CDN необходимо два запроса к одному и тому же ресурсу.</span><span class="sxs-lookup"><span data-stu-id="febb0-162">Two requests for the same asset are sometimes required for the CDN to cache the requested content.</span></span>

<span data-ttu-id="febb0-163">Дополнительные сведения о создании профилей и конечных точек Azure CDN см. в статье [Начало работы с Azure CDN](../cdn/cdn-create-new-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="febb0-163">For more information about creating Azure CDN profiles and endpoints, see [Getting started with Azure CDN](../cdn/cdn-create-new-endpoint.md).</span></span>

## <a name="purge-the-cdn"></a><span data-ttu-id="febb0-164">Очистка CDN</span><span class="sxs-lookup"><span data-stu-id="febb0-164">Purge the CDN</span></span>

<span data-ttu-id="febb0-165">CDN периодически обновляет свои ресурсы из исходного веб-приложения на основе конфигурации срока жизни (TTL).</span><span class="sxs-lookup"><span data-stu-id="febb0-165">The CDN periodically refreshes its resources from the origin web app based on the time-to-live (TTL) configuration.</span></span> <span data-ttu-id="febb0-166">По умолчанию срок жизни составляет 7 дней.</span><span class="sxs-lookup"><span data-stu-id="febb0-166">The default TTL is seven days.</span></span>

<span data-ttu-id="febb0-167">Иногда может потребоваться обновить CDN до истечения срока жизни, например при развертывании обновленного содержимого веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="febb0-167">At times you might need to refresh the CDN before the TTL expiration -- for example, when you deploy updated content to the web app.</span></span> <span data-ttu-id="febb0-168">Чтобы активировать обновление, можно вручную очистить ресурсы CDN.</span><span class="sxs-lookup"><span data-stu-id="febb0-168">To trigger a refresh, you can manually purge the CDN resources.</span></span> 

<span data-ttu-id="febb0-169">В этом разделе руководства вы можете развернуть изменение в веб-приложении и очистить CDN, чтобы активировать обновление кэша CDN.</span><span class="sxs-lookup"><span data-stu-id="febb0-169">In this section of the tutorial, you deploy a change to the web app and purge the CDN to trigger the CDN to refresh its cache.</span></span>

### <a name="deploy-a-change-to-the-web-app"></a><span data-ttu-id="febb0-170">Развертывание изменений в веб-приложении</span><span class="sxs-lookup"><span data-stu-id="febb0-170">Deploy a change to the web app</span></span>

<span data-ttu-id="febb0-171">Откройте файл `index.html` и добавьте "-V2" в заголовок H1, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="febb0-171">Open the `index.html` file and add "- V2" to the H1 heading, as shown in the following example:</span></span> 

```
<h1>Azure App Service - Sample Static HTML Site - V2</h1>
```

<span data-ttu-id="febb0-172">Зафиксируйте изменение и разверните его в веб-приложении.</span><span class="sxs-lookup"><span data-stu-id="febb0-172">Commit your change and deploy it to the web app.</span></span>

```bash
git commit -am "version 2"
git push azure master
```

<span data-ttu-id="febb0-173">После завершения развертывания откройте URL-адрес веб-приложения, и вы увидите изменения.</span><span class="sxs-lookup"><span data-stu-id="febb0-173">Once deployment has completed, browse to the web app URL and you see the change.</span></span>

```
http://<appname>.azurewebsites.net/index.html
```

![Элемент "V2" в заголовке веб-приложения](media/app-service-web-tutorial-content-delivery-network/v2-in-web-app-title.png)

<span data-ttu-id="febb0-175">Перейдите по URL-адресу конечной точки CDN, чтобы открыть домашнюю страницу. Вы не увидите изменения, так как срок действия кэшированной версии CDN еще не истек.</span><span class="sxs-lookup"><span data-stu-id="febb0-175">Browse to the CDN endpoint URL for the home page and you don't see the change because the cached version in the CDN hasn't expired yet.</span></span> 

```
http://<endpointname>.azureedge.net/index.html
```

![В заголовке в CDN нет элемента "V2"](media/app-service-web-tutorial-content-delivery-network/no-v2-in-cdn-title.png)

### <a name="purge-the-cdn-in-the-portal"></a><span data-ttu-id="febb0-177">Очистка CDN на портале</span><span class="sxs-lookup"><span data-stu-id="febb0-177">Purge the CDN in the portal</span></span>

<span data-ttu-id="febb0-178">Чтобы активировать обновление кэшированной версии в CDN, нужно очистить CDN.</span><span class="sxs-lookup"><span data-stu-id="febb0-178">To trigger the CDN to update its cached version, purge the CDN.</span></span>

<span data-ttu-id="febb0-179">На портале в области навигации слева выберите раздел **Группы ресурсов**, а затем выберите группу ресурсов, созданную для веб-приложения (myResourceGroup).</span><span class="sxs-lookup"><span data-stu-id="febb0-179">In the portal left navigation, select **Resource groups**, and then select the resource group that you created for your web app (myResourceGroup).</span></span>

![Выбор группы ресурсов](media/app-service-web-tutorial-content-delivery-network/portal-select-group.png)

<span data-ttu-id="febb0-181">В списке ресурсов выберите конечную точку CDN.</span><span class="sxs-lookup"><span data-stu-id="febb0-181">In the list of resources, select your CDN endpoint.</span></span>

![Выбор конечной точки](media/app-service-web-tutorial-content-delivery-network/portal-select-endpoint.png)

<span data-ttu-id="febb0-183">В верхней части страницы **Конечная точка** нажмите кнопку **Очистить**.</span><span class="sxs-lookup"><span data-stu-id="febb0-183">At the top of the **Endpoint** page, click **Purge**.</span></span>

![Нажатие кнопки "Очистить"](media/app-service-web-tutorial-content-delivery-network/portal-select-purge.png)

<span data-ttu-id="febb0-185">Введите пути к содержимому, которые необходимо очистить.</span><span class="sxs-lookup"><span data-stu-id="febb0-185">Enter the content paths you wish to purge.</span></span> <span data-ttu-id="febb0-186">Вы можете передать полный путь к файлу, чтобы очистить отдельный файл, или сегмент пути, чтобы очистить и обновить все содержимое папки.</span><span class="sxs-lookup"><span data-stu-id="febb0-186">You can pass a complete file path to purge an individual file, or a path segment to purge and refresh all content in a folder.</span></span> <span data-ttu-id="febb0-187">Так как вы изменили файл `index.html`, убедитесь, что вы указали путь к нему.</span><span class="sxs-lookup"><span data-stu-id="febb0-187">Since you changed `index.html`, make sure that is one of the paths.</span></span>

<span data-ttu-id="febb0-188">В нижней части страницы нажмите кнопку **Очистить**.</span><span class="sxs-lookup"><span data-stu-id="febb0-188">At the bottom of the page, select **Purge**.</span></span>

![Страница очистки](media/app-service-web-tutorial-content-delivery-network/app-service-web-purge-cdn.png)

### <a name="verify-that-the-cdn-is-updated"></a><span data-ttu-id="febb0-190">Проверка обновления CDN</span><span class="sxs-lookup"><span data-stu-id="febb0-190">Verify that the CDN is updated</span></span>

<span data-ttu-id="febb0-191">Подождите, пока запрос очистки завершит обработку. Обычно это длится несколько минут.</span><span class="sxs-lookup"><span data-stu-id="febb0-191">Wait until the purge request finishes processing, typically a couple of minutes.</span></span> <span data-ttu-id="febb0-192">Чтобы просмотреть текущее состояние, выберите значок колокольчика в верхней части страницы.</span><span class="sxs-lookup"><span data-stu-id="febb0-192">To see the current status, select the bell icon at the top of the page.</span></span> 

![Уведомление об очистке](media/app-service-web-tutorial-content-delivery-network/portal-purge-notification.png)

<span data-ttu-id="febb0-194">Перейдите по URL-адресу конечной точки CDN, чтобы открыть файл `index.html`, и вы увидите "V2" в заголовке на домашней странице.</span><span class="sxs-lookup"><span data-stu-id="febb0-194">Browse to the CDN endpoint URL for `index.html`, and now you see the V2 that you added to the title on the home page.</span></span> <span data-ttu-id="febb0-195">Это означает, что кэш CDN обновлен.</span><span class="sxs-lookup"><span data-stu-id="febb0-195">This shows that the CDN cache has been refreshed.</span></span>

```
http://<endpointname>.azureedge.net/index.html
```

!["V2" в заголовке в CDN](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title.png)

<span data-ttu-id="febb0-197">Дополнительные сведения см. в статье [Очистка конечной точки сети CDN Azure](../cdn/cdn-purge-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="febb0-197">For more information, see [Purge an Azure CDN endpoint](../cdn/cdn-purge-endpoint.md).</span></span> 

## <a name="use-query-strings-to-version-content"></a><span data-ttu-id="febb0-198">Использование строк запросов для управления версиями содержимого</span><span class="sxs-lookup"><span data-stu-id="febb0-198">Use query strings to version content</span></span>

<span data-ttu-id="febb0-199">В Azure CDN доступны следующие варианты режима кэширования:</span><span class="sxs-lookup"><span data-stu-id="febb0-199">The Azure CDN offers the following caching behavior options:</span></span>

* <span data-ttu-id="febb0-200">игнорировать строки запросов;</span><span class="sxs-lookup"><span data-stu-id="febb0-200">Ignore query strings</span></span>
* <span data-ttu-id="febb0-201">обходить кэширование для строк запросов;</span><span class="sxs-lookup"><span data-stu-id="febb0-201">Bypass caching for query strings</span></span>
* <span data-ttu-id="febb0-202">кэшировать все уникальные URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="febb0-202">Cache every unique URL</span></span> 

<span data-ttu-id="febb0-203">Первый вариант используется по умолчанию. Это означает, что существует только одна кэшированная версия ресурса, независимо от строки запроса в URL-адресе.</span><span class="sxs-lookup"><span data-stu-id="febb0-203">The first of these is the default, which means there is only one cached version of an asset regardless of the query string in the URL.</span></span> 

<span data-ttu-id="febb0-204">В этом разделе руководства можно изменить режим кэширования, чтобы кэшировать каждый уникальный URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="febb0-204">In this section of the tutorial, you change the caching behavior to cache every unique URL.</span></span>

### <a name="change-the-cache-behavior"></a><span data-ttu-id="febb0-205">Изменение поведения кэширования</span><span class="sxs-lookup"><span data-stu-id="febb0-205">Change the cache behavior</span></span>

<span data-ttu-id="febb0-206">На портале Azure на странице **Конечная точка CDN** выберите раздел **Кэш**.</span><span class="sxs-lookup"><span data-stu-id="febb0-206">In the Azure portal **CDN Endpoint** page, select **Cache**.</span></span>

<span data-ttu-id="febb0-207">Для параметра **Режим кэширования строк запросов** выберите в раскрывающемся списке **Кэшировать каждый уникальный URL-адрес**.</span><span class="sxs-lookup"><span data-stu-id="febb0-207">Select **Cache every unique URL** from the **Query string caching behavior** drop-down list.</span></span>

<span data-ttu-id="febb0-208">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="febb0-208">Select **Save**.</span></span>

![Выбор режима кэширования строки запроса](media/app-service-web-tutorial-content-delivery-network/portal-select-caching-behavior.png)

### <a name="verify-that-unique-urls-are-cached-separately"></a><span data-ttu-id="febb0-210">Проверка кэширования уникальных URL-адресов по отдельности</span><span class="sxs-lookup"><span data-stu-id="febb0-210">Verify that unique URLs are cached separately</span></span>

<span data-ttu-id="febb0-211">В браузере откройте домашнюю страницу по адресу конечной точки CDN, включив строку запроса:</span><span class="sxs-lookup"><span data-stu-id="febb0-211">In a browser, navigate to the home page at the CDN endpoint, but include a query string:</span></span> 

```
http://<endpointname>.azureedge.net/index.html?q=1
```

<span data-ttu-id="febb0-212">CDN возвращает текущее содержимое веб-приложения, которое включает "V2" в заголовке.</span><span class="sxs-lookup"><span data-stu-id="febb0-212">The CDN returns the current web app content, which includes "V2" in the heading.</span></span> 

<span data-ttu-id="febb0-213">Чтобы убедиться, что эта страница кэшируется в CDN, обновите страницу.</span><span class="sxs-lookup"><span data-stu-id="febb0-213">To ensure that this page is cached in the CDN, refresh the page.</span></span> 

<span data-ttu-id="febb0-214">Откройте файл `index.html` и замените "V2" значением "V3". Затем разверните изменение.</span><span class="sxs-lookup"><span data-stu-id="febb0-214">Open `index.html` and change "V2" to "V3", and deploy the change.</span></span> 

```bash
git commit -am "version 3"
git push azure master
```

<span data-ttu-id="febb0-215">В браузере откройте URL-адрес конечной точки CDN с новой строкой запроса, например `q=2`.</span><span class="sxs-lookup"><span data-stu-id="febb0-215">In a browser, go to the CDN endpoint URL with a new query string such as `q=2`.</span></span> <span data-ttu-id="febb0-216">CDN получает текущий файл `index.html` и отображает значение "V3".</span><span class="sxs-lookup"><span data-stu-id="febb0-216">The CDN gets the current `index.html` file and displays "V3".</span></span>  <span data-ttu-id="febb0-217">Но при переходе к конечной точке CDN с о строкой запроса `q=1` отображается значение "V2".</span><span class="sxs-lookup"><span data-stu-id="febb0-217">But if you navigate to the CDN endpoint with the `q=1` query string, you see "V2".</span></span>

```
http://<endpointname>.azureedge.net/index.html?q=2
```

!["V3" в заголовке CDN, строка запроса 2](media/app-service-web-tutorial-content-delivery-network/v3-in-cdn-title-qs2.png)

```
http://<endpointname>.azureedge.net/index.html?q=1
```

!["V2" в заголовке CDN, строка запроса 1](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title-qs1.png)

<span data-ttu-id="febb0-220">Этот результат показывает, что каждая строка запроса обрабатывается по-разному:</span><span class="sxs-lookup"><span data-stu-id="febb0-220">This output shows that each query string is treated differently:</span></span>

* <span data-ttu-id="febb0-221">строка "q=1" использовалась ранее, поэтому возвращается кэшированное содержимое (V2);</span><span class="sxs-lookup"><span data-stu-id="febb0-221">q=1 was used before, so cached contents are returned (V2).</span></span>
* <span data-ttu-id="febb0-222">строка "q=2" используется впервые, поэтому извлекается и возвращается последнее содержимое веб-приложения (V3).</span><span class="sxs-lookup"><span data-stu-id="febb0-222">q=2 is new, so the latest web app contents are retrieved and returned (V3).</span></span>

<span data-ttu-id="febb0-223">Дополнительные сведения см. в статье [Управление режимом кэширования Azure CDN с помощью строк запросов](../cdn/cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="febb0-223">For more information, see [Control Azure CDN caching behavior with query strings](../cdn/cdn-query-string.md).</span></span>

## <a name="map-a-custom-domain-to-a-cdn-endpoint"></a><span data-ttu-id="febb0-224">Сопоставление личного домена с конечной точкой CDN</span><span class="sxs-lookup"><span data-stu-id="febb0-224">Map a custom domain to a CDN endpoint</span></span>

<span data-ttu-id="febb0-225">Чтобы сопоставить личный домен с конечной точкой CDN, нужно создать запись CNAME.</span><span class="sxs-lookup"><span data-stu-id="febb0-225">You'll map your custom domain to your CDN Endpoint by creating a CNAME record.</span></span> <span data-ttu-id="febb0-226">Запись CNAME — это компонент DNS, позволяющий сопоставить исходный и конечный домены.</span><span class="sxs-lookup"><span data-stu-id="febb0-226">A CNAME record is a DNS feature that maps a source domain to a destination domain.</span></span> <span data-ttu-id="febb0-227">Например, можно сопоставить `cdn.contoso.com` или `static.contoso.com` с `contoso.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="febb0-227">For example, you might map `cdn.contoso.com` or `static.contoso.com` to `contoso.azureedge.net`.</span></span>

<span data-ttu-id="febb0-228">Если у вас нет личного домена, ознакомьтесь с [руководством по доменам службы приложений](custom-dns-web-site-buydomains-web-app.md), чтобы узнать, как приобрести домен с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="febb0-228">If you don't have a custom domain, consider following the [App Service domain tutorial](custom-dns-web-site-buydomains-web-app.md) to purchase a domain using the Azure portal.</span></span> 

### <a name="find-the-hostname-to-use-with-the-cname"></a><span data-ttu-id="febb0-229">Поиск имени узла для использования с CNAME</span><span class="sxs-lookup"><span data-stu-id="febb0-229">Find the hostname to use with the CNAME</span></span>

<span data-ttu-id="febb0-230">На портале Azure на странице **Конечная точка** в области навигации слева выберите раздел **Обзор**. Затем нажмите кнопку **+ Custom Domain** (Добавить личный домен) в верхней части страницы.</span><span class="sxs-lookup"><span data-stu-id="febb0-230">In the Azure portal **Endpoint** page, make sure **Overview** is selected in the left navigation, and then select the **+ Custom Domain** button at the top of the page.</span></span>

![Нажатие кнопки добавления личного домена](media/app-service-web-tutorial-content-delivery-network/portal-select-add-domain.png)

<span data-ttu-id="febb0-232">На странице **Добавление пользовательского домена** вы увидите имя узла конечной точки, которое нужно использовать при создании записи CNAME.</span><span class="sxs-lookup"><span data-stu-id="febb0-232">In the **Add a custom domain** page, you see the endpoint host name to use in creating a CNAME record.</span></span> <span data-ttu-id="febb0-233">Имя узла является производным от URL-адреса конечной точки CDN: **&lt;имя_конечной_точки>.azureedge.net**.</span><span class="sxs-lookup"><span data-stu-id="febb0-233">The host name is derived from your CDN endpoint URL: **&lt;EndpointName>.azureedge.net**.</span></span> 

![Страница добавления домена](media/app-service-web-tutorial-content-delivery-network/portal-add-domain.png)

### <a name="configure-the-cname-with-your-domain-registrar"></a><span data-ttu-id="febb0-235">Настройка записи CNAME в регистраторе домена</span><span class="sxs-lookup"><span data-stu-id="febb0-235">Configure the CNAME with your domain registrar</span></span>

<span data-ttu-id="febb0-236">Перейдите на веб-сайт вашего регистратора доменных имен и найдите раздел, посвященный созданию записей DNS.</span><span class="sxs-lookup"><span data-stu-id="febb0-236">Navigate to your domain registrar's web site, and locate the section for creating DNS records.</span></span> <span data-ttu-id="febb0-237">Это может быть такой раздел, как **Доменное имя**, **DNS** или **Управление сервером доменных имен**.</span><span class="sxs-lookup"><span data-stu-id="febb0-237">You might find this in a section such as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>

<span data-ttu-id="febb0-238">Найдите раздел управления записями CNAME.</span><span class="sxs-lookup"><span data-stu-id="febb0-238">Find the section for managing CNAMEs.</span></span> <span data-ttu-id="febb0-239">Может понадобиться перейти на страницу дополнительных параметров и найти слова CNAME, Псевдоним или Поддомены.</span><span class="sxs-lookup"><span data-stu-id="febb0-239">You may have to go to an advanced settings page and look for the words CNAME, Alias, or Subdomains.</span></span>

<span data-ttu-id="febb0-240">Создайте запись CNAME, которая сопоставляет выбранный вами поддомен (например, **static** или **cdn**) с **именем узла конечной точки**, найденным ранее на портале.</span><span class="sxs-lookup"><span data-stu-id="febb0-240">Create a CNAME record that maps your chosen subdomain (for example, **static** or **cdn**) to the **Endpoint host name** shown earlier in the portal.</span></span> 

### <a name="enter-the-custom-domain-in-azure"></a><span data-ttu-id="febb0-241">Ввод имени личного домена в Azure</span><span class="sxs-lookup"><span data-stu-id="febb0-241">Enter the custom domain in Azure</span></span>

<span data-ttu-id="febb0-242">Вернитесь на страницу **Добавление пользовательского домена** и укажите в диалоговом окне личный домен, включая поддомен.</span><span class="sxs-lookup"><span data-stu-id="febb0-242">Return to the **Add a custom domain** page, and enter your custom domain, including the subdomain, in the dialog box.</span></span> <span data-ttu-id="febb0-243">Например, введите `cdn.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="febb0-243">For example, enter `cdn.contoso.com`.</span></span>   
   
<span data-ttu-id="febb0-244">Azure проверит наличие записи CNAME для введенного имени домена.</span><span class="sxs-lookup"><span data-stu-id="febb0-244">Azure verifies that the CNAME record exists for the domain name you have entered.</span></span> <span data-ttu-id="febb0-245">Если запись CNAME правильна, пользовательский домен проходит проверку.</span><span class="sxs-lookup"><span data-stu-id="febb0-245">If the CNAME is correct, your custom domain is validated.</span></span>

<span data-ttu-id="febb0-246">Иногда может потребоваться некоторое время для распространения записи CNAME по серверам имен в Интернете.</span><span class="sxs-lookup"><span data-stu-id="febb0-246">It can take time for the CNAME record to propagate to name servers on the Internet.</span></span> <span data-ttu-id="febb0-247">Если домен не проверяется сразу, подождите несколько минут и повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="febb0-247">If your domain is not validated immediately, wait a few minutes and try again.</span></span>

### <a name="test-the-custom-domain"></a><span data-ttu-id="febb0-248">Тестирование личного домена</span><span class="sxs-lookup"><span data-stu-id="febb0-248">Test the custom domain</span></span>

<span data-ttu-id="febb0-249">В браузере откройте файл `index.html`, используя личный домен (например, `cdn.contoso.com/index.html`), чтобы убедиться, что вы переходите на ту же страницу, которая открывается при переходе непосредственно по адресу `<endpointname>azureedge.net/index.html`.</span><span class="sxs-lookup"><span data-stu-id="febb0-249">In a browser, navigate to the `index.html` file using your custom domain (for example, `cdn.contoso.com/index.html`) to verify that the result is the same as when you go directly to `<endpointname>azureedge.net/index.html`.</span></span>

![Домашняя страница примера приложения по URL-адресу с личным доменом](media/app-service-web-tutorial-content-delivery-network/home-page-custom-domain.png)

<span data-ttu-id="febb0-251">Дополнительные сведения см. в статье [Сопоставление содержимого Azure CDN с пользовательским доменом](../cdn/cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="febb0-251">For more information, see [Map Azure CDN content to a custom domain](../cdn/cdn-map-content-to-custom-domain.md).</span></span>

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="febb0-252">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="febb0-252">Next steps</span></span>

<span data-ttu-id="febb0-253">Вы научились выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="febb0-253">What you learned:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="febb0-254">создание конечной точки CDN;</span><span class="sxs-lookup"><span data-stu-id="febb0-254">Create a CDN endpoint.</span></span>
> * <span data-ttu-id="febb0-255">обновление кэшированных ресурсов;</span><span class="sxs-lookup"><span data-stu-id="febb0-255">Refresh cached assets.</span></span>
> * <span data-ttu-id="febb0-256">использование строк запросов для управления кэшированными версиями;</span><span class="sxs-lookup"><span data-stu-id="febb0-256">Use query strings to control cached versions.</span></span>
> * <span data-ttu-id="febb0-257">использование личного домена для конечной точки CDN.</span><span class="sxs-lookup"><span data-stu-id="febb0-257">Use a custom domain for the CDN endpoint.</span></span>

<span data-ttu-id="febb0-258">Чтобы узнать, как оптимизировать производительность CDN, см. следующие статьи:</span><span class="sxs-lookup"><span data-stu-id="febb0-258">Learn how to optimize CDN performance in the following articles:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="febb0-259">Повышение производительности за счет сжатия файлов в Azure CDN</span><span class="sxs-lookup"><span data-stu-id="febb0-259">Improve performance by compressing files in Azure CDN</span></span>](../cdn/cdn-improve-performance.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="febb0-260">Предварительная загрузка ресурсов на конечной точке CDN Azure</span><span class="sxs-lookup"><span data-stu-id="febb0-260">Pre-load assets on an Azure CDN endpoint</span></span>](../cdn/cdn-preload-endpoint.md)
