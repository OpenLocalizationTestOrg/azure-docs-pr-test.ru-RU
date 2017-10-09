---
title: "aaaUsing требуемого состояния конфигурации с наборы масштабирования виртуальных машин | Документы Microsoft"
description: "С помощью набора масштабирования виртуальной машины с hello расширений Azure DSC"
services: virtual-machine-scale-sets
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: c8f047b5-0e6c-4ef3-8a47-f1b284d32942
ms.service: virtual-machine-scale-sets
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 04/05/2017
ms.author: zachal
ms.openlocfilehash: a35f1ca6700aa4889978032aa512882db50d6573
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-virtual-machine-scale-sets-with-hello-azure-dsc-extension"></a>С помощью набора масштабирования виртуальной машины с hello расширений Azure DSC
[Наборы масштабирования виртуальных машин](virtual-machine-scale-sets-overview.md) может использоваться с hello [Azure требуемого состояния (DSC)](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) обработчика расширений. Наборы масштабирования виртуальной машины предоставляют toodeploy способом и управлять большим количеством виртуальных машин и гибко можно свернуть или развернуть в tooload ответа. DSC — используется tooconfigure hello виртуальных машин, как они переходит в оперативный режим, они работают под управлением программного обеспечения производственного hello.

## <a name="differences-between-deploying-toovirtual-machines-and-virtual-machine-scale-sets"></a>Различия при развертывании машины tooVirtual и наборы масштабирования виртуальных машин
Базовая структура шаблона Hello для набора масштабирования виртуальных машин немного отличается от одной виртуальной Машины. В частности в одной виртуальной Машины развертывает расширения в узле «virtualMachines» hello. Отсутствует запись типа «расширения», где DSC добавляется toohello шаблона

```
"resources": [
          {
              "name": "Microsoft.Powershell.DSC",
              "type": "extensions",
              "location": "[resourceGroup().location]",
              "apiVersion": "2015-06-15",
              "dependsOn": [
                  "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
              ],
              "tags": {
                  "displayName": "dscExtension"
              },
              "properties": {
                  "publisher": "Microsoft.Powershell",
                  "type": "DSC",
                  "typeHandlerVersion": "2.20",
                  "autoUpgradeMinorVersion": false,
                  "forceUpdateTag": "[parameters('dscExtensionUpdateTagVersion')]",
                  "settings": {
                      "configuration": {
                          "url": "[concat(parameters('_artifactsLocation'), '/', variables('dscExtensionArchiveFolder'), '/', variables('dscExtensionArchiveFileName'))]",
                          "script": "DscExtension.ps1",
                          "function": "Main"
                      },
                      "configurationArguments": {
                          "nodeName": "[variables('vmName')]"
                      }
                  },
                  "protectedSettings": {
                      "configurationUrlSasToken": "[parameters('_artifactsLocationSasToken')]"
                  }
              }
          }
      ]
```

Узел набора масштабирования виртуальной машины имеет раздел «свойства» с «ExtensionProfile» атрибута «VirtualMachineProfile» hello. DSC добавляется в раздел extensions:

```
"extensionProfile": {
            "extensions": [
                {
                    "name": "Microsoft.Powershell.DSC",
                    "properties": {
                        "publisher": "Microsoft.Powershell",
                        "type": "DSC",
                        "typeHandlerVersion": "2.20",
                        "autoUpgradeMinorVersion": false,
                        "forceUpdateTag": "[parameters('DscExtensionUpdateTagVersion')]",
                        "settings": {
                            "configuration": {
                                "url": "[concat(parameters('_artifactsLocation'), '/', variables('DscExtensionArchiveFolder'), '/', variables('DscExtensionArchiveFileName'))]",
                                "script": "DscExtension.ps1",
                                "function": "Main"
                            },
                            "configurationArguments": {
                                "nodeName": "localhost"
                            }
                        },
                        "protectedSettings": {
                            "configurationUrlSasToken": "[parameters('_artifactsLocationSasToken')]"
                        }
                    }
                }
            ]
```

## <a name="behavior-for-a-virtual-machine-scale-set"></a>Поведение для масштабируемого набора виртуальных машин
поведение Hello для набора масштабирования виртуальной машины — это поведение идентичные toohello для одной виртуальной Машины. При создании новой виртуальной Машины, она автоматически снабжаются hello расширения DSC. Если более новая версия WMF требуется модулем hello приветствия hello ВМ перезагружает перед переходит в оперативный режим. Он находится в оперативном режиме, загружает .zip hello DSC конфигурации и инициализировать его на hello виртуальной Машины. Дополнительные сведения можно найти в [hello Обзор расширение Azure DSC](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="next-steps"></a>Дальнейшие действия
Изучите hello [шаблона Azure Resource Manager для расширения hello DSC](../virtual-machines/windows/extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Узнайте, как hello [учетные данные безопасно обрабатываются расширение DSC](../virtual-machines/windows/extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Дополнительные сведения о hello обработчик расширений Azure DSC см. в разделе [обработчик расширений Azure настройки требуемого состояния введение toohello](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Дополнительные сведения о PowerShell DSC [посетите центр документации PowerShell hello](https://msdn.microsoft.com/powershell/dsc/overview). 

