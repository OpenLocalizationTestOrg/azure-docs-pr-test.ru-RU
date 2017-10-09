---
title: "aaaStream данные из Stream Analytics в хранилище Озера данных | Документы Microsoft"
description: "Использование Azure Stream Analytics toostream данных в хранилище Озера данных Azure"
services: data-lake-store,stream-analytics
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: edb58e0b-311f-44b0-a499-04d7e6c07a90
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 68c727d4807db0abe6efa90145d68c78902eb789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="stream-data-from-azure-storage-blob-into-data-lake-store-using-azure-stream-analytics"></a><span data-ttu-id="94e95-103">Потоковая передача данных из большого двоичного объекта службы хранилища Azure в хранилище озера данных с помощью Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="94e95-103">Stream data from Azure Storage Blob into Data Lake Store using Azure Stream Analytics</span></span>
<span data-ttu-id="94e95-104">В этой статье вы узнаете, как toouse Azure Озера данных хранения в качестве выходных данных для задания Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="94e95-104">In this article you will learn how toouse Azure Data Lake Store as an output for an Azure Stream Analytics job.</span></span> <span data-ttu-id="94e95-105">В этой статье демонстрируется простой сценарий, который считывает данные из большого двоичного объекта хранилища Azure (input) и записывает hello хранилища Озера данных tooData (output).</span><span class="sxs-lookup"><span data-stu-id="94e95-105">This article demonstrates a simple scenario that reads data from an Azure Storage blob (input) and writes hello data tooData Lake Store (output).</span></span>

