---
title: "Создание функции, активируемой сообщениями очереди, в Azure | Документация Майкрософт"
description: "Создавайте независимые от сервера функции, активируемые сообщениями, отправленными в очередь службы хранилища Azure."
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
ms.openlocfilehash: 92a03154bf5a8945e2de9606afd138803c76fafe
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-triggered-by-azure-queue-storage"></a><span data-ttu-id="d4354-103">Создание функции, активируемой хранилищем очередей Azure</span><span class="sxs-lookup"><span data-stu-id="d4354-103">Create a function triggered by Azure Queue storage</span></span>

<span data-ttu-id="d4354-104">Узнайте, как создавать функцию, активируемую при отправке сообщений в очередь службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="d4354-104">Learn how to create a function triggered when messages are submitted to an Azure Storage queue.</span></span>

![Просмотр сообщения в журналах](./media/functions-create-storage-queue-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="d4354-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d4354-106">Prerequisites</span></span>

- <span data-ttu-id="d4354-107">Скачайте и установите [обозреватель хранилищ Microsoft Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="d4354-107">Download and install the [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

- <span data-ttu-id="d4354-108">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="d4354-108">An Azure subscription.</span></span> <span data-ttu-id="d4354-109">Если у вас еще нет подписки Azure, создайте [бесплатную учетную запись](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начать работу.</span><span class="sxs-lookup"><span data-stu-id="d4354-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="d4354-110">Создание приложения-функции Azure</span><span class="sxs-lookup"><span data-stu-id="d4354-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Приложение-функция успешно создана.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="d4354-112">Затем создайте функцию в новом приложении-функции.</span><span class="sxs-lookup"><span data-stu-id="d4354-112">Next, you create a function in the new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-queue-triggered-function"></a><span data-ttu-id="d4354-113">Создание функции, активируемой очередью</span><span class="sxs-lookup"><span data-stu-id="d4354-113">Create a Queue triggered function</span></span>

1. <span data-ttu-id="d4354-114">Разверните приложение-функцию и нажмите кнопку **+** рядом с элементом **Функции**.</span><span class="sxs-lookup"><span data-stu-id="d4354-114">Expand your function app and click the **+** button next to **Functions**.</span></span> <span data-ttu-id="d4354-115">Если это первая функция в приложении-функции, выберите **Пользовательская функция**.</span><span class="sxs-lookup"><span data-stu-id="d4354-115">If this is the first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="d4354-116">Откроется полный набор шаблонов функций.</span><span class="sxs-lookup"><span data-stu-id="d4354-116">This displays the complete set of function templates.</span></span>

    ![Страница быстрого начала работы с функциями на портале Azure](./media/functions-create-storage-queue-triggered-function/add-first-function.png)

2. <span data-ttu-id="d4354-118">Выберите шаблон **QueueTrigger** для нужного языка и используйте параметры, как указано в таблице.</span><span class="sxs-lookup"><span data-stu-id="d4354-118">Select the **QueueTrigger** template for your desired language, and  use the settings as specified in the table.</span></span>

    ![Создайте функцию, активируемую очередью службы хранилища.](./media/functions-create-storage-queue-triggered-function/functions-create-queue-storage-trigger-portal.png)
    
    | <span data-ttu-id="d4354-120">Настройка</span><span class="sxs-lookup"><span data-stu-id="d4354-120">Setting</span></span> | <span data-ttu-id="d4354-121">Рекомендуемое значение</span><span class="sxs-lookup"><span data-stu-id="d4354-121">Suggested value</span></span> | <span data-ttu-id="d4354-122">Описание</span><span class="sxs-lookup"><span data-stu-id="d4354-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="d4354-123">**Имя очереди**</span><span class="sxs-lookup"><span data-stu-id="d4354-123">**Queue name**</span></span>   | <span data-ttu-id="d4354-124">myqueue-items</span><span class="sxs-lookup"><span data-stu-id="d4354-124">myqueue-items</span></span>    | <span data-ttu-id="d4354-125">Имя очереди для подключения к вашей учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="d4354-125">Name of the queue to connect to in your Storage account.</span></span> |
    | <span data-ttu-id="d4354-126">**Подключение к учетной записи хранения**</span><span class="sxs-lookup"><span data-stu-id="d4354-126">**Storage account connection**</span></span> | <span data-ttu-id="d4354-127">AzureWebJobStorage</span><span class="sxs-lookup"><span data-stu-id="d4354-127">AzureWebJobStorage</span></span> | <span data-ttu-id="d4354-128">Вы можете использовать подключение к учетной записи хранения, которое уже используется вашим приложением-функцией, или создать его.</span><span class="sxs-lookup"><span data-stu-id="d4354-128">You can use the storage account connection already being used by your function app, or create a new one.</span></span>  |
    | <span data-ttu-id="d4354-129">**Имя функции**</span><span class="sxs-lookup"><span data-stu-id="d4354-129">**Name your function**</span></span> | <span data-ttu-id="d4354-130">Уникальное для вашего приложения-функции</span><span class="sxs-lookup"><span data-stu-id="d4354-130">Unique in your function app</span></span> | <span data-ttu-id="d4354-131">Имя функции, активируемой очередью.</span><span class="sxs-lookup"><span data-stu-id="d4354-131">Name of this queue triggered function.</span></span> |

3. <span data-ttu-id="d4354-132">Щелкните **Создать**, чтобы создать функцию.</span><span class="sxs-lookup"><span data-stu-id="d4354-132">Click **Create** to create your function.</span></span>

<span data-ttu-id="d4354-133">Затем необходимо подключиться к своей учетной записи хранения Azure и создать очередь службы хранилища **myqueue-items**.</span><span class="sxs-lookup"><span data-stu-id="d4354-133">Next, you connect to your Azure Storage account and create the **myqueue-items** storage queue.</span></span>

## <a name="create-the-queue"></a><span data-ttu-id="d4354-134">Создание очереди</span><span class="sxs-lookup"><span data-stu-id="d4354-134">Create the queue</span></span>

1. <span data-ttu-id="d4354-135">Щелкните **Интегрировать** в своей функции, затем разверните узел **Документация** и скопируйте **имя учетной записи** и **ключ учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="d4354-135">In your function, click **Integrate**, expand **Documentation**, and copy both **Account name** and **Account key**.</span></span> <span data-ttu-id="d4354-136">Эти учетные данные используются для подключения к учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="d4354-136">You use these credentials to connect to the storage account.</span></span> <span data-ttu-id="d4354-137">Если вы уже подключились к учетной записи хранения, перейдите к шагу 4.</span><span class="sxs-lookup"><span data-stu-id="d4354-137">If you have already connected your storage account, skip to step 4.</span></span>

    ![Получение учетных данных для подключения к учетной записи хранения.](./media/functions-create-storage-queue-triggered-function/functions-storage-account-connection.png)<span data-ttu-id="d4354-139">v</span><span class="sxs-lookup"><span data-stu-id="d4354-139">v</span></span>

1. <span data-ttu-id="d4354-140">Запустите инструмент [Обозреватель службы хранилища Microsoft Azure](http://storageexplorer.com/), щелкните значок подключения слева, выберите **Use a storage account name and key** (Использовать имя и ключ учетной записи хранения), а затем щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="d4354-140">Run the [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, click the connect icon on the left, choose **Use a storage account name and key**, and click **Next**.</span></span>

    ![Запуск инструмента "Обозреватель учетной записи хранения"](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-1.png)

1. <span data-ttu-id="d4354-142">Введите **имя учетной записи** и **ключ учетной записи** из шага 1, щелкните **Далее**, а затем — **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="d4354-142">Enter the **Account name** and **Account key** from step 1, click **Next** and then **Connect**.</span></span>

    ![Введите учетные данные хранилища и подключитесь.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-2.png)

1. <span data-ttu-id="d4354-144">Разверните подключенную учетную запись хранения, щелкните правой кнопкой мыши **Очереди** (Контейнеры больших двоичных объектов), а затем щелкните **Создать очередь**, введите `myqueue-items` и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="d4354-144">Expand the attached storage account, right-click **Queues**, click **Create queue**, type `myqueue-items`, and then press enter.</span></span>

    ![Создание очереди службы хранилища](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-create-queue.png)

<span data-ttu-id="d4354-146">Теперь, когда вы создали очередь хранилища, испытайте функцию, добавив сообщение в очередь.</span><span class="sxs-lookup"><span data-stu-id="d4354-146">Now that you have a storage queue, you can test the function by adding a message to the queue.</span></span>

## <a name="test-the-function"></a><span data-ttu-id="d4354-147">Проверка функции</span><span class="sxs-lookup"><span data-stu-id="d4354-147">Test the function</span></span>

1. <span data-ttu-id="d4354-148">На портале Azure перейдите к вашей функции, в нижней части страницы разверните **Журналы** и убедитесь, что потоковая передача журналов не остановлена.</span><span class="sxs-lookup"><span data-stu-id="d4354-148">Back in the Azure portal, browse to your function expand the **Logs** at the bottom of the page and make sure that log streaming isn't paused.</span></span>

1. <span data-ttu-id="d4354-149">Разверните свою учетную запись в обозревателе хранилищ, узел **Очереди** и **myqueue-items**, а затем щелкните **Add message** (Добавить сообщение).</span><span class="sxs-lookup"><span data-stu-id="d4354-149">In Storage Explorer, expand your storage account, **Queues**, and **myqueue-items**, then click **Add message**.</span></span>

    ![Добавление сообщения в очередь](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-add-message.png)

1. <span data-ttu-id="d4354-151">Введите сообщение Hello World</span><span class="sxs-lookup"><span data-stu-id="d4354-151">Type your "Hello World!"</span></span> <span data-ttu-id="d4354-152">в поле **Текст сообщения** и щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d4354-152">message in **Message text** and click **OK**.</span></span>

1. <span data-ttu-id="d4354-153">Подождите несколько секунд, а затем вернитесь в журналы функции и убедитесь, что новое сообщение было считано из очереди.</span><span class="sxs-lookup"><span data-stu-id="d4354-153">Wait for a few seconds, then go back to your function logs and verify that the new message has been read from the queue.</span></span>

    ![Просмотр сообщения в журналах](./media/functions-create-storage-queue-triggered-function/functions-queue-storage-trigger-view-logs.png)

1. <span data-ttu-id="d4354-155">Вернитесь в обозреватель хранилища, щелкните **Обновить** и убедитесь, что сообщение было обработано и больше не находится в очереди.</span><span class="sxs-lookup"><span data-stu-id="d4354-155">Back in Storage Explorer, click **Refresh** and verify that the message has been processed and is no longer in the queue.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="d4354-156">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="d4354-156">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="d4354-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d4354-157">Next steps</span></span>

<span data-ttu-id="d4354-158">Вы создали функцию, которая выполняется при добавлении сообщения в очередь хранилища.</span><span class="sxs-lookup"><span data-stu-id="d4354-158">You have created a function that runs when a message is added to a storage queue.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="d4354-159">Дополнительные сведения о триггерах хранилища очередей см. в статье [Привязки очередей службы хранилища для Функций Azure](functions-bindings-storage-queue.md).</span><span class="sxs-lookup"><span data-stu-id="d4354-159">For more information about Queue storage triggers, see [Azure Functions Storage queue bindings](functions-bindings-storage-queue.md).</span></span>