---
title: "aaaReplicate виртуальных машинах Azure между регионами Azure | Документы Microsoft"
description: "Обобщает hello действия требуется tooreplicate виртуальных машинах Azure между регионами Azure со службой Azure Site Recovery hello в hello портал Azure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: 6dd36239-4363-4538-bf80-a18e71b8ec67
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: f4ac386f040945131f8a10f02143437f4441e298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a>Репликация виртуальных машин Azure между регионами с помощью Azure Site Recovery

>В этой статье Обзор tooreplicate необходимые шаги hello Azure виртуальных машин (ВМ) в tooAzure одного региона Azure виртуальные машины в другом регионе. 

>[!NOTE]
>
> Репликация виртуальных машин Azure сейчас доступна в режиме предварительной версии.

Учет комментарии и вопросы hello нижней части этой статьи, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="step-1-review-architecture"></a>Шаг 1. Общие сведения об архитектуре

Перед началом развертывания ознакомьтесь архитектура сценария hello и hello компоненты, необходимые toodeploy.

Go слишком[шаг 1: обзор архитектуры hello](azure-to-azure-walkthrough-architecture.md)


## <a name="step-2-review-prerequisites"></a>Шаг 2. Проверка предварительных требований

Проверьте, что у hello Azure необходимые компоненты в местах, включая подписки, виртуальных сетей, учетные записи хранения и требования виртуальной Машины.

Go слишком[шаг 2: Проверьте предварительные условия и ограничения](azure-to-azure-walkthrough-prerequisites.md)


## <a name="step-3-plan-networking"></a>Шаг 3. Планирование сетей

Проверьте, что исходящие подключения настроены на виртуальных машинах Azure, требуется tooreplicate и подключения из локального настраиваются.

Go слишком[шаг 4: Планирование сети](azure-to-azure-walkthrough-network.md)



## <a name="step-4-create-a-vault"></a>Шаг 4. Создание хранилища 

Требуется tooset копирование tooorchestrate хранилище служб восстановления и управление репликацией и укажите регион источника hello.

Go слишком[шаг 4: Создание хранилища](azure-to-azure-walkthrough-vault.md)


## <a name="step-5-enable-replication"></a>Шаг 5. Включение репликации


репликация tooenable, настройте параметры целевого расположения, настройте политику репликации и выберите hello виртуальных машинах Azure, которые должны tooreplicate. После включения, происходит начальной репликации hello виртуальной Машины.

Go слишком[шаг 5: включение репликации](azure-to-azure-walkthrough-enable-replication.md)


## <a name="step-6-run-a-test-failover"></a>Шаг 6. Выполнение тестовой отработки отказа

После завершения первоначальной репликации, а разностная репликация выполняется, можно запустить тест отработки отказа toomake, убедиться, что все работает правильно.

Go слишком[шаг 6: запустите тестовую отработку отказа](azure-to-azure-walkthrough-test-failover.md)


