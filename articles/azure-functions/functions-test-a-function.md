---
title: "aaaTesting функции Azure | Документы Microsoft"
description: "Тестирование функций Azure с помощью Postman, cURL и Node.js."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "функции azure, функции, обработка событий, webhook, динамические вычисления, независимая архитектура, тестирование"
ms.assetid: c00f3082-30d2-46b3-96ea-34faf2f15f77
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 02/02/2017
ms.author: wesmc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a084f8dbc8089356c3c19d789dc9098f2bb63052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="strategies-for-testing-your-code-in-azure-functions"></a><span data-ttu-id="49730-104">Методика тестирования кода с помощью Функций Azure</span><span class="sxs-lookup"><span data-stu-id="49730-104">Strategies for testing your code in Azure Functions</span></span>

<span data-ttu-id="49730-105">В этом разделе показаны различные функции tootest способами, включая использование hello следующие общие подходы hello:</span><span class="sxs-lookup"><span data-stu-id="49730-105">This topic demonstrates hello various ways tootest functions, including using hello following general approaches:</span></span>

+ <span data-ttu-id="49730-106">инструменты на основе HTTP, например cURL, Postman и даже веб-браузер для веб-триггеров;</span><span class="sxs-lookup"><span data-stu-id="49730-106">HTTP-based tools, such as cURL, Postman, and even a web browser for web-based triggers</span></span>
+ <span data-ttu-id="49730-107">Azure Storage Explorer tootest триггеры, основанные на хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="49730-107">Azure Storage Explorer, tootest Azure Storage-based triggers</span></span>
+ <span data-ttu-id="49730-108">Вкладка теста на портале Azure функции hello</span><span class="sxs-lookup"><span data-stu-id="49730-108">Test tab in hello Azure Functions portal</span></span>
+ <span data-ttu-id="49730-109">активируемая по таймеру функция;</span><span class="sxs-lookup"><span data-stu-id="49730-109">Timer-triggered function</span></span>
+ <span data-ttu-id="49730-110">приложение или платформа для тестирования.</span><span class="sxs-lookup"><span data-stu-id="49730-110">Testing application or framework</span></span>

<span data-ttu-id="49730-111">Все эти методы тестирования использовать функцию триггер HTTP, принимающее вводимые данные через текст запроса hello или параметр строки запроса.</span><span class="sxs-lookup"><span data-stu-id="49730-111">All these testing methods use an HTTP trigger function that accepts input through either a query string parameter or hello request body.</span></span> <span data-ttu-id="49730-112">В первом разделе hello создания этой функции.</span><span class="sxs-lookup"><span data-stu-id="49730-112">You create this function in hello first section.</span></span>

