---
title: "ресурсы Azure tooreplicate aaaPrepare локальной tooAzure виртуальных машин VMware с помощью Azure Site Recovery | Документы Microsoft"
description: "Основные сведения, необходимые на месте в Azure перед началом репликации tooAzure виртуальных машин VMware в локальной среде, с помощью Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 4e320d9b-8bb8-46bb-ba21-77c5d16748ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: ac72fff0593783add789408ecfeb1812d70108b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-vmware-replication-tooazure"></a>Шаг 5: Подготовка ресурсов Azure для репликации tooAzure VMWare


Используйте инструкции hello в этой статье tooprepare Azure ресурсы, чтобы можно было реплицировать tooAzure локальной машины, с помощью hello [Azure Site Recovery](site-recovery-overview.md) службы.

Учет комментарии и вопросы hello нижней части этой статьи, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="before-you-start"></a>Перед началом работы

Убедитесь, что вы прочитали hello [предварительные требования](vmware-walkthrough-prerequisites.md)

## <a name="set-up-an-azure-account"></a>Настройка учетной записи Azure

- Получите [учетную запись Microsoft Azure](http://azure.microsoft.com/).
- Начните с [бесплатной пробной версии](https://azure.microsoft.com/pricing/free-trial/).
- Проверьте областей hello поддерживается для восстановления сайта в группе географическая доступность в [сведения о ценах Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
- Дополнительные сведения о [цены Site Recovery](site-recovery-faq.md#pricing)и получить hello [сведения о ценах](https://azure.microsoft.com/pricing/details/site-recovery/).



## <a name="set-up-an-azure-network"></a>Настроить сеть Azure

- Настройка сети Azure. Виртуальные машины Azure будут размещаться в этой сети при создании после отработки отказа.
- Восстановление сайта в hello портал Azure можно использовать настройки сетей в [диспетчера ресурсов](../resource-manager-deployment-model.md), или в классическом режиме.
- сеть Hello должны находиться в hello же регионе, что hello в хранилище службы восстановления
- Ознакомьтесь со сведениями о [ценах на виртуальную сеть](https://azure.microsoft.com/pricing/details/virtual-network/).
- Ознакомьтесь с дополнительными сведениями о [подключении к виртуальным машинам Azure](site-recovery-network-design.md) после отработки отказа.


## <a name="set-up-an-azure-storage-account"></a>Настроить учетную запись хранения Azure

- Site Recovery реплицирует tooAzure машин в локальном хранилище. Виртуальные машины Azure создаются из хранилища hello после отработки отказа.
- Настройте [учетную запись хранения Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) для реплицированных данных.
- Восстановление сайта в hello портал Azure можно использовать учетные записи хранения в диспетчере ресурсов или в классическом режиме.
- Hello учетной записи хранения может быть стандартной или [premium](../storage/common/storage-premium-storage.md).
- Если вы настроите учетную запись уровня "Премиум", вам также понадобится дополнительная учетная запись уровня "Стандартный" для данных журнала.


## <a name="next-steps"></a>Дальнейшие действия

Go слишком[шаг 6: Подготовка VMware ресурсы](vmware-walkthrough-prepare-vmware.md)
