---
title: "aaaCreate без сервера API, с помощью функции Azure | Документы Microsoft"
description: "Как toocreate без сервера API, с помощью функции Azure"
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
ms.openlocfilehash: 877e3b229d5477fc5fec594ccd284fb55d7f3c07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-serverless-api-using-azure-functions"></a><span data-ttu-id="13ed3-103">Создание бессерверного API с помощью Функций Azure</span><span class="sxs-lookup"><span data-stu-id="13ed3-103">Create a serverless API using Azure Functions</span></span>

<span data-ttu-id="13ed3-104">В этом учебнике вы узнаете, как функции Azure обеспечивает toobuild высокомасштабируемых API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="13ed3-104">In this tutorial you will learn how Azure Functions allows you toobuild highly-scalable APIs.</span></span> <span data-ttu-id="13ed3-105">Функции Azure сочетается с набором встроенных триггеров HTTP и привязками, что позволяет легко tooauthor конечную точку в различных языках, включая Node.JS, C# и многое другое.</span><span class="sxs-lookup"><span data-stu-id="13ed3-105">Azure Functions comes with a collection of built-in HTTP triggers and bindings which make it easy tooauthor an endpoint in a variety of languages, including Node.JS, C#, and more.</span></span> <span data-ttu-id="13ed3-106">В этом учебнике будет выполнена настройка триггера HTTP toohandle определенных действий в конструкции своего API.</span><span class="sxs-lookup"><span data-stu-id="13ed3-106">In this tutorial, you will customize an HTTP trigger toohandle specific actions in your API design.</span></span> <span data-ttu-id="13ed3-107">Вы также подготовите ваш API к увеличению размеров, интегрировав его с прокси-серверами Функций Azure и установив макет API.</span><span class="sxs-lookup"><span data-stu-id="13ed3-107">You will also prepare for growing your API by integrating it with Azure Functions Proxies and setting up mock APIs.</span></span> <span data-ttu-id="13ed3-108">Все это можно сделать поверх hello функции без сервера вычислительную среду, поэтому tooworry о масштабировании ресурсов не нужно — просто позволяет сосредоточиться на логике API.</span><span class="sxs-lookup"><span data-stu-id="13ed3-108">All of this is accomplished on top of hello Functions serverless compute environment, so you don't have tooworry about scaling resources - you can just focus on your API logic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="13ed3-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="13ed3-109">Prerequisites</span></span> 

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

<span data-ttu-id="13ed3-110">Полученная функция Hello будет использоваться для hello конца данного учебника.</span><span class="sxs-lookup"><span data-stu-id="13ed3-110">hello resulting function will be used for hello rest of this tutorial.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="13ed3-111">Войдите в tooAzure</span><span class="sxs-lookup"><span data-stu-id="13ed3-111">Sign in tooAzure</span></span>

