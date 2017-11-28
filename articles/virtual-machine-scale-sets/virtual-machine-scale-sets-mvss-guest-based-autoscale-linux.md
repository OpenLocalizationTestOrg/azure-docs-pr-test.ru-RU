---
title: "Использование автоматического масштабирования Azure с метриками гостевой виртуальной машины в шаблоне масштабируемого набора Linux | Документация Майкрософт"
description: "Узнайте, как с помощью гостевых метрик в наборе масштабирования виртуальных машин Linux шаблона tooautoscale"
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
ms.openlocfilehash: 7afbef943a5f15c7a72dcf7114f46d521c504424
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="autoscale-using-guest-metrics-in-a-linux-scale-set-template"></a><span data-ttu-id="66c59-103">Автоматическое масштабирование с помощью метрик гостевой виртуальной машины в шаблоне масштабируемого набора Linux</span><span class="sxs-lookup"><span data-stu-id="66c59-103">Autoscale using guest metrics in a Linux scale set template</span></span>

<span data-ttu-id="66c59-104">Существует два типа метрик в Azure, который собирается с виртуальными машинами и масштабировать наборов: некоторые поставляются из hello размещения виртуальной Машины и другие берутся из гостевой Виртуальной машине hello.</span><span class="sxs-lookup"><span data-stu-id="66c59-104">There are two types of metrics in Azure that are gathered from VMs and scale sets: some come from hello host VM and others come from hello guest VM.</span></span> <span data-ttu-id="66c59-105">Показателей узла не требуют дополнительной настройки, так как они собираются hello узлом виртуальной Машины, а гостевых метрик требуют нам tooinstall hello [расширение диагностики Windows Azure](../virtual-machines/windows/extensions-diagnostics-template.md) или hello [диагностики Azure Linux расширение](../virtual-machines/linux/diagnostic-extension.md) в hello гостевая виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="66c59-105">Host metrics do not require additional setup because they are collected by hello host VM, whereas guest metrics require us tooinstall hello [Windows Azure Diagnostics extension](../virtual-machines/windows/extensions-diagnostics-template.md) or hello [Linux Azure Diagnostics extension](../virtual-machines/linux/diagnostic-extension.md) in hello guest VM.</span></span> <span data-ttu-id="66c59-106">Один распространенные причины toouse гостевой метрики вместо показателей узла представляют что гостевых метрик предоставляет расширенный набор показателей, чем показателей узла.</span><span class="sxs-lookup"><span data-stu-id="66c59-106">One common reason toouse guest metrics instead of host metrics is that guest metrics provide a larger selection of metrics than host metrics.</span></span> <span data-ttu-id="66c59-107">Один из таких примеров — это метрики потребления памяти, которые доступны только через метрики гостевой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="66c59-107">One such example is memory-consumption metrics, which are only available via guest metrics.</span></span> <span data-ttu-id="66c59-108">перечислены показателей узла Hello поддерживается [здесь](../monitoring-and-diagnostics/monitoring-supported-metrics.md), и перечислены часто используемые гостевых метрик [здесь](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="66c59-108">hello supported host metrics are listed [here](../monitoring-and-diagnostics/monitoring-supported-metrics.md), and commonly used guest metrics are listed [here](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span></span> <span data-ttu-id="66c59-109">В этой статье показано, как toomodify hello [Минимальный масштаб допустимого шаблона набора](./virtual-machine-scale-sets-mvss-start.md) toouse автомасштабирования правила, основанные на гостевых метрик для набора масштабирования Linux.</span><span class="sxs-lookup"><span data-stu-id="66c59-109">This article shows how toomodify hello [minimum viable scale set template](./virtual-machine-scale-sets-mvss-start.md) toouse autoscale rules based on guest metrics for Linux scale sets.</span></span>

## <a name="change-hello-template-definition"></a><span data-ttu-id="66c59-110">Измените определение шаблона hello</span><span class="sxs-lookup"><span data-stu-id="66c59-110">Change hello template definition</span></span>

<span data-ttu-id="66c59-111">Наш шаблон Минимальный масштаб допустимого набора может видеть [здесь](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), и можно будет увидеть нашей шаблон для развертывания hello Linux набор масштабирования с гостевые автомасштабирования [здесь](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="66c59-111">Our minimum viable scale set template can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), and our template for deploying hello Linux scale set with guest-based autoscale can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json).</span></span> <span data-ttu-id="66c59-112">Давайте рассмотрим toocreate hello diff использовать этот шаблон (`git diff minimum-viable-scale-set existing-vnet`) по частям:</span><span class="sxs-lookup"><span data-stu-id="66c59-112">Let's examine hello diff used toocreate this template (`git diff minimum-viable-scale-set existing-vnet`) piece by piece:</span></span>

<span data-ttu-id="66c59-113">Сначала добавим параметры для `storageAccountName` и `storageAccountSasToken`.</span><span class="sxs-lookup"><span data-stu-id="66c59-113">First, we add parameters for `storageAccountName` and `storageAccountSasToken`.</span></span> <span data-ttu-id="66c59-114">агент диагностики Hello будут храниться данные метрик в [таблицы](../cosmos-db/table-storage-how-to-use-dotnet.md) в этой учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="66c59-114">hello diagnostics agent will store metric data in a [table](../cosmos-db/table-storage-how-to-use-dotnet.md) in this storage account.</span></span> <span data-ttu-id="66c59-115">Начиная с hello диагностики Linux Agent версии 3.0 больше не поддерживается с помощью ключа доступа к хранилищу.</span><span class="sxs-lookup"><span data-stu-id="66c59-115">As of hello Linux Diagnostics Agent version 3.0, using a storage access key is no longer supported.</span></span> <span data-ttu-id="66c59-116">Необходимо использовать [маркер SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="66c59-116">We must use a [SAS Token](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span></span>

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

<span data-ttu-id="66c59-117">Далее мы изменить набор масштабирования hello `extensionProfile` расширения диагностики tooinclude hello.</span><span class="sxs-lookup"><span data-stu-id="66c59-117">Next, we modify hello scale set `extensionProfile` tooinclude hello diagnostics extension.</span></span> <span data-ttu-id="66c59-118">В данной конфигурации мы укажите идентификатор hello шкалы набор показателей toocollect hello ресурсов, а также hello учетной записи хранилища и метрики hello toostore toouse маркера SAS.</span><span class="sxs-lookup"><span data-stu-id="66c59-118">In this configuration, we specify hello resource ID of hello scale set toocollect metrics from, as well as hello storage account and SAS token toouse toostore hello metrics.</span></span> <span data-ttu-id="66c59-119">Мы также указать, как часто объединяются метрики hello (в данном случае каждую минуту) и какие tootrack метрики (в этом вариантов процент используемой памяти).</span><span class="sxs-lookup"><span data-stu-id="66c59-119">We also specify how frequently hello metrics are aggregated (in this case every minute) and which metrics tootrack (in this case percent used memory).</span></span> <span data-ttu-id="66c59-120">Дополнительные сведения об этой конфигурации и других метриках см. в [этой документации](../virtual-machines/linux/diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="66c59-120">For more detailed information on this configuration and metrics other than percent used memory, see [this documentation](../virtual-machines/linux/diagnostic-extension.md).</span></span>

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

<span data-ttu-id="66c59-121">Наконец, мы добавим `autoscaleSettings` автомасштабирования tooconfigure ресурсов на основании этих показателей.</span><span class="sxs-lookup"><span data-stu-id="66c59-121">Finally, we add an `autoscaleSettings` resource tooconfigure autoscale based on these metrics.</span></span> <span data-ttu-id="66c59-122">Этот ресурс содержит `dependsOn` предложение, которое ссылается на шкале hello задать tooensure, прежде чем tooautoscale существует набор масштабирования hello его.</span><span class="sxs-lookup"><span data-stu-id="66c59-122">This resource has a `dependsOn` clause that references hello scale set tooensure that hello scale set exists before attempting tooautoscale it.</span></span> <span data-ttu-id="66c59-123">Если мы выбрать различные метрики tooautoscale на, мы бы использовали hello `counterSpecifier` из конфигурации модуля диагностики hello как hello `metricName` в настройки автомасштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="66c59-123">If we choose a different metric tooautoscale on, we would use hello `counterSpecifier` from hello diagnostics extension configuration as hello `metricName` in hello autoscale configuration.</span></span> <span data-ttu-id="66c59-124">Дополнительные сведения о настройке автомасштабирования см. в разделе hello [автомасштабирования рекомендации](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md) и hello [справочной документации API REST Azure монитор](https://msdn.microsoft.com/library/azure/dn931928.aspx).</span><span class="sxs-lookup"><span data-stu-id="66c59-124">For more information on autoscale configuration, see hello [autoscale best practices](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md) and hello [Azure Monitor REST API reference documentation](https://msdn.microsoft.com/library/azure/dn931928.aspx).</span></span>

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





## <a name="next-steps"></a><span data-ttu-id="66c59-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="66c59-125">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
