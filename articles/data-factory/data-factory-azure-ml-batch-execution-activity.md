---
title: "Создание прогнозирующих конвейеров данных с помощью фабрики данных Azure | Документация Майкрософт"
description: "Описывается, как создавать прогнозирующие конвейеры с помощью фабрики данных Azure и машинного обучения Azure."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 4fad8445-4e96-4ce0-aa23-9b88e5ec1965
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: d8e2c9583fc909e4e015e2d40473d2754529d8ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-predictive-pipelines-using-azure-machine-learning-and-azure-data-factory"></a><span data-ttu-id="9c147-103">Создание прогнозирующих конвейеров с помощью машинного обучения Azure и фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="9c147-103">Create predictive pipelines using Azure Machine Learning and Azure Data Factory</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="9c147-104">Действие Hive</span><span class="sxs-lookup"><span data-stu-id="9c147-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="9c147-105">Действие Pig</span><span class="sxs-lookup"><span data-stu-id="9c147-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="9c147-106">Действие MapReduce</span><span class="sxs-lookup"><span data-stu-id="9c147-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="9c147-107">Потоковая активность Hadoop</span><span class="sxs-lookup"><span data-stu-id="9c147-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="9c147-108">Действие Spark</span><span class="sxs-lookup"><span data-stu-id="9c147-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="9c147-109">Действие выполнения пакета машинного обучения</span><span class="sxs-lookup"><span data-stu-id="9c147-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="9c147-110">Действие "Обновить ресурс" в службе машинного обучения</span><span class="sxs-lookup"><span data-stu-id="9c147-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="9c147-111">Действие хранимой процедуры</span><span class="sxs-lookup"><span data-stu-id="9c147-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="9c147-112">Действие U-SQL в Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="9c147-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="9c147-113">Настраиваемое действие .NET</span><span class="sxs-lookup"><span data-stu-id="9c147-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="introduction"></a><span data-ttu-id="9c147-114">Введение</span><span class="sxs-lookup"><span data-stu-id="9c147-114">Introduction</span></span>

