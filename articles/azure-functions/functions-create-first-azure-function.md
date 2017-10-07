---
title: "aaaCreate функции первого из hello портал Azure | Документы Microsoft"
description: "Узнайте, как первый Azure функции для выполнения без сервера с помощью toocreate hello портал Azure."
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
ms.openlocfilehash: 84283d7d4bc6015061946af4589f9a70ae61f36b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-in-hello-azure-portal"></a><span data-ttu-id="178c8-103">Создание первой функции в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="178c8-103">Create your first function in hello Azure portal</span></span>

<span data-ttu-id="178c8-104">Функции Azure позволяет выполнять код в среде без сервера без необходимости toofirst создания виртуальной Машины или публикации веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="178c8-104">Azure Functions lets you execute your code in a serverless environment without having toofirst create a VM or publish a web application.</span></span> <span data-ttu-id="178c8-105">В этом разделе рассказано, как toouse функционирует toocreate функции «hello world» в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="178c8-105">In this topic, learn how toouse Functions toocreate a "hello world" function in hello Azure portal.</span></span>

![Создание функции приложения в hello портал Azure](./media/functions-create-first-azure-function/function-app-in-portal-editor.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="log-in-tooazure"></a><span data-ttu-id="178c8-107">Войдите в tooAzure</span><span class="sxs-lookup"><span data-stu-id="178c8-107">Log in tooAzure</span></span>

<span data-ttu-id="178c8-108">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="178c8-108">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="178c8-109">Создание приложения-функции</span><span class="sxs-lookup"><span data-stu-id="178c8-109">Create a function app</span></span>

<span data-ttu-id="178c8-110">Требуется выполнение функции приложения toohost hello функций.</span><span class="sxs-lookup"><span data-stu-id="178c8-110">You must have a function app toohost hello execution of your functions.</span></span> <span data-ttu-id="178c8-111">позволяющее группировать функции в логические единицы и упростить развертывание и совместное использование ресурсов, а также управление ими.</span><span class="sxs-lookup"><span data-stu-id="178c8-111">A function app lets you group functions as a logic unit for easier management, deployment, and sharing of resources.</span></span> 

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

<span data-ttu-id="178c8-112">Создайте функцию в приложение новые функции hello.</span><span class="sxs-lookup"><span data-stu-id="178c8-112">Next, you create a function in hello new function app.</span></span>

## <span data-ttu-id="178c8-113"><a name="create-function"></a>Создание функции, активируемой HTTP</span><span class="sxs-lookup"><span data-stu-id="178c8-113"><a name="create-function"></a>Create an HTTP triggered function</span></span>

1. <span data-ttu-id="178c8-114">Разверните приложение новые функции, а затем щелкните hello  **+**  рядом слишком**функции**.</span><span class="sxs-lookup"><span data-stu-id="178c8-114">Expand your new function app, then click hello **+** button next too**Functions**.</span></span>

2.  <span data-ttu-id="178c8-115">В hello **быстро приступить к работе** выберите **веб-перехватчика + API**, **выбрать язык** функции, а затем щелкните **создания этой функции** .</span><span class="sxs-lookup"><span data-stu-id="178c8-115">In hello **Get started quickly** page, select **WebHook + API**, **Choose a language** for your function, and click **Create this function**.</span></span> 
   
    ![Примеры использования функций в hello портал Azure.](./media/functions-create-first-azure-function/function-app-quickstart-node-webhook.png)

<span data-ttu-id="178c8-117">Функция создается в выбранный язык с помощью шаблона hello для функции активации HTTP.</span><span class="sxs-lookup"><span data-stu-id="178c8-117">A function is created in your chosen language using hello template for an HTTP triggered function.</span></span> <span data-ttu-id="178c8-118">Можно запустить новые функции hello, отправив запрос HTTP.</span><span class="sxs-lookup"><span data-stu-id="178c8-118">You can run hello new function by sending an HTTP request.</span></span>

## <a name="test-hello-function"></a><span data-ttu-id="178c8-119">Проверка функции hello</span><span class="sxs-lookup"><span data-stu-id="178c8-119">Test hello function</span></span>

1. <span data-ttu-id="178c8-120">В новой функции щелкните **</> Получить URL-адрес функции**, выберите **По умолчанию (ключ функции)**и нажмите кнопку **Копировать**.</span><span class="sxs-lookup"><span data-stu-id="178c8-120">In your new function, click **</> Get function URL**, select **default (Function key)**, and then click **Copy**.</span></span> 

    ![Скопируйте URL-адрес функции hello из hello портал Azure](./media/functions-create-first-azure-function/function-app-develop-tab-testing.png)

2. <span data-ttu-id="178c8-122">Вставьте URL-адрес функции hello в адресной строке браузера.</span><span class="sxs-lookup"><span data-stu-id="178c8-122">Paste hello function URL into your browser's address bar.</span></span> <span data-ttu-id="178c8-123">Добавить строку hello запроса `&name=<yourname>` toothis hello URL-адрес и нажмите клавишу `Enter` ключа запроса hello tooexecute клавиатуры.</span><span class="sxs-lookup"><span data-stu-id="178c8-123">Append hello query string `&name=<yourname>` toothis URL and press hello `Enter` key on your keyboard tooexecute hello request.</span></span> <span data-ttu-id="178c8-124">Hello ниже приведен пример hello ответ, возвращаемый функцией "hello" в браузере Edge hello:</span><span class="sxs-lookup"><span data-stu-id="178c8-124">hello following is an example of hello response returned by hello function in hello Edge browser:</span></span>

    ![Функция ответа в браузер hello.](./media/functions-create-first-azure-function/function-app-browser-testing.png)

    <span data-ttu-id="178c8-126">URL-адрес содержит ключ, который требуется, по умолчанию tooaccess запрос Hello работу по протоколу HTTP.</span><span class="sxs-lookup"><span data-stu-id="178c8-126">hello request URL includes a key that is required, by default, tooaccess your function over HTTP.</span></span>   

3. <span data-ttu-id="178c8-127">При выполнении функции сведения трассировки записываются журналы toohello.</span><span class="sxs-lookup"><span data-stu-id="178c8-127">When your function runs, trace information is written toohello logs.</span></span> <span data-ttu-id="178c8-128">выходные данные трассировки hello toosee из предыдущего выполнения hello, вернитесь tooyour функции hello портала и нажмите кнопку hello стрелкой hello нижней части экрана tooexpand hello **журналы**.</span><span class="sxs-lookup"><span data-stu-id="178c8-128">toosee hello trace output from hello previous execution, return tooyour function in hello portal and click hello up arrow at hello bottom of hello screen tooexpand **Logs**.</span></span> 

   ![Функции просмотра журнала в hello портал Azure.](./media/functions-create-first-azure-function/function-view-logs.png)

## <a name="clean-up-resources"></a><span data-ttu-id="178c8-130">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="178c8-130">Clean up resources</span></span>

[!INCLUDE [Clean up resources](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="178c8-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="178c8-131">Next steps</span></span>

<span data-ttu-id="178c8-132">Вы создали приложение-функцию с простой функцией, активируемой HTTP.</span><span class="sxs-lookup"><span data-stu-id="178c8-132">You have created a function app with a simple HTTP triggered function.</span></span>  

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="178c8-133">Дополнительные сведения см. в статье [Привязки HTTP и webhook в функциях Azure](functions-bindings-http-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="178c8-133">For more information, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span>



