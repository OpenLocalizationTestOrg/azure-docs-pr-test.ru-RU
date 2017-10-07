---
title: "aaaReplicate виртуальных машин Hyper-V в VMM облаков tooAzure с Azure Site Recovery | Документы Microsoft"
description: "Общие сведения для репликации виртуальных машин Hyper-V в tooAzure облака VMM, с помощью службы Azure Site Recovery hello"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: d6f729a49cc86ea07bebc4d7266fd7b58b3998f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-site-recovery-in-hello-azure-portal"></a>Реплицировать виртуальные машины Hyper-V в tooAzure облака VMM, использование в hello портала Azure Site Recovery
> [!div class="op_single_selector"]
> * [Портал Azure](site-recovery-vmm-to-azure.md)
> * [Классическая модель Azure](site-recovery-vmm-to-azure-classic.md)
> * [PowerShell — Resource Manager](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [PowerShell — классическая модель](site-recovery-deploy-with-powershell.md)


В этой статье приведены общие сведения о необходимых tooreplicate действия hello в локальной среде Hyper-V виртуальных машин (ВМ), управляемых в tooAzure облаках диспетчера виртуальных машин System Center (VMM), с помощью hello [Azure Site Recovery](site-recovery-overview.md) в Здравствуйте, портал Azure.

После считывания в этой статье, отправлять любые комментарии, внизу hello, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="step-1-review-hello-scenario-architecture"></a>Шаг 1: Просмотрите архитектура сценария hello

Прежде чем начать развертывание, просмотрите hello архитектура сценария и убедитесь, что вы понимаете все компоненты hello необходим toodeploy.

Go слишком[шаг 1: обзор архитектуры hello](vmm-to-azure-walkthrough-architecture.md)

## <a name="step-2-review-prerequisites-and-limitations"></a>Шаг 2. Просмотр предварительных условий и ограничений

Убедитесь, что вы понимаете предварительные условия для развертывания hello и ограничения.

**Предварительные требования Azure**: учетная запись Microsoft Azure, сети Azure и учетные записи хранения.
**Локальные серверы VMM и узлы Hyper-V.** Убедитесь, что серверы VMM и узлы Hyper-V совместимы и подготовлены к развертыванию Site Recovery.
**Репликация виртуальных машин**: Убедитесь, что требуется tooreplicate виртуальные машины соответствуют требованиям Azure.

Go слишком[шаг 2: Проверьте предварительные условия и ограничения](vmm-to-azure-walkthrough-prerequisites.md)

## <a name="step-3-plan-capacity"></a>Шаг 3. Планирование ресурсов

При выполнении полного развертывания, необходимо toofigure какие ресурсы репликации необходимо. Существует несколько из доступных toohelp средства это сделать. Если вы выполняете быстро настроить среду tootest hello, этот шаг можно пропустить.

Go слишком[Step 3: Планирование емкости](vmm-to-azure-walkthrough-capacity.md)

## <a name="step-4-plan-networking"></a>Шаг 4. Планирование сетей

Необходимо toodo какой-либо сети, планирование tooensure, можно настроить сетевое сопоставление, при развертывании hello сценарий, что виртуальные машины Azure будут tooAzure подключенных виртуальных сетей, после отработки отказа, и, что они назначены соответствующие IP-адреса.

Go слишком[шаг 4: Планирование сети](vmm-to-azure-walkthrough-network.md)


## <a name="step-5-prepare-azure-resources"></a>Шаг 5. Подготовка ресурсов Azure

Настройте учетную запись, сети и хранилище Azure. Это можно сделать при развертывании, но мы рекомендуем это сделать до начала процесса.

Go слишком[шаг 5: Подготовка Azure](vmm-to-azure-walkthrough-prepare-azure.md)

## <a name="step-6-prepare-vmm-and-hyper-v"></a>Шаг 6. Подготовка VMM и Hyper-V

Подготовка серверов VMM в локальной среде hello и узлов Hyper-V для развертывания службы восстановления сайтов.

Go слишком[шаг 6: Подготовка локальных серверов](vmm-to-azure-walkthrough-vmm-hyper-v.md)

## <a name="step-7-set-up-a-vault"></a>Шаг 7. Настройка хранилища

Настройте хранилище служб восстановления. хранилище Hello содержит параметры конфигурации и управляет репликации.

[Шаг 7. Настройка хранилища для репликации Hyper-V](vmm-to-azure-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a>Шаг 8. Настройка параметров исходной и целевой среды

Настройка hello исходное и конечное расположение репликации. Добавьте хранилище toohello сервера VMM hello и загружать файлы установки hello для компонентов Site Recovery. Запустите программу установки поставщика Azure Site Recovery на сервере VMM hello. Программа установки устанавливает hello поставщика на сервере VMM hello и регистрирует hello сервер в хранилище hello. Установка агента служб восстановления Microsoft hello на каждом узле Hyper-V.

Go слишком[Step 8: исходный и целевой настройки](vmm-to-azure-walkthrough-source-target.md)

## <a name="step-9-configure-network-mapping"></a>Шаг 9. Настройка сетевого сопоставления

Карта локальной виртуальной Машины VMM сетей tooAzure виртуальных сетей. После отработки отказа виртуальные машины Azure создаются в hello сеть Azure, которая сопоставляет ВМ toohello локальную сеть, в которой hello находится источник Hyper-V.

Go слишком[шаг 9: настройте сетевое сопоставление](vmm-to-azure-walkthrough-network-mapping.md)


## <a name="step-10-set-up-a-replication-policy"></a>Шаг 10. Настройка политики репликации

Укажите, как локальные виртуальные машины будут реплицированных tooAzure.

Go слишком[шаг 10: настроить политику репликации](vmm-to-azure-walkthrough-replication.md)


## <a name="step-11-enable-replication-for-vms"></a>Шаг 11. Включение репликации для виртуальных машин

Выберите виртуальные машины hello требуется tooreplicate. Включение виртуальной Машины для tooAzure начальной репликации hello триггеры репликации, за которым следует текущих разностной репликации.

Go слишком[шаг 11: включение репликации](vmm-to-azure-walkthrough-enable-replication.md)


## <a name="step-12-run-a-test-failover"></a>Шаг 12. Запуск тестовой отработки отказа

Выполните тест отработки отказа toomake, убедиться, что все работает должным образом.

Go слишком[шаг 12: запустите тестовую отработку отказа](vmm-to-azure-walkthrough-test-failover.md)


