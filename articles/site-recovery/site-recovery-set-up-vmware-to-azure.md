---
title: "Настройка среды источника hello (VMware tooAzure) | Документы Microsoft"
description: "В этой статье описывается, как tooset копирование вашей локальной среды toostart, репликация VMware виртуальной машины tooAzure."
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
ms.openlocfilehash: cbeeffc1061b11223e12ff3e237fa7e55b999aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-source-environment-vmware-tooazure"></a>Настройка среды источника hello (VMware tooAzure)
> [!div class="op_single_selector"]
> * [VMware tooAzure](./site-recovery-set-up-vmware-to-azure.md)
> * [Физический tooAzure](./site-recovery-set-up-physical-to-azure.md)

В этой статье описывается, как tooset копирование toostart вашей локальной среды, репликация виртуальных машин выполняется на VMware tooAzure.

## <a name="prerequisites"></a>Предварительные требования

Hello предполагается, что вы уже создали:
- Хранилище служб восстановления в hello [портал Azure](http://portal.azure.com "портал Azure").
- Специальная учетная запись на сервере VMware vCenter, которую можно использовать для [автоматического обнаружения](./site-recovery-vmware-to-azure.md).
- Виртуальная машина сервера, на котором tooinstall hello конфигурации.

## <a name="configuration-server-minimum-requirements"></a>Минимальные требования к серверу конфигурации
программное обеспечение сервера Hello конфигурации должен быть развернут на высокодоступной виртуальной машины VMware. Привет, в следующей таблице перечислены hello минимумом оборудования, программного обеспечения и требования к сети для сервера конфигурации.
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> На основе HTTPS прокси-серверы не поддерживаются сервером конфигурации hello.

## <a name="choose-your-protection-goals"></a>Выбор целевых объектов для защиты

1. В hello портал Azure, перейдите toohello **службы восстановления** хранилище колонки и выберите вашего хранилища.
2. Меню hello ресурсов хранилища hello go слишком**Приступая к работе** > **Site Recovery** > **шаг 1: Подготовка инфраструктуры**  >  **Цель защиты**.

    ![Выбор цели](./media/site-recovery-set-up-vmware-to-azure/choose-goals.png)
3. В **цель защиты**выберите **tooAzure**и выберите **Да, с VMware vSphere низкоуровневой оболочки**. Нажмите кнопку **ОК**.

    ![Выбор цели](./media/site-recovery-set-up-vmware-to-azure/choose-goals2.png)

## <a name="set-up-hello-source-environment"></a>Настройка среды источника hello
Настройка среды hello источника включает в себя два основных действия:

- Установка и регистрация сервера конфигурации в службе Site Recovery.
- Обнаружение локальных виртуальных машин, подключившись Site Recovery tooyour локальной VMware vCenter или vSphere EXSi узлов.

### <a name="step-1-install-and-register-a-configuration-server"></a>Этап 1. Установка и регистрация сервера конфигурации

1. Щелкните **Шаг 1. Подготовка инфраструктуры** > **Источник**. В **Подготовка источника**, если у вас нет сервера конфигурации, щелкните **+ сервер конфигурации** tooadd один.

    ![Настройка источника](./media/site-recovery-set-up-vmware-to-azure/set-source1.png)
2. На hello **добавить сервер** колонки, убедитесь, что **сервер конфигурации** отображается в **тип сервера**.
4. Загрузите файл установки hello установка единой Site Recovery.
5. Загрузите ключ регистрации в хранилище hello. При запуске программы установки единой необходим ключ регистрации hello. Hello ключ действителен в течение пяти дней после его создания.

    ![Настройка источника](./media/site-recovery-set-up-vmware-to-azure/set-source2.png)
6. На компьютере hello используется в качестве сервера конфигурации hello выполните **Установка Azure Site Recovery единой** tooinstall hello конфигурации сервера, сервера обработки hello и образец hello целевого сервера.

#### <a name="run-azure-site-recovery-unified-setup"></a>Выполнение единой установки Azure Site Recovery

> [!TIP]
> Регистрация сервера конфигурации не выполняется, если время hello на системные часы компьютера отличается от местного времени более пяти минут. Синхронизацию системных часов с [сервер времени](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) перед началом установки hello.

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> Сервер конфигурации Hello могут устанавливаться через командную строку. Дополнительные сведения см. в разделе [Установка hello конфигурации сервера с помощью средства командной строки](http://aka.ms/installconfigsrv).

#### <a name="add-hello-vmware-account-for-automatic-discovery"></a>Добавьте учетную запись VMware hello автоматического обнаружения

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="step-2-add-a-vcenter"></a>Этап 2. Добавление сервера vCenter
tooallow Azure Site Recovery toodiscover виртуальных машин, работающих в локальной среде, необходимо tooconnect VMware vCenter Server или узлы vSphere ESXi с Site Recovery.

Выберите **+ vCenter** toostart подключение сервера VMware vCenter server или узла ESXi VMware vSphere.

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]


## <a name="common-issues"></a>Распространенные проблемы
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a>Дальнейшие действия
[Настройка целевой среды](./site-recovery-prepare-target-vmware-to-azure.md) в Azure.
