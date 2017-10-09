---
title: "Подсистема балансировки - нагрузки на aaaCreate из Интернета, Azure PowerShell классический | Документы Microsoft"
description: "Узнайте, как из Интернета toocreate Подсистема балансировки загрузки в классическом режиме, с помощью PowerShell"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 73e8bfa4-8086-4ef0-9e35-9e00b24be319
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 76d9a712a0acda223fc86b80be9c35c0ed9f3a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-powershell"></a>Приступая к работе по созданию балансировщика нагрузки (классический режим) для Интернета в PowerShell

> [!div class="op_single_selector"]
> * [классический портал Azure](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [Интерфейс командной строки Azure](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [облачных служб Azure](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> Перед началом работы с ресурсами Azure, он является важным toounderstand, что Azure в данный момент существуют две модели развертывания: диспетчера ресурсов Azure и классическом. Обязательно изучите [модели и инструменты развертывания](../azure-classic-rm.md) , прежде чем приступить к работе с какими бы то ни было ресурсами Azure. Для просмотра документации hello для различных средств, щелкнув вкладки hello hello верхней части этой статьи. В этой статье рассматриваются hello классической модели развертывания. Вы также можете [Узнайте, как с помощью диспетчера ресурсов Azure подсистемы балансировки нагрузки, toocreate из Интернета](load-balancer-get-started-internet-arm-ps.md).

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-load-balancer-using-powershell"></a>Настройка балансировки нагрузки с помощью PowerShell

tooset копирование подсистемы балансировки нагрузки с помощью powershell, следуйте инструкциям hello:

1. Если ранее не пользовались Azure PowerShell, см. раздел [как tooInstall и настройка Azure PowerShell](/powershell/azure/overview) и следуйте инструкциям hello все toohello hello способом завершения toosign в Azure и выберите свою подписку.
2. После создания виртуальной машины, можно использовать командлеты PowerShell tooadd виртуальной машины tooa подсистемы балансировки нагрузки в пределах hello же облачной службе.

В hello примере будут добавлены набор балансировки нагрузки вызывается toocloud «веб-ферма» «mytestcloud» (или myctestcloud.cloudapp.net), добавление toovirtual подсистемы балансировки нагрузки, hello конечных точек для hello машины службы с именем «web1» и «web2». Hello балансировки нагрузки получает сетевой трафик через порт 80 и равномерно распределяется между виртуальными машинами hello определяется hello локальную конечную точку (в этом вариантов порт 80) с использованием TCP.

### <a name="step-1"></a>Шаг 1

Создание конечной точки балансировки нагрузки для hello первой виртуальной Машины «web1»

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

### <a name="step-2"></a>Шаг 2

Создайте другой конечной точкой hello второй виртуальной Машины «web2» с помощью hello же нагрузки имя набора балансировки

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web2" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

## <a name="remove-a-virtual-machine-from-a-load-balancer"></a>Удаление виртуальной машины из балансировщика нагрузки

Можно использовать Remove-AzureEndpoint tooremove конечной точки виртуальной машины из балансировки нагрузки hello

```powershell
Get-azureVM -ServiceName mytestcloud  -Name web1 |Remove-AzureEndpoint -Name httpin | Update-AzureVM
```

## <a name="next-steps"></a>Дальнейшие действия

Вы также можете [приступить к созданию внутреннего балансировщика нагрузки](load-balancer-get-started-ilb-classic-ps.md) и настроить [режим распределения](load-balancer-distribution-mode.md) для определенного поведения балансировщика нагрузки.

Если приложению tookeep подключений проверки активности для серверов в подсистему балансировки нагрузки, можно понять больше о [простоя параметры времени ожидания TCP для подсистемы балансировки нагрузки](load-balancer-tcp-idle-timeout.md). Это поможет toolearn о поведении простоя подключения при использовании подсистемы балансировки нагрузки Azure.
