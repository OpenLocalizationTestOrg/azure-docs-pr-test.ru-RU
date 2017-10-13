---
title: "Подготовка ресурсов Azure для репликации виртуальных машин VMware из локальной среды в Azure с помощью Azure Site Recovery | Документация Майкрософт"
description: "Эта статья содержит сведения о компонентах, которые необходимо настроить в Azure, прежде чем приступить к репликации виртуальных машин VMware из локальной среды в Azure с помощью Azure Site Recovery."
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
ms.openlocfilehash: 40abff72278c9f8d9f701023fd473fe52c17b421
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="step-5-prepare-azure-resources-for-vmware-replication-to-azure"></a>Шаг 5. Подготовка ресурсов Azure для репликации из VMWare в Azure


Используйте инструкции этой статьи, чтобы подготовить ресурсы Azure для репликации виртуальных машин из локальной среды в Azure с помощью службы [Azure Site Recovery](site-recovery-overview.md).

Комментарии или вопросы можно добавить в конце этой статьи или на [форуме по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="before-you-start"></a>Перед началом работы

Ознакомьтесь со статьей о [предварительных требованиях](vmware-walkthrough-prerequisites.md).

## <a name="set-up-an-azure-account"></a>Настройка учетной записи Azure

- Получите [учетную запись Microsoft Azure](http://azure.microsoft.com/).
- Начните с [бесплатной пробной версии](https://azure.microsoft.com/pricing/free-trial/).
- Сведения о поддерживаемых регионах для Site Recovery см. в разделе "Географическая доступность" на странице [цен на службу Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
- Ознакомьтесь с расходами [при использования Site Recovery](site-recovery-faq.md#pricing) и [сведениями о ценах](https://azure.microsoft.com/pricing/details/site-recovery/).



## <a name="set-up-an-azure-network"></a>Настроить сеть

- Настройка сети Azure. Виртуальные машины Azure будут размещаться в этой сети при создании после отработки отказа.
- Используя службу Site Recovery на портале Azure, можно настроить сети в [Resource Manager](../resource-manager-deployment-model.md) или в классическом режиме.
- Сеть должна располагаться в том же регионе, что и хранилище служб восстановления.
- Ознакомьтесь со сведениями о [ценах на виртуальную сеть](https://azure.microsoft.com/pricing/details/virtual-network/).
- Ознакомьтесь с дополнительными сведениями о [подключении к виртуальным машинам Azure](site-recovery-network-design.md) после отработки отказа.


## <a name="set-up-an-azure-storage-account"></a>Настроить учетную запись хранения Azure

- Служба Site Recovery реплицирует локальные машины в службе хранилища Azure. После отработки отказа виртуальные машины Azure создаются из хранилища.
- Настройте [учетную запись хранения Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) для реплицированных данных.
- Используя службу Site Recovery на портале Azure, можно настроить учетные записи хранения в Resource Manager или в классическом режиме.
- Учетная запись хранения может быть уровня "Стандартный" или [Премиум](../storage/common/storage-premium-storage.md).
- Если вы настроите учетную запись уровня "Премиум", вам также понадобится дополнительная учетная запись уровня "Стандартный" для данных журнала.


## <a name="next-steps"></a>Дальнейшие действия

Перейдите к разделу [Шаг 6. Подготовка ресурсов VMware](vmware-walkthrough-prepare-vmware.md).
