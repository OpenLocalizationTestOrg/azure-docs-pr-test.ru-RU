---
title: "aaaEnable tooAzure репликации для виртуальных машин Hyper-V в VMM облаков с помощью Azure Site Recovery | Документы Microsoft"
description: "Описывает, как облаков tooenable tooAzure репликации для виртуальных машин Hyper-V в VMM, с помощью службы Azure Site Recovery hello"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 89a2c4fc-7e03-4a86-a2c0-52831ccebc1a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 1a39bf65490c59a89a5e891184cadfacc2adee6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-11-enable-replication-tooazure-for-hyper-v-vms-in-vmm-clouds"></a>Шаг 11: Включение tooAzure репликации для виртуальных машин Hyper-V в облаках VMM

После настройки политики репликации, используйте статьи tooenable репликации для виртуальных машин Hyper-V локально (ВМ) управляются в облаках диспетчера виртуальных машин System Center (VMM)), tooAzure, с помощью hello [Azure Site Recovery](site-recovery-overview.md)в hello портал Azure.

Учет комментарии и вопросы hello нижней части этой статьи, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Перед началом

Убедитесь, что учетная запись Azure имеет правильные hello [разрешений](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)toocreate виртуальных машинах Azure. [Узнайте больше](../active-directory/role-based-access-built-in-roles.md) об управлении доступом на основе ролей в Azure.

## <a name="exclude-disks-from-replication"></a>Исключение дисков из репликации

По умолчанию реплицируются все диски на виртуальной машине. Диски можно исключить из репликации. Например tooreplicate диски с временные данные или данные, которая обновляется каждый раз, компьютер не имеет смысла или повторном запуске приложения (например pagefile.sys или базы данных tempdb SQL Server). [Дополнительные сведения](site-recovery-exclude-disk.md)

## <a name="replicate-vms"></a>Репликация виртуальных машин

Включите репликацию для виртуальных машин, сделав следующее.  

1. Последовательно выберите **Шаг 2. Репликация приложения** > **Источник**. После включения репликации hello первый раз, нажмите кнопку **+ реплицировать** в репликации tooenable hello хранилище для дополнительных компьютеров.

    ![Включение репликации](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication1.png)
2. В hello **источника** колонки, сервер VMM выберите hello и облака hello в какой hello Hyper-V находятся узлы. Нажмите кнопку **ОК**.

    ![Включение репликации](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication-source.png)
3. В **целевой**, выберите подписку hello, модель развертывания после отработки отказа, и hello учетной записи хранилища, которые вы используете для реплицированные данные.

    ![Включение репликации](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication-target.png)
4. Выберите учетную запись хранения hello, требуется toouse. Если требуется другой учетной записи хранилища от тех, у вас есть toouse можно [создать](#set-up-an-azure-storage-account). Если вы используете учетную запись хранения premium для реплицируемых данных, необходимо tooselect дополнительные стандартные журналы учетной записи хранения toostore репликации, отображающие data.toocreate организациями tooon текущие изменения учетной записи хранилища с помощью диспетчера ресурсов модели hello Нажмите кнопку **создать новый**. Toocreate учетной записи хранилища с помощью классической модели hello, выполните, [в hello портал Azure](../storage/common/storage-create-storage-account.md). Нажмите кнопку **ОК**.
5. Выберите hello Azure toowhich сети и подсети виртуальных машинах Azure будут подключаться, когда они создаются после отработки отказа. Выберите **настроить сейчас для всех выбранных компьютеров**, tooapply hello сетевой параметр tooall выбранные машины для защиты. Выберите **настроить позже**, tooselect hello сети Azure на один компьютер. Если требуется toouse другую сеть от тех, у вас есть, вы можете [создать](#set-up-an-azure-network). Здравствуйте, toocreate сети с помощью диспетчера ресурсов щелкните модель **создать новый**. Toocreate сети с помощью классической модели hello, выполните, [в hello портал Azure](../virtual-network/virtual-networks-create-vnet-classic-pportal.md). Выберите подсеть (если это применимо). Нажмите кнопку **ОК**.
6. В **виртуальные машины** > **выберите виртуальные машины**щелкните и выберите каждый компьютер, tooreplicate. Можно выбрать только те компьютеры, для которых можно включить репликацию. Нажмите кнопку **ОК**.

    ![Включение репликации](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication5.png)

7. В **свойства** > **Настройка свойств**выберите hello операционной системы для виртуальных машин выбранных hello и hello диска ОС.

    - Убедитесь, что hello виртуальной Машины Azure имя (целевой) соответствует [требования к виртуальной машине Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).   
    - По умолчанию выбраны все диски hello hello виртуальная машина для репликации, но tooexclude диски можно снять их.

        - Может потребоваться пропускная способность репликации tooexclude дисков tooreduce. Например не может потребоваться tooreplicate дисков с данными или перезагрузки данных, которая обновляется каждый раз, компьютер или приложений (например, файл подкачки pagefile.sys или tempdb Microsoft SQL Server). Hello диска можно исключить из репликации, сняв выделение hello диска.
        - Исключать можно только базовые диски. Нельзя исключить диски операционной системы.
        - Мы не рекомендуем исключать динамические диски. Site Recovery не может определить тип виртуального жесткого диска (базовый или динамический) в гостевой виртуальной машине. Если все зависимые динамические диски не исключены, hello защищенного динамического диска будет отображаться как неисправный диск при hello виртуальной Машины при сбое и hello данные на этом диске не будет доступен.
        - После включения репликации добавить или удалить диски для репликации нельзя. Если требуется tooadd или исключить диск, требуется toodisable защиты для виртуальной Машины hello и повторно включить.
        - Диски, созданные в Azure вручную, не будут восстановлены в исходном расположении. Например если сбой более чем трех дисков и создайте два непосредственно в виртуальной Машине Azure, только hello три диска которых были отработка отказа не будет выполнен обратно из Azure tooHyper-V. Нельзя включать дисков, созданных вручную в восстановление после сбоя или обратная репликация из tooAzure Hyper-V.
        - Если исключить диск, который требуется для toooperate приложения, после отработки отказа tooAzure необходимо toocreate его вручную в Azure, поэтому этот hello реплицируются приложения могут запускать. Кроме того службы автоматизации Azure может интегрировать в план восстановления, диск hello toocreate во время отработки отказа машины hello.

    Нажмите кнопку **ОК** toosave изменений. Позже можно задать дополнительные свойства.

    ![Включение репликации](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication6-with-exclude-disk.png)

8. В **параметры репликации** > **Настройка параметров репликации**, выберите политику репликации hello требуется tooapply к hello защищенных виртуальных машин. Нажмите кнопку **ОК**. Можно изменить политику репликации hello в **политики репликации** > имя политики > **изменение параметров**. Изменения будут применены как к ВМ, для которых уже выполняется репликация, так и к новым ВМ.

   ![Включение репликации](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication7.png)

Вы можете отслеживать ход выполнения hello **включить защиту** задания в **заданий** > **задания Site Recovery**. После hello **окончательной установки защиты** выполняется задание, hello машина готова для отработки отказа.



## <a name="next-steps"></a>Дальнейшие действия

Go слишком[шаг 12: запустите тестовую отработку отказа](vmm-to-azure-walkthrough-test-failover.md)
