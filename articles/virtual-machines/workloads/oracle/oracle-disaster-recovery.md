---
title: "aaaOverview сценария Oracle аварийного восстановления в среде Azure | Документы Microsoft"
description: "Сценарий аварийного восстановления базы данных Oracle Database 12c в среде Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 6/2/2017
ms.author: rclaus
ms.openlocfilehash: 1fa69e1ba044b46b27695fec92fd9ca82df796f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-for-an-oracle-database-12c-database-in-an-azure-environment"></a>Аварийное восстановление базы данных Oracle Database 12c в среде Azure.

## <a name="assumptions"></a>Предположения

- У вас есть представление о структуре Oracle Data Guard и средах Azure.


## <a name="goals"></a>Цели
- Проектирование топологии hello и конфигурации, соответствующие требованиям аварийного восстановления (DR).

## <a name="scenario-1-primary-and-dr-sites-on-azure"></a>Сценарий 1. Основные сайты и сайты аварийного восстановления в Azure

У клиента есть Oracle базы данных set на первичном сайте hello. Сайт аварийного восстановления находится в другом регионе. Hello клиент использует Oracle Data Guard для быстрого восстановления между этими сайтами. Первичный сайт Hello оказывает баз данных-получателей для отчетности и других целей. 

### <a name="topology"></a>Топология

Ниже приведена сводка hello Настройка Azure:

- два сайта (первичный сайт и сайт для аварийного восстановления);
- две виртуальные сети;
- две базы данных Oracle с Data Guard (основная и резервная);
- две базы данных Oracle с Golden Gate или Data Guard (только основной сайт);
- Две службы приложения, основной и один на сайте hello аварийного восстановления
- *Наборе доступности* которого используется для базы данных и приложения службы на первичном сайте hello
- Один jumpbox на каждом сайте, который ограничивает доступ toohello частной сети и разрешает только вход администратора
- среда Jumpbox, служба приложения, база данных и VPN-шлюз в отдельных подсетях;
- группа безопасности сети, применяющаяся в подсетях приложения и базы данных;

![Снимок экрана со страницей топологии hello аварийного восстановления](./media/oracle-disaster-recovery/oracle_topology_01.png)

## <a name="scenario-2-primary-site-on-premises-and-dr-site-on-azure"></a>Сценарий 2. Основной локальный сайт и сайт аварийного восстановления в Azure

Клиент имеет локальную базу данных Oracle (основной сайт). Сайт аварийного восстановления — в Azure. Oracle Data Guard используется для быстрого восстановления между этими сайтами. Первичный сайт Hello оказывает баз данных-получателей для отчетности и других целей. 

Существует два подхода для такой конфигурации.

### <a name="approach-1-direct-connections-between-on-premises-and-azure-requiring-open-tcp-ports-on-hello-firewall"></a>Способ 1: Прямые соединения между локальной и Azure, требуется открыть TCP-порты в брандмауэре hello 

Мы не рекомендуем прямые подключения, так как они определяют toohello порты TCP hello за пределами world.

#### <a name="topology"></a>Топология

Ниже приводится сводка hello Настройка Azure:

- один сайт для аварийного восстановления; 
- Одна виртуальную сеть
- одна база данных Oracle с Data Guard (активная);
- Одно приложение службы на сайте hello аварийного восстановления
- Один jumpbox, ограничивает доступ toohello частной сети, а только вход администратором
- среда Jumpbox, служба приложения, база данных и VPN-шлюз в отдельных подсетях;
- группа безопасности сети, применяющаяся в подсетях приложения и базы данных;
- Политика и правила NSG tooallow входящего трафика TCP-порт 1521 (или порта, определяемые пользователем)
- NSG правила и политики toorestrict только hello IP-адрес или адреса локальной (базы данных или приложения) tooaccess hello виртуальной сети

![Снимок экрана со страницей топологии hello аварийного восстановления](./media/oracle-disaster-recovery/oracle_topology_02.png)

### <a name="approach-2-site-to-site-vpn"></a>Способ 2. VPN-подключение типа "сеть — сеть"
Оптимальным способом является использование VPN-подключения типа "сеть — сеть". Дополнительные сведения о настройке VPN см. в статье [Создание виртуальной сети с VPN типа "сеть — сеть" с помощью интерфейса командной строки](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).

#### <a name="topology"></a>Топология

Ниже приводится сводка hello Настройка Azure:

- один сайт для аварийного восстановления; 
- Одна виртуальную сеть 
- одна база данных Oracle с Data Guard (активная);
- Одно приложение службы на сайте hello аварийного восстановления
- Один jumpbox, ограничивает доступ toohello частной сети, а только вход администратором
- среда Jumpbox, служба приложения, база данных и VPN-шлюз находятся в отдельных подсетях;
- группа безопасности сети, применяющаяся в подсетях приложения и базы данных;
- VPN-подключение типа "сеть — сеть" между локальной средой и Azure.

![Снимок экрана со страницей топологии hello аварийного восстановления](./media/oracle-disaster-recovery/oracle_topology_03.png)

## <a name="additional-reading"></a>Дополнительные материалы

- [Design and implement an Oracle database in Azure](oracle-design.md) (Разработка базы данных Oracle и ее реализация в Azure)
- [Реализация Oracle Data Guard на виртуальной машине Azure под управлением Linux](configure-oracle-dataguard.md)
- [Реализация Oracle Golden Gate на виртуальной машине Azure под управлением Linux](configure-oracle-golden-gate.md)
- [Создание резервных копий и восстановление базы данных Oracle Database 12c на виртуальной машине Linux в Azure](oracle-backup-recovery.md)


## <a name="next-steps"></a>Дальнейшие действия

- Изучите [руководство по созданию высокодоступных виртуальных машин](../../linux/create-cli-complete.md).
- [Изучите примеры развертывания виртуальных машин с помощью интерфейса командной строки](../../linux/cli-samples.md).
