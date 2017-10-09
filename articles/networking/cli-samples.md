---
title: "Образцы CLI aaaAzure | Документы Microsoft"
description: "Примеры Azure CLI"
services: virtual-network
documentationcenter: virtual-network
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 04/25/2017
ms.author: kumud
ms.openlocfilehash: 8001b7e72480cfd0122325f7fb81c32aaad072d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-networking"></a>Примеры Azure CLI для работы с сетью

Hello следующей таблице представлены ссылки toobash сценариев, созданных с использованием hello Azure CLI.

| | |
|-|-|
|**Подключение между ресурсами Azure**||
| [Создание виртуальной сети для многоуровневых приложений](./scripts/virtual-network-cli-sample-multi-tier-application.md?toc=%2fazure%2fnetworking%2ftoc.json) | Создание виртуальной сети с интерфейсной и внутренней подсетями. Подсети интерфейса toohello трафика является ограниченной tooHTTP и SSH, при toohello трафика конечной подсети ограниченный tooMySQL, порт 3306. |
| [Пиринг между двумя виртуальными сетями](./scripts/virtual-network-cli-sample-peer-two-virtual-networks.md?toc=%2fazure%2fnetworking%2ftoc.json) | Создается и выполняется подключение двух виртуальных сетей в hello одного региона. |
| [Маршрутизация трафика через виртуальный сетевой модуль](./scripts/virtual-network-cli-sample-route-traffic-through-nva.md?toc=%2fazure%2fnetworking%2ftoc.json) | Создает виртуальную сеть с внешнего и внутреннего интерфейса подсети и виртуальной Машины, которое может tooroute трафика между подсетями hello двух. |
| [Фильтрация входящего и исходящего сетевого трафика виртуальной машины](./scripts/virtual-network-filter-network-traffic.md?toc=%2fazure%2fnetworking%2ftoc.json) | Создание виртуальной сети с интерфейсной и внутренней подсетями. Входящий сетевой трафик интерфейса подсеть toohello является ограниченной tooHTTP, HTTPS и SSH. Исходящий трафик toohello Интернет из внутренней подсети hello не допускается. |
|**Направление трафика и балансировка нагрузки**||
| [Загрузить tooVMs Балансировка трафика для обеспечения высокой доступности](./scripts/load-balancer-linux-cli-sample-nlb.md?toc=%2fazure%2fnetworking%2ftoc.json) | Создает несколько виртуальных машин с высокодоступной конфигурацией с балансировкой нагрузки. |
| [Балансировка нагрузки нескольких веб-сайтов на виртуальных машинах](./scripts/load-balancer-linux-cli-load-balance-multiple-websites-vm.md?toc=%2fazure%2fnetworking%2ftoc.json) | Создает две виртуальные машины с несколькими IP-конфигурации, соединенных tooan группе доступности Azure, доступные через подсистемы балансировки нагрузки Azure. |
| [Направление трафика через несколько регионов для обеспечения высокого уровня доступности приложений](./scripts/traffic-manager-cli-websites-high-availability.md?toc=%2fazure%2fnetworking%2ftoc.json) |  Создание двух планов службы приложений, двух веб-приложений, а также профиля и двух конечных точек диспетчера трафика. |
| | |
