---
title: "Создание бессерверного API с помощью Функций Azure | Документация Майкрософт"
description: "Руководство по созданию бессерверного API с помощью Функций Azure."
services: functions
author: mattchenderson
manager: erikre
ms.service: functions
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: tutorial
ms.date: 05/04/2017
ms.author: mahender
ms.custom: mvc
ms.openlocfilehash: 28056a385b058f7daeca2253ccb304116b49eba0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-serverless-api-using-azure-functions"></a><span data-ttu-id="c064a-103">Создание бессерверного API с помощью Функций Azure</span><span class="sxs-lookup"><span data-stu-id="c064a-103">Create a serverless API using Azure Functions</span></span>

<span data-ttu-id="c064a-104">В этом руководстве вы узнаете, как с помощью Функций Azure создавать высокомасштабируемые API.</span><span class="sxs-lookup"><span data-stu-id="c064a-104">In this tutorial you will learn how Azure Functions allows you to build highly-scalable APIs.</span></span> <span data-ttu-id="c064a-105">Функции Azure поставляются с набором встроенных триггеров и привязок HTTP, которые упрощают создание конечных точек на различных языках, включая Node.JS, C# и другие.</span><span class="sxs-lookup"><span data-stu-id="c064a-105">Azure Functions comes with a collection of built-in HTTP triggers and bindings which make it easy to author an endpoint in a variety of languages, including Node.JS, C#, and more.</span></span> <span data-ttu-id="c064a-106">В этом руководстве вы настроите триггер HTTP, который будет обрабатывать определенные действия в вашем API.</span><span class="sxs-lookup"><span data-stu-id="c064a-106">In this tutorial, you will customize an HTTP trigger to handle specific actions in your API design.</span></span> <span data-ttu-id="c064a-107">Вы также подготовите ваш API к увеличению размеров, интегрировав его с прокси-серверами Функций Azure и установив макет API.</span><span class="sxs-lookup"><span data-stu-id="c064a-107">You will also prepare for growing your API by integrating it with Azure Functions Proxies and setting up mock APIs.</span></span> <span data-ttu-id="c064a-108">Все это будет выполнено в бессерверной вычислительной среде Функций, так что вам не придется беспокоиться о масштабировании ресурсов, вы просто сможете сосредоточиться на логике вашего API.</span><span class="sxs-lookup"><span data-stu-id="c064a-108">All of this is accomplished on top of the Functions serverless compute environment, so you don't have to worry about scaling resources - you can just focus on your API logic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c064a-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c064a-109">Prerequisites</span></span> 

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

<span data-ttu-id="c064a-110">Полученная функция будет использоваться до конца этого руководства.</span><span class="sxs-lookup"><span data-stu-id="c064a-110">The resulting function will be used for the rest of this tutorial.</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="c064a-111">Вход в Azure</span><span class="sxs-lookup"><span data-stu-id="c064a-111">Sign in to Azure</span></span>

<span data-ttu-id="c064a-112">Перейдите на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c064a-112">Open the Azure portal.</span></span> <span data-ttu-id="c064a-113">Для этого войдите на портал [https://portal.azure.com](https://portal.azure.com) с помощью вашей учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="c064a-113">To do this, sign in to [https://portal.azure.com](https://portal.azure.com) with your Azure account.</span></span>

## <a name="customize-your-http-function"></a><span data-ttu-id="c064a-114">Настройка функции HTTP</span><span class="sxs-lookup"><span data-stu-id="c064a-114">Customize your HTTP function</span></span>

<span data-ttu-id="c064a-115">По умолчанию функция, инициируемая HTTP-запросом, настроена для приема любого метода HTTP.</span><span class="sxs-lookup"><span data-stu-id="c064a-115">By default, your HTTP-triggered function is configured to accept any HTTP method.</span></span> <span data-ttu-id="c064a-116">Существует также URL-адрес по умолчанию следующего вида: `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`.</span><span class="sxs-lookup"><span data-stu-id="c064a-116">There is also a default URL of the form `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`.</span></span> <span data-ttu-id="c064a-117">Если вы следовали краткому руководству, тогда `<funcname>`, вероятно, выглядит примерно так: HttpTriggerJS1.</span><span class="sxs-lookup"><span data-stu-id="c064a-117">If you followed the quickstart, then `<funcname>` probably looks something like "HttpTriggerJS1".</span></span> <span data-ttu-id="c064a-118">В этом разделе вы измените функцию, чтобы отвечать только на запросы GET вместо маршрута `/api/hello`.</span><span class="sxs-lookup"><span data-stu-id="c064a-118">In this section, you will modify the function to respond only to GET requests against `/api/hello` route instead.</span></span> 

