---
title: "Архитектура hello aaaReview для Hyper-V репликации tooa вторичного сайта с помощью Azure Site Recovery | Документы Microsoft"
description: "Также приводятся сведения об архитектуре hello по репликации локальных виртуальных машин Hyper-V tooa вторичного System Center VMM сайта с помощью Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 07099161-4cc7-4f32-8eb9-2a71bbf0750b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 0de4b4e8601116c73e6fd710597ce4e561884368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-hyper-v-replication-tooa-secondary-site"></a>Шаг 1: Проверка hello архитектуры для Hyper-V репликации tooa вторичного сайта

В этой статье описывается hello компонентов и процессов, задействованных при репликации локальных виртуальных машин Hyper-V (ВМ) в облаках диспетчера виртуальных машин System Center (VMM), tooa с помощью hello вторичный сайт VMM [Azure Site Recovery](site-recovery-overview.md)в hello портал Azure.

Отправлять все комментарии hello нижней части этой статьи, или в hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



## <a name="architectural-components"></a>Компоненты архитектуры

Вот, что необходимо для репликации виртуальных машин Hyper-V tooa вторичный сайт VMM.

**Компонент** | **Расположение** | **Дополнительные сведения**
--- | --- | ---
**Таблицы Azure** | Подписка в Azure. | Создать хранилище служб восстановления в hello подписки Azure tooorchestrate и управление репликацией между расположениями VMM.
**Сервер VMM** | Необходимо иметь основное и дополнительное расположение VMM. | Мы рекомендуем сервера VMM в первичном сайте hello и по одному в hello вторичного сайта 
**Сервер Hyper-V** |  Один или несколько Hyper-V серверы на hello Первичное и вторичное облака VMM. | Данные реплицируются между hello первичных и вторичных серверах Hyper-V узла по локальной сети hello или VPN с использованием проверки подлинности Kerberos или сертификат.  
**Виртуальные машины Hyper-V** | Расположены на сервере узла Hyper-V. | сервер узла Hello источник должен иметь минимум одну виртуальную Машину, что требуется tooreplicate.

## <a name="replication-process"></a>Процесс репликации

1. Настройка hello учетная запись Azure, создайте хранилище служб восстановления и укажите, какие действия tooreplicate.
2. Можно настроить hello исходной и целевой настройки репликации, включая установки hello поставщика Azure Site Recovery на серверы VMM и агента служб восстановления Microsoft Azure hello на каждом узле Hyper-V.
3. Можно создать политику репликации для источника hello облака VMM. политика Hello — примененных tooall виртуальными машинами, размещенными на узлах в облаке hello.
4. Включить репликацию для каждой VMM и начальная репликация виртуальной машины выполняется в соответствии с выбранных настроек hello.
5. После начальной репликации начинается репликация разностных изменений. Отслеживаемые изменения для элемента хранятся в HRL-файле.


![Локальный tooon в локальной среде](./media/vmm-to-vmm-walkthrough-architecture/arch-onprem-onprem.png)

## <a name="failover-and-failback-process"></a>Процесс отработки отказа и восстановления размещения

1. Вы можете запустить плановую или внеплановую [отработку отказа](site-recovery-failover.md) между локальными сайтами. Если запустить плановую отработку отказа, то источник виртуальных машин, завершают работу tooensure без потери данных.
2. При сбое одного компьютера или создайте [планы восстановления](site-recovery-create-recovery-plans.md) tooorchestrate отработки отказа нескольких машин.
4. При выполнении внеплановой отработки отказа tooa вторичного сайта после hello отработка отказа машин в дополнительное расположение hello не включена для защиты или репликации. Если вы запустили плановой отработки отказа, после отработки отказа hello, защищенных машин в дополнительное расположение hello.
5. Затем доступ к нагрузки hello hello отработки отказа toostart фиксации из hello реплики виртуальной Машины.
6. Когда на первичном сайте снова станет доступной, необходимо инициировать tooreplicate обратная репликация из первичного toohello вторичного сайта hello. Обратная репликация приводит hello виртуальных машин в защищенное состояние, но hello вторичный центр обработки данных по-прежнему активное расположение hello.
7. toomake hello первичного сайта в активное расположение hello, инициируется плановую отработку отказа из вторичного tooprimary, следуют другой обратной репликации.



## <a name="next-steps"></a>Дальнейшие действия

Go слишком[шаг 2: просмотрите hello предварительные условия и ограничения](vmm-to-vmm-walkthrough-prerequisites.md).
