---
title: "aaaCreate первой функции в Azure с помощью Visual Studio | Документы Microsoft"
description: "Создание и публикация простой tooAzure функции активации HTTP с помощью функции средств Azure для Visual Studio."
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
ms.openlocfilehash: 851e5b98dcc2da00334620896a0ea31f566589f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-using-visual-studio"></a><span data-ttu-id="e0497-104">Создание первой функции с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e0497-104">Create your first function using Visual Studio</span></span>

<span data-ttu-id="e0497-105">Функции Azure позволяет выполнять код в среде без сервера без необходимости toofirst создания виртуальной Машины или публикации веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="e0497-105">Azure Functions lets you execute your code in a serverless environment without having toofirst create a VM or publish a web application.</span></span>

<span data-ttu-id="e0497-106">В этом разделе вы узнаете, как toouse hello 2017 г. Visual Studio tools для функций Azure toocreate и тестов локально функцию «hello world».</span><span class="sxs-lookup"><span data-stu-id="e0497-106">In this topic, you learn how toouse hello Visual Studio 2017 tools for Azure Functions toocreate and test a "hello world" function locally.</span></span> <span data-ttu-id="e0497-107">Затем вы публикуете tooAzure кода функции hello.</span><span class="sxs-lookup"><span data-stu-id="e0497-107">You will then publish hello function code tooAzure.</span></span> <span data-ttu-id="e0497-108">Эти средства доступны как часть рабочей нагрузки разработки Azure hello в Visual Studio 2017 г. версия 15,3 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="e0497-108">These tools are available as part of hello Azure development workload in Visual Studio 2017 version 15.3, or a later version.</span></span>

![Код функций Azure в проекте Visual Studio](./media/functions-create-your-first-function-visual-studio/functions-vstools-intro.png)

## <a name="prerequisites"></a><span data-ttu-id="e0497-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e0497-110">Prerequisites</span></span>

<span data-ttu-id="e0497-111">toocomplete учебника, установки:</span><span class="sxs-lookup"><span data-stu-id="e0497-111">toocomplete this tutorial, install:</span></span>

* <span data-ttu-id="e0497-112">[Visual Studio 2017 г. версия 15,3](https://www.visualstudio.com/vs/preview/), включая hello **разработки Azure** рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="e0497-112">[Visual Studio 2017 version 15.3](https://www.visualstudio.com/vs/preview/), including hello **Azure development** workload.</span></span>

    ![Установка Visual Studio 2017 г. с помощью рабочей нагрузки для разработки Azure hello](./media/functions-create-your-first-function-visual-studio/functions-vs-workloads.png)
    
    >[!NOTE]  
    <span data-ttu-id="e0497-114">После установки или обновления tooVisual Studio 2017 г. версия 15,3, необходимо также toomanually обновления hello 2017 г. Visual Studio tools для функций Azure.</span><span class="sxs-lookup"><span data-stu-id="e0497-114">After you install or upgrade tooVisual Studio 2017 version 15.3, you might also need toomanually update hello Visual Studio 2017 tools for Azure Functions.</span></span> <span data-ttu-id="e0497-115">Можно обновить средства hello из hello **средства** меню в разделе **расширения и обновления...**   >  **Обновления** > **Visual Studio Marketplace** > **функций Azure и веб-задания средства**  >  **Обновление**.</span><span class="sxs-lookup"><span data-stu-id="e0497-115">You can update hello tools from hello **Tools** menu under **Extensions and Updates...** > **Updates** > **Visual Studio Marketplace** > **Azure Functions and Web Jobs Tools** > **Update**.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] 

## <a name="create-an-azure-functions-project-in-visual-studio"></a><span data-ttu-id="e0497-116">Создание проекта функций Azure в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e0497-116">Create an Azure Functions project in Visual Studio</span></span>

[!INCLUDE [Create a project using hello Azure Functions template](../../includes/functions-vstools-create.md)]

<span data-ttu-id="e0497-117">После создания проекта hello созданием первой функции.</span><span class="sxs-lookup"><span data-stu-id="e0497-117">Now that you have created hello project, you can create your first function.</span></span>

## <a name="create-hello-function"></a><span data-ttu-id="e0497-118">Создание функции hello</span><span class="sxs-lookup"><span data-stu-id="e0497-118">Create hello function</span></span>

1. <span data-ttu-id="e0497-119">Щелкните правой кнопкой мыши узел проекта в **обозревателе решений** и выберите **Добавить** > **Новый элемент**.</span><span class="sxs-lookup"><span data-stu-id="e0497-119">In **Solution Explorer**, right-click on your project node and select **Add** > **New Item**.</span></span> <span data-ttu-id="e0497-120">Выберите **Функция Azure** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e0497-120">Select **Azure Function** and click **Add**.</span></span>