<span data-ttu-id="c064a-119">Перейдите к своей функции на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="c064a-119">Navigate to your function in the Azure portal.</span></span> <span data-ttu-id="c064a-120">В левой области навигации выберите **Интегрировать**.</span><span class="sxs-lookup"><span data-stu-id="c064a-120">Select **Integrate** in the left navigation.</span></span>

![Настройка функции HTTP](./media/functions-create-serverless-api/customizing-http.png)

<span data-ttu-id="c064a-122">Используйте настройки триггера HTTP, как указано в таблице.</span><span class="sxs-lookup"><span data-stu-id="c064a-122">Use the HTTP trigger settings as specified in the table.</span></span>

| <span data-ttu-id="c064a-123">Поле</span><span class="sxs-lookup"><span data-stu-id="c064a-123">Field</span></span> | <span data-ttu-id="c064a-124">Образец значения</span><span class="sxs-lookup"><span data-stu-id="c064a-124">Sample value</span></span> | <span data-ttu-id="c064a-125">Описание</span><span class="sxs-lookup"><span data-stu-id="c064a-125">Description</span></span> |
|---|---|---|
| <span data-ttu-id="c064a-126">Разрешенные методы HTTP</span><span class="sxs-lookup"><span data-stu-id="c064a-126">Allowed HTTP methods</span></span> | <span data-ttu-id="c064a-127">Выбранные методы</span><span class="sxs-lookup"><span data-stu-id="c064a-127">Selected methods</span></span> | <span data-ttu-id="c064a-128">Определяет, какие методы HTTP могут использоваться для вызова этой функции</span><span class="sxs-lookup"><span data-stu-id="c064a-128">Determines what HTTP methods may be used to invoke this function</span></span> |
| <span data-ttu-id="c064a-129">Выбранные методы HTTP</span><span class="sxs-lookup"><span data-stu-id="c064a-129">Selected HTTP methods</span></span> | <span data-ttu-id="c064a-130">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="c064a-130">GET</span></span> | <span data-ttu-id="c064a-131">Разрешает использовать только выбранные методы HTTP для вызова этой функции</span><span class="sxs-lookup"><span data-stu-id="c064a-131">Allows only selected HTTP methods to be used to invoke this function</span></span> |
| <span data-ttu-id="c064a-132">Шаблон маршрута</span><span class="sxs-lookup"><span data-stu-id="c064a-132">Route template</span></span> | <span data-ttu-id="c064a-133">/hello</span><span class="sxs-lookup"><span data-stu-id="c064a-133">/hello</span></span> | <span data-ttu-id="c064a-134">Определяет пути, используемые для вызова этой функции</span><span class="sxs-lookup"><span data-stu-id="c064a-134">Determines what route is used to invoke this function</span></span> |

<span data-ttu-id="c064a-135">Обратите внимание, что вы не включали префикс базового пути `/api` в шаблон маршрута, так как он обрабатывается глобальным параметром.</span><span class="sxs-lookup"><span data-stu-id="c064a-135">Note that you did not include the `/api` base path prefix in the route template, as this is handled by a global setting.</span></span>

<span data-ttu-id="c064a-136">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="c064a-136">Click **Save**.</span></span>

<span data-ttu-id="c064a-137">Дополнительные сведения см. в статье [Привязки HTTP и webhook в функциях Azure](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).</span><span class="sxs-lookup"><span data-stu-id="c064a-137">You can learn more about customizing HTTP functions in [Azure Functions HTTP and webhook bindings](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).</span></span>

### <a name="test-your-api"></a><span data-ttu-id="c064a-138">Тестирование API</span><span class="sxs-lookup"><span data-stu-id="c064a-138">Test your API</span></span>

<span data-ttu-id="c064a-139">Протестируйте свою функцию, чтобы увидеть, как она работает с новой поверхностью API.</span><span class="sxs-lookup"><span data-stu-id="c064a-139">Next, test your function to see it working with the new API surface.</span></span>

<span data-ttu-id="c064a-140">Вернитесь на страницу разработки, щелкнув имя функции в левой области навигации.</span><span class="sxs-lookup"><span data-stu-id="c064a-140">Navigate back to the development page by clicking on the function's name in the left navigation.</span></span>

