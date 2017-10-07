---
title: "ошибки расширения виртуальной Машины Windows aaaTroubleshooting | Документы Microsoft"
description: "Узнайте об устранении неполадок в работе расширений виртуальной машины Windows в Azure."
services: virtual-machines-windows
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: top-support-issue,azure-resource-manager
ms.assetid: 878ab9b6-c3e6-40be-82d4-d77fecd5030f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: d24544743d9e0cb1a68ec9ab7718716f918054f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-windows-vm-extension-failures"></a>Troubleshooting Azure Windows VM extension failures
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a>Просмотр состояния расширения
Шаблоны Azure Resource Manager можно выполнять из Azure PowerShell. После выполнения шаблона hello состояние расширения hello можно просмотреть с помощью обозревателя ресурсов Azure или hello средств командной строки.

Пример:

Azure PowerShell

      Get-AzureRmVM -ResourceGroupName $RGName -Name $vmName -Status

Вот пример выходных данных hello.

      Extensions:  {
      "ExtensionType": "Microsoft.Compute.CustomScriptExtension",
      "Name": "myCustomScriptExtension",
      "SubStatuses": [
        {
          "Code": "ComponentStatus/StdOut/succeeded",
          "DisplayStatus": "Provisioning succeeded",
          "Level": "Info",
          "Message": "    Directory: C:\\temp\\n\\n\\nMode                LastWriteTime     Length Name
              \\n----                -------------     ------ ----                              \\n-a---          9/1/2015   2:03 AM         11
              test.txt                          \\n\\n",
                      "Time": null
          },
        {
          "Code": "ComponentStatus/StdErr/succeeded",
          "DisplayStatus": "Provisioning succeeded",
          "Level": "Info",
          "Message": "",
          "Time": null
        }
    }
  ]

## <a name="troubleshooting-extension-failures"></a>Устранение неполадок расширений
### <a name="re-running-hello-extension-on-hello-vm"></a>Повторный запуск расширения hello на hello виртуальной Машины
При выполнении скриптов на виртуальной Машине с помощью настраиваемого расширения скриптов hello иногда может запустить произошла ошибка, когда виртуальная машина успешно создана, но hello в сценарии возникла ошибка. В этих conditons hello, рекомендуется toorecover способом после этой ошибки — расширение tooremove hello и перезапустите процесс hello шаблона.
Примечание: В будущем, эта функция будет улучшенные tooremove hello необходимость удаления расширения hello.

#### <a name="remove-hello-extension-from-azure-powershell"></a>Удалите расширение hello из Azure PowerShell
    Remove-AzureRmVMExtension -ResourceGroupName $RGName -VMName $vmName -Name "myCustomScriptExtension"

После удаления расширения hello hello шаблон может быть повторно выполняется toorun hello сценариев на hello виртуальной Машины.