2. <span data-ttu-id="e0497-121">Выберите **HttpTrigger**, укажите **имя функции**, выберите для параметра **Права доступа** значение **Анонимно** и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e0497-121">Select **HttpTrigger**, type a **Function Name**, select **Anonymous** for **Access Rights**, and click **Create**.</span></span> <span data-ttu-id="e0497-122">Hello функция, созданная осуществляется с помощью запроса HTTP из любого клиента.</span><span class="sxs-lookup"><span data-stu-id="e0497-122">hello function created is accessed by an HTTP request from any client.</span></span> 

    ![Создание функции Azure](./media/functions-create-your-first-function-visual-studio/functions-vstools-add-new-function-2.png)

    <span data-ttu-id="e0497-124">Файл кода добавляется tooyour проект, содержащий класс, реализующий кода функции.</span><span class="sxs-lookup"><span data-stu-id="e0497-124">A code file is added tooyour project that contains a class that implements your function code.</span></span> <span data-ttu-id="e0497-125">Этот код основан на шаблоне, который получает значение имени и выводит сведения о нем.</span><span class="sxs-lookup"><span data-stu-id="e0497-125">This code is based on a template, which receives a name value and echos it back.</span></span> <span data-ttu-id="e0497-126">Hello **FunctionName** атрибута задает имя функции hello.</span><span class="sxs-lookup"><span data-stu-id="e0497-126">hello **FunctionName** attribute sets hello name of your function.</span></span> <span data-ttu-id="e0497-127">Hello **HttpTrigger** атрибут указывает на приветственное сообщение, которое вызывает функции hello.</span><span class="sxs-lookup"><span data-stu-id="e0497-127">hello **HttpTrigger** attribute indicates hello message that triggers hello function.</span></span> 

    ![Файл кода функции](./media/functions-create-your-first-function-visual-studio/functions-code-page.png)

<span data-ttu-id="e0497-129">Созданную функцию, активируемую HTTP, можно протестировать на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="e0497-129">Now that you have created an HTTP-triggered function, you can test it on your local computer.</span></span>

## <a name="test-hello-function-locally"></a><span data-ttu-id="e0497-130">Проверка функции hello локально</span><span class="sxs-lookup"><span data-stu-id="e0497-130">Test hello function locally</span></span>

<span data-ttu-id="e0497-131">Основные инструменты службы Функции Azure позволяют запускать проекты функций Azure на локальном компьютере разработчика.</span><span class="sxs-lookup"><span data-stu-id="e0497-131">Azure Functions Core Tools lets you run Azure Functions project on your local development computer.</span></span> <span data-ttu-id="e0497-132">Все запрашиваемые tooinstall, эти средства hello первом запуске функции из Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e0497-132">You are prompted tooinstall these tools hello first time you start a function from Visual Studio.</span></span>  

1. <span data-ttu-id="e0497-133">tootest работу, нажмите клавишу F5.</span><span class="sxs-lookup"><span data-stu-id="e0497-133">tootest your function, press F5.</span></span> <span data-ttu-id="e0497-134">При необходимости принятия запроса hello из Visual Studio toodownload и установить средства основных функций Azure (CLI).</span><span class="sxs-lookup"><span data-stu-id="e0497-134">If prompted, accept hello request from Visual Studio toodownload and install Azure Functions Core (CLI) tools.</span></span>  <span data-ttu-id="e0497-135">Может также потребоваться tooenable исключение брандмауэра, чтобы средства hello можно обрабатывать HTTP-запросы.</span><span class="sxs-lookup"><span data-stu-id="e0497-135">You may also need tooenable a firewall exception so that hello tools can handle HTTP requests.</span></span>

2. <span data-ttu-id="e0497-136">Копировать URL-адрес hello этой функции из среды выполнения Azure функции hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="e0497-136">Copy hello URL of your function from hello Azure Functions runtime output.</span></span>  

    ![Локальная среда выполнения Azure](./media/functions-create-your-first-function-visual-studio/functions-vstools-f5.png)

3. <span data-ttu-id="e0497-138">Вставьте hello URL-адрес для hello HTTP-запроса в адресной строке браузера.</span><span class="sxs-lookup"><span data-stu-id="e0497-138">Paste hello URL for hello HTTP request into your browser's address bar.</span></span> <span data-ttu-id="e0497-139">Добавить строку hello запроса `&name=<yourname>` toothis URL-адрес и выполнения запроса hello.</span><span class="sxs-lookup"><span data-stu-id="e0497-139">Append hello query string `&name=<yourname>` toothis URL and execute hello request.</span></span> <span data-ttu-id="e0497-140">Hello ниже показан ответ hello в hello браузера toohello локального запроса GET возвращается функцией hello:</span><span class="sxs-lookup"><span data-stu-id="e0497-140">hello following shows hello response in hello browser toohello local GET request returned by hello function:</span></span> 

    ![Функция localhost ответа в браузер hello](./media/functions-create-your-first-function-visual-studio/functions-test-local-browser.png)

4. <span data-ttu-id="e0497-142">отладка, toostop щелкните hello **остановить** на hello инструментов Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e0497-142">toostop debugging, click hello **Stop** button on hello Visual Studio toolbar.</span></span>

