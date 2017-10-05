---
title: "Обновление моделей машинного обучения с помощью фабрики данных Azure | Документация Майкрософт"
description: "Описывается, как создавать прогнозирующие конвейеры с помощью фабрики данных Azure и машинного обучения Azure."
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
ms.openlocfilehash: e31a7a59d14de4382190b39bd70f3ddf6cf673ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="updating-azure-machine-learning-models-using-update-resource-activity"></a><span data-ttu-id="a4eed-103">Обновление моделей машинного обучения Azure с помощью действия "Обновить ресурс"</span><span class="sxs-lookup"><span data-stu-id="a4eed-103">Updating Azure Machine Learning models using Update Resource Activity</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="a4eed-104">Действие Hive</span><span class="sxs-lookup"><span data-stu-id="a4eed-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="a4eed-105">Действие Pig</span><span class="sxs-lookup"><span data-stu-id="a4eed-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="a4eed-106">Действие MapReduce</span><span class="sxs-lookup"><span data-stu-id="a4eed-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="a4eed-107">Потоковая активность Hadoop</span><span class="sxs-lookup"><span data-stu-id="a4eed-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="a4eed-108">Действие Spark</span><span class="sxs-lookup"><span data-stu-id="a4eed-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="a4eed-109">Действие выполнения пакета машинного обучения</span><span class="sxs-lookup"><span data-stu-id="a4eed-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="a4eed-110">Действие "Обновить ресурс" в службе машинного обучения</span><span class="sxs-lookup"><span data-stu-id="a4eed-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="a4eed-111">Действие хранимой процедуры</span><span class="sxs-lookup"><span data-stu-id="a4eed-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="a4eed-112">Действие U-SQL в Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="a4eed-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="a4eed-113">Настраиваемое действие .NET</span><span class="sxs-lookup"><span data-stu-id="a4eed-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="a4eed-114">Эта статья дополняет основную статью, посвященную интеграции фабрики данных Azure и машинного обучения Azure: [Создание прогнозирующих конвейеров с помощью машинного обучения Azure и фабрики данных Azure](data-factory-azure-ml-batch-execution-activity.md).</span><span class="sxs-lookup"><span data-stu-id="a4eed-114">This article complements the main Azure Data Factory - Azure Machine Learning integration article: [Create predictive pipelines using Azure Machine Learning and Azure Data Factory](data-factory-azure-ml-batch-execution-activity.md).</span></span> <span data-ttu-id="a4eed-115">Перед прочтением этой статьи ознакомьтесь с основной статьей, если вы еще этого не сделали.</span><span class="sxs-lookup"><span data-stu-id="a4eed-115">If you haven't already done so, review the main article before reading through this article.</span></span> 

## <a name="overview"></a><span data-ttu-id="a4eed-116">Обзор</span><span class="sxs-lookup"><span data-stu-id="a4eed-116">Overview</span></span>
<span data-ttu-id="a4eed-117">Со временем прогнозные модели из оценивающих экспериментов машинного обучения Azure потребуют повторного обучения с помощью новых наборов входных данных.</span><span class="sxs-lookup"><span data-stu-id="a4eed-117">Over time, the predictive models in the Azure ML scoring experiments need to be retrained using new input datasets.</span></span> <span data-ttu-id="a4eed-118">Когда повторное обучение будет завершено, вам потребуется обновить веб-службу оценки на основании обновленной модели машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="a4eed-118">After you are done with retraining, you want to update the scoring web service with the retrained ML model.</span></span> <span data-ttu-id="a4eed-119">Для использования новых данных и обновления моделей машинного обучения Azure через веб-службы выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a4eed-119">The typical steps to enable retraining and updating Azure ML models via web services are:</span></span>

