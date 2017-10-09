---
title: "Следующий прыжок aaaFind с Azure сети наблюдателя следующего прыжка — PowerShell | Документы Microsoft"
description: "В этой статье описывается, как можно найти какие hello тип следующего прыжка — и адрес ip с помощью следующего прыжка с помощью PowerShell."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 6a656c55-17bd-40f1-905d-90659087639c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fdb0b4a02d95fc45c103fe952fc1afa095414c18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-powershell"></a>Узнать, какой тип следующего прыжка hello является использование возможностей следующего прыжка hello в Наблюдатель сети Azure с помощью PowerShell

> [!div class="op_single_selector"]
> - [Портал Azure](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [Интерфейс командной строки 1.0](network-watcher-check-next-hop-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-next-hop-cli.md)
> - [Azure REST API](network-watcher-check-next-hop-rest.md)

Следующий прыжок является компонентом Наблюдатель сети, который предоставляет возможность hello получить тип следующего прыжка hello и IP-адрес, на основе указанной виртуальной машины. Эта функция полезна при определении Если пакетов, отправляемых виртуальная машина проходит через шлюз, Интернет или назначения tooits tooget виртуальных сетей.

## <a name="before-you-begin"></a>Перед началом работы

В этом сценарии используется hello тип следующего прыжка Azure портала toofind hello и IP-адрес.

Этот сценарий предполагает уже были выполнены шаги hello в [создать Наблюдатель сети](network-watcher-create.md) toocreate Наблюдатель сети. сценарий Hello также предполагается, что группа ресурсов с действительной виртуальной машиной существует toobe используется.

## <a name="scenario"></a>Сценарий

Hello сценарии, описанные в данной статье используется следующего прыжка, функция Наблюдатель сети, извлекают тип следующего прыжка hello и IP-адрес для ресурса. Посетите toolearn Дополнительные сведения о следующего прыжка [следующего прыжка Обзор](network-watcher-next-hop-overview.md).

## <a name="retrieve-network-watcher"></a>Извлечение Наблюдателя за сетями

Первым шагом Hello — экземпляр Наблюдатель сети tooretrieve hello. Hello `$networkWatcher` переменной передается toohello следующего прыжка проверка командлета.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-virtual-machine"></a>Получение виртуальной машины

Следующий прыжок возвращает следующего прыжка hello и hello IP-адрес следующего прыжка hello из виртуальной машины. Идентификатор виртуальной машины является обязательным для командлета hello. Если вы уже знаете идентификатор hello toouse hello виртуальной машины, этот шаг можно пропустить.

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

> [!NOTE]
> Следующий прыжок требуется что toorun распределения ресурсов виртуальной Машины hello.

## <a name="get-hello-network-interfaces"></a>Получить hello сетевых интерфейсов

в этом примере мы получить hello сетевых адаптеров на виртуальной машине требуется Hello IP-адрес сетевого адаптера на виртуальной машине hello. Если вы уже знаете hello IP адрес, о котором требуется tootest на виртуальной машине hello, этот шаг можно пропустить.

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="get-next-hop"></a>Получение следующего прыжка

Теперь мы называем hello `Get-AzureRmNetworkWatcherNextHop` командлета. Мы передайте hello командлет hello Наблюдатель сети виртуальной машины идентификатор, исходный IP-адрес и IP-адрес назначения. В этом примере hello конечный IP-адрес — tooa виртуальной Машины в другой виртуальной сети. Нет шлюза виртуальной сети между двумя виртуальными сетями hello.

```powershell
Get-AzureRmNetworkWatcherNextHop -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id -SourceIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress  -DestinationIPAddress 10.0.2.4 
```

## <a name="review-results"></a>Просмотр результатов

По завершении приведены результаты hello. а также hello тип ресурса, который является возвращается IP-адрес следующего прыжка Hello. В этом случае это hello общедоступный IP-адрес шлюза виртуальной сети hello.

```
NextHopIpAddress NextHopType           RouteTableId 
---------------- -----------           ------------ 
13.78.238.92     VirtualNetworkGateway Gateway Route
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

















