---
title: "aaaReplicate tooAzure виртуальных машин Hyper-V с помощью Azure Site Recovery | Документы Microsoft"
description: "Описывает способ tooorchestrate репликации, отработки отказа и восстановления локальных Hyper-V виртуальных машин tooAzure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: efddd986-bc13-4a1d-932d-5484cdc7ad8d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: ab9cd14149ef32a416428d0f4327aa18b042e9c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-without-vmm-tooazure"></a>TooAzure виртуальных машин (без VMM) реплицировать Hyper-V 

> [!div class="op_single_selector"]
> * [Портал Azure](site-recovery-hyper-v-site-to-azure.md)
> * [Классическая модель Azure](site-recovery-hyper-v-site-to-azure-classic.md)
> * [PowerShell — Resource Manager](site-recovery-deploy-with-powershell-resource-manager.md)
>
>

В этой статье содержится обзор hello шаги, необходимые tooreplicate в локальной среде Hyper-V виртуальных машин tooAzure, с помощью hello [Azure Site Recovery](site-recovery-overview.md) в hello портал Azure. В этом развертывании Hyper-V виртуальные машины не передаются под управление System Center Virtual Machine Manager (VMM).


После считывания в этой статье, отправлять любые комментарии внизу hello или задавайте технические вопросы на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="step-1-review-architecture-and-prerequisites"></a>Шаг 1. Проверка архитектуры и предварительных требований

Чтобы начать развертывание, просмотрите hello архитектура сценария и убедитесь, что вы понимаете все компоненты hello требуется toodeploy

Go слишком[шаг 1: обзор архитектуры hello](hyper-v-site-walkthrough-architecture.md)


## <a name="step-2-review-prerequisites"></a>Шаг 2. Проверка предварительных требований

Убедитесь, что установлены необходимые компоненты hello на месте для каждого компонента развертывания:

- **Предварительные требования Azure**: учетная запись Microsoft Azure, сети Azure и учетные записи хранения.
- **Предварительные требования локальной среды Hyper-V**: убедитесь, что узлы Hyper-V подготовлены к развертыванию Site Recovery.
- **Репликация виртуальных машин**: виртуальные машины, нужно tooreplicate требуется toocomply требованиям Azure.

Go слишком[шаг 2: Проверьте предварительные условия и ограничения](hyper-v-site-walkthrough-prerequisites.md)

## <a name="step-3-plan-capacity"></a>Шаг 3. Планирование ресурсов

При выполнении полного развертывания необходимо toofigure какие ресурсы репликации необходимо. Существует несколько из доступных toohelp средства это сделать. Go tooStep 2. Этот шаг можно пропустить, если вы выполняете быстро настроить среду tootest hello.

Go слишком[Step 3: Планирование емкости](hyper-v-site-walkthrough-capacity.md)

## <a name="step-4-plan-networking"></a>Шаг 4. Планирование сетей

Необходимо toodo какой-либо сети, планирование tooensure виртуальных машинах Azure, подключенной toonetworks после отработки отказа, и что у hello правой IP-адресов.

Go слишком[шаг 4: Планирование сети](hyper-v-site-walkthrough-network.md)

##  <a name="step-5-prepare-azure-resources"></a>Шаг 5. Подготовка ресурсов Azure

Прежде чем начать, настройте сети и хранилище Azure. Это можно сделать при развертывании, но мы рекомендуем это сделать до начала процесса.

Go слишком[шаг 5: Подготовка Azure](hyper-v-site-walkthrough-prepare-azure.md)


## <a name="step-6-prepare-hyper-v"></a>Шаг 6. Подготовка Hyper-V

Убедитесь, что серверы Hyper-V соответствуют требованиям к развертыванию Site Recovery.

Go слишком[шаг 6: Подготовка Hyper-V](hyper-v-site-walkthrough-prepare-hyper-v.md)

## <a name="step-7-set-up-a-vault"></a>Шаг 7. Настройка хранилища

Требуется tooset копирование tooorchestrate хранилище служб восстановления и управление репликацией. При настройке хранилища hello, укажите, что должно tooreplicate, и когда необходимо tooreplicate его.

Go слишком[шаг 7: Создание хранилища](hyper-v-site-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a>Шаг 8. Настройка параметров исходной и целевой среды

Настройка hello исходной и целевой объект, который используется для репликации. Настройка параметров источника включает в себя добавление Hyper-V hosts tooa сайт Hyper-V, установка hello поставщика Site Recovery и агента служб восстановления на каждом узле Hyper-V и регистрации узла hello в hello в хранилище служб восстановления.

Go слишком[Step 8: Настройка hello исходной и целевой](hyper-v-site-walkthrough-source-target.md)

## <a name="step-9-set-up-a-replication-policy"></a>Шаг 9. Настройка политики репликации

Вы настроили параметры политики toospecify репликации для виртуальных машин Hyper-V в хранилище hello.

Go слишком[шаг 9: настроить политику репликации](hyper-v-site-walkthrough-replication.md)


## <a name="step-10-enable-replication"></a>Шаг 10. Включение репликации

После того как вы политику репликации на месте, после включения, происходит начальной репликации hello виртуальной Машины.

Go слишком[шаг 10: включение репликации](hyper-v-site-walkthrough-enable-replication.md)

## <a name="step-11-run-a-test-failover"></a>Шаг 11. Запуск тестовой отработки отказа

После завершения первоначальной репликации, а разностная репликация выполняется, можно запустить тест отработки отказа toomake, убедиться, что все работает правильно.

Go слишком[шаг 11: запустите тестовую отработку отказа](hyper-v-site-walkthrough-test-failover.md)
