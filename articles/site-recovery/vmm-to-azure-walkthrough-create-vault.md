---
title: "aaaSet копирование хранилища для Hyper-V tooAzure репликации (с System Center VMM), с помощью Azure Site Recovery | Документы Microsoft"
description: "Собраны действия hello требуется tooset копии хранилища для Hyper-V tooAzure репликации (с помощью VMM), с помощью Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: b3cd6f03-c33c-406d-91d4-5cba69f79abd
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: f2c90f3c8b0a48db1e57fefd9829d29cffff8d43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-a-vault-for-hyper-v-replication"></a>Шаг 7. Настройка хранилища для репликации Hyper-V

В этой статье описывается настройка хранилища tooset и укажите, какие действия tooreplicate из папки в локальной среде, с помощью hello tooAzure [Azure Site Recovery](site-recovery-overview.md) в hello портал Azure.


Учет комментарии и вопросы hello нижней части этой статьи, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="create-a-recovery-services-vault"></a>Создание хранилища служб восстановления

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]



## <a name="select-a-protection-goal"></a>Выбор целевого объекта защиты

Выберите объект tooreplicate, и когда необходимо tooreplicate для.

1. Щелкните **Хранилища служб восстановления** > хранилище.
2. В hello ресурсов меню, щелкните **Site Recovery** > **Подготовка инфраструктуры** > **цель защиты**.
3. В **цель защиты**выберите **tooAzure** > **Да, с помощью Hyper-V**. Выберите **Да** вы tooconfirm nusing VMM. 

     ![Выбор цели](./media/vmm-to-azure-walkthrough-create-vault/choose-goals.png)



## <a name="next-steps"></a>Дальнейшие действия

Go слишком[Step 8: Настройка исходного и конечного](vmm-to-azure-walkthrough-source-target.md)
