---
title: "Создание первой функции в Azure с помощью Visual Studio | Документация Майкрософт"
description: "Создание и публикация в Azure простой функции, активируемой HTTP, с помощью инструментов функций Azure для Visual Studio."
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
editor: 
tags: 
keywords: "функции azure, функции, обработка событий, вычисления, независимая архитектура"
ms.assetid: 82db1177-2295-4e39-bd42-763f6082e796
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 07/05/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 04370558725d76ffe83d8aaf5d16c88fd2803ba9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-function-using-visual-studio"></a><span data-ttu-id="a7d81-104">Создание первой функции с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a7d81-104">Create your first function using Visual Studio</span></span>

<span data-ttu-id="a7d81-105">Функции Azure позволяют вам выполнять свой код в бессерверной среде без необходимости создавать виртуальную машину или публиковать веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="a7d81-105">Azure Functions lets you execute your code in a serverless environment without having to first create a VM or publish a web application.</span></span>

<span data-ttu-id="a7d81-106">Изучив эту статью, вы научитесь использовать инструменты Visual Studio 2017 для Функций Azure и локально тестировать функцию hello world.</span><span class="sxs-lookup"><span data-stu-id="a7d81-106">In this topic, you learn how to use the Visual Studio 2017 tools for Azure Functions to create and test a "hello world" function locally.</span></span> <span data-ttu-id="a7d81-107">Затем вы опубликуете код функции в Azure.</span><span class="sxs-lookup"><span data-stu-id="a7d81-107">You will then publish the function code to Azure.</span></span> <span data-ttu-id="a7d81-108">Эти средства доступны как часть рабочей нагрузки Azure для разработки в Visual Studio 2017 версии 15.3 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="a7d81-108">These tools are available as part of the Azure development workload in Visual Studio 2017 version 15.3, or a later version.</span></span>

![Код функций Azure в проекте Visual Studio](./media/functions-create-your-first-function-visual-studio/functions-vstools-intro.png)

## <a name="prerequisites"></a><span data-ttu-id="a7d81-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a7d81-110">Prerequisites</span></span>

<span data-ttu-id="a7d81-111">Для работы с этим руководством установите следующие компоненты.</span><span class="sxs-lookup"><span data-stu-id="a7d81-111">To complete this tutorial, install:</span></span>

* <span data-ttu-id="a7d81-112">[Visual Studio 2017 версия 15.3](https://www.visualstudio.com/vs/preview/), включая рабочую нагрузку**разработки в Azure**.</span><span class="sxs-lookup"><span data-stu-id="a7d81-112">[Visual Studio 2017 version 15.3](https://www.visualstudio.com/vs/preview/), including the **Azure development** workload.</span></span>

    ![Установка Visual Studio 2017 с рабочей нагрузкой разработки в Azure](./media/functions-create-your-first-function-visual-studio/functions-vs-workloads.png)
    
    >[!NOTE]  
    <span data-ttu-id="a7d81-114">После установки Visual Studio 2017 версии 15.3 или обновления до этой версии вам также может потребоваться вручную обновить инструменты Visual Studio 2017 для Функций Azure.</span><span class="sxs-lookup"><span data-stu-id="a7d81-114">After you install or upgrade to Visual Studio 2017 version 15.3, you might also need to manually update the Visual Studio 2017 tools for Azure Functions.</span></span> <span data-ttu-id="a7d81-115">Для обновления инструментов можно воспользоваться меню **Инструменты** в разделе **Расширения и обновления...** > **Обновления** > **Visual Studio Marketplace** > **Azure Functions and Web Jobs Tools** (Инструменты для функций и веб-заданий Azure)  > **Обновление**.</span><span class="sxs-lookup"><span data-stu-id="a7d81-115">You can update the tools from the **Tools** menu under **Extensions and Updates...** > **Updates** > **Visual Studio Marketplace** > **Azure Functions and Web Jobs Tools** > **Update**.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] 

## <a name="create-an-azure-functions-project-in-visual-studio"></a><span data-ttu-id="a7d81-116">Создание проекта функций Azure в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a7d81-116">Create an Azure Functions project in Visual Studio</span></span>

[!INCLUDE [Create a project using the Azure Functions template](../../includes/functions-vstools-create.md)]

<span data-ttu-id="a7d81-117">После создания проекта можно приступать к созданию первой функции.</span><span class="sxs-lookup"><span data-stu-id="a7d81-117">Now that you have created the project, you can create your first function.</span></span>

## <a name="create-the-function"></a><span data-ttu-id="a7d81-118">Создание функции</span><span class="sxs-lookup"><span data-stu-id="a7d81-118">Create the function</span></span>

1. <span data-ttu-id="a7d81-119">Щелкните правой кнопкой мыши узел проекта в **обозревателе решений** и выберите **Добавить** > **Новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="a7d81-119">In **Solution Explorer**, right-click on your project node and select **Add** > **New Item**.</span></span> <span data-ttu-id="a7d81-120">Выберите **Функция Azure** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a7d81-120">Select **Azure Function** and click **Add**.</span></span>