<span data-ttu-id="c064a-141">Щелкните **Get function URL** (Получить URL-адрес функции) и скопируйте URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="c064a-141">Click **Get function URL** and copy the URL.</span></span> <span data-ttu-id="c064a-142">Вы должны увидеть, что теперь используется маршрут `/api/hello`.</span><span class="sxs-lookup"><span data-stu-id="c064a-142">You should see that it uses the `/api/hello` route now.</span></span>

<span data-ttu-id="c064a-143">Скопируйте URL-адрес в новую вкладку браузера или в предпочтительный клиент REST.</span><span class="sxs-lookup"><span data-stu-id="c064a-143">Copy the URL into a new browser tab or your preferred REST client.</span></span> <span data-ttu-id="c064a-144">По умолчанию браузер использует функцию GET.</span><span class="sxs-lookup"><span data-stu-id="c064a-144">Browsers will use GET by default.</span></span>

<span data-ttu-id="c064a-145">Выполните функцию и убедитесь, что она работает.</span><span class="sxs-lookup"><span data-stu-id="c064a-145">Run the function and confirm that it is working.</span></span> <span data-ttu-id="c064a-146">Возможно, потребуется указать параметр имени в качестве строки запроса, чтобы использовать код быстрого запуска.</span><span class="sxs-lookup"><span data-stu-id="c064a-146">You may need to provide the "name" parameter as a query string to satisfy the quickstart code.</span></span>

<span data-ttu-id="c064a-147">Вы также можете попытаться вызвать конечную точку с помощью другого метода HTTP, чтобы убедиться, что эта функция не выполняется.</span><span class="sxs-lookup"><span data-stu-id="c064a-147">You can also try calling the endpoint with another HTTP method to confirm that the function is not executed.</span></span> <span data-ttu-id="c064a-148">Для этого необходимо использовать клиент REST, например cURL, Postman или Fiddler.</span><span class="sxs-lookup"><span data-stu-id="c064a-148">For this, you will need to use a REST client, such as cURL, Postman, or Fiddler.</span></span>

## <a name="proxies-overview"></a><span data-ttu-id="c064a-149">Общие сведения о прокси-серверах</span><span class="sxs-lookup"><span data-stu-id="c064a-149">Proxies overview</span></span>

<span data-ttu-id="c064a-150">В следующем разделе вы получите доступ к вашему API через прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="c064a-150">In the next section, you will surface your API through a proxy.</span></span> <span data-ttu-id="c064a-151">Прокси-серверы Функций Azure — это предварительная версия функции, позволяющая вам перенаправлять запросы к другим ресурсам.</span><span class="sxs-lookup"><span data-stu-id="c064a-151">Azure Functions Proxies is a preview feature that allows you to forward requests to other resources.</span></span> <span data-ttu-id="c064a-152">Вы определяете конечную точку HTTP точно так же, как триггер HTTP, но вместо написания кода для выполнения при вызове этой конечной точки вы указываете URL-адрес для удаленной реализации.</span><span class="sxs-lookup"><span data-stu-id="c064a-152">You define an HTTP endpoint just like with HTTP trigger, but instead of writing code to execute when that endpoint is called, you provide a URL to a remote implementation.</span></span> <span data-ttu-id="c064a-153">Это позволяет вам собрать несколько источников API в единую поверхность API, которую можно легко использовать.</span><span class="sxs-lookup"><span data-stu-id="c064a-153">This allows you to compose multiple API sources into a single API surface which is easy for clients to consume.</span></span> <span data-ttu-id="c064a-154">Это особенно полезно, если вы хотите создать свой API как микрослужбы.</span><span class="sxs-lookup"><span data-stu-id="c064a-154">This is particularly useful if you wish to build your API as microservices.</span></span>

