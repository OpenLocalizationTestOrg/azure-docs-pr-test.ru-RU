---
title: "aaaSet политику репликации для виртуальной Машины Hyper-V (с помощью VMM) tooAzure репликации с помощью Azure Site Recovery | Документы Microsoft"
description: "Описывает способ tooset политику репликации для виртуальной Машины Hyper-V (с помощью VMM) tooAzure репликации с помощью Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: ee808b20-324b-4198-b831-edb65b95e8b7
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: e1579fde559ca34eca19a01e740fec28a0df2f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-set-up-a-replication-policy-for-hyper-v-vm-replication-with-vmm-tooazure"></a>Шаг 10: Настройка политики репликации для виртуальных Машин Hyper-V tooAzure репликации (с помощью VMM)


После настройки [сетевое сопоставление](vmm-to-azure-walkthrough-network-mapping.md), использование этой статьи tooconfigure политику репликации T\tooreplicate локальных виртуальных машин Hyper-V управляются в облаках tooAzure диспетчера виртуальных машин System Center (VMM), с помощью hello [ Azure Site Recovery](site-recovery-overview.md) в hello портал Azure.

После считывания в этой статье, отправлять любые комментарии, внизу hello, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



## <a name="create-a-policy"></a>Создание политики

1. Щелкните toocreate новую политику репликации **подготовки инфраструктуры** > **параметры репликации** > **+ Создание и связывание**.

    ![Сеть](./media/vmm-to-azure-walkthrough-replication/gs-replication.png)
2. На странице **Создать и связать политику**укажите имя политики.
3. В **частота копирования**, укажите, как часто tooreplicate дельта-данные после начальной репликации hello (каждые 30 секунд, 5 или 15 минут).

    > [!NOTE]
    >  30 второй частоты не поддерживается при репликации toopremium хранилища. ограничение Hello определяется hello число моментальных снимков для каждого большого двоичного объекта (100), поддерживаемое хранилище premium. [Дополнительные сведения](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob)

4. В **хранения точки восстановления**, укажите в часах, как долго будет hello окна хранения для каждой из точек восстановления. Защищенные виртуальные машины могут быть восстановлены tooany точки внутри окна.
5. В поле **Периодичность создания моментальных снимков с согласованием приложений** укажите, как часто (от 1 до 12 часов) будут создаваться точки восстановления, содержащие согласованные с приложениями моментальные снимки. Hyper-V использует два типа моментальных снимков — стандартного моментального снимка, которая обеспечивает добавочный моментальный снимок всей виртуальной машины hello и согласованных с приложением моментальный снимок, создает моментальный снимок в момент данные приложения hello виртуальной машине hello. Моментальные снимки приложений используйте tooensure службы теневого копирования томов (VSS), приложения находятся в согласованном состоянии при hello моментального снимка. Обратите внимание, что при включении снимков приложений влияет на hello производительность приложений, работающих на исходных виртуальных машинах. Убедитесь, что hello значение, заданное меньше, чем количество дополнительных точек восстановления, настроенные в hello.
6. В **время начала начальной репликации**, указывают, когда toostart hello начальной репликации. Hello репликация выполняется по пропускной способности Интернета, поэтому вы можете tooschedule его вне вашей занятости времени.
7. В **шифровать данные, хранящиеся в Azure**, укажите ли tooencrypt rest данные в хранилище Azure. Нажмите кнопку **ОК**.

    ![Политика репликации](./media/vmm-to-azure-walkthrough-replication/gs-replication2.png)
8. При создании новой политики она автоматически связывается с hello облака VMM. Нажмите кнопку **ОК**. Дополнительные облака VMM (и hello виртуальных машин в них) можно связать с этой политикой репликации в **репликации** > имя политики > **связывание облака VMM**.

    ![Политика репликации](./media/vmm-to-azure-walkthrough-replication/policy-associate.png)



## <a name="next-steps"></a>Дальнейшие действия

Go слишком[шаг 11: включение репликации](vmm-to-azure-walkthrough-enable-replication.md)