2. <span data-ttu-id="a7d81-121">Выберите **HttpTrigger**, укажите **имя функции**, выберите для параметра **Права доступа** значение **Анонимно** и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a7d81-121">Select **HttpTrigger**, type a **Function Name**, select **Anonymous** for **Access Rights**, and click **Create**.</span></span> <span data-ttu-id="a7d81-122">Созданная функция доступна для HTTP-запроса из любого клиента.</span><span class="sxs-lookup"><span data-stu-id="a7d81-122">The function created is accessed by an HTTP request from any client.</span></span> 

    ![Создание функции Azure](./media/functions-create-your-first-function-visual-studio/functions-vstools-add-new-function-2.png)

    <span data-ttu-id="a7d81-124">Файл кода добавляется в проект, который содержит класс, реализующий код функции.</span><span class="sxs-lookup"><span data-stu-id="a7d81-124">A code file is added to your project that contains a class that implements your function code.</span></span> <span data-ttu-id="a7d81-125">Этот код основан на шаблоне, который получает значение имени и выводит сведения о нем.</span><span class="sxs-lookup"><span data-stu-id="a7d81-125">This code is based on a template, which receives a name value and echos it back.</span></span> <span data-ttu-id="a7d81-126">Атрибут **FunctionName** задает имя функции.</span><span class="sxs-lookup"><span data-stu-id="a7d81-126">The **FunctionName** attribute sets the name of your function.</span></span> <span data-ttu-id="a7d81-127">Атрибут **HttpTrigger** указывает сообщение, которое активирует функцию.</span><span class="sxs-lookup"><span data-stu-id="a7d81-127">The **HttpTrigger** attribute indicates the message that triggers the function.</span></span> 

    ![Файл кода функции](./media/functions-create-your-first-function-visual-studio/functions-code-page.png)

<span data-ttu-id="a7d81-129">Созданную функцию, активируемую HTTP, можно протестировать на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="a7d81-129">Now that you have created an HTTP-triggered function, you can test it on your local computer.</span></span>

## <a name="test-the-function-locally"></a><span data-ttu-id="a7d81-130">Локальное тестирование функции</span><span class="sxs-lookup"><span data-stu-id="a7d81-130">Test the function locally</span></span>

<span data-ttu-id="a7d81-131">Основные инструменты службы Функции Azure позволяют запускать проекты функций Azure на локальном компьютере разработчика.</span><span class="sxs-lookup"><span data-stu-id="a7d81-131">Azure Functions Core Tools lets you run Azure Functions project on your local development computer.</span></span> <span data-ttu-id="a7d81-132">Вам будет предложено установить эти инструменты при первом запуске функции из Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a7d81-132">You are prompted to install these tools the first time you start a function from Visual Studio.</span></span>  

1. <span data-ttu-id="a7d81-133">Чтобы проверить работу функции, нажмите клавишу F5.</span><span class="sxs-lookup"><span data-stu-id="a7d81-133">To test your function, press F5.</span></span> <span data-ttu-id="a7d81-134">Если будет предложено, примите запрос от Visual Studio на скачивание и установку основных инструментов службы Функции Azure (CLI).</span><span class="sxs-lookup"><span data-stu-id="a7d81-134">If prompted, accept the request from Visual Studio to download and install Azure Functions Core (CLI) tools.</span></span>  <span data-ttu-id="a7d81-135">Кроме того, вам может понадобиться включить исключение брандмауэра, чтобы инструменты могли обрабатывать HTTP-запросы.</span><span class="sxs-lookup"><span data-stu-id="a7d81-135">You may also need to enable a firewall exception so that the tools can handle HTTP requests.</span></span>

2. <span data-ttu-id="a7d81-136">Скопируйте URL-адрес функции из выходных данных среды выполнения функций Azure.</span><span class="sxs-lookup"><span data-stu-id="a7d81-136">Copy the URL of your function from the Azure Functions runtime output.</span></span>  

    ![Локальная среда выполнения Azure](./media/functions-create-your-first-function-visual-studio/functions-vstools-f5.png)

3. <span data-ttu-id="a7d81-138">Вставьте URL-адрес запроса в адресную строку браузера.</span><span class="sxs-lookup"><span data-stu-id="a7d81-138">Paste the URL for the HTTP request into your browser's address bar.</span></span> <span data-ttu-id="a7d81-139">Добавьте строку запроса `&name=<yourname>` в этот URL-адрес и выполните запрос.</span><span class="sxs-lookup"><span data-stu-id="a7d81-139">Append the query string `&name=<yourname>` to this URL and execute the request.</span></span> <span data-ttu-id="a7d81-140">Ниже показан ответ в браузере на локальный запрос GET, возвращаемый функцией:</span><span class="sxs-lookup"><span data-stu-id="a7d81-140">The following shows the response in the browser to the local GET request returned by the function:</span></span> 

    ![Ответ функции localhost в браузере](./media/functions-create-your-first-function-visual-studio/functions-test-local-browser.png)

4. <span data-ttu-id="a7d81-142">Чтобы остановить отладку, нажмите кнопку **Остановить** на панели инструментов Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a7d81-142">To stop debugging, click the **Stop** button on the Visual Studio toolbar.</span></span>