<span data-ttu-id="c064a-155">Прокси-сервер может указывать на любой ресурс HTTP, например:</span><span class="sxs-lookup"><span data-stu-id="c064a-155">A proxy can point to any HTTP resource, such as:</span></span>
- <span data-ttu-id="c064a-156">Функции Azure</span><span class="sxs-lookup"><span data-stu-id="c064a-156">Azure Functions</span></span> 
- <span data-ttu-id="c064a-157">Приложения API в [службе приложений Azure](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is).</span><span class="sxs-lookup"><span data-stu-id="c064a-157">API apps in [Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)</span></span>
- <span data-ttu-id="c064a-158">Контейнеры Docker в [службе приложений под управлением Linux](https://docs.microsoft.com/azure/app-service/app-service-linux-readme).</span><span class="sxs-lookup"><span data-stu-id="c064a-158">Docker containers in [App Service on Linux](https://docs.microsoft.com/azure/app-service/app-service-linux-readme)</span></span>
- <span data-ttu-id="c064a-159">Любой другой размещенный API.</span><span class="sxs-lookup"><span data-stu-id="c064a-159">Any other hosted API</span></span>

<span data-ttu-id="c064a-160">Дополнительные сведения о прокси-сервере см. в статье [Работа с прокси Функций Azure (предварительная версия)].</span><span class="sxs-lookup"><span data-stu-id="c064a-160">To learn more about proxies, see [Working with Azure Functions Proxies (preview)].</span></span>

## <a name="create-your-first-proxy"></a><span data-ttu-id="c064a-161">Создание первого прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="c064a-161">Create your first proxy</span></span>

<span data-ttu-id="c064a-162">В этом разделе вы создадите прокси-сервер, который будет выступать в качестве интерфейса для вашего API.</span><span class="sxs-lookup"><span data-stu-id="c064a-162">In this section, you will create a new proxy which serves as a frontend to your overall API.</span></span> 

### <a name="setting-up-the-frontend-environment"></a><span data-ttu-id="c064a-163">Настройка среды интерфейса</span><span class="sxs-lookup"><span data-stu-id="c064a-163">Setting up the frontend environment</span></span>

<span data-ttu-id="c064a-164">Повторите шаги для [создания приложения-функции](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app), чтобы создать приложение-функцию, в котором вы создадите свой прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="c064a-164">Repeat the steps to [Create a function app](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) to create a new function app in which you will create your proxy.</span></span> <span data-ttu-id="c064a-165">Это новое приложение будет использоваться в качестве интерфейса для нашего API, а измененное приложение-функция — в качестве внутреннего сервера.</span><span class="sxs-lookup"><span data-stu-id="c064a-165">This new app will serve as the frontend for our API, and the function app you were previously editing will serve as a backend.</span></span>

<span data-ttu-id="c064a-166">Перейдите к своему новому приложению-функции интерфейса на портале.</span><span class="sxs-lookup"><span data-stu-id="c064a-166">Navigate to your new frontend function app in the portal.</span></span>

<span data-ttu-id="c064a-167">Выберите элемент **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="c064a-167">Select **Settings**.</span></span> <span data-ttu-id="c064a-168">Включите параметр **Использовать прокси-серверы для API-интерфейсов**.</span><span class="sxs-lookup"><span data-stu-id="c064a-168">Then toggle **Enable Azure Functions Proxies (preview)** to "On".</span></span>

<span data-ttu-id="c064a-169">Выберите **Platform Settings** (Параметры платформы), а затем — **Параметры приложения**.</span><span class="sxs-lookup"><span data-stu-id="c064a-169">Select **Platform Settings** and choose **Application Settings**.</span></span>

<span data-ttu-id="c064a-170">Прокрутите вниз до **Параметры приложения** и создайте параметр с ключом HELLO_HOST.</span><span class="sxs-lookup"><span data-stu-id="c064a-170">Scroll down to **App settings** and create a new setting with key "HELLO_HOST".</span></span> <span data-ttu-id="c064a-171">Задайте узел приложения-функции внутреннего сервера, например `<YourApp>.azurewebsites.net`, в качестве его значения.</span><span class="sxs-lookup"><span data-stu-id="c064a-171">Set its value to the host of your backend function app, such as `<YourApp>.azurewebsites.net`.</span></span> <span data-ttu-id="c064a-172">Это часть URL-адреса, скопированного ранее при тестировании функции HTTP.</span><span class="sxs-lookup"><span data-stu-id="c064a-172">This is part of the URL that you copied earlier when testing your HTTP function.</span></span> <span data-ttu-id="c064a-173">Вы укажете этот параметр при конфигурации позднее.</span><span class="sxs-lookup"><span data-stu-id="c064a-173">You'll reference this setting in the configuration later.</span></span>

> [!NOTE] 
> <span data-ttu-id="c064a-174">Мы рекомендуем использовать параметры приложения для настройки узла, чтобы прокси-сервер не зависел от жестко заданной среды.</span><span class="sxs-lookup"><span data-stu-id="c064a-174">App settings are recommended for the host configuration to prevent a hard-coded environment dependency for the proxy.</span></span> <span data-ttu-id="c064a-175">Использование настроек приложения означает, что вы можете перемещать конфигурацию прокси-сервера между средами. Параметры приложения для конкретной среды будут применяться.</span><span class="sxs-lookup"><span data-stu-id="c064a-175">Using app settings means that you can move the proxy configuration between environments, and the environment-specific app settings will be applied.</span></span>

<span data-ttu-id="c064a-176">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="c064a-176">Click **Save**.</span></span>

### <a name="creating-a-proxy-on-the-frontend"></a><span data-ttu-id="c064a-177">Создание прокси-сервера в интерфейсе</span><span class="sxs-lookup"><span data-stu-id="c064a-177">Creating a proxy on the frontend</span></span>

<span data-ttu-id="c064a-178">Вернитесь к своему приложению-функции интерфейса на портале.</span><span class="sxs-lookup"><span data-stu-id="c064a-178">Navigate back to your frontend function app in the portal.</span></span>

<span data-ttu-id="c064a-179">В области навигации слева щелкните значок "+" рядом с "Прокси (предварительная версия)".</span><span class="sxs-lookup"><span data-stu-id="c064a-179">In the left-hand navigation, click the plus sign '+' next to "Proxies (preview)".</span></span>

![Создание прокси](./media/functions-create-serverless-api/creating-proxy.png)

<span data-ttu-id="c064a-181">Используйте настройки прокси-сервера, как указано в таблице.</span><span class="sxs-lookup"><span data-stu-id="c064a-181">Use proxy settings as specified in the table.</span></span>

| <span data-ttu-id="c064a-182">Поле</span><span class="sxs-lookup"><span data-stu-id="c064a-182">Field</span></span> | <span data-ttu-id="c064a-183">Образец значения</span><span class="sxs-lookup"><span data-stu-id="c064a-183">Sample value</span></span> | <span data-ttu-id="c064a-184">Описание</span><span class="sxs-lookup"><span data-stu-id="c064a-184">Description</span></span> |
|---|---|---|
| <span data-ttu-id="c064a-185">Имя</span><span class="sxs-lookup"><span data-stu-id="c064a-185">Name</span></span> | <span data-ttu-id="c064a-186">HelloProxy</span><span class="sxs-lookup"><span data-stu-id="c064a-186">HelloProxy</span></span> | <span data-ttu-id="c064a-187">Понятное имя, используемое только для управления</span><span class="sxs-lookup"><span data-stu-id="c064a-187">A friendly name used only for management</span></span> |
| <span data-ttu-id="c064a-188">Шаблон маршрута</span><span class="sxs-lookup"><span data-stu-id="c064a-188">Route template</span></span> | <span data-ttu-id="c064a-189">/api/hello</span><span class="sxs-lookup"><span data-stu-id="c064a-189">/api/hello</span></span> | <span data-ttu-id="c064a-190">Определяет пути, используемые для вызова этого прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="c064a-190">Determines what route is used to invoke this proxy</span></span> |
| <span data-ttu-id="c064a-191">Внутренний URL-адрес</span><span class="sxs-lookup"><span data-stu-id="c064a-191">Backend URL</span></span> | <span data-ttu-id="c064a-192">https://%HELLO_HOST%/api/hello</span><span class="sxs-lookup"><span data-stu-id="c064a-192">https://%HELLO_HOST%/api/hello</span></span> | <span data-ttu-id="c064a-193">Определяет конечную точку, к которой должен быть отправлен запрос</span><span class="sxs-lookup"><span data-stu-id="c064a-193">Specifies the endpoint to which the request should be proxied</span></span> |

<span data-ttu-id="c064a-194">Обратите внимание, что прокси-сервер не предоставляет префикс базового пути `/api`, который нужно включить в шаблон маршрута.</span><span class="sxs-lookup"><span data-stu-id="c064a-194">Note that Proxies does not provide the `/api` base path prefix, and this must be included in the route template.</span></span>

<span data-ttu-id="c064a-195">Синтаксис `%HELLO_HOST%` будет ссылаться на созданный ранее параметр приложения.</span><span class="sxs-lookup"><span data-stu-id="c064a-195">The `%HELLO_HOST%` syntax will reference the app setting you created earlier.</span></span> <span data-ttu-id="c064a-196">Разрешенный URL-адрес будет указывать на исходную функцию.</span><span class="sxs-lookup"><span data-stu-id="c064a-196">The resolved URL will point to your original function.</span></span>

<span data-ttu-id="c064a-197">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c064a-197">Click **Create**.</span></span>

<span data-ttu-id="c064a-198">Вы можете испытать новый прокси-сервер, скопировав URL-адрес прокси-сервера и протестировав его в браузере или с помощью избранного клиента HTTP.</span><span class="sxs-lookup"><span data-stu-id="c064a-198">You can try out your new proxy by copying the Proxy URL and testing it in the browser or with your favorite HTTP client.</span></span>

## <a name="create-a-mock-api"></a><span data-ttu-id="c064a-199">Создание макета API</span><span class="sxs-lookup"><span data-stu-id="c064a-199">Create a mock API</span></span>

<span data-ttu-id="c064a-200">Вы создадите макет API для своего решения с помощью прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="c064a-200">Next, you will use a proxy to create a mock API for your solution.</span></span> <span data-ttu-id="c064a-201">Это позволяет разрабатывать клиент без необходимости полного внедрения внутреннего сервера.</span><span class="sxs-lookup"><span data-stu-id="c064a-201">This allows client development to progress, without needing the backend fully implemented.</span></span> <span data-ttu-id="c064a-202">Позже при разработке вы можете создать приложение-функцию, которое поддерживает эту логику, и перенаправить на него свой прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="c064a-202">Later in development, you could create a new function app which supports this logic and redirect your proxy to it.</span></span>

<span data-ttu-id="c064a-203">Чтобы создать макет API, мы создадим прокси-сервер, в этот раз с помощью [редактора службы приложений](https://github.com/projectkudu/kudu/wiki/App-Service-Editor).</span><span class="sxs-lookup"><span data-stu-id="c064a-203">To create this mock API, we will create a new proxy, this time using the [App Service Editor](https://github.com/projectkudu/kudu/wiki/App-Service-Editor).</span></span> <span data-ttu-id="c064a-204">Чтобы начать работу, перейдите к своему приложению-функции на портале.</span><span class="sxs-lookup"><span data-stu-id="c064a-204">To get started, navigate to your function app in the portal.</span></span> <span data-ttu-id="c064a-205">Выберите **Функции платформы** и найдите **редактор службы приложений**.</span><span class="sxs-lookup"><span data-stu-id="c064a-205">Select **Platform features** and find **App Service Editor**.</span></span> <span data-ttu-id="c064a-206">Если вы щелкнете его, в новой вкладке откроется редактор службы приложений.</span><span class="sxs-lookup"><span data-stu-id="c064a-206">Clicking this will open the App Service Editor in a new tab.</span></span>

<span data-ttu-id="c064a-207">В левой области навигации выберите `proxies.json`.</span><span class="sxs-lookup"><span data-stu-id="c064a-207">Select `proxies.json` in the left navigation.</span></span> <span data-ttu-id="c064a-208">Это файл, в котором хранятся конфигурации для всех ваших прокси-серверов.</span><span class="sxs-lookup"><span data-stu-id="c064a-208">This is the file which stores the configuration for all of your proxies.</span></span> <span data-ttu-id="c064a-209">Если вы используете один из [методов развертывания Функций](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), это файл, который вы будете поддерживать в системе управления версиями.</span><span class="sxs-lookup"><span data-stu-id="c064a-209">If you use one of the [Functions deployment methods](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), this is the file you will maintain in source control.</span></span> <span data-ttu-id="c064a-210">Дополнительные сведения об этом файле см. в разделе [Расширенная конфигурация](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).</span><span class="sxs-lookup"><span data-stu-id="c064a-210">To learn more about this file, see [Proxies advanced configuration](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).</span></span>

<span data-ttu-id="c064a-211">Если вы выполнили все указания пошагового руководства, ваш файл proxies.json должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c064a-211">If you've followed along so far, your proxies.json should look like the following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        }
    }
}
```

<span data-ttu-id="c064a-212">Затем добавьте макет API.</span><span class="sxs-lookup"><span data-stu-id="c064a-212">Next you'll add your mock API.</span></span> <span data-ttu-id="c064a-213">Замените свой файл proxies.json следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="c064a-213">Replace your proxies.json file with the following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        },
        "GetUserByName" : {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/users/{username}"
            },
            "responseOverrides": {
                "response.statusCode": "200",
                "response.headers.Content-Type" : "application/json",
                "response.body": {
                    "name": "{username}",
                    "description": "Awesome developer and master of serverless APIs",
                    "skills": [
                        "Serverless",
                        "APIs",
                        "Azure",
                        "Cloud"
                    ]
                }
            }
        }
    }
}
```

