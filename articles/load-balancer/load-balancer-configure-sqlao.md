---
title: "aaaConfigure балансировки нагрузки для SQL всегда on | Документы Microsoft"
description: "Настроить toowork подсистемы балансировки нагрузки с помощью SQL всегда на и как tooleverage powershell toocreate Подсистема балансировки нагрузки для реализации SQL hello"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: d7bc3790-47d3-4e95-887c-c533011e4afd
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: ac6200b18f725dadee2555b80055327d379417d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-load-balancer-for-sql-always-on"></a>Настройка подсистемы балансировки нагрузки для AlwaysOn SQL

Группы доступности AlwaysOn SQL Server теперь можно использовать совместно с внутренней подсистемой балансировки нагрузки. Группа доступности — это флагманское решение SQL Server, обеспечивающее высокий уровень доступности и аварийное восстановление. Hello прослушивателя группы доступности позволяет клиентским приложениям tooseamlessly подключения toohello первичной реплике, независимо от hello число реплик hello в конфигурации hello.

Hello имя прослушивателя (DNS) — IP-адрес сопоставленных tooa балансировки нагрузки и балансировку нагрузки Azure направляет hello входящего трафика tooonly hello сервера-источника в наборе реплик hello.

Поддержку внутренней подсистемы балансировки нагрузки можно использовать для конечных точек (прослушивателя) AlwaysOn SQL Server. Теперь могут контролировать доступность hello hello прослушивателя и выберите hello балансировкой нагрузки IP-адрес из определенной подсети в виртуальной сети (VNet).

Используя ILB hello прослушивателя, hello конечной точки SQL server (например, Server = tcp:ListenerName, 1433, базы данных = имя базы данных), доступен только для:

* Службы и виртуальные машины в hello одной виртуальной сети
* Службы и виртуальные машины из подключенной локальной сети
* Службы и виртуальные машины из взаимосвязанных виртуальных сетей

![ILB_SQLAO_NewPic](./media/load-balancer-configure-sqlao/sqlao1.png)

Рис. 1. Группа SQL AlwaysOn, в которой настроена подсистема балансировки нагрузки с выходом в Интернет

## <a name="add-internal-load-balancer-toohello-service"></a>Добавление службы toohello внутренней подсистемы балансировки нагрузки

1. На следующий пример hello мы Настройка виртуальной сети, содержащей подсеть с именем «подсеть-1".

    ```powershell
    Add-AzureInternalLoadBalancer -InternalLoadBalancerName ILB_SQL_AO -SubnetName Subnet-1 -ServiceName SqlSvc
    ```
2. Добавление конечных точек с балансировкой нагрузки для внутренней подсистемы балансировки нагрузки на каждой виртуальной машине

    ```powershell
    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc1 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -
    DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM

    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc2 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM
    ```

    В приведенном выше примере hello, у вас есть 2 ВМ вызываемой «sqlsvc1» и «sqlsvc2» работает в облаке hello службы «Sqlsvc». После создания hello ILB с `DirectServerReturn` переключения, можно добавить конечные точки с балансировкой toohello ILB tooallow SQL tooconfigure hello прослушиватели группы доступности hello загрузки.

Подробные указания см. в статье [Настройка внутреннего балансировщика нагрузки для группы доступности AlwaysOn в Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).

## <a name="see-also"></a>См. также
[Приступая к настройке подсистемы балансировки нагрузки, доступной в Интернете](load-balancer-get-started-internet-arm-ps.md)

[Приступая к настройке внутренней подсистемы балансировки нагрузки](load-balancer-get-started-ilb-arm-ps.md)

[Настройка режима распределения подсистемы балансировки нагрузки](load-balancer-distribution-mode.md)

[Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки](load-balancer-tcp-idle-timeout.md)
