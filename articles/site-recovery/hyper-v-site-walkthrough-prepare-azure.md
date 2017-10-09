---
title: "с помощью Azure Site Recovery виртуальных машин Hyper-V (без System Center VMM) tooAzure aaaPrepare ресурсы Azure tooreplicate | Документы Microsoft"
description: "Основные сведения, необходимые на месте в Azure перед началом репликации с помощью Azure Site Recovery tooAzure виртуальных машин Hyper-V (без VMM)"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 28fa722c-675e-4637-98eb-7ccbf3806d69
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: f659e300c39253b0eaf7218bee9d39b11682edb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-hyper-v-replication-tooazure"></a>Шаг 5: Подготовка ресурсов Azure для tooAzure репликации Hyper-V

Используйте инструкции hello в этой статье tooprepare Azure, чтобы можно было реплицировать локальные ресурсы виртуальных машин Hyper-V (без System Center VMM) с помощью hello tooAzure [Azure Site Recovery](site-recovery-overview.md) службы.

После считывания в этой статье, отправлять любые комментарии внизу hello или задавайте технические вопросы на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="before-you-start"></a>Перед началом работы

Убедитесь, что вы прочитали hello [предварительные требования](hyper-v-site-walkthrough-prerequisites.md)

## <a name="set-up-an-azure-account"></a>Настройка учетной записи Azure

- Получите [учетную запись Microsoft Azure](http://azure.microsoft.com/).
- Начните с [бесплатной пробной версии](https://azure.microsoft.com/pricing/free-trial/).
- Проверьте областей hello поддерживается для восстановления сайта в группе географическая доступность в [сведения о ценах Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
- Дополнительные сведения о [цены Site Recovery](site-recovery-faq.md#pricing)и получить hello [сведения о ценах](https://azure.microsoft.com/pricing/details/site-recovery/).


## <a name="set-up-an-azure-network"></a>Настроить сеть Azure

- Настройка сети Azure. Виртуальные машины Azure будут размещаться в этой сети при создании после отработки отказа.
- сеть Hello должны находиться в hello же регионе, что hello в хранилище службы восстановления
- Восстановление сайта в hello портал Azure можно использовать настройки сетей в [диспетчера ресурсов](../resource-manager-deployment-model.md), или в классическом режиме.
- Рекомендуется настроить сеть перед началом работы. Если этого не сделать, то необходимо toodo его во время развертывания службы восстановления сайтов.
- Ознакомьтесь со сведениями о [ценах на виртуальную сеть](https://azure.microsoft.com/pricing/details/virtual-network/).


## <a name="set-up-an-azure-storage-account"></a>Настроить учетную запись хранения Azure

- Site Recovery реплицирует tooAzure машин в локальном хранилище. Виртуальные машины Azure создаются из хранилища hello после отработки отказа.
- Настройка standard и premium [учетной записи хранилища Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) tooAzure репликации toohold данных.
- [Хранилище Premium](../storage/common/storage-premium-storage.md) обычно используется для виртуальных машин, требующих постоянно высокое производительности операций ввода-ВЫВОДА и toohost низкую задержку операций ввода-ВЫВОДА интенсивных рабочих нагрузок.
- Если вы хотите toouse toostore учетной записи premium реплицированные данные, необходимо также стандартные журналы учетной записи хранения toostore репликации, отслеживания текущих изменений tooon локальные данные.
- В зависимости от модели ресурсов hello хотите toouse отработку отказа виртуальных машин Azure, настройте учетную запись в [режим диспетчера ресурсов](../storage/common/storage-create-storage-account.md), или [классический режим](../storage/common/storage-create-storage-account.md).
- Рекомендуется настроить учетную запись хранения до начала работы. Если не требуется toodo его во время развертывания службы восстановления сайтов. Hello должны находиться в hello же регионе, что hello в хранилище служб восстановления.
- Не удается переместить использовать учетные записи хранения с Site Recovery для групп ресурсов в hello же подписки, или в разных подписках.


## <a name="next-steps"></a>Дальнейшие действия

Go слишком[шаг 6: ресурсы Подготовка Hyper-V](hyper-v-site-walkthrough-prepare-hyper-v.md)
