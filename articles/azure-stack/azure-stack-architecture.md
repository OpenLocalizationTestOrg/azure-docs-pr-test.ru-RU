---
title: "aaaMicrosoft архитектура пакета средств разработки стек Azure | Документы Microsoft"
description: "Здравствуйте, представление архитектуры пакета средств разработки Microsoft Azure стека."
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: a7e61ea4-be2f-4e55-9beb-7a079f348e05
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: helaw
ms.openlocfilehash: 32a19ced7ddd57b97ba796679c116132090402e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-stack-development-kit-architecture"></a>Архитектура пакета средств разработки Microsoft Azure стека
Hello пакет средств разработки стек Azure — это развертывание одного узла Azure стека. Все компоненты hello устанавливаются в виртуальных машин, работающих на одном хост-компьютере. 

## <a name="logical-architecture-diagram"></a>Диаграмма логической архитектуры
Hello следующей схеме показана логическая архитектура hello пакет средств разработки Azure стека hello и его компонентов.

![](media/azure-stack-architecture/image1.png)

## <a name="virtual-machine-roles"></a>Роли виртуальной машины
Hello пакет средств разработки стек Azure предлагает службы, с помощью следующих виртуальных машин на узле hello hello:

| Имя | Описание |
| ----- | ----- |
| **AzS ACS01** | Службы хранилища Azure стека.|
| **AzS ADFS01** | Службы федерации Active Directory (ADFS).  |
| **AzS BGPNAT01** | Пограничный маршрутизатор и предоставляет возможности NAT и VPN Azure стека. |
| **AzS CA01** | Службы сертификатов центр служб ролей Azure стека.|
| **AzS DC01** | Active Directory, DNS и DHCP-службы для стека Microsoft Azure.|
| **AzS ERCS01** | Консоль аварийного восстановления виртуальной Машины. |
| **AzS GWY01** | Шлюз служб как VPN-подключения сеть сеть для сетей клиентов.|
| **AzS NC01** | Сетевой контроллер управляет службами сетевой стек Azure.  |
| **AzS SLB01** | Балансировка нагрузки мультиплексор служб Azure стека для клиентов и служб инфраструктуры Azure стека.  |
| **AzS SQL01** | Для ролей инфраструктуры Azure стека хранения внутренних данных.  |
| **AzS WAS01** | Службы диспетчера ресурсов Azure и портала администрирования Azure стека.|
| **AzS WASP01**| Стек пользователя (клиент) Azure и службы диспетчера ресурсов Azure.|
| **AzS XRP01** | Контроллер управления инфраструктуры для стека Microsoft Azure, включая hello поставщики ресурсов вычисления, сети и хранилища.|


## <a name="next-steps"></a>Дальнейшие действия
[Развертывание стек Azure](azure-stack-deploy.md)

[Первый tootry сценариев](azure-stack-first-scenarios.md)

