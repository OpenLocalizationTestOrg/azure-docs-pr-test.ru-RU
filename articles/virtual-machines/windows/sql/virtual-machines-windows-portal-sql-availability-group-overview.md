---
title: "Общие сведения о группах доступности сервера - виртуальных машинах Azure - aaaSQL | Документы Microsoft"
description: "В этой статье рассматриваются группы доступности SQL Server на виртуальных машинах Azure."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 601eebb1-fc2c-4f5b-9c05-0e6ffd0e5334
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/13/2017
ms.author: mikeray
ms.openlocfilehash: ecac8b8c5073021af2aa22a05490bb8c4c20ed17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-sql-server-always-on-availability-groups-on-azure-virtual-machines"></a>Введение в группы доступности AlwaysOn SQL Server на виртуальных машинах Azure #

В этой статье рассматриваются группы доступности SQL Server на виртуальных машинах Azure. 

Группы доступности AlwaysOn на виртуальных машинах Azure, аналогичные tooAlways групп доступности на локальном компьютере. Дополнительные сведения см. в разделе [Группы доступности AlwaysOn (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx). 

Hello диаграмме показаны компоненты hello завершения доступности группы серверов SQL Server в виртуальных машинах Azure.

![Группа доступности](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

Hello ключевое различие для группы доступности на виртуальных машинах Azure, hello виртуальных машинах Azure, требуют [подсистемы балансировки нагрузки](../../../load-balancer/load-balancer-overview.md). Подсистема балансировки нагрузки Hello содержит hello IP-адресов для прослушивателя группы доступности hello. Если используется несколько групп доступности, то каждой из них требуется прослушиватель. Одна подсистема балансировки нагрузки может обслуживать несколько прослушивателей.

Когда вы будете готовы toobuild aroup доступности SQL Server на виртуальных машинах Azure, см. в toothese учебники.

## <a name="automatically-create-an-availability-group-from-a-template"></a>Автоматическое создание группы доступности из шаблона

[Автоматическая настройка группы доступности AlwaysOn на виртуальной машине Azure в модели Resource Manager](virtual-machines-windows-portal-sql-alwayson-availability-groups.md)

## <a name="manually-create-an-availability-group-in-azure-portal"></a>Создание группы доступности на портале Azure вручную

Можно также создать виртуальные машины hello самостоятельно без шаблона hello. Во-первых выполните hello предварительные требования, а затем создайте группу доступности hello. В разделе hello следующие вопросы: 

- [Настройка необходимых компонентов для создания групп доступности AlwaysOn в виртуальных машинах Azure](virtual-machines-windows-portal-sql-availability-group-prereq.md)

- [Создание группы доступности AlwaysOn tooimprove доступности и аварийного восстановления](virtual-machines-windows-portal-sql-availability-group-tutorial.md)

## <a name="next-steps"></a>Дальнейшие действия

[Настройка группы доступности AlwaysOn на виртуальных машинах Azure в разных регионах](virtual-machines-windows-portal-sql-availability-group-dr.md).
