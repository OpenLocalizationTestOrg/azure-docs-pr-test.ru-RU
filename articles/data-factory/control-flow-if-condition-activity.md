---
title: "Действие условия If в фабрике данных Azure | Документация Майкрософт"
description: "Действие условия If позволяет управлять потоком обработки на основе условия."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2018
ms.author: shlo
ms.openlocfilehash: 016cd8ac8dc4b65117bf8c07e8d8d4c74c8d9623
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/23/2018
---
# <a name="if-condition-activity-in-azure-data-factory"></a>Действие условия If в фабрике данных Azure
Действие условия If предоставляет те же функциональные возможности, что и инструкция if в языках программирования. Оно определяет набор действий, если условие принимает значение `true`, и другой набор действий, если условие принимает значение `false`. 


> [!NOTE]
> Эта статья относится к версии 2 фабрики данных, которая в настоящее время доступна в предварительной версии. Если вы используете общедоступную версию 1 службы фабрики данных, см. статью [Introduction to Azure Data Factory](v1/data-factory-introduction.md) (Введение в фабрику данных Azure).

## <a name="syntax"></a>Синтаксис

```json

{
    "name": "<Name of the activity>",
    "type": "IfCondition",
    "typeProperties": {
            "expression": {
            "value": "<expression that evaluates to true or false>",
            "type": "Expression"
            },

            "ifTrueActivities": [
            {
                "<Activity 1 definition>"
            },
            {
                "<Activity 2 definition>"
            },
            {
                "<Activity N definition>"
            }
        ],

        "ifFalseActivities": [
            {
                "<Activity 1 definition>"
            },
            {
                "<Activity 2 definition>"
            },
            {
                "<Activity N definition>"
            }
            ]
    }
}
```

## <a name="type-properties"></a>Свойства типа

Свойство | ОПИСАНИЕ | Допустимые значения | Обязательно
-------- | ----------- | -------------- | --------
name | Имя действия условия If. | Строка | Yes
Тип | Для этого свойства необходимо задать значение **IfCondition**. | Строка | Yes
expression | Выражение, для которого возвращается значение true или false. | Yes
ifTrueActivities | Набор действий, которые выполняются, если выражение получает значение `true`. | Yes
ifFalseActivities | Набор действий, которые выполняются, если выражение получает значение `false`. | Yes

## <a name="example"></a>Пример
В этом примере конвейер копирует данные из входной папки в выходную папку. Выходная папка определяется значением параметра конвейера routeSelection. Если значение routeSelection — true, данные копируются в outputPath1, а если значение routeSelection — false, данные копируются в outputPath2. 

> [!NOTE]
> Этот раздел содержит определения JSON и примеры команд PowerShell для выполнения действий в конвейере. Пошаговые инструкции по созданию конвейера фабрики данных с помощью Azure PowerShell и определений JSON см. в [этом руководстве](quickstart-create-data-factory-powershell.md).

### <a name="pipeline-with-if-condition-activity-adfv2quickstartpipelinejson"></a>Конвейер с действием условия If (Adfv2QuickStartPipeline.json)

```json
{
    "name": "Adfv2QuickStartPipeline",
    "properties": {
        "activities": [
            {
                "name": "MyIfCondition",
                "type": "IfCondition",
                "typeProperties": {
                    "expression":  {
                        "value":  "@bool(pipeline().parameters.routeSelection)", 
                        "type": "Expression"
                     },
                                           
                    "ifTrueActivities": [
                        {
                            "name": "CopyFromBlobToBlob1",
                            "type": "Copy",
                            "inputs": [
                                {
                                    "referenceName": "BlobDataset",
                                    "parameters": {
                                        "path": "@pipeline().parameters.inputPath"
                                    },
                                    "type": "DatasetReference"
                                }
                            ],
                            "outputs": [
                                {
                                    "referenceName": "BlobDataset",
                                    "parameters": {
                                        "path": "@pipeline().parameters.outputPath1"
                                    },
                                    "type": "DatasetReference"
                                }
                            ],
                            "typeProperties": {
                                "source": {
                                    "type": "BlobSource"
                                },
                                "sink": {
                                    "type": "BlobSink"
                                }
                            }
                        }                                   
                    ],
                    "ifFalseActivities": [
                        {
                            "name": "CopyFromBlobToBlob2",
                            "type": "Copy",
                            "inputs": [
                                {
                                    "referenceName": "BlobDataset",
                                    "parameters": {
                                        "path": "@pipeline().parameters.inputPath"
                                    },
                                    "type": "DatasetReference"
                                }
                            ],
                            "outputs": [
                                {
                                    "referenceName": "BlobDataset",
                                    "parameters": {
                                        "path": "@pipeline().parameters.outputPath2"
                                    },
                                    "type": "DatasetReference"
                                }
                            ],
                            "typeProperties": {
                                "source": {
                                    "type": "BlobSource"
                                },
                                "sink": {
                                    "type": "BlobSink"
                                }
                            }
                        }
                    ]                    
                }
            }
        ],
        "parameters": {
            "inputPath": {
                "type": "String"
            },
            "outputPath1": {
                "type": "String"
            },
            "outputPath2": {
                "type": "String"
            },
            "routeSelection": {
                "type": "String"
            }                        
        }
    }
}
```

