---
title: "aaaUpdate моделей машинного обучения, с помощью фабрики данных Azure | Документы Microsoft"
description: "Описывает, как toocreate создание прогнозирующих конвейеров с помощью фабрики данных Azure и машинного обучения Azure"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 6e5e4d2cfd245c7a9ed3bb9cdacca1f7f82b9620
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="updating-azure-machine-learning-models-using-update-resource-activity"></a><span data-ttu-id="b728a-103">Обновление моделей машинного обучения Azure с помощью действия "Обновить ресурс"</span><span class="sxs-lookup"><span data-stu-id="b728a-103">Updating Azure Machine Learning models using Update Resource Activity</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="b728a-104">Действие Hive</span><span class="sxs-lookup"><span data-stu-id="b728a-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="b728a-105">Действие Pig</span><span class="sxs-lookup"><span data-stu-id="b728a-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="b728a-106">Действие MapReduce</span><span class="sxs-lookup"><span data-stu-id="b728a-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="b728a-107">Потоковая активность Hadoop</span><span class="sxs-lookup"><span data-stu-id="b728a-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="b728a-108">Действие Spark</span><span class="sxs-lookup"><span data-stu-id="b728a-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="b728a-109">Действие выполнения пакета машинного обучения</span><span class="sxs-lookup"><span data-stu-id="b728a-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="b728a-110">Действие "Обновить ресурс" в службе машинного обучения</span><span class="sxs-lookup"><span data-stu-id="b728a-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="b728a-111">Действие хранимой процедуры</span><span class="sxs-lookup"><span data-stu-id="b728a-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="b728a-112">Действие U-SQL в Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="b728a-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="b728a-113">Настраиваемое действие .NET</span><span class="sxs-lookup"><span data-stu-id="b728a-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="b728a-114">В этой статье дополняет hello основной фабрики данных Azure - статье интеграции машинного обучения Azure: [создание прогнозирующих конвейеров с помощью машинного обучения Azure и фабрики данных Azure](data-factory-azure-ml-batch-execution-activity.md).</span><span class="sxs-lookup"><span data-stu-id="b728a-114">This article complements hello main Azure Data Factory - Azure Machine Learning integration article: [Create predictive pipelines using Azure Machine Learning and Azure Data Factory](data-factory-azure-ml-batch-execution-activity.md).</span></span> <span data-ttu-id="b728a-115">Если это еще не сделано, изучите статью основные hello перед прочтя эту статью.</span><span class="sxs-lookup"><span data-stu-id="b728a-115">If you haven't already done so, review hello main article before reading through this article.</span></span> 

## <a name="overview"></a><span data-ttu-id="b728a-116">Обзор</span><span class="sxs-lookup"><span data-stu-id="b728a-116">Overview</span></span>
<span data-ttu-id="b728a-117">Со временем hello прогнозных моделей в экспериментах оценки машинного Обучения Azure hello должны toobe повторное обучение с помощью новых входных наборов данных.</span><span class="sxs-lookup"><span data-stu-id="b728a-117">Over time, hello predictive models in hello Azure ML scoring experiments need toobe retrained using new input datasets.</span></span> <span data-ttu-id="b728a-118">После завершения переподготовки, вы хотите tooupdate hello оценки веб-службы с hello повторное Обучение модели машинного Обучения.</span><span class="sxs-lookup"><span data-stu-id="b728a-118">After you are done with retraining, you want tooupdate hello scoring web service with hello retrained ML model.</span></span> <span data-ttu-id="b728a-119">Hello типичные действия tooenable переподготовки и обновление моделей машинного Обучения Azure через веб-службы являются:</span><span class="sxs-lookup"><span data-stu-id="b728a-119">hello typical steps tooenable retraining and updating Azure ML models via web services are:</span></span>

