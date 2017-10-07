---
title: "aaaReplicate приложений с помощью SQL Server и Azure Site Recovery | Документы Microsoft"
description: "В этой статье описывается как tooreplicate SQL Server с помощью Azure Site Recovery для возможности аварийного SQL Server."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: pratshar
ms.openlocfilehash: 99755f2cd2f7e924071f1e230ac4a0bda88f0a39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="protect-sql-server-using-sql-server-disaster-recovery-and-azure-site-recovery"></a>Защита SQL Server с помощью аварийного восстановления SQL Server и Azure Site Recovery

В этой статье описывается, как hello tooprotect SQL Server серверной части, состоящий из SQL Server непрерывности и аварийного восстановления (BCDR) технологии, приложения и [Azure Site Recovery](site-recovery-overview.md).

Прежде чем начать, убедитесь, что вы ознакомлены с возможностями аварийного восстановления SQL Server, включая отказоустойчивую кластеризацию, группы доступности AlwaysOn, зеркальное отображение базы данных и доставку журналов.


## <a name="sql-server-deployments"></a>Развертывания SQL Server

Многих рабочих нагрузок использовать SQL Server в качестве основы, и их можно интегрировать с приложениями SharePoint, и SAP, служб данных tooimplement.  Вы можете развернуть SQL Server несколькими способами:

* **Изолированный сервер SQL Server**. SQL Server и все базы данных размещаются на одном компьютере (физическом или виртуальном). Если сервер виртуальный, то для обеспечения локальной высокой доступности используется кластеризация размещения. Высокая доступность на уровне гостя не обеспечивается.
* **Экземпляры отказоустойчивых кластеров SQL Server (Always On FCI).** В этом случае два или несколько узлов экземпляров SQL Server с общими дисками настраиваются в отказоустойчивом кластере Windows. Если узел не работает, hello кластера может переключить SQL Server tooanother экземпляра. Эта настройка является типовыми tooimplement высокий уровень доступности на первичном сайте. Это развертывание не защищает от сбоя или простоя в слое hello общего хранилища. Общий диск может быть реализован с использованием интерфейса iSCSI, Fiber Channel или общих VHDX-файлов.
* **Группы доступности SQL AlwaysOn.** В этом случае два или несколько узлов настраиваются в кластере без общих ресурсов, в котором базы данных SQL Server настроены в группе доступности с синхронной репликацией и автоматической отработкой отказа.

 В этой статье использует следующие технологии собственного SQL аварийного восстановления для восстановления баз данных tooa удаленный сайт hello:

* SQL группы доступности AlwaysOn, tooprovide для аварийного восстановления для SQL Server 2012 или 2014 выпуски Enterprise.
* Зеркальное отображение базы данных SQL в режиме высокого уровня безопасности для SQL Server Standard (любой версии) или SQL Server 2008 R2.

## <a name="site-recovery-support"></a>Поддержка Site Recovery

### <a name="supported-scenarios"></a>Поддерживаемые сценарии использования.
Site Recovery можно защитить SQL Server, как описано в таблице hello.

**Сценарий** | **tooa вторичного сайта** | **tooAzure**
--- | --- | ---
**Hyper-V** | Да | Да
**VMware** | Да | Да
**Физический сервер** | Да | Да

### <a name="supported-sql-server-versions"></a>Поддерживаемые версии SQL Server
Эти версии SQL Server поддерживаются для сценариев hello поддерживается:

* SQL Server 2016 Enterprise и Standard;
* SQL Server 2014 Enterprise и Standard;
* SQL Server 2012 Enterprise и Standard;
* SQL Server 2008 R2 Enterprise и Standard.

### <a name="supported-sql-server-integration"></a>Поддерживаемая интеграция SQL Server

Site Recovery можно интегрировать с собственного SQL Server BCDR технологии, приведены в таблице hello, tooprovide решение аварийного восстановления.

