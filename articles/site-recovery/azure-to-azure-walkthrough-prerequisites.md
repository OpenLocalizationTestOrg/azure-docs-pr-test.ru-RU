---
title: "При репликации виртуальных машин Azure tooanother области aaaBefore | Документы Microsoft"
description: "Собраны действия hello необходимо tootake перед репликацией между регионами Azure, с помощью службы Azure Site Recovery hello виртуальных машинах Azure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: 7fa633075eeb52d0c184a1dd8d53ccc15644f518
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-before-you-start"></a>Шаг 2. Перед началом работы

После знакомства hello [архитектура](azure-to-azure-walkthrough-architecture.md) для репликации виртуальных машин (ВМ) Azure между областей Azure с [Azure Site Recovery](site-recovery-overview.md), использование предварительных требований tooverify этой статьи. 

- Завершив hello статьи, должны иметь clear понять что требуется развертывание hello toomake работать и будут завершены обязательные шаги hello.
- Отправлять все комментарии hello нижней части этой статьи, или задать вопросы в hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

>[!NOTE]
>
> Репликация виртуальных машин Azure сейчас доступна в режиме предварительной версии.



## <a name="support-recommendations"></a>Рекомендации по поддержке

Таблица hello проверки ниже.

**Компонент** | **Требование**
--- | ---
**Хранилище служб восстановления** | Рекомендуется создавать хранилище служб восстановления, в конечном hello регион Azure, что требуется toouse для аварийного восстановления. Например если вы хотите tooreplicate источник виртуальных машин в tooCentral США, восток США, создайте хранилище hello в центральной части США.
**Подписка Azure.** | Подписки Azure должно быть включено toocreate виртуальных машин, в целевое расположение hello, что требуется toouse как hello аварийного восстановления область. Обратитесь в службу поддержки tooenable hello требуется квота.
**Емкость в целевом регионе** | Подписки hello hello целевой регион Azure, должна иметь достаточно мощности для виртуальных машин, учетных записей хранения и сетевых компонентов.
**Хранилище** | Используйте hello [руководство по организации хранилища](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) источника виртуальных машинах Azure, tooavoid проблем с производительностью.<br/><br/> Учетные записи хранения должна находиться в hello же регионе, что хранилище hello.<br/><br/> Не удается выполнить репликацию учетных записей toopremium в центральной и Южной Индии.<br/><br/> При развертывании репликации с параметрами по умолчанию hello Site Recovery создает hello необходимые учетные записи хранения на основе конфигурации источника hello. При настройке параметров выполните hello [целевые показатели масштабируемости для дисков виртуальной Машины](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks).
**Сеть** | Необходимо tooallow исходящие подключения из виртуальных машин Azure, для конкретного URL-адреса или IP-диапазонов.<br/><br/> Сети должны находиться в hello же регионе, что хранилище hello. 
**Azure** | Убедитесь, что все последние корневых сертификатов hello находятся на hello виртуальной Машины Azure для Windows и Linux. Если они не будет возможности tooregister hello виртуальной Машины в Site Recovery, из-за ограничений безопасности.
**Учетная запись Azure** | Учетная запись пользователя Azure должен toohave определенных [разрешений](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable репликацию виртуальной машины Azure.

Получить полный список требований к поддержке в hello [Матрица поддержки](site-recovery-support-matrix-azure-to-azure.md)


## <a name="set-permissions-on-hello-account"></a>Установка разрешений для учетной записи hello

1. Узнайте, как hello [разрешений](site-recovery-role-based-linked-access-control.md) необходимо для репликации.
2. Выполните следующие [инструкции](../active-directory/role-based-access-control-configure.md#add-access) tooadd разрешения.


## <a name="verify-target-resources"></a>Проверка целевых ресурсов

1. Включить вашей подписки Azure tooallow toocreate ВМ в hello ориентировании области требуется toouse для аварийного восстановления, которые должны toouse как hello аварийного восстановления область. Обратитесь в службу поддержки tooenable hello требуется квота.
2. Убедитесь, что ваша подписка имеет достаточно ресурсов tooenable виртуальные машины, с размеры, которые соответствуют источнику виртуальных машин. По умолчанию при настройке репликации Site Recovery подбора hello того же размера hello целевым ВМ или hello ближайший возможный размер. Дополнительные сведения об [устранении неполадок](site-recovery-azure-to-azure-troubleshoot-errors.md#azure-resource-quota-issues-error-code-150097) с целевыми ресурсами.

## <a name="verify-azure-vm-certificates"></a>Проверка сертификатов виртуальной машины Azure

1. Проверьте все корневые сертификаты последнюю hello, присутствуют в hello Windows или виртуальных машин Linux требуется tooreplicate. Если отсутствуют последние корневые сертификаты hello, hello виртуальной Машины не может быть зарегистрированных tooSite восстановления из-за ограничений toosecurity.
2. Для ВМ Windows hello следующие:

    - Установите последние обновления Windows все hello на hello виртуальной Машины, таким образом, все hello доверенных корневых сертификатов на компьютере hello.
    - В отключенной среде этапа hello Стандартная центра обновления Windows процесса или сертификат обновления в организации, tooget hello последнюю корневых сертификатов и обновленного списка CRL на виртуальных машинах hello.
3. Для виртуальных машин Linux выполните hello руководстве для Linux распространителя tooget hello последнюю доверенные корневые сертификаты и последний список отзыва сертификатов hello на hello виртуальной Машины. Дополнительные сведения об [устранении неполадок](site-recovery-azure-to-azure-troubleshoot-errors.md#trusted-root-certificates-error-code-151066) с доверенными корневыми сертификатами.


## <a name="next-steps"></a>Дальнейшие действия

Go слишком[Step 3: Планирование сети](azure-to-azure-walkthrough-network.md) tooset копирование исходящие подключения.
