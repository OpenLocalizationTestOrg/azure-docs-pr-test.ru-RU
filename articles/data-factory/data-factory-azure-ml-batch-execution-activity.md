---
title: "конвейеры aaaCreate прогнозирующих данных, с помощью фабрики данных Azure | Документы Microsoft"
description: "Описывает, как toocreate создание прогнозирующих конвейеров с помощью фабрики данных Azure и машинного обучения Azure"
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
ms.openlocfilehash: 943210c28b1696e299ff9b7cc96369b95f182354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-predictive-pipelines-using-azure-machine-learning-and-azure-data-factory"></a><span data-ttu-id="0acbf-103">Создание прогнозирующих конвейеров с помощью машинного обучения Azure и фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="0acbf-103">Create predictive pipelines using Azure Machine Learning and Azure Data Factory</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="0acbf-104">Действие Hive</span><span class="sxs-lookup"><span data-stu-id="0acbf-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="0acbf-105">Действие Pig</span><span class="sxs-lookup"><span data-stu-id="0acbf-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="0acbf-106">Действие MapReduce</span><span class="sxs-lookup"><span data-stu-id="0acbf-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="0acbf-107">Потоковая активность Hadoop</span><span class="sxs-lookup"><span data-stu-id="0acbf-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="0acbf-108">Действие Spark</span><span class="sxs-lookup"><span data-stu-id="0acbf-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="0acbf-109">Действие выполнения пакета машинного обучения</span><span class="sxs-lookup"><span data-stu-id="0acbf-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="0acbf-110">Действие "Обновить ресурс" в службе машинного обучения</span><span class="sxs-lookup"><span data-stu-id="0acbf-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="0acbf-111">Действие хранимой процедуры</span><span class="sxs-lookup"><span data-stu-id="0acbf-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="0acbf-112">Действие U-SQL в Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="0acbf-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="0acbf-113">Настраиваемое действие .NET</span><span class="sxs-lookup"><span data-stu-id="0acbf-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="introduction"></a><span data-ttu-id="0acbf-114">Введение</span><span class="sxs-lookup"><span data-stu-id="0acbf-114">Introduction</span></span>