### <a name="azure-machine-learning"></a><span data-ttu-id="9c147-115">Машинное обучение Azure</span><span class="sxs-lookup"><span data-stu-id="9c147-115">Azure Machine Learning</span></span>
<span data-ttu-id="9c147-116">[Машинное обучение Azure](https://azure.microsoft.com/documentation/services/machine-learning/) позволяет создавать, тестировать и развертывать решения для прогнозной аналитики.</span><span class="sxs-lookup"><span data-stu-id="9c147-116">[Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) enables you to build, test, and deploy predictive analytics solutions.</span></span> <span data-ttu-id="9c147-117">Этот процесс можно обобщить до трех этапов.</span><span class="sxs-lookup"><span data-stu-id="9c147-117">From a high-level point of view, it is done in three steps:</span></span>

1. <span data-ttu-id="9c147-118">**Создание обучающего эксперимента**.</span><span class="sxs-lookup"><span data-stu-id="9c147-118">**Create a training experiment**.</span></span> <span data-ttu-id="9c147-119">Это можно сделать с помощью Студии машинного обучения Microsoft Azure,</span><span class="sxs-lookup"><span data-stu-id="9c147-119">You do this step by using the Azure ML Studio.</span></span> <span data-ttu-id="9c147-120">которая представляет собой среду совместной визуальной разработки, используемую для обучения и проверки модели прогнозной аналитики с использованием данных для обучения.</span><span class="sxs-lookup"><span data-stu-id="9c147-120">The ML studio is a collaborative visual development environment that you use to train and test a predictive analytics model using training data.</span></span>
2. <span data-ttu-id="9c147-121">**Преобразование обучающего эксперимента в прогнозный**.</span><span class="sxs-lookup"><span data-stu-id="9c147-121">**Convert it to a predictive experiment**.</span></span> <span data-ttu-id="9c147-122">Когда модель будет обучена с помощью существующих данных и готова для оценки новых данных, следует подготовить и оптимизировать эксперимент для оценки.</span><span class="sxs-lookup"><span data-stu-id="9c147-122">Once your model has been trained with existing data and you are ready to use it to score new data, you prepare and streamline your experiment for scoring.</span></span>
3. <span data-ttu-id="9c147-123">**Развертывание эксперимента в виде веб-службы**.</span><span class="sxs-lookup"><span data-stu-id="9c147-123">**Deploy it as a web service**.</span></span> <span data-ttu-id="9c147-124">Оценивающий эксперимент можно опубликовать в виде веб-службы Azure.</span><span class="sxs-lookup"><span data-stu-id="9c147-124">You can publish your scoring experiment as an Azure web service.</span></span> <span data-ttu-id="9c147-125">С помощью конечной точки этой веб-службы вы можете отправлять данные в свою модель и получать из нее результаты прогнозов.</span><span class="sxs-lookup"><span data-stu-id="9c147-125">You can send data to your model via this web service end point and receive result predictions fro the model.</span></span>  

### <a name="azure-data-factory"></a><span data-ttu-id="9c147-126">Фабрика данных Azure</span><span class="sxs-lookup"><span data-stu-id="9c147-126">Azure Data Factory</span></span>
<span data-ttu-id="9c147-127">Фабрика данных представляет собой облачную службу интеграции информации, которая организует и автоматизирует **перемещение** и **преобразование** данных.</span><span class="sxs-lookup"><span data-stu-id="9c147-127">Data Factory is a cloud-based data integration service that orchestrates and automates the **movement** and **transformation** of data.</span></span> <span data-ttu-id="9c147-128">Вы можете создавать решения для интеграции данных с помощью фабрики данных Azure, которая получает, преобразует и обрабатывает данные из различных хранилищ, а также публикует обработанные данные в хранилищах данных.</span><span class="sxs-lookup"><span data-stu-id="9c147-128">You can create data integration solutions using Azure Data Factory that can ingest data from various data stores, transform/process the data, and publish the result data to the data stores.</span></span>

<span data-ttu-id="9c147-129">Служба фабрики данных позволяет создавать конвейеры данных для перемещения и преобразования данных, а затем запускать конвейеры по указанному расписанию (ежечасно, ежедневно, еженедельно и т. д.).</span><span class="sxs-lookup"><span data-stu-id="9c147-129">Data Factory service allows you to create data pipelines that move and transform data, and then run the pipelines on a specified schedule (hourly, daily, weekly, etc.).</span></span> <span data-ttu-id="9c147-130">Служба также предоставляет широкие возможности визуализации для отображения журнала преобразований данных и зависимостей между конвейерами данных, а также для мониторинга всех конвейеров данных в едином представлении с целью оперативного выявления проблем и настройки оповещений.</span><span class="sxs-lookup"><span data-stu-id="9c147-130">It also provides rich visualizations to display the lineage and dependencies between your data pipelines, and monitor all your data pipelines from a single unified view to easily pinpoint issues and setup monitoring alerts.</span></span>

<span data-ttu-id="9c147-131">См. статьи [Общие сведения о службе фабрики данных Azure](data-factory-introduction.md) и [Создание первого конвейера](data-factory-build-your-first-pipeline.md), чтобы быстро приступить к работе со службой фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="9c147-131">See [Introduction to Azure Data Factory](data-factory-introduction.md) and [Build your first pipeline](data-factory-build-your-first-pipeline.md) articles to quickly get started with the Azure Data Factory service.</span></span>

### <a name="data-factory-and-machine-learning-together"></a><span data-ttu-id="9c147-132">Фабрика данных и машинное обучение вместе</span><span class="sxs-lookup"><span data-stu-id="9c147-132">Data Factory and Machine Learning together</span></span>
<span data-ttu-id="9c147-133">Фабрика данных Azure позволяет легко создавать конвейеры, в которых для прогнозной аналитики используется опубликованная веб-служба [машинного обучения Azure][azure-machine-learning].</span><span class="sxs-lookup"><span data-stu-id="9c147-133">Azure Data Factory enables you to easily create pipelines that use a published [Azure Machine Learning][azure-machine-learning] web service for predictive analytics.</span></span> <span data-ttu-id="9c147-134">С помощью **действия выполнения пакета** в конвейере фабрики данных Azure можно обращаться к веб-службе машинного обучения Azure, чтобы создавать прогнозы по данным в пакете.</span><span class="sxs-lookup"><span data-stu-id="9c147-134">Using the **Batch Execution Activity** in an Azure Data Factory pipeline, you can invoke an Azure ML web service to make predictions on the data in batch.</span></span> <span data-ttu-id="9c147-135">Подробные сведения см. в разделе [Обращение к веб-службе машинного обучения Azure с помощью действия выполнения пакета](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity).</span><span class="sxs-lookup"><span data-stu-id="9c147-135">See [Invoking an Azure ML web service using the Batch Execution Activity](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) section for details.</span></span>

<span data-ttu-id="9c147-136">Со временем прогнозные модели из оценивающих экспериментов машинного обучения Azure потребуют повторного обучения с помощью новых наборов входных данных.</span><span class="sxs-lookup"><span data-stu-id="9c147-136">Over time, the predictive models in the Azure ML scoring experiments need to be retrained using new input datasets.</span></span> <span data-ttu-id="9c147-137">Чтобы повторно обучить модель машинного обучения Azure из конвейера фабрики данных, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="9c147-137">You can retrain an Azure ML model from a Data Factory pipeline by doing the following steps:</span></span>

1. <span data-ttu-id="9c147-138">Опубликуйте обучающий (не прогнозный) эксперимент в виде веб-службы.</span><span class="sxs-lookup"><span data-stu-id="9c147-138">Publish the training experiment (not predictive experiment) as a web service.</span></span> <span data-ttu-id="9c147-139">Как и при публикации прогнозного эксперимента, это можно сделать в Студии машинного обучения Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9c147-139">You do this step in the Azure ML Studio as you did to expose predictive experiment as a web service in the previous scenario.</span></span>
2. <span data-ttu-id="9c147-140">Чтобы обратиться к веб-службе для получения обучающего эксперимента, воспользуйтесь действием «Выполнение пакета» машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="9c147-140">Use the Azure ML Batch Execution Activity to invoke the web service for the training experiment.</span></span> <span data-ttu-id="9c147-141">По сути, действие «Выполнение пакета» машинного обучения Azure можно использовать для обращения как к веб-службе обучения, так и веб-службе оценки.</span><span class="sxs-lookup"><span data-stu-id="9c147-141">Basically, you can use the Azure ML Batch Execution activity to invoke both training web service and scoring web service.</span></span>

<span data-ttu-id="9c147-142">Когда повторное обучение будет завершено, обновите веб-службу оценки (прогнозный эксперимент, опубликованный в виде веб-службы) на основании обученной заново модели, используя **действие обновления ресурса машинного обучения Azure**.</span><span class="sxs-lookup"><span data-stu-id="9c147-142">After you are done with retraining, update the scoring web service (predictive experiment exposed as a web service) with the newly trained model by using the **Azure ML Update Resource Activity**.</span></span> <span data-ttu-id="9c147-143">Дополнительные сведения см. в статье [Updating Azure Machine Learning models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) (Обновление моделей машинного обучения Azure с помощью действия "Обновить ресурс").</span><span class="sxs-lookup"><span data-stu-id="9c147-143">See [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) article for details.</span></span>

## <a name="invoking-a-web-service-using-batch-execution-activity"></a><span data-ttu-id="9c147-144">Вызов веб-службы с помощью действия выполнения пакета</span><span class="sxs-lookup"><span data-stu-id="9c147-144">Invoking a web service using Batch Execution Activity</span></span>
<span data-ttu-id="9c147-145">Можно управлять перемещением и обработкой данных с помощью фабрики данных Azure, а затем осуществлять пакетное выполнение, используя Машинное обучение Azure.</span><span class="sxs-lookup"><span data-stu-id="9c147-145">You use Azure Data Factory to orchestrate data movement and processing, and then perform batch execution using Azure Machine Learning.</span></span> <span data-ttu-id="9c147-146">Для этого выполните действия верхнего уровня:</span><span class="sxs-lookup"><span data-stu-id="9c147-146">Here are the top-level steps:</span></span>

1. <span data-ttu-id="9c147-147">Создайте связанную службу Машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="9c147-147">Create an Azure Machine Learning linked service.</span></span> <span data-ttu-id="9c147-148">Вам потребуются следующие значения:</span><span class="sxs-lookup"><span data-stu-id="9c147-148">You need the following values:</span></span>

   1. <span data-ttu-id="9c147-149">**Универсальный код ресурса (URI) запроса** для API пакетного выполнения.</span><span class="sxs-lookup"><span data-stu-id="9c147-149">**Request URI** for the Batch Execution API.</span></span> <span data-ttu-id="9c147-150">Чтобы найти URI запроса, перейдите по ссылке **Выполнение пакета** на странице веб-служб.</span><span class="sxs-lookup"><span data-stu-id="9c147-150">You can find the Request URI by clicking the **BATCH EXECUTION** link in the web services page.</span></span>
   2. <span data-ttu-id="9c147-151">**Ключ API** для опубликованной веб-службы машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="9c147-151">**API key** for the published Azure Machine Learning web service.</span></span> <span data-ttu-id="9c147-152">Чтобы найти ключ API, щелкните опубликованную веб-службу.</span><span class="sxs-lookup"><span data-stu-id="9c147-152">You can find the API key by clicking the web service that you have published.</span></span>
   3. <span data-ttu-id="9c147-153">Используйте действие **AzureMLBatchExecution** .</span><span class="sxs-lookup"><span data-stu-id="9c147-153">Use the **AzureMLBatchExecution** activity.</span></span>

      ![Панель мониторинга машинного обучения](./media/data-factory-azure-ml-batch-execution-activity/AzureMLDashboard.png)

      ![Универсальный код ресурса (URI) пакета](./media/data-factory-azure-ml-batch-execution-activity/batch-uri.png)

### <a name="scenario-experiments-using-web-service-inputsoutputs-that-refer-to-data-in-azure-blob-storage"></a><span data-ttu-id="9c147-156">Сценарий: эксперименты с вводом-выводом веб-службы, ссылающейся на данные в хранилище больших двоичных объектов Azure</span><span class="sxs-lookup"><span data-stu-id="9c147-156">Scenario: Experiments using Web service inputs/outputs that refer to data in Azure Blob Storage</span></span>
<span data-ttu-id="9c147-157">В этом сценарии веб-служба Машинного обучения Azure делает прогнозы с использованием данных из файла в хранилище больших двоичных объектов Azure и сохраняет результаты прогнозирования в хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="9c147-157">In this scenario, the Azure Machine Learning Web service makes predictions using data from a file in an Azure blob storage and stores the prediction results in the blob storage.</span></span> <span data-ttu-id="9c147-158">Следующий код JSON определяет конвейер фабрики данных действием AzureMLBatchExecution.</span><span class="sxs-lookup"><span data-stu-id="9c147-158">The following JSON defines a Data Factory pipeline with an AzureMLBatchExecution activity.</span></span> <span data-ttu-id="9c147-159">У действия имеется входной (**DecisionTreeInputBlob**) и выходной (**DecisionTreeResultBlob**) наборы данных.</span><span class="sxs-lookup"><span data-stu-id="9c147-159">The activity has the dataset **DecisionTreeInputBlob** as input and **DecisionTreeResultBlob** as the output.</span></span> <span data-ttu-id="9c147-160">Набор **DecisionTreeInputBlob** передается в веб-службу в качестве входных данных с помощью свойства JSON **webServiceInput**,</span><span class="sxs-lookup"><span data-stu-id="9c147-160">The **DecisionTreeInputBlob** is passed as an input to the web service by using the **webServiceInput** JSON property.</span></span> <span data-ttu-id="9c147-161">а **DecisionTreeResultBlob** — в качестве выходных данных с помощью свойства JSON **webServiceOutputs**.</span><span class="sxs-lookup"><span data-stu-id="9c147-161">The **DecisionTreeResultBlob** is passed as an output to the Web service by using the **webServiceOutputs** JSON property.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="9c147-162">Если веб-служба принимает несколько входных наборов данных, используйте свойство **webServiceInputs** вместо **webServiceInput**.</span><span class="sxs-lookup"><span data-stu-id="9c147-162">If the web service takes multiple inputs, use the **webServiceInputs** property instead of using **webServiceInput**.</span></span> <span data-ttu-id="9c147-163">В соответствующем разделе [Веб-службе требуется несколько входных данных](#web-service-requires-multiple-inputs) приведен пример использования свойства webServiceInputs.</span><span class="sxs-lookup"><span data-stu-id="9c147-163">See the [Web service requires multiple inputs](#web-service-requires-multiple-inputs) section for an example of using the webServiceInputs property.</span></span>
>
> <span data-ttu-id="9c147-164">Наборы данных, на которые ссылаются свойства **webServiceInput**/**webServiceInputs** и **webServiceOutputs** (в **typeProperties**), также должны быть включены во **входные** и **выходные** данные действия.</span><span class="sxs-lookup"><span data-stu-id="9c147-164">Datasets that are referenced by the **webServiceInput**/**webServiceInputs** and **webServiceOutputs** properties (in **typeProperties**) must also be included in the Activity **inputs** and **outputs**.</span></span>
>
> <span data-ttu-id="9c147-165">В эксперименте Машинного обучения Azure у входных и выходных портов и глобальных параметров есть имена по умолчанию (input1, input2), которые можно настроить.</span><span class="sxs-lookup"><span data-stu-id="9c147-165">In your Azure ML experiment, web service input and output ports and global parameters have default names ("input1", "input2") that you can customize.</span></span> <span data-ttu-id="9c147-166">Имена, используемые для параметров webServiceInputs, webServiceOutputs и globalParameters, должны точно совпадать с именами в экспериментах.</span><span class="sxs-lookup"><span data-stu-id="9c147-166">The names you use for webServiceInputs, webServiceOutputs, and globalParameters settings must exactly match the names in the experiments.</span></span> <span data-ttu-id="9c147-167">Пример полезных данных запроса можно просмотреть на странице справки по выполнению пакета для конечной точки Машинного обучения Azure, чтобы проверить ожидаемое сопоставление.</span><span class="sxs-lookup"><span data-stu-id="9c147-167">You can view the sample request payload on the Batch Execution Help page for your Azure ML endpoint to verify the expected mapping.</span></span>
>
>

```JSON
{
  "name": "PredictivePipeline",
  "properties": {
    "description": "use AzureML model",
    "activities": [
      {
        "name": "MLActivity",
        "type": "AzureMLBatchExecution",
        "description": "prediction analysis on batch input",
        "inputs": [
          {
            "name": "DecisionTreeInputBlob"
          }
        ],
        "outputs": [
          {
            "name": "DecisionTreeResultBlob"
          }
        ],
        "linkedServiceName": "MyAzureMLLinkedService",
        "typeProperties":
        {
            "webServiceInput": "DecisionTreeInputBlob",
            "webServiceOutputs": {
                "output1": "DecisionTreeResultBlob"
            }                
        },
        "policy": {
          "concurrency": 3,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        }
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```
> [!NOTE]
> <span data-ttu-id="9c147-168">Только входные и выходные данные действия AzureMLBatchExecution могут передаваться как параметры веб-службы.</span><span class="sxs-lookup"><span data-stu-id="9c147-168">Only inputs and outputs of the AzureMLBatchExecution activity can be passed as parameters to the Web service.</span></span> <span data-ttu-id="9c147-169">Например, в приведенном выше фрагменте JSON DecisionTreeInputBlob —входные данные действия AzureMLBatchExecution, которые передаются в качестве входных данных в веб-службу через параметр webServiceInput.</span><span class="sxs-lookup"><span data-stu-id="9c147-169">For example, in the above JSON snippet, DecisionTreeInputBlob is an input to the AzureMLBatchExecution activity, which is passed as an input to the Web service via webServiceInput parameter.</span></span>   
>
>

### <a name="example"></a><span data-ttu-id="9c147-170">Пример</span><span class="sxs-lookup"><span data-stu-id="9c147-170">Example</span></span>
<span data-ttu-id="9c147-171">В этом примере для размещения входных и выходных данных используется служба хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="9c147-171">This example uses Azure Storage to hold both the input and output data.</span></span>

<span data-ttu-id="9c147-172">Советуем, прежде чем приступить к этому примеру, ознакомиться со статьей [Учебник. Создание первого конвейера для обработки данных с помощью кластера Hadoop][adf-build-1st-pipeline].</span><span class="sxs-lookup"><span data-stu-id="9c147-172">We recommend that you go through the [Build your first pipeline with Data Factory][adf-build-1st-pipeline] tutorial before going through this example.</span></span> <span data-ttu-id="9c147-173">C помощью редактора фабрики данных можно создать артефакты фабрики данных (связанные службы, наборы данных и конвейер) для этого примера.</span><span class="sxs-lookup"><span data-stu-id="9c147-173">Use the Data Factory Editor to create Data Factory artifacts (linked services, datasets, pipeline) in this example.</span></span>   

1. <span data-ttu-id="9c147-174">Создайте **связанную службу** для **службы хранилища Azure**.</span><span class="sxs-lookup"><span data-stu-id="9c147-174">Create a **linked service** for your **Azure Storage**.</span></span> <span data-ttu-id="9c147-175">Если входные и выходные файлы находятся в разных учетных записях хранения, то потребуются две связанные службы.</span><span class="sxs-lookup"><span data-stu-id="9c147-175">If the input and output files are in different storage accounts, you need two linked services.</span></span> <span data-ttu-id="9c147-176">Ниже приведен пример JSON:</span><span class="sxs-lookup"><span data-stu-id="9c147-176">Here is a JSON example:</span></span>

    ```JSON
    {
      "name": "StorageLinkedService",
      "properties": {
        "type": "AzureStorage",
        "typeProperties": {
          "connectionString": "DefaultEndpointsProtocol=https;AccountName=[acctName];AccountKey=[acctKey]"
        }
      }
    }
    ```
2. <span data-ttu-id="9c147-177">Создайте **входной** **набор данных** фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="9c147-177">Create the **input** Azure Data Factory **dataset**.</span></span> <span data-ttu-id="9c147-178">В отличие от некоторых других наборов данных фабрики данных, эти наборы должны содержать значения **folderPath** и **fileName**.</span><span class="sxs-lookup"><span data-stu-id="9c147-178">Unlike some other Data Factory datasets, these datasets must contain both **folderPath** and **fileName** values.</span></span> <span data-ttu-id="9c147-179">Можно использовать секционирование для выполнения каждого пакета (каждого среза данных) для обработки или создания уникальных входных и выходных файлов.</span><span class="sxs-lookup"><span data-stu-id="9c147-179">You can use partitioning to cause each batch execution (each data slice) to process or produce unique input and output files.</span></span> <span data-ttu-id="9c147-180">Возможно, потребуется включить некоторые вышестоящие действия для преобразования входных данных в формат CSV-файла и его размещения в учетной записи хранения для каждого среза.</span><span class="sxs-lookup"><span data-stu-id="9c147-180">You may need to include some upstream activity to transform the input into the CSV file format and place it in the storage account for each slice.</span></span> <span data-ttu-id="9c147-181">В этом случае не будут включены параметры **external** и **externalData**, как показано в примере ниже, а DecisionTreeInputBlob будет выходным набором данных другого действия.</span><span class="sxs-lookup"><span data-stu-id="9c147-181">In that case, you would not include the **external** and **externalData** settings shown in the following example, and your DecisionTreeInputBlob would be the output dataset of a different Activity.</span></span>

    ```JSON
    {
      "name": "DecisionTreeInputBlob",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "azuremltesting/input",
          "fileName": "in.csv",
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "external": true,
        "availability": {
          "frequency": "Day",
          "interval": 1
        },
        "policy": {
          "externalData": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3
          }
        }
      }
    }
    ```

    <span data-ttu-id="9c147-182">Входной CSV-файл должен содержать строку заголовков столбцов.</span><span class="sxs-lookup"><span data-stu-id="9c147-182">Your input csv file must have the column header row.</span></span> <span data-ttu-id="9c147-183">Если вы используете **действие копирования** для создания или перемещения CSV-файла в хранилище BLOB-объектов, следует установить для свойства **blobWriterAddHeader** приемника значение **true**.</span><span class="sxs-lookup"><span data-stu-id="9c147-183">If you are using the **Copy Activity** to create/move the csv into the blob storage, you should set the sink property **blobWriterAddHeader** to **true**.</span></span> <span data-ttu-id="9c147-184">Например:</span><span class="sxs-lookup"><span data-stu-id="9c147-184">For example:</span></span>

    ```JSON
    sink:
    {
        "type": "BlobSink",     
        "blobWriterAddHeader": true
    }
    ```

    <span data-ttu-id="9c147-185">если CSV-файл не имеет строку заголовков, может появиться следующая ошибка: **Ошибка в действии: ошибка при чтении строки. Непредвиденный токен: StartObject. Путь '', строка 1, позиция 1**.</span><span class="sxs-lookup"><span data-stu-id="9c147-185">If the csv file does not have the header row, you may see the following error: **Error in Activity: Error reading string. Unexpected token: StartObject. Path '', line 1, position 1**.</span></span>
3. <span data-ttu-id="9c147-186">Создайте **выходной** **набор данных** фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="9c147-186">Create the **output** Azure Data Factory **dataset**.</span></span> <span data-ttu-id="9c147-187">В этом примере используется секционирование для создания уникального выходного пути при выполнении каждого из срезов.</span><span class="sxs-lookup"><span data-stu-id="9c147-187">This example uses partitioning to create a unique output path for each slice execution.</span></span> <span data-ttu-id="9c147-188">Без этого действие перезапишет файл.</span><span class="sxs-lookup"><span data-stu-id="9c147-188">Without the partitioning, the activity would overwrite the file.</span></span>

    ```JSON
    {
      "name": "DecisionTreeResultBlob",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "azuremltesting/scored/{folderpart}/",
          "fileName": "{filepart}result.csv",
          "partitionedBy": [
            {
              "name": "folderpart",
              "value": {
                "type": "DateTime",
                "date": "SliceStart",
                "format": "yyyyMMdd"
              }
            },
            {
              "name": "filepart",
              "value": {
                "type": "DateTime",
                "date": "SliceStart",
                "format": "HHmmss"
              }
            }
          ],
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "availability": {
          "frequency": "Day",
          "interval": 15
        }
      }
    }
    ```
4. <span data-ttu-id="9c147-189">Создайте **связанную службу** типа **AzureMLLinkedService**, предоставляющую ключ API и URL-адрес выполнения пакета для модели.</span><span class="sxs-lookup"><span data-stu-id="9c147-189">Create a **linked service** of type: **AzureMLLinkedService**, providing the API key and model batch execution URL.</span></span>

    ```JSON
    {
      "name": "MyAzureMLLinkedService",
      "properties": {
        "type": "AzureML",
        "typeProperties": {
          "mlEndpoint": "https://[batch execution endpoint]/jobs",
          "apiKey": "[apikey]"
        }
      }
    }
    ```
5. <span data-ttu-id="9c147-190">Наконец, создайте конвейер, содержащий действие **AzureMLBatchExecution** .</span><span class="sxs-lookup"><span data-stu-id="9c147-190">Finally, author a pipeline containing an **AzureMLBatchExecution** Activity.</span></span> <span data-ttu-id="9c147-191">Конвейер выполняет следующие действия:</span><span class="sxs-lookup"><span data-stu-id="9c147-191">At runtime, pipeline performs the following steps:</span></span>

   1. <span data-ttu-id="9c147-192">Получает расположение входного файла из входных наборов данных.</span><span class="sxs-lookup"><span data-stu-id="9c147-192">Gets the location of the input file from your input datasets.</span></span>
   2. <span data-ttu-id="9c147-193">Вызывает API пакетного выполнения машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="9c147-193">Invokes the Azure Machine Learning batch execution API</span></span>
   3. <span data-ttu-id="9c147-194">Копирует выходные данные пакетного выполнения в заданный большой двоичный объект в выходном наборе данных.</span><span class="sxs-lookup"><span data-stu-id="9c147-194">Copies the batch execution output to the blob given in your output dataset.</span></span>

      > [!NOTE]
      > <span data-ttu-id="9c147-195">У действия AzureMLBatchExecution может быть ноль или более входных наборов данных и один или несколько выходных наборов данных.</span><span class="sxs-lookup"><span data-stu-id="9c147-195">AzureMLBatchExecution activity can have zero or more inputs and one or more outputs.</span></span>
      >
      >

    ```JSON
    {
        "name": "PredictivePipeline",
        "properties": {
            "description": "use AzureML model",
            "activities": [
            {
                "name": "MLActivity",
                "type": "AzureMLBatchExecution",
                "description": "prediction analysis on batch input",
                "inputs": [
                {
                    "name": "DecisionTreeInputBlob"
                }
                ],
                "outputs": [
                {
                    "name": "DecisionTreeResultBlob"
                }
                ],
                "linkedServiceName": "MyAzureMLLinkedService",
                "typeProperties":
                {
                    "webServiceInput": "DecisionTreeInputBlob",
                    "webServiceOutputs": {
                        "output1": "DecisionTreeResultBlob"
                    }                
                },
                "policy": {
                    "concurrency": 3,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            }
            ],
            "start": "2016-02-13T00:00:00Z",
            "end": "2016-02-14T00:00:00Z"
        }
    }
    ```

      <span data-ttu-id="9c147-196">Даты **начала** и **окончания** должны быть в [формате ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="9c147-196">Both **start** and **end** datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="9c147-197">Например, 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="9c147-197">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="9c147-198">Значение времени окончания (**end**) является необязательным.</span><span class="sxs-lookup"><span data-stu-id="9c147-198">The **end** time is optional.</span></span> <span data-ttu-id="9c147-199">Если не указать значение свойства **end**, оно вычисляется по формуле **время начала + 48 часов**.</span><span class="sxs-lookup"><span data-stu-id="9c147-199">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours.**"</span></span> <span data-ttu-id="9c147-200">Чтобы запустить конвейер в течение неопределенного срока, укажите значение **9999-09-09** в качестве значения свойства **end**.</span><span class="sxs-lookup"><span data-stu-id="9c147-200">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span> <span data-ttu-id="9c147-201">Дополнительные сведения о свойствах JSON см. в [справочнике по скриптам JSON](https://msdn.microsoft.com/library/dn835050.aspx).</span><span class="sxs-lookup"><span data-stu-id="9c147-201">See [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) for details about JSON properties.</span></span>

      > [!NOTE]
      > <span data-ttu-id="9c147-202">Указывать входные данные для действия AzureMLBatchExecution необязательно.</span><span class="sxs-lookup"><span data-stu-id="9c147-202">Specifying input for the AzureMLBatchExecution activity is optional.</span></span>
      >
      >

### <a name="scenario-experiments-using-readerwriter-modules-to-refer-to-data-in-various-storages"></a><span data-ttu-id="9c147-203">Сценарий: эксперименты со использованием модулей чтения и записи для обращения к данным в различных хранилищах</span><span class="sxs-lookup"><span data-stu-id="9c147-203">Scenario: Experiments using Reader/Writer Modules to refer to data in various storages</span></span>
<span data-ttu-id="9c147-204">При создании экспериментов с Машинным обучением Azure еще одним распространенным сценарием является использование модулей чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="9c147-204">Another common scenario when creating Azure ML experiments is to use Reader and Writer modules.</span></span> <span data-ttu-id="9c147-205">Модуль чтения используется для загрузки данных в эксперимент, а модуль записи — для сохранения данных экспериментов.</span><span class="sxs-lookup"><span data-stu-id="9c147-205">The reader module is used to load data into an experiment and the writer module is to save data from your experiments.</span></span> <span data-ttu-id="9c147-206">Дополнительные сведения о модулях [чтения](https://msdn.microsoft.com/library/azure/dn905997.aspx) и [записи](https://msdn.microsoft.com/library/azure/dn905984.aspx) см. в соответствующих разделах в библиотеке MSDN.</span><span class="sxs-lookup"><span data-stu-id="9c147-206">For details about reader and writer modules, see [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span></span>     

<span data-ttu-id="9c147-207">При использовании модулей чтения и записи рекомендуется указывать параметр веб-службы для каждого их свойства.</span><span class="sxs-lookup"><span data-stu-id="9c147-207">When using the reader and writer modules, it is good practice to use a Web service parameter for each property of these reader/writer modules.</span></span> <span data-ttu-id="9c147-208">Эти параметры веб-службы позволяют настроить значения во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="9c147-208">These web parameters enable you to configure the values during runtime.</span></span> <span data-ttu-id="9c147-209">Например, можно создать эксперимент с модулем чтения, который использует базу данных SQL Azure: XXX.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="9c147-209">For example, you could create an experiment with a reader module that uses an Azure SQL Database: XXX.database.windows.net.</span></span> <span data-ttu-id="9c147-210">После развертывания веб-службы вам необходимо включить объекты-получатели веб-службы, чтобы указать другой сервер Azure SQL, YYY.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="9c147-210">After the web service has been deployed, you want to enable the consumers of the web service to specify another Azure SQL Server called YYY.database.windows.net.</span></span> <span data-ttu-id="9c147-211">Вы можете использовать параметр веб-службы, чтобы разрешить настройку этого значения.</span><span class="sxs-lookup"><span data-stu-id="9c147-211">You can use a Web service parameter to allow this value to be configured.</span></span>

> [!NOTE]
> <span data-ttu-id="9c147-212">Входные и выходные данные веб-службы отличаются от параметров веб-службы.</span><span class="sxs-lookup"><span data-stu-id="9c147-212">Web service input and output are different from Web service parameters.</span></span> <span data-ttu-id="9c147-213">В первом сценарии вы узнали, как можно указать ввод и вывод для веб-службы Машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="9c147-213">In the first scenario, you have seen how an input and output can be specified for an Azure ML Web service.</span></span> <span data-ttu-id="9c147-214">В этом сценарии вы передаете параметры для веб-службы, соответствующие свойствам модулей чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="9c147-214">In this scenario, you pass parameters for a Web service that correspond to properties of reader/writer modules.</span></span>
>
>

<span data-ttu-id="9c147-215">Рассмотрим сценарий использования параметров веб-службы.</span><span class="sxs-lookup"><span data-stu-id="9c147-215">Let's look at a scenario for using Web service parameters.</span></span> <span data-ttu-id="9c147-216">Вы развернули веб-службу машинного обучения Azure, которая использует модуль чтения для чтения данных из одного из поддерживаемых источников данных машинного обучения Azure (например, базы данных SQL Azure).</span><span class="sxs-lookup"><span data-stu-id="9c147-216">You have a deployed Azure Machine Learning web service that uses a reader module to read data from one of the data sources supported by Azure Machine Learning (for example: Azure SQL Database).</span></span> <span data-ttu-id="9c147-217">После пакетного выполнения результаты записываются с помощью модуля записи (база данных SQL Azure).</span><span class="sxs-lookup"><span data-stu-id="9c147-217">After the batch execution is performed, the results are written using a Writer module (Azure SQL Database).</span></span>  <span data-ttu-id="9c147-218">В экспериментах не определены входные и выходные данные веб-службы.</span><span class="sxs-lookup"><span data-stu-id="9c147-218">No web service inputs and outputs are defined in the experiments.</span></span> <span data-ttu-id="9c147-219">В этом случае мы советуем настроить соответствующие параметры веб-службы для модулей чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="9c147-219">In this case, we recommend that you configure relevant web service parameters for the reader and writer modules.</span></span> <span data-ttu-id="9c147-220">Это позволит настроить их при использовании действия AzureMLBatchExecution.</span><span class="sxs-lookup"><span data-stu-id="9c147-220">This configuration allows the reader/writer modules to be configured when using the AzureMLBatchExecution activity.</span></span> <span data-ttu-id="9c147-221">Параметры веб-службы указываются в разделе **globalParameters** действия JSON, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="9c147-221">You specify Web service parameters in the **globalParameters** section in the activity JSON as follows.</span></span>

```JSON
"typeProperties": {
    "globalParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```

<span data-ttu-id="9c147-222">Вы также можете использовать [функции фабрики данных](data-factory-functions-variables.md) при передаче значений для параметров веб-службы, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="9c147-222">You can also use [Data Factory Functions](data-factory-functions-variables.md) in passing values for the Web service parameters as shown in the following example:</span></span>

```JSON
"typeProperties": {
    "globalParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> <span data-ttu-id="9c147-223">В параметрах веб-службы учитывается регистр, поэтому убедитесь, что имена, которые указываются в действии JSON, соответствуют именам, предоставляемым веб-службой.</span><span class="sxs-lookup"><span data-stu-id="9c147-223">The Web service parameters are case-sensitive, so ensure that the names you specify in the activity JSON match the ones exposed by the Web service.</span></span>
>
>

### <a name="using-a-reader-module-to-read-data-from-multiple-files-in-azure-blob"></a><span data-ttu-id="9c147-224">Использование модуля чтения для чтения данных из нескольких файлов в большом двоичном объекте Azure</span><span class="sxs-lookup"><span data-stu-id="9c147-224">Using a Reader module to read data from multiple files in Azure Blob</span></span>
<span data-ttu-id="9c147-225">Конвейеры больших данных с такими действиями, как Pig и Hive, могут формировать один или несколько выходных файлов без расширений.</span><span class="sxs-lookup"><span data-stu-id="9c147-225">Big data pipelines with activities such as Pig and Hive can produce one or more output files with no extensions.</span></span> <span data-ttu-id="9c147-226">Например, если указать внешнюю таблицу Hive, данные для нее могут храниться в хранилище больших двоичных объектов с следующим именем: 000000_0.</span><span class="sxs-lookup"><span data-stu-id="9c147-226">For example, when you specify an external Hive table, the data for the external Hive table can be stored in Azure blob storage with the following name 000000_0.</span></span> <span data-ttu-id="9c147-227">В эксперименте можно применять модуль чтения для чтения нескольких файлов и использовать их для прогнозирования.</span><span class="sxs-lookup"><span data-stu-id="9c147-227">You can use the reader module in an experiment to read multiple files, and use them for predictions.</span></span>

<span data-ttu-id="9c147-228">При использовании модуля чтения в эксперименте Машинного обучения Azure вы можете указать в качестве входных данных большой двоичный объект Azure.</span><span class="sxs-lookup"><span data-stu-id="9c147-228">When using the reader module in an Azure Machine Learning experiment, you can specify Azure Blob as an input.</span></span> <span data-ttu-id="9c147-229">Файлы в хранилище BLOB-объектов Azure могут представлять собой выходные файлы (например, 000000_0), созданные с помощью сценария Pig и Hive, который выполняется в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9c147-229">The files in the Azure blob storage can be the output files (Example: 000000_0) that are produced by a Pig and Hive script running on HDInsight.</span></span> <span data-ttu-id="9c147-230">Модуль чтения позволяет читать файлы (без расширений). Для этого необходимо настроить параметр **Path to container, directory/blob** (Путь к контейнеру, каталогу или большому двоичному объекту).</span><span class="sxs-lookup"><span data-stu-id="9c147-230">The reader module allows you to read files (with no extensions) by configuring the **Path to container, directory/blob**.</span></span> <span data-ttu-id="9c147-231">Параметр **Path to container** (Путь к контейнеру) указывает на контейнер, а **directory/blob** (Путь к каталогу или большому двоичному объекту) — на папку, содержащую файлы, как показано на рисунке ниже.</span><span class="sxs-lookup"><span data-stu-id="9c147-231">The **Path to container** points to the container and **directory/blob** points to folder that contains the files as shown in the following image.</span></span> <span data-ttu-id="9c147-232">Звездочка (\*) **указывает на то, что все файлы в контейнере или папке (например, data/aggregateddata/year=2014/month-6/\*)** будут считываться в рамках эксперимента.</span><span class="sxs-lookup"><span data-stu-id="9c147-232">The asterisk that is, \*) **specifies that all the files in the container/folder (that is, data/aggregateddata/year=2014/month-6/\*)** are read as part of the experiment.</span></span>

![Свойства большого двоичного объекта Azure](./media/data-factory-create-predictive-pipelines/azure-blob-properties.png)

### <a name="example"></a><span data-ttu-id="9c147-234">Пример</span><span class="sxs-lookup"><span data-stu-id="9c147-234">Example</span></span>
#### <a name="pipeline-with-azuremlbatchexecution-activity-with-web-service-parameters"></a><span data-ttu-id="9c147-235">Конвейер с действием AzureMLBatchExecution с параметрами веб-службы</span><span class="sxs-lookup"><span data-stu-id="9c147-235">Pipeline with AzureMLBatchExecution activity with Web Service Parameters</span></span>

```JSON
{
  "name": "MLWithSqlReaderSqlWriter",
  "properties": {
    "description": "Azure ML model with sql azure reader/writer",
    "activities": [
      {
        "name": "MLSqlReaderSqlWriterActivity",
        "type": "AzureMLBatchExecution",
        "description": "test",
        "inputs": [
          {
            "name": "MLSqlInput"
          }
        ],
        "outputs": [
          {
            "name": "MLSqlOutput"
          }
        ],
        "linkedServiceName": "MLSqlReaderSqlWriterDecisionTreeModel",
        "typeProperties":
        {
            "webServiceInput": "MLSqlInput",
            "webServiceOutputs": {
                "output1": "MLSqlOutput"
            }
              "globalParameters": {
                "Database server name": "<myserver>.database.windows.net",
                "Database name": "<database>",
                "Server user account name": "<user name>",
                "Server user account password": "<password>"
              }              
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        },
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```

<span data-ttu-id="9c147-236">В приведенном выше примере JSON:</span><span class="sxs-lookup"><span data-stu-id="9c147-236">In the above JSON example:</span></span>

* <span data-ttu-id="9c147-237">Развернутая веб-служба Машинного обучения Azureиспользует модуль чтения и модуль записи для чтения данных из базы данных SQL Azure и записи их в нее.</span><span class="sxs-lookup"><span data-stu-id="9c147-237">The deployed Azure Machine Learning Web service uses a reader and a writer module to read/write data from/to an Azure SQL Database.</span></span> <span data-ttu-id="9c147-238">Эта веб-служба предоставляет следующие параметры: Database server name, Database name, Server user account name и Server user account password.</span><span class="sxs-lookup"><span data-stu-id="9c147-238">This Web service exposes the following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span></span>  
* <span data-ttu-id="9c147-239">Даты **начала** и **окончания** должны быть в [формате ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="9c147-239">Both **start** and **end** datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="9c147-240">Например, 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="9c147-240">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="9c147-241">Значение времени окончания (**end**) является необязательным.</span><span class="sxs-lookup"><span data-stu-id="9c147-241">The **end** time is optional.</span></span> <span data-ttu-id="9c147-242">Если не указать значение свойства **end**, оно вычисляется по формуле **время начала + 48 часов**.</span><span class="sxs-lookup"><span data-stu-id="9c147-242">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours.**"</span></span> <span data-ttu-id="9c147-243">Чтобы запустить конвейер в течение неопределенного срока, укажите значение **9999-09-09** в качестве значения свойства **end**.</span><span class="sxs-lookup"><span data-stu-id="9c147-243">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span> <span data-ttu-id="9c147-244">Дополнительные сведения о свойствах JSON см. в [справочнике по скриптам JSON](https://msdn.microsoft.com/library/dn835050.aspx).</span><span class="sxs-lookup"><span data-stu-id="9c147-244">See [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) for details about JSON properties.</span></span>

### <a name="other-scenarios"></a><span data-ttu-id="9c147-245">Другие сценарии</span><span class="sxs-lookup"><span data-stu-id="9c147-245">Other scenarios</span></span>
#### <a name="web-service-requires-multiple-inputs"></a><span data-ttu-id="9c147-246">Веб-службе требуется несколько входных данных</span><span class="sxs-lookup"><span data-stu-id="9c147-246">Web service requires multiple inputs</span></span>
<span data-ttu-id="9c147-247">Если веб-служба принимает несколько входных наборов данных, используйте свойство **webServiceInputs** вместо **webServiceInput**.</span><span class="sxs-lookup"><span data-stu-id="9c147-247">If the web service takes multiple inputs, use the **webServiceInputs** property instead of using **webServiceInput**.</span></span> <span data-ttu-id="9c147-248">Наборы данных, на которые ссылается свойство **webServiceInputs**, также должны быть включены в раздел **inputs** действия.</span><span class="sxs-lookup"><span data-stu-id="9c147-248">Datasets that are referenced by the **webServiceInputs** must also be included in the Activity **inputs**.</span></span>

<span data-ttu-id="9c147-249">В эксперименте Машинного обучения Azure у входных и выходных портов и глобальных параметров есть имена по умолчанию (input1, input2), которые можно настроить.</span><span class="sxs-lookup"><span data-stu-id="9c147-249">In your Azure ML experiment, web service input and output ports and global parameters have default names ("input1", "input2") that you can customize.</span></span> <span data-ttu-id="9c147-250">Имена, используемые для параметров webServiceInputs, webServiceOutputs и globalParameters, должны точно совпадать с именами в экспериментах.</span><span class="sxs-lookup"><span data-stu-id="9c147-250">The names you use for webServiceInputs, webServiceOutputs, and globalParameters settings must exactly match the names in the experiments.</span></span> <span data-ttu-id="9c147-251">Пример полезных данных запроса можно просмотреть на странице справки по выполнению пакета для конечной точки Машинного обучения Azure, чтобы проверить ожидаемое сопоставление.</span><span class="sxs-lookup"><span data-stu-id="9c147-251">You can view the sample request payload on the Batch Execution Help page for your Azure ML endpoint to verify the expected mapping.</span></span>

```JSON
{
    "name": "PredictivePipeline",
    "properties": {
        "description": "use AzureML model",
        "activities": [{
            "name": "MLActivity",
            "type": "AzureMLBatchExecution",
            "description": "prediction analysis on batch input",
            "inputs": [{
                "name": "inputDataset1"
            }, {
                "name": "inputDataset2"
            }],
            "outputs": [{
                "name": "outputDataset"
            }],
            "linkedServiceName": "MyAzureMLLinkedService",
            "typeProperties": {
                "webServiceInputs": {
                    "input1": "inputDataset1",
                    "input2": "inputDataset2"
                },
                "webServiceOutputs": {
                    "output1": "outputDataset"
                }
            },
            "policy": {
                "concurrency": 3,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "02:00:00"
            }
        }],
        "start": "2016-02-13T00:00:00Z",
        "end": "2016-02-14T00:00:00Z"
    }
}
```

#### <a name="web-service-does-not-require-an-input"></a><span data-ttu-id="9c147-252">Веб-служба не требует входных данных</span><span class="sxs-lookup"><span data-stu-id="9c147-252">Web Service does not require an input</span></span>
<span data-ttu-id="9c147-253">Веб-службы пакетного выполнения Azure ML можно использовать для выполнения любых рабочих процессов, например сценариев R и Python, не требующих никаких входных данных.</span><span class="sxs-lookup"><span data-stu-id="9c147-253">Azure ML batch execution web services can be used to run any workflows, for example R or Python scripts, that may not require any inputs.</span></span> <span data-ttu-id="9c147-254">Кроме того, эксперимент можно настроить с помощью модуля чтения, не предоставляющего никаких глобальных параметров.</span><span class="sxs-lookup"><span data-stu-id="9c147-254">Or, the experiment might be configured with a Reader module that does not expose any GlobalParameters.</span></span> <span data-ttu-id="9c147-255">В этом случае настройка действия AzureMLBatchExecution выполняется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9c147-255">In that case, the AzureMLBatchExecution Activity would be configured as follows:</span></span>

```JSON
{
    "name": "scoring service",
    "type": "AzureMLBatchExecution",
    "outputs": [
        {
            "name": "myBlob"
        }
    ],
    "typeProperties": {
        "webServiceOutputs": {
            "output1": "myBlob"
        }              
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

#### <a name="web-service-does-not-require-an-inputoutput"></a><span data-ttu-id="9c147-256">Веб-служба не требует входных или выходных данных</span><span class="sxs-lookup"><span data-stu-id="9c147-256">Web Service does not require an input/output</span></span>
<span data-ttu-id="9c147-257">В веб-службе пакетного выполнения Azure ML выходные данные могут быть не настроены.</span><span class="sxs-lookup"><span data-stu-id="9c147-257">The Azure ML batch execution web service might not have any Web Service output configured.</span></span> <span data-ttu-id="9c147-258">В данном примере не настроены ни входные или выходные параметры, ни глобальные параметры.</span><span class="sxs-lookup"><span data-stu-id="9c147-258">In this example, there is no Web Service input or output, nor are any GlobalParameters configured.</span></span> <span data-ttu-id="9c147-259">Выходные данные в действии настроены, но не назначены в качестве выходных данных в свойстве webServiceOutput.</span><span class="sxs-lookup"><span data-stu-id="9c147-259">There is still an output configured on the activity itself, but it is not given as a webServiceOutput.</span></span>

```JSON
{
    "name": "retraining",
    "type": "AzureMLBatchExecution",
    "outputs": [
        {
            "name": "placeholderOutputDataset"
        }
    ],
    "typeProperties": {
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

#### <a name="web-service-uses-readers-and-writers-and-the-activity-runs-only-when-other-activities-have-succeeded"></a><span data-ttu-id="9c147-260">Веб-служба использует модули чтения и записи, а действие выполняется только при успешном завершении других действий</span><span class="sxs-lookup"><span data-stu-id="9c147-260">Web Service uses readers and writers, and the activity runs only when other activities have succeeded</span></span>
<span data-ttu-id="9c147-261">Модули чтения и записи веб-службы Azure ML могут быть настроены на работу с использованием или без использования глобальных параметров.</span><span class="sxs-lookup"><span data-stu-id="9c147-261">The Azure ML web service reader and writer modules might be configured to run with or without any GlobalParameters.</span></span> <span data-ttu-id="9c147-262">Однако вызовы службы можно встроить в конвейер с использованием зависимостей наборов данных для вызова службы только при успешном завершении обработки вышестоящих данных.</span><span class="sxs-lookup"><span data-stu-id="9c147-262">However, you may want to embed service calls in a pipeline that uses dataset dependencies to invoke the service only when some upstream processing has completed.</span></span> <span data-ttu-id="9c147-263">При таком подходе после окончания пакетного выполнения можно запустить другое действие.</span><span class="sxs-lookup"><span data-stu-id="9c147-263">You can also trigger some other action after the batch execution has completed using this approach.</span></span> <span data-ttu-id="9c147-264">В этом случае зависимости можно представить, используя входные и выходные данные действия, но не называя их входными или выходными данными веб-службы.</span><span class="sxs-lookup"><span data-stu-id="9c147-264">In that case, you can express the dependencies using activity inputs and outputs, without naming any of them as Web Service inputs or outputs.</span></span>

```JSON
{
    "name": "retraining",
    "type": "AzureMLBatchExecution",
    "inputs": [
        {
            "name": "upstreamData1"
        },
        {
            "name": "upstreamData2"
        }
    ],
    "outputs": [
        {
            "name": "downstreamData"
        }
    ],
    "typeProperties": {
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

<span data-ttu-id="9c147-265">**Общие выводы** :</span><span class="sxs-lookup"><span data-stu-id="9c147-265">The **takeaways** are:</span></span>

* <span data-ttu-id="9c147-266">Если в конечной точке эксперимента используются входные данные веб-службы, они представляются набором данных больших двоичных объектов и включаются во входные данные действия, а также в свойство webServiceInput.</span><span class="sxs-lookup"><span data-stu-id="9c147-266">If your experiment endpoint uses a webServiceInput: it is represented by a blob dataset and is included in the activity inputs and the webServiceInput property.</span></span> <span data-ttu-id="9c147-267">В противном случае свойство webServiceInput опускается.</span><span class="sxs-lookup"><span data-stu-id="9c147-267">Otherwise, the webServiceInput property is omitted.</span></span>
* <span data-ttu-id="9c147-268">Если в конечной точке эксперимента используются выходные данные веб-службы, они представляются наборами данных больших двоичных объектов и включаются в выходные данные действия, а также в свойство webServiceOutputs.</span><span class="sxs-lookup"><span data-stu-id="9c147-268">If your experiment endpoint uses webServiceOutput(s): they are represented by blob datasets and are included in the activity outputs and in the webServiceOutputs property.</span></span> <span data-ttu-id="9c147-269">Выходные данные действия и свойство webServiceOutputs сопоставляются с именем выходных данных в эксперименте.</span><span class="sxs-lookup"><span data-stu-id="9c147-269">The activity outputs and webServiceOutputs are mapped by the name of each output in the experiment.</span></span> <span data-ttu-id="9c147-270">В противном случае свойство webServiceOutputs опускается.</span><span class="sxs-lookup"><span data-stu-id="9c147-270">Otherwise, the webServiceOutputs property is omitted.</span></span>
* <span data-ttu-id="9c147-271">Если конечная точка эксперимента раскрывает глобальные параметры, они даются в свойстве globalParameters действия в виде пар "ключ — значение".</span><span class="sxs-lookup"><span data-stu-id="9c147-271">If your experiment endpoint exposes globalParameter(s), they are given in the activity globalParameters property as key, value pairs.</span></span> <span data-ttu-id="9c147-272">В противном случае свойство globalParameters опускается.</span><span class="sxs-lookup"><span data-stu-id="9c147-272">Otherwise, the globalParameters property is omitted.</span></span> <span data-ttu-id="9c147-273">В ключах учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="9c147-273">The keys are case-sensitive.</span></span> <span data-ttu-id="9c147-274">[функции фабрики данных Azure](data-factory-functions-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="9c147-274">[Azure Data Factory functions](data-factory-functions-variables.md) may be used in the values.</span></span>
* <span data-ttu-id="9c147-275">Дополнительные наборы данных могут включаться в свойства входных и выходных данных действия без включения соответствующих ссылок в раздел typeProperties свойства.</span><span class="sxs-lookup"><span data-stu-id="9c147-275">Additional datasets may be included in the Activity inputs and outputs properties, without being referenced in the Activity typeProperties.</span></span> <span data-ttu-id="9c147-276">Они управляют выполнением с помощью зависимостей срезов. В остальном действие AzureMLBatchExecution их игнорирует.</span><span class="sxs-lookup"><span data-stu-id="9c147-276">These datasets govern execution using slice dependencies but are otherwise ignored by the AzureMLBatchExecution Activity.</span></span>


## <a name="updating-models-using-update-resource-activity"></a><span data-ttu-id="9c147-277">Обновление моделей с помощью действия обновления ресурса</span><span class="sxs-lookup"><span data-stu-id="9c147-277">Updating models using Update Resource Activity</span></span>
<span data-ttu-id="9c147-278">Когда повторное обучение будет завершено, обновите веб-службу оценки (прогнозный эксперимент, опубликованный в виде веб-службы) на основании обученной заново модели, используя **действие обновления ресурса машинного обучения Azure**.</span><span class="sxs-lookup"><span data-stu-id="9c147-278">After you are done with retraining, update the scoring web service (predictive experiment exposed as a web service) with the newly trained model by using the **Azure ML Update Resource Activity**.</span></span> <span data-ttu-id="9c147-279">Дополнительные сведения см. в статье [Updating Azure Machine Learning models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) (Обновление моделей машинного обучения Azure с помощью действия "Обновить ресурс").</span><span class="sxs-lookup"><span data-stu-id="9c147-279">See [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) article for details.</span></span>

### <a name="reader-and-writer-modules"></a><span data-ttu-id="9c147-280">Модули чтения и записи</span><span class="sxs-lookup"><span data-stu-id="9c147-280">Reader and Writer Modules</span></span>
<span data-ttu-id="9c147-281">Распространенный сценарий использования параметров веб-службы заключается в использовании модулей чтения и записи SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="9c147-281">A common scenario for using Web service parameters is the use of Azure SQL Readers and Writers.</span></span> <span data-ttu-id="9c147-282">Модуль чтения используется для загрузки данных в эксперимент из служб управления данными за пределами Студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="9c147-282">The reader module is used to load data into an experiment from data management services outside Azure Machine Learning Studio.</span></span> <span data-ttu-id="9c147-283">Модуль записи используется для сохранения данных из экспериментов в службах управления данными за пределами Студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="9c147-283">The writer module is to save data from your experiments into data management services outside Azure Machine Learning Studio.</span></span>  

<span data-ttu-id="9c147-284">Сведения о модулях [чтения](https://msdn.microsoft.com/library/azure/dn905997.aspx) и [записи](https://msdn.microsoft.com/library/azure/dn905984.aspx) больших двоичных объектов Azure и SQL Azure см. в соответствующих разделах в библиотеке MSDN.</span><span class="sxs-lookup"><span data-stu-id="9c147-284">For details about Azure Blob/Azure SQL reader/writer, see [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span></span> <span data-ttu-id="9c147-285">В примере из предыдущего раздела используется модуль чтения и модуль записи больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="9c147-285">The example in the previous section used the Azure Blob reader and Azure Blob writer.</span></span> <span data-ttu-id="9c147-286">В этом разделе рассматривается использование модуля чтения и модуля записи SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="9c147-286">This section discusses using Azure SQL reader and Azure SQL writer.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="9c147-287">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="9c147-287">Frequently asked questions</span></span>
<span data-ttu-id="9c147-288">**Вопрос.** Имеется несколько файлов, сформированных моими конвейерами больших данных.</span><span class="sxs-lookup"><span data-stu-id="9c147-288">**Q:** I have multiple files that are generated by my big data pipelines.</span></span> <span data-ttu-id="9c147-289">Можно использовать действие AzureMLBatchExecution для работы с этими файлами?</span><span class="sxs-lookup"><span data-stu-id="9c147-289">Can I use the AzureMLBatchExecution Activity to work on all the files?</span></span>

<span data-ttu-id="9c147-290">**Ответ.** Да.</span><span class="sxs-lookup"><span data-stu-id="9c147-290">**A:** Yes.</span></span> <span data-ttu-id="9c147-291">Дополнительные сведения см. в статье **Использование модуля чтения для чтения данных из нескольких файлов в большом двоичном объекте Azure**.</span><span class="sxs-lookup"><span data-stu-id="9c147-291">See the **Using a Reader module to read data from multiple files in Azure Blob** section for details.</span></span>

## <a name="azure-ml-batch-scoring-activity"></a><span data-ttu-id="9c147-292">Действие количественной оценки Azure ML</span><span class="sxs-lookup"><span data-stu-id="9c147-292">Azure ML Batch Scoring Activity</span></span>
<span data-ttu-id="9c147-293">Если вы используете действие **AzureMLBatchScoring** для интеграции с Машинным обучением Azure, мы рекомендуем использовать последнее действие **AzureMLBatchExecution**.</span><span class="sxs-lookup"><span data-stu-id="9c147-293">If you are using the **AzureMLBatchScoring** activity to integrate with Azure Machine Learning, we recommend that you use the latest **AzureMLBatchExecution** activity.</span></span>

<span data-ttu-id="9c147-294">Действие AzureMLBatchExecution введено в 2015 году в августовском выпуске пакета SDK для Azure и Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9c147-294">The AzureMLBatchExecution activity is introduced in the August 2015 release of Azure SDK and Azure PowerShell.</span></span>

<span data-ttu-id="9c147-295">Если вы планируете использовать действие AzureMLBatchScoring дальше, продолжите чтение этого раздела.</span><span class="sxs-lookup"><span data-stu-id="9c147-295">If you want to continue using the AzureMLBatchScoring activity, continue reading through this section.</span></span>  

### <a name="azure-ml-batch-scoring-activity-using-azure-storage-for-inputoutput"></a><span data-ttu-id="9c147-296">Действие количественной оценки Azure ML с использованием хранилища Azure в качестве входных и (или) выходных данных</span><span class="sxs-lookup"><span data-stu-id="9c147-296">Azure ML Batch Scoring activity using Azure Storage for input/output</span></span>

```JSON
{
  "name": "PredictivePipeline",
  "properties": {
    "description": "use AzureML model",
    "activities": [
      {
        "name": "MLActivity",
        "type": "AzureMLBatchScoring",
        "description": "prediction analysis on batch input",
        "inputs": [
          {
            "name": "ScoringInputBlob"
          }
        ],
        "outputs": [
          {
            "name": "ScoringResultBlob"
          }
        ],
        "linkedServiceName": "MyAzureMLLinkedService",
        "policy": {
          "concurrency": 3,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        }
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```

### <a name="web-service-parameters"></a><span data-ttu-id="9c147-297">Параметры веб-службы</span><span class="sxs-lookup"><span data-stu-id="9c147-297">Web Service Parameters</span></span>
<span data-ttu-id="9c147-298">Чтобы указать значения для параметров веб-службы, добавьте раздел **typeProperties** в раздел **AzureMLBatchScoringActivty** в конвейере JSON, как показано в примере ниже.</span><span class="sxs-lookup"><span data-stu-id="9c147-298">To specify values for Web service parameters, add a **typeProperties** section to the **AzureMLBatchScoringActivty** section in the pipeline JSON as shown in the following example:</span></span>

```JSON
"typeProperties": {
    "webServiceParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```
<span data-ttu-id="9c147-299">Вы также можете использовать [функции фабрики данных](data-factory-functions-variables.md) при передаче значений для параметров веб-службы, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="9c147-299">You can also use [Data Factory Functions](data-factory-functions-variables.md) in passing values for the Web service parameters as shown in the following example:</span></span>

```JSON
"typeProperties": {
    "webServiceParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> <span data-ttu-id="9c147-300">В параметрах веб-службы учитывается регистр, поэтому убедитесь, что имена, которые указываются в действии JSON, соответствуют именам, предоставляемым веб-службой.</span><span class="sxs-lookup"><span data-stu-id="9c147-300">The Web service parameters are case-sensitive, so ensure that the names you specify in the activity JSON match the ones exposed by the Web service.</span></span>
>
>

## <a name="see-also"></a><span data-ttu-id="9c147-301">См. также</span><span class="sxs-lookup"><span data-stu-id="9c147-301">See Also</span></span>
* [<span data-ttu-id="9c147-302">Запись блога Azure: «Приступая к работе с фабрикой данных Azure и Машинным обучением Azure»</span><span class="sxs-lookup"><span data-stu-id="9c147-302">Azure blog post: Getting started with Azure Data Factory and Azure Machine Learning</span></span>](https://azure.microsoft.com/blog/getting-started-with-azure-data-factory-and-azure-machine-learning-4/)

[adf-build-1st-pipeline]: data-factory-build-your-first-pipeline.md

[azure-machine-learning]: http://azure.microsoft.com/services/machine-learning/