**Компонент** | **Дополнительные сведения** | **SQL Server** |
--- | --- | ---
**Группы доступности AlwaysOn** | Несколько отдельных экземпляров SQL Server, каждый из которых запущен в отказоустойчивом кластере с несколькими узлами.<br/><br/>Базы данных можно объединить в группы отработки отказа, которые затем можно скопировать (зеркальное отображение) на экземпляры SQL Server, благодаря чему исключается необходимость в общем хранилище.<br/><br/>Обеспечивает аварийное восстановление между основным сайтом и одним или несколькими дополнительными сайтами. Два узла можно настроить в кластере без общих ресурсов, в котором базы данных SQL Server настроены в группе доступности с синхронной репликацией и автоматической отработкой отказа. | SQL Server Enterprise 2014 и 2012
**Отказоустойчивая кластеризация (AlwaysOn FCI)** | SQL Server применяет отказоустойчивую кластеризацию Windows для обеспечения высокого уровня доступности локальных рабочих нагрузок SQL Server.<br/><br/>Узлы, на которых выполняются экземпляры SQL Server с общими дисками, настроены в отказоустойчивом кластере. Если экземпляр не работает при сбое toodifferent один кластер hello.<br/><br/>Hello кластера не защищает от сбоев или простоев в общем хранилище. Hello общего диска можно реализовать с помощью iSCSI, fiber channel, или в общих vhdx-файлы. | Выпуски SQL Server Enterprise<br/><br/>SQL Server Standard edition (только для ограниченного tootwo узлов)
**Зеркальное отображение базы данных (в режиме высокого уровня безопасности)** | Обеспечивает защиту одной базы данных tooa одной дополнительной копии. Доступно как в режиме репликации с высоким уровнем безопасности (синхронный режим), так и в режиме репликации с высоким уровнем производительности (асинхронный режим). Не требует наличия отказоустойчивого кластера. | SQL Server 2008 R2<br/><br/>Все выпуски SQL Server Enterprise
**Автономный SQL Server** | Hello SQL Server и базы данных размещаются на одном сервере (физических или виртуальных). Кластеризацию узлов используется для обеспечения высокой доступности, если виртуальный сервер hello. Без высокой доступности гостевого уровня. | Выпуск Enterprise или Standard

## <a name="deployment-recommendations"></a>Рекомендации по развертыванию

В таблице перечислены рекомендации относительно интеграции технологий SQL Server BCDR в Site Recovery.

| **Версия** | **Выпуск** | **Развертывание** | **Tooon локально в локальной среде** | **TooAzure в локальной среде** |
| --- | --- | --- | --- | --- |
| SQL Server 2014 или 2012 |Enterprise |Экземпляр отказоустойчивого кластера |Группы доступности AlwaysOn |Группы доступности AlwaysOn |
|| Enterprise |Группы доступности AlwaysOn для обеспечения высокой доступности |Группы доступности AlwaysOn |Группы доступности AlwaysOn | |
|| Standard |Экземпляр отказоустойчивого кластера (FCI) |Репликация Site Recovery с локальным зеркалом |Репликация Site Recovery с локальным зеркалом | |
|| Enterprise или Standard |Автономный |Репликация Site Recovery |Репликация Site Recovery | |
| SQL Server 2008 R2 или 2008 |Enterprise или Standard |Экземпляр отказоустойчивого кластера (FCI) |Репликация Site Recovery с локальным зеркалом |Репликация Site Recovery с локальным зеркалом |
|| Enterprise или Standard |Автономный |Репликация Site Recovery |Репликация Site Recovery | |
| SQL Server (любая версия) |Enterprise или Standard |Экземпляр отказоустойчивого кластера — приложение DTC |Репликация Site Recovery |Не поддерживается |

## <a name="deployment-prerequisites"></a>Предварительные условия для развертывания

