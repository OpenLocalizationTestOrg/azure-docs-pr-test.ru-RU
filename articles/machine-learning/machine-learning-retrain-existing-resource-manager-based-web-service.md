---
title: "существующий прогнозной aaaRetrain веб-службы | Документы Microsoft"
description: "Узнайте, как tooretrain модели и обновление hello web toouse службы hello вновь обученной модели машинного обучения Azure."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: cc4c26a2-5672-4255-a767-cfd971e46775
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: v-donglo
ms.openlocfilehash: fb0760d0a2adc34fc5f3df1ae41bdac075f91bf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-an-existing-predictive-web-service"></a><span data-ttu-id="c28b6-103">Переобучение прогнозной веб-службы</span><span class="sxs-lookup"><span data-stu-id="c28b6-103">Retrain an existing predictive web service</span></span>
<span data-ttu-id="c28b6-104">В этом документе описываются hello переподготовки процесс для hello следующие сценарии:</span><span class="sxs-lookup"><span data-stu-id="c28b6-104">This document describes hello retraining process for hello following scenario:</span></span>

* <span data-ttu-id="c28b6-105">Есть обучающий и прогнозный эксперименты, развернутые в качестве веб-службы, готовой к эксплуатации.</span><span class="sxs-lookup"><span data-stu-id="c28b6-105">You have a training experiment and a predictive experiment that you have deployed as an operationalized web service.</span></span>
* <span data-ttu-id="c28b6-106">У вас есть новые данные, которые должны вашей прогнозной web service toouse tooperform его оценки.</span><span class="sxs-lookup"><span data-stu-id="c28b6-106">You have new data that you want your predictive web service toouse tooperform its scoring.</span></span>

