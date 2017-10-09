---
title: "Проверьте aaaVerify трафика с потоком IP Наблюдатель сети Azure - REST | Документы Microsoft"
description: "В этой статье описывается как toocheck, если разрешен или запрещен трафик tooor из виртуальной машины"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 3307a79f-03be-46a0-aaaf-b2079cb5f3b2
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 956db0d326db597c6c402a9e8d4a5522c47c02d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-with-ip-flow-verify-a-component-of-azure-network-watcher"></a>Проверка состояния входящего и исходящего трафика (разрешен или запрещен) путем проверки IP-потока (компонент Наблюдателя за сетями Azure)

> [!div class="op_single_selector"]
> - [Портал Azure](network-watcher-check-ip-flow-verify-portal.md)
> - [PowerShell](network-watcher-check-ip-flow-verify-powershell.md)
> - [Интерфейс командной строки 1.0](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-ip-flow-verify-cli.md)
> - [Azure REST API](network-watcher-check-ip-flow-verify-rest.md)


Проверьте IP потока — это функция Наблюдатель сети, который позволяет вам tooverify, если трафик tooor из виртуальной машины. Hello проверку можно провести для входящего и исходящего трафика. Этот сценарий является полезным tooget текущее состояние ли виртуальной машины могут взаимодействовать tooan внешнего ресурса или внутреннего сервера. Проверьте IP потока может быть tooverify используется, если правила группы безопасности сети (NSG) правильно настроены и устранение неполадок потоки, которые заблокированы правила NSG. Кроме того, использует IP-адрес потока проверки tooensure трафика, что требуется заблокированных блокировано правильно hello NSG.

## <a name="before-you-begin"></a>Перед началом работы

ARMclient — используется toocall hello REST API с помощью PowerShell. Пакет ARMClient можно скачать на сайте [Chocolatey](https://chocolatey.org/packages/ARMClient).

Этот сценарий предполагает уже были выполнены шаги hello в [создать Наблюдатель сети](network-watcher-create.md) toocreate Наблюдатель сети.

## <a name="scenario"></a>Сценарий

В этом сценарии используется tooverify проверьте потока IP, если виртуальная машина может обмениваться информацией машины tooanother через порт 443. Если трафик hello запрещен, он возвращает hello правило безопасности, блокирующее, трафик. Посетите toolearn Дополнительные сведения о IP потока проверьте, [IP потока проверить Обзор](network-watcher-ip-flow-verify-overview.md)

В рамках этого сценария вы:

* Получение виртуальной машины
* Вызов проверки IP-потока
* проверите результаты;

## <a name="log-in-with-armclient"></a>выполните вход с помощью ARMClient;

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a>Получение виртуальной машины

Запустите следующий сценарий tooreturn hello виртуальной машины. Hello следующий код должен значений для переменных hello.

* **subscriptionId** -hello toouse идентификатор подписки.
* **resourceGroupName** — hello имя группы ресурсов, содержащем виртуальные машины.

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

Hello сведения, необходимые — идентификатор hello в тип hello `Microsoft.Compute/virtualMachines`. Hello результаты должны быть примерно toohello следующий образец кода:

```json
...,
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft
.Network/networkInterfaces/contosovm842"
            }
          ]
        },
        "provisioningState": "Succeeded"
      },
      "resources": [
        {
          "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft.Com
pute/virtualMachines/ContosoVM/extensions/CustomScriptExtension"
        }
      ],
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```

## <a name="call-ip-flow-verify"></a>Вызов проверки IP-потока

Hello следующий пример создает запрос tooverify hello трафика для указанной виртуальной машины. Hello ответ возвращается, если трафик hello или запрещен трафик hello. Если он запрещен трафик также возвращает какие блоки правило hello трафика.

> [!NOTE]
> Проверьте потока IP требует, что выделена hello ресурса виртуальной Машины.

Hello сценарий требует ресурсов hello идентификатор виртуальной машины и сетевой интерфейсной платы на виртуальной машине hello. Эти значения предоставляются hello предшествующих выходных данных.

> [!Important]
> Для всех ОСТАЛЬНЫХ Наблюдатель сети вызовы hello имя группы ресурсов в запросе hello, что URI является hello, содержащей экземпляр hello Наблюдатель сети, не hello ресурсы при выполнении hello диагностических действий на.

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"
$networkWatcherName = "<network watcher name>"
$vmName = "<vm name>"
$vmNICName = "<vm NIC name>"
$direction = "<direction of traffic>" # Examples are: Inbound or Outbound
$localIP = "<source IP>"
$localPort = "<source Port>"
$remoteIP = "<destination IP>"
$remotePort = "<destination Port>" # Examples are: 80, or 80-120
$protocol = "<UDP, TCP or *>"
$targetUri = "<uri of target resource>" # Example: /subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.compute/virtualMachine/${vmName}
$targetNic = "<uri of target nic resource>" # Example: /subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkInterfaces/${vmNICName}

$requestBody = @"
{
    'targetResourceId':  '$targetUri',
    'direction':  '$direction',
    'protocol':  '$protocol',
    'localPort':  '$localPort',
    'remotePort':  '$remotePort',
    'localIPAddress':  '$localIP',
    'remoteIPAddress':  '$remoteIP',
    'targetNICResourceId':  '$targetNic'
}
"@
        
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/ipFlowVerify?api-version=2016-12-01" $requestBody -verbose
```

## <a name="understanding-hello-results"></a>Основные сведения о результатах hello

Hello вы получаете вы узнаете, разрешен или запрещен трафик hello. Hello ответа выглядит как один из следующих примеров hello.

**Разрешен**

```json
{
  "access": "Allow",
  "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

**Запрещен**

```json
{
  "access": "Deny",
  "ruleName": "defaultSecurityRules/DefaultInboundDenyAll"
}
```

## <a name="next-steps"></a>Дальнейшие действия

Если трафик блокируется, и его не следует, см. раздел [Управление группами безопасности сети](../virtual-network/virtual-network-manage-nsg-arm-portal.md) toolearn Дополнительные сведения о группах безопасности сети.












