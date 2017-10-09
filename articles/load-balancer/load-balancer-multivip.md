---
title: "aaaMutiple виртуальные IP-адреса для облачной службы"
description: "Общие сведения о multiVIP и как tooset несколько виртуальных IP-адресов в облачной службе"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: 85f6d26a-3df5-4b8e-96a1-92b2793b5284
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: b3e0f2b24968cb75a7064484a09ffe94505bb70b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multiple-vips-for-a-cloud-service"></a>Настройка нескольких виртуальных IP-адресов для облачной службы

Облачные службы Azure для доступа к hello общедоступный Интернет с помощью IP-адрес, предоставленный службой Azure. Этот общедоступный IP-адрес является ссылка tooas виртуального IP-адреса (виртуальный IP-адрес), так как он связан toohello Azure подсистемы балансировки нагрузки, а не hello в облачную службу hello экземпляров виртуальной машины (VM). Доступ к любому экземпляру виртуальной машины в облачной службе можно получить с помощью одного виртуального IP-адреса.

Однако существуют сценарии, в которых может потребоваться более одного виртуального IP-адреса в качестве точки входа toohello же облачной службе. Например облачной службы может содержать несколько веб-сайтов, требующих подключения SSL, с использованием порта 443, по умолчанию hello, как каждый сайт размещается для другого клиента или клиента. В этом случае необходимо toohave другой открытый IP-адреса для каждого веб-сайта. Hello схеме ниже показан типичный несколькими клиентами размещения веб-сайтов с необходимостью несколько SSL-сертификатов на hello же открытый порт.

![Сценарий SSL с несколькими виртуальными IP-адресами](./media/load-balancer-multivip/Figure1.png)

В примере hello выше, все виртуальные IP-адреса используйте hello же открытый порт (443) и трафик перенаправленный tooone или более нагрузки взаимосвязанных виртуальных машин на уникальный частный порт для hello внутренний IP-адрес облачной службы hello размещение всех hello веб-сайтов.

> [!NOTE]
> Другой используйте hello требующих hello ситуации несколько виртуальных IP-адресов размещается несколько прослушивателей группы доступности SQL AlwaysOn в hello же набор виртуальных машин.

Виртуальные IP-адреса являются динамическими по умолчанию, это означает, что со временем может меняться hello фактических IP-адрес toohello облачной службы. tooprevent, ситуации, вы можете зарезервировать VIP-адрес для службы. toolearn Дополнительные сведения о зарезервированных виртуальных IP-адресов в разделе [зарезервированный общедоступный IP-адрес](../virtual-network/virtual-networks-reserved-public-ip.md).

