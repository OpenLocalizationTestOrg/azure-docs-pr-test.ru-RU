---
title: "Получение таблиц ARP. Устранение неполадок ExpressRoute (Resource Manager) | Документация Майкрософт"
description: "Эта страница содержит инструкции по получении hello ARP таблицы за канал ExpressRoute"
documentationcenter: na
services: expressroute
author: ganesr
manager: carolz
editor: tysonn
ms.assetid: 0a6bf1d5-6baf-44dd-87d3-1ebd2fd08bdc
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/30/2017
ms.author: ganesr
ms.openlocfilehash: c386b031814d40ef6ea3ce5e0eaaab9634470e8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="getting-arp-tables-in-hello-resource-manager-deployment-model"></a>Получение ARP таблиц в модели развертывания диспетчера ресурсов hello
> [!div class="op_single_selector"]
> * [PowerShell — Resource Manager](expressroute-troubleshooting-arp-resource-manager.md)
> * [PowerShell — классическая модель](expressroute-troubleshooting-arp-classic.md)
> 
> 

В этой статье рассматриваются hello действия toolearn приветствия таблицы ARP для своего канала ExpressRoute. 

> [!IMPORTANT]
> Данный документ является предполагаемым toohelp диагностики и устранения проблем простой. Это не toobe предназначен для замены технической поддержки Майкрософт. Необходимо открыть запрос в службу поддержки с [поддержки Майкрософт](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) Если проблему не удается toosolve hello, с помощью hello рекомендации, описанные ниже.
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a>Протокол ARP и таблицы ARP
Протокол ARP — это протокол уровня 2, определенный в стандарте [RFC 826](https://tools.ietf.org/html/rfc826). ARP — используется toomap hello Ethernet-адреса (MAC-адрес) IP-адрес.

Hello таблицы ARP содержит сопоставления hello ipv4-адреса и MAC-адрес для конкретного пиринга. Hello таблицы ARP для пиринга ExpressRoute цепь предоставляет следующую информацию для каждого интерфейса (первичная и Вторичная) hello

1. Сопоставление локального маршрутизатора IP-адрес toohello MAC адрес интерфейса
2. Сопоставление ExpressRoute интерфейса IP-адрес toohello MAC адреса маршрутизатора
3. Срок действия сопоставления hello

Таблицы ARP помогают проверить конфигурацию уровня 2 и устранить проблемы с подключением на базовом уровне 2. 

Пример таблицы ARP. 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


Hello следующий раздел содержит сведения о том, как можно просмотреть hello таблицы ARP просмотрен hello ExpressRoute периметрическими маршрутизаторами. 

## <a name="prerequisites-for-learning-arp-tables"></a>Необходимые условия для изучения таблиц ARP
Убедитесь, что следующие hello перед дальнейшей работе

* Настроен действительный канал ExpressRoute по крайней мере с одним пирингом. Hello канала должен быть настроен с поставщиком услуг подключения hello полностью. Вы (или поставщиком соединения) необходимо настроить хотя бы один из пиринги hello (Azure открытого, закрытого, Azure и Microsoft) для этой цепи.
* Диапазоны IP-адресов, используемым для настройки пиринги hello (Azure открытого, закрытого, Azure и Microsoft). Просмотрите примеры hello IP-адресов назначения в hello [странице требований маршрутизации ExpressRoute](expressroute-routing.md) tooget представление о том, как IP-адресов, сопоставленный toointerfaces с вашей стороны и на стороне ExpressRoute hello. Сведения о конфигурации пиринга hello можно получить, просмотрев hello [странице конфигурации пиринга ExpressRoute](expressroute-howto-routing-arm.md).
* Сведения для команды, сети и использовать поставщика услуг подключения на hello MAC-адреса интерфейсов с этих IP-адресов.
* Необходимо иметь hello последнюю версию модуля PowerShell для Azure (версия 1,50 или более поздней версии).

## <a name="getting-hello-arp-tables-for-your-expressroute-circuit"></a>Получение таблиц hello ARP для своего канала ExpressRoute
Этот раздел предоставляет инструкции по как можно просмотреть hello таблицы ARP на пиринг с помощью PowerShell. Вы или поставщиком соединения следует настроить пиринг hello, прежде чем углубляться в дальнейшей. Каждый канал имеет два пути (первичный и вторичный). Вы можете проверить hello таблицы ARP для каждого пути независимо друг от друга.

### <a name="arp-tables-for-azure-private-peering"></a>Таблицы ARP для частного пиринга Azure
Привет, выполнив командлет предоставляет hello ARP таблиц для открытого пиринга Azure

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure private peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Primary

        # ARP table for Azure private peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Secondary 

Ниже приведен пример выходных данных для одного пути hello

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a>Таблицы ARP для общедоступного пиринга Azure
Привет, выполнив командлет предоставляет hello ARP таблиц для частного пиринга Azure

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure public peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Primary

        # ARP table for Azure public peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Secondary 


Ниже приведен пример выходных данных для одного пути hello

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1   ffff.eeee.dddd
          0 Microsoft         64.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a>Таблицы ARP для пиринга Майкрософт
Привет, выполнив командлет предоставляет hello ARP таблиц для пиринг Майкрософт

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Microsoft peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Primary

        # ARP table for Microsoft peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Secondary 


Ниже приведен пример выходных данных для одного пути hello

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


## <a name="how-toouse-this-information"></a>Как toouse эти сведения
Hello таблицы ARP пиринга используется toodetermine проверить подключение и настройка уровня 2. В этом разделе описывается, как будут выглядеть таблицы ARP в различных сценариях.

### <a name="arp-table-when-a-circuit-is-in-operational-state-expected-state"></a>Таблица ARP, когда канал находится в рабочем состоянии (ожидаемое состояние)
* Hello таблицы ARP будет создана запись с допустимым IP-адреса и MAC-адрес на стороне локальной hello и аналогичный элемент для hello стороны Майкрософт. 
* последний октет Hello hello локального IP-адреса всегда будет нечетным числом.
* последний октет hello IP-адрес Microsoft Hello всегда будет четное число.
* Здравствуйте, одинаковый MAC-адрес будет отображаться в hello стороны Майкрософт для всех 3 пиринги (первичного или вторичного). 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

### <a name="arp-table-when-on-premises--connectivity-provider-side-has-problems"></a>Таблица ARP в случае проблем на стороне локальной сети или поставщика услуг подключения
Если возникли проблемы с hello в локальной или поставщика услуг подключения может появиться, либо только одна запись появится в hello ARP таблицы или hello локальный MAC-адрес будет отображать неполные. При этом будут отображены сопоставление hello hello MAC-адрес и IP-адреса в hello стороны Майкрософт. 
  
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------    
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

или
       
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------   
         0 On-Prem           65.0.0.1   Incomplete
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


> [!NOTE]
> Запрос в службу поддержки с вашей toodebug подключения поставщика подобные проблемы. Если hello таблицы ARP отсутствует IP-адресов интерфейсов hello сопоставляются tooMAC адреса, hello просмотрите следующую информацию:
> 
> 1. Если назначена hello первый IP-адрес подсети hello /30 для hello связь между hello MSEE PR и MSEE используется в интерфейсе hello MSEE PR. Azure всегда использует hello второй IP-адрес для MSEEs.
> 2. Убедитесь, если hello клиента (C-тег) и теги VLAN службы (S-Tag) соответствуют на пару MSEE PR и MSEE.
> 

### <a name="arp-table-when-microsoft-side-has-problems"></a>Таблица ARP в случае проблем на стороне сети Майкрософт
* Таблицы ARP, показанный для пиринга при возникновении проблем на стороне Microsoft hello не будет. 
* Отправьте запрос в [службу поддержки Майкрософт](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). Укажите, что у вас проблема с подключением уровня 2. 

## <a name="next-steps"></a>Дальнейшие действия
* Проверка конфигураций уровня 3 для канала ExpressRoute.
  * Получение состояния hello маршрута сводки toodetermine сеансов BGP 
  * Получить какие префиксов объявленных через ExpressRoute toodetermine таблицы маршрутов
* Проверка передачи данных путем просмотра входящих и выходящих байтов.
* Отправьте запрос в [службу поддержки Майкрософт](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) , если у вас по-прежнему возникают проблемы.