1. <span data-ttu-id="b728a-120">Создайте эксперимент в [Студии машинного обучения Azure](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="b728a-120">Create an experiment in [Azure ML Studio](https://studio.azureml.net).</span></span>
2. <span data-ttu-id="b728a-121">Если вас устраивают hello модели, используйте Azure ML Studio toopublish веб-службы для обоих hello **эксперимента обучения** и оценки /**прогнозной эксперимента**.</span><span class="sxs-lookup"><span data-stu-id="b728a-121">When you are satisfied with hello model, use Azure ML Studio toopublish web services for both hello **training experiment** and scoring/**predictive experiment**.</span></span>

<span data-ttu-id="b728a-122">Hello следующей таблице описаны hello веб-служб, используемых в этом примере.</span><span class="sxs-lookup"><span data-stu-id="b728a-122">hello following table describes hello web services used in this example.</span></span>  <span data-ttu-id="b728a-123">Подробные сведения см. в статье [Программное переобучение моделей машинного обучения](../machine-learning/machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="b728a-123">See [Retrain Machine Learning models programmatically](../machine-learning/machine-learning-retrain-models-programmatically.md) for details.</span></span>

- <span data-ttu-id="b728a-124">**Веб-служба обучения**: получает данные для обучения и создает обученные модели.</span><span class="sxs-lookup"><span data-stu-id="b728a-124">**Training web service** - Receives training data and produces trained models.</span></span> <span data-ttu-id="b728a-125">Hello переподготовки hello выходные данные — это файл .ilearner в службе хранилища больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="b728a-125">hello output of hello retraining is an .ilearner file in an Azure Blob storage.</span></span> <span data-ttu-id="b728a-126">Hello **по умолчанию конечная точка** создается автоматически для при публикации обучения hello поэкспериментировать веб-службы.</span><span class="sxs-lookup"><span data-stu-id="b728a-126">hello **default endpoint** is automatically created for you when you publish hello training experiment as a web service.</span></span> <span data-ttu-id="b728a-127">Можно создать дополнительные конечные точки, но hello примере используются только конечная точка по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="b728a-127">You can create more endpoints but hello example uses only hello default endpoint.</span></span>
- <span data-ttu-id="b728a-128">**Веб-служба оценки**: получает данные без метки и осуществляет прогнозирование.</span><span class="sxs-lookup"><span data-stu-id="b728a-128">**Scoring web service** - Receives unlabeled data examples and makes predictions.</span></span> <span data-ttu-id="b728a-129">Hello выходные данные прогноза, могут иметь различные формы, например, в CSV-файл или строк в базе данных Azure SQL, в зависимости от конфигурации hello hello эксперимента.</span><span class="sxs-lookup"><span data-stu-id="b728a-129">hello output of prediction could have various forms, such as a .csv file or rows in an Azure SQL database, depending on hello configuration of hello experiment.</span></span> <span data-ttu-id="b728a-130">Конечная точка по умолчанию Hello автоматически создается при публикации hello прогнозной эксперимент как веб-службы.</span><span class="sxs-lookup"><span data-stu-id="b728a-130">hello default endpoint is automatically created for you when you publish hello predictive experiment as a web service.</span></span> 

<span data-ttu-id="b728a-131">Hello на рисунке ниже показана связь hello обучения и оценки конечные точки в Azure ML.</span><span class="sxs-lookup"><span data-stu-id="b728a-131">hello following picture depicts hello relationship between training and scoring endpoints in Azure ML.</span></span>

![ВЕБ-СЛУЖБЫ](./media/data-factory-azure-ml-batch-execution-activity/web-services.png)

<span data-ttu-id="b728a-133">Можно вызвать hello **обучения веб-службы** с помощью hello **действие выполнения пакета машинного Обучения Azure**.</span><span class="sxs-lookup"><span data-stu-id="b728a-133">You can invoke hello **training web service** by using hello **Azure ML Batch Execution Activity**.</span></span> <span data-ttu-id="b728a-134">Это действие аналогично обращению к веб-службе машинного обучения Azure (веб-службе оценки) для получения данных оценки.</span><span class="sxs-lookup"><span data-stu-id="b728a-134">Invoking a training web service is same as invoking an Azure ML web service (scoring web service) for scoring data.</span></span> <span data-ttu-id="b728a-135">Здравствуйте выше титульных разделов, как к веб-службе машинного Обучения Azure с фабрикой данных Azure tooinvoke конвейера подробно.</span><span class="sxs-lookup"><span data-stu-id="b728a-135">hello preceding sections cover how tooinvoke an Azure ML web service from an Azure Data Factory pipeline in detail.</span></span> 

<span data-ttu-id="b728a-136">Можно вызвать hello **оценки веб-службы** с помощью hello **действия ресурса обновления машинного Обучения Azure** tooupdate hello веб-службы с hello вновь обученной модели.</span><span class="sxs-lookup"><span data-stu-id="b728a-136">You can invoke hello **scoring web service** by using hello **Azure ML Update Resource Activity** tooupdate hello web service with hello newly trained model.</span></span> <span data-ttu-id="b728a-137">Привет, следующие примеры содержат определения связанной службы:</span><span class="sxs-lookup"><span data-stu-id="b728a-137">hello following examples provide linked service definitions:</span></span> 

## <a name="scoring-web-service-is-a-classic-web-service"></a><span data-ttu-id="b728a-138">Веб-служба оценки — классическая веб-служба</span><span class="sxs-lookup"><span data-stu-id="b728a-138">Scoring web service is a classic web service</span></span>
<span data-ttu-id="b728a-139">Если hello оценки веб-службы **классического веб-службы**, создать второй hello **конечной точки не по умолчанию и обновляемые** с помощью hello [портал Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="b728a-139">If hello scoring web service is a **classic web service**, create hello second **non-default and updatable endpoint** by using hello [Azure portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="b728a-140">Инструкции см. в статье [Создание конечных точек](../machine-learning/machine-learning-create-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="b728a-140">See [Create Endpoints](../machine-learning/machine-learning-create-endpoint.md) article for steps.</span></span> <span data-ttu-id="b728a-141">После создания обновляемых конечной точки не по умолчанию hello hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="b728a-141">After you create hello non-default updatable endpoint, do hello following steps:</span></span>

* <span data-ttu-id="b728a-142">Нажмите кнопку **ПАКЕТНОЕ выполнение** tooget hello URI значение для hello **mlEndpoint** свойства JSON.</span><span class="sxs-lookup"><span data-stu-id="b728a-142">Click **BATCH EXECUTION** tooget hello URI value for hello **mlEndpoint** JSON property.</span></span>
* <span data-ttu-id="b728a-143">Нажмите кнопку **обновления РЕСУРСА** tooget значение URI hello для hello ссылки **updateResourceEndpoint** свойства JSON.</span><span class="sxs-lookup"><span data-stu-id="b728a-143">Click **UPDATE RESOURCE** link tooget hello URI value for hello **updateResourceEndpoint** JSON property.</span></span> <span data-ttu-id="b728a-144">ключ API Hello — на самой странице hello конечной точки (в нижнем правом углу hello).</span><span class="sxs-lookup"><span data-stu-id="b728a-144">hello API key is on hello endpoint page itself (in hello bottom-right corner).</span></span>

![обновляемая конечная точка](./media/data-factory-azure-ml-batch-execution-activity/updatable-endpoint.png)

<span data-ttu-id="b728a-146">Следующий пример Hello предоставляет пример определения JSON для hello AzureML связанной службы.</span><span class="sxs-lookup"><span data-stu-id="b728a-146">hello following example provides a sample JSON definition for hello AzureML linked service.</span></span> <span data-ttu-id="b728a-147">Здравствуйте, apiKey hello связанная служба использует для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="b728a-147">hello linked service uses hello apiKey for authentication.</span></span>  

```json
{
    "name": "updatableScoringEndpoint2",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/xxx/services/--scoring experiment--/jobs",
            "apiKey": "endpoint2Key",
            "updateResourceEndpoint": "https://management.azureml.net/workspaces/xxx/webservices/--scoring experiment--/endpoints/endpoint2"
        }
    }
}
```

## <a name="scoring-web-service-is-azure-resource-manager-web-service"></a><span data-ttu-id="b728a-148">Веб-служба оценки — веб-служба Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b728a-148">Scoring web service is Azure Resource Manager web service</span></span> 
<span data-ttu-id="b728a-149">Если веб-служба hello hello новый тип веб-службу, предоставляющую конечную точку диспетчера ресурсов Azure, нет необходимости tooadd hello второй **нестандартных** конечной точки.</span><span class="sxs-lookup"><span data-stu-id="b728a-149">If hello web service is hello new type of web service that exposes an Azure Resource Manager endpoint, you do not need tooadd hello second **non-default** endpoint.</span></span> <span data-ttu-id="b728a-150">Hello **updateResourceEndpoint** в hello связанной службы имеет формат hello:</span><span class="sxs-lookup"><span data-stu-id="b728a-150">hello **updateResourceEndpoint** in hello linked service is of hello format:</span></span> 

```
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resource-group-name}/providers/Microsoft.MachineLearning/webServices/{web-service-name}?api-version=2016-05-01-preview. 
```

<span data-ttu-id="b728a-151">Вы можете получить значения для владельцев месте в URL-АДРЕСЕ hello при запросе hello веб-службы на hello [веб-портал Azure машины обучения службы](https://services.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="b728a-151">You can get values for place holders in hello URL when querying hello web service on hello [Azure Machine Learning Web Services Portal](https://services.azureml.net/).</span></span> <span data-ttu-id="b728a-152">Hello новый тип конечной точки обновления ресурса требуется маркер AAD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="b728a-152">hello new type of update resource endpoint requires an AAD (Azure Active Directory) token.</span></span> <span data-ttu-id="b728a-153">Укажите **servicePrincipalId** и **servicePrincipalKey** в связанной службе AzureML.</span><span class="sxs-lookup"><span data-stu-id="b728a-153">Specify **servicePrincipalId** and **servicePrincipalKey**in AzureML linked service.</span></span> <span data-ttu-id="b728a-154">В разделе [как участника службы и назначьте разрешения toomanage ресурсов Azure toocreate](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b728a-154">See [how toocreate service principal and assign permissions toomanage Azure resource](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="b728a-155">Ниже приведен пример определения связанной службы AzureML.</span><span class="sxs-lookup"><span data-stu-id="b728a-155">Here is a sample AzureML linked service definition:</span></span> 

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "description": "hello linked service for AML web service.",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/0000000000000000000000000000000000000/services/0000000000000000000000000000000000000/jobs?api-version=2.0",
            "apiKey": "xxxxxxxxxxxx",
            "updateResourceEndpoint": "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myRG/providers/Microsoft.MachineLearning/webServices/myWebService?api-version=2016-05-01-preview",
            "servicePrincipalId": "000000000-0000-0000-0000-0000000000000",
            "servicePrincipalKey": "xxxxx",
            "tenant": "mycompany.com"
        }
    }
}
```

<span data-ttu-id="b728a-156">Hello следующий сценарий более подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="b728a-156">hello following scenario provides more details.</span></span> <span data-ttu-id="b728a-157">Он представляет пример повторного обучения и обновления моделей машинного обучения Azure из конвейера фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="b728a-157">It has an example for retraining and updating Azure ML models from an Azure Data Factory pipeline.</span></span>

## <a name="scenario-retraining-and-updating-an-azure-ml-model"></a><span data-ttu-id="b728a-158">Сценарий: повторное обучение и обновление модели машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="b728a-158">Scenario: retraining and updating an Azure ML model</span></span>
<span data-ttu-id="b728a-159">Этот раздел содержит пример конвейера, который использует hello **операции при выполнении пакета Azure ML** tooretrain модели.</span><span class="sxs-lookup"><span data-stu-id="b728a-159">This section provides a sample pipeline that uses hello **Azure ML Batch Execution activity** tooretrain a model.</span></span> <span data-ttu-id="b728a-160">конвейер Hello также использует hello **действия ресурса обновления машинного Обучения Azure** tooupdate модели hello в hello оценки веб-службы.</span><span class="sxs-lookup"><span data-stu-id="b728a-160">hello pipeline also uses hello **Azure ML Update Resource activity** tooupdate hello model in hello scoring web service.</span></span> <span data-ttu-id="b728a-161">Кроме того, раздел Hello предоставляет hello фрагменты JSON для всех связанных службах, наборы данных и конвейер в примере hello.</span><span class="sxs-lookup"><span data-stu-id="b728a-161">hello section also provides JSON snippets for all hello linked services, datasets, and pipeline in hello example.</span></span>

<span data-ttu-id="b728a-162">Вот представление диаграммы hello конвейера образец hello.</span><span class="sxs-lookup"><span data-stu-id="b728a-162">Here is hello diagram view of hello sample pipeline.</span></span> <span data-ttu-id="b728a-163">Как видите, hello действие выполнения пакета машинного Обучения Azure принимает входные данные обучения hello и создает выходные данные обучения (файл iLearner).</span><span class="sxs-lookup"><span data-stu-id="b728a-163">As you can see, hello Azure ML Batch Execution Activity takes hello training input and produces a training output (iLearner file).</span></span> <span data-ttu-id="b728a-164">Hello действия ресурса обновления машинного Обучения Azure принимает выходные данные обучения и обновления hello модели в hello оценки конечной веб-службы.</span><span class="sxs-lookup"><span data-stu-id="b728a-164">hello Azure ML Update Resource Activity takes this training output and updates hello model in hello scoring web service endpoint.</span></span> <span data-ttu-id="b728a-165">Hello действия ресурса обновления не создает никаких выходных данных.</span><span class="sxs-lookup"><span data-stu-id="b728a-165">hello Update Resource Activity does not produce any output.</span></span> <span data-ttu-id="b728a-166">Hello placeholderBlob является просто пустой результирующий набор данных, которые требуются для конвейера hello toorun служба фабрики данных Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b728a-166">hello placeholderBlob is just a dummy output dataset that is required by hello Azure Data Factory service toorun hello pipeline.</span></span>

![схема конвейера](./media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

### <a name="azure-blob-storage-linked-service"></a><span data-ttu-id="b728a-168">Связанная служба хранилища BLOB-объектов Azure</span><span class="sxs-lookup"><span data-stu-id="b728a-168">Azure Blob storage linked service:</span></span>
<span data-ttu-id="b728a-169">Hello хранилища Azure содержит hello следующие данные:</span><span class="sxs-lookup"><span data-stu-id="b728a-169">hello Azure Storage holds hello following data:</span></span>

* <span data-ttu-id="b728a-170">Данные для обучения.</span><span class="sxs-lookup"><span data-stu-id="b728a-170">training data.</span></span> <span data-ttu-id="b728a-171">Hello входные данные для hello Azure ML обучения веб-службы.</span><span class="sxs-lookup"><span data-stu-id="b728a-171">hello input data for hello Azure ML training web service.</span></span>  
* <span data-ttu-id="b728a-172">Файл iLearner.</span><span class="sxs-lookup"><span data-stu-id="b728a-172">iLearner file.</span></span> <span data-ttu-id="b728a-173">Здравствуйте, выходные данные hello Azure ML обучения веб-службы.</span><span class="sxs-lookup"><span data-stu-id="b728a-173">hello output from hello Azure ML training web service.</span></span> <span data-ttu-id="b728a-174">Этот файл также является hello ввода toohello действия ресурса обновления.</span><span class="sxs-lookup"><span data-stu-id="b728a-174">This file is also hello input toohello Update Resource activity.</span></span>  

<span data-ttu-id="b728a-175">Вот определение JSON образец hello hello связанной службы.</span><span class="sxs-lookup"><span data-stu-id="b728a-175">Here is hello sample JSON definition of hello linked service:</span></span>

```JSON
{
    "name": "StorageLinkedService",
      "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=name;AccountKey=key"
        }
    }
}
```

### <a name="training-input-dataset"></a><span data-ttu-id="b728a-176">Входной набор данных для обучения:</span><span class="sxs-lookup"><span data-stu-id="b728a-176">Training input dataset:</span></span>
<span data-ttu-id="b728a-177">Hello следующий набор данных представляет hello входной обучающие данные для hello Azure ML обучения веб-службы.</span><span class="sxs-lookup"><span data-stu-id="b728a-177">hello following dataset represents hello input training data for hello Azure ML training web service.</span></span> <span data-ttu-id="b728a-178">Этот набор данных в качестве входного значения Hello Azure ML Пакетное выполнение действия.</span><span class="sxs-lookup"><span data-stu-id="b728a-178">hello Azure ML Batch Execution activity takes this dataset as an input.</span></span>

```JSON
{
    "name": "trainingData",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "labeledexamples",
            "fileName": "labeledexamples.arff",
            "format": {
                "type": "TextFormat"
            }
        },
        "availability": {
            "frequency": "Week",
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

### <a name="training-output-dataset"></a><span data-ttu-id="b728a-179">Выходной набор данных для обучения:</span><span class="sxs-lookup"><span data-stu-id="b728a-179">Training output dataset:</span></span>
<span data-ttu-id="b728a-180">Hello следующий набор данных представляет hello выходной файл iLearner из hello Azure ML обучения веб-службы.</span><span class="sxs-lookup"><span data-stu-id="b728a-180">hello following dataset represents hello output iLearner file from hello Azure ML training web service.</span></span> <span data-ttu-id="b728a-181">Действие выполнения пакета машинного Обучения Azure Hello создает этот набор данных.</span><span class="sxs-lookup"><span data-stu-id="b728a-181">hello Azure ML Batch Execution Activity produces this dataset.</span></span> <span data-ttu-id="b728a-182">Этот набор данных также является hello ввода toohello действия ресурса обновления машинного Обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="b728a-182">This dataset is also hello input toohello Azure ML Update Resource activity.</span></span>

```JSON
{
    "name": "trainedModelBlob",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "trainingoutput",
            "fileName": "model.ilearner",
            "format": {
                "type": "TextFormat"
            }
        },
        "availability": {
            "frequency": "Week",
            "interval": 1
        }
    }
}
```

### <a name="linked-service-for-azure-ml-training-endpoint"></a><span data-ttu-id="b728a-183">Связанная служба для конечной точки машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="b728a-183">Linked service for Azure ML training endpoint</span></span>
<span data-ttu-id="b728a-184">Привет, следующий фрагмент JSON определяет Azure связанной службы машинного обучения, указывающий конечную точку по умолчанию toohello hello обучения веб-службы.</span><span class="sxs-lookup"><span data-stu-id="b728a-184">hello following JSON snippet defines an Azure Machine Learning linked service that points toohello default endpoint of hello training web service.</span></span>

```JSON
{    
    "name": "trainingEndpoint",
      "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/xxx/services/--training experiment--/jobs",
              "apiKey": "myKey"
        }
      }
}
```

<span data-ttu-id="b728a-185">В **Azure ML Studio**, hello следующие параметры tooget для **mlEndpoint** и **apiKey**:</span><span class="sxs-lookup"><span data-stu-id="b728a-185">In **Azure ML Studio**, do hello following tooget values for **mlEndpoint** and **apiKey**:</span></span>

1. <span data-ttu-id="b728a-186">Нажмите кнопку **веб-службы** hello левом меню.</span><span class="sxs-lookup"><span data-stu-id="b728a-186">Click **WEB SERVICES** on hello left menu.</span></span>
2. <span data-ttu-id="b728a-187">Нажмите кнопку hello **обучения веб-службы** в списке hello веб-служб.</span><span class="sxs-lookup"><span data-stu-id="b728a-187">Click hello **training web service** in hello list of web services.</span></span>
3. <span data-ttu-id="b728a-188">Щелкните "Копировать" рядом слишком**ключ API** текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="b728a-188">Click copy next too**API key** text box.</span></span> <span data-ttu-id="b728a-189">Вставьте ключ hello в буфер обмена hello в редактор JSON фабрики данных hello.</span><span class="sxs-lookup"><span data-stu-id="b728a-189">Paste hello key in hello clipboard into hello Data Factory JSON editor.</span></span>
4. <span data-ttu-id="b728a-190">В hello **Azure ML studio**, нажмите кнопку **ПАКЕТНОЕ выполнение** ссылку.</span><span class="sxs-lookup"><span data-stu-id="b728a-190">In hello **Azure ML studio**, click **BATCH EXECUTION** link.</span></span>
5. <span data-ttu-id="b728a-191">Копировать hello **URI запроса** из hello **запроса** раздела и вставьте его в редактор JSON фабрики данных hello.</span><span class="sxs-lookup"><span data-stu-id="b728a-191">Copy hello **Request URI** from hello **Request** section and paste it into hello Data Factory JSON editor.</span></span>   

### <a name="linked-service-for-azure-ml-updatable-scoring-endpoint"></a><span data-ttu-id="b728a-192">Связанная служба для обновляемой конечной точки оценки машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="b728a-192">Linked Service for Azure ML updatable scoring endpoint:</span></span>
<span data-ttu-id="b728a-193">Привет, следующий фрагмент JSON определяет Azure связанной службы машинного обучения, указывающий toohello нестандартных обновляемых конечную точку hello оценки веб-службы.</span><span class="sxs-lookup"><span data-stu-id="b728a-193">hello following JSON snippet defines an Azure Machine Learning linked service that points toohello non-default updatable endpoint of hello scoring web service.</span></span>  

```JSON
{
    "name": "updatableScoringEndpoint2",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/00000000eb0abe4d6bbb1d7886062747d7/services/00000000026734a5889e02fbb1f65cefd/jobs?api-version=2.0",
            "apiKey": "sooooooooooh3WvG1hBfKS2BNNcfwSO7hhY6dY98noLfOdqQydYDIXyf2KoIaN3JpALu/AKtflHWMOCuicm/Q==",
            "updateResourceEndpoint": "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/myWebService?api-version=2016-05-01-preview",
            "servicePrincipalId": "fe200044-c008-4008-a005-94000000731",
            "servicePrincipalKey": "zWa0000000000Tp6FjtZOspK/WMA2tQ08c8U+gZRBlw=",
            "tenant": "mycompany.com"
        }
    }
}
```

### <a name="placeholder-output-dataset"></a><span data-ttu-id="b728a-194">Заполнитель выходного набора данных</span><span class="sxs-lookup"><span data-stu-id="b728a-194">Placeholder output dataset:</span></span>
<span data-ttu-id="b728a-195">Hello действия ресурса обновления машинного Обучения Azure не создает никаких выходных данных.</span><span class="sxs-lookup"><span data-stu-id="b728a-195">hello Azure ML Update Resource activity does not generate any output.</span></span> <span data-ttu-id="b728a-196">Однако фабрики данных Azure требует toodrive hello выходного набора данных расписания конвейера.</span><span class="sxs-lookup"><span data-stu-id="b728a-196">However, Azure Data Factory requires an output dataset toodrive hello schedule of a pipeline.</span></span> <span data-ttu-id="b728a-197">Поэтому в этом примере используется фиктивный набор данных (заполнитель набора данных).</span><span class="sxs-lookup"><span data-stu-id="b728a-197">Therefore, we use a dummy/placeholder dataset in this example.</span></span>  

```JSON
{
    "name": "placeholderBlob",
    "properties": {
        "availability": {
            "frequency": "Week",
            "interval": 1
        },
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "any",
            "format": {
                "type": "TextFormat"
            }
        }
    }
}
```

### <a name="pipeline"></a><span data-ttu-id="b728a-198">Конвейер</span><span class="sxs-lookup"><span data-stu-id="b728a-198">Pipeline</span></span>
<span data-ttu-id="b728a-199">Hello конвейера содержит два действия: **AzureMLBatchExecution** и **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="b728a-199">hello pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span></span> <span data-ttu-id="b728a-200">Hello операции при выполнении пакета машинного Обучения Azure принимает hello обучающие данные в качестве входных данных и создает файл iLearner, как выходные данные.</span><span class="sxs-lookup"><span data-stu-id="b728a-200">hello Azure ML Batch Execution activity takes hello training data as input and produces an iLearner file as an output.</span></span> <span data-ttu-id="b728a-201">Действие Hello вызывает hello обучения веб-службы (эксперимента обучения в виде веб-службы) с входными данными hello обучающих данных и получает от веб-службы hello файл ilearner hello.</span><span class="sxs-lookup"><span data-stu-id="b728a-201">hello activity invokes hello training web service (training experiment exposed as a web service) with hello input training data and receives hello ilearner file from hello webservice.</span></span> <span data-ttu-id="b728a-202">Hello placeholderBlob является просто пустой результирующий набор данных, которые требуются для конвейера hello toorun служба фабрики данных Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b728a-202">hello placeholderBlob is just a dummy output dataset that is required by hello Azure Data Factory service toorun hello pipeline.</span></span>

![схема конвейера](./media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [
            {
                "name": "retraining",
                "type": "AzureMLBatchExecution",
                "inputs": [
                    {
                        "name": "trainingData"
                    }
                ],
                "outputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "typeProperties": {
                    "webServiceInput": "trainingData",
                    "webServiceOutputs": {
                        "output1": "trainedModelBlob"
                    }              
                 },
                "linkedServiceName": "trainingEndpoint",
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            },
            {
                "type": "AzureMLUpdateResource",
                "typeProperties": {
                    "trainedModelName": "Training Exp for ADF ML [trained model]",
                    "trainedModelDatasetName" :  "trainedModelBlob"
                },
                "inputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "outputs": [
                    {
                        "name": "placeholderBlob"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "AzureML Update Resource",
                "linkedServiceName": "updatableScoringEndpoint2"
            }
        ],
        "start": "2016-02-13T00:00:00Z",
           "end": "2016-02-14T00:00:00Z"
    }
}
```
