---
title: "Следующий прыжок aaaFind с Azure сети наблюдателя следующего прыжка — Azure CLI 1.0 | Документы Microsoft"
description: "В этой статье описывается, как можно найти какие hello тип следующего прыжка — и адрес ip с помощью следующего прыжка с помощью Azure CLI."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 0700c274-3e0d-4dca-acfa-3ceac8990613
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 54124c051021413695d70ba93c370605abc6ebbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-azure-cli-10"></a>Узнать, какой тип следующего прыжка hello является использование возможностей следующего прыжка hello в Наблюдатель сети Azure с помощью Azure CLI 1.0

> [!div class="op_single_selector"]
> - [Портал Azure](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [Интерфейс командной строки 1.0](network-watcher-check-next-hop-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-next-hop-cli.md)
> - [Azure REST API](network-watcher-check-next-hop-rest.md)

Следующий прыжок является компонентом Наблюдатель сети, который предоставляет возможность hello получить тип следующего прыжка hello и IP-адрес, на основе указанной виртуальной машины. Эта функция полезна при определении Если пакетов, отправляемых виртуальная машина проходит через шлюз, Интернет или назначения tooits tooget виртуальных сетей.

В этой статье используется кроссплатформенной Azure CLI 1.0, доступный для Windows, Mac и Linux.

## <a name="before-you-begin"></a>Перед началом работы

В этом сценарии используется hello тип следующего прыжка Azure CLI toofind hello и IP-адрес.

Этот сценарий предполагает уже были выполнены шаги hello в [создать Наблюдатель сети](network-watcher-create.md) toocreate Наблюдатель сети. сценарий Hello также предполагается, что группа ресурсов с действительной виртуальной машиной существует toobe используется.

## <a name="scenario"></a>Сценарий

Hello сценарии, описанные в данной статье используется следующего прыжка, функция Наблюдатель сети, извлекают тип следующего прыжка hello и IP-адрес для ресурса. Посетите toolearn Дополнительные сведения о следующего прыжка [следующего прыжка Обзор](network-watcher-next-hop-overview.md).


## <a name="get-next-hop"></a>Получение следующего прыжка

Следующий прыжок tooget hello мы называем hello `azure netowrk watcher next-hop` командлета. Мы передаем группы ресурсов Наблюдатель сети hello командлет hello, hello NetworkWatcher, виртуальной машины идентификатор, исходный IP-адрес и IP-адрес назначения. В этом примере hello конечный IP-адрес — tooa виртуальной Машины в другой виртуальной сети. Нет шлюза виртуальной сети между двумя виртуальными сетями hello. 

```azurecli
azure network watcher next-hop -g resourceGroupName -n networkWatcherName -t targetResourceId -a <source-ip> -d <destination-ip>
```

> [!NOTE]
Если hello виртуальной Машины имеет несколько сетевых адаптеров и IP-пересылки включен на всех сетевых адаптеров hello, hello параметров сетевого Адаптера (-я nic-id) должно быть указано. В противном случае этот параметр является необязательным.

## <a name="review-results"></a>Просмотр результатов

По завершении приведены результаты hello. а также hello тип ресурса, который является возвращается IP-адрес следующего прыжка Hello.

```
data:    Next Hop Ip Address             : 10.0.1.2
info:    network watcher next-hop command OK
```

Hello ниже перечислены в настоящее время доступных значений NextHopType hello.

**Типы следующего прыжка**

* Интернет
* VirtualAppliance
* VirtualNetworkGateway
* VnetLocal
* HyperNetGateway
* VnetPeering
* None

## <a name="next-steps"></a>Дальнейшие действия

Узнайте, как tooreview параметров группы безопасности сети программным способом, посетив [NSG аудита и Наблюдатель сети](network-watcher-nsg-auditing-powershell.md)
