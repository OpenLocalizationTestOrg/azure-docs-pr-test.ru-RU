---
title: "aaaEnable репликации для виртуальных машин Hyper-V, репликация tooAzure (без System Center VMM) с Azure Site Recovery | Документы Microsoft"
description: "Собраны действия hello необходимо tooAzure tooenable репликации для виртуальных машин Hyper-V с помощью службы Azure Site Recovery hello"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: bd31ef01-69f1-4591-a519-e42510a6e2f4
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: 1589cb7aa1fe954e075cb7bf1f4a4ec199ed3ec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-enable-replication-for-hyper-v-vms-replicating-tooazure"></a>Шаг 10: Включение репликации для виртуальных машин Hyper-V, репликация tooAzure


В этой статье описывается, как репликация tooenable для локальных виртуальных машин Hyper-V (не под управлением System Center VMM) tooAzure, с помощью hello [Azure Site Recovery](site-recovery-overview.md) в hello портал Azure.

Учет комментарии и вопросы hello нижней части этой статьи, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).




## <a name="before-you-start"></a>Перед началом работы

Прежде чем начать, убедитесь, что учетная запись Azure пользователя имеет необходимые hello [разрешений](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable репликацию новых tooAzure виртуальной машины.

## <a name="exclude-disks-from-replication"></a>Исключение дисков из репликации

По умолчанию реплицируются все диски на виртуальной машине. Диски можно исключить из репликации. Например tooreplicate диски с временные данные или данные, которая обновляется каждый раз, компьютер не имеет смысла или повторном запуске приложения (например pagefile.sys или базы данных tempdb SQL Server). [Дополнительные сведения](site-recovery-exclude-disk.md)


## <a name="replicate-vms"></a>Репликация виртуальных машин

Включите репликацию для виртуальных машин, сделав следующее.          

1. Выберите **Репликация приложения** > **Источник**. После настройки репликации для hello первый раз, можно щелкнуть **+ реплицировать** tooenable репликации для дополнительных компьютеров.

    ![Включение репликации](./media/hyper-v-site-walkthrough-enable-replication/enable-replication.png)
2. В **источника**, выберите узел Hyper-V hello. Нажмите кнопку **ОК**.
3. В **целевой**, выберите подписку хранилище hello и hello модель отработки отказа требуется toouse в Azure (классического или ресурса управления), после отработки отказа.
4. Выберите учетную запись хранения hello, требуется toouse. Если нет необходимости toouse учетную запись, вы можете [создать](#set-up-an-azure-storage-account). Нажмите кнопку **ОК**.
5. Выберите hello Azure toowhich сети и подсети виртуальных машин Azure подключится, когда они создаются отработки отказа.

    - Выберите tooapply hello параметры tooall виртуальных машин в сети включена для репликации, **настроить сейчас для всех выбранных компьютеров**.
    - Выберите **настроить позже** tooselect hello сети Azure на один компьютер.
    - Если у вас нет сети, требуется toouse, вы можете [создать](#set-up-an-azure-network). Выберите подсеть (если это применимо). Нажмите кнопку **ОК**.

   ![Включение репликации](./media/hyper-v-site-walkthrough-enable-replication/enable-replication11.png)

6. В **виртуальные машины** > **выберите виртуальные машины**щелкните и выберите каждый компьютер, tooreplicate. Можно выбрать только те компьютеры, для которых можно включить репликацию. Нажмите кнопку **ОК**.

    ![Включение репликации](./media/hyper-v-site-walkthrough-enable-replication/enable-replication5-for-exclude-disk.png)

7. В **свойства** > **Настройка свойств**выберите hello операционной системы для виртуальных машин выбранных hello и hello диска ОС.
8. Убедитесь, что hello виртуальной Машины Azure имя (целевой) соответствует [требования к виртуальной машине Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
9. По умолчанию выбраны все диски hello hello виртуальной Машины, для репликации. Снимите флажок дисков tooexclude их.
10. Нажмите кнопку **ОК** toosave изменений. Позже можно задать дополнительные свойства.

    ![Включение репликации](./media/hyper-v-site-walkthrough-enable-replication/enable-replication6-with-exclude-disk.png)

11. В **параметры репликации** > **Настройка параметров репликации**, выберите политику репликации hello требуется tooapply к hello защищенных виртуальных машин. Нажмите кнопку **ОК**. Можно изменить политику репликации hello в **политики репликации** > политики name > **изменение параметров**. Изменения будут применяться к компьютерам, для которых уже выполняется репликация, и к новым компьютерам.


   ![Включение репликации](./media/hyper-v-site-walkthrough-enable-replication/enable-replication7.png)

Вы можете отслеживать ход выполнения hello **включить защиту** задания в **заданий** > **задания Site Recovery**. После hello **окончательной установки защиты** задание запускается hello машина готова для отработки отказа.


## <a name="next-steps"></a>Дальнейшие действия


Go слишком[шаг 11: запустите тестовую отработку отказа](hyper-v-site-walkthrough-test-failover.md)
