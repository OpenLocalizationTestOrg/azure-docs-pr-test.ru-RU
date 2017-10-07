---
title: "aaaMigrate виртуальные машины IaaS Azure между регионами Azure | Документы Microsoft"
description: "Используйте виртуальные машины Azure IaaS Azure Site Recovery toomigrate из tooanother один регион Azure."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8a29e0d9-0010-4739-972f-02b8bdf360f6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: c84dc77716b8d19969eab60707ed1332ca39b893
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-azure-iaas-virtual-machines-between-azure-regions-with-azure-site-recovery"></a>Перенос виртуальных машин IaaS Azure между регионами Azure с помощью Azure Site Recovery
## <a name="overview"></a>Обзор
Вас приветствует tooAzure Site Recovery. В этой статье следует используйте, если необходимо, чтобы виртуальные машины Azure toomigrate между регионами Azure. Перед началом работы обратите внимание на следующее:

* В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: модель Azure Resource Manager и классическая модель. Azure также содержит два портала — hello классический портал Azure, поддерживающий hello классической модели развертывания и hello портал Azure с поддержкой обе модели развертывания. Hello основные шаги для миграции: hello же ли в диспетчере ресурсов или в классическом настраиваете Site Recovery. Однако hello инструкции пользовательского интерфейса и снимки экрана в этой статье относятся к hello портал Azure.
* **В настоящее время только можно переносить из одного региона tooanother. Можно выполнить переход виртуальных машин из одного региона Azure tooanother, но вы не удается восстановить после сбоя их еще раз.**

Отправьте все комментарии или вопросы hello нижней части этой статьи, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="prerequisites"></a>Предварительные требования
Вот что нужно для этого развертывания:

* **Виртуальные машины IaaS**: hello требуется toomigrate виртуальных машин. При переносе виртуальных машин используйте те же инструкции, что и для физических компьютеров.

## <a name="deployment-steps"></a>Шаги по развертыванию
Этот раздел описывает шаги развертывания hello hello новый портал Azure.

1. [Создайте хранилище](site-recovery-vmware-to-azure.md).
2. [Включите репликацию](site-recovery-vmware-to-azure.md). Включите репликацию hello виртуальные машины toomigrate и задайте Azure в качестве источника. 
3. [ Запустите внеплановую отработку отказа](site-recovery-failover.md). После завершения начальной репликации запускаются незапланированной отработки отказа из одного региона Azure tooanother. При необходимости можно создать план восстановления и запускать несколько виртуальных машин незапланированной отработки отказа, toomigrate между регионами. [Узнайте подробнее](site-recovery-create-recovery-plans.md) о планах восстановления.

## <a name="next-steps"></a>Дальнейшие действия
Сведения о других сценариях репликации см. в статье [Что такое Site Recovery?](site-recovery-overview.md)
