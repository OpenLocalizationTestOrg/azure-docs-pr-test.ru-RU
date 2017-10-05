---
title: "Тестирование Функций Azure | Документация Майкрософт"
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
ms.openlocfilehash: aca03ba4137893157fcbe6650336782ab88cd234
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="strategies-for-testing-your-code-in-azure-functions"></a><span data-ttu-id="ebc45-104">Методика тестирования кода с помощью Функций Azure</span><span class="sxs-lookup"><span data-stu-id="ebc45-104">Strategies for testing your code in Azure Functions</span></span>

<span data-ttu-id="ebc45-105">В этом разделе показаны различные способы тестирования функций, включая следующие общие подходы:</span><span class="sxs-lookup"><span data-stu-id="ebc45-105">This topic demonstrates the various ways to test functions, including using the following general approaches:</span></span>

+ <span data-ttu-id="ebc45-106">инструменты на основе HTTP, например cURL, Postman и даже веб-браузер для веб-триггеров;</span><span class="sxs-lookup"><span data-stu-id="ebc45-106">HTTP-based tools, such as cURL, Postman, and even a web browser for web-based triggers</span></span>
+ <span data-ttu-id="ebc45-107">Azure Storage Explorer для тестирования триггеров на основе службы хранилища Azure;</span><span class="sxs-lookup"><span data-stu-id="ebc45-107">Azure Storage Explorer, to test Azure Storage-based triggers</span></span>
+ <span data-ttu-id="ebc45-108">вкладка тестирования на портале функций Azure;</span><span class="sxs-lookup"><span data-stu-id="ebc45-108">Test tab in the Azure Functions portal</span></span>
+ <span data-ttu-id="ebc45-109">активируемая по таймеру функция;</span><span class="sxs-lookup"><span data-stu-id="ebc45-109">Timer-triggered function</span></span>
+ <span data-ttu-id="ebc45-110">приложение или платформа для тестирования.</span><span class="sxs-lookup"><span data-stu-id="ebc45-110">Testing application or framework</span></span>

<span data-ttu-id="ebc45-111">Все эти методы тестирования используют функцию триггера HTTP, которая принимает входные данные через параметр строки запроса или текст запроса.</span><span class="sxs-lookup"><span data-stu-id="ebc45-111">All these testing methods use an HTTP trigger function that accepts input through either a query string parameter or the request body.</span></span> <span data-ttu-id="ebc45-112">Эта функция создается в первом разделе.</span><span class="sxs-lookup"><span data-stu-id="ebc45-112">You create this function in the first section.</span></span>