<span data-ttu-id="c064a-214">При этом добавляется новый прокси, GetUserByName, без свойства backendUri.</span><span class="sxs-lookup"><span data-stu-id="c064a-214">This adds a new proxy, "GetUserByName", without the backendUri property.</span></span> <span data-ttu-id="c064a-215">Вместо вызова другого ресурса он изменяет ответ по умолчанию от прокси-серверов, используя переопределение ответа.</span><span class="sxs-lookup"><span data-stu-id="c064a-215">Instead of calling another resource, it modifies the default response from Proxies using a response override.</span></span> <span data-ttu-id="c064a-216">Переопределение запроса и ответа может также использоваться в сочетании с URL-адресом внутреннего сервера.</span><span class="sxs-lookup"><span data-stu-id="c064a-216">Request and response overrides can also be used in conjunction with a backend URL.</span></span> <span data-ttu-id="c064a-217">Это особенно полезно при перенаправлении к устаревшим системам, где вам может потребоваться изменить заголовки, параметры запроса и т. д. Дополнительные сведения о переопределении запроса и ответа см. в [этой статье](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).</span><span class="sxs-lookup"><span data-stu-id="c064a-217">This is particularly useful when proxying to a legacy system, where you might need to modify headers, query parameters, etc. To learn more about request and response overrides, see [Modifying requests and responses in Proxies](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).</span></span>

