---
title: "Использование шаблонов Azure Resource Manager для создания и настройки рабочей области Log Analytics | Документация Майкрософт"
description: "Шаблоны Azure Resource Manager вы можете применить для создания и настройки рабочих областей Log Analytics."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: jochan
editor: 
ms.assetid: d21ca1b0-847d-4716-bb30-2a8c02a606aa
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: json
ms.topic: article
ms.date: 06/01/2017
ms.author: richrund
ms.openlocfilehash: 505b741d14c594b22108298466c646bf723ce2d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-log-analytics-using-azure-resource-manager-templates"></a><span data-ttu-id="f2068-103">Управление Log Analytics с помощью шаблонов Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f2068-103">Manage Log Analytics using Azure Resource Manager templates</span></span>
<span data-ttu-id="f2068-104">[Шаблоны Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) можно использовать, чтобы создавать и настраивать рабочие области Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="f2068-104">You can use [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) to create and configure Log Analytics workspaces.</span></span> <span data-ttu-id="f2068-105">Примеры задач, которые можно выполнять с помощью шаблонов.</span><span class="sxs-lookup"><span data-stu-id="f2068-105">Examples of the tasks you can perform with templates include:</span></span>

* <span data-ttu-id="f2068-106">Создание рабочей области</span><span class="sxs-lookup"><span data-stu-id="f2068-106">Create a workspace</span></span>
* <span data-ttu-id="f2068-107">Добавление решения</span><span class="sxs-lookup"><span data-stu-id="f2068-107">Add a solution</span></span>
* <span data-ttu-id="f2068-108">Создание сохраненных поисковых запросов</span><span class="sxs-lookup"><span data-stu-id="f2068-108">Create saved searches</span></span>
* <span data-ttu-id="f2068-109">Создание группы компьютеров</span><span class="sxs-lookup"><span data-stu-id="f2068-109">Create a computer group</span></span>
* <span data-ttu-id="f2068-110">Включение сбора журналов IIS с компьютеров, на которых установлен агент Windows</span><span class="sxs-lookup"><span data-stu-id="f2068-110">Enable collection of IIS logs from computers with the Windows agent installed</span></span>
* <span data-ttu-id="f2068-111">Сбор счетчиков производительности с компьютеров под управлением Linux и Windows</span><span class="sxs-lookup"><span data-stu-id="f2068-111">Collect performance counters from Linux and Windows computers</span></span>
* <span data-ttu-id="f2068-112">Сбор событий из системного журнала с компьютеров Linux</span><span class="sxs-lookup"><span data-stu-id="f2068-112">Collect events from syslog on Linux computers</span></span> 
* <span data-ttu-id="f2068-113">Сбор событий из журналов событий Windows</span><span class="sxs-lookup"><span data-stu-id="f2068-113">Collect events from Windows event logs</span></span>
* <span data-ttu-id="f2068-114">Сбор пользовательских журналов событий</span><span class="sxs-lookup"><span data-stu-id="f2068-114">Collect custom event logs</span></span>
* <span data-ttu-id="f2068-115">Добавление агента Log Analytics в виртуальную машину Azure</span><span class="sxs-lookup"><span data-stu-id="f2068-115">Add the log analytics agent to an Azure virtual machine</span></span>
* <span data-ttu-id="f2068-116">Настройка Log Analytics для индексирования данных, собранных системой диагностики Azure</span><span class="sxs-lookup"><span data-stu-id="f2068-116">Configure log analytics to index data collected using Azure diagnostics</span></span>

<span data-ttu-id="f2068-117">Эта статья содержит примеры кода, иллюстрирующие некоторые конфигурации, которые можно выполнить с помощью шаблонов.</span><span class="sxs-lookup"><span data-stu-id="f2068-117">This article provides a template samples that illustrate some of the configuration that you can perform from templates.</span></span>