<span data-ttu-id="e0497-143">После проверки того, что функции hello работает правильно на локальном компьютере, это время toopublish hello проекта tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e0497-143">After you have verified that hello function runs correctly on your local computer, it's time toopublish hello project tooAzure.</span></span>

## <a name="publish-hello-project-tooazure"></a><span data-ttu-id="e0497-144">Публикация проекта tooAzure hello</span><span class="sxs-lookup"><span data-stu-id="e0497-144">Publish hello project tooAzure</span></span>

<span data-ttu-id="e0497-145">Перед публикацией проекта убедитесь, что в вашей подписке Azure есть приложения-функция.</span><span class="sxs-lookup"><span data-stu-id="e0497-145">You must have a function app in your Azure subscription before you can publish your project.</span></span> <span data-ttu-id="e0497-146">Можно создать приложение-функцию непосредственно в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e0497-146">You can create a function app right from Visual Studio.</span></span>

[!INCLUDE [Publish hello project tooAzure](../../includes/functions-vstools-publish.md)]

## <a name="test-your-function-in-azure"></a><span data-ttu-id="e0497-147">Тестирование функции в Azure</span><span class="sxs-lookup"><span data-stu-id="e0497-147">Test your function in Azure</span></span>

1. <span data-ttu-id="e0497-148">Скопируйте hello базовый URL-адрес приложения hello функции из hello страницу профиля публикации.</span><span class="sxs-lookup"><span data-stu-id="e0497-148">Copy hello base URL of hello function app from hello Publish profile page.</span></span> <span data-ttu-id="e0497-149">Замените hello `localhost:port` часть hello URL-адреса, используемые при проверке функции hello локально с hello новый базовый URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="e0497-149">Replace hello `localhost:port` portion of hello URL you used when testing hello function locally with hello new base URL.</span></span> <span data-ttu-id="e0497-150">Как и раньше, убедитесь, что строка запроса hello tooappend `&name=<yourname>` toothis URL-адрес и выполнения запроса hello.</span><span class="sxs-lookup"><span data-stu-id="e0497-150">As before, make sure tooappend hello query string `&name=<yourname>` toothis URL and execute hello request.</span></span>

    <span data-ttu-id="e0497-151">Hello URL-адрес, который вызывает HTTP запуска функции выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e0497-151">hello URL that calls your HTTP triggered function looks like this:</span></span>

        http://<functionappname>.azurewebsites.net/api/<functionname>?name=<yourname> 

2. <span data-ttu-id="e0497-152">Вставьте этот новый URL-адрес для hello HTTP-запроса в адресной строке браузера.</span><span class="sxs-lookup"><span data-stu-id="e0497-152">Paste this new URL for hello HTTP request into your browser's address bar.</span></span> <span data-ttu-id="e0497-153">Hello ниже показан ответ hello в hello браузера toohello удаленного запроса GET возвращается функцией hello:</span><span class="sxs-lookup"><span data-stu-id="e0497-153">hello following shows hello response in hello browser toohello remote GET request returned by hello function:</span></span> 

    ![Функция ответа в браузер hello](./media/functions-create-your-first-function-visual-studio/functions-test-remote-browser.png)
 
## <a name="next-steps"></a><span data-ttu-id="e0497-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e0497-155">Next steps</span></span>

<span data-ttu-id="e0497-156">Вы использовали функции приложения Visual Studio toocreate C# для простой функции активации HTTP.</span><span class="sxs-lookup"><span data-stu-id="e0497-156">You have used Visual Studio toocreate a C# function app with a simple HTTP triggered function.</span></span> 

+ <span data-ttu-id="e0497-157">toolearn как tooconfigure ваш проект toosupport других типов триггеров и привязок, в разделе hello [Настройка hello проекта для локальной разработки](functions-develop-vs.md#configure-the-project-for-local-development) статьи [функции средства Azure для Visual Studio](functions-develop-vs.md).</span><span class="sxs-lookup"><span data-stu-id="e0497-157">toolearn how tooconfigure your project toosupport other types of triggers and bindings, see hello [Configure hello project for local development](functions-develop-vs.md#configure-the-project-for-local-development) section in [Azure Functions Tools for Visual Studio](functions-develop-vs.md).</span></span>
+ <span data-ttu-id="e0497-158">toolearn Дополнительные сведения о локального тестирования и отладки с помощью средства основных функций hello Azure, в разделе [кода и тестов функции Azure локально](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="e0497-158">toolearn more about local testing and debugging using hello Azure Functions Core Tools, see [Code and test Azure Functions locally](functions-run-local.md).</span></span> 
+ <span data-ttu-id="e0497-159">toolearn Дополнительные сведения о разработке функции как библиотеки классов .NET, в разделе [библиотеки классов с помощью .NET с помощью функций Azure](functions-dotnet-class-library.md).</span><span class="sxs-lookup"><span data-stu-id="e0497-159">toolearn more about developing functions as .NET class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span> 

