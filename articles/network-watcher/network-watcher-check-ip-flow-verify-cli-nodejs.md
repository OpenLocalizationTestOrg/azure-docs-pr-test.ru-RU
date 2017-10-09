---
title: "aaaVerify трафика с Azure сети наблюдателя IP потока проверить - Azure CLI | Документы Microsoft"
description: "В этой статье описывается как toocheck, если разрешен или запрещен, с помощью Azure CLI tooor трафик от виртуальной машины"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 92b857ed-c834-4c1b-8ee9-538e7ae7391d
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: c6becc5c142837b04d15490b2b3bd11124434570
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a>Проверьте, если трафик разрешен или запрещен tooor из виртуальной Машины с IP потока проверить компонент Наблюдатель сети Azure

> [!div class="op_single_selector"]
> - [Портал Azure](network-watcher-check-ip-flow-verify-portal.md)
> - [PowerShell](network-watcher-check-ip-flow-verify-powershell.md)
> - [Интерфейс командной строки 1.0](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-ip-flow-verify-cli.md)
> - [Azure REST API](network-watcher-check-ip-flow-verify-rest.md)


Поток IP проверка — это функция Наблюдатель сети, который позволяет вам tooverify, если трафик tooor из виртуальной машины. Этот сценарий является полезным tooget текущее состояние ли виртуальной машины могут взаимодействовать tooan внешнего ресурса или внутреннего сервера. Проверьте IP потока может быть tooverify используется, если правила группы безопасности сети (NSG) правильно настроены и устранение неполадок потоки, которые заблокированы правила NSG. Кроме того, использует IP-адрес потока проверки tooensure трафика, что требуется заблокированных блокировано правильно hello NSG.

В этой статье используется кроссплатформенной Azure CLI 1.0, доступный для Windows, Mac и Linux.

## <a name="before-you-begin"></a>Перед началом работы

Этот сценарий предполагает уже были выполнены шаги hello в [создать Наблюдатель сети](network-watcher-create.md) toocreate Наблюдатель сети или иметь существующий экземпляр Наблюдатель сети. сценарий Hello также предполагается, что группа ресурсов с действительной виртуальной машиной существует toobe используется.

## <a name="scenario"></a>Сценарий

В этом сценарии используется tooverify потока проверьте IP, если виртуальная машина может обмениваться информацией tooa известного Bing IP-адрес. Если трафик hello запрещен, он возвращает hello правило безопасности, блокирующее, трафик. Посетите toolearn Дополнительные сведения о IP потока проверить, [Обзор потока проверьте IP](network-watcher-ip-flow-verify-overview.md)


## <a name="get-a-vm"></a>Получение виртуальной машины

Поток IP проверьте tooor трафика тесты из IP-адреса виртуальной машины tooor из удаленного места назначения. Идентификатор виртуальной машины является обязательным для командлета hello. Если вы уже знаете идентификатор hello toouse hello виртуальной машины, этот шаг можно пропустить.

```
azure vm show -g resourceGroupName -n virtualMachineName
```

## <a name="get-hello-nics"></a>Получить hello сетевых Адаптеров

в этом примере мы получить hello сетевых адаптеров на виртуальной машине требуется Hello IP-адрес сетевого адаптера на виртуальной машине hello. Если вы уже знаете hello IP адрес, о котором требуется tootest на виртуальной машине hello, этот шаг можно пропустить.

```
azure network nic show -g resourceGroupName -n nicName
```

## <a name="run-ip-flow-verify"></a>Выполнение проверки IP-потока

Теперь, когда есть hello сведения, необходимые toorun hello командлета, запустим hello `network watcher ip-flow-verify` командлет tootest hello трафика. В этом примере мы используем hello первый IP-адрес первой hello сетевого адаптера.

```
azure network watcher ip-flow-verify -g resourceGroupName -n networkWatcherName -t targetResourceId -d directionInboundorOutbound -p protocolTCPorUDP -o localPort -m remotePort -l localIpAddr -r remoteIpAddr
```

> [!NOTE]
> Поток IP проверка требует, что toorun распределения ресурсов виртуальной Машины hello.

## <a name="review-results"></a>Просмотр результатов

После выполнения команды `network watcher ip-flow-verify` hello результаты возвращаются, hello следующий пример является hello результаты, возвращенные hello предыдущих шага.

```
data:    Access                          : Deny
data:    Rule Name                       : defaultSecurityRules/DefaultInboundDenyAll
info:    network watcher ip-flow-verify command OK
```

## <a name="next-steps"></a>Дальнейшие действия

Если трафик блокируется, и его не следует, см. раздел [Управление группами безопасности сети](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack вниз hello правила сетевой безопасности группы и безопасности, определенных.

Сведения tooaudit параметры NSG получить [аудита безопасности сети группы (NSG) с Наблюдатель сети](network-watcher-nsg-auditing-powershell.md).

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png
