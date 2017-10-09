---
title: "aaaReplicate физической локальной tooAzure серверов с Azure Site Recovery | Документы Microsoft"
description: "Общие шаги hello репликации рабочих нагрузок на локальных tooAzure физических серверов Windows и Linux с hello службы Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 20122f01-929a-4675-b85b-a9b99d2618bc
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: f801b9544072d4029ec06cc1abfd4ff370e852e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-physical-servers-tooazure-with-site-recovery"></a>Репликация физических серверов tooAzure с Site Recovery

В этой статье содержится обзор hello действия требуется tooreplicate в локальной среде Windows и Linux физических серверов tooAzure, с помощью hello [Azure Site Recovery](site-recovery-overview.md) в hello портал Azure.


## <a name="step-1-review-architecture-and-prerequisites"></a>Шаг 1. Проверка архитектуры и предварительных требований

Прежде чем начать развертывание, просмотрите hello архитектура сценария и убедитесь, что вы понимаете все компоненты hello необходим tooset hello развертывания.

Go слишком[шаг 1: обзор архитектуры hello](physical-walkthrough-architecture.md)


## <a name="step-2-review-prerequisites"></a>Шаг 2. Проверка предварительных требований

Убедитесь, что установлены необходимые компоненты hello на месте для каждого компонента развертывания:

- **Предварительные требования Azure**: учетная запись Microsoft Azure, сети Azure и учетные записи хранения.
- **Локальные компоненты Site Recovery**: компьютер, на котором запущены локальные компоненты Site Recovery.
- **Реплицировать машины**: серверы, требуется tooreplicate должны toocomply с локальной и требования к Azure.

Go слишком[шаг 2: Проверьте предварительные условия и ограничения](physical-walkthrough-prerequisites.md)

## <a name="step-3-plan-capacity"></a>Шаг 3. Планирование ресурсов

При выполнении полного развертывания необходимо toofigure какие ресурсы репликации необходимо. Если вы выполняете быстро настроить среду tootest hello, этот шаг можно пропустить.

Go слишком[Step 3: Планирование емкости](physical-walkthrough-capacity.md)

## <a name="step-4-plan-networking"></a>Шаг 4. Планирование сетей

Необходимо toodo какой-либо сети, планирование tooensure виртуальных машинах Azure, подключенной toonetworks после отработки отказа, и что у hello правой IP-адресов.

Go слишком[шаг 4: Планирование сети](physical-walkthrough-network.md)

##  <a name="step-5-prepare-azure-resources"></a>Шаг 5. Подготовка ресурсов Azure

Прежде чем начать, настройте сети и хранилище Azure. 

Go слишком[шаг 5: Подготовка Azure](physical-walkthrough-prepare-azure.md)


## <a name="step-6-set-up-a-vault"></a>Шаг 6. Настройка хранилища

Настройка tooorchestrate хранилище служб восстановления и управление репликацией. При настройке хранилища hello, укажите, что должно tooreplicate, и когда необходимо tooreplicate его.

Go слишком[шаг 6: Настройка хранилища](physical-walkthrough-create-vault.md)

## <a name="step-7-configure-source-and-target-settings"></a>Шаг 7. Настройка параметров исходной и целевой среды

Настройте параметры для hello исходный и конечный сайт (Azure). Параметры источника включает в себя под управлением tooinstall единой установки hello локальных компонентов Site Recovery.

Go слишком[шаг 7: Настройка hello исходной и целевой](physical-walkthrough-source-target.md)

## <a name="step-8-set-up-a-replication-policy"></a>Шаг 8. Настройка политики репликации

Настройки toospecify политики физических серверов должны быть реплицированы.

Go слишком[Step 8: настроить политику репликации](physical-walkthrough-replication.md)

## <a name="step-9-install-hello-mobility-service"></a>Шаг 9: Установка службы Mobility hello

Hello службы Mobility service необходимо установить на каждом сервере требуется tooreplicate. Существует несколько способов tooset hello службы, с установкой Принудительная или по запросу.

Go слишком[шаг 9: Установка службы Mobility hello](physical-walkthrough-install-mobility.md)

## <a name="step-10-enable-replication"></a>Шаг 10. Включение репликации

После запуска hello службы Mobility service на сервере, можно включить для него репликацию. После включения, происходит начальной репликации hello виртуальной Машины.

Go слишком[шаг 10: включение репликации](physical-walkthrough-enable-replication.md)

## <a name="step-11-run-a-test-failover"></a>Шаг 11. Запуск тестовой отработки отказа

После завершения начальной репликации и разностная репликация выполняется, можно запустить тест отработки отказа toomake, убедиться, что все работает правильно.

Go слишком[шаг 11: запустите тестовую отработку отказа](physical-walkthrough-test-failover.md)