<span data-ttu-id="a7d81-143">Убедитесь, что функция правильно работает на локальном компьютере. Затем опубликуйте проект в Azure.</span><span class="sxs-lookup"><span data-stu-id="a7d81-143">After you have verified that the function runs correctly on your local computer, it's time to publish the project to Azure.</span></span>

## <a name="publish-the-project-to-azure"></a><span data-ttu-id="a7d81-144">Публикация проекта в Azure</span><span class="sxs-lookup"><span data-stu-id="a7d81-144">Publish the project to Azure</span></span>

<span data-ttu-id="a7d81-145">Перед публикацией проекта убедитесь, что в вашей подписке Azure есть приложения-функция.</span><span class="sxs-lookup"><span data-stu-id="a7d81-145">You must have a function app in your Azure subscription before you can publish your project.</span></span> <span data-ttu-id="a7d81-146">Можно создать приложение-функцию непосредственно в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a7d81-146">You can create a function app right from Visual Studio.</span></span>

[!INCLUDE [Publish the project to Azure](../../includes/functions-vstools-publish.md)]

## <a name="test-your-function-in-azure"></a><span data-ttu-id="a7d81-147">Тестирование функции в Azure</span><span class="sxs-lookup"><span data-stu-id="a7d81-147">Test your function in Azure</span></span>

1. <span data-ttu-id="a7d81-148">Скопируйте базовый URL-адрес приложения-функции на странице профиля публикации.</span><span class="sxs-lookup"><span data-stu-id="a7d81-148">Copy the base URL of the function app from the Publish profile page.</span></span> <span data-ttu-id="a7d81-149">Замените часть `localhost:port` URL-адреса, который использовался при локальной проверке функции новым базовым URL-адресом.</span><span class="sxs-lookup"><span data-stu-id="a7d81-149">Replace the `localhost:port` portion of the URL you used when testing the function locally with the new base URL.</span></span> <span data-ttu-id="a7d81-150">Как и ранее, добавьте строку запроса `&name=<yourname>` в этот URL-адрес и выполните запрос.</span><span class="sxs-lookup"><span data-stu-id="a7d81-150">As before, make sure to append the query string `&name=<yourname>` to this URL and execute the request.</span></span>

    <span data-ttu-id="a7d81-151">URL-адрес, который вызывает функцию, активируемую HTTP, выглядит так:</span><span class="sxs-lookup"><span data-stu-id="a7d81-151">The URL that calls your HTTP triggered function looks like this:</span></span>

        http://<functionappname>.azurewebsites.net/api/<functionname>?name=<yourname> 

2. <span data-ttu-id="a7d81-152">Вставьте этот URL-адрес HTTP-запроса в адресную строку браузера.</span><span class="sxs-lookup"><span data-stu-id="a7d81-152">Paste this new URL for the HTTP request into your browser's address bar.</span></span> <span data-ttu-id="a7d81-153">Ниже показан ответ в браузере на удаленный запрос GET, возвращаемый функцией:</span><span class="sxs-lookup"><span data-stu-id="a7d81-153">The following shows the response in the browser to the remote GET request returned by the function:</span></span> 

    ![Ответ функции в браузере](./media/functions-create-your-first-function-visual-studio/functions-test-remote-browser.png)
 
## <a name="next-steps"></a><span data-ttu-id="a7d81-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a7d81-155">Next steps</span></span>

<span data-ttu-id="a7d81-156">С помощью Visual Studio вы создали приложение-функцию C# с простой функцией, активируемой HTTP.</span><span class="sxs-lookup"><span data-stu-id="a7d81-156">You have used Visual Studio to create a C# function app with a simple HTTP triggered function.</span></span> 

+ <span data-ttu-id="a7d81-157">Дополнительные сведения о настройке проекта для поддержки других типов триггеров и привязок см. в разделе [Настройка проекта для локальной разработки](functions-develop-vs.md#configure-the-project-for-local-development) в статье [Инструменты Функций Azure для Visual Studio](functions-develop-vs.md).</span><span class="sxs-lookup"><span data-stu-id="a7d81-157">To learn how to configure your project to support other types of triggers and bindings, see the [Configure the project for local development](functions-develop-vs.md#configure-the-project-for-local-development) section in [Azure Functions Tools for Visual Studio](functions-develop-vs.md).</span></span>
+ <span data-ttu-id="a7d81-158">Дополнительные сведения о локальном тестировании и отладке с помощью основных инструментов функций Azure см. в статье [Как программировать и тестировать функции Azure в локальной среде](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="a7d81-158">To learn more about local testing and debugging using the Azure Functions Core Tools, see [Code and test Azure Functions locally](functions-run-local.md).</span></span> 
+ <span data-ttu-id="a7d81-159">Дополнительные сведения о разработке функций, таких как библиотек классов .NET, см. в статье [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md) (Использование библиотек классов .NET с помощью Функций Azure).</span><span class="sxs-lookup"><span data-stu-id="a7d81-159">To learn more about developing functions as .NET class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span> 

