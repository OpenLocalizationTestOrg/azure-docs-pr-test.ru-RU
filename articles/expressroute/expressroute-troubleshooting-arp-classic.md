---
title: "Получение таблиц ARP. Устранение неполадок ExpressRoute (классическая модель) | Документация Майкрософт"
description: "Эта страница содержит инструкции по началу hello ARP таблицы за канал ExpressRoute."
documentationcenter: na
services: expressroute
author: ganesr
manager: carolz
editor: tysonn
ms.assetid: b5856acf-03c2-4933-8111-6ce12998d92a
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/30/2017
ms.author: ganesr
ms.openlocfilehash: 2b01304a38fa0e0def27dbd7c391d7ad8bbdabff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="getting-arp-tables-in-hello-classic-deployment-model"></a>Получение таблицы ARP в hello классической модели развертывания
> [!div class="op_single_selector"]
> * [PowerShell — Resource Manager](expressroute-troubleshooting-arp-resource-manager.md)
> * [PowerShell — классическая модель](expressroute-troubleshooting-arp-classic.md)
> 
> 

В этой статье содержится описание этапов hello для получения таблиц hello протокола разрешения адресов (ARP) для своего канала Azure ExpressRoute.

> [!IMPORTANT]
> Данный документ является предполагаемым toohelp диагностики и устранения проблем простой. Это не toobe предназначен для замены технической поддержки Майкрософт. Если не удается решить проблему hello с помощью hello следующие рекомендации, запрос в службу поддержки с [Microsoft Azure Справка и поддержка](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a>Протокол ARP и таблицы ARP
ARP — это протокол уровня 2, который определен в [RFC 826](https://tools.ietf.org/html/rfc826). ARP — используется toomap Ethernet (MAC-адрес) tooan IP-адрес.

Таблицы ARP содержит сопоставления hello IPv4-адреса и MAC-адрес для конкретного пиринга. Hello таблицы ARP для пиринга ExpressRoute цепь предоставляет hello следующую информацию для каждого интерфейса (первичная и Вторичная).

1. Сопоставление локального маршрутизатора IP-адрес tooa MAC адрес интерфейса
2. Сопоставление ExpressRoute маршрутизатора интерфейса IP-адрес tooa MAC адреса
3. Возраст Hello hello сопоставления

Таблицы ARP помогают проверять конфигурацию уровня 2 и устранять проблемы с подключением на базовом уровне 2.

Ниже приведен пример таблицы ARP.

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


Hello следующий раздел содержит сведения о как tooview hello таблицы ARP, видимые hello ExpressRoute периметрическими маршрутизаторами.

## <a name="prerequisites-for-using-arp-tables"></a>Необходимые условия для использования таблиц ARP
Убедитесь, что следующие hello перед продолжением:

* Настроен действительный канал ExpressRoute по крайней мере с одним пирингом. Hello канала должен быть настроен с поставщиком услуг подключения hello полностью. Вы (или поставщиком соединения) необходимо настроить хотя бы один из пиринги hello (Azure открытого, закрытого, Azure или Майкрософт) для этой цепи.
* Диапазоны IP-адресов, которые используются для настройки пиринги hello (Azure открытого, закрытого, Azure и Microsoft). Просмотрите примеры hello IP-адресов назначения в hello [странице требований маршрутизации ExpressRoute](expressroute-routing.md) tooget представление о том, как IP-адресов, сопоставленный toointerfaces на ваш aise и на стороне ExpressRoute hello. Сведения о конфигурации пиринга hello можно получить, просмотрев hello [странице конфигурации пиринга ExpressRoute](expressroute-howto-routing-classic.md).
* Сведения от поставщика сетевых команды или подключения к MAC-адреса hello hello интерфейсов, которые используются с этих IP-адресов.
* Hello последнюю версию модуля Windows PowerShell для Azure (версия 1.50 или более поздней версии).

## <a name="arp-tables-for-your-expressroute-circuit"></a>Таблицы ARP для канала ExpressRoute
Этот раздел содержит инструкции о как tooview hello ARP таблицы для каждого типа пиринг с помощью PowerShell. Прежде чем продолжить, вы или поставщиком соединения должен пиринг tooconfigure hello. Каждый канал имеет два пути (первичный и вторичный). Вы можете проверить hello таблицы ARP для каждого пути независимо друг от друга.

### <a name="arp-tables-for-azure-private-peering"></a>Таблицы ARP для частного пиринга Azure
Привет, выполнив командлет предоставляет hello ARP таблиц для открытого пиринга Azure:

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure private peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Primary

        # ARP table for Azure private peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Secondary

Ниже приведен пример выходных данных в один из путей hello.

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a>Таблицы ARP для общедоступного пиринга Azure
Привет, выполнив командлет предоставляет hello ARP таблиц для частного пиринга Azure.

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure public peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Primary

        # ARP table for Azure public peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Secondary

Ниже приведен пример выходных данных в один из путей hello.

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


Ниже приведен пример выходных данных в один из путей hello.

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1 ffff.eeee.dddd
          0 Microsoft         64.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a>Таблицы ARP для пиринга Майкрософт
Привет, выполнив командлет предоставляет hello ARP таблиц пиринг Майкрософт:

    # ARP table for Microsoft peering--primary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Primary

    # ARP table for Microsoft peering--secondary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Secondary


Ниже приведен пример выходных данных для одного пути hello:

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc


## <a name="how-toouse-this-information"></a>Как toouse эти сведения
Hello таблицы ARP пиринга может быть конфигурации используется toovalidate уровня 2 и подключение. В этом разделе описывается, как выглядят таблицы ARP в различных сценариях.

### <a name="arp-table-when-a-circuit-is-in-an-operational-expected-state"></a>Таблица ARP, когда канал находится в рабочем состоянии (ожидаемое состояние)
* Hello таблицы ARP имеет запись hello локальной стороне с допустимым IP- и MAC-адресом и аналогичные запись для hello стороны Майкрософт.
* последний октет Hello hello локального IP-адреса всегда является нечетным числом.
* последний октет Hello hello Microsoft IP-адреса всегда является четным числом.
* Здравствуйте, одинаковый MAC-адрес отображается на hello стороны Майкрософт для всех трех пиринги (первичный или вторичный).

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

### <a name="arp-table-when-its-on-premises-or-when-hello-connectivity-provider-side-has-problems"></a>Таблицы ARP, когда она локальной или когда стороны поставщика услуг подключения hello имеется проблем
 В таблицы ARP hello отображается только одна запись. Здесь показано сопоставление hello hello MAC-адрес и hello IP-адрес, который используется на стороне Microsoft hello.

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

> [!NOTE]
> При возникновении такую проблему, откройте поддержки запросов с вашей tooresolve подключения поставщика.
> 
> 

### <a name="arp-table-when-hello-microsoft-side-has-problems"></a>Таблицы ARP hello Microsoft side проблемы при
* Таблицы ARP, показанный для пиринга при возникновении проблем на стороне Microsoft hello не будет.
* Отправьте запрос на поддержку с помощью функции [Справка и поддержка Microsoft Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). Укажите, что у вас возникла проблема с возможностями подключения уровня 2.

## <a name="next-steps"></a>Дальнейшие действия
* Проверка конфигураций уровня 3 для канала ExpressRoute.
  * Отслеживает состояние hello маршрута сводки toodetermine сеансов BGP.
  * Получите toodetermine таблицы маршрутов, какие префиксов объявленных через ExpressRoute.
* Проверка передачи данных путем просмотра входящих и исходящих байтов.
* Отправьте запрос на поддержку с помощью функции [Справка и поддержка Microsoft Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) , если у вас по-прежнему возникают проблемы.

