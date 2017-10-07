---
title: "aaaCreate функции в Azure, активируемых сообщений очереди | Документы Microsoft"
description: "Использовать функции Azure toocreate без сервера функция, вызываемая сообщений отправить tooan очереди службы хранилища Azure."
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 361da2a4-15d1-4903-bdc4-cc4b27fc3ff4
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: e9501ed336b502eaeee3fa62ec4ae085c76de0ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-azure-queue-storage"></a><span data-ttu-id="7d5bd-103">Создание функции, активируемой хранилищем очередей Azure</span><span class="sxs-lookup"><span data-stu-id="7d5bd-103">Create a function triggered by Azure Queue storage</span></span>

<span data-ttu-id="7d5bd-104">Узнайте, как toocreate функции, вызываемые при сообщения, отправленные tooan очереди службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="7d5bd-104">Learn how toocreate a function triggered when messages are submitted tooan Azure Storage queue.</span></span>

![Представление сообщений в журналах hello.](./media/functions-create-storage-queue-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="7d5bd-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7d5bd-106">Prerequisites</span></span>

- <span data-ttu-id="7d5bd-107">Загрузите и установите hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="7d5bd-107">Download and install hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

- <span data-ttu-id="7d5bd-108">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="7d5bd-108">An Azure subscription.</span></span> <span data-ttu-id="7d5bd-109">Если у вас еще нет подписки Azure, создайте [бесплатную учетную запись](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начать работу.</span><span class="sxs-lookup"><span data-stu-id="7d5bd-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="7d5bd-110">Создание приложения-функции Azure</span><span class="sxs-lookup"><span data-stu-id="7d5bd-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Приложение-функция успешно создана.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="7d5bd-112">Создайте функцию в приложение новые функции hello.</span><span class="sxs-lookup"><span data-stu-id="7d5bd-112">Next, you create a function in hello new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-queue-triggered-function"></a><span data-ttu-id="7d5bd-113">Создание функции, активируемой очередью</span><span class="sxs-lookup"><span data-stu-id="7d5bd-113">Create a Queue triggered function</span></span>

1. <span data-ttu-id="7d5bd-114">Разверните приложения функции и щелкните hello  **+**  рядом слишком**функции**.</span><span class="sxs-lookup"><span data-stu-id="7d5bd-114">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="7d5bd-115">Если это первая функция hello в приложении функции, выберите **пользовательские функции**.</span><span class="sxs-lookup"><span data-stu-id="7d5bd-115">If this is hello first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="7d5bd-116">Откроется hello полный набор шаблонов функций.</span><span class="sxs-lookup"><span data-stu-id="7d5bd-116">This displays hello complete set of function templates.</span></span>

    ![Страница быстрого запуска функции в hello портал Azure](./media/functions-create-storage-queue-triggered-function/add-first-function.png)

2. <span data-ttu-id="7d5bd-118">Выберите hello **QueueTrigger** шаблона для нужного языка и использовать параметры hello, как указано в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="7d5bd-118">Select hello **QueueTrigger** template for your desired language, and  use hello settings as specified in hello table.</span></span>

    ![Создание функции активации очереди хранилища hello.](./media/functions-create-storage-queue-triggered-function/functions-create-queue-storage-trigger-portal.png)
    
    | <span data-ttu-id="7d5bd-120">Настройка</span><span class="sxs-lookup"><span data-stu-id="7d5bd-120">Setting</span></span> | <span data-ttu-id="7d5bd-121">Рекомендуемое значение</span><span class="sxs-lookup"><span data-stu-id="7d5bd-121">Suggested value</span></span> | <span data-ttu-id="7d5bd-122">Описание</span><span class="sxs-lookup"><span data-stu-id="7d5bd-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="7d5bd-123">**Имя очереди**</span><span class="sxs-lookup"><span data-stu-id="7d5bd-123">**Queue name**</span></span>   | <span data-ttu-id="7d5bd-124">myqueue-items</span><span class="sxs-lookup"><span data-stu-id="7d5bd-124">myqueue-items</span></span>    | <span data-ttu-id="7d5bd-125">Имя hello очереди tooconnect tooin вашей учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="7d5bd-125">Name of hello queue tooconnect tooin your Storage account.</span></span> |
    | <span data-ttu-id="7d5bd-126">**Подключение к учетной записи хранения**</span><span class="sxs-lookup"><span data-stu-id="7d5bd-126">**Storage account connection**</span></span> | <span data-ttu-id="7d5bd-127">AzureWebJobStorage</span><span class="sxs-lookup"><span data-stu-id="7d5bd-127">AzureWebJobStorage</span></span> | <span data-ttu-id="7d5bd-128">Можно использовать уже используется приложением функции подключения к учетной записи хранилища hello или создайте новую.</span><span class="sxs-lookup"><span data-stu-id="7d5bd-128">You can use hello storage account connection already being used by your function app, or create a new one.</span></span>  |
    | <span data-ttu-id="7d5bd-129">**Имя функции**</span><span class="sxs-lookup"><span data-stu-id="7d5bd-129">**Name your function**</span></span> | <span data-ttu-id="7d5bd-130">Уникальное для вашего приложения-функции</span><span class="sxs-lookup"><span data-stu-id="7d5bd-130">Unique in your function app</span></span> | <span data-ttu-id="7d5bd-131">Имя функции, активируемой очередью.</span><span class="sxs-lookup"><span data-stu-id="7d5bd-131">Name of this queue triggered function.</span></span> |

3. <span data-ttu-id="7d5bd-132">Нажмите кнопку **создать** toocreate функции.</span><span class="sxs-lookup"><span data-stu-id="7d5bd-132">Click **Create** toocreate your function.</span></span>

<span data-ttu-id="7d5bd-133">Затем подключите учетную запись хранилища Azure tooyour и создать hello **myqueue элементы** очереди хранилища.</span><span class="sxs-lookup"><span data-stu-id="7d5bd-133">Next, you connect tooyour Azure Storage account and create hello **myqueue-items** storage queue.</span></span>

## <a name="create-hello-queue"></a><span data-ttu-id="7d5bd-134">Создать очередь hello</span><span class="sxs-lookup"><span data-stu-id="7d5bd-134">Create hello queue</span></span>

1. <span data-ttu-id="7d5bd-135">Щелкните **Интегрировать** в своей функции, затем разверните узел **Документация** и скопируйте **имя учетной записи** и **ключ учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="7d5bd-135">In your function, click **Integrate**, expand **Documentation**, and copy both **Account name** and **Account key**.</span></span> <span data-ttu-id="7d5bd-136">Можно использовать учетную запись хранения tooconnect toohello эти учетные данные.</span><span class="sxs-lookup"><span data-stu-id="7d5bd-136">You use these credentials tooconnect toohello storage account.</span></span> <span data-ttu-id="7d5bd-137">Если вы уже подключились вашей учетной записи хранилища, пропустите toostep 4.</span><span class="sxs-lookup"><span data-stu-id="7d5bd-137">If you have already connected your storage account, skip toostep 4.</span></span>

    ![Получите учетные данные для подключения учетной записи хранилища hello.](./media/functions-create-storage-queue-triggered-function/functions-storage-account-connection.png)<span data-ttu-id="7d5bd-139">v</span><span class="sxs-lookup"><span data-stu-id="7d5bd-139">v</span></span>

1. <span data-ttu-id="7d5bd-140">Запустите hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) инструмент, нажмите кнопку hello значок слева hello подключения, выберите **использовать имя учетной записи хранения и ключ**и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7d5bd-140">Run hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, click hello connect icon on hello left, choose **Use a storage account name and key**, and click **Next**.</span></span>

    ![Запустите средство hello обозреватель учетной записи хранилища.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-1.png)

1. <span data-ttu-id="7d5bd-142">Введите hello **имя учетной записи** и **ключ учетной записи** из шага 1, нажмите кнопку **Далее** и затем **Connect**.</span><span class="sxs-lookup"><span data-stu-id="7d5bd-142">Enter hello **Account name** and **Account key** from step 1, click **Next** and then **Connect**.</span></span>

    ![Введите учетные данные хранилища hello и подключения.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-2.png)

1. <span data-ttu-id="7d5bd-144">Hello присоединенного учетной записи хранилища, щелкните правой кнопкой **очереди**, нажмите кнопку **создать очередь**, тип `myqueue-items`, и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="7d5bd-144">Expand hello attached storage account, right-click **Queues**, click **Create queue**, type `myqueue-items`, and then press enter.</span></span>

    ![Создание очереди службы хранилища](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-create-queue.png)

<span data-ttu-id="7d5bd-146">Теперь, когда очередь хранилища можно проверить функции hello, добавив toohello очереди сообщений.</span><span class="sxs-lookup"><span data-stu-id="7d5bd-146">Now that you have a storage queue, you can test hello function by adding a message toohello queue.</span></span>

## <a name="test-hello-function"></a><span data-ttu-id="7d5bd-147">Проверка функции hello</span><span class="sxs-lookup"><span data-stu-id="7d5bd-147">Test hello function</span></span>

1. <span data-ttu-id="7d5bd-148">Обратно в hello портал Azure, функция tooyour обзора разверните hello **журналы** hello нижней части страницы hello и убедитесь, что не приостановлен, журналов потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="7d5bd-148">Back in hello Azure portal, browse tooyour function expand hello **Logs** at hello bottom of hello page and make sure that log streaming isn't paused.</span></span>

1. <span data-ttu-id="7d5bd-149">Разверните свою учетную запись в обозревателе хранилищ, узел **Очереди** и **myqueue-items**, а затем щелкните **Add message** (Добавить сообщение).</span><span class="sxs-lookup"><span data-stu-id="7d5bd-149">In Storage Explorer, expand your storage account, **Queues**, and **myqueue-items**, then click **Add message**.</span></span>

    ![Добавьте toohello очереди сообщений.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-add-message.png)

1. <span data-ttu-id="7d5bd-151">Введите сообщение Hello World</span><span class="sxs-lookup"><span data-stu-id="7d5bd-151">Type your "Hello World!"</span></span> <span data-ttu-id="7d5bd-152">в поле **Текст сообщения** и щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="7d5bd-152">message in **Message text** and click **OK**.</span></span>

1. <span data-ttu-id="7d5bd-153">Подождите несколько секунд, а затем вернитесь tooyour журналов функций и убедитесь, что новые сообщения hello уже считаны из очереди hello.</span><span class="sxs-lookup"><span data-stu-id="7d5bd-153">Wait for a few seconds, then go back tooyour function logs and verify that hello new message has been read from hello queue.</span></span>

    ![Представление сообщений в журналах hello.](./media/functions-create-storage-queue-triggered-function/functions-queue-storage-trigger-view-logs.png)

1. <span data-ttu-id="7d5bd-155">Назад в обозреватель хранилищ щелкните **обновление** и убедитесь, что приветственное сообщение было обработано и hello очереди больше не.</span><span class="sxs-lookup"><span data-stu-id="7d5bd-155">Back in Storage Explorer, click **Refresh** and verify that hello message has been processed and is no longer in hello queue.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="7d5bd-156">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="7d5bd-156">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="7d5bd-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7d5bd-157">Next steps</span></span>

<span data-ttu-id="7d5bd-158">Вы создали функцию, которая выполняется при добавлении tooa хранилища очереди сообщений.</span><span class="sxs-lookup"><span data-stu-id="7d5bd-158">You have created a function that runs when a message is added tooa storage queue.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="7d5bd-159">Дополнительные сведения о триггерах хранилища очередей см. в статье [Привязки очередей службы хранилища для Функций Azure](functions-bindings-storage-queue.md).</span><span class="sxs-lookup"><span data-stu-id="7d5bd-159">For more information about Queue storage triggers, see [Azure Functions Storage queue bindings](functions-bindings-storage-queue.md).</span></span>