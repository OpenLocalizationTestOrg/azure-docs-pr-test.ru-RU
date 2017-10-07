---
title: "aaaSet копирование хранилища для виртуальной Машины Azure repliction между регионами с Azure Site Recovery | Документы Microsoft"
description: "Собраны действия hello необходимо tooset копии хранилища Azure репликации между регионах Azure, с помощью Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: 40472189-3d80-4963-b175-8bddcbc2f61f
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: 9959c59c7ea57114763f13bf060404ddd267ba80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-set-up-a-vault-for-azure-tooazure-replication"></a>Шаг 4: Настройка хранилища Azure tooAzure репликации

После [Планирование сетей](azure-to-azure-walkthrough-network.md), использование этой статьи tooset копии хранилища для виртуальных машин (ВМ) Azure репликации tooanother регион Azure, с помощью hello [Azure Site Recovery](site-recovery-overview.md) в hello портал Azure.

- Завершив hello статьи, необходимо настроить хранилище служб восстановления.
- Отправлять все комментарии hello нижней части этой статьи, или задать вопросы в hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



>[!NOTE]
>
> Репликация виртуальных машин Azure сейчас доступна в режиме предварительной версии.




## <a name="create-a-vault"></a>Создание хранилища

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> Рекомендуется создать хранилище служб восстановления hello в hello место хранения вашей tooreplicate виртуальных машин. Например, если в целевом расположении hello центральный нам, создайте хранилище hello в **центральной части США**.


## <a name="next-steps"></a>Дальнейшие действия

Go слишком[шаг 5: включение репликации](azure-to-azure-walkthrough-enable-replication.md)
