---
title: "вторичный сайт Hyper-V aaaEnable репликации tooa с Azure Site Recovery | Документы Microsoft"
description: "Описывает, как tooenable репликации для виртуальных машин Hyper-V, репликация tooa получателей System Center VMM сайта с помощью Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d8782d14-9fef-4396-8912-ff945efc851b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: b4484e0118cb23f343187fe867d9795d30926baf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-enable-replication-tooa-secondary-site-for-hyper-v-vms"></a>Шаг 9: Включение репликации tooa вторичного сайта для виртуальных машин Hyper-V


После настройки политики репликации, этот статье tooenable репликации tooa получателей диспетчера виртуальных машин System Center (VMM) сайт используется для локального Hyper-V виртуальных машин (ВМ) с помощью [Azure Site Recovery](site-recovery-overview.md).

После считывания в этой статье, отправлять любые комментарии, внизу hello, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



## <a name="select-vms-tooreplicate"></a>Выберите tooreplicate виртуальные машины

1. Последовательно выберите **Шаг 2. Репликация приложения** > **Источник**. 

    ![Включение репликации](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication1.png)

2. В **источника**, выберите сервер VMM hello и облака, в которых hello находятся узлы Hyper-V требуется tooreplicate hello. Нажмите кнопку **ОК**.

    ![Включение репликации](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication2.png)
3. В **целевой**, проверьте hello дополнительный сервер VMM и облака.
4. В **виртуальные машины**, выберите виртуальные машины hello требуется tooprotect из списка hello.

    ![Включение защиты виртуальной машины](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication5.png)

Вы можете отслеживать ход выполнения hello **включить защиту** действия в **заданий** > **задания Site Recovery**. После hello **окончательной установки защиты** завершения задания, hello начальная репликация завершается и hello виртуальная машина будет готова для отработки отказа.

Обратите внимание на следующее.

- Можно также включить защиту для виртуальных машин в консоли VMM hello. Нажмите кнопку **включить защиту** на панели инструментов hello в свойствах виртуальной машины hello > **Azure Site Recovery** вкладки.
- После включения репликации, можно просмотреть свойства для hello виртуальной Машины в **реплицируются элементы**. На hello **Essentials** панели мониторинга, можно просмотреть информацию о политике репликации hello hello виртуальной Машины и ее состояние. Щелкните **Свойства** для получения дополнительных сведений.

## <a name="onboard-existing-vms"></a>Включение имеющихся виртуальных машин

Если в VMM есть виртуальные машины, которые реплицируются с помощью реплики Hyper-V, их можно включить в репликацию Azure Site Recovery следующим образом.

1. Убедитесь, что сервер hello Hyper-V, размещающий hello существующей виртуальной Машины находится в основное облако hello и вторичное облако hello расположен сервер Hyper-V, hello, размещение hello реплики виртуальной машины.
2. Убедитесь, что политика репликации настроена для hello основное облако VMM.
3. Включение репликации для основной виртуальной машины hello. Восстановления сайтов Azure и VMM убедитесь, что hello того же сервера реплики и виртуальной машины обнаруживается и будет использовать Azure Site Recovery и установить репликацию с использованием hello указаны параметры.


## <a name="next-steps"></a>Дальнейшие действия

Go слишком[шаг 10: запустите тестовую отработку отказа](vmm-to-vmm-walkthrough-test-failover.md).
