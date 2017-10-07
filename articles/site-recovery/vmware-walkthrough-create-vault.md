---
title: "aaaSet копирование хранилища для VMware tooAzure репликации, с помощью Azure Site Recovery | Документы Microsoft"
description: "Собраны действия hello требуется tooset копирование хранилище для tooAzure репликации VMware с помощью Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8bce940e-f19f-4418-8360-aee7b073519a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 8a7755a6c9a3f55f241c615e425285bc4b782493
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-a-vault-for-vmware-replication-tooazure"></a>Шаг 7: Настройка хранилища для VMware tooAzure репликации


В этой статье описывается настройка хранилища tooset и укажите, какие действия tooreplicate из папки в локальной среде, с помощью hello tooAzure [Azure Site Recovery](site-recovery-overview.md) в hello портал Azure.


Учет комментарии и вопросы hello нижней части этой статьи, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).




## <a name="create-a-recovery-services-vault"></a>Создание хранилища служб восстановления

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a>Выбор целевого объекта защиты

Выберите объект tooreplicate, и когда необходимо tooreplicate для.

1. Щелкните **Хранилища служб восстановления** > хранилище.
2. В hello ресурсов меню, щелкните **Site Recovery** > **Подготовка инфраструктуры** > **цель защиты**.
3. В **цель защиты**выберите **tooAzure** > **Да, с VMware vSphere низкоуровневой оболочки**.



## <a name="next-steps"></a>Дальнейшие действия

Go слишком[Step 8: Настройка исходного и конечного](vmware-walkthrough-source-target.md)
