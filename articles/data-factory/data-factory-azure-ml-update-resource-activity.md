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
# <a name="updating-azure-machine-learning-models-using-update-resource-activity"></a>Обновление моделей машинного обучения Azure с помощью действия "Обновить ресурс"

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Действие Hive](data-factory-hive-activity.md) 
> * [Действие Pig](data-factory-pig-activity.md)
> * [Действие MapReduce](data-factory-map-reduce.md)
> * [Потоковая активность Hadoop](data-factory-hadoop-streaming-activity.md)
> * [Действие Spark](data-factory-spark.md)
> * [Действие выполнения пакета машинного обучения](data-factory-azure-ml-batch-execution-activity.md)
> * [Действие "Обновить ресурс" в службе машинного обучения](data-factory-azure-ml-update-resource-activity.md)
> * [Действие хранимой процедуры](data-factory-stored-proc-activity.md)
> * [Действие U-SQL в Data Lake Analytics](data-factory-usql-activity.md)
> * [Настраиваемое действие .NET](data-factory-use-custom-activities.md)

В этой статье дополняет hello основной фабрики данных Azure - статье интеграции машинного обучения Azure: [создание прогнозирующих конвейеров с помощью машинного обучения Azure и фабрики данных Azure](data-factory-azure-ml-batch-execution-activity.md). Если это еще не сделано, изучите статью основные hello перед прочтя эту статью. 

## <a name="overview"></a>Обзор
Со временем hello прогнозных моделей в экспериментах оценки машинного Обучения Azure hello должны toobe повторное обучение с помощью новых входных наборов данных. После завершения переподготовки, вы хотите tooupdate hello оценки веб-службы с hello повторное Обучение модели машинного Обучения. Hello типичные действия tooenable переподготовки и обновление моделей машинного Обучения Azure через веб-службы являются:

