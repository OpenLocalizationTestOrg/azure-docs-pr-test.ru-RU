---
title: "функция в Azure, активируемых хранилища больших двоичных объектов aaaCreate | Документы Microsoft"
description: "Использование функции Azure toocreate данной функции, которая вызывается для элементов добавлен tooAzure хранилища больших двоичных объектов."
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: d6bff41c-a624-40c1-bbc7-80590df29ded
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: acb7d29abb07a22da11d0e65d2ed54591f8e3f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-azure-blob-storage"></a><span data-ttu-id="9f9f0-103">Создание функции, активируемой хранилищем BLOB-объектов Azure</span><span class="sxs-lookup"><span data-stu-id="9f9f0-103">Create a function triggered by Azure Blob storage</span></span>

<span data-ttu-id="9f9f0-104">Узнайте, как toocreate функции, вызываемые при файлы, загрузить tooor обновляется в хранилище больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="9f9f0-104">Learn how toocreate a function triggered when files are uploaded tooor updated in Azure Blob storage.</span></span>

![Представление сообщений в журналах hello.](./media/functions-create-storage-blob-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="9f9f0-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9f9f0-106">Prerequisites</span></span>

+ <span data-ttu-id="9f9f0-107">Загрузите и установите hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="9f9f0-107">Download and install hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>
+ <span data-ttu-id="9f9f0-108">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="9f9f0-108">An Azure subscription.</span></span> <span data-ttu-id="9f9f0-109">Если у вас еще нет подписки Azure, создайте [бесплатную учетную запись](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начать работу.</span><span class="sxs-lookup"><span data-stu-id="9f9f0-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="9f9f0-110">Создание приложения-функции Azure</span><span class="sxs-lookup"><span data-stu-id="9f9f0-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Приложение-функция успешно создана.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="9f9f0-112">Создайте функцию в приложение новые функции hello.</span><span class="sxs-lookup"><span data-stu-id="9f9f0-112">Next, you create a function in hello new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-blob-storage-triggered-function"></a><span data-ttu-id="9f9f0-113">Создание функции, активируемой хранилищем BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="9f9f0-113">Create a Blob storage triggered function</span></span>

1. <span data-ttu-id="9f9f0-114">Разверните приложения функции и щелкните hello  **+**  рядом слишком**функции**.</span><span class="sxs-lookup"><span data-stu-id="9f9f0-114">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="9f9f0-115">Если это первая функция hello в приложении функции, выберите **пользовательские функции**.</span><span class="sxs-lookup"><span data-stu-id="9f9f0-115">If this is hello first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="9f9f0-116">Откроется hello полный набор шаблонов функций.</span><span class="sxs-lookup"><span data-stu-id="9f9f0-116">This displays hello complete set of function templates.</span></span>

    ![Страница быстрого запуска функции в hello портал Azure](./media/functions-create-storage-blob-triggered-function/add-first-function.png)

2. <span data-ttu-id="9f9f0-118">Выберите hello **BlobTrigger** шаблона для нужного языка и использовать параметры hello, как указано в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="9f9f0-118">Select hello **BlobTrigger** template for your desired language, and use hello settings as specified in hello table.</span></span>

    ![Создайте функцию запуска хранилища больших двоичных объектов hello.](./media/functions-create-storage-blob-triggered-function/functions-create-blob-storage-trigger-portal.png)

    | <span data-ttu-id="9f9f0-120">Настройка</span><span class="sxs-lookup"><span data-stu-id="9f9f0-120">Setting</span></span> | <span data-ttu-id="9f9f0-121">Рекомендуемое значение</span><span class="sxs-lookup"><span data-stu-id="9f9f0-121">Suggested value</span></span> | <span data-ttu-id="9f9f0-122">Описание</span><span class="sxs-lookup"><span data-stu-id="9f9f0-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="9f9f0-123">**Путь**</span><span class="sxs-lookup"><span data-stu-id="9f9f0-123">**Path**</span></span>   | <span data-ttu-id="9f9f0-124">mycontainer/{name}</span><span class="sxs-lookup"><span data-stu-id="9f9f0-124">mycontainer/{name}</span></span>    | <span data-ttu-id="9f9f0-125">Расположение в хранилище BLOB-объектов отслеживается.</span><span class="sxs-lookup"><span data-stu-id="9f9f0-125">Location in Blob storage being monitored.</span></span> <span data-ttu-id="9f9f0-126">Имя файла Hello hello большого двоичного объекта передается в привязке hello как hello _имя_ параметра.</span><span class="sxs-lookup"><span data-stu-id="9f9f0-126">hello file name of hello blob is passed in hello binding as hello _name_ parameter.</span></span>  |
    | <span data-ttu-id="9f9f0-127">**Подключение к учетной записи хранения**</span><span class="sxs-lookup"><span data-stu-id="9f9f0-127">**Storage account connection**</span></span> | <span data-ttu-id="9f9f0-128">AzureWebJobStorage</span><span class="sxs-lookup"><span data-stu-id="9f9f0-128">AzureWebJobStorage</span></span> | <span data-ttu-id="9f9f0-129">Можно использовать уже используется приложением функции подключения к учетной записи хранилища hello или создайте новую.</span><span class="sxs-lookup"><span data-stu-id="9f9f0-129">You can use hello storage account connection already being used by your function app, or create a new one.</span></span>  |
    | <span data-ttu-id="9f9f0-130">**Имя функции**</span><span class="sxs-lookup"><span data-stu-id="9f9f0-130">**Name your function**</span></span> | <span data-ttu-id="9f9f0-131">Уникальное для вашего приложения-функции</span><span class="sxs-lookup"><span data-stu-id="9f9f0-131">Unique in your function app</span></span> | <span data-ttu-id="9f9f0-132">Имя функции, активируемой большим двоичным объектом.</span><span class="sxs-lookup"><span data-stu-id="9f9f0-132">Name of this blob triggered function.</span></span> |

3. <span data-ttu-id="9f9f0-133">Нажмите кнопку **создать** toocreate функции.</span><span class="sxs-lookup"><span data-stu-id="9f9f0-133">Click **Create** toocreate your function.</span></span>

<span data-ttu-id="9f9f0-134">Затем подключите учетную запись хранилища Azure tooyour и создать hello **mycontainer** контейнера.</span><span class="sxs-lookup"><span data-stu-id="9f9f0-134">Next, you connect tooyour Azure Storage account and create hello **mycontainer** container.</span></span>

## <a name="create-hello-container"></a><span data-ttu-id="9f9f0-135">Создание контейнера hello</span><span class="sxs-lookup"><span data-stu-id="9f9f0-135">Create hello container</span></span>

1. <span data-ttu-id="9f9f0-136">Щелкните **Интегрировать** в своей функции, затем разверните узел **Документация** и скопируйте **имя учетной записи** и **ключ учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="9f9f0-136">In your function, click **Integrate**, expand **Documentation**, and copy both **Account name** and **Account key**.</span></span> <span data-ttu-id="9f9f0-137">Можно использовать учетную запись хранения tooconnect toohello эти учетные данные.</span><span class="sxs-lookup"><span data-stu-id="9f9f0-137">You use these credentials tooconnect toohello storage account.</span></span> <span data-ttu-id="9f9f0-138">Если вы уже подключились вашей учетной записи хранилища, пропустите toostep 4.</span><span class="sxs-lookup"><span data-stu-id="9f9f0-138">If you have already connected your storage account, skip toostep 4.</span></span>

    ![Получите учетные данные для подключения учетной записи хранилища hello.](./media/functions-create-storage-blob-triggered-function/functions-storage-account-connection.png)

1. <span data-ttu-id="9f9f0-140">Запустите hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) инструмент, нажмите кнопку hello значок слева hello подключения, выберите **использовать имя учетной записи хранения и ключ**и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="9f9f0-140">Run hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, click hello connect icon on hello left, choose **Use a storage account name and key**, and click **Next**.</span></span>

    ![Запустите средство hello обозреватель учетной записи хранилища.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-1.png)

1. <span data-ttu-id="9f9f0-142">Введите hello **имя учетной записи** и **ключ учетной записи** из шага 1, нажмите кнопку **Далее** и затем **Connect**.</span><span class="sxs-lookup"><span data-stu-id="9f9f0-142">Enter hello **Account name** and **Account key** from step 1, click **Next** and then **Connect**.</span></span> 

    ![Введите учетные данные хранилища hello и подключения.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-2.png)

1. <span data-ttu-id="9f9f0-144">Hello присоединенного учетной записи хранилища, щелкните правой кнопкой **контейнеры больших двоичных объектов**, нажмите кнопку **создать контейнер больших двоичных объектов**, тип `mycontainer`, и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="9f9f0-144">Expand hello attached storage account, right-click **Blob containers**, click **Create blob container**, type `mycontainer`, and then press enter.</span></span>

    ![Создание очереди службы хранилища](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-create-blob-container.png)

<span data-ttu-id="9f9f0-146">Теперь, когда контейнер больших двоичных объектов, можно проверить функции hello передав toohello контейнера файлов.</span><span class="sxs-lookup"><span data-stu-id="9f9f0-146">Now that you have a blob container, you can test hello function by uploading a file toohello container.</span></span>

## <a name="test-hello-function"></a><span data-ttu-id="9f9f0-147">Проверка функции hello</span><span class="sxs-lookup"><span data-stu-id="9f9f0-147">Test hello function</span></span>

1. <span data-ttu-id="9f9f0-148">Обратно в hello портал Azure, функция tooyour обзора разверните hello **журналы** hello нижней части страницы hello и убедитесь, что не приостановлен, журналов потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="9f9f0-148">Back in hello Azure portal, browse tooyour function expand hello **Logs** at hello bottom of hello page and make sure that log streaming isn't paused.</span></span>

1. <span data-ttu-id="9f9f0-149">В обозревателе хранилищ разверните вашу учетную запись хранения, **Blob containers** (Контейнеры больших двоичных объектов) и **mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="9f9f0-149">In Storage Explorer, expand your storage account, **Blob containers**, and **mycontainer**.</span></span> <span data-ttu-id="9f9f0-150">Щелкните **Отправка**, а затем **Отправка файлов**.</span><span class="sxs-lookup"><span data-stu-id="9f9f0-150">Click **Upload** and then **Upload files...**.</span></span>

    ![Отправьте файл toohello BLOB-контейнере.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-upload-file-blob.png)

1. <span data-ttu-id="9f9f0-152">В hello **передачи файлов** диалоговое окно, нажмите кнопку hello **файлы** поля.</span><span class="sxs-lookup"><span data-stu-id="9f9f0-152">In hello **Upload files** dialog box, click hello **Files** field.</span></span> <span data-ttu-id="9f9f0-153">Обзор tooa файл на локальном компьютере, таких как файл изображения, выберите его и нажмите кнопку **откройте** и затем **отправить**.</span><span class="sxs-lookup"><span data-stu-id="9f9f0-153">Browse tooa file on your local computer, such as an image file, select it and click **Open** and then **Upload**.</span></span>

1. <span data-ttu-id="9f9f0-154">Вернитесь к предыдущему окну tooyour журналов функций и убедитесь, что были прочитаны hello большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="9f9f0-154">Go back tooyour function logs and verify that hello blob has been read.</span></span>

   ![Представление сообщений в журналах hello.](./media/functions-create-storage-blob-triggered-function/functions-blob-storage-trigger-view-logs.png)

    >[!NOTE]
    > <span data-ttu-id="9f9f0-156">При выполнении функции приложения в плане использования по умолчанию hello могут существовать задержки вверх tooseveral минут между hello добавлении или обновлении большого двоичного объекта и hello функции запустилась.</span><span class="sxs-lookup"><span data-stu-id="9f9f0-156">When your function app runs in hello default Consumption plan, there may be a delay of up tooseveral minutes between hello blob being added or updated and hello function being triggered.</span></span> <span data-ttu-id="9f9f0-157">Выполняйте свое приложение-функцию в рамках плана службы приложений, если требуется малая задержка в функции, активируемой большим двоичным объектом.</span><span class="sxs-lookup"><span data-stu-id="9f9f0-157">If you need low latency in your blob triggered functions, consider running your function app in an App Service plan.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="9f9f0-158">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="9f9f0-158">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="9f9f0-159">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9f9f0-159">Next steps</span></span>

<span data-ttu-id="9f9f0-160">Вы создали функцию, которая выполняется при добавлении tooor обновить большой двоичный объект в хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="9f9f0-160">You have created a function that runs when a blob is added tooor updated in Blob storage.</span></span> 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="9f9f0-161">Дополнительные сведения о триггерах хранилища BLOB-объектов см.в статье [Привязки больших двоичных объектов службы хранилища для Функций Azure](functions-bindings-storage-blob.md).</span><span class="sxs-lookup"><span data-stu-id="9f9f0-161">For more information about Blob storage triggers, see [Azure Functions Blob storage bindings](functions-bindings-storage-blob.md).</span></span>