1. <span data-ttu-id="a4eed-120">Создайте эксперимент в [Студии машинного обучения Azure](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="a4eed-120">Create an experiment in [Azure ML Studio](https://studio.azureml.net).</span></span>
2. <span data-ttu-id="a4eed-121">Если модель вас устраивает, то опубликуйте веб-службы для **обучающего эксперимента** и оценивающего или **прогнозного эксперимента** с помощью Студии машинного обучения Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="a4eed-121">When you are satisfied with the model, use Azure ML Studio to publish web services for both the **training experiment** and scoring/**predictive experiment**.</span></span>

<span data-ttu-id="a4eed-122">В следующей таблице описаны веб-службы, используемые в данном примере.</span><span class="sxs-lookup"><span data-stu-id="a4eed-122">The following table describes the web services used in this example.</span></span>  <span data-ttu-id="a4eed-123">Подробные сведения см. в статье [Программное переобучение моделей машинного обучения](../machine-learning/machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="a4eed-123">See [Retrain Machine Learning models programmatically](../machine-learning/machine-learning-retrain-models-programmatically.md) for details.</span></span>

- <span data-ttu-id="a4eed-124">**Веб-служба обучения**: получает данные для обучения и создает обученные модели.</span><span class="sxs-lookup"><span data-stu-id="a4eed-124">**Training web service** - Receives training data and produces trained models.</span></span> <span data-ttu-id="a4eed-125">Результат повторного обучения — файл формата ILEARNER в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="a4eed-125">The output of the retraining is an .ilearner file in an Azure Blob storage.</span></span> <span data-ttu-id="a4eed-126">При публикации обучающего эксперимента в виде веб-службы автоматически создается **конечная точка по умолчанию** .</span><span class="sxs-lookup"><span data-stu-id="a4eed-126">The **default endpoint** is automatically created for you when you publish the training experiment as a web service.</span></span> <span data-ttu-id="a4eed-127">Вы можете создать несколько конечных точек, но в этом примере используется только конечная точка по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a4eed-127">You can create more endpoints but the example uses only the default endpoint.</span></span>
- <span data-ttu-id="a4eed-128">**Веб-служба оценки**: получает данные без метки и осуществляет прогнозирование.</span><span class="sxs-lookup"><span data-stu-id="a4eed-128">**Scoring web service** - Receives unlabeled data examples and makes predictions.</span></span> <span data-ttu-id="a4eed-129">Результаты прогноза могут записываться в различных форматах, например в CSV-файлы или строки в базе данных SQL Azure (в зависимости от конфигурации эксперимента).</span><span class="sxs-lookup"><span data-stu-id="a4eed-129">The output of prediction could have various forms, such as a .csv file or rows in an Azure SQL database, depending on the configuration of the experiment.</span></span> <span data-ttu-id="a4eed-130">При публикации прогнозного эксперимента в виде веб-службы автоматически создается конечная точка по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a4eed-130">The default endpoint is automatically created for you when you publish the predictive experiment as a web service.</span></span> 

<span data-ttu-id="a4eed-131">На следующей схеме показана связь между конечными точками обучения и конечными точками оценки в машинном обучении Azure.</span><span class="sxs-lookup"><span data-stu-id="a4eed-131">The following picture depicts the relationship between training and scoring endpoints in Azure ML.</span></span>

![ВЕБ-СЛУЖБЫ](./media/data-factory-azure-ml-batch-execution-activity/web-services.png)

<span data-ttu-id="a4eed-133">Чтобы вызвать **веб-службу обучения**, воспользуйтесь **действием выполнения пакета машинного обучения Azure**.</span><span class="sxs-lookup"><span data-stu-id="a4eed-133">You can invoke the **training web service** by using the **Azure ML Batch Execution Activity**.</span></span> <span data-ttu-id="a4eed-134">Это действие аналогично обращению к веб-службе машинного обучения Azure (веб-службе оценки) для получения данных оценки.</span><span class="sxs-lookup"><span data-stu-id="a4eed-134">Invoking a training web service is same as invoking an Azure ML web service (scoring web service) for scoring data.</span></span> <span data-ttu-id="a4eed-135">В предыдущих разделах подробно описано, как обращаться к веб-службе машинного обучения Azure из конвейера фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="a4eed-135">The preceding sections cover how to invoke an Azure ML web service from an Azure Data Factory pipeline in detail.</span></span> 

<span data-ttu-id="a4eed-136">Чтобы обновить веб-службу с помощью заново обученной модели, можно вызвать **веб-службу оценки**, воспользовавшись **действием ресурса обновления машинного обучения Azure**.</span><span class="sxs-lookup"><span data-stu-id="a4eed-136">You can invoke the **scoring web service** by using the **Azure ML Update Resource Activity** to update the web service with the newly trained model.</span></span> <span data-ttu-id="a4eed-137">Ниже приведены примеры определений связанной службы.</span><span class="sxs-lookup"><span data-stu-id="a4eed-137">The following examples provide linked service definitions:</span></span> 

## <a name="scoring-web-service-is-a-classic-web-service"></a><span data-ttu-id="a4eed-138">Веб-служба оценки — классическая веб-служба</span><span class="sxs-lookup"><span data-stu-id="a4eed-138">Scoring web service is a classic web service</span></span>
<span data-ttu-id="a4eed-139">Если веб-служба оценки является **классической веб-службой**, то создайте вторую **обновляемую конечную точку не по умолчанию** с помощью [портала Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="a4eed-139">If the scoring web service is a **classic web service**, create the second **non-default and updatable endpoint** by using the [Azure portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="a4eed-140">Инструкции см. в статье [Создание конечных точек](../machine-learning/machine-learning-create-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="a4eed-140">See [Create Endpoints](../machine-learning/machine-learning-create-endpoint.md) article for steps.</span></span> <span data-ttu-id="a4eed-141">Создав обновляемую конечную точку не по умолчанию, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="a4eed-141">After you create the non-default updatable endpoint, do the following steps:</span></span>

* <span data-ttu-id="a4eed-142">Щелкните **Выполнение пакета**, чтобы получить значение URI свойства JSON **mlEndpoint**.</span><span class="sxs-lookup"><span data-stu-id="a4eed-142">Click **BATCH EXECUTION** to get the URI value for the **mlEndpoint** JSON property.</span></span>
* <span data-ttu-id="a4eed-143">Затем щелкните **Обновить ресурс**, чтобы получить значение URI свойства JSON **updateResourceEndpoint**.</span><span class="sxs-lookup"><span data-stu-id="a4eed-143">Click **UPDATE RESOURCE** link to get the URI value for the **updateResourceEndpoint** JSON property.</span></span> <span data-ttu-id="a4eed-144">Ключ API указывается на странице конечной точки (в правом нижнем углу).</span><span class="sxs-lookup"><span data-stu-id="a4eed-144">The API key is on the endpoint page itself (in the bottom-right corner).</span></span>

![обновляемая конечная точка](./media/data-factory-azure-ml-batch-execution-activity/updatable-endpoint.png)

<span data-ttu-id="a4eed-146">В следующем примере представлен вариант определения JSON для связанной службы AzureML.</span><span class="sxs-lookup"><span data-stu-id="a4eed-146">The following example provides a sample JSON definition for the AzureML linked service.</span></span> <span data-ttu-id="a4eed-147">Связанная служба использует для аутентификации ключ apiKey.</span><span class="sxs-lookup"><span data-stu-id="a4eed-147">The linked service uses the apiKey for authentication.</span></span>  

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

## <a name="scoring-web-service-is-azure-resource-manager-web-service"></a><span data-ttu-id="a4eed-148">Веб-служба оценки — веб-служба Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a4eed-148">Scoring web service is Azure Resource Manager web service</span></span> 
<span data-ttu-id="a4eed-149">Если веб-служба является новым типом веб-службы и предоставляет конечную точку Azure Resource Manager, то необходимо добавить вторую конечную точку **не по умолчанию**.</span><span class="sxs-lookup"><span data-stu-id="a4eed-149">If the web service is the new type of web service that exposes an Azure Resource Manager endpoint, you do not need to add the second **non-default** endpoint.</span></span> <span data-ttu-id="a4eed-150">Конечная точка **updateResourceEndpoint** в связанной службе имеет такой формат:</span><span class="sxs-lookup"><span data-stu-id="a4eed-150">The **updateResourceEndpoint** in the linked service is of the format:</span></span> 

```
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resource-group-name}/providers/Microsoft.MachineLearning/webServices/{web-service-name}?api-version=2016-05-01-preview. 
```

<span data-ttu-id="a4eed-151">Значения для заполнителей в URL-адресе при выполнении запросов к веб-службе можно найти на [портале веб-служб машинного обучения Azure](https://services.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="a4eed-151">You can get values for place holders in the URL when querying the web service on the [Azure Machine Learning Web Services Portal](https://services.azureml.net/).</span></span> <span data-ttu-id="a4eed-152">Для нового типа конечной точки обновления ресурса требуется маркер AAD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="a4eed-152">The new type of update resource endpoint requires an AAD (Azure Active Directory) token.</span></span> <span data-ttu-id="a4eed-153">Укажите **servicePrincipalId** и **servicePrincipalKey** в связанной службе AzureML.</span><span class="sxs-lookup"><span data-stu-id="a4eed-153">Specify **servicePrincipalId** and **servicePrincipalKey**in AzureML linked service.</span></span> <span data-ttu-id="a4eed-154">Ознакомьтесь со статьей [Создание приложения Active Directory и субъекта-службы с доступом к ресурсам с помощью портала](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a4eed-154">See [how to create service principal and assign permissions to manage Azure resource](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="a4eed-155">Ниже приведен пример определения связанной службы AzureML.</span><span class="sxs-lookup"><span data-stu-id="a4eed-155">Here is a sample AzureML linked service definition:</span></span> 

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "description": "The linked service for AML web service.",
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

<span data-ttu-id="a4eed-156">Ниже приведен сценарий с более подробными сведениями.</span><span class="sxs-lookup"><span data-stu-id="a4eed-156">The following scenario provides more details.</span></span> <span data-ttu-id="a4eed-157">Он представляет пример повторного обучения и обновления моделей машинного обучения Azure из конвейера фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="a4eed-157">It has an example for retraining and updating Azure ML models from an Azure Data Factory pipeline.</span></span>

## <a name="scenario-retraining-and-updating-an-azure-ml-model"></a><span data-ttu-id="a4eed-158">Сценарий: повторное обучение и обновление модели машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="a4eed-158">Scenario: retraining and updating an Azure ML model</span></span>
<span data-ttu-id="a4eed-159">В этом разделе показан пример конвейера, который использует **действие выполнения пакета машинного обучения Azure** для повторного обучения модели,</span><span class="sxs-lookup"><span data-stu-id="a4eed-159">This section provides a sample pipeline that uses the **Azure ML Batch Execution activity** to retrain a model.</span></span> <span data-ttu-id="a4eed-160">а также **действие ресурса обновления машинного обучения Azure** для обновления модели в веб-службе оценки.</span><span class="sxs-lookup"><span data-stu-id="a4eed-160">The pipeline also uses the **Azure ML Update Resource activity** to update the model in the scoring web service.</span></span> <span data-ttu-id="a4eed-161">Здесь также приведены фрагменты JSON для всех связанных служб, наборов данных и конвейера, которые используются в примере.</span><span class="sxs-lookup"><span data-stu-id="a4eed-161">The section also provides JSON snippets for all the linked services, datasets, and pipeline in the example.</span></span>

<span data-ttu-id="a4eed-162">Пример конвейера представлен на схеме.</span><span class="sxs-lookup"><span data-stu-id="a4eed-162">Here is the diagram view of the sample pipeline.</span></span> <span data-ttu-id="a4eed-163">Как видите, действие "Выполнение пакета" машинного обучения Azure принимает входные данные обучения и создает выходные данные обучения (файл iLearner).</span><span class="sxs-lookup"><span data-stu-id="a4eed-163">As you can see, the Azure ML Batch Execution Activity takes the training input and produces a training output (iLearner file).</span></span> <span data-ttu-id="a4eed-164">Действие «Обновить ресурс» машинного обучения Azure принимает эти результаты и обновляет модель через конечную точку веб-службы оценки.</span><span class="sxs-lookup"><span data-stu-id="a4eed-164">The Azure ML Update Resource Activity takes this training output and updates the model in the scoring web service endpoint.</span></span> <span data-ttu-id="a4eed-165">Действие «Обновить ресурс» не создает никаких выходных данных.</span><span class="sxs-lookup"><span data-stu-id="a4eed-165">The Update Resource Activity does not produce any output.</span></span> <span data-ttu-id="a4eed-166">Набор данных placeholderBlob является фиктивным набором данных, который необходим фабрике данных Azure для запуска конвейера.</span><span class="sxs-lookup"><span data-stu-id="a4eed-166">The placeholderBlob is just a dummy output dataset that is required by the Azure Data Factory service to run the pipeline.</span></span>

![схема конвейера](./media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

### <a name="azure-blob-storage-linked-service"></a><span data-ttu-id="a4eed-168">Связанная служба хранилища BLOB-объектов Azure</span><span class="sxs-lookup"><span data-stu-id="a4eed-168">Azure Blob storage linked service:</span></span>
<span data-ttu-id="a4eed-169">Служба хранилища Azure содержит следующие данные:</span><span class="sxs-lookup"><span data-stu-id="a4eed-169">The Azure Storage holds the following data:</span></span>

* <span data-ttu-id="a4eed-170">Данные для обучения.</span><span class="sxs-lookup"><span data-stu-id="a4eed-170">training data.</span></span> <span data-ttu-id="a4eed-171">Это входные данные для веб-службы машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="a4eed-171">The input data for the Azure ML training web service.</span></span>  
* <span data-ttu-id="a4eed-172">Файл iLearner.</span><span class="sxs-lookup"><span data-stu-id="a4eed-172">iLearner file.</span></span> <span data-ttu-id="a4eed-173">Это выходные данные из веб-службы машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="a4eed-173">The output from the Azure ML training web service.</span></span> <span data-ttu-id="a4eed-174">Этот файл также служит в качестве входных данных для действия "Обновить ресурс".</span><span class="sxs-lookup"><span data-stu-id="a4eed-174">This file is also the input to the Update Resource activity.</span></span>  

<span data-ttu-id="a4eed-175">Вот пример определения JSON для связанной службы:</span><span class="sxs-lookup"><span data-stu-id="a4eed-175">Here is the sample JSON definition of the linked service:</span></span>

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

### <a name="training-input-dataset"></a><span data-ttu-id="a4eed-176">Входной набор данных для обучения:</span><span class="sxs-lookup"><span data-stu-id="a4eed-176">Training input dataset:</span></span>
<span data-ttu-id="a4eed-177">Следующий набор данных представляет собой учебные данные для веб-службы машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="a4eed-177">The following dataset represents the input training data for the Azure ML training web service.</span></span> <span data-ttu-id="a4eed-178">Действие «Выполнение пакета» машинного обучения Azure использует этот набор в качестве входных данных.</span><span class="sxs-lookup"><span data-stu-id="a4eed-178">The Azure ML Batch Execution activity takes this dataset as an input.</span></span>

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

### <a name="training-output-dataset"></a><span data-ttu-id="a4eed-179">Выходной набор данных для обучения:</span><span class="sxs-lookup"><span data-stu-id="a4eed-179">Training output dataset:</span></span>
<span data-ttu-id="a4eed-180">Следующий набор данных представляет собой выходной файл iLearner из веб-службы машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="a4eed-180">The following dataset represents the output iLearner file from the Azure ML training web service.</span></span> <span data-ttu-id="a4eed-181">Этот набор данных создается с помощью действия "Выполнение пакета" машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="a4eed-181">The Azure ML Batch Execution Activity produces this dataset.</span></span> <span data-ttu-id="a4eed-182">Этот набор данных также является входным для действия "Обновить ресурс" машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="a4eed-182">This dataset is also the input to the Azure ML Update Resource activity.</span></span>

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

### <a name="linked-service-for-azure-ml-training-endpoint"></a><span data-ttu-id="a4eed-183">Связанная служба для конечной точки машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="a4eed-183">Linked service for Azure ML training endpoint</span></span>
<span data-ttu-id="a4eed-184">Следующий фрагмент JSON определяет связанную службу машинного обучения Azure, которая указывает на конечную точку веб-службы обучения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a4eed-184">The following JSON snippet defines an Azure Machine Learning linked service that points to the default endpoint of the training web service.</span></span>

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

<span data-ttu-id="a4eed-185">Чтобы получить значения **mlEndpoint** и **apiKey**, выполните следующие действия в **Студии машинного обучения Azure**:</span><span class="sxs-lookup"><span data-stu-id="a4eed-185">In **Azure ML Studio**, do the following to get values for **mlEndpoint** and **apiKey**:</span></span>

1. <span data-ttu-id="a4eed-186">В меню слева щелкните **ВЕБ-СЛУЖБЫ** .</span><span class="sxs-lookup"><span data-stu-id="a4eed-186">Click **WEB SERVICES** on the left menu.</span></span>
2. <span data-ttu-id="a4eed-187">В списке веб-служб выберите **веб-службу обучения** .</span><span class="sxs-lookup"><span data-stu-id="a4eed-187">Click the **training web service** in the list of web services.</span></span>
3. <span data-ttu-id="a4eed-188">Рядом с полем **Ключ API** нажмите кнопку копирования.</span><span class="sxs-lookup"><span data-stu-id="a4eed-188">Click copy next to **API key** text box.</span></span> <span data-ttu-id="a4eed-189">Вставьте ключ из буфера обмена в редактор JSON фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="a4eed-189">Paste the key in the clipboard into the Data Factory JSON editor.</span></span>
4. <span data-ttu-id="a4eed-190">В **Студии машинного обучения Azure** щелкните ссылку **Выполнение пакета**.</span><span class="sxs-lookup"><span data-stu-id="a4eed-190">In the **Azure ML studio**, click **BATCH EXECUTION** link.</span></span>
5. <span data-ttu-id="a4eed-191">Скопируйте **URI запроса** из раздела **Запрос** и вставьте его в редактор JSON фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="a4eed-191">Copy the **Request URI** from the **Request** section and paste it into the Data Factory JSON editor.</span></span>   

### <a name="linked-service-for-azure-ml-updatable-scoring-endpoint"></a><span data-ttu-id="a4eed-192">Связанная служба для обновляемой конечной точки оценки машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="a4eed-192">Linked Service for Azure ML updatable scoring endpoint:</span></span>
<span data-ttu-id="a4eed-193">Следующий фрагмент JSON определяет связанную службу машинного обучения Azure, которая указывает на конечную точку веб-службы оценки не по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a4eed-193">The following JSON snippet defines an Azure Machine Learning linked service that points to the non-default updatable endpoint of the scoring web service.</span></span>  

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

### <a name="placeholder-output-dataset"></a><span data-ttu-id="a4eed-194">Заполнитель выходного набора данных</span><span class="sxs-lookup"><span data-stu-id="a4eed-194">Placeholder output dataset:</span></span>
<span data-ttu-id="a4eed-195">Действие "Обновить ресурс" машинного обучения Azure не создает никаких выходных данных.</span><span class="sxs-lookup"><span data-stu-id="a4eed-195">The Azure ML Update Resource activity does not generate any output.</span></span> <span data-ttu-id="a4eed-196">Однако фабрике данных Azure требуется выходной набор данных для планирования конвейера.</span><span class="sxs-lookup"><span data-stu-id="a4eed-196">However, Azure Data Factory requires an output dataset to drive the schedule of a pipeline.</span></span> <span data-ttu-id="a4eed-197">Поэтому в этом примере используется фиктивный набор данных (заполнитель набора данных).</span><span class="sxs-lookup"><span data-stu-id="a4eed-197">Therefore, we use a dummy/placeholder dataset in this example.</span></span>  

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

### <a name="pipeline"></a><span data-ttu-id="a4eed-198">Конвейер</span><span class="sxs-lookup"><span data-stu-id="a4eed-198">Pipeline</span></span>
<span data-ttu-id="a4eed-199">Конвейер содержит два действия: **AzureMLBatchExecution** и **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="a4eed-199">The pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span></span> <span data-ttu-id="a4eed-200">Действие "Выполнение пакета" машинного обучения Azure принимает входные данные для обучения и создает выходной файл iLearner.</span><span class="sxs-lookup"><span data-stu-id="a4eed-200">The Azure ML Batch Execution activity takes the training data as input and produces an iLearner file as an output.</span></span> <span data-ttu-id="a4eed-201">Это действие обращается к веб-службе обучения (обучающему эксперименту, опубликованному в виде веб-службы), передает ей данные для обучения и получает файл ilearner.</span><span class="sxs-lookup"><span data-stu-id="a4eed-201">The activity invokes the training web service (training experiment exposed as a web service) with the input training data and receives the ilearner file from the webservice.</span></span> <span data-ttu-id="a4eed-202">Набор данных placeholderBlob является фиктивным набором данных, который необходим фабрике данных Azure для запуска конвейера.</span><span class="sxs-lookup"><span data-stu-id="a4eed-202">The placeholderBlob is just a dummy output dataset that is required by the Azure Data Factory service to run the pipeline.</span></span>

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
