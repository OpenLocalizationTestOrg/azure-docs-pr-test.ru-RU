---
title: "Создание первой функции на портале Azure | Документация Майкрософт"
description: "Узнайте, как создать первую функцию Azure, выполняемую без сервера, с помощью портала Azure."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 96cf87b9-8db6-41a8-863a-abb828e3d06d
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/07/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 3ec1f278f21d89782137625aff200f07f15fd9fb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-function-in-the-azure-portal"></a><span data-ttu-id="732fc-103">Создание первой функции на портале Azure</span><span class="sxs-lookup"><span data-stu-id="732fc-103">Create your first function in the Azure portal</span></span>

<span data-ttu-id="732fc-104">Функции Azure позволяют вам выполнять свой код в бессерверной среде без необходимости создавать виртуальную машину или публиковать веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="732fc-104">Azure Functions lets you execute your code in a serverless environment without having to first create a VM or publish a web application.</span></span> <span data-ttu-id="732fc-105">В этой статье вы узнаете, как создать функцию Hello World на портале Azure с помощью Функций.</span><span class="sxs-lookup"><span data-stu-id="732fc-105">In this topic, learn how to use Functions to create a "hello world" function in the Azure portal.</span></span>

![Создание приложения-функции на портале Azure](./media/functions-create-first-azure-function/function-app-in-portal-editor.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="log-in-to-azure"></a><span data-ttu-id="732fc-107">Вход в Azure</span><span class="sxs-lookup"><span data-stu-id="732fc-107">Log in to Azure</span></span>

<span data-ttu-id="732fc-108">Войдите на [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="732fc-108">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="732fc-109">Создание приложения-функции</span><span class="sxs-lookup"><span data-stu-id="732fc-109">Create a function app</span></span>

<span data-ttu-id="732fc-110">Для выполнения функций вам понадобится приложение-функция,</span><span class="sxs-lookup"><span data-stu-id="732fc-110">You must have a function app to host the execution of your functions.</span></span> <span data-ttu-id="732fc-111">позволяющее группировать функции в логические единицы и упростить развертывание и совместное использование ресурсов, а также управление ими.</span><span class="sxs-lookup"><span data-stu-id="732fc-111">A function app lets you group functions as a logic unit for easier management, deployment, and sharing of resources.</span></span> 

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

<span data-ttu-id="732fc-112">Затем создайте функцию в новом приложении-функции.</span><span class="sxs-lookup"><span data-stu-id="732fc-112">Next, you create a function in the new function app.</span></span>

## <span data-ttu-id="732fc-113"><a name="create-function"></a>Создание функции, активируемой HTTP</span><span class="sxs-lookup"><span data-stu-id="732fc-113"><a name="create-function"></a>Create an HTTP triggered function</span></span>

1. <span data-ttu-id="732fc-114">Разверните новое приложение-функцию, нажмите кнопку **+** рядом с **Функции**.</span><span class="sxs-lookup"><span data-stu-id="732fc-114">Expand your new function app, then click the **+** button next to **Functions**.</span></span>

2.  <span data-ttu-id="732fc-115">На странице **быстрого начала работы** щелкните **Веб-перехватчик + API**, **выберите язык для функции** и щелкните **Создать функцию**.</span><span class="sxs-lookup"><span data-stu-id="732fc-115">In the **Get started quickly** page, select **WebHook + API**, **Choose a language** for your function, and click **Create this function**.</span></span> 
   
    ![Быстрое начало работы с Функциями на портале Azure.](./media/functions-create-first-azure-function/function-app-quickstart-node-webhook.png)

<span data-ttu-id="732fc-117">С помощью шаблона функции, активируемой HTTP, будет создана функция на выбранном вами языке.</span><span class="sxs-lookup"><span data-stu-id="732fc-117">A function is created in your chosen language using the template for an HTTP triggered function.</span></span> <span data-ttu-id="732fc-118">Вы можете запустить новую функцию, отправив HTTP-запрос.</span><span class="sxs-lookup"><span data-stu-id="732fc-118">You can run the new function by sending an HTTP request.</span></span>

## <a name="test-the-function"></a><span data-ttu-id="732fc-119">Проверка функции</span><span class="sxs-lookup"><span data-stu-id="732fc-119">Test the function</span></span>

1. <span data-ttu-id="732fc-120">В новой функции щелкните **</> Получить URL-адрес функции**, выберите **По умолчанию (ключ функции)**и нажмите кнопку **Копировать**.</span><span class="sxs-lookup"><span data-stu-id="732fc-120">In your new function, click **</> Get function URL**, select **default (Function key)**, and then click **Copy**.</span></span> 

    ![Копирование URL-адреса функции с портала Azure](./media/functions-create-first-azure-function/function-app-develop-tab-testing.png)

2. <span data-ttu-id="732fc-122">Вставьте URL-адрес функции в адресную строку браузера.</span><span class="sxs-lookup"><span data-stu-id="732fc-122">Paste the function URL into your browser's address bar.</span></span> <span data-ttu-id="732fc-123">Добавьте строку запроса `&name=<yourname>` в этот URL-адрес и нажмите клавишу `Enter` на клавиатуре, чтобы выполнить этот запрос.</span><span class="sxs-lookup"><span data-stu-id="732fc-123">Append the query string `&name=<yourname>` to this URL and press the `Enter` key on your keyboard to execute the request.</span></span> <span data-ttu-id="732fc-124">Ниже приведен пример ответа, возвращаемого функцией в браузере Edge:</span><span class="sxs-lookup"><span data-stu-id="732fc-124">The following is an example of the response returned by the function in the Edge browser:</span></span>

    ![Ответ функции в браузере.](./media/functions-create-first-azure-function/function-app-browser-testing.png)

    <span data-ttu-id="732fc-126">URL-адрес запроса включает ключ, который по умолчанию необходим для доступа к функции по протоколу HTTP.</span><span class="sxs-lookup"><span data-stu-id="732fc-126">The request URL includes a key that is required, by default, to access your function over HTTP.</span></span>   

3. <span data-ttu-id="732fc-127">При выполнении функции сведения о трассировке записываются в журналы.</span><span class="sxs-lookup"><span data-stu-id="732fc-127">When your function runs, trace information is written to the logs.</span></span> <span data-ttu-id="732fc-128">Для просмотра выходных данных трассировки из предыдущего выполнения вернитесь к своей функции на портале и щелкните стрелку вверх в нижней части экрана, чтобы развернуть **Журналы**.</span><span class="sxs-lookup"><span data-stu-id="732fc-128">To see the trace output from the previous execution, return to your function in the portal and click the up arrow at the bottom of the screen to expand **Logs**.</span></span> 

   ![Средство просмотра журналов Функций на портале Azure.](./media/functions-create-first-azure-function/function-view-logs.png)

## <a name="clean-up-resources"></a><span data-ttu-id="732fc-130">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="732fc-130">Clean up resources</span></span>

[!INCLUDE [Clean up resources](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="732fc-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="732fc-131">Next steps</span></span>

<span data-ttu-id="732fc-132">Вы создали приложение-функцию с простой функцией, активируемой HTTP.</span><span class="sxs-lookup"><span data-stu-id="732fc-132">You have created a function app with a simple HTTP triggered function.</span></span>  

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="732fc-133">Дополнительные сведения см. в статье [Привязки HTTP и webhook в функциях Azure](functions-bindings-http-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="732fc-133">For more information, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span>



