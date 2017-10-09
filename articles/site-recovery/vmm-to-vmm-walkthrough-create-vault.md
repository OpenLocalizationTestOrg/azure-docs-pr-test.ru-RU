---
title: "aaaCreate хранилища для Hyper-V репликации tooa вторичного сайта с помощью Azure Site Recovery | Документы Microsoft"
description: "Описывает, как toocreate хранилище при репликации виртуальных машин Hyper-V tooa получателей System Center VMM сайта с Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: ff65dbfb-cb26-410e-ab48-76971625db08
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 96ee09cbf2376a5089b9efa09dc7ab3fb7d472cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-create-a-vault-for-hyper-v-replication-tooa-secondary-site"></a>Шаг 5: Создание хранилища для Hyper-V репликации tooa вторичного сайта

После подготовки локальной [серверы диспетчера виртуальных машин System Center (VMM) и узлы Hyper-V и кластеры](vmm-to-vmm-walkthrough-vmm-hyper-v.md) для Hyper-V репликации tooa вторичного сайта с помощью [Azure Site Recovery](site-recovery-overview.md), можно создать Хранилище служб восстановления и выберите hello сценарий репликации.

После считывания в этой статье, отправлять любые комментарии, внизу hello, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="create-a-recovery-services-vault"></a>Создание хранилища служб восстановления

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]


## <a name="choose-a-protection-goal"></a>Выбор цели защиты

Выберите том, что необходимо tooreplicate, а также место tooreplicate для.

1. Щелкните **Site Recovery** > **Шаг 1. Подготовка инфраструктуры** > **Цель защиты**.
2. Выберите **сайта toorecovery**и выберите **Да, с помощью Hyper-V**.
3. Выберите **Да** tooindicate вы используете узлов Hyper-V hello toomanage VMM.
4. Выберите **Да**, если используется дополнительный сервер VMM. Если вы развертываете репликацию между облаками, развернутыми на одном сервере VMM, щелкните **Нет**. Нажмите кнопку **ОК**.

    ![Выбор цели](./media/vmm-to-vmm-walkthrough-create-vault/choose-goals.png)



## <a name="next-steps"></a>Дальнейшие действия

Go слишком[шаг 6: Настройка hello репликации исходной и целевой](vmm-to-vmm-walkthrough-source-target.md).