### <a name="azure-machine-learning"></a><span data-ttu-id="0acbf-115">Машинное обучение Azure</span><span class="sxs-lookup"><span data-stu-id="0acbf-115">Azure Machine Learning</span></span>
<span data-ttu-id="0acbf-116">[Машинное обучение Azure](https://azure.microsoft.com/documentation/services/machine-learning/) позволяет toobuild, тестировать и развертывать прогнозирующие аналитические решения.</span><span class="sxs-lookup"><span data-stu-id="0acbf-116">[Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) enables you toobuild, test, and deploy predictive analytics solutions.</span></span> <span data-ttu-id="0acbf-117">Этот процесс можно обобщить до трех этапов.</span><span class="sxs-lookup"><span data-stu-id="0acbf-117">From a high-level point of view, it is done in three steps:</span></span>

1. <span data-ttu-id="0acbf-118">**Создание обучающего эксперимента**.</span><span class="sxs-lookup"><span data-stu-id="0acbf-118">**Create a training experiment**.</span></span> <span data-ttu-id="0acbf-119">Выполните этот шаг с помощью hello Azure ML Studio.</span><span class="sxs-lookup"><span data-stu-id="0acbf-119">You do this step by using hello Azure ML Studio.</span></span> <span data-ttu-id="0acbf-120">Hello ML studio является коллективную визуальную среду разработки использовать tootrain и проверки модели прогнозирования с помощью обучающих данных.</span><span class="sxs-lookup"><span data-stu-id="0acbf-120">hello ML studio is a collaborative visual development environment that you use tootrain and test a predictive analytics model using training data.</span></span>
2. <span data-ttu-id="0acbf-121">**Преобразовать прогнозной эксперимента tooa**.</span><span class="sxs-lookup"><span data-stu-id="0acbf-121">**Convert it tooa predictive experiment**.</span></span> <span data-ttu-id="0acbf-122">После обучения модели с существующие данные и будут готовы toouse его tooscore новых данных, подготовки и оптимизировать свой эксперимент оценки.</span><span class="sxs-lookup"><span data-stu-id="0acbf-122">Once your model has been trained with existing data and you are ready toouse it tooscore new data, you prepare and streamline your experiment for scoring.</span></span>
3. <span data-ttu-id="0acbf-123">**Развертывание эксперимента в виде веб-службы**.</span><span class="sxs-lookup"><span data-stu-id="0acbf-123">**Deploy it as a web service**.</span></span> <span data-ttu-id="0acbf-124">Оценивающий эксперимент можно опубликовать в виде веб-службы Azure.</span><span class="sxs-lookup"><span data-stu-id="0acbf-124">You can publish your scoring experiment as an Azure web service.</span></span> <span data-ttu-id="0acbf-125">Можно отправлять tooyour модели данных посредством этой конечной точки службы web и получения результатов прогнозов из модели hello.</span><span class="sxs-lookup"><span data-stu-id="0acbf-125">You can send data tooyour model via this web service end point and receive result predictions fro hello model.</span></span>  

### <a name="azure-data-factory"></a><span data-ttu-id="0acbf-126">Фабрика данных Azure</span><span class="sxs-lookup"><span data-stu-id="0acbf-126">Azure Data Factory</span></span>
<span data-ttu-id="0acbf-127">Фабрика данных — это служба интеграции данных на основе облака, которая координирует и автоматизирует процессы hello **перемещения** и **преобразования** данных.</span><span class="sxs-lookup"><span data-stu-id="0acbf-127">Data Factory is a cloud-based data integration service that orchestrates and automates hello **movement** and **transformation** of data.</span></span> <span data-ttu-id="0acbf-128">Можно создать решений по интеграции данных с помощью фабрики данных Azure, можно получать данные из различных хранилищ данных, преобразования или процесс данных hello и публикации хранилищ данных toohello данных результата hello.</span><span class="sxs-lookup"><span data-stu-id="0acbf-128">You can create data integration solutions using Azure Data Factory that can ingest data from various data stores, transform/process hello data, and publish hello result data toohello data stores.</span></span>

<span data-ttu-id="0acbf-129">Служба фабрики данных позволяет вам toocreate конвейеры данных, перемещения и преобразования данных и запустите конвейеры hello по указанному расписанию (ежечасно, ежедневно, еженедельно, и т. д.).</span><span class="sxs-lookup"><span data-stu-id="0acbf-129">Data Factory service allows you toocreate data pipelines that move and transform data, and then run hello pipelines on a specified schedule (hourly, daily, weekly, etc.).</span></span> <span data-ttu-id="0acbf-130">Также предоставляет широкие возможности визуализации toodisplay hello журнала обращений и преобразований, так и зависимости между конвейеры данных и отслеживать все конвейеры данных из найти решение проблем с tooeasily единое представление и установки предупреждений мониторинга.</span><span class="sxs-lookup"><span data-stu-id="0acbf-130">It also provides rich visualizations toodisplay hello lineage and dependencies between your data pipelines, and monitor all your data pipelines from a single unified view tooeasily pinpoint issues and setup monitoring alerts.</span></span>

<span data-ttu-id="0acbf-131">В разделе [tooAzure введение фабрики данных](data-factory-introduction.md) и [построение первой конвейер](data-factory-build-your-first-pipeline.md) tooquickly статьи Приступая к работе с hello служба фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="0acbf-131">See [Introduction tooAzure Data Factory](data-factory-introduction.md) and [Build your first pipeline](data-factory-build-your-first-pipeline.md) articles tooquickly get started with hello Azure Data Factory service.</span></span>

### <a name="data-factory-and-machine-learning-together"></a><span data-ttu-id="0acbf-132">Фабрика данных и машинное обучение вместе</span><span class="sxs-lookup"><span data-stu-id="0acbf-132">Data Factory and Machine Learning together</span></span>
<span data-ttu-id="0acbf-133">Azure позволяет фабрики данных, вы tooeasily создавать конвейеры, использующих опубликованной [машинного обучения Azure] [ azure-machine-learning] веб-службы для прогнозирования.</span><span class="sxs-lookup"><span data-stu-id="0acbf-133">Azure Data Factory enables you tooeasily create pipelines that use a published [Azure Machine Learning][azure-machine-learning] web service for predictive analytics.</span></span> <span data-ttu-id="0acbf-134">С помощью hello **действие выполнения пакета** в конвейере фабрики данных Azure, можно вызвать прогнозы toomake машинного Обучения Azure веб-службы на hello данных в пакете.</span><span class="sxs-lookup"><span data-stu-id="0acbf-134">Using hello **Batch Execution Activity** in an Azure Data Factory pipeline, you can invoke an Azure ML web service toomake predictions on hello data in batch.</span></span> <span data-ttu-id="0acbf-135">В разделе [вызова машинного Обучения Azure веб-службы с использованием hello действие выполнения пакета](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) подробные сведения см.</span><span class="sxs-lookup"><span data-stu-id="0acbf-135">See [Invoking an Azure ML web service using hello Batch Execution Activity](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) section for details.</span></span>

<span data-ttu-id="0acbf-136">Со временем hello прогнозных моделей в экспериментах оценки машинного Обучения Azure hello должны toobe повторное обучение с помощью новых входных наборов данных.</span><span class="sxs-lookup"><span data-stu-id="0acbf-136">Over time, hello predictive models in hello Azure ML scoring experiments need toobe retrained using new input datasets.</span></span> <span data-ttu-id="0acbf-137">Можно повторить Обучение модели машинного Обучения Azure из конвейера фабрики данных, выполнив следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="0acbf-137">You can retrain an Azure ML model from a Data Factory pipeline by doing hello following steps:</span></span>

1. <span data-ttu-id="0acbf-138">Опубликуйте эксперимента обучения hello (не прогнозной эксперимента) как веб-службы.</span><span class="sxs-lookup"><span data-stu-id="0acbf-138">Publish hello training experiment (not predictive experiment) as a web service.</span></span> <span data-ttu-id="0acbf-139">На этом шаге hello Azure ML Studio сделать, как в случае tooexpose прогнозной эксперимент как веб-службы в предыдущем сценарии hello.</span><span class="sxs-lookup"><span data-stu-id="0acbf-139">You do this step in hello Azure ML Studio as you did tooexpose predictive experiment as a web service in hello previous scenario.</span></span>
2. <span data-ttu-id="0acbf-140">Используйте hello действие выполнения пакета машинного Обучения Azure tooinvoke hello веб-службы для hello эксперимента обучения.</span><span class="sxs-lookup"><span data-stu-id="0acbf-140">Use hello Azure ML Batch Execution Activity tooinvoke hello web service for hello training experiment.</span></span> <span data-ttu-id="0acbf-141">По сути можно использовать tooinvoke действие hello Azure ML Пакетное выполнение веб-службы обучения и оценки веб-службы.</span><span class="sxs-lookup"><span data-stu-id="0acbf-141">Basically, you can use hello Azure ML Batch Execution activity tooinvoke both training web service and scoring web service.</span></span>

<span data-ttu-id="0acbf-142">После завершения переподготовки, обновите hello оценки веб-службы (прогнозной эксперимент, предоставляемых как веб-службы) с hello вновь обученной модели с помощью hello **действия ресурса обновления машинного Обучения Azure**.</span><span class="sxs-lookup"><span data-stu-id="0acbf-142">After you are done with retraining, update hello scoring web service (predictive experiment exposed as a web service) with hello newly trained model by using hello **Azure ML Update Resource Activity**.</span></span> <span data-ttu-id="0acbf-143">Дополнительные сведения см. в статье [Updating Azure Machine Learning models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) (Обновление моделей машинного обучения Azure с помощью действия "Обновить ресурс").</span><span class="sxs-lookup"><span data-stu-id="0acbf-143">See [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) article for details.</span></span>

## <a name="invoking-a-web-service-using-batch-execution-activity"></a><span data-ttu-id="0acbf-144">Вызов веб-службы с помощью действия выполнения пакета</span><span class="sxs-lookup"><span data-stu-id="0acbf-144">Invoking a web service using Batch Execution Activity</span></span>
<span data-ttu-id="0acbf-145">Перемещение данных tooorchestrate фабрики данных Azure и обработки и затем выполнить пакетное выполнение с помощью машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="0acbf-145">You use Azure Data Factory tooorchestrate data movement and processing, and then perform batch execution using Azure Machine Learning.</span></span> <span data-ttu-id="0acbf-146">Ниже приведены шаги верхнего уровня hello.</span><span class="sxs-lookup"><span data-stu-id="0acbf-146">Here are hello top-level steps:</span></span>

1. <span data-ttu-id="0acbf-147">Создайте связанную службу Машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="0acbf-147">Create an Azure Machine Learning linked service.</span></span> <span data-ttu-id="0acbf-148">Требуется hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="0acbf-148">You need hello following values:</span></span>

   1. <span data-ttu-id="0acbf-149">**URI запроса** для hello API выполнения пакета.</span><span class="sxs-lookup"><span data-stu-id="0acbf-149">**Request URI** for hello Batch Execution API.</span></span> <span data-ttu-id="0acbf-150">Hello URI запроса можно найти, щелкнув hello **ПАКЕТНОЕ выполнение** ссылку hello веб-странице службы.</span><span class="sxs-lookup"><span data-stu-id="0acbf-150">You can find hello Request URI by clicking hello **BATCH EXECUTION** link in hello web services page.</span></span>
   2. <span data-ttu-id="0acbf-151">**Ключ API** hello опубликованных веб-службы машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="0acbf-151">**API key** for hello published Azure Machine Learning web service.</span></span> <span data-ttu-id="0acbf-152">Ключ API hello можно найти, щелкнув hello веб-службу, которая опубликована.</span><span class="sxs-lookup"><span data-stu-id="0acbf-152">You can find hello API key by clicking hello web service that you have published.</span></span>
   3. <span data-ttu-id="0acbf-153">Используйте hello **AzureMLBatchExecution** действия.</span><span class="sxs-lookup"><span data-stu-id="0acbf-153">Use hello **AzureMLBatchExecution** activity.</span></span>

      ![Панель мониторинга машинного обучения](./media/data-factory-azure-ml-batch-execution-activity/AzureMLDashboard.png)

      ![Универсальный код ресурса (URI) пакета](./media/data-factory-azure-ml-batch-execution-activity/batch-uri.png)

### <a name="scenario-experiments-using-web-service-inputsoutputs-that-refer-toodata-in-azure-blob-storage"></a><span data-ttu-id="0acbf-156">Сценарий: Экспериментов с помощью Web service ввода вывода, ссылающиеся toodata в хранилище больших двоичных объектов Azure</span><span class="sxs-lookup"><span data-stu-id="0acbf-156">Scenario: Experiments using Web service inputs/outputs that refer toodata in Azure Blob Storage</span></span>
<span data-ttu-id="0acbf-157">В этом сценарии hello Azure Machine Learning, веб-службы делает прогнозов с использованием данных из файла в хранилище больших двоичных объектов и сохраняет результаты прогноза hello в hello хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="0acbf-157">In this scenario, hello Azure Machine Learning Web service makes predictions using data from a file in an Azure blob storage and stores hello prediction results in hello blob storage.</span></span> <span data-ttu-id="0acbf-158">Hello следующий JSON определяет конвейера фабрики данных с AzureMLBatchExecution действия.</span><span class="sxs-lookup"><span data-stu-id="0acbf-158">hello following JSON defines a Data Factory pipeline with an AzureMLBatchExecution activity.</span></span> <span data-ttu-id="0acbf-159">Hello действие имеет набор данных hello **DecisionTreeInputBlob** в качестве входного и **DecisionTreeResultBlob** в качестве выходных данных hello.</span><span class="sxs-lookup"><span data-stu-id="0acbf-159">hello activity has hello dataset **DecisionTreeInputBlob** as input and **DecisionTreeResultBlob** as hello output.</span></span> <span data-ttu-id="0acbf-160">Hello **DecisionTreeInputBlob** передается в качестве входного toohello веб-службы с помощью hello **webServiceInput** свойства JSON.</span><span class="sxs-lookup"><span data-stu-id="0acbf-160">hello **DecisionTreeInputBlob** is passed as an input toohello web service by using hello **webServiceInput** JSON property.</span></span> <span data-ttu-id="0acbf-161">Hello **DecisionTreeResultBlob** передается в качестве выходных данных toohello веб-службы с помощью hello **webServiceOutputs** свойства JSON.</span><span class="sxs-lookup"><span data-stu-id="0acbf-161">hello **DecisionTreeResultBlob** is passed as an output toohello Web service by using hello **webServiceOutputs** JSON property.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="0acbf-162">Если веб-служба hello принимает несколько входов, использовать hello **webServiceInputs** свойство вместо **webServiceInput**.</span><span class="sxs-lookup"><span data-stu-id="0acbf-162">If hello web service takes multiple inputs, use hello **webServiceInputs** property instead of using **webServiceInput**.</span></span> <span data-ttu-id="0acbf-163">. В разделе hello [веб-службы требуется несколько входов](#web-service-requires-multiple-inputs) раздела Пример использования свойства webServiceInputs hello.</span><span class="sxs-lookup"><span data-stu-id="0acbf-163">See hello [Web service requires multiple inputs](#web-service-requires-multiple-inputs) section for an example of using hello webServiceInputs property.</span></span>
>
> <span data-ttu-id="0acbf-164">Наборы данных, на которые ссылается hello **webServiceInput**/**webServiceInputs** и **webServiceOutputs** свойства (в  **typeProperties**) также должно быть включено в действие hello **входов** и **выводит**.</span><span class="sxs-lookup"><span data-stu-id="0acbf-164">Datasets that are referenced by hello **webServiceInput**/**webServiceInputs** and **webServiceOutputs** properties (in **typeProperties**) must also be included in hello Activity **inputs** and **outputs**.</span></span>
>
> <span data-ttu-id="0acbf-165">В эксперименте Машинного обучения Azure у входных и выходных портов и глобальных параметров есть имена по умолчанию (input1, input2), которые можно настроить.</span><span class="sxs-lookup"><span data-stu-id="0acbf-165">In your Azure ML experiment, web service input and output ports and global parameters have default names ("input1", "input2") that you can customize.</span></span> <span data-ttu-id="0acbf-166">имя, используемое для webServiceInputs, webServiceOutputs и globalParameters параметры как Hello должен точно соответствовать имена hello в экспериментах hello.</span><span class="sxs-lookup"><span data-stu-id="0acbf-166">hello names you use for webServiceInputs, webServiceOutputs, and globalParameters settings must exactly match hello names in hello experiments.</span></span> <span data-ttu-id="0acbf-167">Полезные данные запроса образец hello можно просмотреть на странице справки выполнения пакета hello для hello ожидается сопоставлении tooverify конечная точка машинного Обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="0acbf-167">You can view hello sample request payload on hello Batch Execution Help page for your Azure ML endpoint tooverify hello expected mapping.</span></span>
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
> <span data-ttu-id="0acbf-168">Только входные и выходные данные действия AzureMLBatchExecution hello могут передаваться как параметры toohello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="0acbf-168">Only inputs and outputs of hello AzureMLBatchExecution activity can be passed as parameters toohello Web service.</span></span> <span data-ttu-id="0acbf-169">Например в hello выше фрагменте кода JSON DecisionTreeInputBlob является входной toohello AzureMLBatchExecution действия, которое передается в качестве входного toohello веб-службы через параметр webServiceInput.</span><span class="sxs-lookup"><span data-stu-id="0acbf-169">For example, in hello above JSON snippet, DecisionTreeInputBlob is an input toohello AzureMLBatchExecution activity, which is passed as an input toohello Web service via webServiceInput parameter.</span></span>   
>
>

### <a name="example"></a><span data-ttu-id="0acbf-170">Пример</span><span class="sxs-lookup"><span data-stu-id="0acbf-170">Example</span></span>
<span data-ttu-id="0acbf-171">Этот пример использует хранилище Azure toohold оба hello входных и выходных данных.</span><span class="sxs-lookup"><span data-stu-id="0acbf-171">This example uses Azure Storage toohold both hello input and output data.</span></span>

<span data-ttu-id="0acbf-172">Рекомендуется пройти hello [построение первой конвейер с фабрикой данных] [ adf-build-1st-pipeline] учебника перед переходом в этом примере.</span><span class="sxs-lookup"><span data-stu-id="0acbf-172">We recommend that you go through hello [Build your first pipeline with Data Factory][adf-build-1st-pipeline] tutorial before going through this example.</span></span> <span data-ttu-id="0acbf-173">В этом примере, используйте артефактов фабрики данных Редактор фабрики данных toocreate hello (связанные службы, наборы данных, конвейера).</span><span class="sxs-lookup"><span data-stu-id="0acbf-173">Use hello Data Factory Editor toocreate Data Factory artifacts (linked services, datasets, pipeline) in this example.</span></span>   

1. <span data-ttu-id="0acbf-174">Создайте **связанную службу** для **службы хранилища Azure**.</span><span class="sxs-lookup"><span data-stu-id="0acbf-174">Create a **linked service** for your **Azure Storage**.</span></span> <span data-ttu-id="0acbf-175">Если hello входные и выходные файлы находятся в разных учетных записей хранения, то необходимо два связанных служб.</span><span class="sxs-lookup"><span data-stu-id="0acbf-175">If hello input and output files are in different storage accounts, you need two linked services.</span></span> <span data-ttu-id="0acbf-176">Ниже приведен пример JSON:</span><span class="sxs-lookup"><span data-stu-id="0acbf-176">Here is a JSON example:</span></span>

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
2. <span data-ttu-id="0acbf-177">Создать hello **ввода** фабрики данных Azure **набора данных**.</span><span class="sxs-lookup"><span data-stu-id="0acbf-177">Create hello **input** Azure Data Factory **dataset**.</span></span> <span data-ttu-id="0acbf-178">В отличие от некоторых других наборов данных фабрики данных, эти наборы должны содержать значения **folderPath** и **fileName**.</span><span class="sxs-lookup"><span data-stu-id="0acbf-178">Unlike some other Data Factory datasets, these datasets must contain both **folderPath** and **fileName** values.</span></span> <span data-ttu-id="0acbf-179">Можно использовать секционирования toocause каждого tooprocess пакетного выполнения (каждый фрагмент данных) или создать уникальный входных данных и выходные файлы.</span><span class="sxs-lookup"><span data-stu-id="0acbf-179">You can use partitioning toocause each batch execution (each data slice) tooprocess or produce unique input and output files.</span></span> <span data-ttu-id="0acbf-180">Может потребоваться tooinclude некоторые hello tootransform восходящего действия введены в hello CSV-файл и поместить его в hello учетной записи хранилища для каждого среза.</span><span class="sxs-lookup"><span data-stu-id="0acbf-180">You may need tooinclude some upstream activity tootransform hello input into hello CSV file format and place it in hello storage account for each slice.</span></span> <span data-ttu-id="0acbf-181">В этом случае не будет включена hello **внешних** и **externalData** параметры, отображаемые в hello следующий пример и вашей DecisionTreeInputBlob бы hello выходной набор данных из другого действия.</span><span class="sxs-lookup"><span data-stu-id="0acbf-181">In that case, you would not include hello **external** and **externalData** settings shown in hello following example, and your DecisionTreeInputBlob would be hello output dataset of a different Activity.</span></span>

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

    <span data-ttu-id="0acbf-182">Входные CSV-файл должен иметь hello строку заголовков столбцов.</span><span class="sxs-lookup"><span data-stu-id="0acbf-182">Your input csv file must have hello column header row.</span></span> <span data-ttu-id="0acbf-183">Если вы используете hello **действие копирования** toocreate или перемещения hello csv в хранилище больших двоичных объектов hello, необходимо задать значение свойства приемника hello **blobWriterAddHeader** слишком**true**.</span><span class="sxs-lookup"><span data-stu-id="0acbf-183">If you are using hello **Copy Activity** toocreate/move hello csv into hello blob storage, you should set hello sink property **blobWriterAddHeader** too**true**.</span></span> <span data-ttu-id="0acbf-184">Например:</span><span class="sxs-lookup"><span data-stu-id="0acbf-184">For example:</span></span>

    ```JSON
    sink:
    {
        "type": "BlobSink",     
        "blobWriterAddHeader": true
    }
    ```

    <span data-ttu-id="0acbf-185">Если hello CSV-файле отсутствует строка заголовка hello, может появиться следующая ошибка hello: **ошибки в действии: ошибка при чтении строки. Непредвиденный токен: StartObject. Путь '', строка 1, позиция 1**.</span><span class="sxs-lookup"><span data-stu-id="0acbf-185">If hello csv file does not have hello header row, you may see hello following error: **Error in Activity: Error reading string. Unexpected token: StartObject. Path '', line 1, position 1**.</span></span>
3. <span data-ttu-id="0acbf-186">Создать hello **вывода** фабрики данных Azure **набора данных**.</span><span class="sxs-lookup"><span data-stu-id="0acbf-186">Create hello **output** Azure Data Factory **dataset**.</span></span> <span data-ttu-id="0acbf-187">В этом примере секционирования toocreate уникальный выходной путь для каждого выполнения среза.</span><span class="sxs-lookup"><span data-stu-id="0acbf-187">This example uses partitioning toocreate a unique output path for each slice execution.</span></span> <span data-ttu-id="0acbf-188">Без секционирования hello, действие hello перезапишет файл hello.</span><span class="sxs-lookup"><span data-stu-id="0acbf-188">Without hello partitioning, hello activity would overwrite hello file.</span></span>

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
4. <span data-ttu-id="0acbf-189">Создание **связанная служба** типа: **AzureMLLinkedService**, предоставив ключ hello API и модели URL-адрес выполнения пакета.</span><span class="sxs-lookup"><span data-stu-id="0acbf-189">Create a **linked service** of type: **AzureMLLinkedService**, providing hello API key and model batch execution URL.</span></span>

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
5. <span data-ttu-id="0acbf-190">Наконец, создайте конвейер, содержащий действие **AzureMLBatchExecution** .</span><span class="sxs-lookup"><span data-stu-id="0acbf-190">Finally, author a pipeline containing an **AzureMLBatchExecution** Activity.</span></span> <span data-ttu-id="0acbf-191">Во время выполнения конвейера выполняет следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="0acbf-191">At runtime, pipeline performs hello following steps:</span></span>

   1. <span data-ttu-id="0acbf-192">Получает расположение hello hello входного файла из входных наборов данных.</span><span class="sxs-lookup"><span data-stu-id="0acbf-192">Gets hello location of hello input file from your input datasets.</span></span>
   2. <span data-ttu-id="0acbf-193">Вызывает выполнение пакета машинного обучения Azure hello API</span><span class="sxs-lookup"><span data-stu-id="0acbf-193">Invokes hello Azure Machine Learning batch execution API</span></span>
   3. <span data-ttu-id="0acbf-194">Копирует hello пакетного выполнения вывода toohello больших двоичных объектов в выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="0acbf-194">Copies hello batch execution output toohello blob given in your output dataset.</span></span>

      > [!NOTE]
      > <span data-ttu-id="0acbf-195">У действия AzureMLBatchExecution может быть ноль или более входных наборов данных и один или несколько выходных наборов данных.</span><span class="sxs-lookup"><span data-stu-id="0acbf-195">AzureMLBatchExecution activity can have zero or more inputs and one or more outputs.</span></span>
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

      <span data-ttu-id="0acbf-196">Даты **начала** и **окончания** должны быть в [формате ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="0acbf-196">Both **start** and **end** datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="0acbf-197">Например, 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="0acbf-197">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="0acbf-198">Hello **окончания** времени является необязательным.</span><span class="sxs-lookup"><span data-stu-id="0acbf-198">hello **end** time is optional.</span></span> <span data-ttu-id="0acbf-199">Если не указать значение для hello **окончания** свойство, оно вычисляется как «**start + 48 часов.**»</span><span class="sxs-lookup"><span data-stu-id="0acbf-199">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours.**"</span></span> <span data-ttu-id="0acbf-200">конвейер hello toorun неопределенно долгое время, укажите **9999-09-09** как значение hello для hello **окончания** свойство.</span><span class="sxs-lookup"><span data-stu-id="0acbf-200">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span> <span data-ttu-id="0acbf-201">Дополнительные сведения о свойствах JSON см. в [справочнике по скриптам JSON](https://msdn.microsoft.com/library/dn835050.aspx).</span><span class="sxs-lookup"><span data-stu-id="0acbf-201">See [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) for details about JSON properties.</span></span>

      > [!NOTE]
      > <span data-ttu-id="0acbf-202">Входные данные для действия AzureMLBatchExecution hello указывать не обязательно.</span><span class="sxs-lookup"><span data-stu-id="0acbf-202">Specifying input for hello AzureMLBatchExecution activity is optional.</span></span>
      >
      >

### <a name="scenario-experiments-using-readerwriter-modules-toorefer-toodata-in-various-storages"></a><span data-ttu-id="0acbf-203">Сценарий: Экспериментов с помощью toodata toorefer модулей чтения и записи в различных хранилищах</span><span class="sxs-lookup"><span data-stu-id="0acbf-203">Scenario: Experiments using Reader/Writer Modules toorefer toodata in various storages</span></span>
<span data-ttu-id="0acbf-204">При создании экспериментах Azure ML другим распространенным сценарием является toouse модулей чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="0acbf-204">Another common scenario when creating Azure ML experiments is toouse Reader and Writer modules.</span></span> <span data-ttu-id="0acbf-205">модуль считывания Hello используется tooload данных в эксперимент она hello модуль записи данных toosave из эксперимента.</span><span class="sxs-lookup"><span data-stu-id="0acbf-205">hello reader module is used tooload data into an experiment and hello writer module is toosave data from your experiments.</span></span> <span data-ttu-id="0acbf-206">Дополнительные сведения о модулях [чтения](https://msdn.microsoft.com/library/azure/dn905997.aspx) и [записи](https://msdn.microsoft.com/library/azure/dn905984.aspx) см. в соответствующих разделах в библиотеке MSDN.</span><span class="sxs-lookup"><span data-stu-id="0acbf-206">For details about reader and writer modules, see [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span></span>     

<span data-ttu-id="0acbf-207">При использовании hello модулей чтения и записи, это хороший способ toouse параметр веб-службы для каждого свойства из этих модулей чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="0acbf-207">When using hello reader and writer modules, it is good practice toouse a Web service parameter for each property of these reader/writer modules.</span></span> <span data-ttu-id="0acbf-208">Эти параметры web включить tooconfigure hello значения во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="0acbf-208">These web parameters enable you tooconfigure hello values during runtime.</span></span> <span data-ttu-id="0acbf-209">Например, можно создать эксперимент с модулем чтения, который использует базу данных SQL Azure: XXX.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="0acbf-209">For example, you could create an experiment with a reader module that uses an Azure SQL Database: XXX.database.windows.net.</span></span> <span data-ttu-id="0acbf-210">После развертывания веб-службу hello потребители hello tooenable hello web service toospecify требуется другой сервер SQL Azure, называется YYY.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="0acbf-210">After hello web service has been deployed, you want tooenable hello consumers of hello web service toospecify another Azure SQL Server called YYY.database.windows.net.</span></span> <span data-ttu-id="0acbf-211">Tooallow параметр Web service можно использовать этот toobe значение настройки.</span><span class="sxs-lookup"><span data-stu-id="0acbf-211">You can use a Web service parameter tooallow this value toobe configured.</span></span>

> [!NOTE]
> <span data-ttu-id="0acbf-212">Входные и выходные данные веб-службы отличаются от параметров веб-службы.</span><span class="sxs-lookup"><span data-stu-id="0acbf-212">Web service input and output are different from Web service parameters.</span></span> <span data-ttu-id="0acbf-213">В первом сценарии hello вы уже узнали, как входа и выхода можно указать для службы Azure ML Web.</span><span class="sxs-lookup"><span data-stu-id="0acbf-213">In hello first scenario, you have seen how an input and output can be specified for an Azure ML Web service.</span></span> <span data-ttu-id="0acbf-214">В этом сценарии передать параметры для веб-службы, которые соответствуют tooproperties модулей чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="0acbf-214">In this scenario, you pass parameters for a Web service that correspond tooproperties of reader/writer modules.</span></span>
>
>

<span data-ttu-id="0acbf-215">Рассмотрим сценарий использования параметров веб-службы.</span><span class="sxs-lookup"><span data-stu-id="0acbf-215">Let's look at a scenario for using Web service parameters.</span></span> <span data-ttu-id="0acbf-216">У вас есть развернутой веб-службы машинного обучения Azure, использующего модуль tooread модуль чтения данных из одного из источников данных hello поддерживается машинным обучением Azure (например: база данных SQL Azure).</span><span class="sxs-lookup"><span data-stu-id="0acbf-216">You have a deployed Azure Machine Learning web service that uses a reader module tooread data from one of hello data sources supported by Azure Machine Learning (for example: Azure SQL Database).</span></span> <span data-ttu-id="0acbf-217">После выполнения пакетного hello hello записаны результаты с помощью модуля записи (база данных SQL Azure).</span><span class="sxs-lookup"><span data-stu-id="0acbf-217">After hello batch execution is performed, hello results are written using a Writer module (Azure SQL Database).</span></span>  <span data-ttu-id="0acbf-218">Нет web service входных и выходных данных определяются в экспериментах hello.</span><span class="sxs-lookup"><span data-stu-id="0acbf-218">No web service inputs and outputs are defined in hello experiments.</span></span> <span data-ttu-id="0acbf-219">В этом случае рекомендуется настраивать параметры соответствующих веб-службы для hello модулей чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="0acbf-219">In this case, we recommend that you configure relevant web service parameters for hello reader and writer modules.</span></span> <span data-ttu-id="0acbf-220">Эта конфигурация обеспечивает hello чтения и записи toobe модули настроены при помощи hello AzureMLBatchExecution действия.</span><span class="sxs-lookup"><span data-stu-id="0acbf-220">This configuration allows hello reader/writer modules toobe configured when using hello AzureMLBatchExecution activity.</span></span> <span data-ttu-id="0acbf-221">Укажите параметры веб-службы в hello **globalParameters** раздела действие hello JSON.</span><span class="sxs-lookup"><span data-stu-id="0acbf-221">You specify Web service parameters in hello **globalParameters** section in hello activity JSON as follows.</span></span>

```JSON
"typeProperties": {
    "globalParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```

<span data-ttu-id="0acbf-222">Можно также использовать [функции фабрики данных](data-factory-functions-variables.md) при передаче значения для hello параметры веб-службы, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="0acbf-222">You can also use [Data Factory Functions](data-factory-functions-variables.md) in passing values for hello Web service parameters as shown in hello following example:</span></span>

```JSON
"typeProperties": {
    "globalParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> <span data-ttu-id="0acbf-223">Параметры веб-службы Hello чувствительны к регистру, поэтому убедитесь hello имена, указываемые в действии hello JSON соответствует hello из них, предоставляемые hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="0acbf-223">hello Web service parameters are case-sensitive, so ensure that hello names you specify in hello activity JSON match hello ones exposed by hello Web service.</span></span>
>
>

### <a name="using-a-reader-module-tooread-data-from-multiple-files-in-azure-blob"></a><span data-ttu-id="0acbf-224">С помощью модуля tooread модуль чтения данных из нескольких файлов в BLOB-объектов Azure</span><span class="sxs-lookup"><span data-stu-id="0acbf-224">Using a Reader module tooread data from multiple files in Azure Blob</span></span>
<span data-ttu-id="0acbf-225">Конвейеры больших данных с такими действиями, как Pig и Hive, могут формировать один или несколько выходных файлов без расширений.</span><span class="sxs-lookup"><span data-stu-id="0acbf-225">Big data pipelines with activities such as Pig and Hive can produce one or more output files with no extensions.</span></span> <span data-ttu-id="0acbf-226">Например при указании внешнюю таблицу Hive hello данных для внешней таблицы Hive hello могут храниться в хранилище больших двоичных объектов с hello, следуя 000000_0 имя.</span><span class="sxs-lookup"><span data-stu-id="0acbf-226">For example, when you specify an external Hive table, hello data for hello external Hive table can be stored in Azure blob storage with hello following name 000000_0.</span></span> <span data-ttu-id="0acbf-227">Можно использовать модуль чтения hello в эксперименте tooread несколько файлов и использовать их для прогнозов.</span><span class="sxs-lookup"><span data-stu-id="0acbf-227">You can use hello reader module in an experiment tooread multiple files, and use them for predictions.</span></span>

<span data-ttu-id="0acbf-228">При использовании модуля чтения hello в эксперимент машинного обучения Azure, можно указать в качестве ввода больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="0acbf-228">When using hello reader module in an Azure Machine Learning experiment, you can specify Azure Blob as an input.</span></span> <span data-ttu-id="0acbf-229">файлы Hello в hello хранилище больших двоичных объектов может быть hello выходные файлы (пример: 000000_0), созданные с помощью сценарий Pig и Hive в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0acbf-229">hello files in hello Azure blob storage can be hello output files (Example: 000000_0) that are produced by a Pig and Hive script running on HDInsight.</span></span> <span data-ttu-id="0acbf-230">Hello модуля чтения позволяет tooread файлы (с без расширения), настроив hello **toocontainer путь, каталог или большого двоичного объекта**.</span><span class="sxs-lookup"><span data-stu-id="0acbf-230">hello reader module allows you tooread files (with no extensions) by configuring hello **Path toocontainer, directory/blob**.</span></span> <span data-ttu-id="0acbf-231">Hello **toocontainer путь** точки toohello контейнера и **каталога или большого двоичного объекта** указывает toofolder файлами hello, как показано в hello после изображения.</span><span class="sxs-lookup"><span data-stu-id="0acbf-231">hello **Path toocontainer** points toohello container and **directory/blob** points toofolder that contains hello files as shown in hello following image.</span></span> <span data-ttu-id="0acbf-232">Hello именно звездочка \*) **указывает, что все hello файлы в папку контейнера hello (то есть данных/aggregateddata/год = 2014-месяц-6 /\*)** считываются как часть эксперимента hello.</span><span class="sxs-lookup"><span data-stu-id="0acbf-232">hello asterisk that is, \*) **specifies that all hello files in hello container/folder (that is, data/aggregateddata/year=2014/month-6/\*)** are read as part of hello experiment.</span></span>

![Свойства большого двоичного объекта Azure](./media/data-factory-create-predictive-pipelines/azure-blob-properties.png)

### <a name="example"></a><span data-ttu-id="0acbf-234">Пример</span><span class="sxs-lookup"><span data-stu-id="0acbf-234">Example</span></span>
#### <a name="pipeline-with-azuremlbatchexecution-activity-with-web-service-parameters"></a><span data-ttu-id="0acbf-235">Конвейер с действием AzureMLBatchExecution с параметрами веб-службы</span><span class="sxs-lookup"><span data-stu-id="0acbf-235">Pipeline with AzureMLBatchExecution activity with Web Service Parameters</span></span>

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

<span data-ttu-id="0acbf-236">В hello в приведенном выше примере JSON:</span><span class="sxs-lookup"><span data-stu-id="0acbf-236">In hello above JSON example:</span></span>

* <span data-ttu-id="0acbf-237">Hello развернуты служба использует средство чтения и записи модуля tooread и записи данных из компьютер обучения Azure веб-tooan базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="0acbf-237">hello deployed Azure Machine Learning Web service uses a reader and a writer module tooread/write data from/tooan Azure SQL Database.</span></span> <span data-ttu-id="0acbf-238">Этот веб-служба предоставляет hello следующие четыре параметра: имя сервера, имя базы данных, имя учетной записи пользователя сервера и пароль учетной записи пользователя сервера базы данных.</span><span class="sxs-lookup"><span data-stu-id="0acbf-238">This Web service exposes hello following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span></span>  
* <span data-ttu-id="0acbf-239">Даты **начала** и **окончания** должны быть в [формате ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="0acbf-239">Both **start** and **end** datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="0acbf-240">Например, 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="0acbf-240">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="0acbf-241">Hello **окончания** времени является необязательным.</span><span class="sxs-lookup"><span data-stu-id="0acbf-241">hello **end** time is optional.</span></span> <span data-ttu-id="0acbf-242">Если не указать значение для hello **окончания** свойство, оно вычисляется как «**start + 48 часов.**»</span><span class="sxs-lookup"><span data-stu-id="0acbf-242">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours.**"</span></span> <span data-ttu-id="0acbf-243">конвейер hello toorun неопределенно долгое время, укажите **9999-09-09** как значение hello для hello **окончания** свойство.</span><span class="sxs-lookup"><span data-stu-id="0acbf-243">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span> <span data-ttu-id="0acbf-244">Дополнительные сведения о свойствах JSON см. в [справочнике по скриптам JSON](https://msdn.microsoft.com/library/dn835050.aspx).</span><span class="sxs-lookup"><span data-stu-id="0acbf-244">See [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) for details about JSON properties.</span></span>

### <a name="other-scenarios"></a><span data-ttu-id="0acbf-245">Другие сценарии</span><span class="sxs-lookup"><span data-stu-id="0acbf-245">Other scenarios</span></span>
#### <a name="web-service-requires-multiple-inputs"></a><span data-ttu-id="0acbf-246">Веб-службе требуется несколько входных данных</span><span class="sxs-lookup"><span data-stu-id="0acbf-246">Web service requires multiple inputs</span></span>
<span data-ttu-id="0acbf-247">Если веб-служба hello принимает несколько входов, использовать hello **webServiceInputs** свойство вместо **webServiceInput**.</span><span class="sxs-lookup"><span data-stu-id="0acbf-247">If hello web service takes multiple inputs, use hello **webServiceInputs** property instead of using **webServiceInput**.</span></span> <span data-ttu-id="0acbf-248">Наборы данных, на которые ссылается hello **webServiceInputs** также должны быть включены в действие hello **входов**.</span><span class="sxs-lookup"><span data-stu-id="0acbf-248">Datasets that are referenced by hello **webServiceInputs** must also be included in hello Activity **inputs**.</span></span>

<span data-ttu-id="0acbf-249">В эксперименте Машинного обучения Azure у входных и выходных портов и глобальных параметров есть имена по умолчанию (input1, input2), которые можно настроить.</span><span class="sxs-lookup"><span data-stu-id="0acbf-249">In your Azure ML experiment, web service input and output ports and global parameters have default names ("input1", "input2") that you can customize.</span></span> <span data-ttu-id="0acbf-250">имя, используемое для webServiceInputs, webServiceOutputs и globalParameters параметры как Hello должен точно соответствовать имена hello в экспериментах hello.</span><span class="sxs-lookup"><span data-stu-id="0acbf-250">hello names you use for webServiceInputs, webServiceOutputs, and globalParameters settings must exactly match hello names in hello experiments.</span></span> <span data-ttu-id="0acbf-251">Полезные данные запроса образец hello можно просмотреть на странице справки выполнения пакета hello для hello ожидается сопоставлении tooverify конечная точка машинного Обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="0acbf-251">You can view hello sample request payload on hello Batch Execution Help page for your Azure ML endpoint tooverify hello expected mapping.</span></span>

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

#### <a name="web-service-does-not-require-an-input"></a><span data-ttu-id="0acbf-252">Веб-служба не требует входных данных</span><span class="sxs-lookup"><span data-stu-id="0acbf-252">Web Service does not require an input</span></span>
<span data-ttu-id="0acbf-253">Azure ML пакетного выполнения веб-службы может быть используется toorun все рабочие процессы, например R или сценариев Python, который не может потребоваться входные данные.</span><span class="sxs-lookup"><span data-stu-id="0acbf-253">Azure ML batch execution web services can be used toorun any workflows, for example R or Python scripts, that may not require any inputs.</span></span> <span data-ttu-id="0acbf-254">Или эксперимента hello могут быть настроены с помощью модуля чтения, не предоставляет все GlobalParameters.</span><span class="sxs-lookup"><span data-stu-id="0acbf-254">Or, hello experiment might be configured with a Reader module that does not expose any GlobalParameters.</span></span> <span data-ttu-id="0acbf-255">В этом случае hello AzureMLBatchExecution действие будет настроена следующим образом:</span><span class="sxs-lookup"><span data-stu-id="0acbf-255">In that case, hello AzureMLBatchExecution Activity would be configured as follows:</span></span>

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

#### <a name="web-service-does-not-require-an-inputoutput"></a><span data-ttu-id="0acbf-256">Веб-служба не требует входных или выходных данных</span><span class="sxs-lookup"><span data-stu-id="0acbf-256">Web Service does not require an input/output</span></span>
<span data-ttu-id="0acbf-257">Hello Azure ML пакетного выполнения веб-службы могут не иметь никаких выходных данных веб-службы настроены.</span><span class="sxs-lookup"><span data-stu-id="0acbf-257">hello Azure ML batch execution web service might not have any Web Service output configured.</span></span> <span data-ttu-id="0acbf-258">В данном примере не настроены ни входные или выходные параметры, ни глобальные параметры.</span><span class="sxs-lookup"><span data-stu-id="0acbf-258">In this example, there is no Web Service input or output, nor are any GlobalParameters configured.</span></span> <span data-ttu-id="0acbf-259">По-прежнему выхода, настроенного на само действие hello, но он не указан в качестве webServiceOutput.</span><span class="sxs-lookup"><span data-stu-id="0acbf-259">There is still an output configured on hello activity itself, but it is not given as a webServiceOutput.</span></span>

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

#### <a name="web-service-uses-readers-and-writers-and-hello-activity-runs-only-when-other-activities-have-succeeded"></a><span data-ttu-id="0acbf-260">Веб-служба использует чтения и записи и hello действие выполняется только в том случае, если другие действия успешно выполнены</span><span class="sxs-lookup"><span data-stu-id="0acbf-260">Web Service uses readers and writers, and hello activity runs only when other activities have succeeded</span></span>
<span data-ttu-id="0acbf-261">Hello Azure ML веб-службы чтения и записи модули, может быть настроенный toorun независимо от любой GlobalParameters.</span><span class="sxs-lookup"><span data-stu-id="0acbf-261">hello Azure ML web service reader and writer modules might be configured toorun with or without any GlobalParameters.</span></span> <span data-ttu-id="0acbf-262">Тем не менее вы можете tooembed службы вызовов в конвейера, который использует службу hello tooinvoke зависимости набора данных только в том случае, когда некоторые вышестоящего Обработка завершена.</span><span class="sxs-lookup"><span data-stu-id="0acbf-262">However, you may want tooembed service calls in a pipeline that uses dataset dependencies tooinvoke hello service only when some upstream processing has completed.</span></span> <span data-ttu-id="0acbf-263">Вы можете запускать другие действия после завершения выполнения пакета hello этот подход.</span><span class="sxs-lookup"><span data-stu-id="0acbf-263">You can also trigger some other action after hello batch execution has completed using this approach.</span></span> <span data-ttu-id="0acbf-264">В этом случае можно выразить с помощью действия входов и выходов, без задания имени, такого как веб-службе входные и выходные данные зависимостей hello.</span><span class="sxs-lookup"><span data-stu-id="0acbf-264">In that case, you can express hello dependencies using activity inputs and outputs, without naming any of them as Web Service inputs or outputs.</span></span>

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

<span data-ttu-id="0acbf-265">Hello **общие выводы** являются:</span><span class="sxs-lookup"><span data-stu-id="0acbf-265">hello **takeaways** are:</span></span>

* <span data-ttu-id="0acbf-266">Если ваш конечная эксперимента использует webServiceInput: он представлен набор данных BLOB-объектов и входит в состав входные данные действия hello и свойство webServiceInput hello.</span><span class="sxs-lookup"><span data-stu-id="0acbf-266">If your experiment endpoint uses a webServiceInput: it is represented by a blob dataset and is included in hello activity inputs and hello webServiceInput property.</span></span> <span data-ttu-id="0acbf-267">В противном случае свойство webServiceInput hello опускается.</span><span class="sxs-lookup"><span data-stu-id="0acbf-267">Otherwise, hello webServiceInput property is omitted.</span></span>
* <span data-ttu-id="0acbf-268">Если ваш конечная эксперимента использует webServiceOutput(s): они представляются в наборах данных больших двоичных объектов и включены в выходных данных действия hello и в свойстве webServiceOutputs hello.</span><span class="sxs-lookup"><span data-stu-id="0acbf-268">If your experiment endpoint uses webServiceOutput(s): they are represented by blob datasets and are included in hello activity outputs and in hello webServiceOutputs property.</span></span> <span data-ttu-id="0acbf-269">Выводит действие Hello и webServiceOutputs, сопоставляются по имени hello каждого выхода в эксперименте hello.</span><span class="sxs-lookup"><span data-stu-id="0acbf-269">hello activity outputs and webServiceOutputs are mapped by hello name of each output in hello experiment.</span></span> <span data-ttu-id="0acbf-270">В противном случае свойство webServiceOutputs hello опускается.</span><span class="sxs-lookup"><span data-stu-id="0acbf-270">Otherwise, hello webServiceOutputs property is omitted.</span></span>
* <span data-ttu-id="0acbf-271">Если конечная точка эксперимента предоставляет globalParameter(s), они задаются в свойстве globalParameters действие hello в виде пар ключ/значение.</span><span class="sxs-lookup"><span data-stu-id="0acbf-271">If your experiment endpoint exposes globalParameter(s), they are given in hello activity globalParameters property as key, value pairs.</span></span> <span data-ttu-id="0acbf-272">В противном случае свойство globalParameters hello опускается.</span><span class="sxs-lookup"><span data-stu-id="0acbf-272">Otherwise, hello globalParameters property is omitted.</span></span> <span data-ttu-id="0acbf-273">ключи Hello чувствительны к регистру.</span><span class="sxs-lookup"><span data-stu-id="0acbf-273">hello keys are case-sensitive.</span></span> <span data-ttu-id="0acbf-274">[Функции фабрики данных Azure](data-factory-functions-variables.md) могут использоваться в значениях hello.</span><span class="sxs-lookup"><span data-stu-id="0acbf-274">[Azure Data Factory functions](data-factory-functions-variables.md) may be used in hello values.</span></span>
* <span data-ttu-id="0acbf-275">Дополнительные наборы данных могут быть включены в свойства входов и выходов действия hello, без, на которую ссылается действие typeProperties hello.</span><span class="sxs-lookup"><span data-stu-id="0acbf-275">Additional datasets may be included in hello Activity inputs and outputs properties, without being referenced in hello Activity typeProperties.</span></span> <span data-ttu-id="0acbf-276">Эти наборы данных определяют выполнение с помощью зависимости среза, но пропускаются hello AzureMLBatchExecution действия.</span><span class="sxs-lookup"><span data-stu-id="0acbf-276">These datasets govern execution using slice dependencies but are otherwise ignored by hello AzureMLBatchExecution Activity.</span></span>


## <a name="updating-models-using-update-resource-activity"></a><span data-ttu-id="0acbf-277">Обновление моделей с помощью действия обновления ресурса</span><span class="sxs-lookup"><span data-stu-id="0acbf-277">Updating models using Update Resource Activity</span></span>
<span data-ttu-id="0acbf-278">После завершения переподготовки, обновите hello оценки веб-службы (прогнозной эксперимент, предоставляемых как веб-службы) с hello вновь обученной модели с помощью hello **действия ресурса обновления машинного Обучения Azure**.</span><span class="sxs-lookup"><span data-stu-id="0acbf-278">After you are done with retraining, update hello scoring web service (predictive experiment exposed as a web service) with hello newly trained model by using hello **Azure ML Update Resource Activity**.</span></span> <span data-ttu-id="0acbf-279">Дополнительные сведения см. в статье [Updating Azure Machine Learning models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) (Обновление моделей машинного обучения Azure с помощью действия "Обновить ресурс").</span><span class="sxs-lookup"><span data-stu-id="0acbf-279">See [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) article for details.</span></span>

### <a name="reader-and-writer-modules"></a><span data-ttu-id="0acbf-280">Модули чтения и записи</span><span class="sxs-lookup"><span data-stu-id="0acbf-280">Reader and Writer Modules</span></span>
<span data-ttu-id="0acbf-281">Распространенный сценарий использования параметры веб-службы является использование hello Azure SQL чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="0acbf-281">A common scenario for using Web service parameters is hello use of Azure SQL Readers and Writers.</span></span> <span data-ttu-id="0acbf-282">модуль считывания Hello — используется tooload данных в эксперимент из служб управления данными вне студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="0acbf-282">hello reader module is used tooload data into an experiment from data management services outside Azure Machine Learning Studio.</span></span> <span data-ttu-id="0acbf-283">модуль записи Hello — toosave данные из экспериментов в службах управления данными вне студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="0acbf-283">hello writer module is toosave data from your experiments into data management services outside Azure Machine Learning Studio.</span></span>  

<span data-ttu-id="0acbf-284">Сведения о модулях [чтения](https://msdn.microsoft.com/library/azure/dn905997.aspx) и [записи](https://msdn.microsoft.com/library/azure/dn905984.aspx) больших двоичных объектов Azure и SQL Azure см. в соответствующих разделах в библиотеке MSDN.</span><span class="sxs-lookup"><span data-stu-id="0acbf-284">For details about Azure Blob/Azure SQL reader/writer, see [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span></span> <span data-ttu-id="0acbf-285">пример Hello в предыдущем разделе hello использовать hello больших двоичных объектов Azure чтения и записи больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="0acbf-285">hello example in hello previous section used hello Azure Blob reader and Azure Blob writer.</span></span> <span data-ttu-id="0acbf-286">В этом разделе рассматривается использование модуля чтения и модуля записи SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="0acbf-286">This section discusses using Azure SQL reader and Azure SQL writer.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="0acbf-287">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="0acbf-287">Frequently asked questions</span></span>
<span data-ttu-id="0acbf-288">**Вопрос.** Имеется несколько файлов, сформированных моими конвейерами больших данных.</span><span class="sxs-lookup"><span data-stu-id="0acbf-288">**Q:** I have multiple files that are generated by my big data pipelines.</span></span> <span data-ttu-id="0acbf-289">Можно использовать toowork hello AzureMLBatchExecution действия для всех файлов hello</span><span class="sxs-lookup"><span data-stu-id="0acbf-289">Can I use hello AzureMLBatchExecution Activity toowork on all hello files?</span></span>

<span data-ttu-id="0acbf-290">**Ответ.** Да.</span><span class="sxs-lookup"><span data-stu-id="0acbf-290">**A:** Yes.</span></span> <span data-ttu-id="0acbf-291">В разделе hello **с помощью модуля tooread модуль чтения данных из нескольких файлов в большом двоичном объекте Azure** подробные сведения см.</span><span class="sxs-lookup"><span data-stu-id="0acbf-291">See hello **Using a Reader module tooread data from multiple files in Azure Blob** section for details.</span></span>

## <a name="azure-ml-batch-scoring-activity"></a><span data-ttu-id="0acbf-292">Действие количественной оценки Azure ML</span><span class="sxs-lookup"><span data-stu-id="0acbf-292">Azure ML Batch Scoring Activity</span></span>
<span data-ttu-id="0acbf-293">Если вы используете hello **AzureMLBatchScoring** toointegrate действия с машинного обучения Azure, рекомендуется использовать последнюю hello **AzureMLBatchExecution** действия.</span><span class="sxs-lookup"><span data-stu-id="0acbf-293">If you are using hello **AzureMLBatchScoring** activity toointegrate with Azure Machine Learning, we recommend that you use hello latest **AzureMLBatchExecution** activity.</span></span>

<span data-ttu-id="0acbf-294">Hello действия AzureMLBatchExecution впервые появился в hello августа 2015 г. выпуск пакета SDK для Azure и Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0acbf-294">hello AzureMLBatchExecution activity is introduced in hello August 2015 release of Azure SDK and Azure PowerShell.</span></span>

<span data-ttu-id="0acbf-295">Если требуется использование действия AzureMLBatchScoring hello toocontinue продолжайте чтение в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="0acbf-295">If you want toocontinue using hello AzureMLBatchScoring activity, continue reading through this section.</span></span>  

### <a name="azure-ml-batch-scoring-activity-using-azure-storage-for-inputoutput"></a><span data-ttu-id="0acbf-296">Действие количественной оценки Azure ML с использованием хранилища Azure в качестве входных и (или) выходных данных</span><span class="sxs-lookup"><span data-stu-id="0acbf-296">Azure ML Batch Scoring activity using Azure Storage for input/output</span></span>

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

### <a name="web-service-parameters"></a><span data-ttu-id="0acbf-297">Параметры веб-службы</span><span class="sxs-lookup"><span data-stu-id="0acbf-297">Web Service Parameters</span></span>
<span data-ttu-id="0acbf-298">Добавьте значения toospecify параметры веб-службы **typeProperties** toohello раздел **AzureMLBatchScoringActivty** раздела hello конвейера JSON, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="0acbf-298">toospecify values for Web service parameters, add a **typeProperties** section toohello **AzureMLBatchScoringActivty** section in hello pipeline JSON as shown in hello following example:</span></span>

```JSON
"typeProperties": {
    "webServiceParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```
<span data-ttu-id="0acbf-299">Можно также использовать [функции фабрики данных](data-factory-functions-variables.md) при передаче значения для hello параметры веб-службы, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="0acbf-299">You can also use [Data Factory Functions](data-factory-functions-variables.md) in passing values for hello Web service parameters as shown in hello following example:</span></span>

```JSON
"typeProperties": {
    "webServiceParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> <span data-ttu-id="0acbf-300">Параметры веб-службы Hello чувствительны к регистру, поэтому убедитесь hello имена, указываемые в действии hello JSON соответствует hello из них, предоставляемые hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="0acbf-300">hello Web service parameters are case-sensitive, so ensure that hello names you specify in hello activity JSON match hello ones exposed by hello Web service.</span></span>
>
>

## <a name="see-also"></a><span data-ttu-id="0acbf-301">См. также</span><span class="sxs-lookup"><span data-stu-id="0acbf-301">See Also</span></span>
* [<span data-ttu-id="0acbf-302">Запись блога Azure: «Приступая к работе с фабрикой данных Azure и Машинным обучением Azure»</span><span class="sxs-lookup"><span data-stu-id="0acbf-302">Azure blog post: Getting started with Azure Data Factory and Azure Machine Learning</span></span>](https://azure.microsoft.com/blog/getting-started-with-azure-data-factory-and-azure-machine-learning-4/)

[adf-build-1st-pipeline]: data-factory-build-your-first-pipeline.md

[azure-machine-learning]: http://azure.microsoft.com/services/machine-learning/
