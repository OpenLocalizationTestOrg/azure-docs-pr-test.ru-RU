---
title: "Переобучение имеющейся веб-службы прогнозной аналитики | Документация Майкрософт"
description: "Узнайте, как переобучить модель и обновить веб-службу так, чтобы она использовала заново обученную модель в службе машинного обучения Azure."
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
ms.openlocfilehash: bdc994daf441d397157f8e6cbcf84d72584927f0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="retrain-an-existing-predictive-web-service"></a><span data-ttu-id="c4363-103">Переобучение прогнозной веб-службы</span><span class="sxs-lookup"><span data-stu-id="c4363-103">Retrain an existing predictive web service</span></span>
<span data-ttu-id="c4363-104">В этом документе описан процесс переобучения для следующего сценария:</span><span class="sxs-lookup"><span data-stu-id="c4363-104">This document describes the retraining process for the following scenario:</span></span>

* <span data-ttu-id="c4363-105">Есть обучающий и прогнозный эксперименты, развернутые в качестве веб-службы, готовой к эксплуатации.</span><span class="sxs-lookup"><span data-stu-id="c4363-105">You have a training experiment and a predictive experiment that you have deployed as an operationalized web service.</span></span>
* <span data-ttu-id="c4363-106">Есть новые данные, которые нужно использовать в прогнозной веб-службе, чтобы оценить их.</span><span class="sxs-lookup"><span data-stu-id="c4363-106">You have new data that you want your predictive web service to use to perform its scoring.</span></span>

