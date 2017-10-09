---
title: "aaaReplicate tooAzure виртуальных машин VMware с Azure Site Recovery | Документы Microsoft"
description: "Общие сведения о hello действия для рабочих нагрузок на виртуальных машин VMware tooAzure репликации"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 7104f67a3635b916048dcb61bca770c89f0c77fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-vms-tooazure-with-site-recovery"></a>Репликация виртуальных машин VMware tooAzure с Site Recovery

В этой статье содержится обзор hello действия требуется tooreplicate локальной VMware виртуальные машины tooAzure, с помощью hello [Azure Site Recovery](site-recovery-overview.md) в hello портал Azure.


![Процесс развертывания](./media/vmware-walkthrough-overview/vmware-to-azure-process.png)

**Рис. 1. Общие сведения о процессе развертывания**

## <a name="step-1-review-architecture-and-prerequisites"></a>Шаг 1. Проверка архитектуры и предварительных требований

Чтобы начать развертывание, просмотрите hello архитектура сценария и убедитесь, что вы понимаете все компоненты hello требуется toodeploy

Go слишком[шаг 1: обзор архитектуры hello](vmware-walkthrough-architecture.md)


## <a name="step-2-review-prerequisites"></a>Шаг 2. Проверка предварительных требований

Убедитесь, что установлены необходимые компоненты hello на месте для каждого компонента развертывания:

- **Предварительные требования Azure**: учетная запись Microsoft Azure, сети Azure и учетные записи хранения.
- **Локальные компоненты Site Recovery**: компьютер, на котором запущены локальные компоненты Site Recovery.
- **В локальной среде VMware предварительные требования**: требуется tooset учетных записей, чтобы Site Recovery можно обращаться к серверов VMware и виртуальные машины.
- **Репликация виртуальных машин**: виртуальные машины должны toocomply необходимость tooreplicate требованиям Azure и установлен компонент службы мобильности hello.

Go слишком[шаг 2: Проверьте предварительные условия и ограничения](vmware-walkthrough-prerequisites.md)

## <a name="step-3-plan-capacity"></a>Шаг 3. Планирование ресурсов

При выполнении полного развертывания необходимо toofigure какие ресурсы репликации необходимо. Существует несколько из доступных toohelp средства это сделать. Go tooStep 2. Этот шаг можно пропустить, если вы выполняете быстро настроить среду tootest hello.

Go слишком[Step 3: Планирование емкости](vmware-walkthrough-capacity.md)

## <a name="step-4-plan-networking"></a>Шаг 4. Планирование сетей

Необходимо toodo какой-либо сети, планирование tooensure виртуальных машинах Azure, подключенной toonetworks после отработки отказа, и что у hello правой IP-адресов.

Go слишком[шаг 4: Планирование сети](vmware-walkthrough-network.md)

##  <a name="step-5-prepare-azure-resources"></a>Шаг 5. Подготовка ресурсов Azure

Прежде чем начать, настройте сети и хранилище Azure. Это можно сделать при развертывании, но мы рекомендуем это сделать до начала процесса.

Go слишком[шаг 5: Подготовка Azure](vmware-walkthrough-prepare-azure.md)


## <a name="step-6-prepare-vmware"></a>Шаг 6. Подготовка VMware

Необходимые tooset учетные записи, используемые для восстановления сайта.

- Tooautomatically серверов виртуализации VMware доступа обнаружения виртуальных машин.
- Доступ к службе Mobility hello tooinstall виртуальных машин. Каждая виртуальная машина, требуется tooreplicate должен быть установлен прежде чем агент службы Mobility hello можно включить для него репликацию.

Go слишком[шаг 6: Подготовка VMware](vmware-walkthrough-prepare-vmware.md)

## <a name="step-7-set-up-a-vault"></a>Шаг 7. Настройка хранилища

Требуется tooset копирование tooorchestrate хранилище служб восстановления и управление репликацией. При настройке хранилища hello, укажите, что должно tooreplicate, и когда необходимо tooreplicate его.

Go слишком[шаг 7: Настройка хранилища](vmware-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a>Шаг 8. Настройка параметров исходной и целевой среды

Настройка hello исходной и целевой объект, который используется для репликации. Настройка параметров источника включает запущен tooinstall единой установки компонентов Site Recovery hello в локальной среде.

Go слишком[Step 8: Настройка hello исходной и целевой](vmware-walkthrough-source-target.md)

## <a name="step-9-set-up-a-replication-policy"></a>Шаг 9. Настройка политики репликации

Вы настроили параметры политики toospecify репликации для виртуальных машин VMware в хранилище hello.

Go слишком[шаг 9: настроить политику репликации](vmware-walkthrough-replication.md)

## <a name="step-10-install-hello-mobility-service"></a>Шаг 10: Установка службы Mobility hello

должен быть установлен Hello службы Mobility service на каждой виртуальной Машины будет tooreplicate. Существует несколько способов tooset hello службы с установкой Принудительная или по запросу.

Go слишком[шаг 10: Установка службы Mobility hello](vmware-walkthrough-install-mobility.md)

## <a name="step-11-enable-replication"></a>Шаг 11. Включение репликации

После запуска hello службы Mobility service на виртуальной Машине можно включить для него репликацию. После включения, происходит начальной репликации hello виртуальной Машины.

Go слишком[шаг 11: включение репликации](vmware-walkthrough-enable-replication.md)

## <a name="step-12-run-a-test-failover"></a>Шаг 12. Запуск тестовой отработки отказа

После завершения первоначальной репликации, а разностная репликация выполняется, можно запустить тест отработки отказа toomake, убедиться, что все работает правильно.

Go слишком[шаг 12: запустите тестовую отработку отказа](vmware-walkthrough-test-failover.md)