<span data-ttu-id="c064a-218">Протестируйте макет API, вызвав конечную точку `/api/users/{username}` с помощью браузера или избранного клиента REST.</span><span class="sxs-lookup"><span data-stu-id="c064a-218">Test your mock API by calling the `/api/users/{username}` endpoint using a browser or your favorite REST client.</span></span> <span data-ttu-id="c064a-219">Замените _{username}_ строковым значением, представляющим имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="c064a-219">Be sure to replace _{username}_ with a string value representing a username.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c064a-220">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c064a-220">Next steps</span></span>

<span data-ttu-id="c064a-221">В этом руководстве вы научились создавать и настраивать API с помощью решения "Функции Azure",</span><span class="sxs-lookup"><span data-stu-id="c064a-221">In this tutorial, you learned how to build and customize an API on Azure Functions.</span></span> <span data-ttu-id="c064a-222">а также объединять несколько API, включая макеты, в единую поверхность API.</span><span class="sxs-lookup"><span data-stu-id="c064a-222">You also learned how to bring multiple APIs, including mocks, together as a unified API surface.</span></span> <span data-ttu-id="c064a-223">Вы можете использовать эти методы для создания API любой сложности, работая в бессерверной вычислительной модели, предоставляемой Функциями Azure.</span><span class="sxs-lookup"><span data-stu-id="c064a-223">You can use these techniques to build out APIs of any complexity, all while running on the serverless compute model provided by Azure Functions.</span></span>

<span data-ttu-id="c064a-224">Следующие ссылки могут оказаться полезными при дальнейшей разработке API:</span><span class="sxs-lookup"><span data-stu-id="c064a-224">The following references may be helpful as you develop your API further:</span></span>

- [<span data-ttu-id="c064a-225">Привязки HTTP и webhook в функциях Azure</span><span class="sxs-lookup"><span data-stu-id="c064a-225">Azure Functions HTTP and webhook bindings</span></span>](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook)
- <span data-ttu-id="c064a-226">[Работа с прокси Функций Azure (предварительная версия)]</span><span class="sxs-lookup"><span data-stu-id="c064a-226">[Working with Azure Functions Proxies (preview)]</span></span>
- [<span data-ttu-id="c064a-227">Создание метаданных OpenAPI 2.0 (Swagger) для приложения-функции (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="c064a-227">Documenting an Azure Functions API (preview)</span></span>](https://docs.microsoft.com/azure/azure-functions/functions-api-definition-getting-started)


[Create your first function]: https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function
[Работа с прокси Функций Azure (предварительная версия)]: https://docs.microsoft.com/azure/azure-functions/functions-proxies