> [!NOTE]
> <span data-ttu-id="94e95-106">В настоящее время создание и Настройка хранилища Озера данных выводит для Stream Analytics поддерживается только в hello [классический портал Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="94e95-106">At this time, creation and configuration of Data Lake Store outputs for Stream Analytics is supported only in hello [Azure Classic Portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="94e95-107">Таким образом некоторые части этого учебника будет использовать hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="94e95-107">Hence, some parts of this tutorial will use hello Azure Classic Portal.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="94e95-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="94e95-108">Prerequisites</span></span>
<span data-ttu-id="94e95-109">Прежде чем начать работу с учебником, необходимо иметь следующие hello.</span><span class="sxs-lookup"><span data-stu-id="94e95-109">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="94e95-110">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="94e95-110">**An Azure subscription**.</span></span> <span data-ttu-id="94e95-111">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="94e95-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="94e95-112">**Учетная запись хранения Azure.**</span><span class="sxs-lookup"><span data-stu-id="94e95-112">**Azure Storage account**.</span></span> <span data-ttu-id="94e95-113">Контейнер больших двоичных объектов на основе данных tooinput учетная запись используется для задания Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="94e95-113">You will use a blob container from this account tooinput data for a Stream Analytics job.</span></span> <span data-ttu-id="94e95-114">Для этого учебника Предположим, что учетную запись хранилища **storageforasa** и именем контейнера в учетной записи hello **storageforasacontainer**.</span><span class="sxs-lookup"><span data-stu-id="94e95-114">For this tutorial, assume you have a storage account called **storageforasa** and a container within hello account called **storageforasacontainer**.</span></span> <span data-ttu-id="94e95-115">После создания контейнера hello, отправьте файл tooit образца данных.</span><span class="sxs-lookup"><span data-stu-id="94e95-115">Once you have created hello container, upload a sample data file tooit.</span></span> 
  
* <span data-ttu-id="94e95-116">**Учетная запись хранилища озера данных Azure**.</span><span class="sxs-lookup"><span data-stu-id="94e95-116">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="94e95-117">Следуйте инструкциям hello в [Приступая к работе с хранилища Озера данных Azure, с помощью портала Azure hello](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="94e95-117">Follow hello instructions at [Get started with Azure Data Lake Store using hello Azure Portal](data-lake-store-get-started-portal.md).</span></span> <span data-ttu-id="94e95-118">Предположим, у вас есть учетная запись хранилища Data Lake Store **asadatalakestore**.</span><span class="sxs-lookup"><span data-stu-id="94e95-118">Let's assume you have a Data Lake Store account called **asadatalakestore**.</span></span> 

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="94e95-119">Создание задания Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="94e95-119">Create a Stream Analytics Job</span></span>
<span data-ttu-id="94e95-120">Для начала нужно создать задание Stream Analytics с источником входных данных и целевым объектом для выходных данных.</span><span class="sxs-lookup"><span data-stu-id="94e95-120">You start by creating a Stream Analytics job that includes an input source and an output destination.</span></span> <span data-ttu-id="94e95-121">В этом учебнике hello источник представляет собой контейнер больших двоичных объектов Azure и назначение hello — хранилище Озера данных.</span><span class="sxs-lookup"><span data-stu-id="94e95-121">For this tutorial, hello source is an Azure blob container and hello destination is Data Lake Store.</span></span>

1. <span data-ttu-id="94e95-122">Войдите на toohello [портала Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="94e95-122">Sign on toohello [Azure Portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="94e95-123">Hello левой панели щелкните **заданий Stream Analytics**, а затем нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="94e95-123">From hello left pane, click **Stream Analytics jobs**, and then click **Add**.</span></span>

    <span data-ttu-id="94e95-124">![Создание задания Stream Analytics](./media/data-lake-store-stream-analytics/create.job.png "Создание задания Stream Analytics")</span><span class="sxs-lookup"><span data-stu-id="94e95-124">![Create a Stream Analytics Job](./media/data-lake-store-stream-analytics/create.job.png "Create a Stream Analytics job")</span></span>

    > [!NOTE]
    > <span data-ttu-id="94e95-125">Убедитесь, что создание задания в hello же регионе, что учетная запись хранения hello, или вы повлечет за собой дополнительные затраты на перемещение данных между регионами.</span><span class="sxs-lookup"><span data-stu-id="94e95-125">Make sure you create job in hello same region as hello storage account or you will incur additional cost of moving data between regions.</span></span>
    >

## <a name="create-a-blob-input-for-hello-job"></a><span data-ttu-id="94e95-126">Создание входных данных больших двоичных объектов для задания hello</span><span class="sxs-lookup"><span data-stu-id="94e95-126">Create a Blob input for hello job</span></span>

1. <span data-ttu-id="94e95-127">Привет открыть страницу для задания Stream Analytics hello, hello левой панели щелкните hello **входов** , а затем щелкните **добавить**.</span><span class="sxs-lookup"><span data-stu-id="94e95-127">Open hello page for hello Stream Analytics job, from hello left pane click hello **Inputs** tab, and then click **Add**.</span></span>

    <span data-ttu-id="94e95-128">![Добавьте задание входных tooyour](./media/data-lake-store-stream-analytics/create.input.1.png "добавить задание входных tooyour")</span><span class="sxs-lookup"><span data-stu-id="94e95-128">![Add an input tooyour job](./media/data-lake-store-stream-analytics/create.input.1.png "Add an input tooyour job")</span></span>

2. <span data-ttu-id="94e95-129">На hello **вводимые** колонке предоставляют hello следующие значения.</span><span class="sxs-lookup"><span data-stu-id="94e95-129">On hello **New input** blade, provide hello following values.</span></span>

    <span data-ttu-id="94e95-130">![Добавьте задание входных tooyour](./media/data-lake-store-stream-analytics/create.input.2.png "добавить задание входных tooyour")</span><span class="sxs-lookup"><span data-stu-id="94e95-130">![Add an input tooyour job](./media/data-lake-store-stream-analytics/create.input.2.png "Add an input tooyour job")</span></span>

    * <span data-ttu-id="94e95-131">Для **входных псевдонимов**, введите уникальное имя для входных данных задания hello.</span><span class="sxs-lookup"><span data-stu-id="94e95-131">For **Input alias**, enter a unique name for hello job input.</span></span>
    * <span data-ttu-id="94e95-132">**Тип источника** — выберите **Поток данных**.</span><span class="sxs-lookup"><span data-stu-id="94e95-132">For **Source type**, select **Data stream**.</span></span>
    * <span data-ttu-id="94e95-133">**Источник** — выберите **Хранилище больших двоичных объектов**.</span><span class="sxs-lookup"><span data-stu-id="94e95-133">For **Source**, select **Blob storage**.</span></span>
    * <span data-ttu-id="94e95-134">**Подписка** — выберите **Использовать хранилище BLOB-объектов из текущей подписки**.</span><span class="sxs-lookup"><span data-stu-id="94e95-134">For **Subscription**, select **Use blob storage from current subscription**.</span></span>
    * <span data-ttu-id="94e95-135">Для **учетной записи хранилища**, выберите учетную запись хранения hello, созданный в рамках hello необходимых компонентов.</span><span class="sxs-lookup"><span data-stu-id="94e95-135">For **Storage account**, select hello storage account that you created as part of hello prerequisites.</span></span> 
    * <span data-ttu-id="94e95-136">Для **контейнера**выберите контейнер hello, созданную в hello выбранную учетную запись хранилища.</span><span class="sxs-lookup"><span data-stu-id="94e95-136">For **Container**, select hello container that you created in hello selected storage account.</span></span>
    * <span data-ttu-id="94e95-137">**Формат сериализации событий** — выберите **CSV**.</span><span class="sxs-lookup"><span data-stu-id="94e95-137">For **Event serialization format**, select **CSV**.</span></span>
    * <span data-ttu-id="94e95-138">**Разделитель** — выберите **Табуляция**.</span><span class="sxs-lookup"><span data-stu-id="94e95-138">For **Delimiter**, select **tab**.</span></span>
    * <span data-ttu-id="94e95-139">**Кодировка** — выберите **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="94e95-139">For **Encoding**, select **UTF-8**.</span></span>

    <span data-ttu-id="94e95-140">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="94e95-140">Click **Create**.</span></span> <span data-ttu-id="94e95-141">портал Hello теперь добавляет hello входных данных и проверяет подключение tooit hello.</span><span class="sxs-lookup"><span data-stu-id="94e95-141">hello portal now adds hello input and tests hello connection tooit.</span></span>


## <a name="create-a-data-lake-store-output-for-hello-job"></a><span data-ttu-id="94e95-142">Создание хранилища Озера данных вывода для задания hello</span><span class="sxs-lookup"><span data-stu-id="94e95-142">Create a Data Lake Store output for hello job</span></span>

1. <span data-ttu-id="94e95-143">Откройте страницу приветствия для задания Stream Analytics hello, щелкните hello **выходов** , а затем щелкните **добавить**.</span><span class="sxs-lookup"><span data-stu-id="94e95-143">Open hello page for hello Stream Analytics job, click hello **Outputs** tab, and then click **Add**.</span></span>

    <span data-ttu-id="94e95-144">![Добавьте Задание вывода tooyour](./media/data-lake-store-stream-analytics/create.output.1.png "добавить задание tooyour выходных данных")</span><span class="sxs-lookup"><span data-stu-id="94e95-144">![Add an output tooyour job](./media/data-lake-store-stream-analytics/create.output.1.png "Add an output tooyour job")</span></span>

2. <span data-ttu-id="94e95-145">На hello **новый Выход** колонке предоставляют hello следующие значения.</span><span class="sxs-lookup"><span data-stu-id="94e95-145">On hello **New output** blade, provide hello following values.</span></span>

    <span data-ttu-id="94e95-146">![Добавьте Задание вывода tooyour](./media/data-lake-store-stream-analytics/create.output.2.png "добавить задание tooyour выходных данных")</span><span class="sxs-lookup"><span data-stu-id="94e95-146">![Add an output tooyour job](./media/data-lake-store-stream-analytics/create.output.2.png "Add an output tooyour job")</span></span>

    * <span data-ttu-id="94e95-147">Для **Псевдоним выхода**, введите уникальное имя для выходных данных задания hello.</span><span class="sxs-lookup"><span data-stu-id="94e95-147">For **Output alias**, enter a a unique name for hello job output.</span></span> <span data-ttu-id="94e95-148">Это понятное имя, используемое в выходных данных запроса toothis хранилища Озера данных запросов toodirect hello.</span><span class="sxs-lookup"><span data-stu-id="94e95-148">This is a friendly name used in queries toodirect hello query output toothis Data Lake Store.</span></span>
    * <span data-ttu-id="94e95-149">**Приемник** — выберите **Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="94e95-149">For **Sink**, select **Data Lake Store**.</span></span>
    * <span data-ttu-id="94e95-150">Появится запрос tooauthorize доступ к учетной записи хранилища Озера tooData.</span><span class="sxs-lookup"><span data-stu-id="94e95-150">You will be prompted tooauthorize access tooData Lake Store account.</span></span> <span data-ttu-id="94e95-151">Щелкните **Авторизовать**.</span><span class="sxs-lookup"><span data-stu-id="94e95-151">Click **Authorize**.</span></span>

3. <span data-ttu-id="94e95-152">На hello **новый Выход** колонке продолжить hello tooprovide следующие значения.</span><span class="sxs-lookup"><span data-stu-id="94e95-152">On hello **New output** blade, continue tooprovide hello following values.</span></span>

    <span data-ttu-id="94e95-153">![Добавьте Задание вывода tooyour](./media/data-lake-store-stream-analytics/create.output.3.png "добавить задание tooyour выходных данных")</span><span class="sxs-lookup"><span data-stu-id="94e95-153">![Add an output tooyour job](./media/data-lake-store-stream-analytics/create.output.3.png "Add an output tooyour job")</span></span>

    * <span data-ttu-id="94e95-154">Для **имя учетной записи**, выберите учетную запись хранилища Озера данных hello, уже созданных место toobe выходные данные задания hello, отправляемые.</span><span class="sxs-lookup"><span data-stu-id="94e95-154">For **Account name**, select hello Data Lake Store account you already created where you want hello job output toobe sent to.</span></span>
    * <span data-ttu-id="94e95-155">Для **шаблон префикс пути**, введите путь, используемый файл toowrite файлов в пределах hello указанного хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="94e95-155">For **Path prefix pattern**, enter a file path used toowrite your files within hello specified Data Lake Store account.</span></span>
    * <span data-ttu-id="94e95-156">Для **формат даты**, если вы использовали токен даты hello префикс пути, можно выбрать формат даты hello, в котором упорядочены файлов.</span><span class="sxs-lookup"><span data-stu-id="94e95-156">For **Date format**, if you used a date token in hello prefix path, you can select hello date format in which your files are organized.</span></span>
    * <span data-ttu-id="94e95-157">Для **формат времени**, если вы использовали токен времени hello префикс пути, укажите формат времени hello, в котором упорядочены файлов.</span><span class="sxs-lookup"><span data-stu-id="94e95-157">For **Time format**, if you used a time token in hello prefix path, specify hello time format in which your files are organized.</span></span>
    * <span data-ttu-id="94e95-158">**Формат сериализации событий** — выберите **CSV**.</span><span class="sxs-lookup"><span data-stu-id="94e95-158">For **Event serialization format**, select **CSV**.</span></span>
    * <span data-ttu-id="94e95-159">**Разделитель** — выберите **Табуляция**.</span><span class="sxs-lookup"><span data-stu-id="94e95-159">For **Delimiter**, select **tab**.</span></span>
    * <span data-ttu-id="94e95-160">**Кодировка** — выберите **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="94e95-160">For **Encoding**, select **UTF-8**.</span></span>
    
    <span data-ttu-id="94e95-161">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="94e95-161">Click **Create**.</span></span> <span data-ttu-id="94e95-162">портал Hello теперь добавляет выход hello и проверяет подключение tooit hello.</span><span class="sxs-lookup"><span data-stu-id="94e95-162">hello portal now adds hello output and tests hello connection tooit.</span></span>
    
## <a name="run-hello-stream-analytics-job"></a><span data-ttu-id="94e95-163">Запустить задание Stream Analytics hello</span><span class="sxs-lookup"><span data-stu-id="94e95-163">Run hello Stream Analytics job</span></span>

1. <span data-ttu-id="94e95-164">toorun задания Stream Analytics, необходимо выполнить запрос из hello **запроса** вкладки. В этом учебнике, можно выполнить запрос образец hello, заменив заполнители hello hello задания входных и выходных псевдонимов, как показано на снимке экрана приветствия ниже.</span><span class="sxs-lookup"><span data-stu-id="94e95-164">toorun a Stream Analytics job, you must run a query from hello **Query** tab. For this tutorial, you can run hello sample query by replacing hello placeholders with hello job input and output aliases, as shown in hello screen capture below.</span></span>

    <span data-ttu-id="94e95-165">![Выполнение запроса](./media/data-lake-store-stream-analytics/run.query.png "Выполнение запроса")</span><span class="sxs-lookup"><span data-stu-id="94e95-165">![Run query](./media/data-lake-store-stream-analytics/run.query.png "Run query")</span></span>

2. <span data-ttu-id="94e95-166">Нажмите кнопку **Сохранить** от hello в верхней части экрана приветствия, а затем из hello **Обзор** щелкните **запустить**.</span><span class="sxs-lookup"><span data-stu-id="94e95-166">Click **Save** from hello top of hello screen, and then from hello **Overview** tab, click **Start**.</span></span> <span data-ttu-id="94e95-167">В диалоговом окне приветствия выберите **время пользовательского**и задайте hello текущую дату и время.</span><span class="sxs-lookup"><span data-stu-id="94e95-167">From hello dialog box, select **Custom Time**, and then set hello current date and time.</span></span>

    <span data-ttu-id="94e95-168">![Установка времени задания](./media/data-lake-store-stream-analytics/run.query.2.png "Установка времени задания")</span><span class="sxs-lookup"><span data-stu-id="94e95-168">![Set job time](./media/data-lake-store-stream-analytics/run.query.2.png "Set job time")</span></span>

    <span data-ttu-id="94e95-169">Нажмите кнопку **запустить** toostart hello задания.</span><span class="sxs-lookup"><span data-stu-id="94e95-169">Click **Start** toostart hello job.</span></span> <span data-ttu-id="94e95-170">Он может занять tooa пару минут toostart hello задания.</span><span class="sxs-lookup"><span data-stu-id="94e95-170">It can take up tooa couple minutes toostart hello job.</span></span>

3. <span data-ttu-id="94e95-171">данные tootrigger hello задания toopick hello из большого двоичного объекта hello, скопируйте toohello файла образца данных BLOB-контейнере.</span><span class="sxs-lookup"><span data-stu-id="94e95-171">tootrigger hello job toopick hello data from hello blob, copy a sample data file toohello blob container.</span></span> <span data-ttu-id="94e95-172">Образец файла данных можно получить из hello [репозитории Озера данных Azure](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).</span><span class="sxs-lookup"><span data-stu-id="94e95-172">You can get a sample data file from hello [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).</span></span> <span data-ttu-id="94e95-173">В этом учебнике, давайте скопируйте файл hello **vehicle1_09142014.csv**.</span><span class="sxs-lookup"><span data-stu-id="94e95-173">For this tutorial, let's copy hello file **vehicle1_09142014.csv**.</span></span> <span data-ttu-id="94e95-174">Можно использовать различные клиенты, такие как [обозреватель хранилищ Azure](http://storageexplorer.com/), контейнер больших двоичных объектов tooa tooupload данных.</span><span class="sxs-lookup"><span data-stu-id="94e95-174">You can use various clients, such as [Azure Storage Explorer](http://storageexplorer.com/), tooupload data tooa blob container.</span></span>

4. <span data-ttu-id="94e95-175">Из hello **Обзор** в разделе **мониторинг**, обработкой данных hello в разделе.</span><span class="sxs-lookup"><span data-stu-id="94e95-175">From hello **Overview** tab, under **Monitoring**, see how hello data was processed.</span></span>

    <span data-ttu-id="94e95-176">![Мониторинг задания](./media/data-lake-store-stream-analytics/run.query.3.png "Мониторинг задания")</span><span class="sxs-lookup"><span data-stu-id="94e95-176">![Monitor job](./media/data-lake-store-stream-analytics/run.query.3.png "Monitor job")</span></span>

5. <span data-ttu-id="94e95-177">Наконец можно проверить, что выходные данные задания hello доступен в учетной записи хранилища Озера данных hello.</span><span class="sxs-lookup"><span data-stu-id="94e95-177">Finally, you can verify that hello job output data is available in hello Data Lake Store account.</span></span> 

    <span data-ttu-id="94e95-178">![Проверка выходных данных](./media/data-lake-store-stream-analytics/run.query.4.png "Проверка выходных данных")</span><span class="sxs-lookup"><span data-stu-id="94e95-178">![Verify output](./media/data-lake-store-stream-analytics/run.query.4.png "Verify output")</span></span>

    <span data-ttu-id="94e95-179">Панели обозревателя данных hello, обратите внимание на то, что hello вывода письменного tooa путь к папке, как указывается в hello хранилища Озера данных параметры вывода (`streamanalytics/job/output/{date}/{time}`).</span><span class="sxs-lookup"><span data-stu-id="94e95-179">In hello Data Explorer pane, notice that hello output is written tooa folder path as specified in hello Data Lake Store output settings (`streamanalytics/job/output/{date}/{time}`).</span></span>  

## <a name="see-also"></a><span data-ttu-id="94e95-180">См. также</span><span class="sxs-lookup"><span data-stu-id="94e95-180">See also</span></span>
* [<span data-ttu-id="94e95-181">Создание toouse кластера HDInsight хранилища Озера данных</span><span class="sxs-lookup"><span data-stu-id="94e95-181">Create an HDInsight cluster toouse Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