<span data-ttu-id="13ed3-112">Здравствуйте, откройте портал Azure.</span><span class="sxs-lookup"><span data-stu-id="13ed3-112">Open hello Azure portal.</span></span> <span data-ttu-id="13ed3-113">toodo, вход слишком[https://portal.azure.com](https://portal.azure.com) с учетной записью Azure.</span><span class="sxs-lookup"><span data-stu-id="13ed3-113">toodo this, sign in too[https://portal.azure.com](https://portal.azure.com) with your Azure account.</span></span>

## <a name="customize-your-http-function"></a><span data-ttu-id="13ed3-114">Настройка функции HTTP</span><span class="sxs-lookup"><span data-stu-id="13ed3-114">Customize your HTTP function</span></span>

<span data-ttu-id="13ed3-115">По умолчанию функции активации HTTP является настроенным tooaccept любой метод HTTP.</span><span class="sxs-lookup"><span data-stu-id="13ed3-115">By default, your HTTP-triggered function is configured tooaccept any HTTP method.</span></span> <span data-ttu-id="13ed3-116">Отсутствует URL-адрес по умолчанию hello формы `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`.</span><span class="sxs-lookup"><span data-stu-id="13ed3-116">There is also a default URL of hello form `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`.</span></span> <span data-ttu-id="13ed3-117">Если вы следовали hello краткое руководство, затем `<funcname>` , скорее всего, будет выглядеть примерно так «HttpTriggerJS1».</span><span class="sxs-lookup"><span data-stu-id="13ed3-117">If you followed hello quickstart, then `<funcname>` probably looks something like "HttpTriggerJS1".</span></span> <span data-ttu-id="13ed3-118">В этом разделе будет изменить hello функция toorespond только tooGET запросов к `/api/hello` вместо маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="13ed3-118">In this section, you will modify hello function toorespond only tooGET requests against `/api/hello` route instead.</span></span> 

<span data-ttu-id="13ed3-119">Перейдите tooyour функции hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="13ed3-119">Navigate tooyour function in hello Azure portal.</span></span> <span data-ttu-id="13ed3-120">Выберите **Интеграция** в hello навигации слева.</span><span class="sxs-lookup"><span data-stu-id="13ed3-120">Select **Integrate** in hello left navigation.</span></span>

![Настройка функции HTTP](./media/functions-create-serverless-api/customizing-http.png)

<span data-ttu-id="13ed3-122">Используйте параметры триггера HTTP, как указано в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="13ed3-122">Use the HTTP trigger settings as specified in hello table.</span></span>

| <span data-ttu-id="13ed3-123">Поле</span><span class="sxs-lookup"><span data-stu-id="13ed3-123">Field</span></span> | <span data-ttu-id="13ed3-124">Образец значения</span><span class="sxs-lookup"><span data-stu-id="13ed3-124">Sample value</span></span> | <span data-ttu-id="13ed3-125">Описание</span><span class="sxs-lookup"><span data-stu-id="13ed3-125">Description</span></span> |
|---|---|---|
| <span data-ttu-id="13ed3-126">Разрешенные методы HTTP</span><span class="sxs-lookup"><span data-stu-id="13ed3-126">Allowed HTTP methods</span></span> | <span data-ttu-id="13ed3-127">Выбранные методы</span><span class="sxs-lookup"><span data-stu-id="13ed3-127">Selected methods</span></span> | <span data-ttu-id="13ed3-128">Определяет, какие методы HTTP может быть tooinvoke используется эта функция</span><span class="sxs-lookup"><span data-stu-id="13ed3-128">Determines what HTTP methods may be used tooinvoke this function</span></span> |
| <span data-ttu-id="13ed3-129">Выбранные методы HTTP</span><span class="sxs-lookup"><span data-stu-id="13ed3-129">Selected HTTP methods</span></span> | <span data-ttu-id="13ed3-130">ПОЛУЧЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="13ed3-130">GET</span></span> | <span data-ttu-id="13ed3-131">Разрешает только выбранных toobe методы HTTP, используемых tooinvoke этой функции</span><span class="sxs-lookup"><span data-stu-id="13ed3-131">Allows only selected HTTP methods toobe used tooinvoke this function</span></span> |
| <span data-ttu-id="13ed3-132">Шаблон маршрута</span><span class="sxs-lookup"><span data-stu-id="13ed3-132">Route template</span></span> | <span data-ttu-id="13ed3-133">/hello</span><span class="sxs-lookup"><span data-stu-id="13ed3-133">/hello</span></span> | <span data-ttu-id="13ed3-134">Определяет, какие маршрута используется tooinvoke этой функции</span><span class="sxs-lookup"><span data-stu-id="13ed3-134">Determines what route is used tooinvoke this function</span></span> |

<span data-ttu-id="13ed3-135">Обратите внимание, что не содержит hello `/api` основной префикс пути в шаблоне маршрута hello, как обрабатывается глобальный параметр.</span><span class="sxs-lookup"><span data-stu-id="13ed3-135">Note that you did not include hello `/api` base path prefix in hello route template, as this is handled by a global setting.</span></span>

<span data-ttu-id="13ed3-136">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="13ed3-136">Click **Save**.</span></span>

<span data-ttu-id="13ed3-137">Дополнительные сведения см. в статье [Привязки HTTP и webhook в функциях Azure](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).</span><span class="sxs-lookup"><span data-stu-id="13ed3-137">You can learn more about customizing HTTP functions in [Azure Functions HTTP and webhook bindings](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).</span></span>

### <a name="test-your-api"></a><span data-ttu-id="13ed3-138">Тестирование API</span><span class="sxs-lookup"><span data-stu-id="13ed3-138">Test your API</span></span>

<span data-ttu-id="13ed3-139">Теперь необходимо проверьте на toosee функция его работа с hello новую поверхность API.</span><span class="sxs-lookup"><span data-stu-id="13ed3-139">Next, test your function toosee it working with hello new API surface.</span></span>

<span data-ttu-id="13ed3-140">Перейдите назад toohello разработки страницы, щелкнув имя функции hello в hello навигации слева.</span><span class="sxs-lookup"><span data-stu-id="13ed3-140">Navigate back toohello development page by clicking on hello function's name in hello left navigation.</span></span>

<span data-ttu-id="13ed3-141">Нажмите кнопку **получить URL-адрес функции** и скопируйте URL-адрес hello.</span><span class="sxs-lookup"><span data-stu-id="13ed3-141">Click **Get function URL** and copy hello URL.</span></span> <span data-ttu-id="13ed3-142">Вы увидите, что он использует hello `/api/hello` теперь маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="13ed3-142">You should see that it uses hello `/api/hello` route now.</span></span>

<span data-ttu-id="13ed3-143">Скопируйте URL-адрес hello в новую вкладку браузера или предпочтительный клиент REST.</span><span class="sxs-lookup"><span data-stu-id="13ed3-143">Copy hello URL into a new browser tab or your preferred REST client.</span></span> <span data-ttu-id="13ed3-144">По умолчанию браузер использует функцию GET.</span><span class="sxs-lookup"><span data-stu-id="13ed3-144">Browsers will use GET by default.</span></span>

<span data-ttu-id="13ed3-145">Запустите функции hello и убедитесь, что он работает.</span><span class="sxs-lookup"><span data-stu-id="13ed3-145">Run hello function and confirm that it is working.</span></span> <span data-ttu-id="13ed3-146">Параметр «name» hello tooprovide может потребоваться как краткое руководство кода hello toosatisfy строку запроса.</span><span class="sxs-lookup"><span data-stu-id="13ed3-146">You may need tooprovide hello "name" parameter as a query string toosatisfy hello quickstart code.</span></span>

<span data-ttu-id="13ed3-147">Можно также попытаться вызова hello конечной точки с другой tooconfirm метод HTTP, что функция hello не выполняется.</span><span class="sxs-lookup"><span data-stu-id="13ed3-147">You can also try calling hello endpoint with another HTTP method tooconfirm that hello function is not executed.</span></span> <span data-ttu-id="13ed3-148">Для этого потребуется toouse клиента REST, например перелистывание, почтальон или Fiddler.</span><span class="sxs-lookup"><span data-stu-id="13ed3-148">For this, you will need toouse a REST client, such as cURL, Postman, or Fiddler.</span></span>

## <a name="proxies-overview"></a><span data-ttu-id="13ed3-149">Общие сведения о прокси-серверах</span><span class="sxs-lookup"><span data-stu-id="13ed3-149">Proxies overview</span></span>

<span data-ttu-id="13ed3-150">В следующем разделе hello обнаружатся API через прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="13ed3-150">In hello next section, you will surface your API through a proxy.</span></span> <span data-ttu-id="13ed3-151">Azure функции прокси имеет функцию предварительного просмотра, позволяющая ресурсы tooother tooforward запросов.</span><span class="sxs-lookup"><span data-stu-id="13ed3-151">Azure Functions Proxies is a preview feature that allows you tooforward requests tooother resources.</span></span> <span data-ttu-id="13ed3-152">Так же, как определить конечную точку HTTP с триггером HTTP, но вместо написания кода tooexecute при вызове этой конечной точки, можно предоставить реализацию удаленного tooa URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="13ed3-152">You define an HTTP endpoint just like with HTTP trigger, but instead of writing code tooexecute when that endpoint is called, you provide a URL tooa remote implementation.</span></span> <span data-ttu-id="13ed3-153">Это позволяет toocompose API нескольких источников в одну область API, которой могут легко tooconsume клиентов.</span><span class="sxs-lookup"><span data-stu-id="13ed3-153">This allows you toocompose multiple API sources into a single API surface which is easy for clients tooconsume.</span></span> <span data-ttu-id="13ed3-154">Это особенно полезно в том случае, если вы хотите toobuild API как микрослужбами.</span><span class="sxs-lookup"><span data-stu-id="13ed3-154">This is particularly useful if you wish toobuild your API as microservices.</span></span>

<span data-ttu-id="13ed3-155">Прокси-сервер может указывать ресурсов tooany HTTP, такие как:</span><span class="sxs-lookup"><span data-stu-id="13ed3-155">A proxy can point tooany HTTP resource, such as:</span></span>
- <span data-ttu-id="13ed3-156">Функции Azure</span><span class="sxs-lookup"><span data-stu-id="13ed3-156">Azure Functions</span></span> 
- <span data-ttu-id="13ed3-157">Приложения API в [службе приложений Azure](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is).</span><span class="sxs-lookup"><span data-stu-id="13ed3-157">API apps in [Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)</span></span>
- <span data-ttu-id="13ed3-158">Контейнеры Docker в [службе приложений под управлением Linux](https://docs.microsoft.com/azure/app-service/app-service-linux-readme).</span><span class="sxs-lookup"><span data-stu-id="13ed3-158">Docker containers in [App Service on Linux](https://docs.microsoft.com/azure/app-service/app-service-linux-readme)</span></span>
- <span data-ttu-id="13ed3-159">Любой другой размещенный API.</span><span class="sxs-lookup"><span data-stu-id="13ed3-159">Any other hosted API</span></span>

<span data-ttu-id="13ed3-160">toolearn Дополнительные сведения о прокси-серверы, в разделе [работа с прокси-серверы функции Azure (Предварительная версия)].</span><span class="sxs-lookup"><span data-stu-id="13ed3-160">toolearn more about proxies, see [Working with Azure Functions Proxies (preview)].</span></span>

## <a name="create-your-first-proxy"></a><span data-ttu-id="13ed3-161">Создание первого прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="13ed3-161">Create your first proxy</span></span>

<span data-ttu-id="13ed3-162">В этом разделе вы создадите новый прокси какие служит в качестве tooyour переднего плана общий API.</span><span class="sxs-lookup"><span data-stu-id="13ed3-162">In this section, you will create a new proxy which serves as a frontend tooyour overall API.</span></span> 

### <a name="setting-up-hello-frontend-environment"></a><span data-ttu-id="13ed3-163">Настройка среды hello переднего плана</span><span class="sxs-lookup"><span data-stu-id="13ed3-163">Setting up hello frontend environment</span></span>

<span data-ttu-id="13ed3-164">Повторите шаги hello слишком[создать приложение функция](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) toocreate новое приложение функции, в которой будет создан прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="13ed3-164">Repeat hello steps too[Create a function app](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) toocreate a new function app in which you will create your proxy.</span></span> <span data-ttu-id="13ed3-165">Это новое приложение будет служить hello переднего плана для наших API и приложение hello функция, которую вы редактировали будет служить в качестве серверной части.</span><span class="sxs-lookup"><span data-stu-id="13ed3-165">This new app will serve as hello frontend for our API, and hello function app you were previously editing will serve as a backend.</span></span>

<span data-ttu-id="13ed3-166">Перейдите в новое приложение функция переднего плана tooyour hello портала.</span><span class="sxs-lookup"><span data-stu-id="13ed3-166">Navigate tooyour new frontend function app in hello portal.</span></span>

<span data-ttu-id="13ed3-167">Выберите элемент **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="13ed3-167">Select **Settings**.</span></span> <span data-ttu-id="13ed3-168">Затем переключать **включить Azure функции прокси-серверов (Предварительная версия)** слишком «On».</span><span class="sxs-lookup"><span data-stu-id="13ed3-168">Then toggle **Enable Azure Functions Proxies (preview)** too"On".</span></span>

<span data-ttu-id="13ed3-169">Выберите **Platform Settings** (Параметры платформы), а затем — **Параметры приложения**.</span><span class="sxs-lookup"><span data-stu-id="13ed3-169">Select **Platform Settings** and choose **Application Settings**.</span></span>

<span data-ttu-id="13ed3-170">Прокрутите список вниз слишком**параметры приложения** и создать новый параметр с ключом «HELLO_HOST».</span><span class="sxs-lookup"><span data-stu-id="13ed3-170">Scroll down too**App settings** and create a new setting with key "HELLO_HOST".</span></span> <span data-ttu-id="13ed3-171">Задать ведущим toohello значение серверной части функции приложения, например `<YourApp>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="13ed3-171">Set its value toohello host of your backend function app, such as `<YourApp>.azurewebsites.net`.</span></span> <span data-ttu-id="13ed3-172">Это часть URL-адреса hello, скопированное ранее при тестировании функции HTTP.</span><span class="sxs-lookup"><span data-stu-id="13ed3-172">This is part of hello URL that you copied earlier when testing your HTTP function.</span></span> <span data-ttu-id="13ed3-173">Будет ссылаться этот параметр в конфигурации hello позже.</span><span class="sxs-lookup"><span data-stu-id="13ed3-173">You'll reference this setting in hello configuration later.</span></span>

> [!NOTE] 
> <span data-ttu-id="13ed3-174">Параметры приложения рекомендуется использовать tooprevent конфигурации узла hello зависимость жестко среды для hello прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="13ed3-174">App settings are recommended for hello host configuration tooprevent a hard-coded environment dependency for hello proxy.</span></span> <span data-ttu-id="13ed3-175">С помощью параметров приложения означает, что hello конфигурация прокси-сервера можно переместить между средами и будут применены параметры среды приложения hello.</span><span class="sxs-lookup"><span data-stu-id="13ed3-175">Using app settings means that you can move hello proxy configuration between environments, and hello environment-specific app settings will be applied.</span></span>

<span data-ttu-id="13ed3-176">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="13ed3-176">Click **Save**.</span></span>

### <a name="creating-a-proxy-on-hello-frontend"></a><span data-ttu-id="13ed3-177">Создание учетной записи-посредника на сервере переднего плана hello</span><span class="sxs-lookup"><span data-stu-id="13ed3-177">Creating a proxy on hello frontend</span></span>

<span data-ttu-id="13ed3-178">Перейдите назад tooyour переднего плана функции приложения hello портала.</span><span class="sxs-lookup"><span data-stu-id="13ed3-178">Navigate back tooyour frontend function app in hello portal.</span></span>

<span data-ttu-id="13ed3-179">В левой области навигации hello щелкните hello знак плюс «+» Далее слишком «Прокси-сервер (Предварительная версия)».</span><span class="sxs-lookup"><span data-stu-id="13ed3-179">In hello left-hand navigation, click hello plus sign '+' next too"Proxies (preview)".</span></span>

![Создание прокси](./media/functions-create-serverless-api/creating-proxy.png)

<span data-ttu-id="13ed3-181">Используйте параметры прокси-сервера, как указано в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="13ed3-181">Use proxy settings as specified in hello table.</span></span>

| <span data-ttu-id="13ed3-182">Поле</span><span class="sxs-lookup"><span data-stu-id="13ed3-182">Field</span></span> | <span data-ttu-id="13ed3-183">Образец значения</span><span class="sxs-lookup"><span data-stu-id="13ed3-183">Sample value</span></span> | <span data-ttu-id="13ed3-184">Описание</span><span class="sxs-lookup"><span data-stu-id="13ed3-184">Description</span></span> |
|---|---|---|
| <span data-ttu-id="13ed3-185">Имя</span><span class="sxs-lookup"><span data-stu-id="13ed3-185">Name</span></span> | <span data-ttu-id="13ed3-186">HelloProxy</span><span class="sxs-lookup"><span data-stu-id="13ed3-186">HelloProxy</span></span> | <span data-ttu-id="13ed3-187">Понятное имя, используемое только для управления</span><span class="sxs-lookup"><span data-stu-id="13ed3-187">A friendly name used only for management</span></span> |
| <span data-ttu-id="13ed3-188">Шаблон маршрута</span><span class="sxs-lookup"><span data-stu-id="13ed3-188">Route template</span></span> | <span data-ttu-id="13ed3-189">/api/hello</span><span class="sxs-lookup"><span data-stu-id="13ed3-189">/api/hello</span></span> | <span data-ttu-id="13ed3-190">Определяет, какие маршрута используется tooinvoke этот прокси-сервер</span><span class="sxs-lookup"><span data-stu-id="13ed3-190">Determines what route is used tooinvoke this proxy</span></span> |
| <span data-ttu-id="13ed3-191">Внутренний URL-адрес</span><span class="sxs-lookup"><span data-stu-id="13ed3-191">Backend URL</span></span> | <span data-ttu-id="13ed3-192">https://%HELLO_HOST%/api/hello</span><span class="sxs-lookup"><span data-stu-id="13ed3-192">https://%HELLO_HOST%/api/hello</span></span> | <span data-ttu-id="13ed3-193">Указывает, что запроса hello toowhich hello конечной точки должно быть прокси</span><span class="sxs-lookup"><span data-stu-id="13ed3-193">Specifies hello endpoint toowhich hello request should be proxied</span></span> |

<span data-ttu-id="13ed3-194">Обратите внимание, что учетные записи-посредники не предоставляет hello `/api` префикс пути к базовой папке и это должно быть включено в шаблон маршрута hello.</span><span class="sxs-lookup"><span data-stu-id="13ed3-194">Note that Proxies does not provide hello `/api` base path prefix, and this must be included in hello route template.</span></span>

<span data-ttu-id="13ed3-195">Hello `%HELLO_HOST%` синтаксис будет ссылаться на параметр приложения hello, созданного ранее.</span><span class="sxs-lookup"><span data-stu-id="13ed3-195">hello `%HELLO_HOST%` syntax will reference hello app setting you created earlier.</span></span> <span data-ttu-id="13ed3-196">Hello разрешен URL-адрес будет указывать tooyour исходной функции.</span><span class="sxs-lookup"><span data-stu-id="13ed3-196">hello resolved URL will point tooyour original function.</span></span>

<span data-ttu-id="13ed3-197">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="13ed3-197">Click **Create**.</span></span>

<span data-ttu-id="13ed3-198">Можно опробовать новый прокси-сервера путем копирования hello URL-адрес прокси-сервера и его тестирование в браузере hello или с HTTP клиента по вашему выбору.</span><span class="sxs-lookup"><span data-stu-id="13ed3-198">You can try out your new proxy by copying hello Proxy URL and testing it in hello browser or with your favorite HTTP client.</span></span>

## <a name="create-a-mock-api"></a><span data-ttu-id="13ed3-199">Создание макета API</span><span class="sxs-lookup"><span data-stu-id="13ed3-199">Create a mock API</span></span>

<span data-ttu-id="13ed3-200">Далее будет использовать прокси-сервер toocreate макетов API для вашего решения.</span><span class="sxs-lookup"><span data-stu-id="13ed3-200">Next, you will use a proxy toocreate a mock API for your solution.</span></span> <span data-ttu-id="13ed3-201">Это позволяет Разработка клиентских приложений tooprogress без необходимости полностью реализован серверной hello.</span><span class="sxs-lookup"><span data-stu-id="13ed3-201">This allows client development tooprogress, without needing hello backend fully implemented.</span></span> <span data-ttu-id="13ed3-202">Позже при разработке можно создать новое приложение функция, которая поддерживает эту логику и перенаправления вашей tooit прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="13ed3-202">Later in development, you could create a new function app which supports this logic and redirect your proxy tooit.</span></span>

<span data-ttu-id="13ed3-203">toocreate данный макет API, мы создадим новый прокси-сервер, с применением hello [редактор службы приложения](https://github.com/projectkudu/kudu/wiki/App-Service-Editor).</span><span class="sxs-lookup"><span data-stu-id="13ed3-203">toocreate this mock API, we will create a new proxy, this time using hello [App Service Editor](https://github.com/projectkudu/kudu/wiki/App-Service-Editor).</span></span> <span data-ttu-id="13ed3-204">tooget к работе, перейдите tooyour функции приложения hello портала.</span><span class="sxs-lookup"><span data-stu-id="13ed3-204">tooget started, navigate tooyour function app in hello portal.</span></span> <span data-ttu-id="13ed3-205">Выберите **Функции платформы** и найдите **редактор службы приложений**.</span><span class="sxs-lookup"><span data-stu-id="13ed3-205">Select **Platform features** and find **App Service Editor**.</span></span> <span data-ttu-id="13ed3-206">При нажатии этой кнопки открывается редактор службы приложения hello в новой вкладке.</span><span class="sxs-lookup"><span data-stu-id="13ed3-206">Clicking this will open hello App Service Editor in a new tab.</span></span>

<span data-ttu-id="13ed3-207">Выберите `proxies.json` в hello навигации слева.</span><span class="sxs-lookup"><span data-stu-id="13ed3-207">Select `proxies.json` in hello left navigation.</span></span> <span data-ttu-id="13ed3-208">Это файл hello, в котором хранятся hello конфигурации для всех прокси.</span><span class="sxs-lookup"><span data-stu-id="13ed3-208">This is hello file which stores hello configuration for all of your proxies.</span></span> <span data-ttu-id="13ed3-209">При использовании hello [функции методы развертывания](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), это файл hello будут обслуживаться в системе управления версиями.</span><span class="sxs-lookup"><span data-stu-id="13ed3-209">If you use one of hello [Functions deployment methods](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), this is hello file you will maintain in source control.</span></span> <span data-ttu-id="13ed3-210">toolearn более об этом файле см [учетные записи-посредники Расширенная конфигурация](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).</span><span class="sxs-lookup"><span data-stu-id="13ed3-210">toolearn more about this file, see [Proxies advanced configuration](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).</span></span>

<span data-ttu-id="13ed3-211">Если вы выполнили моменту, ваш proxies.json должен выглядеть hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="13ed3-211">If you've followed along so far, your proxies.json should look like hello following:</span></span>

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

<span data-ttu-id="13ed3-212">Затем добавьте макет API.</span><span class="sxs-lookup"><span data-stu-id="13ed3-212">Next you'll add your mock API.</span></span> <span data-ttu-id="13ed3-213">Замените файл proxies.json hello следующее:</span><span class="sxs-lookup"><span data-stu-id="13ed3-213">Replace your proxies.json file with hello following:</span></span>

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

<span data-ttu-id="13ed3-214">При этом добавляется новый прокси, «GetUserByName» без свойства backendUri hello.</span><span class="sxs-lookup"><span data-stu-id="13ed3-214">This adds a new proxy, "GetUserByName", without hello backendUri property.</span></span> <span data-ttu-id="13ed3-215">Вместо того чтобы вызывать другой ресурс, она изменяет hello ответа по умолчанию из прокси-серверы, используя переопределения ответа.</span><span class="sxs-lookup"><span data-stu-id="13ed3-215">Instead of calling another resource, it modifies hello default response from Proxies using a response override.</span></span> <span data-ttu-id="13ed3-216">Переопределение запроса и ответа может также использоваться в сочетании с URL-адресом внутреннего сервера.</span><span class="sxs-lookup"><span data-stu-id="13ed3-216">Request and response overrides can also be used in conjunction with a backend URL.</span></span> <span data-ttu-id="13ed3-217">Это особенно полезно, когда перенаправление tooa устаревших систем, требующие toomodify заголовки, параметры запроса, toolearn т. д. Дополнительные сведения о переопределения запроса и ответа, в разделе [изменение запросов и ответов в прокси-](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).</span><span class="sxs-lookup"><span data-stu-id="13ed3-217">This is particularly useful when proxying tooa legacy system, where you might need toomodify headers, query parameters, etc. toolearn more about request and response overrides, see [Modifying requests and responses in Proxies](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).</span></span>

<span data-ttu-id="13ed3-218">Протестируйте макетов API, вызывающему Привет `/api/users/{username}` конечную точку с помощью браузера или REST клиента по вашему выбору.</span><span class="sxs-lookup"><span data-stu-id="13ed3-218">Test your mock API by calling hello `/api/users/{username}` endpoint using a browser or your favorite REST client.</span></span> <span data-ttu-id="13ed3-219">Быть убедиться, что tooreplace _{username}_ с строковое значение, представляющее имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="13ed3-219">Be sure tooreplace _{username}_ with a string value representing a username.</span></span>

## <a name="next-steps"></a><span data-ttu-id="13ed3-220">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="13ed3-220">Next steps</span></span>

<span data-ttu-id="13ed3-221">В этом учебнике вы узнали, как toobuild и настраивать API для функций Azure.</span><span class="sxs-lookup"><span data-stu-id="13ed3-221">In this tutorial, you learned how toobuild and customize an API on Azure Functions.</span></span> <span data-ttu-id="13ed3-222">Вы также узнали, как toobring несколько API, в том числе фиктивных, друг с другом виде единой рабочей области API.</span><span class="sxs-lookup"><span data-stu-id="13ed3-222">You also learned how toobring multiple APIs, including mocks, together as a unified API surface.</span></span> <span data-ttu-id="13ed3-223">Можно использовать эти методы toobuild out API-интерфейсы любой сложности, все время работы на hello без сервера вычислений модели, предоставляемой функций Azure.</span><span class="sxs-lookup"><span data-stu-id="13ed3-223">You can use these techniques toobuild out APIs of any complexity, all while running on hello serverless compute model provided by Azure Functions.</span></span>

<span data-ttu-id="13ed3-224">Hello следующие ссылки могут пригодиться при разработке дальнейшей API:</span><span class="sxs-lookup"><span data-stu-id="13ed3-224">hello following references may be helpful as you develop your API further:</span></span>

- [<span data-ttu-id="13ed3-225">Привязки HTTP и webhook в функциях Azure</span><span class="sxs-lookup"><span data-stu-id="13ed3-225">Azure Functions HTTP and webhook bindings</span></span>](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook)
- <span data-ttu-id="13ed3-226">[работа с прокси-серверы функции Azure (Предварительная версия)]</span><span class="sxs-lookup"><span data-stu-id="13ed3-226">[Working with Azure Functions Proxies (preview)]</span></span>
- [<span data-ttu-id="13ed3-227">Создание метаданных OpenAPI 2.0 (Swagger) для приложения-функции (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="13ed3-227">Documenting an Azure Functions API (preview)</span></span>](https://docs.microsoft.com/azure/azure-functions/functions-api-definition-getting-started)


[Create your first function]: https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function
[работа с прокси-серверы функции Azure (Предварительная версия)]: https://docs.microsoft.com/azure/azure-functions/functions-proxies
