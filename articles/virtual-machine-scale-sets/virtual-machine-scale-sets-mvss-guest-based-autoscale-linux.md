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
# <a name="autoscale-using-guest-metrics-in-a-linux-scale-set-template"></a>Автоматическое масштабирование с помощью метрик гостевой виртуальной машины в шаблоне масштабируемого набора Linux

Существует два типа метрик в Azure, который собирается с виртуальными машинами и масштабировать наборов: некоторые поставляются из hello размещения виртуальной Машины и другие берутся из гостевой Виртуальной машине hello. Показателей узла не требуют дополнительной настройки, так как они собираются hello узлом виртуальной Машины, а гостевых метрик требуют нам tooinstall hello [расширение диагностики Windows Azure](../virtual-machines/windows/extensions-diagnostics-template.md) или hello [диагностики Azure Linux расширение](../virtual-machines/linux/diagnostic-extension.md) в hello гостевая виртуальная машина. Один распространенные причины toouse гостевой метрики вместо показателей узла представляют что гостевых метрик предоставляет расширенный набор показателей, чем показателей узла. Один из таких примеров — это метрики потребления памяти, которые доступны только через метрики гостевой виртуальной машины. перечислены показателей узла Hello поддерживается [здесь](../monitoring-and-diagnostics/monitoring-supported-metrics.md), и перечислены часто используемые гостевых метрик [здесь](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md). В этой статье показано, как toomodify hello [Минимальный масштаб допустимого шаблона набора](./virtual-machine-scale-sets-mvss-start.md) toouse автомасштабирования правила, основанные на гостевых метрик для набора масштабирования Linux.

## <a name="change-hello-template-definition"></a>Измените определение шаблона hello

Наш шаблон Минимальный масштаб допустимого набора может видеть [здесь](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), и можно будет увидеть нашей шаблон для развертывания hello Linux набор масштабирования с гостевые автомасштабирования [здесь](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json). Давайте рассмотрим toocreate hello diff использовать этот шаблон (`git diff minimum-viable-scale-set existing-vnet`) по частям:

Сначала добавим параметры для `storageAccountName` и `storageAccountSasToken`. агент диагностики Hello будут храниться данные метрик в [таблицы](../cosmos-db/table-storage-how-to-use-dotnet.md) в этой учетной записи хранения. Начиная с hello диагностики Linux Agent версии 3.0 больше не поддерживается с помощью ключа доступа к хранилищу. Необходимо использовать [маркер SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

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

Далее мы изменить набор масштабирования hello `extensionProfile` расширения диагностики tooinclude hello. В данной конфигурации мы укажите идентификатор hello шкалы набор показателей toocollect hello ресурсов, а также hello учетной записи хранилища и метрики hello toostore toouse маркера SAS. Мы также указать, как часто объединяются метрики hello (в данном случае каждую минуту) и какие tootrack метрики (в этом вариантов процент используемой памяти). Дополнительные сведения об этой конфигурации и других метриках см. в [этой документации](../virtual-machines/linux/diagnostic-extension.md).

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

Наконец, мы добавим `autoscaleSettings` автомасштабирования tooconfigure ресурсов на основании этих показателей. Этот ресурс содержит `dependsOn` предложение, которое ссылается на шкале hello задать tooensure, прежде чем tooautoscale существует набор масштабирования hello его. Если мы выбрать различные метрики tooautoscale на, мы бы использовали hello `counterSpecifier` из конфигурации модуля диагностики hello как hello `metricName` в настройки автомасштабирования hello. Дополнительные сведения о настройке автомасштабирования см. в разделе hello [автомасштабирования рекомендации](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md) и hello [справочной документации API REST Azure монитор](https://msdn.microsoft.com/library/azure/dn931928.aspx).

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





## <a name="next-steps"></a>Дальнейшие действия

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
