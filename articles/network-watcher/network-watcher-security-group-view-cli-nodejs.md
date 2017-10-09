---
title: "Сетевая безопасность aaaAnalyze с представлением группы безопасности Наблюдатель сети Azure - Azure CLI 1.0 | Документы Microsoft"
description: "В этой статье описывается, как tooanalyze toouse Azure CLI 1.0 a виртуальных машин безопасности с представлением группы безопасности."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: a986ff4f-7e0c-4994-95e1-4ac824986500
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 96383a734b94d215d5b0f3d47339e46940d700b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-azure-cli-10"></a>Анализ безопасности виртуальных машин с помощью Azure CLI 1.0 и представления группы безопасности

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-security-group-view-powershell.md)
> - [Интерфейс командной строки 1.0](network-watcher-security-group-view-cli-nodejs.md)
> - [CLI 2.0](network-watcher-security-group-view-cli.md)
> - [REST API](network-watcher-security-group-view-rest.md)

Представление "Группа безопасности" возвращает правила безопасности сети настроены и эффективным, примененные tooa виртуальной машины. Эта возможность является полезным tooaudit и диагностики сетевых групп безопасности и правила, настроенные на tooensure трафика виртуальных Машин выполняется правильно разрешен или запрещен. В этой статье мы показано, как настроить tooretrieve hello и эффективной защиты правила tooa виртуальной машины с помощью Azure CLI

В этой статье используется кроссплатформенной Azure CLI 1.0, доступный для Windows, Mac и Linux. Наблюдатель за сетями в настоящее время использует Azure CLI 1.0 в качестве интерфейса командной строки.

## <a name="before-you-begin"></a>Перед началом работы

Этот сценарий предполагает уже были выполнены шаги hello в [создать Наблюдатель сети](network-watcher-create.md) toocreate Наблюдатель сети.

## <a name="scenario"></a>Сценарий

Hello сценарий, описанный в этой статье извлекает настроен hello и правила безопасности для данной виртуальной машине.

## <a name="get-a-vm"></a>Получение виртуальной машины

Виртуальная машина — hello необходимые toorun `vm list` командлета. Hello следующая команда выводит список виртуальных machinese hello в группе ресурсов:

```azurecli
azure vm list -g resourceGroupName
```

Если известно hello виртуальной машины, можно использовать hello `vm show` tooget командлет его идентификатором ресурса:

```azurecli
azure vm show -g resourceGroupName -n virtualMachineName
```

## <a name="retrieve-security-group-view"></a>Получение представления группы безопасности

Hello следующим шагом является результат представления группы безопасности hello tooretrieve. Добавление hello «--json» флаг отформатирует результаты hello в формате json.

```azurecli
azure network watcher security-group-view -g resourceGroupName -n networkWatcherName -t targetResourceId --json
```

## <a name="viewing-hello-results"></a>Просмотр результатов hello

Hello следующий пример — сокращенный ответа возвращаемых результатов hello. Hello результаты показывают все правила безопасности эффективный и примененные hello на виртуальной машине hello разбит на группы **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, и  **EffectiveSecurityRules**.

```json
{
  "networkInterfaces": [
    {
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testnic",
      "securityRuleAssociations": {
        "networkInterfaceAssociation": {
          "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testvm",
          "securityRules": [
            {
              "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/test-nsg/securityRules/default-allow-rdp",
              "protocol": "TCP",
              "sourcePortRange": "*",
              "destinationPortRange": "3389",
              "sourceAddressPrefix": "*",
              "destinationAddressPrefix": "*",
              "access": "Allow",
              "priority": 1000,
              "direction": "Inbound",
              "provisioningState": "Succeeded",
              "name": "default-allow-rdp",
              "etag": "W/\"00000000-0000-0000-0000-000000000000\""
            }
          ]
        },
        "defaultSecurityRules": [
          {
            "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/networkSecurityGroups//defaultSecurityRules/",
            "description": "Allow inbound traffic from all VMs in VNET",
            "protocol": "*",
            "sourcePortRange": "*",
            "destinationPortRange": "*",
            "sourceAddressPrefix": "VirtualNetwork",
            "destinationAddressPrefix": "VirtualNetwork",
            "access": "Allow",
            "priority": 65000,
            "direction": "Inbound",
            "provisioningState": "Succeeded",
            "name": "AllowVnetInBound"
          }
        ]
      }
    }
  ]
}
```

## <a name="next-steps"></a>Дальнейшие действия

Посетите [аудита безопасности сети группы (NSG) с Наблюдатель сети](network-watcher-nsg-auditing-powershell.md) toolearn способ проверки tooautomate групп безопасности сети.

Дополнительные сведения о правилах безопасности hello, которые будут применяться tooyour сетевым ресурсам, посетив [Общие сведения о представлении группы безопасности](network-watcher-security-group-view-overview.md)
