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
# <a name="using-virtual-machine-scale-sets-with-hello-azure-dsc-extension"></a><span data-ttu-id="42ec9-103">С помощью набора масштабирования виртуальной машины с hello расширений Azure DSC</span><span class="sxs-lookup"><span data-stu-id="42ec9-103">Using Virtual Machine Scale Sets with hello Azure DSC Extension</span></span>
<span data-ttu-id="42ec9-104">[Наборы масштабирования виртуальных машин](virtual-machine-scale-sets-overview.md) может использоваться с hello [Azure требуемого состояния (DSC)](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) обработчика расширений.</span><span class="sxs-lookup"><span data-stu-id="42ec9-104">[Virtual Machine Scale Sets](virtual-machine-scale-sets-overview.md) can be used with hello [Azure Desired State Configuration (DSC)](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) extension handler.</span></span> <span data-ttu-id="42ec9-105">Наборы масштабирования виртуальной машины предоставляют toodeploy способом и управлять большим количеством виртуальных машин и гибко можно свернуть или развернуть в tooload ответа.</span><span class="sxs-lookup"><span data-stu-id="42ec9-105">Virtual machine scale sets provide a way toodeploy and manage large numbers of virtual machines, and can elastically scale in and out in response tooload.</span></span> <span data-ttu-id="42ec9-106">DSC — используется tooconfigure hello виртуальных машин, как они переходит в оперативный режим, они работают под управлением программного обеспечения производственного hello.</span><span class="sxs-lookup"><span data-stu-id="42ec9-106">DSC is used tooconfigure hello VMs as they come online so they are running hello production software.</span></span>

## <a name="differences-between-deploying-toovirtual-machines-and-virtual-machine-scale-sets"></a><span data-ttu-id="42ec9-107">Различия при развертывании машины tooVirtual и наборы масштабирования виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="42ec9-107">Differences between deploying tooVirtual Machines and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="42ec9-108">Базовая структура шаблона Hello для набора масштабирования виртуальных машин немного отличается от одной виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="42ec9-108">hello underlying template structure for a virtual machine scale set is slightly different from a single VM.</span></span> <span data-ttu-id="42ec9-109">В частности в одной виртуальной Машины развертывает расширения в узле «virtualMachines» hello.</span><span class="sxs-lookup"><span data-stu-id="42ec9-109">Specifically, a single VM deploys extensions under hello "virtualMachines" node.</span></span> <span data-ttu-id="42ec9-110">Отсутствует запись типа «расширения», где DSC добавляется toohello шаблона</span><span class="sxs-lookup"><span data-stu-id="42ec9-110">There is an entry of type "extensions" where DSC is added toohello template</span></span>

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

<span data-ttu-id="42ec9-111">Узел набора масштабирования виртуальной машины имеет раздел «свойства» с «ExtensionProfile» атрибута «VirtualMachineProfile» hello.</span><span class="sxs-lookup"><span data-stu-id="42ec9-111">A virtual machine scale set node has a "properties" section with hello "VirtualMachineProfile", "extensionProfile" attribute.</span></span> <span data-ttu-id="42ec9-112">DSC добавляется в раздел extensions:</span><span class="sxs-lookup"><span data-stu-id="42ec9-112">DSC is added under "extensions"</span></span>

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

## <a name="behavior-for-a-virtual-machine-scale-set"></a><span data-ttu-id="42ec9-113">Поведение для масштабируемого набора виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="42ec9-113">Behavior for a Virtual Machine Scale Set</span></span>
<span data-ttu-id="42ec9-114">поведение Hello для набора масштабирования виртуальной машины — это поведение идентичные toohello для одной виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="42ec9-114">hello behavior for a virtual machine scale set is identical toohello behavior for a single VM.</span></span> <span data-ttu-id="42ec9-115">При создании новой виртуальной Машины, она автоматически снабжаются hello расширения DSC.</span><span class="sxs-lookup"><span data-stu-id="42ec9-115">When a new VM is created, it is automatically provisioned with hello DSC extension.</span></span> <span data-ttu-id="42ec9-116">Если более новая версия WMF требуется модулем hello приветствия hello ВМ перезагружает перед переходит в оперативный режим.</span><span class="sxs-lookup"><span data-stu-id="42ec9-116">If a newer version of hello WMF is required by hello extension, hello VM reboots before coming online.</span></span> <span data-ttu-id="42ec9-117">Он находится в оперативном режиме, загружает .zip hello DSC конфигурации и инициализировать его на hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="42ec9-117">Once it is online, it downloads hello DSC configuration .zip and provision it on hello VM.</span></span> <span data-ttu-id="42ec9-118">Дополнительные сведения можно найти в [hello Обзор расширение Azure DSC](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="42ec9-118">More details can be found in [hello Azure DSC Extension Overview](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="42ec9-119">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="42ec9-119">Next steps</span></span>
<span data-ttu-id="42ec9-120">Изучите hello [шаблона Azure Resource Manager для расширения hello DSC](../virtual-machines/windows/extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="42ec9-120">Examine hello [Azure Resource Manager template for hello DSC extension](../virtual-machines/windows/extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="42ec9-121">Узнайте, как hello [учетные данные безопасно обрабатываются расширение DSC](../virtual-machines/windows/extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="42ec9-121">Learn how hello [DSC extension securely handles credentials](../virtual-machines/windows/extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="42ec9-122">Дополнительные сведения о hello обработчик расширений Azure DSC см. в разделе [обработчик расширений Azure настройки требуемого состояния введение toohello](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="42ec9-122">For more information on hello Azure DSC extension handler, see [Introduction toohello Azure Desired State Configuration extension handler](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="42ec9-123">Дополнительные сведения о PowerShell DSC [посетите центр документации PowerShell hello](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="42ec9-123">For more information about PowerShell DSC, [visit hello PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

