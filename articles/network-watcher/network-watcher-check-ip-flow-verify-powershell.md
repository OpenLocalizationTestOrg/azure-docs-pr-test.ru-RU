---
title: "Проверьте aaaverify трафика с потоком IP Наблюдатель сети Azure - PowerShell | Документы Microsoft"
description: "В этой статье описывается как toocheck, если разрешен или запрещен, с помощью PowerShell tooor трафик от виртуальной машины"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e1dad757-8c5d-467f-812e-7cc751143207
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 924da1de1bd554e15816886f8e51d7f170f0e7ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a>Проверьте, нельзя ли трафик разрешен или запрещен tooor из виртуальной Машины с потоком IP проверить компонент Наблюдатель сети Azure

> [!div class="op_single_selector"]
> - [Портал Azure](network-watcher-check-ip-flow-verify-portal.md)
> - [PowerShell](network-watcher-check-ip-flow-verify-powershell.md)
> - [Интерфейс командной строки 1.0](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-ip-flow-verify-cli.md)
> - [Azure REST API](network-watcher-check-ip-flow-verify-rest.md)


Проверьте IP потока — это функция Наблюдатель сети, который позволяет вам tooverify, если трафик tooor из виртуальной машины. Этот сценарий является полезным tooget текущее состояние ли виртуальной машины могут взаимодействовать tooan внешнего ресурса или внутреннего сервера. Проверьте IP потока может быть tooverify используется, если правила группы безопасности сети (NSG) правильно настроены и устранение неполадок потоки, которые заблокированы правила NSG. Кроме того, использует IP-адрес потока проверки tooensure трафика, что требуется заблокированных блокировано правильно hello NSG.

## <a name="before-you-begin"></a>Перед началом работы

Этот сценарий предполагает уже были выполнены шаги hello в [создать Наблюдатель сети](network-watcher-create.md) toocreate Наблюдатель сети или иметь существующий экземпляр Наблюдатель сети. сценарий Hello также предполагается, что группа ресурсов с действительной виртуальной машиной существует toobe используется.

## <a name="scenario"></a>Сценарий

Этот сценарий использует IP потока проверьте tooverify, если виртуальная машина может обмениваться информацией tooa известного Bing IP-адрес. Если трафик hello запрещен, он возвращает hello правило безопасности, блокирующее, трафик. Дополнительные сведения о потоке IP проверить, посетите toolearn [IP потока проверить Обзор](network-watcher-ip-flow-verify-overview.md)

## <a name="retrieve-network-watcher"></a>Извлечение Наблюдателя за сетями

Первым шагом Hello — экземпляр Наблюдатель сети tooretrieve hello. Hello `$networkWatcher` переменной передается toohello IP потока проверьте командлета.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a>Получение виртуальной машины

Поток IP проверьте tooor трафика тесты из IP-адреса виртуальной машины tooor из удаленного места назначения. Идентификатор виртуальной машины является обязательным для командлета hello. Если вы уже знаете идентификатор hello toouse hello виртуальной машины, этот шаг можно пропустить.

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="get-hello-nics"></a>Получить hello сетевых Адаптеров

в этом примере мы получить hello сетевых адаптеров на виртуальной машине требуется Hello IP-адрес сетевого адаптера на виртуальной машине hello. Если вы уже знаете hello IP адрес, о котором требуется tootest на виртуальной машине hello, этот шаг можно пропустить.

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="run-ip-flow-verify"></a>Выполнение проверки IP-потока

Теперь, когда есть hello сведения, необходимые toorun hello командлета, запустим hello `Test-AzureRmNetworkWatcherIPFlow` командлет tootest hello трафика. В этом примере мы используем hello первый IP-адрес первой hello сетевого адаптера.

```powershell
Test-AzureRmNetworkWatcherIPFlow -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id `
-Direction Outbound -Protocol TCP `
-LocalIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress -LocalPort 6895 -RemoteIPAddress 204.79.197.200 -RemotePort 80
```

> [!NOTE]
> Проверьте потока IP требует, что toorun распределения ресурсов виртуальной Машины hello.

## <a name="review-results"></a>Просмотр результатов

После выполнения команды `Test-AzureRmNetworkWatcherIPFlow` hello результаты возвращаются, hello следующий пример является hello результаты, возвращенные hello предыдущих шага.

```
Access RuleName                                  
------ --------                                  
Allow  defaultSecurityRules/AllowInternetOutBound
```

## <a name="next-steps"></a>Дальнейшие действия

Если трафик блокируется, и его не следует, см. раздел [Управление группами безопасности сети](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack вниз hello правила сетевой безопасности группы и безопасности, определенных.

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