## <a name="create-and-configure-a-log-analytics-workspace"></a><span data-ttu-id="f2068-118">Создание и настройка рабочей области Log Analytics</span><span class="sxs-lookup"><span data-stu-id="f2068-118">Create and configure a Log Analytics Workspace</span></span>
<span data-ttu-id="f2068-119">Этот пример шаблона иллюстрирует следующие задачи.</span><span class="sxs-lookup"><span data-stu-id="f2068-119">The following template sample illustrates how to:</span></span>

1. <span data-ttu-id="f2068-120">Создание рабочей области, а также настройка хранения данных.</span><span class="sxs-lookup"><span data-stu-id="f2068-120">Create a workspace, including setting data retention</span></span>
2. <span data-ttu-id="f2068-121">Добавление решений в рабочую область</span><span class="sxs-lookup"><span data-stu-id="f2068-121">Add solutions to the workspace</span></span>
3. <span data-ttu-id="f2068-122">Создание сохраненных поисковых запросов</span><span class="sxs-lookup"><span data-stu-id="f2068-122">Create saved searches</span></span>
4. <span data-ttu-id="f2068-123">Создание группы компьютеров</span><span class="sxs-lookup"><span data-stu-id="f2068-123">Create a computer group</span></span>
5. <span data-ttu-id="f2068-124">Включение сбора журналов IIS с компьютеров, на которых установлен агент Windows</span><span class="sxs-lookup"><span data-stu-id="f2068-124">Enable collection of IIS logs from computers with the Windows agent installed</span></span>
6. <span data-ttu-id="f2068-125">Сбор счетчиков производительности логического диска с компьютеров под управлением Linux ("Процент использования индексных дескрипторов"; "Свободно мегабайт"; "Процент используемого места"; "Количество обращений к диску (в секунду)"; "Количество обращений чтения или записи (в секунду))"</span><span class="sxs-lookup"><span data-stu-id="f2068-125">Collect Logical Disk perf counters from Linux computers (% Used Inodes; Free Megabytes; % Used Space; Disk Transfers/sec; Disk Reads/sec; Disk Writes/sec)</span></span>
7. <span data-ttu-id="f2068-126">Сбор событий из системного журнала с компьютеров Linux</span><span class="sxs-lookup"><span data-stu-id="f2068-126">Collect syslog events from Linux computers</span></span>
8. <span data-ttu-id="f2068-127">Сбор событий (ошибок и предупреждений) из журнала событий приложений с компьютеров Windows</span><span class="sxs-lookup"><span data-stu-id="f2068-127">Collect Error and Warning events from the Application Event Log from Windows computers</span></span>
9. <span data-ttu-id="f2068-128">Сбор данных счетчика производительности "Доступный объем памяти" (в МБ) с компьютеров Windows</span><span class="sxs-lookup"><span data-stu-id="f2068-128">Collect Memory Available Mbytes performance counter from Windows computers</span></span>
10. <span data-ttu-id="f2068-129">Сбор пользовательского журнала</span><span class="sxs-lookup"><span data-stu-id="f2068-129">Collect a custom log</span></span> 
11. <span data-ttu-id="f2068-130">Сбор журналов IIS и журналов событий Windows, которые система диагностики Azure записывает в учетную запись хранилища</span><span class="sxs-lookup"><span data-stu-id="f2068-130">Collect IIS logs and Windows Event logs written by Azure diagnostics to a storage account</span></span>

```
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "workspaceName": {
      "type": "string",
      "metadata": {
        "description": "workspaceName"
      }
    },
    "serviceTier": {
      "type": "string",
      "allowedValues": [
        "Free",
        "Standalone",
        "PerNode"
      ],
      "metadata": {
        "description": "Service Tier: Free, Standalone, or PerNode"
    }
      },
    "dataRetention": {
      "type": "int",
      "defaultValue": 30,
      "minValue": 7,
      "maxValue": 730,
      "metadata": {
        "description": "Number of days of retention. Free plans can only have 7 days, Standalone and OMS plans include 30 days for free"
      }
    },
    "location": {
      "type": "string",
      "allowedValues": [
        "East US",
        "West Europe",
        "Southeast Asia",
        "Australia Southeast"
      ]
    },
    "applicationDiagnosticsStorageAccountName": {
        "type": "string",
        "metadata": {
          "description": "Name of the storage account with Azure diagnostics output"
        }
    },
    "applicationDiagnosticsStorageAccountResourceGroup": {
        "type": "string",
        "metadata": {
          "description": "The resource group name containing the storage account with Azure diagnostics output"
        }
    }
  },
  "variables": {
    "Updates": {
      "Name": "[Concat('Updates', '(', parameters('workspaceName'), ')')]",
      "GalleryName": "Updates"
    },
    "AntiMalware": {
      "Name": "[concat('AntiMalware', '(', parameters('workspaceName'), ')')]",
      "GalleryName": "AntiMalware"
    },
    "SQLAssessment": {
      "Name": "[Concat('SQLAssessment', '(', parameters('workspaceName'), ')')]",
      "GalleryName": "SQLAssessment"
    },
    "diagnosticsStorageAccount": "[resourceId(parameters('applicationDiagnosticsStorageAccountResourceGroup'), 'Microsoft.Storage/storageAccounts', parameters('applicationDiagnosticsStorageAccountName'))]"
  },
  "resources": [
    {
      "apiVersion": "2015-11-01-preview",
      "type": "Microsoft.OperationalInsights/workspaces",
      "name": "[parameters('workspaceName')]",
      "location": "[parameters('location')]",
      "properties": {
        "sku": {
          "Name": "[parameters('serviceTier')]"
        },
    "retention": "[parameters('dataRetention')]"
      },
      "resources": [
        {
          "apiVersion": "2015-11-01-preview",
          "name": "VMSS Queries2",
          "type": "savedSearches",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "properties": {
            "Category": "VMSS",
            "ETag": "*",
            "DisplayName": "VMSS Instance Count",
            "Query": "Type:Event Source=ServiceFabricNodeBootstrapAgent | dedup Computer | measure count () by Computer",
            "Version": 1
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleWindowsEvent1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "WindowsEvent",
          "properties": {
            "eventLogName": "Application",
            "eventTypes": [
              {
                "eventType": "Error"
              },
              {
                "eventType": "Warning"
              }
            ]
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleWindowsPerfCounter1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "WindowsPerformanceCounter",
          "properties": {
            "objectName": "Memory",
            "instanceName": "*",
            "intervalSeconds": 10,
            "counterName": "Available MBytes"
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleIISLog1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "IISLogs",
          "properties": {
            "state": "OnPremiseEnabled"
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleSyslog1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "LinuxSyslog",
          "properties": {
            "syslogName": "kern",
            "syslogSeverities": [
              {
                "severity": "emerg"
              },
              {
                "severity": "alert"
              },
              {
                "severity": "crit"
              },
              {
                "severity": "err"
              },
              {
                "severity": "warning"
              }
            ]
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleSyslogCollection1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "LinuxSyslogCollection",
          "properties": {
            "state": "Enabled"
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleLinuxPerf1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "LinuxPerformanceObject",
          "properties": {
            "performanceCounters": [
              {
                "counterName": "% Used Inodes"
              },
              {
                "counterName": "Free Megabytes"
              },
              {
                "counterName": "% Used Space"
              },
              {
                "counterName": "Disk Transfers/sec"
              },
              {
                "counterName": "Disk Reads/sec"
              },
              {
                "counterName": "Disk Writes/sec"
              }
            ],
            "objectName": "Logical Disk",
            "instanceName": "*",
            "intervalSeconds": 10
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleLinuxPerfCollection1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "LinuxPerformanceCollection",
          "properties": {
            "state": "Enabled"
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleCustomLog1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "CustomLog",
          "properties": {
            "customLogName": "sampleCustomLog1",
            "description": "test custom log datasources",
            "inputs": [
              {
                "location": {
                  "fileSystemLocations": {
                    "windowsFileTypeLogPaths": [ "e:\\iis5\\*.log" ],
                    "linuxFileTypeLogPaths": [ "/var/logs" ]
                  }
                },
                "recordDelimiter": {
                  "regexDelimiter": {
                    "pattern": "\\n",
                    "matchIndex": 0,
                    "matchIndexSpecified": true,
                    "numberedGroup": null
                  }
                }
              }
            ],
            "extractions": [
              {
                "extractionName": "TimeGenerated",
                "extractionType": "DateTime",
                "extractionProperties": {
                  "dateTimeExtraction": {
                    "regex": null,
                    "joinStringRegex": null
                  }
                }
              }
            ]
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleCustomLogCollection1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "CustomLogCollection",
          "properties": {
            "state": "LinuxLogsEnabled"
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "name": "[concat(parameters('applicationDiagnosticsStorageAccountName'),parameters('workspaceName'))]",
          "type": "storageinsightconfigs",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "properties": {
            "containers": [ 
              "wad-iis-logfiles" 
            ],
            "tables": [
              "WADWindowsEventLogsTable"
            ],
            "storageAccount": {
              "id": "[variables('diagnosticsStorageAccount')]",
              "key": "[listKeys(variables('diagnosticsStorageAccount'),'2015-06-15').key1]"
            }
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "location": "[parameters('location')]",
          "name": "[variables('Updates').Name]",
          "type": "Microsoft.OperationsManagement/solutions",
          "id": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationsManagement/solutions/', variables('Updates').Name)]",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "properties": {
            "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          },
          "plan": {
            "name": "[variables('Updates').Name]",
            "publisher": "Microsoft",
            "product": "[Concat('OMSGallery/', variables('Updates').GalleryName)]",
            "promotionCode": ""
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "location": "[parameters('location')]",
          "name": "[variables('AntiMalware').Name]",
          "type": "Microsoft.OperationsManagement/solutions",
          "id": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationsManagement/solutions/', variables('AntiMalware').Name)]",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "properties": {
            "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          },
          "plan": {
            "name": "[variables('AntiMalware').Name]",
            "publisher": "Microsoft",
            "product": "[Concat('OMSGallery/', variables('AntiMalware').GalleryName)]",
            "promotionCode": ""
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "location": "[parameters('location')]",
          "name": "[variables('SQLAssessment').Name]",
          "type": "Microsoft.OperationsManagement/solutions",
          "id": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationsManagement/solutions/', variables('SQLAssessment').Name)]",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "properties": {
            "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          },
          "plan": {
            "name": "[variables('SQLAssessment').Name]",
            "publisher": "Microsoft",
            "product": "[Concat('OMSGallery/', variables('SQLAssessment').GalleryName)]",
            "promotionCode": ""
          }
        }
      ]
    }
  ],
  "outputs": {
    "workspaceOutput": {
      "value": "[reference(concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName')), '2015-11-01-preview')]",
      "type": "object"
    }
  }
}

```
### <a name="deploying-the-sample-template"></a><span data-ttu-id="f2068-131">Развертывание примера шаблона</span><span class="sxs-lookup"><span data-stu-id="f2068-131">Deploying the sample template</span></span>
<span data-ttu-id="f2068-132">Чтобы развернуть этот шаблон, запустите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f2068-132">To deploy the sample template:</span></span>

1. <span data-ttu-id="f2068-133">Сохраните прилагаемый пример в файл, например с именем `azuredeploy.json`</span><span class="sxs-lookup"><span data-stu-id="f2068-133">Save the attached sample in a file, for example `azuredeploy.json`</span></span> 
2. <span data-ttu-id="f2068-134">Измените шаблон так, чтобы получить нужную конфигурацию</span><span class="sxs-lookup"><span data-stu-id="f2068-134">Edit the template to have the configuration you want</span></span>
3. <span data-ttu-id="f2068-135">Разверните итоговый шаблон с помощью PowerShell или командной строки</span><span class="sxs-lookup"><span data-stu-id="f2068-135">Use PowerShell or the command line to deploy the template</span></span>

#### <a name="powershell"></a><span data-ttu-id="f2068-136">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f2068-136">PowerShell</span></span>
`New-AzureRmResourceGroupDeployment -Name <deployment-name> -ResourceGroupName <resource-group-name> -TemplateFile azuredeploy.json`

#### <a name="command-line"></a><span data-ttu-id="f2068-137">Команда</span><span class="sxs-lookup"><span data-stu-id="f2068-137">Command line</span></span>
```
azure config mode arm
azure group deployment create <my-resource-group> <my-deployment-name> --TemplateFile azuredeploy.json
```


## <a name="example-resource-manager-templates"></a><span data-ttu-id="f2068-138">Примеры шаблонов Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f2068-138">Example Resource Manager templates</span></span>
<span data-ttu-id="f2068-139">Коллекция шаблонов Azure позволяет быстро начать работу, применяя предложенные шаблоны для Log Analytics, в том числе перечисленные ниже.</span><span class="sxs-lookup"><span data-stu-id="f2068-139">The Azure quickstart template gallery includes several templates for Log Analytics, including:</span></span>

* [<span data-ttu-id="f2068-140">Развертывание виртуальной машины под управлением Windows с расширением Log Analytics</span><span class="sxs-lookup"><span data-stu-id="f2068-140">Deploy a virtual machine running Windows with the Log Analytics VM extension</span></span>](https://azure.microsoft.com/documentation/templates/201-oms-extension-windows-vm/)
* [<span data-ttu-id="f2068-141">Развертывание виртуальной машины под управлением Linux с расширением Log Analytics</span><span class="sxs-lookup"><span data-stu-id="f2068-141">Deploy a virtual machine running Linux with the Log Analytics VM extension</span></span>](https://azure.microsoft.com/documentation/templates/201-oms-extension-ubuntu-vm/)
* [<span data-ttu-id="f2068-142">Мониторинг Azure Site Recovery с использованием существующей рабочей области Log Analytics</span><span class="sxs-lookup"><span data-stu-id="f2068-142">Monitor Azure Site Recovery using an existing Log Analytics workspace</span></span>](https://azure.microsoft.com/documentation/templates/asr-oms-monitoring/)
* [<span data-ttu-id="f2068-143">Мониторинг веб-приложений Azure с использованием существующей рабочей области Log Analytics</span><span class="sxs-lookup"><span data-stu-id="f2068-143">Monitor Azure Web Apps using an existing Log Analytics workspace</span></span>](https://azure.microsoft.com/documentation/templates/101-webappazure-oms-monitoring/)
* [<span data-ttu-id="f2068-144">Мониторинг SQL Azure с использованием существующей рабочей области Log Analytics</span><span class="sxs-lookup"><span data-stu-id="f2068-144">Monitor SQL Azure using an existing Log Analytics workspace</span></span>](https://azure.microsoft.com/documentation/templates/101-sqlazure-oms-monitoring/)
* [<span data-ttu-id="f2068-145">Развертывание кластера Service Fabric и его мониторинг с помощью существующей рабочей области Log Analytics</span><span class="sxs-lookup"><span data-stu-id="f2068-145">Deploy a Service Fabric cluster and monitor it with an existing Log Analytics workspace</span></span>](https://azure.microsoft.com/documentation/templates/service-fabric-oms/)
* [<span data-ttu-id="f2068-146">Развертывание кластера Service Fabric и создание рабочей области Log Analytics для его мониторинга</span><span class="sxs-lookup"><span data-stu-id="f2068-146">Deploy a Service Fabric cluster and create a Log Analytics workspace to monitor it</span></span>](https://azure.microsoft.com/documentation/templates/service-fabric-vmss-oms/)

## <a name="next-steps"></a><span data-ttu-id="f2068-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f2068-147">Next steps</span></span>
* [<span data-ttu-id="f2068-148">Развертывание агентов на виртуальных машинах Azure с помощью шаблонов Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f2068-148">Deploy agents into Azure VMs using Resource Manager templates</span></span>](log-analytics-azure-vm-extension.md)

