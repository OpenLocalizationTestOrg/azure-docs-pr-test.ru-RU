---
title: "Примеры PowerShell aaaAzure | Документы Microsoft"
description: "Примеры сценариев Azure PowerShell."
services: virtual-network
documentationcenter: virtual-network
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/24/2017
ms.author: georgewallace
ms.openlocfilehash: 130a6e755691b46a9549cad5acaa5bde4fe38e95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-powershell-samples-for-networking"></a>Примеры Azure PowerShell для работы с сетями

Hello приведенной ниже таблице указаны ссылки tooscripts, созданного с помощью Azure PowerShell.

| | |
|-|-|
|**Подключение между ресурсами Azure**||
| [Создание виртуальной сети для многоуровневых приложений](./scripts/virtual-network-powershell-sample-multi-tier-application.md?toc=%2fazure%2fnetworking%2ftoc.json) | Создание виртуальной сети с интерфейсной и внутренней подсетями. Подсети интерфейса toohello трафика ограниченный tooHTTP, при toohello трафика конечной подсети ограниченный tooSQL, порт 1433. |
| [Пиринг между двумя виртуальными сетями](./scripts/virtual-network-powershell-sample-peer-two-virtual-networks.md?toc=%2fazure%2fnetworking%2ftoc.json) | Создается и выполняется подключение двух виртуальных сетей в hello одного региона. |
| [Маршрутизация трафика через виртуальный сетевой модуль](./scripts/virtual-network-powershell-sample-route-traffic-through-nva.md?toc=%2fazure%2fnetworking%2ftoc.json) | Создает виртуальную сеть с внешнего и внутреннего интерфейса подсети и виртуальной Машины, которое может tooroute трафика между подсетями hello двух. |
| [Фильтрация входящего и исходящего сетевого трафика виртуальной машины](./scripts/virtual-network-powershell-filter-network-traffic.md?toc=%2fazure%2fnetworking%2ftoc.json) | Создание виртуальной сети с интерфейсной и внутренней подсетями. Входящий сетевой трафик интерфейса подсеть toohello является ограниченной tooHTTP и HTTPS... Исходящий трафик toohello Интернет из внутренней подсети hello не допускается. |
|**Направление трафика и балансировка нагрузки**||
| [Загрузить tooVMs Балансировка трафика для обеспечения высокой доступности](./scripts/load-balancer-windows-powershell-sample-nlb.md?toc=%2fazure%2fnetworking%2ftoc.json) | Создает несколько виртуальных машин с высокодоступной конфигурацией с балансировкой нагрузки. |
| [Балансировка нагрузки нескольких веб-сайтов на виртуальных машинах](./scripts/load-balancer-windows-powershell-load-balance-multiple-websites-vm.md?toc=%2fazure%2fnetworking%2ftoc.json) | Создает две виртуальные машины с несколькими IP-конфигурации, соединенных tooan группе доступности Azure, доступные через подсистемы балансировки нагрузки Azure. |
| [Направление трафика через несколько регионов для обеспечения высокого уровня доступности приложений](./scripts/traffic-manager-powershell-websites-high-availability.md?toc=%2fazure%2fnetworking%2ftoc.json) |  Создание двух планов службы приложений, двух веб-приложений, а также профиля и двух конечных точек диспетчера трафика. |
| | |