* Локальное развертывание SQL Server с поддерживаемой версией SQL Server. Обычно также требуется служба Active Directory для SQL Server.
* требования к Hello для hello требуется toodeploy сценария. Дополнительные сведения о требованиях к поддержки для [tooAzure репликации](site-recovery-support-matrix-to-azure.md) и [локальной](site-recovery-support-matrix.md), и [необходимые условия для развертывания](site-recovery-prereq.md).
* tooset настройки восстановления в Azure, выполнения hello [Оценка готовности виртуальной машины Azure](http://www.microsoft.com/download/details.aspx?id=40898) средства на виртуальных машинах SQL Server, toomake убедиться, что они совместимы с Azure и Site Recovery.

## <a name="set-up-active-directory"></a>настроить Active Directory;

Настройка Active Directory в hello восстановления вторичного сайта, для SQL Server toorun должным образом.

* **Малого предприятия**— с небольшим числом приложений и один контроллер домена для hello на локальном сайте, если требуется toofail hello всего узла, рекомендуется использовать контроллер домена hello tooreplicate репликации Site Recovery дополнительный ЦОД toohello или tooAzure.
* **Средний toolarge enterprise**— Если у вас есть большое количество приложений в лесу Active Directory, и требуется toofail по приложения или рабочей нагрузки, рекомендуется настроить дополнительный контроллер домена в дополнительном ЦОД hello, или в Azure. При использовании Always On доступности группы toorecover tooa удаленного сайта, мы рекомендуем настроить другой дополнительного контроллера домена на вторичном сайте hello, или в Azure, toouse для экземпляра SQL Server восстановлена hello.

инструкции Hello в данной статье предположить, что контроллер домена доступен в дополнительное расположение hello. [Узнайте больше](site-recovery-active-directory.md) о защите Active Directory с помощью Site Recovery.


## <a name="integrate-with-sql-server-always-on-for-replication-tooazure"></a>Интеграция с SQL Server Always On для tooAzure репликации

Вот что нужно toodo:

1. Импортировать скрипты в учетную запись службы автоматизации Azure. Это поле содержит скрипты hello toofailover группы доступности SQL в [виртуальная машина диспетчера ресурсов](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/asr-automation-recovery/scripts/ASR-SQL-FailoverAG.ps1) и [классической виртуальной машины](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/asr-automation-recovery/scripts/ASR-SQL-FailoverAGClassic.ps1).

    [![Развертывание tooAzure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)


1. Добавьте ASR SQL-FailoverAG как действие перед первой группы hello hello плана восстановления.

1. Следуйте инструкциям hello, доступных в toocreate hello скрипта с именем hello переменной tooprovide автоматизации групп доступности hello.

### <a name="steps-toodo-a-test-failover"></a>Toodo шаги теста отработки отказа

В SQL AlwaysOn нет встроенной поддержки тестовой отработки отказа. Поэтому рекомендуется hello следующее:

1. Настройка [резервного копирования Azure](../backup/backup-azure-vms.md) на виртуальной машине hello, на котором размещена реплика группы доступности hello в Azure.

1. Перед тем как запускать тестовую отработку отказа плана восстановления hello, восстановиться hello резервную копию, созданную в предыдущем шаге hello hello виртуальной машины.

    ![Восстановление из службы архивации Azure ](./media/site-recovery-sql/restore-from-backup.png)

1. [Принудительный кворум](https://docs.microsoft.com/sql/sql-server/failover-clusters/windows/force-a-wsfc-cluster-to-start-without-a-quorum#PowerShellProcedure) hello виртуальной машине восстановления из резервной копии.

1. Обновление IP-адреса IP tooan hello прослушивателя в hello тестовой отработки отказа сети.

    ![Обновление IP-адреса прослушивателя](./media/site-recovery-sql/update-listener-ip.png)

1. Подключите прослушиватель.

    ![Подключение прослушивателя](./media/site-recovery-sql/bring-listener-online.png)

1. Создание подсистемы балансировки нагрузки, с одного IP-адресом, созданных под интерфейсных IP пула соответствующего tooeach прослушивателя группы доступности и с виртуальной машины SQL hello, добавленные в hello внутренний пул.

     ![Создание балансировщика нагрузки — внешний пул IP-адресов ](./media/site-recovery-sql/create-load-balancer1.png)

    ![Создание балансировщика нагрузки — серверный пул IP-адресов ](./media/site-recovery-sql/create-load-balancer2.png)

1. Выполните тестовую отработку отказа плана восстановления hello.

### <a name="steps-toodo-a-failover"></a>Toodo действия отработки отказа

После добавления скрипта hello в плане восстановления hello и проверенные hello плана восстановления, выполнив тестовую отработку отказа, можно выполнить отработку отказа плана восстановления hello.


## <a name="integrate-with-sql-server-always-on-for-replication-tooa-secondary-on-premises-site"></a>Интегрировать с SQL Server Always On для репликации tooa дополнительного локального сайта

Если группы доступности hello SQL Server использует для высокого уровня доступности (или экземпляра отказоустойчивого Кластера), рекомендуется использовать группы доступности на сайте восстановления hello также. Обратите внимание, что это применяется tooapps, которые не используют распределенные транзакции.

1. [Настройте базы данных](https://msdn.microsoft.com/library/hh213078.aspx) для их добавления в группы доступности.
1. Создание виртуальной сети на вторичном сайте hello.
1. Настройте сеть сеть VPN-подключение между виртуальной сети hello и hello первичного сайта.
1. Создание виртуальной машины на сайте восстановления hello и установить SQL Server на него.
1. Расширить hello существующих Always On toohello группы доступности новой виртуальной Машины SQL Server. Настройте этот экземпляр SQL Server в качестве копии асинхронной реплики.
1. Создание прослушивателя группы доступности или обновление hello существующий прослушиватель tooinclude hello асинхронная реплика виртуальной машины.
1. Убедитесь, что фермы приложения hello настроена с помощью прослушивателя hello. Если она настроена с помощью имени сервера базы данных hello обновить прослушиватель toouse hello, вам требуется tooreconfigure его после отработки отказа hello.

Для приложений, использующих распределенные транзакции, мы рекомендуем развернуть Site Recovery с помощью [репликации VMware или физического сервера типа "сеть — сеть"](site-recovery-vmware-to-vmware.md).

### <a name="recovery-plan-considerations"></a>Рекомендации по плану восстановления
1. Добавьте этот образец скрипта toohello библиотеки VMM, на hello первичных и вторичных сайтах.

        Param(
        [string]$SQLAvailabilityGroupPath
        )
        import-module sqlps
        Switch-SqlAvailabilityGroup -Path $SQLAvailabilityGroupPath -AllowDataLoss -force

1. При создании плана восстановления для приложения hello, добавьте pre действие tooGroup 1 сценариев шаг, вызывающий toofail сценария hello через группы доступности.

## <a name="protect-a-standalone-sql-server"></a>Защита автономного сервера SQL Server

В этом сценарии рекомендуется использовать компьютере с SQL Server Site Recovery репликации tooprotect hello. Hello точные действия будут зависеть от является ли виртуальная машина или физический сервер SQL Server и требуется tooreplicate tooAzure или дополнительного локального сайта. Дополнительные сведения см. в статье [Что такое Site Recovery?](site-recovery-overview.md)

## <a name="protect-a-sql-server-cluster-standard-editionwindows-server-2008-r2"></a>Защита кластера SQL Server (версия Standard для Windows Server 2008 R2)

Кластер под управлением SQL Server Standard edition или SQL Server 2008 R2 мы рекомендуем использовать tooprotect Site Recovery репликации SQL Server.

### <a name="on-premises-tooon-premises"></a>Локальный tooon в локальной среде

* Если приложение hello работает с распределенными транзакциями рекомендуется развертывании [Site Recovery с репликацией SAN](site-recovery-vmm-san.md) в среде Hyper-V или [tooVMware сервер VMware или физическими](site-recovery-vmware-to-vmware.md) для среды VMware.
* Для приложений без использования DTC используйте hello выше подход toorecover hello кластера как автономный сервер за счет использования локального высокого уровня безопасности зеркальной базы данных.

### <a name="on-premises-tooazure"></a>TooAzure в локальной среде

Site Recovery не предоставляет виртуальной машине Поддержка кластеров при репликации tooAzure. SQL Server также не предоставляет экономичное решение для аварийного восстановления для выпуска Standard. В этом случае рекомендуется защитить hello в локальной среде SQL Server кластера tooa изолированный экземпляр SQL Server и восстановить ее в Azure.

1. Настройка дополнительных изолированный экземпляр SQL Server на локальном сайте hello.
1. Настройка tooserve экземпляр hello зеркалом hello баз данных, вы хотите tooprotect. Настройте зеркальное отображение в режиме высокого уровня безопасности.
1. Настройка для восстановления сайта на сайте локальной hello, ([Hyper-V](site-recovery-hyper-v-site-to-azure.md) или [виртуальные машины VMware или физическими серверами)](site-recovery-vmware-to-azure-classic.md).
1. Используйте Site Recovery репликации tooreplicate hello новый SQL Server экземпляр tooAzure. Поскольку зеркальное отображение высокий уровень безопасности, синхронизируются с hello первичного кластера, но будет реплицированных tooAzure, с помощью репликации Site Recovery.


![Стандартный кластер](./media/site-recovery-sql/standalone-cluster-local.png)

### <a name="failback-considerations"></a>Рекомендации относительно восстановления размещения

Для кластеров SQL Server Standard восстановление после незапланированной отработки отказа требуется SQL server резервного копирования и восстановления из hello зеркальный экземпляр toohello исходного кластера, с reestablishment hello зеркального отображения.

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения об архитектуре Site Recovery см. [здесь](site-recovery-components.md).