> [!NOTE]
> Информацию о ценах на виртуальные IP-адреса и зарезервированные IP-адреса см. на странице [Цены на IP-адреса](https://azure.microsoft.com/pricing/details/ip-addresses/).

Можно использовать PowerShell tooverify hello виртуальные IP-адреса, используемые облачных служб, а также добавить и удалить виртуальные IP-адреса, связать конечную точку tooan виртуального IP-адреса и Настройка балансировки нагрузки в конкретных виртуальных IP-адресов.

## <a name="limitations"></a>Ограничения

В настоящее время функциональные возможности нескольких виртуальных IP-адресов является ограниченной toohello следующие сценарии:

* **Только IaaS**. Вы можете включить несколько виртуальных IP-адресов для облачных служб, содержащих виртуальные машины. Нельзя использовать несколько виртуальных IP-адресов в сценариях PaaS с экземплярами ролей.
* **Только PowerShell**. Несколькими виртуальными IP-адресами можно управлять только с помощью PowerShell.

Эти ограничения являются временными и могут измениться в любое время. Убедитесь, что toorevisit tooverify будущие изменения этой страницы.

## <a name="how-tooadd-a-vip-tooa-cloud-service"></a>Как tooa tooadd VIP облачной службы
tooyour службе tooadd VIP-адрес, выполните следующую команду PowerShell hello:

```powershell
Add-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

Эта команда выводит примерно toohello результат, следующий пример:

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Add-AzureVirtualIP   4bd7b638-d2e7-216f-ba38-5221233d70ce Succeeded

## <a name="how-tooremove-a-vip-from-a-cloud-service"></a>Как tooremove VIP-адрес из облачной службы
в примере hello выше выполнения hello следующую команду PowerShell hello tooremove виртуальных IP-адресов добавлены tooyour службы:

```powershell
Remove-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

> [!IMPORTANT]
> VIP-адрес можно удалить только в том случае, если у него есть не tooit конечных точек, связанных.


## <a name="how-tooretrieve-vip-information-from-a-cloud-service"></a>Каким образом сведения tooretrieve виртуальных IP-адресов из облачной службы
hello tooretrieve виртуальные IP-адреса связанный с облачной службой, запустите следующий сценарий PowerShell hello:

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

сценарий Hello отображает результат аналогичные toohello, следующий пример:

    Address         : 191.238.74.148
    IsDnsProgrammed : True
    Name            : Vip1
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip2
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip3
    ReservedIPName  :
    ExtensionData   :

В этом примере hello облачная служба имеет 3 виртуальные IP-адреса:

* **Vip1** Здравствуйте виртуальных IP-адресов по умолчанию, вам известно, что поскольку hello для IsDnsProgrammedName значение tootrue.
* **Vip2** и **Vip3** не используются, так как они не имеют IP-адресов. Они будут использоваться только в том случае, если вы связываете конечной точки toohello виртуальных IP-адресов.

> [!NOTE]
> За использование дополнительных виртуальных IP-адресов в подписке начнет взиматься плата, когда они будут связаны с конечной точкой. Дополнительную информацию о ценах см. на странице [Цены на IP-адреса](https://azure.microsoft.com/pricing/details/ip-addresses/).

## <a name="how-tooassociate-a-vip-tooan-endpoint"></a>Как конечная точка tooan tooassociate VIP-адрес

tooassociate VIP-адрес в облаке tooan конечную точку службы, запустите следующую команду PowerShell hello:

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -Protocol tcp -LocalPort 8080 -PublicPort 80 -VirtualIPName Vip2 |
    Update-AzureVM
```

Hello команда создает конечная точка с именем виртуальный IP-адрес связанного toohello *Vip2* через порт *80*и связывает его toohello виртуальной Машины с именем *myVM1* в облачной службе с именем  *myService* с помощью *TCP* через порт *8080*.

tooverify конфигурация hello, запустите следующую команду PowerShell hello:

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

Hello выходные данные выглядят аналогично toohello в следующем примере:

    Address         : 191.238.74.148
    IsDnsProgrammed : True
    Name            : Vip1
    ReservedIPName  :
    ExtensionData   :

    Address         : 191.238.74.13
    IsDnsProgrammed :
    Name            : Vip2
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip3
    ReservedIPName  :
    ExtensionData   :

## <a name="how-tooenable-load-balancing-on-a-specific-vip"></a>Как tooenable балансировку нагрузки для определенного виртуального IP-адреса

Вы можете связать один виртуальный IP-адрес с несколькими виртуальными машинами для балансировки нагрузки. Например, у вас есть облачная служба с именем *myService* и две виртуальные машины с именами *myVM1* и *myVM2*. Облачная служба имеет несколько виртуальных IP-адресов, имя одного из которых — *Vip2*. Если требуется, весь трафик tooport tooensure *81* на *Vip2* распределяются между *myVM1* и *myVM2* через порт *8181* , запустите hello следующий сценарий PowerShell:

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2 -DefaultProbe |
    Update-AzureVM

Get-AzureVM -ServiceName myService -Name myVM2 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2  -DefaultProbe |
    Update-AzureVM
```

Можно также обновить ваш toouse подсистемы балансировки нагрузки различных виртуальных IP-адресов. Например при запуске hello следующую команду PowerShell, мы изменим hello балансировки toouse набора виртуальных IP-адресов, с именем Vip1:

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName myService -LBSetName myLBSet -VirtualIPName Vip1
```

## <a name="next-steps"></a>Дальнейшие действия

[Служба анализа журналов для балансировщика нагрузки Azure (предварительная версия)](load-balancer-monitor-log.md)

[Обзор подсистемы балансировки нагрузки, доступной в Интернете](load-balancer-internet-overview.md)

[Приступая к работе с подсистемой балансировки нагрузки, доступной в Интернете](load-balancer-get-started-internet-arm-ps.md)

[Обзор виртуальной сети](../virtual-network/virtual-networks-overview.md)

[API REST зарезервированных IP-адресов](https://msdn.microsoft.com/library/azure/dn722420.aspx)
