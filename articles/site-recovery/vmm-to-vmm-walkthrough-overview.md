---
title: "aaaReplicate виртуальных машин Hyper-V tooa вторичный сайт VMM с помощью Azure Site Recovery | Документы Microsoft"
description: "Обзор репликации виртуальных машин Hyper-V tooa вторичный сайт VMM с помощью портала Azure hello."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 476ca82a-8f5c-4498-9dcf-e1011d60ed59
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: raynew
ms.openlocfilehash: 90e44bfc2237dfa7646fb2b7b1e533a7f6d83c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site"></a>Реплицировать виртуальные машины Hyper-V в VMM облаков tooa вторичного сайта, VMM

> [!div class="op_single_selector"]
> * [Портал Azure](site-recovery-vmm-to-vmm.md)
> * [Классический портал.](site-recovery-vmm-to-vmm-classic.md)
> * [PowerShell — Resource Manager](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

В этой статье содержится обзор hello действия требуются tooreplicate в локальной среде Hyper-V виртуальных машин (ВМ), управляемых в облаках диспетчера виртуальных машин System Center (VMM), tooa вторичного расположения VMM, с помощью [Azure Site Recovery](site-recovery-overview.md)в hello портал Azure.

После считывания в этой статье, отправлять любые комментарии, внизу hello, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="step-1-review-hello-scenario-architecture"></a>Шаг 1: Просмотрите архитектура сценария hello

Прежде чем начать развертывание, просмотрите hello архитектура сценария и убедитесь, что вы понимаете все компоненты hello необходим toodeploy.

Go слишком[шаг 1: обзор архитектуры hello](vmm-to-vmm-walkthrough-architecture.md).

## <a name="step-2-review-prerequisites-and-limitations"></a>Шаг 2. Просмотр предварительных условий и ограничений

Убедитесь, что вы понимаете предварительные условия для развертывания hello и ограничения.

**Необходимые компоненты Azure**: необходима подписка Microsoft Azure и служб восстановления Azure, хранилище, tooorchestrate и управление репликацией.
**Локальные серверы VMM и узлы Hyper-V.** Убедитесь, что серверы VMM и узлы Hyper-V совместимы и подготовлены к развертыванию Site Recovery.

Go слишком[шаг 2: Проверьте предварительные условия и ограничения](vmm-to-vmm-walkthrough-prerequisites.md).

## <a name="step-3-plan-networking"></a>Шаг 3. Планирование сетей

Необходимо toodo какой-либо сети, планирование tooensure, которые можно настроить сетевое сопоставление между сетями виртуальных Машин VMM при развертывании hello сценария.

Go слишком[Step 3: Планирование сети](vmm-to-vmm-walkthrough-network.md).


## <a name="step-4-prepare-vmm-and-hyper-v"></a>Шаг 4. Подготовка VMM и Hyper-V

Подготовка серверов VMM hello и узлов Hyper-V для развертывания службы восстановления сайтов.

Go слишком[шаг 4: Подготовка локальных серверов](vmm-to-vmm-walkthrough-vmm-hyper-v.md).

## <a name="step-5-set-up-a-vault"></a>Шаг 5. Настройка хранилища

Настройте хранилище служб восстановления. хранилище Hello содержит параметры конфигурации и управляет репликации.

[Шаг 5. Создание хранилища для репликации Hyper-V на дополнительный сайт](vmm-to-vmm-walkthrough-create-vault.md).

## <a name="step-6-set-up-source-and-target-settings"></a>Шаг 6. Настройка исходной и целевой среды

Настройка hello исходной и целевой репликации VMM местоположений. Добавьте хранилище toohello серверы VMM hello и загружать файлы установки hello для компонентов Site Recovery. Запустите программу установки поставщика Azure Site Recovery на сервере VMM hello. Программа установки устанавливает hello поставщика на сервере VMM hello и регистрирует hello сервер в хранилище hello. Установка агента служб восстановления Microsoft hello на каждом узле Hyper-V.

Go слишком[шаг 6: Настройка параметров исходной и целевой hello](vmm-to-vmm-walkthrough-source-target.md).

## <a name="step-7-configure-network-mapping"></a>Шаг 7. Настройка сетевого сопоставления

Сопоставьте сети виртуальных Машин VMM в исходном и целевом расположении hello. После отработки отказа виртуальные машины создаются в целевой сети hello, maps toohello исходной сетью виртуальной Машины в какой hello находится исходной виртуальной Машины Hyper-V.

Go слишком[шаг 7: Настройка сетевого сопоставления](vmm-to-vmm-walkthrough-network-mapping.md).


## <a name="step-8-set-up-a-replication-policy"></a>Шаг 8. Настройка политики репликации

Укажите, как виртуальные машины будут реплицироваться между расположениями VMM.

Go слишком[Step 8: настроить политику репликации](vmm-to-vmm-walkthrough-replication.md).


## <a name="step-9-enable-replication-for-vms"></a>Шаг 9. Включение репликации для виртуальных машин

Выберите виртуальные машины hello требуется tooreplicate. Включить виртуальную Машину для репликации триггеры hello начальной репликации toohello вторичного сайта, за которым следует текущих разностной репликации.

Go слишком[шаг 9: включить репликацию](vmm-to-vmm-walkthrough-enable-replication.md).


## <a name="step-10-run-a-test-failover"></a>Шаг 10. Запуск тестовой отработки отказа

Выполните тест отработки отказа toomake, убедиться, что все работает должным образом.

Go слишком[шаг 10: запустите тестовую отработку отказа](vmm-to-vmm-walkthrough-test-failover.md).
