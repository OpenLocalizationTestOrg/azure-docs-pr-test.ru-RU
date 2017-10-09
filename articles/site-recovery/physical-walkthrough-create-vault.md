---
title: "aaaSet копирование хранилища для tooAzure репликации физического сервера с помощью Azure Site Recovery | Документы Microsoft"
description: "Собраны действия hello необходимо tooset копирование tooAzure физических серверов tooreplicate хранилище, с помощью Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d99f2605-f417-4995-be77-5323136b814f
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 988928e3ece31116823f132cc39223fe44443468
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-set-up-a-vault-for-physical-server-replication-tooazure"></a>Шаг 6: Настройка хранилища для репликации tooAzure физического сервера


В этой статье описывается как tooset копии хранилища. Создание хранилища hello и укажите, какие действия tooreplicate из вашего tooAzure расположения в локальной среде, с помощью hello [Azure Site Recovery](site-recovery-overview.md) в hello портал Azure.


Учет комментарии и вопросы hello нижней части этой статьи, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).




## <a name="create-a-recovery-services-vault"></a>Создание хранилища служб восстановления

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a>Выбор целевого объекта защиты

Выберите объект tooreplicate, и когда необходимо tooreplicate для.

1. Щелкните **Хранилища служб восстановления** > хранилище.
2. В hello ресурсов меню, щелкните **Site Recovery** > **Подготовка инфраструктуры** > **цель защиты**.
3. В **цель защиты**выберите **tooAzure** > **не виртуализированных, другие**.


## <a name="next-steps"></a>Дальнейшие действия

Go слишком[шаг 7: Настройка исходного и конечного](physical-walkthrough-source-target.md)
