---
title: "функция в Azure, активируемых веб-перехватчика GitHub aaaCreate | Документы Microsoft"
description: "Используйте функции Azure toocreate без сервера функция, вызываемая веб-перехватчика GitHub."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 36ef34b8-3729-4940-86d2-cb8e176fcc06
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 8ffcde82c9310d749159ed53eab113658e38a030
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-a-github-webhook"></a><span data-ttu-id="4729d-103">Создание функции, активируемой объектом webhook GitHub</span><span class="sxs-lookup"><span data-stu-id="4729d-103">Create a function triggered by a GitHub webhook</span></span>

<span data-ttu-id="4729d-104">Узнайте, как toocreate функцию, которая инициируется с полезными данными GitHub конкретного веб-перехватчика HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="4729d-104">Learn how toocreate a function that is triggered by an HTTP webhook request with a GitHub-specific payload.</span></span>

![Веб-перехватчика Github активации функции hello портал Azure](./media/functions-create-github-webhook-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="4729d-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4729d-106">Prerequisites</span></span>

+ <span data-ttu-id="4729d-107">Учетная запись GitHub с хотя бы одним проектом.</span><span class="sxs-lookup"><span data-stu-id="4729d-107">A GitHub account with at least one project.</span></span>
+ <span data-ttu-id="4729d-108">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="4729d-108">An Azure subscription.</span></span> <span data-ttu-id="4729d-109">Если у вас еще нет подписки Azure, создайте [бесплатную учетную запись](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начать работу.</span><span class="sxs-lookup"><span data-stu-id="4729d-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="4729d-110">Создание приложения-функции Azure</span><span class="sxs-lookup"><span data-stu-id="4729d-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Приложение-функция успешно создана.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="4729d-112">Создайте функцию в приложение новые функции hello.</span><span class="sxs-lookup"><span data-stu-id="4729d-112">Next, you create a function in hello new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-github-webhook-triggered-function"></a><span data-ttu-id="4729d-113">Создание функции, активируемой объектом webhook GitHub</span><span class="sxs-lookup"><span data-stu-id="4729d-113">Create a GitHub webhook triggered function</span></span>

1. <span data-ttu-id="4729d-114">Разверните приложения функции и щелкните hello  **+**  рядом слишком**функции**.</span><span class="sxs-lookup"><span data-stu-id="4729d-114">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="4729d-115">Если это первая функция hello в приложении функции, выберите **пользовательские функции**.</span><span class="sxs-lookup"><span data-stu-id="4729d-115">If this is hello first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="4729d-116">Откроется hello полный набор шаблонов функций.</span><span class="sxs-lookup"><span data-stu-id="4729d-116">This displays hello complete set of function templates.</span></span>

    ![Страница быстрого запуска функции в hello портал Azure](./media/functions-create-github-webhook-triggered-function/add-first-function.png)

2. <span data-ttu-id="4729d-118">Выберите hello **GitHub веб-перехватчика** шаблона для нужный язык.</span><span class="sxs-lookup"><span data-stu-id="4729d-118">Select hello **GitHub WebHook** template for your desired language.</span></span> <span data-ttu-id="4729d-119">**Присвойте функции имя** и щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="4729d-119">**Name your function**, then select **Create**.</span></span>

     ![Создайте функцию запуска веб-перехватчика GitHub в hello портал Azure](./media/functions-create-github-webhook-triggered-function/functions-create-github-webhook-trigger.png) 

3. <span data-ttu-id="4729d-121">В новые функции, щелкните **URL-адрес функции <> / Get**, затем скопируйте и сохраните значения hello.</span><span class="sxs-lookup"><span data-stu-id="4729d-121">In your new function, click **</> Get function URL**, then copy and save hello values.</span></span> <span data-ttu-id="4729d-122">Здравствуйте, такие же действия **<> / GitHub получить секрет**.</span><span class="sxs-lookup"><span data-stu-id="4729d-122">Do hello same thing for **</> Get GitHub secret**.</span></span> <span data-ttu-id="4729d-123">Используйте эти веб-перехватчика значения tooconfigure hello в GitHub.</span><span class="sxs-lookup"><span data-stu-id="4729d-123">You use these values tooconfigure hello webhook in GitHub.</span></span>

    ![Просмотрите код функции hello](./media/functions-create-github-webhook-triggered-function/functions-copy-function-url-github-secret.png)

<span data-ttu-id="4729d-125">Затем создайте объект webhook в репозитории GitHub.</span><span class="sxs-lookup"><span data-stu-id="4729d-125">Next, you create a webhook in your GitHub repository.</span></span>

## <a name="configure-hello-webhook"></a><span data-ttu-id="4729d-126">Настройка веб-перехватчика hello</span><span class="sxs-lookup"><span data-stu-id="4729d-126">Configure hello webhook</span></span>

1. <span data-ttu-id="4729d-127">На портале GitHub перейдите tooa репозитория, вы являетесь владельцем.</span><span class="sxs-lookup"><span data-stu-id="4729d-127">In GitHub, navigate tooa repository that you own.</span></span> <span data-ttu-id="4729d-128">Вы можете использовать любые репозитории, для которых создали ответвления.</span><span class="sxs-lookup"><span data-stu-id="4729d-128">You can also use any repository that you have forked.</span></span> <span data-ttu-id="4729d-129">Toofork репозиторий используйте <https://github.com/Azure-Samples/functions-quickstart>.</span><span class="sxs-lookup"><span data-stu-id="4729d-129">If you need toofork a repository, use <https://github.com/Azure-Samples/functions-quickstart>.</span></span>

1. <span data-ttu-id="4729d-130">Щелкните **Параметры**, **Веб-перехватчики**, а затем — **Добавить веб-перехватчик**.</span><span class="sxs-lookup"><span data-stu-id="4729d-130">Click **Settings**, then click **Webhooks**, and  **Add webhook**.</span></span>

    ![Добавление объекта webhook GitHub](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-2.png)

1. <span data-ttu-id="4729d-132">Использовать параметры, как указано в таблице hello, а затем нажмите кнопку **добавить веб-перехватчика**.</span><span class="sxs-lookup"><span data-stu-id="4729d-132">Use settings as specified in hello table, then click **Add webhook**.</span></span>

    ![Задать URL-адрес веб-перехватчика hello и секрет](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-3.png)

| <span data-ttu-id="4729d-134">Настройка</span><span class="sxs-lookup"><span data-stu-id="4729d-134">Setting</span></span> | <span data-ttu-id="4729d-135">Рекомендуемое значение</span><span class="sxs-lookup"><span data-stu-id="4729d-135">Suggested value</span></span> | <span data-ttu-id="4729d-136">Описание</span><span class="sxs-lookup"><span data-stu-id="4729d-136">Description</span></span> |
|---|---|---|
| <span data-ttu-id="4729d-137">**Payload URL** (URL-адрес полезных данных)</span><span class="sxs-lookup"><span data-stu-id="4729d-137">**Payload URL**</span></span> | <span data-ttu-id="4729d-138">Скопированное значение</span><span class="sxs-lookup"><span data-stu-id="4729d-138">Copied value</span></span> | <span data-ttu-id="4729d-139">Используйте значение hello, возвращенное **URL-адрес функции <> / Get**.</span><span class="sxs-lookup"><span data-stu-id="4729d-139">Use hello value returned by  **</> Get function URL**.</span></span> |
| <span data-ttu-id="4729d-140">**Секрет**</span><span class="sxs-lookup"><span data-stu-id="4729d-140">**Secret**</span></span>   | <span data-ttu-id="4729d-141">Скопированное значение</span><span class="sxs-lookup"><span data-stu-id="4729d-141">Copied value</span></span> | <span data-ttu-id="4729d-142">Используйте значение hello, возвращенное **<> / GitHub получить секрет**.</span><span class="sxs-lookup"><span data-stu-id="4729d-142">Use hello value returned by  **</> Get GitHub secret**.</span></span> |
| <span data-ttu-id="4729d-143">**Тип содержимого**</span><span class="sxs-lookup"><span data-stu-id="4729d-143">**Content type**</span></span> | <span data-ttu-id="4729d-144">приложение/json</span><span class="sxs-lookup"><span data-stu-id="4729d-144">application/json</span></span> | <span data-ttu-id="4729d-145">функция Hello ожидает полезные данные JSON.</span><span class="sxs-lookup"><span data-stu-id="4729d-145">hello function expects a JSON payload.</span></span> |
| <span data-ttu-id="4729d-146">Триггеры событий</span><span class="sxs-lookup"><span data-stu-id="4729d-146">Event triggers</span></span> | <span data-ttu-id="4729d-147">Let me select individual events (Я выбираю отдельные события)</span><span class="sxs-lookup"><span data-stu-id="4729d-147">Let me select individual events</span></span> | <span data-ttu-id="4729d-148">Нам нужен только tootrigger на проблему комментирования событий.</span><span class="sxs-lookup"><span data-stu-id="4729d-148">We only want tootrigger on issue comment events.</span></span>  |
| | <span data-ttu-id="4729d-149">Issue comment (Примечание к вопросу)</span><span class="sxs-lookup"><span data-stu-id="4729d-149">Issue comment</span></span> |  |

<span data-ttu-id="4729d-150">Теперь hello веб-перехватчика имеет настроенный tootrigger функции при добавлении нового комментария проблему.</span><span class="sxs-lookup"><span data-stu-id="4729d-150">Now, hello webhook is configured tootrigger your function when a new issue comment is added.</span></span>

## <a name="test-hello-function"></a><span data-ttu-id="4729d-151">Проверка функции hello</span><span class="sxs-lookup"><span data-stu-id="4729d-151">Test hello function</span></span>

1. <span data-ttu-id="4729d-152">В репозитории GitHub откройте hello **проблемы** вкладку в новом окне браузера.</span><span class="sxs-lookup"><span data-stu-id="4729d-152">In your GitHub repository, open hello **Issues** tab in a new browser window.</span></span>

1. <span data-ttu-id="4729d-153">В новом окне приветствия щелкните **новая проблема**, введите заголовок и нажмите кнопку **отправить новый выпуск**.</span><span class="sxs-lookup"><span data-stu-id="4729d-153">In hello new window, click **New Issue**, type a title, and then click **Submit new issue**.</span></span>

1. <span data-ttu-id="4729d-154">В выпуске hello, введите комментарий и нажмите кнопку **комментарий**.</span><span class="sxs-lookup"><span data-stu-id="4729d-154">In hello issue, type a comment and click **Comment**.</span></span>

    ![Добавление примечания к вопросу GitHub](./media/functions-create-github-webhook-triggered-function/functions-github-webhook-add-comment.png)

1. <span data-ttu-id="4729d-156">Вернитесь к предыдущему окну toohello портал и просмотрите журналы hello.</span><span class="sxs-lookup"><span data-stu-id="4729d-156">Go back toohello portal and view hello logs.</span></span> <span data-ttu-id="4729d-157">Должна появиться запись трассировки hello новым текстом комментария.</span><span class="sxs-lookup"><span data-stu-id="4729d-157">You should see a trace entry with hello new comment text.</span></span>

     ![Просмотр текста hello комментария в журналах hello.](./media/functions-create-github-webhook-triggered-function/function-app-view-logs.png)

## <a name="clean-up-resources"></a><span data-ttu-id="4729d-159">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="4729d-159">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="4729d-160">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4729d-160">Next steps</span></span>

<span data-ttu-id="4729d-161">Вы создали функцию, которая выполняется при получении запроса объекта webhook GitHub.</span><span class="sxs-lookup"><span data-stu-id="4729d-161">You have created a function that runs when a request is received from a GitHub webhook.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="4729d-162">Дополнительные сведения см. в статье [Привязки HTTP и веб-перехватчика в функциях Azure](functions-bindings-http-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="4729d-162">For more information about webhook triggers, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span>