## <a name="create-a-function-for-testing"></a><span data-ttu-id="49730-113">Создание функции для тестирования</span><span class="sxs-lookup"><span data-stu-id="49730-113">Create a function for testing</span></span>
<span data-ttu-id="49730-114">Для большей части этого учебника мы используем немного измененной версии шаблона функции HttpTrigger JavaScript, который будет использоваться при создании функции hello.</span><span class="sxs-lookup"><span data-stu-id="49730-114">For most of this tutorial, we use a slightly modified version of hello HttpTrigger JavaScript function template that is available when you create a function.</span></span> <span data-ttu-id="49730-115">Если вам нужна помощь при создании функции, просмотрите этот [учебник](functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="49730-115">If you need help creating a function, review this [tutorial](functions-create-first-azure-function.md).</span></span> <span data-ttu-id="49730-116">Выберите hello **HttpTrigger - JavaScript** шаблона при создании тестовой функции hello в hello [портал Azure].</span><span class="sxs-lookup"><span data-stu-id="49730-116">Choose hello **HttpTrigger- JavaScript** template when creating hello test function in hello [Azure portal].</span></span>

<span data-ttu-id="49730-117">Hello шаблона функции по умолчанию является по сути «hello world» функцией, выводящий имя серверной hello из hello запроса текст или параметром строки запроса, `name=<your name>`.</span><span class="sxs-lookup"><span data-stu-id="49730-117">hello default function template is basically a "hello world" function that echoes back hello name from hello request body or query string parameter, `name=<your name>`.</span></span>  <span data-ttu-id="49730-118">Мы обновим кода hello tooalso позволяют tooprovide hello имя и адрес как содержимое JSON в теле запроса hello.</span><span class="sxs-lookup"><span data-stu-id="49730-118">We'll update hello code tooalso allow you tooprovide hello name and an address as JSON content in hello request body.</span></span> <span data-ttu-id="49730-119">Затем функция hello возвращает эти задней toohello клиента при ее наличии.</span><span class="sxs-lookup"><span data-stu-id="49730-119">Then hello function echoes these back toohello client when available.</span></span>   

<span data-ttu-id="49730-120">Добавьте функции hello hello, следующий код, который мы будет использовать для тестирования:</span><span class="sxs-lookup"><span data-stu-id="49730-120">Update hello function with hello following code, which we will use for testing:</span></span>

```javascript
module.exports = function (context, req) {
    context.log("HTTP trigger function processed a request. RequestUri=%s", req.originalUrl);
    context.log("Request Headers = " + JSON.stringify(req.headers));
    var res;

    if (req.query.name || (req.body && req.body.name)) {
        if (typeof req.query.name != "undefined") {
            context.log("Name was provided as a query string param...");
            res = ProcessNewUserInformation(context, req.query.name);
        }
        else {
            context.log("Processing user info from request body...");
            res = ProcessNewUserInformation(context, req.body.name, req.body.address);
        }
    }
    else {
        res = {
            status: 400,
            body: "Please pass a name on hello query string or in hello request body"
        };
    }
    context.done(null, res);
};
function ProcessNewUserInformation(context, name, address) {
    context.log("Processing user information...");
    context.log("name = " + name);
    var echoString = "Hello " + name;
    var res;

    if (typeof address != "undefined") {
        echoString += "\n" + "hello address you provided is " + address;
        context.log("address = " + address);
    }
    res = {
        // status: 200, /* Defaults too200 */
        body: echoString
    };
    return res;
}
```

## <a name="test-a-function-with-tools"></a><span data-ttu-id="49730-121">Тестирование функции с помощью инструментов</span><span class="sxs-lookup"><span data-stu-id="49730-121">Test a function with tools</span></span>
<span data-ttu-id="49730-122">За пределами hello портал Azure существуют различные инструменты, можно использовать tootrigger функций для тестирования.</span><span class="sxs-lookup"><span data-stu-id="49730-122">Outside hello Azure portal, there are various tools that you can use tootrigger your functions for testing.</span></span> <span data-ttu-id="49730-123">К ним относятся инструменты тестирования HTTP на основе пользовательского интерфейса или командной строки, средства доступа к службе хранилища Azure и даже простой веб-браузер.</span><span class="sxs-lookup"><span data-stu-id="49730-123">These include HTTP testing tools (both UI-based and command line), Azure Storage access tools, and even a simple web browser.</span></span>

### <a name="test-with-a-browser"></a><span data-ttu-id="49730-124">Тестирование с помощью браузера</span><span class="sxs-lookup"><span data-stu-id="49730-124">Test with a browser</span></span>
<span data-ttu-id="49730-125">веб-обозреватель Hello — функций tootrigger простым способом через HTTP.</span><span class="sxs-lookup"><span data-stu-id="49730-125">hello web browser is a simple way tootrigger functions via HTTP.</span></span> <span data-ttu-id="49730-126">Браузер можно использовать для запросов GET, в которых не требуются полезные данные текста, а применяются только параметры строки запроса.</span><span class="sxs-lookup"><span data-stu-id="49730-126">You can use a browser for GET requests that do not require a body payload, and that use only query string parameters.</span></span>

<span data-ttu-id="49730-127">было определено ранее, hello копирования функции hello tootest **URL-адрес функции** из портала hello.</span><span class="sxs-lookup"><span data-stu-id="49730-127">tootest hello function we defined earlier, copy hello **Function Url** from hello portal.</span></span> <span data-ttu-id="49730-128">Он имеет hello следующие формы:</span><span class="sxs-lookup"><span data-stu-id="49730-128">It has hello following form:</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="49730-129">Добавление hello `name` параметр строки запроса toohello.</span><span class="sxs-lookup"><span data-stu-id="49730-129">Append hello `name` parameter toohello query string.</span></span> <span data-ttu-id="49730-130">Использовать фактическое имя для hello `<Enter a name here>` заполнителя.</span><span class="sxs-lookup"><span data-stu-id="49730-130">Use an actual name for hello `<Enter a name here>` placeholder.</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>&name=<Enter a name here>

<span data-ttu-id="49730-131">URL-адрес hello вставить в браузере и должны получить ответ аналогичные toohello следующее.</span><span class="sxs-lookup"><span data-stu-id="49730-131">Paste hello URL into your browser, and you should get a response similar toohello following.</span></span>

![Снимок экрана: вкладка браузера Chrome с ответом теста](./media/functions-test-a-function/browser-test.png)

<span data-ttu-id="49730-133">Данный пример является браузера Chrome hello, который создает оболочку для hello вернул строку в формате XML.</span><span class="sxs-lookup"><span data-stu-id="49730-133">This example is hello Chrome browser, which wraps hello returned string in XML.</span></span> <span data-ttu-id="49730-134">Другие обозреватели отображают только hello строковое значение.</span><span class="sxs-lookup"><span data-stu-id="49730-134">Other browsers display just hello string value.</span></span>

<span data-ttu-id="49730-135">На портале hello **журналы** вывода окна, аналогичные toohello ниже регистрируется при выполнении функции hello:</span><span class="sxs-lookup"><span data-stu-id="49730-135">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-03-23T07:34:59  Welcome, you are now connected toolog-streaming service.
    2016-03-23T07:35:09.195 Function started (Id=61a8c5a9-5e44-4da0-909d-91d293f20445)
    2016-03-23T07:35:10.338 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==&name=Glenn from a browser
    2016-03-23T07:35:10.338 Request Headers = {"cache-control":"max-age=0","connection":"Keep-Alive","accept":"text/html","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T07:35:10.338 Name was provided as a query string param.
    2016-03-23T07:35:10.338 Processing User Information...
    2016-03-23T07:35:10.369 Function completed (Success, Id=61a8c5a9-5e44-4da0-909d-91d293f20445)

### <a name="test-with-postman"></a><span data-ttu-id="49730-136">Тестирование с помощью приложения Postman</span><span class="sxs-lookup"><span data-stu-id="49730-136">Test with Postman</span></span>
<span data-ttu-id="49730-137">Рекомендуется использовать средство tootest Hello большинство функций — почтальон, который интегрируется с браузера Chrome hello.</span><span class="sxs-lookup"><span data-stu-id="49730-137">hello recommended tool tootest most of your functions is Postman, which integrates with hello Chrome browser.</span></span> <span data-ttu-id="49730-138">в разделе tooinstall почтальон, [получить почтальон](https://www.getpostman.com/).</span><span class="sxs-lookup"><span data-stu-id="49730-138">tooinstall Postman, see [Get Postman](https://www.getpostman.com/).</span></span> <span data-ttu-id="49730-139">Приложение Postman позволяет контролировать намного больше атрибутов HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="49730-139">Postman provides control over many more attributes of an HTTP request.</span></span>

> [!TIP]
> <span data-ttu-id="49730-140">Средство hello HTTP тестирования, наиболее вы знакомы с.</span><span class="sxs-lookup"><span data-stu-id="49730-140">Use hello HTTP testing tool that you are most comfortable with.</span></span> <span data-ttu-id="49730-141">Ниже приведены некоторые tooPostman альтернативных вариантов.</span><span class="sxs-lookup"><span data-stu-id="49730-141">Here are some alternatives tooPostman:</span></span>  
>
> * [<span data-ttu-id="49730-142">Fiddler</span><span class="sxs-lookup"><span data-stu-id="49730-142">Fiddler</span></span>](http://www.telerik.com/fiddler)  
> * [<span data-ttu-id="49730-143">Paw.</span><span class="sxs-lookup"><span data-stu-id="49730-143">Paw</span></span>](https://luckymarmot.com/paw)  
>
>

<span data-ttu-id="49730-144">функция hello tootest с текстом запроса в почтальон:</span><span class="sxs-lookup"><span data-stu-id="49730-144">tootest hello function with a request body in Postman:</span></span>

1. <span data-ttu-id="49730-145">Запуск из hello почтальон **приложений** кнопку в hello верхнего левого угла окна браузера Chrome.</span><span class="sxs-lookup"><span data-stu-id="49730-145">Start Postman from hello **Apps** button in hello upper-left corner of a Chrome browser window.</span></span>
2. <span data-ttu-id="49730-146">Скопируйте **URL-адрес функции** и вставьте его в Postman.</span><span class="sxs-lookup"><span data-stu-id="49730-146">Copy your **Function Url**, and paste it into Postman.</span></span> <span data-ttu-id="49730-147">Он включает параметр строки запроса доступа к коду hello.</span><span class="sxs-lookup"><span data-stu-id="49730-147">It includes hello access code query string parameter.</span></span>
3. <span data-ttu-id="49730-148">Изменение метода hello HTTP слишком**POST**.</span><span class="sxs-lookup"><span data-stu-id="49730-148">Change hello HTTP method too**POST**.</span></span>
4. <span data-ttu-id="49730-149">Нажмите кнопку **текст** > **необработанные**и добавьте аналогичные toohello следующий текст запроса JSON:</span><span class="sxs-lookup"><span data-stu-id="49730-149">Click **Body** > **raw**, and add a JSON request body similar toohello following:</span></span>

    ```json
    {
        "name" : "Wes testing with Postman",
        "address" : "Seattle, WA 98101"
    }
    ```
5. <span data-ttu-id="49730-150">Нажмите кнопку **Send**(Отправить).</span><span class="sxs-lookup"><span data-stu-id="49730-150">Click **Send**.</span></span>

<span data-ttu-id="49730-151">Hello ниже приведен пример функции простые эхо тестирования hello в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="49730-151">hello following image shows testing hello simple echo function example in this tutorial.</span></span>

![Снимок экрана: пользовательский интерфейс Postman](./media/functions-test-a-function/postman-test.png)

<span data-ttu-id="49730-153">На портале hello **журналы** вывода окна, аналогичные toohello ниже регистрируется при выполнении функции hello:</span><span class="sxs-lookup"><span data-stu-id="49730-153">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-03-23T08:04:51  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:04:57.107 Function started (Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)
    2016-03-23T08:04:57.763 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==
    2016-03-23T08:04:57.763 Request Headers = {"cache-control":"no-cache","connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:04:57.763 Processing user info from request body...
    2016-03-23T08:04:57.763 Processing User Information...
    2016-03-23T08:04:57.763 name = Wes testing with Postman
    2016-03-23T08:04:57.763 address = Seattle, W.A. 98101
    2016-03-23T08:04:57.795 Function completed (Success, Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)

### <a name="test-with-curl-from-hello-command-line"></a><span data-ttu-id="49730-154">Тестирование с помощью перелистывание из командной строки hello</span><span class="sxs-lookup"><span data-stu-id="49730-154">Test with cURL from hello command line</span></span>
<span data-ttu-id="49730-155">Часто при тестировании программного обеспечения не необходимые toolook любое дальнейшей, чем hello командной строки toohelp отладки приложения.</span><span class="sxs-lookup"><span data-stu-id="49730-155">Often when you're testing software, it's not necessary toolook any further than hello command line toohelp debug your application.</span></span> <span data-ttu-id="49730-156">То же самое справедливо и для функций.</span><span class="sxs-lookup"><span data-stu-id="49730-156">This is no different with testing functions.</span></span> <span data-ttu-id="49730-157">Обратите внимание, что перелистывание hello доступность по умолчанию в системах под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="49730-157">Note that hello cURL is available by default on Linux-based systems.</span></span> <span data-ttu-id="49730-158">В Windows, необходимо сначала загрузить и установить hello [перелистывание средство](https://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="49730-158">On Windows, you must first download and install hello [cURL tool](https://curl.haxx.se/).</span></span>

<span data-ttu-id="49730-159">функция tootest hello, что было определено ранее, hello копирования **URL-адрес функции** из портала hello.</span><span class="sxs-lookup"><span data-stu-id="49730-159">tootest hello function that we defined earlier, copy hello **Function URL** from hello portal.</span></span> <span data-ttu-id="49730-160">Он имеет hello следующие формы:</span><span class="sxs-lookup"><span data-stu-id="49730-160">It has hello following form:</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="49730-161">Это hello URL-адрес для запуска функции.</span><span class="sxs-lookup"><span data-stu-id="49730-161">This is hello URL for triggering your function.</span></span> <span data-ttu-id="49730-162">Проверить это с помощью команды перелистывание hello в командной строке toomake hello GET (`-G` или `--get`) запрос к функции hello:</span><span class="sxs-lookup"><span data-stu-id="49730-162">Test this by using hello cURL command on hello command line toomake a GET (`-G` or `--get`) request against hello function:</span></span>

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="49730-163">Для этого конкретного примера требуются параметр строки запроса, которую можно передать в качестве данных (`-d`) в hello cURL команды:</span><span class="sxs-lookup"><span data-stu-id="49730-163">This particular example requires a query string parameter, which can be passed as Data (`-d`) in hello cURL command:</span></span>

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code> -d name=<Enter a name here>

<span data-ttu-id="49730-164">Команда выполнения hello, отобразится hello следующие выходные данные функции hello в командной строке hello:</span><span class="sxs-lookup"><span data-stu-id="49730-164">Run hello command, and you see hello following output of hello function on hello command line:</span></span>

![Снимок экрана: выходные данные в командной строке](./media/functions-test-a-function/curl-test.png)

<span data-ttu-id="49730-166">На портале hello **журналы** вывода окна, аналогичные toohello ниже регистрируется при выполнении функции hello:</span><span class="sxs-lookup"><span data-stu-id="49730-166">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-04-05T21:55:09  Welcome, you are now connected toolog-streaming service.
    2016-04-05T21:55:30.738 Function started (Id=ae6955da-29db-401a-b706-482fcd1b8f7a)
    2016-04-05T21:55:30.738 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/HttpTriggerNodeJS1?code=XXXXXXX&name=Azure Functions
    2016-04-05T21:55:30.738 Function completed (Success, Id=ae6955da-29db-401a-b706-482fcd1b8f7a)

### <a name="test-a-blob-trigger-by-using-storage-explorer"></a><span data-ttu-id="49730-167">Тестирование триггера больших двоичных объектов с помощью Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="49730-167">Test a blob trigger by using Storage Explorer</span></span>
<span data-ttu-id="49730-168">Функцию триггера больших двоичных объектов можно протестировать с помощью [Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="49730-168">You can test a blob trigger function by using [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

1. <span data-ttu-id="49730-169">В hello [портал Azure] функции приложения, создайте функцию триггер больших двоичных объектов C#, F # и JavaScript.</span><span class="sxs-lookup"><span data-stu-id="49730-169">In hello [Azure portal] for your function app, create a C#, F# or JavaScript blob trigger function.</span></span> <span data-ttu-id="49730-170">Задать hello toomonitor toohello путь контейнера больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="49730-170">Set hello path toomonitor toohello name of your blob container.</span></span> <span data-ttu-id="49730-171">Например:</span><span class="sxs-lookup"><span data-stu-id="49730-171">For example:</span></span>

        files
2. <span data-ttu-id="49730-172">Нажмите кнопку hello  **+**  кнопку tooselect или создать учетную запись хранения hello требуется toouse.</span><span class="sxs-lookup"><span data-stu-id="49730-172">Click hello **+** button tooselect or create hello storage account you want toouse.</span></span> <span data-ttu-id="49730-173">Затем щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="49730-173">Then click **Create**.</span></span>
3. <span data-ttu-id="49730-174">Создайте текстовый файл с после текста hello и сохраните его:</span><span class="sxs-lookup"><span data-stu-id="49730-174">Create a text file with hello following text, and save it:</span></span>

        A text file for blob trigger function testing.
4. <span data-ttu-id="49730-175">Запустите [обозреватель хранилищ Azure](http://storageexplorer.com/)и соедините контейнер больших двоичных объектов toohello в учетной записи хранения hello отслеживается.</span><span class="sxs-lookup"><span data-stu-id="49730-175">Run [Azure Storage Explorer](http://storageexplorer.com/), and connect toohello blob container in hello storage account being monitored.</span></span>
5. <span data-ttu-id="49730-176">Нажмите кнопку **отправить** tooupload hello текстовый файл.</span><span class="sxs-lookup"><span data-stu-id="49730-176">Click **Upload** tooupload hello text file.</span></span>

    ![Снимок экрана: Storage Explorer](./media/functions-test-a-function/azure-storage-explorer-test.png)

<span data-ttu-id="49730-178">Код функции триггера больших двоичных объектов по умолчанию Hello сообщает обработки hello hello большого двоичного объекта в журналы hello:</span><span class="sxs-lookup"><span data-stu-id="49730-178">hello default blob trigger function code reports hello processing of hello blob in hello logs:</span></span>

    2016-03-24T11:30:10  Welcome, you are now connected toolog-streaming service.
    2016-03-24T11:30:34.472 Function started (Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)
    2016-03-24T11:30:34.472 C# Blob trigger function processed: A text file for blob trigger function testing.
    2016-03-24T11:30:34.472 Function completed (Success, Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)

## <a name="test-a-function-within-functions"></a><span data-ttu-id="49730-179">Тестирование функции в рамках функций</span><span class="sxs-lookup"><span data-stu-id="49730-179">Test a function within functions</span></span>
<span data-ttu-id="49730-180">Hello Azure функции портал предназначен toolet проверки HTTP и таймер запускается функции.</span><span class="sxs-lookup"><span data-stu-id="49730-180">hello Azure Functions portal is designed toolet you test HTTP and timer triggered functions.</span></span> <span data-ttu-id="49730-181">Можно также создать tootrigger функции других функций, которые вы тестируете.</span><span class="sxs-lookup"><span data-stu-id="49730-181">You can also create functions tootrigger other functions that you are testing.</span></span>

### <a name="test-with-hello-functions-portal-run-button"></a><span data-ttu-id="49730-182">Тестирование с помощью портала кнопку запуска hello функции</span><span class="sxs-lookup"><span data-stu-id="49730-182">Test with hello Functions portal Run button</span></span>
<span data-ttu-id="49730-183">Предоставляет портал Hello **запуска** кнопки, которые можно использовать некоторые toodo ограниченный тестирования.</span><span class="sxs-lookup"><span data-stu-id="49730-183">hello portal provides a **Run** button that you can use toodo some limited testing.</span></span> <span data-ttu-id="49730-184">Текст запроса можно предоставить с помощью кнопки hello, но не может предоставить параметры строки запроса или обновления заголовков запроса.</span><span class="sxs-lookup"><span data-stu-id="49730-184">You can provide a request body by using hello button, but you can't provide query string parameters or update request headers.</span></span>

<span data-ttu-id="49730-185">Проверить функцию триггер hello HTTP, созданную ранее, добавив в hello JSON строка аналогичные toohello после **текст запроса** поля.</span><span class="sxs-lookup"><span data-stu-id="49730-185">Test hello HTTP trigger function we created earlier by adding a JSON string similar toohello following in hello **Request body** field.</span></span> <span data-ttu-id="49730-186">Нажмите кнопку hello **запуска** кнопки.</span><span class="sxs-lookup"><span data-stu-id="49730-186">Then click hello **Run** button.</span></span>

```json
{
    "name" : "Wes testing Run button",
    "address" : "USA"
}
```

<span data-ttu-id="49730-187">На портале hello **журналы** вывода окна, аналогичные toohello ниже регистрируется при выполнении функции hello:</span><span class="sxs-lookup"><span data-stu-id="49730-187">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-03-23T08:03:12  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:03:17.357 Function started (Id=753a01b0-45a8-4125-a030-3ad543a89409)
    2016-03-23T08:03:18.697 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/wesmchttptriggernodejs1
    2016-03-23T08:03:18.697 Request Headers = {"connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:03:18.697 Processing user info from request body...
    2016-03-23T08:03:18.697 Processing User Information...
    2016-03-23T08:03:18.697 name = Wes testing Run button
    2016-03-23T08:03:18.697 address = USA
    2016-03-23T08:03:18.744 Function completed (Success, Id=753a01b0-45a8-4125-a030-3ad543a89409)


### <a name="test-with-a-timer-trigger"></a><span data-ttu-id="49730-188">Тестирование с помощью триггера таймера</span><span class="sxs-lookup"><span data-stu-id="49730-188">Test with a timer trigger</span></span>
<span data-ttu-id="49730-189">Некоторые функции не удается проверить адекватно с упомянутых ранее средств hello.</span><span class="sxs-lookup"><span data-stu-id="49730-189">Some functions can't be adequately tested with hello tools mentioned previously.</span></span> <span data-ttu-id="49730-190">Например, функцию триггера очереди, которая выполняется при поступлении сообщения в [хранилище очередей Azure](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="49730-190">For example, consider a queue trigger function that runs when a message is dropped into [Azure Queue storage](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span> <span data-ttu-id="49730-191">Можно всегда написать код toodrop сообщения в очереди, и соответствующий пример приведен в проект консольного приложения предоставляется далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="49730-191">You can always write code toodrop a message into your queue, and an example of this in a console project is provided later in this article.</span></span> <span data-ttu-id="49730-192">Однако существует другой подход, который можно использовать для непосредственного тестирования функций.</span><span class="sxs-lookup"><span data-stu-id="49730-192">However, there is another approach you can use that tests functions directly.</span></span>  

<span data-ttu-id="49730-193">Можно использовать триггер таймера, настроенный с привязкой для вывода очереди.</span><span class="sxs-lookup"><span data-stu-id="49730-193">You can use a timer trigger configured with a queue output binding.</span></span> <span data-ttu-id="49730-194">Этот код триггера таймера можно написать тест сообщений hello toohello в очереди.</span><span class="sxs-lookup"><span data-stu-id="49730-194">That timer trigger code can then write hello test messages toohello queue.</span></span> <span data-ttu-id="49730-195">В этом разделе описан пример.</span><span class="sxs-lookup"><span data-stu-id="49730-195">This section walks through an example.</span></span>

<span data-ttu-id="49730-196">Дополнительные сведения об использовании привязок с помощью функций Azure, в разделе hello [Справочник разработчика Azure функции](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="49730-196">For more in-depth information on using bindings with Azure Functions, see hello [Azure Functions developer reference](functions-reference.md).</span></span>

#### <a name="create-a-queue-trigger-for-testing"></a><span data-ttu-id="49730-197">Создание триггера очереди для тестирования</span><span class="sxs-lookup"><span data-stu-id="49730-197">Create a queue trigger for testing</span></span>
<span data-ttu-id="49730-198">toodemonstrate этого подхода сначала создается функция очереди триггера, мы хотим tootest для очереди с именем `queue-newusers`.</span><span class="sxs-lookup"><span data-stu-id="49730-198">toodemonstrate this approach, we first create a queue trigger function that we want tootest for a queue named `queue-newusers`.</span></span> <span data-ttu-id="49730-199">Эта функция обрабатывает имя и адрес нового пользователя, поступившие в хранилище очередей.</span><span class="sxs-lookup"><span data-stu-id="49730-199">This function processes name and address information dropped into Queue storage for a new user.</span></span>

> [!NOTE]
> <span data-ttu-id="49730-200">При использовании имени другую очередь, убедитесь, что используется имя hello соответствует toohello [именование очередей и метаданные](https://msdn.microsoft.com/library/dd179349.aspx) правила.</span><span class="sxs-lookup"><span data-stu-id="49730-200">If you use a different queue name, make sure hello name you use conforms toohello [Naming Queues and MetaData](https://msdn.microsoft.com/library/dd179349.aspx) rules.</span></span> <span data-ttu-id="49730-201">В противном случае возникает ошибка.</span><span class="sxs-lookup"><span data-stu-id="49730-201">Otherwise, you get an error.</span></span>
>
>

1. <span data-ttu-id="49730-202">В hello [портал Azure] функции приложения, щелкните **новая функция** > **QueueTrigger - C#**.</span><span class="sxs-lookup"><span data-stu-id="49730-202">In hello [Azure portal] for your function app, click **New Function** > **QueueTrigger - C#**.</span></span>
2. <span data-ttu-id="49730-203">Введите имя toobe hello очереди, отслеживаемый с помощью функции hello очереди:</span><span class="sxs-lookup"><span data-stu-id="49730-203">Enter hello queue name toobe monitored by hello queue function:</span></span>

        queue-newusers
3. <span data-ttu-id="49730-204">Нажмите кнопку hello  **+**  кнопку tooselect или создать учетную запись хранения hello требуется toouse.</span><span class="sxs-lookup"><span data-stu-id="49730-204">Click hello **+** button tooselect or create hello storage account you want toouse.</span></span> <span data-ttu-id="49730-205">Затем щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="49730-205">Then click **Create**.</span></span>
4. <span data-ttu-id="49730-206">Не закрывайте это окно браузера портала, можно наблюдать за hello записи в журнале для hello очереди функции шаблона по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="49730-206">Leave this portal browser window open, so you can monitor hello log entries for hello default queue function template code.</span></span>

#### <a name="create-a-timer-trigger-toodrop-a-message-in-hello-queue"></a><span data-ttu-id="49730-207">Создайте триггер таймера toodrop сообщение в очередь hello</span><span class="sxs-lookup"><span data-stu-id="49730-207">Create a timer trigger toodrop a message in hello queue</span></span>
1. <span data-ttu-id="49730-208">Откройте hello [портал Azure] в новом окне браузера и перейдите tooyour функции приложения.</span><span class="sxs-lookup"><span data-stu-id="49730-208">Open hello [Azure portal] in a new browser window, and navigate tooyour function app.</span></span>
2. <span data-ttu-id="49730-209">Щелкните **Новая функция** > **TimerTrigger — C#**.</span><span class="sxs-lookup"><span data-stu-id="49730-209">Click **New Function** > **TimerTrigger - C#**.</span></span> <span data-ttu-id="49730-210">Введите выражение cron tooset частоту hello таймера код проверяет работу очереди.</span><span class="sxs-lookup"><span data-stu-id="49730-210">Enter a cron expression tooset how often hello timer code tests your queue function.</span></span> <span data-ttu-id="49730-211">Затем щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="49730-211">Then click **Create**.</span></span> <span data-ttu-id="49730-212">Если требуется toorun теста hello каждые 30 секунд, можно использовать hello следующие [выражение CRON](https://wikipedia.org/wiki/Cron#CRON_expression):</span><span class="sxs-lookup"><span data-stu-id="49730-212">If you want hello test toorun every 30 seconds, you can use hello following [CRON expression](https://wikipedia.org/wiki/Cron#CRON_expression):</span></span>

        */30 * * * * *
3. <span data-ttu-id="49730-213">Нажмите кнопку hello **Интеграция** вкладка нового таймера триггера.</span><span class="sxs-lookup"><span data-stu-id="49730-213">Click hello **Integrate** tab for your new timer trigger.</span></span>
4. <span data-ttu-id="49730-214">В разделе **Выходные данные** щелкните **+ Новое выходное значение**.</span><span class="sxs-lookup"><span data-stu-id="49730-214">Under **Output**, click **+ New Output**.</span></span> <span data-ttu-id="49730-215">Затем последовательно щелкните **Очередь** и **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="49730-215">Then click **queue** and **Select**.</span></span>
5. <span data-ttu-id="49730-216">Имя заметки hello, используйте для hello **объект очереди сообщений**.</span><span class="sxs-lookup"><span data-stu-id="49730-216">Note hello name you use for hello **queue message object**.</span></span> <span data-ttu-id="49730-217">Можно использовать в коде функции hello таймера.</span><span class="sxs-lookup"><span data-stu-id="49730-217">You use this in hello timer function code.</span></span>

        myQueue
6. <span data-ttu-id="49730-218">Введите имя очереди hello, куда отправлять сообщение hello:</span><span class="sxs-lookup"><span data-stu-id="49730-218">Enter hello queue name where hello message is sent:</span></span>

        queue-newusers
7. <span data-ttu-id="49730-219">Нажмите кнопку hello  **+**  кнопку tooselect учетной записи хранилища hello ранее используется с триггером очереди hello.</span><span class="sxs-lookup"><span data-stu-id="49730-219">Click hello **+** button tooselect hello storage account you used previously with hello queue trigger.</span></span> <span data-ttu-id="49730-220">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="49730-220">Then click **Save**.</span></span>
8. <span data-ttu-id="49730-221">Нажмите кнопку hello **разработка** вкладку, триггер таймера.</span><span class="sxs-lookup"><span data-stu-id="49730-221">Click hello **Develop** tab for your timer trigger.</span></span>
9. <span data-ttu-id="49730-222">Привет, следующий код для функции таймера hello C#, можно использовать при условии, что вы использовали hello же очереди сообщений имя объекта, показанного выше.</span><span class="sxs-lookup"><span data-stu-id="49730-222">You can use hello following code for hello C# timer function, as long as you used hello same queue message object name shown earlier.</span></span> <span data-ttu-id="49730-223">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="49730-223">Then click **Save**.</span></span>

    ```cs
    using System;

    public static void Run(TimerInfo myTimer, out String myQueue, TraceWriter log)
    {
        String newUser =
        "{\"name\":\"User testing from C# timer function\",\"address\":\"XYZ\"}";

        log.Verbose($"C# Timer trigger function executed at: {DateTime.Now}");   
        log.Verbose($"{newUser}");   

        myQueue = newUser;
    }
    ```

<span data-ttu-id="49730-224">На этом этапе hello таймера функции C# выполняется каждые 30 секунд, если используется выражение cron hello.</span><span class="sxs-lookup"><span data-stu-id="49730-224">At this point, hello C# timer function executes every 30 seconds if you used hello example cron expression.</span></span> <span data-ttu-id="49730-225">Каждый выполнение отчета Hello журналы для функции hello таймера:</span><span class="sxs-lookup"><span data-stu-id="49730-225">hello logs for hello timer function report each execution:</span></span>

    2016-03-24T10:27:02  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.004 Function started (Id=04061790-974f-4043-b851-48bd4ac424d1)
    2016-03-24T10:27:30.004 C# Timer trigger function executed at: 3/24/2016 10:27:30 AM
    2016-03-24T10:27:30.004 {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.004 Function completed (Success, Id=04061790-974f-4043-b851-48bd4ac424d1)

<span data-ttu-id="49730-226">В окне браузера hello для функции hello очереди можно увидеть каждого обрабатываемого сообщения:</span><span class="sxs-lookup"><span data-stu-id="49730-226">In hello browser window for hello queue function, you can see each message being processed:</span></span>

    2016-03-24T10:27:06  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)

## <a name="test-a-function-with-code"></a><span data-ttu-id="49730-227">Тестирование функции с помощью кода</span><span class="sxs-lookup"><span data-stu-id="49730-227">Test a function with code</span></span>
<span data-ttu-id="49730-228">Может потребоваться toocreate внешних tootest приложение или платформу функций.</span><span class="sxs-lookup"><span data-stu-id="49730-228">You may need toocreate an external application or framework tootest your functions.</span></span>

### <a name="test-an-http-trigger-function-with-code-nodejs"></a><span data-ttu-id="49730-229">Тестирование функции HTTP-триггера с помощью кода: Node.js</span><span class="sxs-lookup"><span data-stu-id="49730-229">Test an HTTP trigger function with code: Node.js</span></span>
<span data-ttu-id="49730-230">Можно использовать функции tooexecute приложение Node.js tootest запроса HTTP.</span><span class="sxs-lookup"><span data-stu-id="49730-230">You can use a Node.js app tooexecute an HTTP request tootest your function.</span></span>
<span data-ttu-id="49730-231">Убедитесь, что tooset:</span><span class="sxs-lookup"><span data-stu-id="49730-231">Make sure tooset:</span></span>

* <span data-ttu-id="49730-232">Hello `host` в узел приложения tooyour функции hello запроса параметров.</span><span class="sxs-lookup"><span data-stu-id="49730-232">hello `host` in hello request options tooyour function app host.</span></span>
* <span data-ttu-id="49730-233">Имя функции в hello `path`.</span><span class="sxs-lookup"><span data-stu-id="49730-233">Your function name in hello `path`.</span></span>
* <span data-ttu-id="49730-234">Код доступа (`<your code>`) в hello `path`.</span><span class="sxs-lookup"><span data-stu-id="49730-234">Your access code (`<your code>`) in hello `path`.</span></span>

<span data-ttu-id="49730-235">Пример кода:</span><span class="sxs-lookup"><span data-stu-id="49730-235">Code example:</span></span>

```javascript
var http = require("http");

var nameQueryString = "name=Wes%20Query%20String%20Test%20From%20Node.js";

var nameBodyJSON = {
    name : "Wes testing with Node.JS code",
    address : "Dallas, T.X. 75201"
};

var bodyString = JSON.stringify(nameBodyJSON);

var options = {
  host: "functions841def78.azurewebsites.net",
  //path: "/api/HttpTriggerNodeJS2?code=sc1wt62opn7k9buhrm8jpds4ikxvvj42m5ojdt0p91lz5jnhfr2c74ipoujyq26wab3wk5gkfbt9&" + nameQueryString,
  path: "/api/HttpTriggerNodeJS2?code=sc1wt62opn7k9buhrm8jpds4ikxvvj42m5ojdt0p91lz5jnhfr2c74ipoujyq26wab3wk5gkfbt9",
  method: "POST",
  headers : {
      "Content-Type":"application/json",
      "Content-Length": Buffer.byteLength(bodyString)
    }    
};

callback = function(response) {
  var str = ""
  response.on("data", function (chunk) {
    str += chunk;
  });

  response.on("end", function () {
    console.log(str);
  });
}

var req = http.request(options, callback);
console.log("*** Sending name and address in body ***");
console.log(bodyString);
req.end(bodyString);
```


<span data-ttu-id="49730-236">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="49730-236">Output:</span></span>

    C:\Users\Wesley\testing\Node.js>node testHttpTriggerExample.js
    *** Sending name and address in body ***
    {"name" : "Wes testing with Node.JS code","address" : "Dallas, T.X. 75201"}
    Hello Wes testing with Node.JS code
    hello address you provided is Dallas, T.X. 75201

<span data-ttu-id="49730-237">На портале hello **журналы** вывода окна, аналогичные toohello ниже регистрируется при выполнении функции hello:</span><span class="sxs-lookup"><span data-stu-id="49730-237">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-03-23T08:08:55  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:08:59.736 Function started (Id=607b891c-08a1-427f-910c-af64ae4f7f9c)
    2016-03-23T08:09:01.153 HTTP trigger function processed a request. RequestUri=http://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1/?code=XXXXXXXXXX==
    2016-03-23T08:09:01.153 Request Headers = {"connection":"Keep-Alive","host":"functionsExample.azurewebsites.net"}
    2016-03-23T08:09:01.153 Name not provided as query string param. Checking body...
    2016-03-23T08:09:01.153 Request Body Type = object
    2016-03-23T08:09:01.153 Request Body = [object Object]
    2016-03-23T08:09:01.153 Processing User Information...
    2016-03-23T08:09:01.215 Function completed (Success, Id=607b891c-08a1-427f-910c-af64ae4f7f9c)


### <a name="test-a-queue-trigger-function-with-code-c"></a><span data-ttu-id="49730-238">Тестирование функции триггера очереди с помощью кода: C#</span><span class="sxs-lookup"><span data-stu-id="49730-238">Test a queue trigger function with code: C#</span></span> #
<span data-ttu-id="49730-239">Упоминалось ранее, можно выполнить проверку очереди триггера с помощью кода toodrop сообщения в очереди.</span><span class="sxs-lookup"><span data-stu-id="49730-239">We mentioned earlier that you can test a queue trigger by using code toodrop a message in your queue.</span></span> <span data-ttu-id="49730-240">Привет, следующий пример кода основан на hello C# кода, представленного в hello [Приступая к работе с хранилищем очередей Azure](../storage/queues/storage-dotnet-how-to-use-queues.md) учебника.</span><span class="sxs-lookup"><span data-stu-id="49730-240">hello following example code is based on hello C# code presented in hello [Getting started with Azure Queue storage](../storage/queues/storage-dotnet-how-to-use-queues.md) tutorial.</span></span> <span data-ttu-id="49730-241">По этой ссылке также доступен код для других языков.</span><span class="sxs-lookup"><span data-stu-id="49730-241">Code for other languages is also available from that link.</span></span>

<span data-ttu-id="49730-242">tootest этот код в консольном приложении, необходимо:</span><span class="sxs-lookup"><span data-stu-id="49730-242">tootest this code in a console app, you must:</span></span>

* <span data-ttu-id="49730-243">[Настройка строки подключения хранилища в файле app.config hello](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="49730-243">[Configure your storage connection string in hello app.config file](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>
* <span data-ttu-id="49730-244">Передайте `name` и `address` как приложение toohello параметров.</span><span class="sxs-lookup"><span data-stu-id="49730-244">Pass a `name` and `address` as parameters toohello app.</span></span> <span data-ttu-id="49730-245">Например, `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`.</span><span class="sxs-lookup"><span data-stu-id="49730-245">For example, `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`.</span></span> <span data-ttu-id="49730-246">(Этот код hello имя и адрес для нового пользователя в качестве принимает аргументы командной строки во время выполнения.)</span><span class="sxs-lookup"><span data-stu-id="49730-246">(This code accepts hello name and address for a new user as command-line arguments during runtime.)</span></span>

<span data-ttu-id="49730-247">Пример кода C#:</span><span class="sxs-lookup"><span data-stu-id="49730-247">Example C# code:</span></span>

```cs
static void Main(string[] args)
{
    string name = null;
    string address = null;
    string queueName = "queue-newusers";
    string JSON = null;

    if (args.Length > 0)
    {
        name = args[0];
    }
    if (args.Length > 1)
    {
        address = args[1];
    }

    // Retrieve storage account from connection string
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConfigurationManager.AppSettings["StorageConnectionString"]);

    // Create hello queue client
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

    // Retrieve a reference tooa queue
    CloudQueue queue = queueClient.GetQueueReference(queueName);

    // Create hello queue if it doesn't already exist
    queue.CreateIfNotExists();

    // Create a message and add it toohello queue.
    if (name != null)
    {
        if (address != null)
            JSON = String.Format("{{\"name\":\"{0}\",\"address\":\"{1}\"}}", name, address);
        else
            JSON = String.Format("{{\"name\":\"{0}\"}}", name);
    }

    Console.WriteLine("Adding message too" + queueName + "...");
    Console.WriteLine(JSON);

    CloudQueueMessage message = new CloudQueueMessage(JSON);
    queue.AddMessage(message);
}
```

<span data-ttu-id="49730-248">В окне браузера hello для функции hello очереди можно увидеть каждого обрабатываемого сообщения:</span><span class="sxs-lookup"><span data-stu-id="49730-248">In hello browser window for hello queue function, you can see each message being processed:</span></span>

    2016-03-24T10:27:06  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"Wes testing queues","address":"in a console app"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)


<!-- URLs. -->

[портал Azure]: https://portal.azure.com
