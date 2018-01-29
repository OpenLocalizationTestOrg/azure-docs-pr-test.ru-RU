---
title: "Проверка трафика с использованием проверки потока IP-адресов с помощью Наблюдателя за сетями (Azure CLI) | Документация Майкрософт"
description: "В этой статье описывается, как проверить состояние передачи входящего и исходящего трафика виртуальной машины (разрешен или запрещен) с помощью Azure CLI."
services: network-watcher
documentationcenter: na
author: jimdial
manager: timlt
editor: 
ms.assetid: 92b857ed-c834-4c1b-8ee9-538e7ae7391d
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: jdial
ms.openlocfilehash: f1355cd861722848211277250155c434da1e774d
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/21/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-to-or-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a>Проверка состояния входящего и исходящего трафика виртуальной машины (разрешен или запрещен) путем проверки потока IP-адресов (компонент Наблюдателя за сетями Azure)

> [!div class="op_single_selector"]
> - [портал Azure](network-watcher-check-ip-flow-verify-portal.md)
> - [PowerShell](network-watcher-check-ip-flow-verify-powershell.md)
> - [Интерфейс командной строки 1.0](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-ip-flow-verify-cli.md)
> - [Azure REST API](network-watcher-check-ip-flow-verify-rest.md)


Проверка IP-потока — это компонент Наблюдателя за сетями, позволяющий определить состояние (разрешен или запрещен) входящего и исходящего трафика виртуальной машины. В этом сценарии можно получить сведения о текущем состоянии взаимодействия виртуальной машины с внешним ресурсом или сервером. Проверка потока IP-адресов позволяет убедиться, что правила группы безопасности сети настроены правильно, и устранить неполадки потоков, заблокированных правилами NSG. Такая проверка также гарантирует, что NSG будет соответствующим образом блокировать трафик, который нужно заблокировать.

В этой статье используется кроссплатформенной Azure CLI 1.0, доступный для Windows, Mac и Linux.

## <a name="before-you-begin"></a>Перед началом работы

В этом сценарии предполагается, что у вас уже есть Наблюдатель за сетями или что вы создали его в соответствии с инструкциями в статье [Create a Network Watcher](network-watcher-create.md) (Создание Наблюдателя за сетями). Предполагается также, что у вас имеется группа ресурсов с допустимой виртуальной машиной.

## <a name="scenario"></a>Сценарий

В этом сценарии проверка потока IP-адресов используется, чтобы определить, может ли виртуальная машина обратиться к Bing по известному IP-адресу. Если трафик отклоняется, возвращается правило безопасности, блокирующее трафик. Дополнительные сведения о проверке потока IP-адресов см. в [этом обзоре](network-watcher-ip-flow-verify-overview.md).


## <a name="get-a-vm"></a>Получение виртуальной машины

При проверке IP-потока тестируется входящий и исходящий трафик виртуальной машины по IP-адресу в удаленное расположение и из него. Для командлета требуется идентификатор виртуальной машины. Если вы уже знаете идентификатор виртуальной машины, этот шаг можно пропустить.

```
azure vm show -g resourceGroupName -n virtualMachineName
```

## <a name="get-the-nics"></a>Получение сетевых карт

Вам понадобится IP-адрес сетевой карты на виртуальной машине. В этом примере мы получаем сетевые карты на виртуальной машине. Если вы уже знаете IP-адрес, который необходимо протестировать на виртуальной машине, этот шаг можно пропустить.

```
azure network nic show -g resourceGroupName -n nicName
```

## <a name="run-ip-flow-verify"></a>Выполнение проверки IP-потока

Теперь, когда у нас есть сведения, необходимые для выполнения командлета, мы выполним командлет `network watcher ip-flow-verify` для проверки трафика. В этом примере мы используем первый IP-адрес первой сетевой карты.

```
azure network watcher ip-flow-verify -g resourceGroupName -n networkWatcherName -t targetResourceId -d directionInboundorOutbound -p protocolTCPorUDP -o localPort -m remotePort -l localIpAddr -r remoteIpAddr
```

> [!NOTE]
> Для проверки IP-потока требуется выделение ресурса виртуальной машины для выполнения.

## <a name="review-results"></a>Просмотр результатов

После выполнения командлет `network watcher ip-flow-verify` вернет результаты. Они представлены в следующем примере.

```
data:    Access                          : Deny
data:    Rule Name                       : defaultSecurityRules/DefaultInboundDenyAll
info:    network watcher ip-flow-verify command OK
```

## <a name="next-steps"></a>Дальнейшие действия

Если трафик блокируется, чего не должно быть, см. статью [Управление группами безопасности сети с помощью портала](../virtual-network/virtual-network-manage-nsg-arm-portal.md). В ней содержатся сведения об отслеживании группы безопасности сети и определенных правил безопасности.

Узнайте, как выполнить аудит параметров NSG, в статье [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) (Выполнение аудита групп безопасности сети с помощью Наблюдателя за сетями).

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png