1. Создайте эксперимент в [Студии машинного обучения Azure](https://studio.azureml.net).
2. Если вас устраивают hello модели, используйте Azure ML Studio toopublish веб-службы для обоих hello **эксперимента обучения** и оценки /**прогнозной эксперимента**.

Hello следующей таблице описаны hello веб-служб, используемых в этом примере.  Подробные сведения см. в статье [Программное переобучение моделей машинного обучения](../machine-learning/machine-learning-retrain-models-programmatically.md).

- **Веб-служба обучения**: получает данные для обучения и создает обученные модели. Hello переподготовки hello выходные данные — это файл .ilearner в службе хранилища больших двоичных объектов Azure. Hello **по умолчанию конечная точка** создается автоматически для при публикации обучения hello поэкспериментировать веб-службы. Можно создать дополнительные конечные точки, но hello примере используются только конечная точка по умолчанию hello.
- **Веб-служба оценки**: получает данные без метки и осуществляет прогнозирование. Hello выходные данные прогноза, могут иметь различные формы, например, в CSV-файл или строк в базе данных Azure SQL, в зависимости от конфигурации hello hello эксперимента. Конечная точка по умолчанию Hello автоматически создается при публикации hello прогнозной эксперимент как веб-службы. 

Hello на рисунке ниже показана связь hello обучения и оценки конечные точки в Azure ML.

![ВЕБ-СЛУЖБЫ](./media/data-factory-azure-ml-batch-execution-activity/web-services.png)

Можно вызвать hello **обучения веб-службы** с помощью hello **действие выполнения пакета машинного Обучения Azure**. Это действие аналогично обращению к веб-службе машинного обучения Azure (веб-службе оценки) для получения данных оценки. Здравствуйте выше титульных разделов, как к веб-службе машинного Обучения Azure с фабрикой данных Azure tooinvoke конвейера подробно. 

Можно вызвать hello **оценки веб-службы** с помощью hello **действия ресурса обновления машинного Обучения Azure** tooupdate hello веб-службы с hello вновь обученной модели. Привет, следующие примеры содержат определения связанной службы: 

## <a name="scoring-web-service-is-a-classic-web-service"></a>Веб-служба оценки — классическая веб-служба
Если hello оценки веб-службы **классического веб-службы**, создать второй hello **конечной точки не по умолчанию и обновляемые** с помощью hello [портал Azure](https://manage.windowsazure.com). Инструкции см. в статье [Создание конечных точек](../machine-learning/machine-learning-create-endpoint.md). После создания обновляемых конечной точки не по умолчанию hello hello следующие шаги:

* Нажмите кнопку **ПАКЕТНОЕ выполнение** tooget hello URI значение для hello **mlEndpoint** свойства JSON.
* Нажмите кнопку **обновления РЕСУРСА** tooget значение URI hello для hello ссылки **updateResourceEndpoint** свойства JSON. ключ API Hello — на самой странице hello конечной точки (в нижнем правом углу hello).

![обновляемая конечная точка](./media/data-factory-azure-ml-batch-execution-activity/updatable-endpoint.png)

Следующий пример Hello предоставляет пример определения JSON для hello AzureML связанной службы. Здравствуйте, apiKey hello связанная служба использует для проверки подлинности.  

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

## <a name="scoring-web-service-is-azure-resource-manager-web-service"></a>Веб-служба оценки — веб-служба Azure Resource Manager 
Если веб-служба hello hello новый тип веб-службу, предоставляющую конечную точку диспетчера ресурсов Azure, нет необходимости tooadd hello второй **нестандартных** конечной точки. Hello **updateResourceEndpoint** в hello связанной службы имеет формат hello: 

```
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resource-group-name}/providers/Microsoft.MachineLearning/webServices/{web-service-name}?api-version=2016-05-01-preview. 
```

Вы можете получить значения для владельцев месте в URL-АДРЕСЕ hello при запросе hello веб-службы на hello [веб-портал Azure машины обучения службы](https://services.azureml.net/). Hello новый тип конечной точки обновления ресурса требуется маркер AAD (Azure Active Directory). Укажите **servicePrincipalId** и **servicePrincipalKey** в связанной службе AzureML. В разделе [как участника службы и назначьте разрешения toomanage ресурсов Azure toocreate](../azure-resource-manager/resource-group-create-service-principal-portal.md). Ниже приведен пример определения связанной службы AzureML. 

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

Hello следующий сценарий более подробные сведения. Он представляет пример повторного обучения и обновления моделей машинного обучения Azure из конвейера фабрики данных Azure.

## <a name="scenario-retraining-and-updating-an-azure-ml-model"></a>Сценарий: повторное обучение и обновление модели машинного обучения Azure
Этот раздел содержит пример конвейера, который использует hello **операции при выполнении пакета Azure ML** tooretrain модели. конвейер Hello также использует hello **действия ресурса обновления машинного Обучения Azure** tooupdate модели hello в hello оценки веб-службы. Кроме того, раздел Hello предоставляет hello фрагменты JSON для всех связанных службах, наборы данных и конвейер в примере hello.

Вот представление диаграммы hello конвейера образец hello. Как видите, hello действие выполнения пакета машинного Обучения Azure принимает входные данные обучения hello и создает выходные данные обучения (файл iLearner). Hello действия ресурса обновления машинного Обучения Azure принимает выходные данные обучения и обновления hello модели в hello оценки конечной веб-службы. Hello действия ресурса обновления не создает никаких выходных данных. Hello placeholderBlob является просто пустой результирующий набор данных, которые требуются для конвейера hello toorun служба фабрики данных Azure hello.

![схема конвейера](./media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

### <a name="azure-blob-storage-linked-service"></a>Связанная служба хранилища BLOB-объектов Azure
Hello хранилища Azure содержит hello следующие данные:

* Данные для обучения. Hello входные данные для hello Azure ML обучения веб-службы.  
* Файл iLearner. Здравствуйте, выходные данные hello Azure ML обучения веб-службы. Этот файл также является hello ввода toohello действия ресурса обновления.  

Вот определение JSON образец hello hello связанной службы.

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

### <a name="training-input-dataset"></a>Входной набор данных для обучения:
Hello следующий набор данных представляет hello входной обучающие данные для hello Azure ML обучения веб-службы. Этот набор данных в качестве входного значения Hello Azure ML Пакетное выполнение действия.

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

### <a name="training-output-dataset"></a>Выходной набор данных для обучения:
Hello следующий набор данных представляет hello выходной файл iLearner из hello Azure ML обучения веб-службы. Действие выполнения пакета машинного Обучения Azure Hello создает этот набор данных. Этот набор данных также является hello ввода toohello действия ресурса обновления машинного Обучения Azure.

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

### <a name="linked-service-for-azure-ml-training-endpoint"></a>Связанная служба для конечной точки машинного обучения Azure
Привет, следующий фрагмент JSON определяет Azure связанной службы машинного обучения, указывающий конечную точку по умолчанию toohello hello обучения веб-службы.

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

В **Azure ML Studio**, hello следующие параметры tooget для **mlEndpoint** и **apiKey**:

1. Нажмите кнопку **веб-службы** hello левом меню.
2. Нажмите кнопку hello **обучения веб-службы** в списке hello веб-служб.
3. Щелкните "Копировать" рядом слишком**ключ API** текстовое поле. Вставьте ключ hello в буфер обмена hello в редактор JSON фабрики данных hello.
4. В hello **Azure ML studio**, нажмите кнопку **ПАКЕТНОЕ выполнение** ссылку.
5. Копировать hello **URI запроса** из hello **запроса** раздела и вставьте его в редактор JSON фабрики данных hello.   

### <a name="linked-service-for-azure-ml-updatable-scoring-endpoint"></a>Связанная служба для обновляемой конечной точки оценки машинного обучения Azure
Привет, следующий фрагмент JSON определяет Azure связанной службы машинного обучения, указывающий toohello нестандартных обновляемых конечную точку hello оценки веб-службы.  

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

### <a name="placeholder-output-dataset"></a>Заполнитель выходного набора данных
Hello действия ресурса обновления машинного Обучения Azure не создает никаких выходных данных. Однако фабрики данных Azure требует toodrive hello выходного набора данных расписания конвейера. Поэтому в этом примере используется фиктивный набор данных (заполнитель набора данных).  

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

### <a name="pipeline"></a>Конвейер
Hello конвейера содержит два действия: **AzureMLBatchExecution** и **AzureMLUpdateResource**. Hello операции при выполнении пакета машинного Обучения Azure принимает hello обучающие данные в качестве входных данных и создает файл iLearner, как выходные данные. Действие Hello вызывает hello обучения веб-службы (эксперимента обучения в виде веб-службы) с входными данными hello обучающих данных и получает от веб-службы hello файл ilearner hello. Hello placeholderBlob является просто пустой результирующий набор данных, которые требуются для конвейера hello toorun служба фабрики данных Azure hello.

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