## <a name="create-a-function-for-testing"></a><span data-ttu-id="ebc45-113">Создание функции для тестирования</span><span class="sxs-lookup"><span data-stu-id="ebc45-113">Create a function for testing</span></span>
<span data-ttu-id="ebc45-114">В большей части этого руководства мы будем использовать немного измененную версию шаблона функции JavaScript HttpTrigger, который доступен при создании функции.</span><span class="sxs-lookup"><span data-stu-id="ebc45-114">For most of this tutorial, we use a slightly modified version of the HttpTrigger JavaScript function template that is available when you create a function.</span></span> <span data-ttu-id="ebc45-115">Если вам нужна помощь при создании функции, просмотрите этот [учебник](functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="ebc45-115">If you need help creating a function, review this [tutorial](functions-create-first-azure-function.md).</span></span> <span data-ttu-id="ebc45-116">Выберите шаблон **HttpTrigger- JavaScript** при создании тестовой функции на [портале Azure].</span><span class="sxs-lookup"><span data-stu-id="ebc45-116">Choose the **HttpTrigger- JavaScript** template when creating the test function in the [Azure portal].</span></span>

<span data-ttu-id="ebc45-117">Используемый по умолчанию шаблон функции по сути представляет собой функцию hello world, выводящую на экран имя из текста запроса или параметра строки запроса `name=<your name>`.</span><span class="sxs-lookup"><span data-stu-id="ebc45-117">The default function template is basically a "hello world" function that echoes back the name from the request body or query string parameter, `name=<your name>`.</span></span>  <span data-ttu-id="ebc45-118">Мы обновим код, позволив указать имя и адрес в качестве содержимого JSON в тексте запроса.</span><span class="sxs-lookup"><span data-stu-id="ebc45-118">We'll update the code to also allow you to provide the name and an address as JSON content in the request body.</span></span> <span data-ttu-id="ebc45-119">Затем функция выведет эти значения обратно на клиент при его наличии.</span><span class="sxs-lookup"><span data-stu-id="ebc45-119">Then the function echoes these back to the client when available.</span></span>   

<span data-ttu-id="ebc45-120">Добавьте в функцию следующий код, который будет использоваться для тестирования:</span><span class="sxs-lookup"><span data-stu-id="ebc45-120">Update the function with the following code, which we will use for testing:</span></span>

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
            body: "Please pass a name on the query string or in the request body"
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
        echoString += "\n" + "The address you provided is " + address;
        context.log("address = " + address);
    }
    res = {
        // status: 200, /* Defaults to 200 */
        body: echoString
    };
    return res;
}
```

## <a name="test-a-function-with-tools"></a><span data-ttu-id="ebc45-121">Тестирование функции с помощью инструментов</span><span class="sxs-lookup"><span data-stu-id="ebc45-121">Test a function with tools</span></span>
<span data-ttu-id="ebc45-122">За пределами портала Azure существуют различные инструменты, которые можно использовать для активации функций в целях тестирования.</span><span class="sxs-lookup"><span data-stu-id="ebc45-122">Outside the Azure portal, there are various tools that you can use to trigger your functions for testing.</span></span> <span data-ttu-id="ebc45-123">К ним относятся инструменты тестирования HTTP на основе пользовательского интерфейса или командной строки, средства доступа к службе хранилища Azure и даже простой веб-браузер.</span><span class="sxs-lookup"><span data-stu-id="ebc45-123">These include HTTP testing tools (both UI-based and command line), Azure Storage access tools, and even a simple web browser.</span></span>

### <a name="test-with-a-browser"></a><span data-ttu-id="ebc45-124">Тестирование с помощью браузера</span><span class="sxs-lookup"><span data-stu-id="ebc45-124">Test with a browser</span></span>
<span data-ttu-id="ebc45-125">Веб-браузер — это простой способ активации функций с помощью протокола HTTP.</span><span class="sxs-lookup"><span data-stu-id="ebc45-125">The web browser is a simple way to trigger functions via HTTP.</span></span> <span data-ttu-id="ebc45-126">Браузер можно использовать для запросов GET, в которых не требуются полезные данные текста, а применяются только параметры строки запроса.</span><span class="sxs-lookup"><span data-stu-id="ebc45-126">You can use a browser for GET requests that do not require a body payload, and that use only query string parameters.</span></span>

<span data-ttu-id="ebc45-127">Чтобы протестировать определенную выше функцию, скопируйте **URL-адрес функции** с портала.</span><span class="sxs-lookup"><span data-stu-id="ebc45-127">To test the function we defined earlier, copy the **Function Url** from the portal.</span></span> <span data-ttu-id="ebc45-128">В нем используется следующий формат:</span><span class="sxs-lookup"><span data-stu-id="ebc45-128">It has the following form:</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="ebc45-129">Добавьте параметр `name` к строке запроса.</span><span class="sxs-lookup"><span data-stu-id="ebc45-129">Append the `name` parameter to the query string.</span></span> <span data-ttu-id="ebc45-130">Используйте фактическое имя для заполнителя `<Enter a name here>`.</span><span class="sxs-lookup"><span data-stu-id="ebc45-130">Use an actual name for the `<Enter a name here>` placeholder.</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>&name=<Enter a name here>

<span data-ttu-id="ebc45-131">Вставьте URL-адрес в браузер. Должен отобразиться примерно такой ответ.</span><span class="sxs-lookup"><span data-stu-id="ebc45-131">Paste the URL into your browser, and you should get a response similar to the following.</span></span>

![Снимок экрана: вкладка браузера Chrome с ответом теста](./media/functions-test-a-function/browser-test.png)

<span data-ttu-id="ebc45-133">В данном примере используется браузер Chrome, который заключает возвращаемую строку в формат XML.</span><span class="sxs-lookup"><span data-stu-id="ebc45-133">This example is the Chrome browser, which wraps the returned string in XML.</span></span> <span data-ttu-id="ebc45-134">Другие браузеры отображают только строковое значение.</span><span class="sxs-lookup"><span data-stu-id="ebc45-134">Other browsers display just the string value.</span></span>

<span data-ttu-id="ebc45-135">В окне **Журналы** на портале при выполнении функции регистрируются выходные данные, подобные следующим:</span><span class="sxs-lookup"><span data-stu-id="ebc45-135">In the portal **Logs** window, output similar to the following is logged in executing the function:</span></span>

    2016-03-23T07:34:59  Welcome, you are now connected to log-streaming service.
    2016-03-23T07:35:09.195 Function started (Id=61a8c5a9-5e44-4da0-909d-91d293f20445)
    2016-03-23T07:35:10.338 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==&name=Glenn from a browser
    2016-03-23T07:35:10.338 Request Headers = {"cache-control":"max-age=0","connection":"Keep-Alive","accept":"text/html","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T07:35:10.338 Name was provided as a query string param.
    2016-03-23T07:35:10.338 Processing User Information...
    2016-03-23T07:35:10.369 Function completed (Success, Id=61a8c5a9-5e44-4da0-909d-91d293f20445)

### <a name="test-with-postman"></a><span data-ttu-id="ebc45-136">Тестирование с помощью приложения Postman</span><span class="sxs-lookup"><span data-stu-id="ebc45-136">Test with Postman</span></span>
<span data-ttu-id="ebc45-137">Рекомендуемым инструментом для тестирования большинства функций является приложение Postman, которое интегрируется с браузером Chrome.</span><span class="sxs-lookup"><span data-stu-id="ebc45-137">The recommended tool to test most of your functions is Postman, which integrates with the Chrome browser.</span></span> <span data-ttu-id="ebc45-138">Чтобы установить Postman, см. веб-страницу, на которой можно [получить приложение Postman](https://www.getpostman.com/).</span><span class="sxs-lookup"><span data-stu-id="ebc45-138">To install Postman, see [Get Postman](https://www.getpostman.com/).</span></span> <span data-ttu-id="ebc45-139">Приложение Postman позволяет контролировать намного больше атрибутов HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="ebc45-139">Postman provides control over many more attributes of an HTTP request.</span></span>

> [!TIP]
> <span data-ttu-id="ebc45-140">Используйте инструмент для тестирования на основе HTTP, который для вас наиболее удобен.</span><span class="sxs-lookup"><span data-stu-id="ebc45-140">Use the HTTP testing tool that you are most comfortable with.</span></span> <span data-ttu-id="ebc45-141">Вот некоторые альтернативы Postman:</span><span class="sxs-lookup"><span data-stu-id="ebc45-141">Here are some alternatives to Postman:</span></span>  
>
> * [<span data-ttu-id="ebc45-142">Fiddler</span><span class="sxs-lookup"><span data-stu-id="ebc45-142">Fiddler</span></span>](http://www.telerik.com/fiddler)  
> * [<span data-ttu-id="ebc45-143">Paw.</span><span class="sxs-lookup"><span data-stu-id="ebc45-143">Paw</span></span>](https://luckymarmot.com/paw)  
>
>

<span data-ttu-id="ebc45-144">Чтобы протестировать функцию с текстом запроса в приложении Postman, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ebc45-144">To test the function with a request body in Postman:</span></span>

1. <span data-ttu-id="ebc45-145">Запустите Postman нажатием кнопки **Приложения** в левом верхнем углу окна браузера Chrome.</span><span class="sxs-lookup"><span data-stu-id="ebc45-145">Start Postman from the **Apps** button in the upper-left corner of a Chrome browser window.</span></span>
2. <span data-ttu-id="ebc45-146">Скопируйте **URL-адрес функции** и вставьте его в Postman.</span><span class="sxs-lookup"><span data-stu-id="ebc45-146">Copy your **Function Url**, and paste it into Postman.</span></span> <span data-ttu-id="ebc45-147">В нем содержится параметр строки запроса — код доступа.</span><span class="sxs-lookup"><span data-stu-id="ebc45-147">It includes the access code query string parameter.</span></span>
3. <span data-ttu-id="ebc45-148">Замените метод HTTP на **POST**.</span><span class="sxs-lookup"><span data-stu-id="ebc45-148">Change the HTTP method to **POST**.</span></span>
4. <span data-ttu-id="ebc45-149">Щелкните **Body** > **raw** (Текст > Необработанный) и добавьте текст запроса JSON, подобный следующему:</span><span class="sxs-lookup"><span data-stu-id="ebc45-149">Click **Body** > **raw**, and add a JSON request body similar to the following:</span></span>

    ```json
    {
        "name" : "Wes testing with Postman",
        "address" : "Seattle, WA 98101"
    }
    ```
5. <span data-ttu-id="ebc45-150">Нажмите кнопку **Send**(Отправить).</span><span class="sxs-lookup"><span data-stu-id="ebc45-150">Click **Send**.</span></span>

<span data-ttu-id="ebc45-151">На следующем рисунке показано тестирование простого примера эхо-функции из этого руководства.</span><span class="sxs-lookup"><span data-stu-id="ebc45-151">The following image shows testing the simple echo function example in this tutorial.</span></span>

![Снимок экрана: пользовательский интерфейс Postman](./media/functions-test-a-function/postman-test.png)

<span data-ttu-id="ebc45-153">В окне **Журналы** на портале при выполнении функции регистрируются выходные данные, подобные следующим:</span><span class="sxs-lookup"><span data-stu-id="ebc45-153">In the portal **Logs** window, output similar to the following is logged in executing the function:</span></span>

    2016-03-23T08:04:51  Welcome, you are now connected to log-streaming service.
    2016-03-23T08:04:57.107 Function started (Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)
    2016-03-23T08:04:57.763 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==
    2016-03-23T08:04:57.763 Request Headers = {"cache-control":"no-cache","connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:04:57.763 Processing user info from request body...
    2016-03-23T08:04:57.763 Processing User Information...
    2016-03-23T08:04:57.763 name = Wes testing with Postman
    2016-03-23T08:04:57.763 address = Seattle, W.A. 98101
    2016-03-23T08:04:57.795 Function completed (Success, Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)

### <a name="test-with-curl-from-the-command-line"></a><span data-ttu-id="ebc45-154">Тестирование с помощью cURL из командной строки</span><span class="sxs-lookup"><span data-stu-id="ebc45-154">Test with cURL from the command line</span></span>
<span data-ttu-id="ebc45-155">Часто при тестировании программного обеспечения для отладки приложения достаточно командной строки.</span><span class="sxs-lookup"><span data-stu-id="ebc45-155">Often when you're testing software, it's not necessary to look any further than the command line to help debug your application.</span></span> <span data-ttu-id="ebc45-156">То же самое справедливо и для функций.</span><span class="sxs-lookup"><span data-stu-id="ebc45-156">This is no different with testing functions.</span></span> <span data-ttu-id="ebc45-157">Обратите внимание, что инструмент cURL по умолчанию доступен в системах на основе Linux.</span><span class="sxs-lookup"><span data-stu-id="ebc45-157">Note that the cURL is available by default on Linux-based systems.</span></span> <span data-ttu-id="ebc45-158">При использовании Windows [инструмент cURL](https://curl.haxx.se/) необходимо сначала скачать и установить.</span><span class="sxs-lookup"><span data-stu-id="ebc45-158">On Windows, you must first download and install the [cURL tool](https://curl.haxx.se/).</span></span>

<span data-ttu-id="ebc45-159">Чтобы протестировать определенную выше функцию, скопируйте **URL-адрес функции** с портала.</span><span class="sxs-lookup"><span data-stu-id="ebc45-159">To test the function that we defined earlier, copy the **Function URL** from the portal.</span></span> <span data-ttu-id="ebc45-160">В нем используется следующий формат:</span><span class="sxs-lookup"><span data-stu-id="ebc45-160">It has the following form:</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="ebc45-161">Это URL-адрес для активации функции.</span><span class="sxs-lookup"><span data-stu-id="ebc45-161">This is the URL for triggering your function.</span></span> <span data-ttu-id="ebc45-162">Протестируйте его, используя команду cURL в командной строке, чтобы выполнить запрос GET (`-G` или `--get`) к функции:</span><span class="sxs-lookup"><span data-stu-id="ebc45-162">Test this by using the cURL command on the command line to make a GET (`-G` or `--get`) request against the function:</span></span>

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="ebc45-163">В этом конкретном примере требуется параметр строки запроса, который может быть передан как данные (`-d`) в команде cURL:</span><span class="sxs-lookup"><span data-stu-id="ebc45-163">This particular example requires a query string parameter, which can be passed as Data (`-d`) in the cURL command:</span></span>

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code> -d name=<Enter a name here>

<span data-ttu-id="ebc45-164">Выполните команду, и вы увидите выходные данные функции в командной строке:</span><span class="sxs-lookup"><span data-stu-id="ebc45-164">Run the command, and you see the following output of the function on the command line:</span></span>

![Снимок экрана: выходные данные в командной строке](./media/functions-test-a-function/curl-test.png)

<span data-ttu-id="ebc45-166">В окне **Журналы** на портале при выполнении функции регистрируются выходные данные, подобные следующим:</span><span class="sxs-lookup"><span data-stu-id="ebc45-166">In the portal **Logs** window, output similar to the following is logged in executing the function:</span></span>

    2016-04-05T21:55:09  Welcome, you are now connected to log-streaming service.
    2016-04-05T21:55:30.738 Function started (Id=ae6955da-29db-401a-b706-482fcd1b8f7a)
    2016-04-05T21:55:30.738 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/HttpTriggerNodeJS1?code=XXXXXXX&name=Azure Functions
    2016-04-05T21:55:30.738 Function completed (Success, Id=ae6955da-29db-401a-b706-482fcd1b8f7a)

### <a name="test-a-blob-trigger-by-using-storage-explorer"></a><span data-ttu-id="ebc45-167">Тестирование триггера больших двоичных объектов с помощью Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="ebc45-167">Test a blob trigger by using Storage Explorer</span></span>
<span data-ttu-id="ebc45-168">Функцию триггера больших двоичных объектов можно протестировать с помощью [Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="ebc45-168">You can test a blob trigger function by using [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

1. <span data-ttu-id="ebc45-169">На [портале Azure] для приложения-функции создайте функцию триггера больших двоичных объектов на языке C#, F# или JavaScript.</span><span class="sxs-lookup"><span data-stu-id="ebc45-169">In the [Azure portal] for your function app, create a C#, F# or JavaScript blob trigger function.</span></span> <span data-ttu-id="ebc45-170">Задайте путь для отслеживания имени контейнера больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="ebc45-170">Set the path to monitor to the name of your blob container.</span></span> <span data-ttu-id="ebc45-171">Например:</span><span class="sxs-lookup"><span data-stu-id="ebc45-171">For example:</span></span>

        files
2. <span data-ttu-id="ebc45-172">Нажмите кнопку **+** , чтобы выбрать или создать учетную запись хранения, которую следует использовать.</span><span class="sxs-lookup"><span data-stu-id="ebc45-172">Click the **+** button to select or create the storage account you want to use.</span></span> <span data-ttu-id="ebc45-173">Затем щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ebc45-173">Then click **Create**.</span></span>
3. <span data-ttu-id="ebc45-174">Создайте текстовый файл со следующим содержимым и сохраните его.</span><span class="sxs-lookup"><span data-stu-id="ebc45-174">Create a text file with the following text, and save it:</span></span>

        A text file for blob trigger function testing.
4. <span data-ttu-id="ebc45-175">Запустите [Azure Storage Explorer](http://storageexplorer.com/) и подключитесь к контейнеру больших двоичных объектов в отслеживаемой учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="ebc45-175">Run [Azure Storage Explorer](http://storageexplorer.com/), and connect to the blob container in the storage account being monitored.</span></span>
5. <span data-ttu-id="ebc45-176">Нажмите кнопку **Отправить**, чтобы отправить текстовый файл.</span><span class="sxs-lookup"><span data-stu-id="ebc45-176">Click **Upload** to upload the text file.</span></span>

    ![Снимок экрана: Storage Explorer](./media/functions-test-a-function/azure-storage-explorer-test.png)

<span data-ttu-id="ebc45-178">Используемый по умолчанию код функции триггера больших двоичных объектов сообщит об обработке большого двоичного объекта в журналах:</span><span class="sxs-lookup"><span data-stu-id="ebc45-178">The default blob trigger function code reports the processing of the blob in the logs:</span></span>

    2016-03-24T11:30:10  Welcome, you are now connected to log-streaming service.
    2016-03-24T11:30:34.472 Function started (Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)
    2016-03-24T11:30:34.472 C# Blob trigger function processed: A text file for blob trigger function testing.
    2016-03-24T11:30:34.472 Function completed (Success, Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)

## <a name="test-a-function-within-functions"></a><span data-ttu-id="ebc45-179">Тестирование функции в рамках функций</span><span class="sxs-lookup"><span data-stu-id="ebc45-179">Test a function within functions</span></span>
<span data-ttu-id="ebc45-180">Портал Функций Azure разработан, чтобы помочь в тестировании функций, активируемых с помощью протокола HTTP или по таймеру.</span><span class="sxs-lookup"><span data-stu-id="ebc45-180">The Azure Functions portal is designed to let you test HTTP and timer triggered functions.</span></span> <span data-ttu-id="ebc45-181">Также на нем можно создавать функции для активации других тестируемых функций.</span><span class="sxs-lookup"><span data-stu-id="ebc45-181">You can also create functions to trigger other functions that you are testing.</span></span>

### <a name="test-with-the-functions-portal-run-button"></a><span data-ttu-id="ebc45-182">Тестирование с помощью кнопки "Выполнить" на портале функций</span><span class="sxs-lookup"><span data-stu-id="ebc45-182">Test with the Functions portal Run button</span></span>
<span data-ttu-id="ebc45-183">На портале есть кнопка **Выполнить**, которая позволяет провести ограниченное тестирование.</span><span class="sxs-lookup"><span data-stu-id="ebc45-183">The portal provides a **Run** button that you can use to do some limited testing.</span></span> <span data-ttu-id="ebc45-184">С помощью этой кнопки можно указать текст запроса, но нельзя указать параметры строки запроса или обновить заголовки запроса.</span><span class="sxs-lookup"><span data-stu-id="ebc45-184">You can provide a request body by using the button, but you can't provide query string parameters or update request headers.</span></span>

<span data-ttu-id="ebc45-185">Протестируйте функцию HTTP-триггера, созданную ранее, добавив в поле **Текст запроса** строку JSON, подобную указанной ниже.</span><span class="sxs-lookup"><span data-stu-id="ebc45-185">Test the HTTP trigger function we created earlier by adding a JSON string similar to the following in the **Request body** field.</span></span> <span data-ttu-id="ebc45-186">Затем нажмите кнопку **Выполнить**.</span><span class="sxs-lookup"><span data-stu-id="ebc45-186">Then click the **Run** button.</span></span>

```json
{
    "name" : "Wes testing Run button",
    "address" : "USA"
}
```

<span data-ttu-id="ebc45-187">В окне **Журналы** на портале при выполнении функции регистрируются выходные данные, подобные следующим:</span><span class="sxs-lookup"><span data-stu-id="ebc45-187">In the portal **Logs** window, output similar to the following is logged in executing the function:</span></span>

    2016-03-23T08:03:12  Welcome, you are now connected to log-streaming service.
    2016-03-23T08:03:17.357 Function started (Id=753a01b0-45a8-4125-a030-3ad543a89409)
    2016-03-23T08:03:18.697 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/wesmchttptriggernodejs1
    2016-03-23T08:03:18.697 Request Headers = {"connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:03:18.697 Processing user info from request body...
    2016-03-23T08:03:18.697 Processing User Information...
    2016-03-23T08:03:18.697 name = Wes testing Run button
    2016-03-23T08:03:18.697 address = USA
    2016-03-23T08:03:18.744 Function completed (Success, Id=753a01b0-45a8-4125-a030-3ad543a89409)


### <a name="test-with-a-timer-trigger"></a><span data-ttu-id="ebc45-188">Тестирование с помощью триггера таймера</span><span class="sxs-lookup"><span data-stu-id="ebc45-188">Test with a timer trigger</span></span>
<span data-ttu-id="ebc45-189">Некоторые функции нельзя правильно протестировать с помощью упомянутых ранее средств.</span><span class="sxs-lookup"><span data-stu-id="ebc45-189">Some functions can't be adequately tested with the tools mentioned previously.</span></span> <span data-ttu-id="ebc45-190">Например, функцию триггера очереди, которая выполняется при поступлении сообщения в [хранилище очередей Azure](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="ebc45-190">For example, consider a queue trigger function that runs when a message is dropped into [Azure Queue storage](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span> <span data-ttu-id="ebc45-191">Всегда можно написать код, помещающий сообщение в очередь, пример которого указан в консольном проекте далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="ebc45-191">You can always write code to drop a message into your queue, and an example of this in a console project is provided later in this article.</span></span> <span data-ttu-id="ebc45-192">Однако существует другой подход, который можно использовать для непосредственного тестирования функций.</span><span class="sxs-lookup"><span data-stu-id="ebc45-192">However, there is another approach you can use that tests functions directly.</span></span>  

<span data-ttu-id="ebc45-193">Можно использовать триггер таймера, настроенный с привязкой для вывода очереди.</span><span class="sxs-lookup"><span data-stu-id="ebc45-193">You can use a timer trigger configured with a queue output binding.</span></span> <span data-ttu-id="ebc45-194">Такой код триггера таймера может затем записывать тестовые сообщения в очередь.</span><span class="sxs-lookup"><span data-stu-id="ebc45-194">That timer trigger code can then write the test messages to the queue.</span></span> <span data-ttu-id="ebc45-195">В этом разделе описан пример.</span><span class="sxs-lookup"><span data-stu-id="ebc45-195">This section walks through an example.</span></span>

<span data-ttu-id="ebc45-196">Более подробные сведения об использовании привязок с Функциями Azure см. в статье [Справочник разработчика по Функциям Azure](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="ebc45-196">For more in-depth information on using bindings with Azure Functions, see the [Azure Functions developer reference](functions-reference.md).</span></span>

#### <a name="create-a-queue-trigger-for-testing"></a><span data-ttu-id="ebc45-197">Создание триггера очереди для тестирования</span><span class="sxs-lookup"><span data-stu-id="ebc45-197">Create a queue trigger for testing</span></span>
<span data-ttu-id="ebc45-198">Чтобы продемонстрировать этот подход, мы сначала создадим функцию триггера очереди, которую нам нужно протестировать, для очереди с именем `queue-newusers`.</span><span class="sxs-lookup"><span data-stu-id="ebc45-198">To demonstrate this approach, we first create a queue trigger function that we want to test for a queue named `queue-newusers`.</span></span> <span data-ttu-id="ebc45-199">Эта функция обрабатывает имя и адрес нового пользователя, поступившие в хранилище очередей.</span><span class="sxs-lookup"><span data-stu-id="ebc45-199">This function processes name and address information dropped into Queue storage for a new user.</span></span>

> [!NOTE]
> <span data-ttu-id="ebc45-200">При использовании другого имени очереди убедитесь, что используемое имя соответствует правилам [именования очередей и метаданных](https://msdn.microsoft.com/library/dd179349.aspx) .</span><span class="sxs-lookup"><span data-stu-id="ebc45-200">If you use a different queue name, make sure the name you use conforms to the [Naming Queues and MetaData](https://msdn.microsoft.com/library/dd179349.aspx) rules.</span></span> <span data-ttu-id="ebc45-201">В противном случае возникает ошибка.</span><span class="sxs-lookup"><span data-stu-id="ebc45-201">Otherwise, you get an error.</span></span>
>
>

1. <span data-ttu-id="ebc45-202">На [портале Azure] для приложения-функции щелкните **Новая функция** > **QueueTrigger — C#**.</span><span class="sxs-lookup"><span data-stu-id="ebc45-202">In the [Azure portal] for your function app, click **New Function** > **QueueTrigger - C#**.</span></span>
2. <span data-ttu-id="ebc45-203">Введите имя очереди, которое будет отслеживаться функцией очереди:</span><span class="sxs-lookup"><span data-stu-id="ebc45-203">Enter the queue name to be monitored by the queue function:</span></span>

        queue-newusers
3. <span data-ttu-id="ebc45-204">Нажмите кнопку **+** , чтобы выбрать или создать учетную запись хранения, которую следует использовать.</span><span class="sxs-lookup"><span data-stu-id="ebc45-204">Click the **+** button to select or create the storage account you want to use.</span></span> <span data-ttu-id="ebc45-205">Затем щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ebc45-205">Then click **Create**.</span></span>
4. <span data-ttu-id="ebc45-206">Оставьте это окно браузера с порталом открытым, чтобы можно было отслеживать записи журнала на наличие стандартного кода шаблона функции очереди.</span><span class="sxs-lookup"><span data-stu-id="ebc45-206">Leave this portal browser window open, so you can monitor the log entries for the default queue function template code.</span></span>

#### <a name="create-a-timer-trigger-to-drop-a-message-in-the-queue"></a><span data-ttu-id="ebc45-207">Создание триггера таймера для помещения сообщения в очередь</span><span class="sxs-lookup"><span data-stu-id="ebc45-207">Create a timer trigger to drop a message in the queue</span></span>
1. <span data-ttu-id="ebc45-208">Откройте [портале Azure] в новом окне браузера и перейдите к приложению-функции.</span><span class="sxs-lookup"><span data-stu-id="ebc45-208">Open the [Azure portal] in a new browser window, and navigate to your function app.</span></span>
2. <span data-ttu-id="ebc45-209">Щелкните **Новая функция** > **TimerTrigger — C#**.</span><span class="sxs-lookup"><span data-stu-id="ebc45-209">Click **New Function** > **TimerTrigger - C#**.</span></span> <span data-ttu-id="ebc45-210">Введите выражение CRON, чтобы задать частоту выполнения кода таймера при тестировании функции очереди.</span><span class="sxs-lookup"><span data-stu-id="ebc45-210">Enter a cron expression to set how often the timer code tests your queue function.</span></span> <span data-ttu-id="ebc45-211">Затем щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ebc45-211">Then click **Create**.</span></span> <span data-ttu-id="ebc45-212">Если тестирование нужно выполнять каждые 30 секунд, можно использовать следующее [выражение CRON](https://wikipedia.org/wiki/Cron#CRON_expression):</span><span class="sxs-lookup"><span data-stu-id="ebc45-212">If you want the test to run every 30 seconds, you can use the following [CRON expression](https://wikipedia.org/wiki/Cron#CRON_expression):</span></span>

        */30 * * * * *
3. <span data-ttu-id="ebc45-213">Выберите вкладку **Интеграция** для нового триггера таймера.</span><span class="sxs-lookup"><span data-stu-id="ebc45-213">Click the **Integrate** tab for your new timer trigger.</span></span>
4. <span data-ttu-id="ebc45-214">В разделе **Выходные данные** щелкните **+ Новое выходное значение**.</span><span class="sxs-lookup"><span data-stu-id="ebc45-214">Under **Output**, click **+ New Output**.</span></span> <span data-ttu-id="ebc45-215">Затем последовательно щелкните **Очередь** и **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="ebc45-215">Then click **queue** and **Select**.</span></span>
5. <span data-ttu-id="ebc45-216">Запишите имя, используемое для **объекта сообщения очереди**.</span><span class="sxs-lookup"><span data-stu-id="ebc45-216">Note the name you use for the **queue message object**.</span></span> <span data-ttu-id="ebc45-217">Оно будет использоваться в коде функции таймера.</span><span class="sxs-lookup"><span data-stu-id="ebc45-217">You use this in the timer function code.</span></span>

        myQueue
6. <span data-ttu-id="ebc45-218">Введите имя очереди, в которую будет отправлено сообщение:</span><span class="sxs-lookup"><span data-stu-id="ebc45-218">Enter the queue name where the message is sent:</span></span>

        queue-newusers
7. <span data-ttu-id="ebc45-219">Нажмите кнопку **+**, чтобы выбрать учетную запись хранения, указанную ранее в триггере очереди.</span><span class="sxs-lookup"><span data-stu-id="ebc45-219">Click the **+** button to select the storage account you used previously with the queue trigger.</span></span> <span data-ttu-id="ebc45-220">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="ebc45-220">Then click **Save**.</span></span>
8. <span data-ttu-id="ebc45-221">Выберите вкладку **Разработка** для триггера таймера.</span><span class="sxs-lookup"><span data-stu-id="ebc45-221">Click the **Develop** tab for your timer trigger.</span></span>
9. <span data-ttu-id="ebc45-222">Для функции таймера на языке C# можно использовать приведенный ниже код, если вы использовали то же имя объекта сообщения очереди, указанное выше.</span><span class="sxs-lookup"><span data-stu-id="ebc45-222">You can use the following code for the C# timer function, as long as you used the same queue message object name shown earlier.</span></span> <span data-ttu-id="ebc45-223">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="ebc45-223">Then click **Save**.</span></span>

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

<span data-ttu-id="ebc45-224">На этом этапе функция таймера на C# выполняется каждые 30 секунд, если вы использовали выражение CRON из примера.</span><span class="sxs-lookup"><span data-stu-id="ebc45-224">At this point, the C# timer function executes every 30 seconds if you used the example cron expression.</span></span> <span data-ttu-id="ebc45-225">Журналы для функции таймера сообщают о каждом выполнении:</span><span class="sxs-lookup"><span data-stu-id="ebc45-225">The logs for the timer function report each execution:</span></span>

    2016-03-24T10:27:02  Welcome, you are now connected to log-streaming service.
    2016-03-24T10:27:30.004 Function started (Id=04061790-974f-4043-b851-48bd4ac424d1)
    2016-03-24T10:27:30.004 C# Timer trigger function executed at: 3/24/2016 10:27:30 AM
    2016-03-24T10:27:30.004 {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.004 Function completed (Success, Id=04061790-974f-4043-b851-48bd4ac424d1)

<span data-ttu-id="ebc45-226">В окне браузера для функции очереди отображается каждое обрабатываемое сообщение:</span><span class="sxs-lookup"><span data-stu-id="ebc45-226">In the browser window for the queue function, you can see each message being processed:</span></span>

    2016-03-24T10:27:06  Welcome, you are now connected to log-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)

## <a name="test-a-function-with-code"></a><span data-ttu-id="ebc45-227">Тестирование функции с помощью кода</span><span class="sxs-lookup"><span data-stu-id="ebc45-227">Test a function with code</span></span>
<span data-ttu-id="ebc45-228">Вам может потребоваться создать внешнее приложение или платформу для тестирования функций.</span><span class="sxs-lookup"><span data-stu-id="ebc45-228">You may need to create an external application or framework to test your functions.</span></span>

### <a name="test-an-http-trigger-function-with-code-nodejs"></a><span data-ttu-id="ebc45-229">Тестирование функции HTTP-триггера с помощью кода: Node.js</span><span class="sxs-lookup"><span data-stu-id="ebc45-229">Test an HTTP trigger function with code: Node.js</span></span>
<span data-ttu-id="ebc45-230">Чтобы выполнить HTTP-запрос для тестирования функции, можно использовать приложение Node.js.</span><span class="sxs-lookup"><span data-stu-id="ebc45-230">You can use a Node.js app to execute an HTTP request to test your function.</span></span>
<span data-ttu-id="ebc45-231">Не забудьте задать следующие значения:</span><span class="sxs-lookup"><span data-stu-id="ebc45-231">Make sure to set:</span></span>

* <span data-ttu-id="ebc45-232">для `host` в параметрах запроса — узел приложения функции;</span><span class="sxs-lookup"><span data-stu-id="ebc45-232">The `host` in the request options to your function app host.</span></span>
* <span data-ttu-id="ebc45-233">имя функции в параметре `path`;</span><span class="sxs-lookup"><span data-stu-id="ebc45-233">Your function name in the `path`.</span></span>
* <span data-ttu-id="ebc45-234">код доступа (`<your code>`) в параметре `path`.</span><span class="sxs-lookup"><span data-stu-id="ebc45-234">Your access code (`<your code>`) in the `path`.</span></span>

<span data-ttu-id="ebc45-235">Пример кода:</span><span class="sxs-lookup"><span data-stu-id="ebc45-235">Code example:</span></span>

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


<span data-ttu-id="ebc45-236">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="ebc45-236">Output:</span></span>

    C:\Users\Wesley\testing\Node.js>node testHttpTriggerExample.js
    *** Sending name and address in body ***
    {"name" : "Wes testing with Node.JS code","address" : "Dallas, T.X. 75201"}
    Hello Wes testing with Node.JS code
    The address you provided is Dallas, T.X. 75201

<span data-ttu-id="ebc45-237">В окне **Журналы** на портале при выполнении функции регистрируются выходные данные, подобные следующим:</span><span class="sxs-lookup"><span data-stu-id="ebc45-237">In the portal **Logs** window, output similar to the following is logged in executing the function:</span></span>

    2016-03-23T08:08:55  Welcome, you are now connected to log-streaming service.
    2016-03-23T08:08:59.736 Function started (Id=607b891c-08a1-427f-910c-af64ae4f7f9c)
    2016-03-23T08:09:01.153 HTTP trigger function processed a request. RequestUri=http://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1/?code=XXXXXXXXXX==
    2016-03-23T08:09:01.153 Request Headers = {"connection":"Keep-Alive","host":"functionsExample.azurewebsites.net"}
    2016-03-23T08:09:01.153 Name not provided as query string param. Checking body...
    2016-03-23T08:09:01.153 Request Body Type = object
    2016-03-23T08:09:01.153 Request Body = [object Object]
    2016-03-23T08:09:01.153 Processing User Information...
    2016-03-23T08:09:01.215 Function completed (Success, Id=607b891c-08a1-427f-910c-af64ae4f7f9c)


### <a name="test-a-queue-trigger-function-with-code-c"></a><span data-ttu-id="ebc45-238">Тестирование функции триггера очереди с помощью кода: C#</span><span class="sxs-lookup"><span data-stu-id="ebc45-238">Test a queue trigger function with code: C#</span></span> #
<span data-ttu-id="ebc45-239">Мы уже упоминали, что триггер очереди можно протестировать с помощью кода, поместив сообщение в очередь.</span><span class="sxs-lookup"><span data-stu-id="ebc45-239">We mentioned earlier that you can test a queue trigger by using code to drop a message in your queue.</span></span> <span data-ttu-id="ebc45-240">Следующий пример кода основан на коде C#, представленном в руководстве [Приступая к работе с хранилищем очередей Azure с помощью .NET](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="ebc45-240">The following example code is based on the C# code presented in the [Getting started with Azure Queue storage](../storage/queues/storage-dotnet-how-to-use-queues.md) tutorial.</span></span> <span data-ttu-id="ebc45-241">По этой ссылке также доступен код для других языков.</span><span class="sxs-lookup"><span data-stu-id="ebc45-241">Code for other languages is also available from that link.</span></span>

<span data-ttu-id="ebc45-242">Чтобы протестировать этот код в консольном приложении, необходимо сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="ebc45-242">To test this code in a console app, you must:</span></span>

* <span data-ttu-id="ebc45-243">[Настройте строку подключения хранилища в файле app.config](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="ebc45-243">[Configure your storage connection string in the app.config file](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>
* <span data-ttu-id="ebc45-244">Передайте `name` и `address` в качестве параметров в приложение.</span><span class="sxs-lookup"><span data-stu-id="ebc45-244">Pass a `name` and `address` as parameters to the app.</span></span> <span data-ttu-id="ebc45-245">Например, `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`.</span><span class="sxs-lookup"><span data-stu-id="ebc45-245">For example, `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`.</span></span> <span data-ttu-id="ebc45-246">(Этот код принимает имя и адрес для нового пользователя в качестве аргументов командной строки во время выполнения.)</span><span class="sxs-lookup"><span data-stu-id="ebc45-246">(This code accepts the name and address for a new user as command-line arguments during runtime.)</span></span>

<span data-ttu-id="ebc45-247">Пример кода C#:</span><span class="sxs-lookup"><span data-stu-id="ebc45-247">Example C# code:</span></span>

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

    // Create the queue client
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

    // Retrieve a reference to a queue
    CloudQueue queue = queueClient.GetQueueReference(queueName);

    // Create the queue if it doesn't already exist
    queue.CreateIfNotExists();

    // Create a message and add it to the queue.
    if (name != null)
    {
        if (address != null)
            JSON = String.Format("{{\"name\":\"{0}\",\"address\":\"{1}\"}}", name, address);
        else
            JSON = String.Format("{{\"name\":\"{0}\"}}", name);
    }

    Console.WriteLine("Adding message to " + queueName + "...");
    Console.WriteLine(JSON);

    CloudQueueMessage message = new CloudQueueMessage(JSON);
    queue.AddMessage(message);
}
```

<span data-ttu-id="ebc45-248">В окне браузера для функции очереди отображается каждое обрабатываемое сообщение:</span><span class="sxs-lookup"><span data-stu-id="ebc45-248">In the browser window for the queue function, you can see each message being processed:</span></span>

    2016-03-24T10:27:06  Welcome, you are now connected to log-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"Wes testing queues","address":"in a console app"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)


<!-- URLs. -->

[портале Azure]: https://portal.azure.com