> [!NOTE] 
> <span data-ttu-id="c28b6-107">toodeploy новую веб-службу, необходимо иметь достаточные разрешения в toowhich hello подписки вы развертывание hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="c28b6-107">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="c28b6-108">Дополнительные сведения см. в разделе [управление веб-службы с помощью портала веб-службы Azure Machine Learning hello](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="c28b6-108">For more information see, [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="c28b6-109">Начиная с существующей веб-службы и экспериментов, требуется toofollow следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c28b6-109">Starting with your existing web service and experiments, you need toofollow these steps:</span></span>

1. <span data-ttu-id="c28b6-110">Обновление модели hello.</span><span class="sxs-lookup"><span data-stu-id="c28b6-110">Update hello model.</span></span>
   1. <span data-ttu-id="c28b6-111">Измените ваш tooallow эксперимента обучения для web service входов и выходов.</span><span class="sxs-lookup"><span data-stu-id="c28b6-111">Modify your training experiment tooallow for web service inputs and outputs.</span></span>
   2. <span data-ttu-id="c28b6-112">Развертывание эксперимента обучения hello повторную веб-службы.</span><span class="sxs-lookup"><span data-stu-id="c28b6-112">Deploy hello training experiment as a retraining web service.</span></span>
   3. <span data-ttu-id="c28b6-113">Модель эксперимента обучения hello пакетного выполнения службы (BES) tooretrain hello.</span><span class="sxs-lookup"><span data-stu-id="c28b6-113">Use hello training experiment's Batch Execution Service (BES) tooretrain hello model.</span></span>
2. <span data-ttu-id="c28b6-114">Используйте прогнозирующее эксперимента hello Azure Machine Learning PowerShell командлеты tooupdate hello.</span><span class="sxs-lookup"><span data-stu-id="c28b6-114">Use hello Azure Machine Learning PowerShell cmdlets tooupdate hello predictive experiment.</span></span>
   1. <span data-ttu-id="c28b6-115">Войдите в tooyour учетной записи диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="c28b6-115">Sign in tooyour Azure Resource Manager account.</span></span>
   2. <span data-ttu-id="c28b6-116">Получите определение hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="c28b6-116">Get hello web service definition.</span></span>
   3. <span data-ttu-id="c28b6-117">Экспорт определения hello веб-службы как JSON.</span><span class="sxs-lookup"><span data-stu-id="c28b6-117">Export hello web service definition as JSON.</span></span>
   4. <span data-ttu-id="c28b6-118">Обновление hello ссылка toohello ilearner большой двоичный объект в hello JSON.</span><span class="sxs-lookup"><span data-stu-id="c28b6-118">Update hello reference toohello ilearner blob in hello JSON.</span></span>
   5. <span data-ttu-id="c28b6-119">Импортируйте hello JSON в определении веб-службы.</span><span class="sxs-lookup"><span data-stu-id="c28b6-119">Import hello JSON into a web service definition.</span></span>
   6. <span data-ttu-id="c28b6-120">Обновите hello веб-службы с помощью нового определения веб-службы.</span><span class="sxs-lookup"><span data-stu-id="c28b6-120">Update hello web service with a new web service definition.</span></span>

## <a name="deploy-hello-training-experiment"></a><span data-ttu-id="c28b6-121">Разверните эксперимент обучения hello</span><span class="sxs-lookup"><span data-stu-id="c28b6-121">Deploy hello training experiment</span></span>
<span data-ttu-id="c28b6-122">toodeploy эксперимента обучения hello повторную веб-службы, необходимо добавить модели веб-служб входы и выходы toohello.</span><span class="sxs-lookup"><span data-stu-id="c28b6-122">toodeploy hello training experiment as a retraining web service, you must add web service inputs and outputs toohello model.</span></span> <span data-ttu-id="c28b6-123">Подключив *вывод веб-службы* toohello эксперименте модуль  *[Обучение модели] [ train-model]*  модуля, включите hello эксперимента обучения tooproduce новый обученную модель, которую можно использовать в эксперименте прогнозирования.</span><span class="sxs-lookup"><span data-stu-id="c28b6-123">By connecting a *Web Service Output* module toohello experiment's *[Train Model][train-model]* module, you enable hello training experiment tooproduce a new trained model that you can use in your predictive experiment.</span></span> <span data-ttu-id="c28b6-124">Если у вас есть *модель оценки* модуля, вы также можете присоединить web service вывода tooget hello результаты оценки в качестве выходных данных.</span><span class="sxs-lookup"><span data-stu-id="c28b6-124">If you have an *Evaluate Model* module, you can also attach web service output tooget hello evaluation results as output.</span></span>

<span data-ttu-id="c28b6-125">tooupdate эксперимента обучения:</span><span class="sxs-lookup"><span data-stu-id="c28b6-125">tooupdate your training experiment:</span></span>

1. <span data-ttu-id="c28b6-126">Подключения *Web Service входной* данные tooyour модуля ввода (например, *Очистка недостающих данных* модуля).</span><span class="sxs-lookup"><span data-stu-id="c28b6-126">Connect a *Web Service Input* module tooyour data input (for example, a *Clean Missing Data* module).</span></span> <span data-ttu-id="c28b6-127">Как правило, требуется tooensure, обрабатываемых в качестве входных данных hello таким же, как и исходный обучающих данных.</span><span class="sxs-lookup"><span data-stu-id="c28b6-127">Typically, you want tooensure that your input data is processed in hello same way as your original training data.</span></span>
2. <span data-ttu-id="c28b6-128">Подключение *вывод веб-службы* выходные данные модуля toohello из вашего *Обучение модели* модуля.</span><span class="sxs-lookup"><span data-stu-id="c28b6-128">Connect a *Web Service Output* module toohello output of your *Train Model* module.</span></span>
3. <span data-ttu-id="c28b6-129">При наличии *модель оценки* модуля вы результаты оценки toooutput hello, необходимо подключиться *вывод веб-службы* выходные данные модуля toohello из вашего *модель оценки* модуль.</span><span class="sxs-lookup"><span data-stu-id="c28b6-129">If you have an *Evaluate Model* module and you want toooutput hello evaluation results, connect a *Web Service Output* module toohello output of your *Evaluate Model* module.</span></span>

<span data-ttu-id="c28b6-130">Запустите эксперимент.</span><span class="sxs-lookup"><span data-stu-id="c28b6-130">Run your experiment.</span></span>

<span data-ttu-id="c28b6-131">После этого необходимо развернуть эксперимента обучения hello как веб-службу, которая создает обученной модели и результаты оценки модели.</span><span class="sxs-lookup"><span data-stu-id="c28b6-131">Next, you must deploy hello training experiment as a web service that produces a trained model and model evaluation results.</span></span>  

<span data-ttu-id="c28b6-132">Внизу hello холст эксперимента hello, нажмите кнопку **настройки веб-службы**и выберите **развертывания [новое] веб-службы**.</span><span class="sxs-lookup"><span data-stu-id="c28b6-132">At hello bottom of hello experiment canvas, click **Set Up Web Service**, and then select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="c28b6-133">Откроется портал веб-службы Azure Machine Learning Hello toohello **развертывание веб-службы** страницы.</span><span class="sxs-lookup"><span data-stu-id="c28b6-133">hello Azure Machine Learning Web Services portal opens toohello **Deploy Web Service** page.</span></span> <span data-ttu-id="c28b6-134">Введите имя веб-службы, выберите план платежей, а затем щелкните **Развернуть**.</span><span class="sxs-lookup"><span data-stu-id="c28b6-134">Type a name for your web service, choose a payment plan, and then click **Deploy**.</span></span> <span data-ttu-id="c28b6-135">Hello способ выполнения пакета можно использовать только для создания обученных моделей.</span><span class="sxs-lookup"><span data-stu-id="c28b6-135">You can only use hello Batch Execution method for creating trained models.</span></span>

## <a name="retrain-hello-model-with-new-data-by-using-bes"></a><span data-ttu-id="c28b6-136">Обучение модели hello новыми данными, с помощью СРЕД</span><span class="sxs-lookup"><span data-stu-id="c28b6-136">Retrain hello model with new data by using BES</span></span>
<span data-ttu-id="c28b6-137">В этом примере мы используем hello toocreate C#, переподготовки приложения.</span><span class="sxs-lookup"><span data-stu-id="c28b6-137">For this example, we're using C# toocreate hello retraining application.</span></span> <span data-ttu-id="c28b6-138">Можно также использовать Python или R tooaccomplish образец кода эта задача.</span><span class="sxs-lookup"><span data-stu-id="c28b6-138">You can also use Python or R sample code tooaccomplish this task.</span></span>

<span data-ttu-id="c28b6-139">toocall hello переподготовки API-интерфейсы:</span><span class="sxs-lookup"><span data-stu-id="c28b6-139">toocall hello retraining APIs:</span></span>

1. <span data-ttu-id="c28b6-140">Создайте консольное приложение C# в Visual Studio (**Создать** > **Проект** > **Visual C#** > **Классический рабочий стол Windows** > **Консольное приложение (.NET Framework**).</span><span class="sxs-lookup"><span data-stu-id="c28b6-140">Create a C# console application in Visual Studio: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
2. <span data-ttu-id="c28b6-141">Войдите в систему toohello портала машины обучения веб-служб.</span><span class="sxs-lookup"><span data-stu-id="c28b6-141">Sign in toohello Machine Learning Web Services portal.</span></span>
3. <span data-ttu-id="c28b6-142">Щелкните hello веб-службы, которым вы работаете.</span><span class="sxs-lookup"><span data-stu-id="c28b6-142">Click hello web service that you're working with.</span></span>
4. <span data-ttu-id="c28b6-143">Щелкните **Consume**(Использование).</span><span class="sxs-lookup"><span data-stu-id="c28b6-143">Click **Consume**.</span></span>
5. <span data-ttu-id="c28b6-144">Внизу hello hello **использование** страницы в hello **образец кода** щелкните **пакета**.</span><span class="sxs-lookup"><span data-stu-id="c28b6-144">At hello bottom of hello **Consume** page, in hello **Sample Code** section, click **Batch**.</span></span>
6. <span data-ttu-id="c28b6-145">Скопируйте hello пример кода C# для пакетного выполнения и вставьте его в файл Program.cs hello.</span><span class="sxs-lookup"><span data-stu-id="c28b6-145">Copy hello sample C# code for batch execution and paste it into hello Program.cs file.</span></span> <span data-ttu-id="c28b6-146">Убедитесь, что это пространство имен hello остается без изменений.</span><span class="sxs-lookup"><span data-stu-id="c28b6-146">Make sure that hello namespace remains intact.</span></span>

<span data-ttu-id="c28b6-147">Добавьте пакет NuGet hello Microsoft.AspNet.WebApi.Client, как указано в комментариях hello.</span><span class="sxs-lookup"><span data-stu-id="c28b6-147">Add hello NuGet package Microsoft.AspNet.WebApi.Client, as specified in hello comments.</span></span> <span data-ttu-id="c28b6-148">tooMicrosoft.WindowsAzure.Storage.dll ссылки tooadd hello, сначала необходимо tooinstall hello [клиентской библиотеки для служб хранилища Azure](https://www.nuget.org/packages/WindowsAzure.Storage).</span><span class="sxs-lookup"><span data-stu-id="c28b6-148">tooadd hello reference tooMicrosoft.WindowsAzure.Storage.dll, you might first need tooinstall hello [client library for Azure Storage services](https://www.nuget.org/packages/WindowsAzure.Storage).</span></span>

<span data-ttu-id="c28b6-149">Hello следующем снимке экрана показано hello **использование** портале веб-службы Azure Machine Learning hello.</span><span class="sxs-lookup"><span data-stu-id="c28b6-149">hello following screenshot shows hello **Consume** page in hello Azure Machine Learning Web Services portal.</span></span>

![Страница Consume (Использование)][1]

### <a name="update-hello-apikey-declaration"></a><span data-ttu-id="c28b6-151">Обновление декларации apikey hello</span><span class="sxs-lookup"><span data-stu-id="c28b6-151">Update hello apikey declaration</span></span>
<span data-ttu-id="c28b6-152">Найдите hello **apikey** объявление:</span><span class="sxs-lookup"><span data-stu-id="c28b6-152">Locate hello **apikey** declaration:</span></span>

    const string apiKey = "abc123"; // Replace this with hello API key for hello web service

<span data-ttu-id="c28b6-153">В hello **потребления основные сведения о** раздел hello **использование** найдите hello первичный ключ и скопируйте его toohello **apikey** объявления.</span><span class="sxs-lookup"><span data-stu-id="c28b6-153">In hello **Basic consumption info** section of hello **Consume** page, locate hello primary key and copy it toohello **apikey** declaration.</span></span>

### <a name="update-hello-azure-storage-information"></a><span data-ttu-id="c28b6-154">Обновить сведения о хранилище Azure hello</span><span class="sxs-lookup"><span data-stu-id="c28b6-154">Update hello Azure Storage information</span></span>
<span data-ttu-id="c28b6-155">Hello BES образец кода отправляет файл с локального диска (например, «C:\temp\CensusIpnput.csv») tooAzure хранилища, обрабатывает его и записывает hello результаты назад tooAzure хранилища.</span><span class="sxs-lookup"><span data-stu-id="c28b6-155">hello BES sample code uploads a file from a local drive (for example, "C:\temp\CensusIpnput.csv") tooAzure Storage, processes it, and writes hello results back tooAzure Storage.</span></span>  

<span data-ttu-id="c28b6-156">сведения о tooupdate hello хранилища Azure, необходимо получить hello учетной записи хранения, имя ключа и контейнер сведения для учетной записи хранения из классического портала Azure hello и correspondi hello обновления после выполнения эксперимента, Здравствуйте, возникающие в рабочий процесс должен быть примерно toohello следующее:</span><span class="sxs-lookup"><span data-stu-id="c28b6-156">tooupdate hello Azure Storage information, you must retrieve hello storage account name, key, and container information for your storage account from hello Azure classic portal, and then update hello correspondi After running your experiment, hello resulting workflow should be similar toohello following:</span></span>

![Итоговый рабочий процесс после запуска][4]<span data-ttu-id="c28b6-158">ng значения в коде hello.</span><span class="sxs-lookup"><span data-stu-id="c28b6-158">ng values in hello code.</span></span>

1. <span data-ttu-id="c28b6-159">Войдите в систему toohello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c28b6-159">Sign in toohello Azure classic portal.</span></span>
2. <span data-ttu-id="c28b6-160">В столбце hello навигации слева щелкните **хранения**.</span><span class="sxs-lookup"><span data-stu-id="c28b6-160">In hello left navigation column, click **Storage**.</span></span>
3. <span data-ttu-id="c28b6-161">Из списка hello учетных записей хранения выберите один toostore hello повторное Обучение модели.</span><span class="sxs-lookup"><span data-stu-id="c28b6-161">From hello list of storage accounts, select one toostore hello retrained model.</span></span>
4. <span data-ttu-id="c28b6-162">Внизу hello страницы приветствия щелкните **управление ключами доступа**.</span><span class="sxs-lookup"><span data-stu-id="c28b6-162">At hello bottom of hello page, click **Manage Access Keys**.</span></span>
5. <span data-ttu-id="c28b6-163">Скопируйте и сохраните hello **первичный ключ доступа** и hello закрыть диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="c28b6-163">Copy and save hello **Primary Access Key** and close hello dialog.</span></span>
6. <span data-ttu-id="c28b6-164">В начале hello страницы приветствия, нажмите кнопку **контейнеры**.</span><span class="sxs-lookup"><span data-stu-id="c28b6-164">At hello top of hello page, click **Containers**.</span></span>
7. <span data-ttu-id="c28b6-165">Выберите существующий контейнер, или создайте новую и сохраните имя hello.</span><span class="sxs-lookup"><span data-stu-id="c28b6-165">Select an existing container, or create a new one and save hello name.</span></span>

<span data-ttu-id="c28b6-166">Найдите hello *StorageAccountName*, *StorageAccountKey*, и *StorageContainerName* объявления и обновлять значения hello, которые были сохранены из классического портала hello .</span><span class="sxs-lookup"><span data-stu-id="c28b6-166">Locate hello *StorageAccountName*, *StorageAccountKey*, and *StorageContainerName* declarations, and update hello values that you saved from hello classic portal.</span></span>

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure storage account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage container name

<span data-ttu-id="c28b6-167">Также необходимо убедиться, что в расположении hello, указанных в коде hello доступен hello входного файла.</span><span class="sxs-lookup"><span data-stu-id="c28b6-167">You also must ensure that hello input file is available at hello location that you specify in hello code.</span></span>

### <a name="specify-hello-output-location"></a><span data-ttu-id="c28b6-168">Укажите расположение выходных данных hello</span><span class="sxs-lookup"><span data-stu-id="c28b6-168">Specify hello output location</span></span>
<span data-ttu-id="c28b6-169">При указании расположения вывода hello в полезных данных запроса hello hello расширение файла hello, которая указана в *RelativeLocation* должен быть указан как `ilearner`.</span><span class="sxs-lookup"><span data-stu-id="c28b6-169">When you specify hello output location in hello Request Payload, hello extension of hello file that is specified in *RelativeLocation* must be specified as `ilearner`.</span></span> <span data-ttu-id="c28b6-170">См. следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="c28b6-170">See hello following example:</span></span>

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with hello location you want toouse for your output file and a valid file extension (usually .csv for scoring results or .ilearner for trained models)*/
            }
        },

<span data-ttu-id="c28b6-171">Hello ниже приведен пример выходных данных переподготовки: ![переподготовки выходных данных][6]</span><span class="sxs-lookup"><span data-stu-id="c28b6-171">hello following is an example of retraining output: ![Retraining output][6]</span></span>

## <a name="evaluate-hello-retraining-results"></a><span data-ttu-id="c28b6-172">Привет, переподготовки результаты оценки</span><span class="sxs-lookup"><span data-stu-id="c28b6-172">Evaluate hello retraining results</span></span>
<span data-ttu-id="c28b6-173">При запуске приложения hello hello выводятся hello URL-адрес и маркер подписи общего доступа, которые результаты оценки необходимости tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="c28b6-173">When you run hello application, hello output includes hello URL and shared access signatures token that are necessary tooaccess hello evaluation results.</span></span>

<span data-ttu-id="c28b6-174">Можно просмотреть результаты производительности hello hello повторное Обучение модели путем объединения hello *BaseLocation*, *RelativeLocation*, и *SasBlobToken* из hello выходных результатов для *output2* (как показано в предыдущем переподготовки изображения вывода hello) и вставка hello полный URL-адрес в адресной строке браузера hello.</span><span class="sxs-lookup"><span data-stu-id="c28b6-174">You can see hello performance results of hello retrained model by combining hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from hello output results for *output2* (as shown in hello preceding retraining output image) and pasting hello complete URL into hello browser address bar.</span></span>  

<span data-ttu-id="c28b6-175">Проверьте результаты toodetermine hello ли вновь обученной модели hello выполняет также достаточно hello tooreplace один существующий.</span><span class="sxs-lookup"><span data-stu-id="c28b6-175">Examine hello results toodetermine whether hello newly trained model performs well enough tooreplace hello existing one.</span></span>

<span data-ttu-id="c28b6-176">Копировать hello *BaseLocation*, *RelativeLocation*, и *SasBlobToken* из hello выходные результаты.</span><span class="sxs-lookup"><span data-stu-id="c28b6-176">Copy hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from hello output results.</span></span>

## <a name="retrain-hello-web-service"></a><span data-ttu-id="c28b6-177">Обучение hello веб-службы</span><span class="sxs-lookup"><span data-stu-id="c28b6-177">Retrain hello web service</span></span>
<span data-ttu-id="c28b6-178">При веб-службу, обучение, следует обновить hello прогнозной модели веб-служб определения tooreference hello новый обучения.</span><span class="sxs-lookup"><span data-stu-id="c28b6-178">When you retrain a new web service, you update hello predictive web service definition tooreference hello new trained model.</span></span> <span data-ttu-id="c28b6-179">Hello определение веб-службы – это внутреннее представление hello обученной модели hello веб-службы и не может быть непосредственно изменен.</span><span class="sxs-lookup"><span data-stu-id="c28b6-179">hello web service definition is an internal representation of hello trained model of hello web service and is not directly modifiable.</span></span> <span data-ttu-id="c28b6-180">Убедиться, что для прогнозирования эксперимента и не эксперимента обучения извлекаются hello определение веб-службы.</span><span class="sxs-lookup"><span data-stu-id="c28b6-180">Make sure that you are retrieving hello web service definition for your predictive experiment and not your training experiment.</span></span>

## <a name="sign-in-tooazure-resource-manager"></a><span data-ttu-id="c28b6-181">Войдите в tooAzure диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="c28b6-181">Sign in tooAzure Resource Manager</span></span>
<span data-ttu-id="c28b6-182">Необходимо сначала войти в учетную запись Azure из среды PowerShell hello tooyour с помощью hello [AzureRmAccount добавить](https://msdn.microsoft.com/library/mt619267.aspx) командлета.</span><span class="sxs-lookup"><span data-stu-id="c28b6-182">You must first sign in tooyour Azure account from within hello PowerShell environment by using hello [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

## <a name="get-hello-web-service-definition-object"></a><span data-ttu-id="c28b6-183">Получение hello объекта определения веб-службы</span><span class="sxs-lookup"><span data-stu-id="c28b6-183">Get hello Web Service Definition object</span></span>
<span data-ttu-id="c28b6-184">Затем следует получить hello объекта определения веб-службы путем вызова hello [Get AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) командлета.</span><span class="sxs-lookup"><span data-stu-id="c28b6-184">Next, get hello Web Service Definition object by calling hello [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

<span data-ttu-id="c28b6-185">toodetermine hello группу ресурсов с именем существующей веб-службе, используйте командлет Get-AzureRmMlWebService hello без параметров toodisplay hello веб-служб в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="c28b6-185">toodetermine hello resource group name of an existing web service, run hello Get-AzureRmMlWebService cmdlet without any parameters toodisplay hello web services in your subscription.</span></span> <span data-ttu-id="c28b6-186">Найдите hello веб-службы, а затем найдите на идентификатор его web service.</span><span class="sxs-lookup"><span data-stu-id="c28b6-186">Locate hello web service, and then look at its web service ID.</span></span> <span data-ttu-id="c28b6-187">Hello имя группы ресурсов hello — hello четвертый элемент в качестве идентификатора hello сразу после hello *resourceGroups* элемента.</span><span class="sxs-lookup"><span data-stu-id="c28b6-187">hello name of hello resource group is hello fourth element in hello ID, just after hello *resourceGroups* element.</span></span> <span data-ttu-id="c28b6-188">В следующем примере hello имя группы ресурсов hello — по умолчанию-MachineLearning-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="c28b6-188">In hello following example, hello resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

<span data-ttu-id="c28b6-189">Кроме того, toodetermine hello группу ресурсов с именем существующей веб-службы, войдите в портал веб-службы Azure Machine Learning toohello.</span><span class="sxs-lookup"><span data-stu-id="c28b6-189">Alternatively, toodetermine hello resource group name of an existing web service, sign in toohello Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="c28b6-190">Выберите веб-службу hello.</span><span class="sxs-lookup"><span data-stu-id="c28b6-190">Select hello web service.</span></span> <span data-ttu-id="c28b6-191">Имя группы ресурсов Hello — пятый элемент hello hello и URL-адрес веб-службы hello, сразу после hello *resourceGroups* элемента.</span><span class="sxs-lookup"><span data-stu-id="c28b6-191">hello resource group name is hello fifth element of hello URL of hello web service, just after hello *resourceGroups* element.</span></span> <span data-ttu-id="c28b6-192">В следующем примере hello имя группы ресурсов hello — по умолчанию-MachineLearning-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="c28b6-192">In hello following example, hello resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-hello-web-service-definition-object-as-json"></a><span data-ttu-id="c28b6-193">Экспорт объекта hello определение веб-службы как JSON</span><span class="sxs-lookup"><span data-stu-id="c28b6-193">Export hello Web Service Definition object as JSON</span></span>
<span data-ttu-id="c28b6-194">Определение hello toomodify hello обученной модели toouse hello вновь обучения модели, необходимо сначала использовать hello [AzureRmMlWebService экспорта](https://msdn.microsoft.com/library/azure/mt767935.aspx) tooexport командлет его файла tooa формат JSON.</span><span class="sxs-lookup"><span data-stu-id="c28b6-194">toomodify hello definition of hello trained model toouse hello newly trained model, you must first use hello [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet tooexport it tooa JSON-format file.</span></span>

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-hello-reference-toohello-ilearner-blob"></a><span data-ttu-id="c28b6-195">Обновить hello ilearner toohello эталонный BLOB-объект</span><span class="sxs-lookup"><span data-stu-id="c28b6-195">Update hello reference toohello ilearner blob</span></span>
<span data-ttu-id="c28b6-196">В средствах hello найдите hello [обученной модели], обновление hello *uri* значение в hello *locationInfo* узел с hello URI большого двоичного объекта ilearner hello.</span><span class="sxs-lookup"><span data-stu-id="c28b6-196">In hello assets, locate hello [trained model], update hello *uri* value in hello *locationInfo* node with hello URI of hello ilearner blob.</span></span> <span data-ttu-id="c28b6-197">Hello URI создается путем объединения hello *BaseLocation* и hello *RelativeLocation* из вывода hello hello BES повторную вызова.</span><span class="sxs-lookup"><span data-stu-id="c28b6-197">hello URI is generated by combining hello *BaseLocation* and hello *RelativeLocation* from hello output of hello BES retraining call.</span></span>

     "asset3": {
        "name": "Retrain Sample [trained model]",
        "type": "Resource",
        "locationInfo": {
          "uri": "https://mltestaccount.blob.core.windows.net/azuremlassetscontainer/baca7bca650f46218633552c0bcbba0e.ilearner"
        },
        "outputPorts": {
          "Results dataset": {
            "type": "Dataset"
          }
        }
      },

## <a name="import-hello-json-into-a-web-service-definition-object"></a><span data-ttu-id="c28b6-198">Импортируйте hello JSON в объект определения веб-службы</span><span class="sxs-lookup"><span data-stu-id="c28b6-198">Import hello JSON into a Web Service Definition object</span></span>
<span data-ttu-id="c28b6-199">Необходимо использовать hello [AzureRmMlWebService импорта](https://msdn.microsoft.com/library/azure/mt767925.aspx) hello tooconvert командлет изменения файла JSON обратно в объект определения веб-службы, которые можно использовать tooupdate hello predicative эксперимента.</span><span class="sxs-lookup"><span data-stu-id="c28b6-199">You must use hello [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert hello modified JSON file back into a Web Service Definition object that you can use tooupdate hello predicative experiment.</span></span>

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-hello-web-service"></a><span data-ttu-id="c28b6-200">Обновить hello веб-службы</span><span class="sxs-lookup"><span data-stu-id="c28b6-200">Update hello web service</span></span>
<span data-ttu-id="c28b6-201">Наконец, используйте hello [AzureRmMlWebService обновление](https://msdn.microsoft.com/library/azure/mt767922.aspx) tooupdate командлет hello прогнозной эксперимента.</span><span class="sxs-lookup"><span data-stu-id="c28b6-201">Finally, use hello [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet tooupdate hello predictive experiment.</span></span>

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

[1]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-consume-page.png
[4]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE04.png
[6]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE06.png

<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
