---
title: "Настройка среды источника hello (tooAzure физических серверов) | Документы Microsoft"
description: "В этой статье описывается как tooset копирование toostart вашей локальной среде, репликация физических серверов под управлением Windows или Linux в Azure."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: d4702265bf36910015685d2bba99d6e577531bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-source-environment-physical-server-tooazure"></a>Настройка среды источника hello (физический сервер tooAzure)
> [!div class="op_single_selector"]
> * [VMware tooAzure](./site-recovery-set-up-vmware-to-azure.md)
> * [Физический tooAzure](./site-recovery-set-up-physical-to-azure.md)

В этой статье описывается как tooset копирование toostart вашей локальной среде, репликация физических серверов под управлением Windows или Linux в Azure.

## <a name="prerequisites"></a>Предварительные требования

Hello статьи предполагается, что уже:
1. Хранилище служб восстановления в hello [портал Azure](http://portal.azure.com "портал Azure").
3. Физический компьютер сервера, на котором tooinstall hello конфигурации.

### <a name="configuration-server-minimum-requirements"></a>Минимальные требования к серверу конфигурации
Привет, в следующей таблице перечислены hello минимумом оборудования, программного обеспечения и требования к сети для сервера конфигурации.
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> На основе HTTPS прокси-серверы не поддерживаются сервером конфигурации hello.

## <a name="choose-your-protection-goals"></a>Выбор целевых объектов для защиты

1. В hello портал Azure, перейдите toohello **службы восстановления** хранилищ колонки и выберите вашего хранилища.
2. В hello **ресурсов** хранилища hello, выберите пункт **Приступая к работе** > **Site Recovery** > **шаг 1: Подготовка Инфраструктура** > **цель защиты**.

    ![Выбор цели](./media/site-recovery-set-up-physical-to-azure/choose-goals.png)
3. В **цель защиты**выберите **tooAzure** и **не виртуализированных, другие**, а затем нажмите кнопку **ОК**.

    ![Выбор цели](./media/site-recovery-set-up-physical-to-azure/physical-protection-goal.PNG)

## <a name="set-up-hello-source-environment"></a>Настройка среды источника hello

1. В **Подготовка источника**, если у вас нет сервера конфигурации, щелкните **+ сервер конфигурации** tooadd один.

  ![Настройка источника](./media/site-recovery-set-up-physical-to-azure/plus-config-srv.png)
2. В hello **добавить сервер** колонки, убедитесь, что **сервер конфигурации** отображается в **тип сервера**.
4. Загрузите файл установки hello установка единой Site Recovery.
5. Загрузите ключ регистрации в хранилище hello. При запуске программы установки единой необходим ключ регистрации hello. Hello ключ действителен в течение пяти дней после его создания.

    ![Настройка источника](./media/site-recovery-set-up-physical-to-azure/set-source2.png)
6. На компьютере hello используется в качестве сервера конфигурации hello выполните **Установка Azure Site Recovery единой** tooinstall hello конфигурации сервера, сервера обработки hello и образец hello целевого сервера.

#### <a name="run-azure-site-recovery-unified-setup"></a>Выполнение единой установки Azure Site Recovery

> [!TIP]
> Регистрация сервера конфигурации не выполняется, если время hello на системные часы компьютера — более пяти минут от местного времени. Синхронизацию системных часов с [сервер времени](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) перед началом установки hello.

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> Сервер конфигурации Hello могут устанавливаться через командную строку. Изучите дополнительные сведения об [установке сервера конфигурации с помощью программ командной строки](http://aka.ms/installconfigsrv).


## <a name="common-issues"></a>Распространенные проблемы

[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a>Дальнейшие действия

Следующий этап заключается в [настройке целевой среды](./site-recovery-prepare-target-physical-to-azure.md) в Azure.
