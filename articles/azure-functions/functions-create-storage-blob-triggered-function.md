---
title: "Создание функции, активируемой хранилищем BLOB-объектов, в Azure | Документация Майкрософт"
description: "Создавайте независимые от сервера функции, активируемые элементами, добавляемыми в хранилище BLOB-объектов Azure."
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
ms.openlocfilehash: 1ddd056903b1a2f973a58bd7054ea2b8281607c3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-triggered-by-azure-blob-storage"></a><span data-ttu-id="9a99f-103">Создание функции, активируемой хранилищем BLOB-объектов Azure</span><span class="sxs-lookup"><span data-stu-id="9a99f-103">Create a function triggered by Azure Blob storage</span></span>

<span data-ttu-id="9a99f-104">Узнайте, как создавать функцию, активируемую при добавлении файлов или их обновлении в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="9a99f-104">Learn how to create a function triggered when files are uploaded to or updated in Azure Blob storage.</span></span>

![Просмотр сообщения в журналах](./media/functions-create-storage-blob-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="9a99f-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9a99f-106">Prerequisites</span></span>

+ <span data-ttu-id="9a99f-107">Скачайте и установите [обозреватель хранилищ Microsoft Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="9a99f-107">Download and install the [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>
+ <span data-ttu-id="9a99f-108">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="9a99f-108">An Azure subscription.</span></span> <span data-ttu-id="9a99f-109">Если у вас еще нет подписки Azure, создайте [бесплатную учетную запись](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начать работу.</span><span class="sxs-lookup"><span data-stu-id="9a99f-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="9a99f-110">Создание приложения-функции Azure</span><span class="sxs-lookup"><span data-stu-id="9a99f-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Приложение-функция успешно создана.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="9a99f-112">Затем создайте функцию в новом приложении-функции.</span><span class="sxs-lookup"><span data-stu-id="9a99f-112">Next, you create a function in the new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-blob-storage-triggered-function"></a><span data-ttu-id="9a99f-113">Создание функции, активируемой хранилищем BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="9a99f-113">Create a Blob storage triggered function</span></span>

1. <span data-ttu-id="9a99f-114">Разверните приложение-функцию и нажмите кнопку **+** рядом с элементом **Функции**.</span><span class="sxs-lookup"><span data-stu-id="9a99f-114">Expand your function app and click the **+** button next to **Functions**.</span></span> <span data-ttu-id="9a99f-115">Если это первая функция в приложении-функции, выберите **Пользовательская функция**.</span><span class="sxs-lookup"><span data-stu-id="9a99f-115">If this is the first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="9a99f-116">Откроется полный набор шаблонов функций.</span><span class="sxs-lookup"><span data-stu-id="9a99f-116">This displays the complete set of function templates.</span></span>

    ![Страница быстрого начала работы с функциями на портале Azure](./media/functions-create-storage-blob-triggered-function/add-first-function.png)

2. <span data-ttu-id="9a99f-118">Выберите шаблон **BlobTrigger** для нужного языка и используйте параметры, как указано в таблице.</span><span class="sxs-lookup"><span data-stu-id="9a99f-118">Select the **BlobTrigger** template for your desired language, and use the settings as specified in the table.</span></span>

    ![Создание функции, активируемой хранилищем BLOB-объектов.](./media/functions-create-storage-blob-triggered-function/functions-create-blob-storage-trigger-portal.png)

    | <span data-ttu-id="9a99f-120">Настройка</span><span class="sxs-lookup"><span data-stu-id="9a99f-120">Setting</span></span> | <span data-ttu-id="9a99f-121">Рекомендуемое значение</span><span class="sxs-lookup"><span data-stu-id="9a99f-121">Suggested value</span></span> | <span data-ttu-id="9a99f-122">Описание</span><span class="sxs-lookup"><span data-stu-id="9a99f-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="9a99f-123">**Путь**</span><span class="sxs-lookup"><span data-stu-id="9a99f-123">**Path**</span></span>   | <span data-ttu-id="9a99f-124">mycontainer/{name}</span><span class="sxs-lookup"><span data-stu-id="9a99f-124">mycontainer/{name}</span></span>    | <span data-ttu-id="9a99f-125">Расположение в хранилище BLOB-объектов отслеживается.</span><span class="sxs-lookup"><span data-stu-id="9a99f-125">Location in Blob storage being monitored.</span></span> <span data-ttu-id="9a99f-126">Имя файла большого двоичного объекта передается в привязке как параметр _name_.</span><span class="sxs-lookup"><span data-stu-id="9a99f-126">The file name of the blob is passed in the binding as the _name_ parameter.</span></span>  |
    | <span data-ttu-id="9a99f-127">**Подключение к учетной записи хранения**</span><span class="sxs-lookup"><span data-stu-id="9a99f-127">**Storage account connection**</span></span> | <span data-ttu-id="9a99f-128">AzureWebJobStorage</span><span class="sxs-lookup"><span data-stu-id="9a99f-128">AzureWebJobStorage</span></span> | <span data-ttu-id="9a99f-129">Вы можете использовать подключение к учетной записи хранения, которое уже используется вашим приложением-функцией, или создать его.</span><span class="sxs-lookup"><span data-stu-id="9a99f-129">You can use the storage account connection already being used by your function app, or create a new one.</span></span>  |
    | <span data-ttu-id="9a99f-130">**Имя функции**</span><span class="sxs-lookup"><span data-stu-id="9a99f-130">**Name your function**</span></span> | <span data-ttu-id="9a99f-131">Уникальное для вашего приложения-функции</span><span class="sxs-lookup"><span data-stu-id="9a99f-131">Unique in your function app</span></span> | <span data-ttu-id="9a99f-132">Имя функции, активируемой большим двоичным объектом.</span><span class="sxs-lookup"><span data-stu-id="9a99f-132">Name of this blob triggered function.</span></span> |

3. <span data-ttu-id="9a99f-133">Щелкните **Создать**, чтобы создать функцию.</span><span class="sxs-lookup"><span data-stu-id="9a99f-133">Click **Create** to create your function.</span></span>

<span data-ttu-id="9a99f-134">Затем необходимо подключится к своей учетной записи хранения Azure и создать контейнер **mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="9a99f-134">Next, you connect to your Azure Storage account and create the **mycontainer** container.</span></span>

## <a name="create-the-container"></a><span data-ttu-id="9a99f-135">Создание контейнера</span><span class="sxs-lookup"><span data-stu-id="9a99f-135">Create the container</span></span>

1. <span data-ttu-id="9a99f-136">Щелкните **Интегрировать** в своей функции, затем разверните узел **Документация** и скопируйте **имя учетной записи** и **ключ учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="9a99f-136">In your function, click **Integrate**, expand **Documentation**, and copy both **Account name** and **Account key**.</span></span> <span data-ttu-id="9a99f-137">Эти учетные данные используются для подключения к учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="9a99f-137">You use these credentials to connect to the storage account.</span></span> <span data-ttu-id="9a99f-138">Если вы уже подключились к учетной записи хранения, перейдите к шагу 4.</span><span class="sxs-lookup"><span data-stu-id="9a99f-138">If you have already connected your storage account, skip to step 4.</span></span>

    ![Получение учетных данных для подключения к учетной записи хранения.](./media/functions-create-storage-blob-triggered-function/functions-storage-account-connection.png)

1. <span data-ttu-id="9a99f-140">Запустите инструмент [Обозреватель службы хранилища Microsoft Azure](http://storageexplorer.com/), щелкните значок подключения слева, выберите **Use a storage account name and key** (Использовать имя и ключ учетной записи хранения), а затем щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="9a99f-140">Run the [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, click the connect icon on the left, choose **Use a storage account name and key**, and click **Next**.</span></span>

    ![Запуск инструмента "Обозреватель учетной записи хранения"](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-1.png)

1. <span data-ttu-id="9a99f-142">Введите **имя учетной записи** и **ключ учетной записи** из шага 1, щелкните **Далее**, а затем — **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="9a99f-142">Enter the **Account name** and **Account key** from step 1, click **Next** and then **Connect**.</span></span> 

    ![Введите учетные данные хранилища и подключитесь.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-2.png)

1. <span data-ttu-id="9a99f-144">Разверните подключенные учетную запись хранения, щелкните правой кнопкой мыши **Blob containers** (Контейнеры больших двоичных объектов), а затем щелкните **Create blob container** (Создать контейнер больших двоичных объектов), введите `mycontainer` и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="9a99f-144">Expand the attached storage account, right-click **Blob containers**, click **Create blob container**, type `mycontainer`, and then press enter.</span></span>

    ![Создание очереди службы хранилища](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-create-blob-container.png)

<span data-ttu-id="9a99f-146">Теперь, когда у вас есть контейнер больших двоичных объектов, вы можете проверить функцию, отправив файл в контейнер.</span><span class="sxs-lookup"><span data-stu-id="9a99f-146">Now that you have a blob container, you can test the function by uploading a file to the container.</span></span>

## <a name="test-the-function"></a><span data-ttu-id="9a99f-147">Проверка функции</span><span class="sxs-lookup"><span data-stu-id="9a99f-147">Test the function</span></span>

1. <span data-ttu-id="9a99f-148">На портале Azure перейдите к вашей функции, в нижней части страницы разверните **Журналы** и убедитесь, что потоковая передача журналов не остановлена.</span><span class="sxs-lookup"><span data-stu-id="9a99f-148">Back in the Azure portal, browse to your function expand the **Logs** at the bottom of the page and make sure that log streaming isn't paused.</span></span>

1. <span data-ttu-id="9a99f-149">В обозревателе хранилищ разверните вашу учетную запись хранения, **Blob containers** (Контейнеры больших двоичных объектов) и **mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="9a99f-149">In Storage Explorer, expand your storage account, **Blob containers**, and **mycontainer**.</span></span> <span data-ttu-id="9a99f-150">Щелкните **Отправка**, а затем **Отправка файлов**.</span><span class="sxs-lookup"><span data-stu-id="9a99f-150">Click **Upload** and then **Upload files...**.</span></span>

    ![Отправьте файл в контейнер больших двоичных объектов.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-upload-file-blob.png)

1. <span data-ttu-id="9a99f-152">В диалоговом окне **Отправка файлов** щелкните поле **Файлы**.</span><span class="sxs-lookup"><span data-stu-id="9a99f-152">In the **Upload files** dialog box, click the **Files** field.</span></span> <span data-ttu-id="9a99f-153">Перейдите к файлу на вашем локальном компьютере, например к файлу изображения, выберите его и щелкните **Открыть**, а затем **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="9a99f-153">Browse to a file on your local computer, such as an image file, select it and click **Open** and then **Upload**.</span></span>

1. <span data-ttu-id="9a99f-154">Вернитесь к журналам функции и убедитесь, что большой двоичный объект был считан.</span><span class="sxs-lookup"><span data-stu-id="9a99f-154">Go back to your function logs and verify that the blob has been read.</span></span>

   ![Просмотр сообщения в журналах](./media/functions-create-storage-blob-triggered-function/functions-blob-storage-trigger-view-logs.png)

    >[!NOTE]
    > <span data-ttu-id="9a99f-156">Если ваше приложение-функция выполняется в рамках плана потребления по умолчанию, между добавлением или обновлением большого двоичного объекта и активацией функции могут возникнуть задержки до нескольких минут.</span><span class="sxs-lookup"><span data-stu-id="9a99f-156">When your function app runs in the default Consumption plan, there may be a delay of up to several minutes between the blob being added or updated and the function being triggered.</span></span> <span data-ttu-id="9a99f-157">Выполняйте свое приложение-функцию в рамках плана службы приложений, если требуется малая задержка в функции, активируемой большим двоичным объектом.</span><span class="sxs-lookup"><span data-stu-id="9a99f-157">If you need low latency in your blob triggered functions, consider running your function app in an App Service plan.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="9a99f-158">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="9a99f-158">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="9a99f-159">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9a99f-159">Next steps</span></span>

<span data-ttu-id="9a99f-160">Вы создали функцию, которая выполняется при добавлении или обновлении большого двоичного объекта в хранилище BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="9a99f-160">You have created a function that runs when a blob is added to or updated in Blob storage.</span></span> 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="9a99f-161">Дополнительные сведения о триггерах хранилища BLOB-объектов см.в статье [Привязки больших двоичных объектов службы хранилища для Функций Azure](functions-bindings-storage-blob.md).</span><span class="sxs-lookup"><span data-stu-id="9a99f-161">For more information about Blob storage triggers, see [Azure Functions Blob storage bindings](functions-bindings-storage-blob.md).</span></span>
