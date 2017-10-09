---
title: "aaaTroubleshooting ВМ Linux сбоев расширения | Документы Microsoft"
description: "Узнайте об устранении неполадок в расширении виртуальной машины Linux в Azure."
services: virtual-machines-linux
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: top-support-issue,azure-resource-manager
ms.assetid: f05d93f3-42fc-4a09-9798-d92f7929c417
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: 29a0ca34207421e0014380000a313d3c44e7e594
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-linux-vm-extension-failures"></a>Устранение неполадок расширения виртуальной машины Linux
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a>Просмотр состояния расширения
Шаблоны Azure Resource Manager могут быть выполнены из hello Azure CLI. После выполнения шаблона hello состояние расширения hello можно просмотреть с помощью обозревателя ресурсов Azure или hello средств командной строки.

Пример:

Azure CLI:

      azure vm get-instance-view


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

## <a name="troubleshooting-extenson-failures"></a>Устранение сбоев в расширениях
### <a name="re-running-hello-extension-on-hello-vm"></a>Повторный запуск расширения hello на hello виртуальной Машины
При выполнении скриптов на виртуальной Машине с помощью настраиваемого расширения скриптов hello иногда может запустить произошла ошибка, когда виртуальная машина успешно создана, но hello в сценарии возникла ошибка. В этих conditons hello, рекомендуется toorecover способом после этой ошибки — расширение tooremove hello и перезапустите процесс hello шаблона.
Примечание: В будущем, эта функция будет улучшенные tooremove hello необходимость удаления расширения hello.

#### <a name="remove-hello-extension-from-azure-cli"></a>Удалите расширение hello из Azure CLI
      azure vm extension set --resource-group "KPRG1" --vm-name "kundanapdemo" --publisher-name "Microsoft.Compute.CustomScriptExtension" --name "myCustomScriptExtension" --version 1.4 --uninstall

Где «приложением Publisher name» соответствует тип расширения toohello из выходных данных hello «виртуальная машина azure get экземпляр-View», а имя является именем hello hello расширения ресурса из шаблона hello

После удаления расширения hello hello шаблон может быть повторно выполняется toorun hello сценариев на hello виртуальной Машины.

