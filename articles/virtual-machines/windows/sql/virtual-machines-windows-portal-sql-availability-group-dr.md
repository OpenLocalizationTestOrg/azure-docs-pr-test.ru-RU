---
title: "Группы доступности сервера - виртуальных машинах Azure — аварийного восстановления aaaSQL | Документы Microsoft"
description: "В этой статье объясняется, как группировать tooconfigure доступности SQL Server на виртуальных машинах Azure с репликой в разных регионах."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 388c464e-a16e-4c9d-a0d5-bb7cf5974689
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/02/2017
ms.author: mikeray
ms.openlocfilehash: df6238dc61c5a56879c75c9bf7314c618f43c0ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-always-on-availability-group-on-azure-virtual-machines-in-different-regions"></a>Настройка группы доступности AlwaysOn на виртуальных машинах Azure в разных регионах

В этой статье объясняется, как tooconfigure доступности SQL Server Always On группы реплики на виртуальных машинах Azure в удаленном расположении Azure. Используйте этот конфигурации toosupport аварийного восстановления.

Эта статья относится tooAzure виртуальные машины в режим диспетчера ресурсов.

Hello иллюстрации показан общий развертывания группы доступности на виртуальных машинах Azure.

   ![Группа доступности](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic.png)

В таком развертывании все виртуальные машины находятся в одном регионе Azure. Hello реплики группы доступности могут иметь синхронной фиксации с автоматическим переходом на SQL-1 и SQL 2. toobuild этой архитектуре см [шаблон группы доступности или учебника](virtual-machines-windows-portal-sql-availability-group-overview.md).

Эта архитектура является уязвимым toodowntime Если hello регион Azure становится недоступной. tooovercome этой уязвимости, добавить реплику в другом регионе Azure. Hello следующей схеме показано как выглядит новая архитектура hello.

   ![Аварийное восстановление группы доступности](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic-dr.png)

Hello предыдущей схеме показаны новые виртуальная машина с именем SQL-3. SQL-3 находится в другом регионе Azure. SQL-3 добавляется toohello отказоустойчивого кластера Windows Server. На SQL-3 можно разместить реплику группы доступности. И, наконец Обратите внимание, что этой hello регион Azure для SQL-3 имеет новую подсистему балансировки нагрузки Azure.

>[!NOTE]
> Группы доступности Azure является обязательным, если Здравствуйте, более чем одна виртуальная машина находится в одном регионе. Если только одна виртуальная машина находится в регионе hello, группа доступности hello не является обязательным. Поместить виртуальную машину в группу доступности можно только во время создания виртуальной машины. Если hello виртуальная машина уже находится в наборе доступности, можно добавить виртуальную машину для более поздней версии дополнительную реплику.

В этой архитектуре реплики hello в удаленном регионе hello обычно настраивается с помощью режима доступности асинхронной фиксации и отработка отказа вручную.

Если реплики группы доступности находятся на виртуальных машинах Azure в разных регионах Azure, то для каждого региона требуется:

* шлюз виртуальной сети;
* подключение к шлюзу виртуальной сети.

Hello следующая диаграмма показывает взаимодействие hello сети между центрами обработки данных.

   ![Группа доступности](./media/virtual-machines-windows-portal-sql-availability-group-dr/01-vpngateway-example.png)