> [!NOTE] 
> <span data-ttu-id="c4363-107">Для развертывания новой веб-службы у вас должен быть достаточный уровень разрешений в подписке, в которую выполняется развертывание веб-службы.</span><span class="sxs-lookup"><span data-stu-id="c4363-107">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="c4363-108">Дополнительные сведения см. в статье [Управление веб-службой с помощью портала веб-служб машинного обучения Azure](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="c4363-108">For more information see, [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="c4363-109">Вам необходимо выполнить шаги ниже, начав с существующих веб-службы и экспериментов:</span><span class="sxs-lookup"><span data-stu-id="c4363-109">Starting with your existing web service and experiments, you need to follow these steps:</span></span>

1. <span data-ttu-id="c4363-110">Обновление модели.</span><span class="sxs-lookup"><span data-stu-id="c4363-110">Update the model.</span></span>
   1. <span data-ttu-id="c4363-111">Измените обучающий эксперимент, разрешив использование входных и выходных данных веб-службы.</span><span class="sxs-lookup"><span data-stu-id="c4363-111">Modify your training experiment to allow for web service inputs and outputs.</span></span>
   2. <span data-ttu-id="c4363-112">Разверните обучающий эксперимент в качестве переобучаемой веб-службы.</span><span class="sxs-lookup"><span data-stu-id="c4363-112">Deploy the training experiment as a retraining web service.</span></span>
   3. <span data-ttu-id="c4363-113">Используйте службу выполнения пакетов из обучающего эксперимента, чтобы переобучить модель.</span><span class="sxs-lookup"><span data-stu-id="c4363-113">Use the training experiment's Batch Execution Service (BES) to retrain the model.</span></span>
2. <span data-ttu-id="c4363-114">Используйте командлеты PowerShell Машинного обучения Azure, чтобы обновить прогнозный эксперимент.</span><span class="sxs-lookup"><span data-stu-id="c4363-114">Use the Azure Machine Learning PowerShell cmdlets to update the predictive experiment.</span></span>
   1. <span data-ttu-id="c4363-115">Войти в учетную запись Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c4363-115">Sign in to your Azure Resource Manager account.</span></span>
   2. <span data-ttu-id="c4363-116">Получите определение веб-службы.</span><span class="sxs-lookup"><span data-stu-id="c4363-116">Get the web service definition.</span></span>
   3. <span data-ttu-id="c4363-117">Экспортируйте определение веб-службы в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="c4363-117">Export the web service definition as JSON.</span></span>
   4. <span data-ttu-id="c4363-118">Обновить ссылку на большой двоичный объект ilearner в JSON.</span><span class="sxs-lookup"><span data-stu-id="c4363-118">Update the reference to the ilearner blob in the JSON.</span></span>
   5. <span data-ttu-id="c4363-119">Импортируйте JSON-файл в определение веб-службы.</span><span class="sxs-lookup"><span data-stu-id="c4363-119">Import the JSON into a web service definition.</span></span>
   6. <span data-ttu-id="c4363-120">Обновите веб-службу, используя новое определение веб-службы.</span><span class="sxs-lookup"><span data-stu-id="c4363-120">Update the web service with a new web service definition.</span></span>

## <a name="deploy-the-training-experiment"></a><span data-ttu-id="c4363-121">Развертывание обучающего эксперимента</span><span class="sxs-lookup"><span data-stu-id="c4363-121">Deploy the training experiment</span></span>
<span data-ttu-id="c4363-122">Чтобы развернуть обучающий эксперимент в качестве переобучаемой веб-службы, необходимо добавить ее входные и выходные данные в модель.</span><span class="sxs-lookup"><span data-stu-id="c4363-122">To deploy the training experiment as a retraining web service, you must add web service inputs and outputs to the model.</span></span> <span data-ttu-id="c4363-123">Подключившись к модулю *Web Service Output* (Выходные данные веб-службы) в модуле *[Обучение модели][train-model]*, включите обучающий эксперимент, чтобы создать обученную модель, которую можно использовать в прогнозном эксперименте.</span><span class="sxs-lookup"><span data-stu-id="c4363-123">By connecting a *Web Service Output* module to the experiment's *[Train Model][train-model]* module, you enable the training experiment to produce a new trained model that you can use in your predictive experiment.</span></span> <span data-ttu-id="c4363-124">Если у вас есть модуль *Evaluate Model* (Модель оценки), вы также можете присоединить выходные данные веб-службы, чтобы получить результаты оценки в качестве выходных данных.</span><span class="sxs-lookup"><span data-stu-id="c4363-124">If you have an *Evaluate Model* module, you can also attach web service output to get the evaluation results as output.</span></span>

<span data-ttu-id="c4363-125">Чтобы обновить обучающий эксперимент:</span><span class="sxs-lookup"><span data-stu-id="c4363-125">To update your training experiment:</span></span>

1. <span data-ttu-id="c4363-126">Подключите модуль *Web Service Input* (Входные данные веб-службы) к порту ввода данных (например, модуля *Clean Missing Data* (Очистка недостающих данных)).</span><span class="sxs-lookup"><span data-stu-id="c4363-126">Connect a *Web Service Input* module to your data input (for example, a *Clean Missing Data* module).</span></span> <span data-ttu-id="c4363-127">Вы, естественно, захотите убедиться, что входные данные будут обработаны так же, как исходный набор обучающих данных.</span><span class="sxs-lookup"><span data-stu-id="c4363-127">Typically, you want to ensure that your input data is processed in the same way as your original training data.</span></span>
2. <span data-ttu-id="c4363-128">Подключите модуль *Web Service Output* (Выходные данные веб-службы) к порту вывода модуля *Train Model* (Обучение модели).</span><span class="sxs-lookup"><span data-stu-id="c4363-128">Connect a *Web Service Output* module to the output of your *Train Model* module.</span></span>
3. <span data-ttu-id="c4363-129">При наличии модуля *Evaluate Model* (Оценка модели) и необходимости передать результаты оценки подключите модуль *Web Service Output* (Выходные данные веб-службы) к модулю *Evaluate Model* (Оценка модели).</span><span class="sxs-lookup"><span data-stu-id="c4363-129">If you have an *Evaluate Model* module and you want to output the evaluation results, connect a *Web Service Output* module to the output of your *Evaluate Model* module.</span></span>

<span data-ttu-id="c4363-130">Запустите эксперимент.</span><span class="sxs-lookup"><span data-stu-id="c4363-130">Run your experiment.</span></span>

<span data-ttu-id="c4363-131">Затем необходимо развернуть обучающий эксперимент в качестве веб-службы, которая создает обученную модель и результаты ее оценки.</span><span class="sxs-lookup"><span data-stu-id="c4363-131">Next, you must deploy the training experiment as a web service that produces a trained model and model evaluation results.</span></span>  

<span data-ttu-id="c4363-132">В нижней части холста эксперимента щелкните **Set Up Web Service** (Настроить веб-службу), а затем **Deploy Web Service [New]** (Развернуть веб-службу [новую]).</span><span class="sxs-lookup"><span data-stu-id="c4363-132">At the bottom of the experiment canvas, click **Set Up Web Service**, and then select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="c4363-133">Портал веб-служб Машинного обучения Azure откроется на странице **Deploy Web service** (Развертывание веб-службы).</span><span class="sxs-lookup"><span data-stu-id="c4363-133">The Azure Machine Learning Web Services portal opens to the **Deploy Web Service** page.</span></span> <span data-ttu-id="c4363-134">Введите имя веб-службы, выберите план платежей, а затем щелкните **Развернуть**.</span><span class="sxs-lookup"><span data-stu-id="c4363-134">Type a name for your web service, choose a payment plan, and then click **Deploy**.</span></span> <span data-ttu-id="c4363-135">Чтобы создать обученную модель, можно использовать только метод пакетного выполнения.</span><span class="sxs-lookup"><span data-stu-id="c4363-135">You can only use the Batch Execution method for creating trained models.</span></span>

## <a name="retrain-the-model-with-new-data-by-using-bes"></a><span data-ttu-id="c4363-136">Переобучение модели с использованием новых данных с помощью службы выполнения пакетов</span><span class="sxs-lookup"><span data-stu-id="c4363-136">Retrain the model with new data by using BES</span></span>
<span data-ttu-id="c4363-137">В этом примере для создания приложения переобучения используется код на языке C#.</span><span class="sxs-lookup"><span data-stu-id="c4363-137">For this example, we're using C# to create the retraining application.</span></span> <span data-ttu-id="c4363-138">Кроме того, для этого можно использовать образцы кода на языке R или Python.</span><span class="sxs-lookup"><span data-stu-id="c4363-138">You can also use Python or R sample code to accomplish this task.</span></span>

<span data-ttu-id="c4363-139">Чтобы вызвать интерфейсы API переобучения:</span><span class="sxs-lookup"><span data-stu-id="c4363-139">To call the retraining APIs:</span></span>

1. <span data-ttu-id="c4363-140">Создайте консольное приложение C# в Visual Studio (**Создать** > **Проект** > **Visual C#** > **Классический рабочий стол Windows** > **Консольное приложение (.NET Framework**).</span><span class="sxs-lookup"><span data-stu-id="c4363-140">Create a C# console application in Visual Studio: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
2. <span data-ttu-id="c4363-141">Войдите на портал веб-служб Машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="c4363-141">Sign in to the Machine Learning Web Services portal.</span></span>
3. <span data-ttu-id="c4363-142">Щелкните веб-службу, с которой работаете.</span><span class="sxs-lookup"><span data-stu-id="c4363-142">Click the web service that you're working with.</span></span>
4. <span data-ttu-id="c4363-143">Щелкните **Consume**(Использование).</span><span class="sxs-lookup"><span data-stu-id="c4363-143">Click **Consume**.</span></span>
5. <span data-ttu-id="c4363-144">В нижней части страницы **Consume** (Использование) в разделе **Sample Code** (Пример кода) щелкните **Batch** (Пакет).</span><span class="sxs-lookup"><span data-stu-id="c4363-144">At the bottom of the **Consume** page, in the **Sample Code** section, click **Batch**.</span></span>
6. <span data-ttu-id="c4363-145">Скопируйте пример кода на C# для пакетного выполнения и вставьте его в файл Program.cs.</span><span class="sxs-lookup"><span data-stu-id="c4363-145">Copy the sample C# code for batch execution and paste it into the Program.cs file.</span></span> <span data-ttu-id="c4363-146">Убедитесь, что пространство имен не изменено.</span><span class="sxs-lookup"><span data-stu-id="c4363-146">Make sure that the namespace remains intact.</span></span>

<span data-ttu-id="c4363-147">Добавьте пакет NuGet Microsoft.AspNet.WebApi.Client, как указано в комментариях.</span><span class="sxs-lookup"><span data-stu-id="c4363-147">Add the NuGet package Microsoft.AspNet.WebApi.Client, as specified in the comments.</span></span> <span data-ttu-id="c4363-148">Чтобы добавить ссылку на файл Microsoft.WindowsAzure.Storage.dll, может потребоваться сначала установить [клиентскую библиотеку для служб хранилища Azure](https://www.nuget.org/packages/WindowsAzure.Storage).</span><span class="sxs-lookup"><span data-stu-id="c4363-148">To add the reference to Microsoft.WindowsAzure.Storage.dll, you might first need to install the [client library for Azure Storage services](https://www.nuget.org/packages/WindowsAzure.Storage).</span></span>

<span data-ttu-id="c4363-149">На следующем снимке экрана показана станица **Consume** (Использование) на портале веб-служб Машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="c4363-149">The following screenshot shows the **Consume** page in the Azure Machine Learning Web Services portal.</span></span>

![Страница Consume (Использование)][1]

### <a name="update-the-apikey-declaration"></a><span data-ttu-id="c4363-151">Обновление объявления apiKey</span><span class="sxs-lookup"><span data-stu-id="c4363-151">Update the apikey declaration</span></span>
<span data-ttu-id="c4363-152">Найдите объявление **apiKey**:</span><span class="sxs-lookup"><span data-stu-id="c4363-152">Locate the **apikey** declaration:</span></span>

    const string apiKey = "abc123"; // Replace this with the API key for the web service

<span data-ttu-id="c4363-153">В разделе **Basic consumption info** (Основные сведения об использовании) на странице **Consume** (Использование) найдите первичный ключ и скопируйте его в объявление **apiKey**.</span><span class="sxs-lookup"><span data-stu-id="c4363-153">In the **Basic consumption info** section of the **Consume** page, locate the primary key and copy it to the **apikey** declaration.</span></span>

### <a name="update-the-azure-storage-information"></a><span data-ttu-id="c4363-154">Обновление сведений о службе хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="c4363-154">Update the Azure Storage information</span></span>
<span data-ttu-id="c4363-155">Пример кода службы выполнения пакетов отправляет файл с локального диска (например, C:\temp\CensusIpnput.csv) в службу хранилища Azure, обрабатывает его и записывает результаты обратно в службу хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="c4363-155">The BES sample code uploads a file from a local drive (for example, "C:\temp\CensusIpnput.csv") to Azure Storage, processes it, and writes the results back to Azure Storage.</span></span>  

<span data-ttu-id="c4363-156">Чтобы обновить данные службы хранилища Azure, необходимо получить такую информацию, как имя учетной записи хранения, ее ключ и контейнер, с классического портала Azure, а затем изменить соответствующие значения в коде. После запуска эксперимента итоговый рабочий процесс должен быть аналогичен следующему:</span><span class="sxs-lookup"><span data-stu-id="c4363-156">To update the Azure Storage information, you must retrieve the storage account name, key, and container information for your storage account from the Azure classic portal, and then update the correspondi After running your experiment, the resulting workflow should be similar to the following:</span></span>

![Итоговый рабочий процесс после запуска][4]<span data-ttu-id="c4363-158">.</span><span class="sxs-lookup"><span data-stu-id="c4363-158">ng values in the code.</span></span>

1. <span data-ttu-id="c4363-159">Войдите на классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c4363-159">Sign in to the Azure classic portal.</span></span>
2. <span data-ttu-id="c4363-160">В левой области навигации щелкните **Хранилище**.</span><span class="sxs-lookup"><span data-stu-id="c4363-160">In the left navigation column, click **Storage**.</span></span>
3. <span data-ttu-id="c4363-161">Выберите в списке учетную запись хранения, которая будет использоваться для хранения переобученной модели.</span><span class="sxs-lookup"><span data-stu-id="c4363-161">From the list of storage accounts, select one to store the retrained model.</span></span>
4. <span data-ttu-id="c4363-162">В нижней части страницы щелкните **Управление ключами доступа**.</span><span class="sxs-lookup"><span data-stu-id="c4363-162">At the bottom of the page, click **Manage Access Keys**.</span></span>
5. <span data-ttu-id="c4363-163">Скопируйте и сохраните **Первичный ключ доступа** , а затем закройте диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="c4363-163">Copy and save the **Primary Access Key** and close the dialog.</span></span>
6. <span data-ttu-id="c4363-164">В верхней части страницы щелкните **Контейнеры**.</span><span class="sxs-lookup"><span data-stu-id="c4363-164">At the top of the page, click **Containers**.</span></span>
7. <span data-ttu-id="c4363-165">Выберите существующий контейнер или создайте другой, а затем сохраните его имя.</span><span class="sxs-lookup"><span data-stu-id="c4363-165">Select an existing container, or create a new one and save the name.</span></span>

<span data-ttu-id="c4363-166">Найдите объявления *StorageAccountName*, *StorageAccountKey* и *StorageContainerName*, а затем обновите их, используя значения, взятые с классического портала Azure.</span><span class="sxs-lookup"><span data-stu-id="c4363-166">Locate the *StorageAccountName*, *StorageAccountKey*, and *StorageContainerName* declarations, and update the values that you saved from the classic portal.</span></span>

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure storage account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage container name

<span data-ttu-id="c4363-167">Кроме того, необходимо обеспечить доступность файла входных данных в расположении, указанном в коде.</span><span class="sxs-lookup"><span data-stu-id="c4363-167">You also must ensure that the input file is available at the location that you specify in the code.</span></span>

### <a name="specify-the-output-location"></a><span data-ttu-id="c4363-168">Указание расположения выходных данных</span><span class="sxs-lookup"><span data-stu-id="c4363-168">Specify the output location</span></span>
<span data-ttu-id="c4363-169">Указывая расположение выходных данных для полезных данных запроса, измените расширение файла, заданное в *RelativeLocation*, на `ilearner`.</span><span class="sxs-lookup"><span data-stu-id="c4363-169">When you specify the output location in the Request Payload, the extension of the file that is specified in *RelativeLocation* must be specified as `ilearner`.</span></span> <span data-ttu-id="c4363-170">Как в этом примере:</span><span class="sxs-lookup"><span data-stu-id="c4363-170">See the following example:</span></span>

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with the location you want to use for your output file and a valid file extension (usually .csv for scoring results or .ilearner for trained models)*/
            }
        },

<span data-ttu-id="c4363-171">Ниже приведен пример выходных данных переобучения: ![Выходные данные переобучения][6]</span><span class="sxs-lookup"><span data-stu-id="c4363-171">The following is an example of retraining output: ![Retraining output][6]</span></span>

## <a name="evaluate-the-retraining-results"></a><span data-ttu-id="c4363-172">Оценка результатов переобучения</span><span class="sxs-lookup"><span data-stu-id="c4363-172">Evaluate the retraining results</span></span>
<span data-ttu-id="c4363-173">При выполнении приложения выходные данные содержат URL-адрес и подписанные URL-адреса, необходимые для доступа к результатам оценки.</span><span class="sxs-lookup"><span data-stu-id="c4363-173">When you run the application, the output includes the URL and shared access signatures token that are necessary to access the evaluation results.</span></span>

<span data-ttu-id="c4363-174">Чтобы увидеть результаты работы переобученной модели, введите в адресной строке браузера полный URL-адрес, составленный из значений параметров *BaseLocation*, *RelativeLocaiton* и *SasBlobToken*, содержащихся в выходных данных *output2* (как показано на изображении выше).</span><span class="sxs-lookup"><span data-stu-id="c4363-174">You can see the performance results of the retrained model by combining the *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from the output results for *output2* (as shown in the preceding retraining output image) and pasting the complete URL into the browser address bar.</span></span>  

<span data-ttu-id="c4363-175">Проанализируйте результаты и определите, достаточно ли хорошо работает только что обученная модель, чтобы заменить имеющуюся.</span><span class="sxs-lookup"><span data-stu-id="c4363-175">Examine the results to determine whether the newly trained model performs well enough to replace the existing one.</span></span>

<span data-ttu-id="c4363-176">В полученных выходных данных скопируйте значения параметров *BaseLocation*, *RelativeLocation* и *SasBlobToken*.</span><span class="sxs-lookup"><span data-stu-id="c4363-176">Copy the *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from the output results.</span></span>

## <a name="retrain-the-web-service"></a><span data-ttu-id="c4363-177">Переобучение веб-службы</span><span class="sxs-lookup"><span data-stu-id="c4363-177">Retrain the web service</span></span>
<span data-ttu-id="c4363-178">При переобучении новой веб-службы следует обновить определение прогнозной веб-службы, чтобы оно ссылалось на новую обученную модель.</span><span class="sxs-lookup"><span data-stu-id="c4363-178">When you retrain a new web service, you update the predictive web service definition to reference the new trained model.</span></span> <span data-ttu-id="c4363-179">Определение веб-службы — это внутреннее представление обученной модели веб-службы, которое нельзя изменить напрямую.</span><span class="sxs-lookup"><span data-stu-id="c4363-179">The web service definition is an internal representation of the trained model of the web service and is not directly modifiable.</span></span> <span data-ttu-id="c4363-180">Убедитесь, что извлекается определение веб-службы для прогнозного, а не обучающего эксперимента.</span><span class="sxs-lookup"><span data-stu-id="c4363-180">Make sure that you are retrieving the web service definition for your predictive experiment and not your training experiment.</span></span>

## <a name="sign-in-to-azure-resource-manager"></a><span data-ttu-id="c4363-181">Вход в Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c4363-181">Sign in to Azure Resource Manager</span></span>
<span data-ttu-id="c4363-182">Сначала войдите в учетную запись Azure в среде PowerShell, используя командлет [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx).</span><span class="sxs-lookup"><span data-stu-id="c4363-182">You must first sign in to your Azure account from within the PowerShell environment by using the [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

## <a name="get-the-web-service-definition-object"></a><span data-ttu-id="c4363-183">Получение объекта определения веб-службы</span><span class="sxs-lookup"><span data-stu-id="c4363-183">Get the Web Service Definition object</span></span>
<span data-ttu-id="c4363-184">Теперь получите объект определения веб-службы, вызвав командлет [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx).</span><span class="sxs-lookup"><span data-stu-id="c4363-184">Next, get the Web Service Definition object by calling the [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

<span data-ttu-id="c4363-185">Для определения имени группы ресурсов существующей веб-службы выполните командлет Get-AzureRmMlWebService без каких-либо параметров, чтобы отобразились веб-службы в подписке.</span><span class="sxs-lookup"><span data-stu-id="c4363-185">To determine the resource group name of an existing web service, run the Get-AzureRmMlWebService cmdlet without any parameters to display the web services in your subscription.</span></span> <span data-ttu-id="c4363-186">Найдите необходимую веб-службу и посмотрите ее идентификатор.</span><span class="sxs-lookup"><span data-stu-id="c4363-186">Locate the web service, and then look at its web service ID.</span></span> <span data-ttu-id="c4363-187">Имя группы ресурсов — это четвертый элемент в идентификаторе, который следует сразу за элементом *resourceGroups* .</span><span class="sxs-lookup"><span data-stu-id="c4363-187">The name of the resource group is the fourth element in the ID, just after the *resourceGroups* element.</span></span> <span data-ttu-id="c4363-188">В следующем примере имя группы ресурсов — Default-MachineLearning-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="c4363-188">In the following example, the resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

<span data-ttu-id="c4363-189">Кроме того, чтобы определить имя группы ресурсов существующей веб-службы, можно войти на портал веб-служб Машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="c4363-189">Alternatively, to determine the resource group name of an existing web service, sign in to the Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="c4363-190">Затем выбрать веб-службу.</span><span class="sxs-lookup"><span data-stu-id="c4363-190">Select the web service.</span></span> <span data-ttu-id="c4363-191">Имя группы ресурсов — это пятый элемент в URL-адресе веб-службы, который следует сразу за элементом *resourceGroups* .</span><span class="sxs-lookup"><span data-stu-id="c4363-191">The resource group name is the fifth element of the URL of the web service, just after the *resourceGroups* element.</span></span> <span data-ttu-id="c4363-192">В следующем примере имя группы ресурсов — Default-MachineLearning-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="c4363-192">In the following example, the resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-the-web-service-definition-object-as-json"></a><span data-ttu-id="c4363-193">Экспорт объекта определения веб-службы в формате JSON</span><span class="sxs-lookup"><span data-stu-id="c4363-193">Export the Web Service Definition object as JSON</span></span>
<span data-ttu-id="c4363-194">Чтобы изменить определение обученной модели для использования новой соответствующей модели, необходимо сначала выполнить командлет [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx). Это позволит экспортировать определение в JSON-файл.</span><span class="sxs-lookup"><span data-stu-id="c4363-194">To modify the definition of the trained model to use the newly trained model, you must first use the [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet to export it to a JSON-format file.</span></span>

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-the-reference-to-the-ilearner-blob"></a><span data-ttu-id="c4363-195">Обновление ссылки на большой двоичный объект ilearner</span><span class="sxs-lookup"><span data-stu-id="c4363-195">Update the reference to the ilearner blob</span></span>
<span data-ttu-id="c4363-196">В ресурсах-контейнерах найдите элемент [trained model], обновите значение *uri* в узле *locationInfo*, заменив его универсальным кодом ресурса (URI) BLOB-объекта ilearner.</span><span class="sxs-lookup"><span data-stu-id="c4363-196">In the assets, locate the [trained model], update the *uri* value in the *locationInfo* node with the URI of the ilearner blob.</span></span> <span data-ttu-id="c4363-197">URI формируется в результате объединения параметров *BaseLocation* и *RelativeLocation* из выходных данных вызова переобучения BES.</span><span class="sxs-lookup"><span data-stu-id="c4363-197">The URI is generated by combining the *BaseLocation* and the *RelativeLocation* from the output of the BES retraining call.</span></span>

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

## <a name="import-the-json-into-a-web-service-definition-object"></a><span data-ttu-id="c4363-198">Импорт JSON-файла в объект определения веб-службы</span><span class="sxs-lookup"><span data-stu-id="c4363-198">Import the JSON into a Web Service Definition object</span></span>
<span data-ttu-id="c4363-199">Необходимо использовать командлет [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx), чтобы преобразовать измененный JSON-файл обратно в объект определения веб-службы, который можно использовать для обновления прогнозного эксперимента.</span><span class="sxs-lookup"><span data-stu-id="c4363-199">You must use the [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet to convert the modified JSON file back into a Web Service Definition object that you can use to update the predicative experiment.</span></span>

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-the-web-service"></a><span data-ttu-id="c4363-200">Обновление веб-службы</span><span class="sxs-lookup"><span data-stu-id="c4363-200">Update the web service</span></span>
<span data-ttu-id="c4363-201">Наконец, используйте командлет [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx), чтобы обновить прогнозный эксперимент.</span><span class="sxs-lookup"><span data-stu-id="c4363-201">Finally, use the [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet to update the predictive experiment.</span></span>

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

[1]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-consume-page.png
[4]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE04.png
[6]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE06.png

<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
