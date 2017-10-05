---
title: "Использование автоматического масштабирования Azure с метриками гостевой виртуальной машины в шаблоне масштабируемого набора Linux | Документация Майкрософт"
description: "Узнайте, как выполнять автоматическое масштабирование, используя метрики гостевой виртуальной машины в шаблоне масштабируемого набора виртуальных машин Linux"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: na
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: negat
ms.openlocfilehash: ac0bbb4dbfccca3f3fc31526aeff11afe55d44be
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="autoscale-using-guest-metrics-in-a-linux-scale-set-template"></a><span data-ttu-id="4a9e2-103">Автоматическое масштабирование с помощью метрик гостевой виртуальной машины в шаблоне масштабируемого набора Linux</span><span class="sxs-lookup"><span data-stu-id="4a9e2-103">Autoscale using guest metrics in a Linux scale set template</span></span>

<span data-ttu-id="4a9e2-104">Имеется два типа метрик в Azure, которые собираются с виртуальных машин и масштабируемых наборов: некоторые собирают с виртуальной машины узла, а другие — с гостевой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="4a9e2-104">There are two types of metrics in Azure that are gathered from VMs and scale sets: some come from the host VM and others come from the guest VM.</span></span> <span data-ttu-id="4a9e2-105">Метрики узла не требуют дополнительной настройки, так как они собираются с виртуальной машины узла. В то время как для метрик гостевой виртуальной машины требуется установить [расширение системы диагностики Microsoft Azure](../virtual-machines/windows/extensions-diagnostics-template.md) или [расширение системы диагностики Azure для Linux](../virtual-machines/linux/diagnostic-extension.md) на гостевой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="4a9e2-105">Host metrics do not require additional setup because they are collected by the host VM, whereas guest metrics require us to install the [Windows Azure Diagnostics extension](../virtual-machines/windows/extensions-diagnostics-template.md) or the [Linux Azure Diagnostics extension](../virtual-machines/linux/diagnostic-extension.md) in the guest VM.</span></span> <span data-ttu-id="4a9e2-106">Одна из основных причин использования метрик гостевой виртуальной машины вместо метрик узла заключается в том, что метрики гостевой виртуальной машины предоставляют больший набор показателей, чем метрики узла.</span><span class="sxs-lookup"><span data-stu-id="4a9e2-106">One common reason to use guest metrics instead of host metrics is that guest metrics provide a larger selection of metrics than host metrics.</span></span> <span data-ttu-id="4a9e2-107">Один из таких примеров — это метрики потребления памяти, которые доступны только через метрики гостевой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="4a9e2-107">One such example is memory-consumption metrics, which are only available via guest metrics.</span></span> <span data-ttu-id="4a9e2-108">Поддерживаемые метрики узла перечислены [здесь](../monitoring-and-diagnostics/monitoring-supported-metrics.md), а часто используемые метрики гостевой виртуальной машины — [здесь](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="4a9e2-108">The supported host metrics are listed [here](../monitoring-and-diagnostics/monitoring-supported-metrics.md), and commonly used guest metrics are listed [here](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span></span> <span data-ttu-id="4a9e2-109">В этой статье показано, как изменить [минимальный приемлемый шаблон масштабируемого набора](./virtual-machine-scale-sets-mvss-start.md) для использования правил автоматического масштабирования на основе метрик гостевой виртуальной машины для масштабируемых наборов Linux.</span><span class="sxs-lookup"><span data-stu-id="4a9e2-109">This article shows how to modify the [minimum viable scale set template](./virtual-machine-scale-sets-mvss-start.md) to use autoscale rules based on guest metrics for Linux scale sets.</span></span>

## <a name="change-the-template-definition"></a><span data-ttu-id="4a9e2-110">Изменение определения шаблона</span><span class="sxs-lookup"><span data-stu-id="4a9e2-110">Change the template definition</span></span>

<span data-ttu-id="4a9e2-111">Шаблон минимального приемлемого масштабируемого набора доступен [здесь](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), а шаблон для развертывания масштабируемого набора Linux с помощью автомасштабирования на основе гостевой системы доступен [здесь](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="4a9e2-111">Our minimum viable scale set template can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), and our template for deploying the Linux scale set with guest-based autoscale can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json).</span></span> <span data-ttu-id="4a9e2-112">Давайте рассмотрим DIFF-файл, с помощью которого можно постепенно создать этот шаблон (`git diff minimum-viable-scale-set existing-vnet`).</span><span class="sxs-lookup"><span data-stu-id="4a9e2-112">Let's examine the diff used to create this template (`git diff minimum-viable-scale-set existing-vnet`) piece by piece:</span></span>

<span data-ttu-id="4a9e2-113">Сначала добавим параметры для `storageAccountName` и `storageAccountSasToken`.</span><span class="sxs-lookup"><span data-stu-id="4a9e2-113">First, we add parameters for `storageAccountName` and `storageAccountSasToken`.</span></span> <span data-ttu-id="4a9e2-114">Агент диагностики будет хранить данные метрик в [таблице](../cosmos-db/table-storage-how-to-use-dotnet.md) в этой учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="4a9e2-114">The diagnostics agent will store metric data in a [table](../cosmos-db/table-storage-how-to-use-dotnet.md) in this storage account.</span></span> <span data-ttu-id="4a9e2-115">Начиная с агента диагностики Linux версии 3.0 использование ключа доступа к хранилищу больше не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="4a9e2-115">As of the Linux Diagnostics Agent version 3.0, using a storage access key is no longer supported.</span></span> <span data-ttu-id="4a9e2-116">Необходимо использовать [маркер SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="4a9e2-116">We must use a [SAS Token](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span></span>

```diff
     },
     "adminPassword": {
       "type": "securestring"
+    },
+    "storageAccountName": {
+      "type": "string"
+    },
+    "storageAccountSasToken": {
+      "type": "securestring"
     }
   },
```

<span data-ttu-id="4a9e2-117">Затем мы изменим масштабируемый набор `extensionProfile`, чтобы включить расширение диагностики.</span><span class="sxs-lookup"><span data-stu-id="4a9e2-117">Next, we modify the scale set `extensionProfile` to include the diagnostics extension.</span></span> <span data-ttu-id="4a9e2-118">В этой конфигурации мы указываем идентификатор ресурса масштабируемого набора, который будет использоваться для сбора метрик, а также учетную запись хранения и маркер SAS для хранения метрик.</span><span class="sxs-lookup"><span data-stu-id="4a9e2-118">In this configuration, we specify the resource ID of the scale set to collect metrics from, as well as the storage account and SAS token to use to store the metrics.</span></span> <span data-ttu-id="4a9e2-119">Также указывается то, как часто будут вычисляться метрики (в данном случае — каждую минуту) и какие метрики нужно отслеживать (в этом случае — это процент используемой памяти).</span><span class="sxs-lookup"><span data-stu-id="4a9e2-119">We also specify how frequently the metrics are aggregated (in this case every minute) and which metrics to track (in this case percent used memory).</span></span> <span data-ttu-id="4a9e2-120">Дополнительные сведения об этой конфигурации и других метриках см. в [этой документации](../virtual-machines/linux/diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="4a9e2-120">For more detailed information on this configuration and metrics other than percent used memory, see [this documentation](../virtual-machines/linux/diagnostic-extension.md).</span></span>

```diff
                 }
               }
             ]
+          },
+          "extensionProfile": {
+            "extensions": [
+              {
+                "name": "LinuxDiagnosticExtension",
+                "properties": {
+                  "publisher": "Microsoft.Azure.Diagnostics",
+                  "type": "LinuxDiagnostic",
+                  "typeHandlerVersion": "3.0",
+                  "settings": {
+                    "StorageAccount": "[parameters('storageAccountName')]",
+                    "ladCfg": {
+                      "diagnosticMonitorConfiguration": {
+                        "performanceCounters": {
+                          "sinks": "WADMetricJsonBlob",
+                          "performanceCounterConfiguration": [
+                            {
+                              "unit": "percent",
+                              "type": "builtin",
+                              "class": "memory",
+                              "counter": "percentUsedMemory",
+                              "counterSpecifier": "/builtin/memory/percentUsedMemory",
+                              "condition": "IsAggregate=TRUE"
+                            }
+                          ]
+                        },
+                        "metrics": {
+                          "metricAggregation": [
+                            {
+                              "scheduledTransferPeriod": "PT1M"
+                            }
+                          ],
+                          "resourceId": "[resourceId('Microsoft.Compute/virtualMachineScaleSets', 'myScaleSet')]"
+                        }
+                      }
+                    }
+                  },
+                  "protectedSettings": {
+                    "storageAccountName": "[parameters('storageAccountName')]",
+                    "storageAccountSasToken": "[parameters('storageAccountSasToken')]",
+                    "sinksConfig": {
+                      "sink": [
+                        {
+                          "name": "WADMetricJsonBlob",
+                          "type": "JsonBlob"
+                        }
+                      ]
+                    }
+                  }
+                }
+              }
+            ]
           }
         }
       }
```

<span data-ttu-id="4a9e2-121">Наконец, добавляется ресурс `autoscaleSettings`, чтобы настроить автоматическое масштабирование на основе этих метрик.</span><span class="sxs-lookup"><span data-stu-id="4a9e2-121">Finally, we add an `autoscaleSettings` resource to configure autoscale based on these metrics.</span></span> <span data-ttu-id="4a9e2-122">Для ресурса указано предложение `dependsOn`, которое ссылается на масштабируемый набор, чтобы убедиться, что масштабируемый набор имеется, прежде чем пытаться его масштабировать.</span><span class="sxs-lookup"><span data-stu-id="4a9e2-122">This resource has a `dependsOn` clause that references the scale set to ensure that the scale set exists before attempting to autoscale it.</span></span> <span data-ttu-id="4a9e2-123">Если для автоматического масштабирования выбрана другая метрика, мы бы использовали `counterSpecifier` из конфигурации расширения диагностики в качестве `metricName` в конфигурации автоматического масштабирования.</span><span class="sxs-lookup"><span data-stu-id="4a9e2-123">If we choose a different metric to autoscale on, we would use the `counterSpecifier` from the diagnostics extension configuration as the `metricName` in the autoscale configuration.</span></span> <span data-ttu-id="4a9e2-124">Дополнительные сведения о настройке автомасштабирования см. в статье [Рекомендации по автомасштабированию](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md) и [Создание или обновление параметров автоматического масштабирования](https://msdn.microsoft.com/library/azure/dn931928.aspx).</span><span class="sxs-lookup"><span data-stu-id="4a9e2-124">For more information on autoscale configuration, see the [autoscale best practices](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md) and the [Azure Monitor REST API reference documentation](https://msdn.microsoft.com/library/azure/dn931928.aspx).</span></span>

```diff
+    },
+    {
+      "type": "Microsoft.Insights/autoscaleSettings",
+      "apiVersion": "2015-04-01",
+      "name": "guestMetricsAutoscale",
+      "location": "[resourceGroup().location]",
+      "dependsOn": [
+        "Microsoft.Compute/virtualMachineScaleSets/myScaleSet"
+      ],
+      "properties": {
+        "name": "guestMetricsAutoscale",
+        "targetResourceUri": "[resourceId('Microsoft.Compute/virtualMachineScaleSets', 'myScaleSet')]",
+        "enabled": true,
+        "profiles": [
+          {
+            "name": "Profile1",
+            "capacity": {
+              "minimum": "1",
+              "maximum": "10",
+              "default": "3"
+            },
+            "rules": [
+              {
+                "metricTrigger": {
+                  "metricName": "/builtin/memory/percentUsedMemory",
+                  "metricNamespace": "",
+                  "metricResourceUri": "[resourceId('Microsoft.Compute/virtualMachineScaleSets', 'myScaleSet')]",
+                  "timeGrain": "PT1M",
+                  "statistic": "Average",
+                  "timeWindow": "PT5M",
+                  "timeAggregation": "Average",
+                  "operator": "GreaterThan",
+                  "threshold": 60
+                },
+                "scaleAction": {
+                  "direction": "Increase",
+                  "type": "ChangeCount",
+                  "value": "1",
+                  "cooldown": "PT1M"
+                }
+              },
+              {
+                "metricTrigger": {
+                  "metricName": "/builtin/memory/percentUsedMemory",
+                  "metricNamespace": "",
+                  "metricResourceUri": "[resourceId('Microsoft.Compute/virtualMachineScaleSets', 'myScaleSet')]",
+                  "timeGrain": "PT1M",
+                  "statistic": "Average",
+                  "timeWindow": "PT5M",
+                  "timeAggregation": "Average",
+                  "operator": "LessThan",
+                  "threshold": 30
+                },
+                "scaleAction": {
+                  "direction": "Decrease",
+                  "type": "ChangeCount",
+                  "value": "1",
+                  "cooldown": "PT1M"
+                }
+              }
+            ]
+          }
+        ]
+      }
     }
   ]
 }
```





## <a name="next-steps"></a><span data-ttu-id="4a9e2-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4a9e2-125">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
