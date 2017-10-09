---
title: "aaaSet копирование хранилища для Hyper-V tooAzure репликации (без System Center VMM), с помощью Azure Site Recovery | Документы Microsoft"
description: "Собраны действия hello требуется tooset копирование хранилище для tooAzure репликации Hyper-V с помощью Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a936b3e2-0dbe-47ac-a98e-5285d96dc786
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: e3ef8758faab36d19d0968d98a23105bed7830f6
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
3. В **цель защиты**выберите **tooAzure** > **Да, с помощью Hyper-V**. Выберите **нет** tooconfirm, вы не используете VMM. 

    ![Выбор цели](./media/hyper-v-site-walkthrough-create-vault/choose-goals2.png)



## <a name="next-steps"></a>Дальнейшие действия

Go слишком[Step 8: Настройка исходного и конечного](hyper-v-site-walkthrough-source-target.md)