Еще один пример выражения: 

```json
"expression":  {
    "value":  "@pipeline().parameters.routeSelection == 1", 
    "type": "Expression"
}
```


### <a name="azure-storage-linked-service-azurestoragelinkedservicejson"></a>Связанная служба хранилища Azure (AzureStorageLinkedService.json)

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": {
                "value": "DefaultEndpointsProtocol=https;AccountName=<Azure Storage account name>;AccountKey=<Azure Storage account key>",
                "type": "SecureString"
            }
        }
    }
}
```

### <a name="parameterized-azure-blob-dataset-blobdatasetjson"></a>Параметризованный набор данных большого двоичного объекта Azure (BlobDataset.json)
Конвейер устанавливает для параметра **folderPath** значение **outputPath1** или **outputPath2**. 

```json
{
    "name": "BlobDataset",
    "properties": {
        "type": "AzureBlob",
        "typeProperties": {
            "folderPath": {
                "value": "@{dataset().path}",
                "type": "Expression"
            }
        },
        "linkedServiceName": {
            "referenceName": "AzureStorageLinkedService",
            "type": "LinkedServiceReference"
        },
        "parameters": {
            "path": {
                "type": "String"
            }
        }
    }
}
```

### <a name="pipeline-parameter-json-pipelineparametersjson"></a>JSON-файл с параметрами конвейера (PipelineParameters.json)

```json
{
    "inputPath": "adftutorial/input",
    "outputPath1": "adftutorial/outputIf",
    "outputPath2": "adftutorial/outputElse",
    "routeSelection": "false"
}
```

### <a name="powershell-commands"></a>Команды PowerShell
Эти команды предполагают, что вы сохранили файлы JSON в папку C:\ADF. 

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription "<Your subscription name>"

$resourceGroupName = "<Resource Group Name>"
$dataFactoryName = "<Data Factory Name. Must be globally unique>";
Remove-AzureRmDataFactoryV2 $dataFactoryName -ResourceGroupName $resourceGroupName -force


Set-AzureRmDataFactoryV2 -ResourceGroupName $resourceGroupName -Location "East US" -Name $dataFactoryName
Set-AzureRmDataFactoryV2LinkedService -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "AzureStorageLinkedService" -DefinitionFile "C:\ADF\AzureStorageLinkedService.json"
Set-AzureRmDataFactoryV2Dataset -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "BlobDataset" -DefinitionFile "C:\ADF\BlobDataset.json"
Set-AzureRmDataFactoryV2Pipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -Name "Adfv2QuickStartPipeline" -DefinitionFile "C:\ADF\Adfv2QuickStartPipeline.json"
$runId = Invoke-AzureRmDataFactoryV2Pipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -PipelineName "Adfv2QuickStartPipeline" -ParameterFile C:\ADF\PipelineParameters.json
while ($True) {
    $run = Get-AzureRmDataFactoryV2PipelineRun -ResourceGroupName $resourceGroupName -DataFactoryName $DataFactoryName -PipelineRunId $runId

    if ($run) {
        if ($run.Status -ne 'InProgress') {
            Write-Host "Pipeline run finished. The status is: " $run.Status -foregroundcolor "Yellow"
            $run
            break
        }
        Write-Host  "Pipeline is running...status: InProgress" -foregroundcolor "Yellow"
    }

    Start-Sleep -Seconds 30
}
Write-Host "Activity run details:" -foregroundcolor "Yellow"
$result = Get-AzureRmDataFactoryV2ActivityRun -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -PipelineRunId $runId -RunStartedAfter (Get-Date).AddMinutes(-30) -RunStartedBefore (Get-Date).AddMinutes(30)
$result

Write-Host "Activity 'Output' section:" -foregroundcolor "Yellow"
$result.Output -join "`r`n"

Write-Host "\nActivity 'Error' section:" -foregroundcolor "Yellow"
$result.Error -join "`r`n"
```

## <a name="next-steps"></a>Дополнительная информация
Ознакомьтесь с другими действиями потока управления, которые поддерживаются фабрикой данных: 

- [Действие выполнения конвейера](control-flow-execute-pipeline-activity.md)
- [Действие ForEach](control-flow-for-each-activity.md)
- [Действие получения метаданных](control-flow-get-metadata-activity.md)
- [Действие поиска](control-flow-lookup-activity.md)
- [Веб-действие](control-flow-web-activity.md)