>[!IMPORTANT]
>Эта архитектура влечет за собой оплату исходящего трафика для данных, реплицируемых между регионами Azure. Ознакомьтесь с разделом [Сведения о стоимости пропускной способности](http://azure.microsoft.com/pricing/details/bandwidth/).  

## <a name="create-remote-replica"></a>Создание удаленной реплики

реплики в удаленном центре обработки данных, toocreate hello следующие действия:

1. [Создание виртуальной сети в новой области hello](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md).

1. [Настройка подключения виртуальной сети для виртуальной сети с помощью портала Azure hello](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).

   >[!NOTE]
   >В некоторых случаях возможно подключение к виртуальной сети для виртуальной сети hello toocreate toouse PowerShell. Например при использовании различных учетных записях Azure невозможно настроить соединение hello hello портала. В этом разделе, [VNet к VNet Настройка соединения с помощью портала Azure "hello"](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).

1. [Создание контроллера домена в новой области hello](../../../active-directory/active-directory-new-forest-virtual-machine.md).

   Этот контроллер домена обеспечивает проверку подлинности, если не доступен контроллер домена hello в первичном сайте hello.

1. [Создание виртуальной машины SQL Server в новой области hello](virtual-machines-windows-portal-sql-server-provision.md).

1. [Создайте балансировки нагрузки Azure в сети hello в новой области hello](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).

   Эта подсистема балансировки нагрузки должна:

   - В hello одной сети и подсети как hello новой виртуальной машины.
   - Иметь статический IP-адрес для прослушивателя группы доступности hello.
   - Включить пул серверной части, состоящий из только для виртуальных машин hello в hello же регионе, которые hello подсистемы балансировки нагрузки.
   - Используйте IP-адрес определенного toohello пробы TCP порт.
   - У определенного toohello правила SQL Server hello балансировки нагрузки одного региона.  

1. [Добавить toohello функции отказоустойчивой кластеризации SQL Server, новый](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).

1. [Присоединение hello новому домену toohello SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).

1. [Задать учетную запись домена hello новый SQL Server toouse учетной записи для службы](virtual-machines-windows-portal-sql-availability-group-prereq.md#setServiceAccount).

1. [Добавить новый toohello SQL Server hello отказоустойчивого кластера Windows Server](virtual-machines-windows-portal-sql-availability-group-tutorial.md#addNode).

1. Создайте ресурс IP-адреса в кластере hello.

   Можно создать ресурс IP-адреса hello в диспетчере отказоустойчивости кластеров. Щелкните правой кнопкой мыши роль группы доступности hello, щелкните **добавить ресурс**, **дополнительные ресурсы**и нажмите кнопку **IP-адрес**.

   ![Создание IP-адреса](./media/virtual-machines-windows-portal-sql-availability-group-dr/20-add-ip-resource.png)

   Настройте этот IP-адрес следующим образом.

   - Использование сети hello из hello удаленном центре обработки данных.
   - Назначьте hello IP-адрес из hello новую подсистему балансировки нагрузки Azure. 

1. Здравствуйте, новый SQL Server в диспетчере конфигурации SQL Server на [включить группы доступности AlwaysOn](http://msdn.microsoft.com/library/ff878259.aspx).

1. [Порты брандмауэра откройте hello нового SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).

   Hello номера портов, необходимо tooopen зависят от среды. Открытые порты для зеркального отображения конечной точки и Azure hello загрузить зонда работоспособности подсистемы балансировки.

1. [Добавить группу доступности toohello реплики на hello нового SQL Server](http://msdn.microsoft.com/library/hh213239.aspx).

   Для реплики в удаленном регионе Azure настройте асинхронную репликацию с ручной отработкой отказа.  

1. Добавьте hello ресурс IP-адреса в качестве зависимости для кластера (сетевое имя) точки доступа клиента прослушивателя hello.

   Hello следующем снимке экрана показан правильно настроенный ресурс IP-адреса кластера:

   ![Группа доступности](./media/virtual-machines-windows-portal-sql-availability-group-dr/50-configure-dependency-multiple-ip.png)

   >[!IMPORTANT]
   >Группа ресурсов кластера Hello включает оба IP-адреса. Оба IP-адреса являются зависимости для точки доступа клиента hello прослушивателя. Используйте hello **или** оператор в конфигурации зависимостей hello кластера.

1. [Задайте параметры кластера hello в PowerShell](virtual-machines-windows-portal-sql-availability-group-tutorial.md#setparam).

Запустите сценарий PowerShell hello с hello кластера сетевое имя, IP-адрес и порт пробы, настроенные в подсистеме балансировки нагрузки hello в новой области hello.

   ```PowerShell
   $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster name for hello network in hello new region (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name).
   $IPResourceName = "<IPResourceName>" # hello cluster name for hello new IP Address resource.
   $ILBIP = “<n.n.n.n>” # hello IP Address of hello Internal Load Balancer (ILB) in hello new region. This is hello static IP address for hello load balancer you configured in hello Azure portal.
   [int]$ProbePort = <nnnnn> # hello probe port you set on hello ILB.

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```

## <a name="set-connection-for-multiple-subnets"></a>Настройка подключения для нескольких подсетей

реплика Hello в hello удаленном центре обработки данных является частью группы доступности hello, но он находится в другой подсети. Если эта реплика становится первичной репликой hello, может произойти истечение времени ожидания соединения приложения. Такое поведение является hello такой же, как в развертывании с несколькими подсетями группы доступности в локальной среде. tooallow подключений из клиентских приложений, обновите hello клиентское подключение или настроить кэширование на ресурсу сетевого имени кластера hello разрешение имен.

Желательно, обновите tooset строки подключения клиента hello `MultiSubnetFailover=Yes`. Ознакомьтесь с разделом [Соединение с помощью MultiSubnetFailover](http://msdn.microsoft.com/library/gg471494#Anchor_0).

Если невозможно изменить строки подключения hello, можно настроить кэширование разрешения имен. Ознакомьтесь с разделом [Connection Timeouts in Multi-subnet Availability Group](http://blogs.msdn.microsoft.com/alwaysonpro/2014/06/03/connection-timeouts-in-multi-subnet-availability-group/) (Время ожидания подключения в группе доступности с несколькими подсетями).

## <a name="fail-over-tooremote-region"></a>При сбое tooremote области

tootest прослушивателя подключения toohello удаленной области, можно выполнить переход hello реплики toohello удаленной области. Хотя hello реплики является асинхронным, переход на другой ресурс происходит потеря данных toopotential уязвимым. toofail над без потери данных, изменить toosynchronous режим доступности hello и установить режим tooautomatic hello отработки отказа. Используйте следующие шаги hello.

1. В **обозревателя объектов**, подключитесь toohello экземпляр SQL Server, на котором размещена первичная реплика hello.
1. Выберите **Группы доступности AlwaysOn** > **Группы доступности**, щелкните правой кнопкой мыши группу доступности и выберите **Свойства**.
1. На hello **Общие** в разделе **реплик доступности**, набор hello вторичной реплики в hello DR сайт toouse **синхронная фиксация** режима доступности и **Автоматическое** режим отработки отказа.
1. Если вторичная реплика в одном узле первичную реплику для обеспечения высокой доступности, задайте эту реплику слишком**Asynchronous Commit** и **вручную**.
1. Нажмите кнопку ОК.
1. В **обозревателя объектов**, щелкните правой кнопкой мыши группу доступности hello и нажмите кнопку **Показать панель мониторинга**.
1. На панели мониторинга hello, убедитесь, что hello синхронизировать реплики на сайте hello аварийного восстановления.
1. В **обозревателя объектов**, щелкните правой кнопкой мыши группу доступности hello и нажмите кнопку **отработки отказа...** . Управление входящим SQL Server открывает toofail мастер с сервером SQL Server.  
1. Нажмите кнопку **Далее**и экземпляр SQL Server выберите hello в сайте hello аварийного восстановления. Нажмите **Далее** еще раз.
1. Подключите toohello экземпляр SQL Server на сайте hello аварийного восстановления и нажмите кнопку **Далее**.
1. На hello **Сводка** , проверьте параметры hello и нажмите кнопку **Готово**.

После тестирования подключения, переместите hello первичная реплика задней tooyour первичных данных по центру и изменять настройки tootheir назад режим доступности hello обычной работы. Hello следующей таблице показаны hello обычные параметры функционирования hello архитектуры, описанные в этом документе.

| Расположение | Экземпляр сервера | Роль | Режим доступности | Режим отработки отказа
| ----- | ----- | ----- | ----- | -----
| Основной центр обработки данных | SQL-1 | Первичная | Синхронный | Автоматический
| Основной центр обработки данных | SQL-2 | Вторичная | Синхронный | Автоматический
| Дополнительный или удаленный центр обработки данных | SQL-3 | Вторичная | Асинхронный | Руководство


### <a name="more-information-about-planned-and-forced-manual-failover"></a>Дополнительные сведения о плановой и принудительной отработке отказа вручную

Дополнительные сведения см. в разделе hello следующие вопросы:

- [Выполнение запланированного перехода на другой ресурс вручную для группы доступности (SQL Server)](http://msdn.microsoft.com/library/hh231018.aspx)
- [Выполнение принудительного перехода на другой ресурс вручную для группы доступности (SQL Server)](http://msdn.microsoft.com/library/ff877957.aspx)

## <a name="additional-links"></a>Ссылки на дополнительные материалы

* [Группы доступности Always On](http://msdn.microsoft.com/library/hh510230.aspx)
* [Виртуальные машины Azure](http://docs.microsoft.com/azure/virtual-machines/windows/)
* [Подсистемы Azure Load Balancer](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer)
* [Группы доступности Azure](../manage-availability.md)
