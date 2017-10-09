---
title: "aaaMigrate виртуальных машин из AWS tooAzure | Документы Microsoft"
description: "В этой статье описывается, как toomigrate виртуальных машин выполняется в tooAzure Amazon Web Services (AWS), с помощью Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: bsiva
manager: jwhit
editor: 
ms.assetid: ddb412fd-32a8-4afa-9e39-738b11b91118
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: c99b781ec9cca5b8f9a847d3fc48408062b120b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-virtual-machines-in-amazon-web-services-aws-tooazure-with-azure-site-recovery"></a>Перенос виртуальных машин в tooAzure Amazon Web Services (AWS) с Azure Site Recovery

В этой статье описывается, как toomigrate AWS Windows экземпляров tooAzure виртуальных машин с hello [Azure Site Recovery](site-recovery-overview.md) службы.

Миграция фактически происходит переход из AWS tooAzure. Вы не можете tooAWS машины восстановления размещения и нет текущей репликации. В этой статье описываются шаги hello для миграции в hello портал Azure и основаны на hello инструкции по [репликации tooAzure физический компьютер](site-recovery-vmware-to-azure.md).

Отправьте все комментарии или вопросы hello нижней части этой статьи, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)

## <a name="supported-operating-systems"></a>Поддерживаемые операционные системы

Site Recovery может быть под управлением любой из следующих операционных систем hello экземпляров используется toomigrate EC2:

- Windows (только 64-разрядная версия)
    - Windows Server 2008 R2 с пакетом обновления 1 или более поздняя версия (Поддерживаются только драйверы Citrix PV и драйверы AWS PV. **Экземпляры с драйверами RedHat PV не поддерживаются**.) Windows Server 2012, Windows Server 2012 R2.
- Linux (только 64-разрядная версия)
    - Red Hat Enterprise Linux 6.7 (только виртуализированные экземпляры HVM).

## <a name="prerequisites"></a>Предварительные требования

Вот что нужно для этого развертывания:

* **Сервер конфигурации**: развертывании виртуальной Машины EC2 Amazon под управлением Windows Server 2012 R2 в качестве hello конфигурации сервера. По умолчанию hello другие компоненты Azure Site Recovery (сервер обработки и главного целевого сервера) устанавливаются при развертывании сервера конфигурации hello. В этой статье описываются шаги hello для миграции в hello портал Azure и основаны на hello инструкции по [Дополнительные сведения](site-recovery-components.md)

* **Экземпляры EC2**: hello Amazon EC2 экземплярах виртуальных машин, что требуется toomigrate.

## <a name="deployment-steps"></a>Шаги по развертыванию

1. Создайте хранилище служб восстановления,
2. Hello группы безопасности в экземплярах EC2 должны иметь правила, настроенные tooallow взаимодействия экземпляр EC2 hello, нужно toomigrate, а экземпляр hello плана hello toodeploy сервер конфигурации.

3. На hello же Amazon виртуального частного облака как своих экземпляров EC2 развертывание сервера конфигурации ASR. Ссылаться hello VMware или физических tooAzure необходимые условия для требования для развертывания сервера конфигурации.

    ![DeployCS](./media/site-recovery-migrate-aws-to-azure/migration_pic2.png)

4.  Как только сервер конфигурации развертывается в AWS и зарегистрирован в хранилище служб восстановления, вы увидите hello конфигурации сервера и сервера обработки в меню инфраструктуры Site Recovery как показано ниже:

    ![CSinVault](./media/site-recovery-migrate-aws-to-azure/migration_pic3.png)

5. После развертывания сервера конфигурации hello (он может занять too15 minustes для него tooappear), проверки, он может взаимодействовать с виртуальными машинами hello нужных toomigrate.

6. [Настройте параметры репликации](site-recovery-setup-replication-settings-vmware.md).

7. Включение репликации: включить репликацию для виртуальных машин, которые вы хотите toomigrate hello. Вы можете узнать hello EC2 экземпляров с помощью hello частного IP-адреса, можно получить из консоли EC2 hello.

    ![Выбор виртуальной машины](./media/site-recovery-migrate-aws-to-azure/migration_pic4.png)

8. После защищенных экземпляров hello EC2 и tooAzure hello репликации завершена, [выполнить тестовую отработку отказа](site-recovery-test-failover-to-azure.md) toovalidate производительность приложения в Azure.

    ![TFI](./media/site-recovery-migrate-aws-to-azure/migration_pic5.png)

9. Запуск отработки отказа из AWS tooAzure для каждой виртуальной Машины. При необходимости можно создать план восстановления и запускать несколько виртуальных машин отработки отказа, toomigrate из AWS tooAzure. [Узнайте подробнее](site-recovery-create-recovery-plans.md) о планах восстановления.

10. Для миграции не требуется toocommit отработки отказа. Вместо этого выберите параметр выполнения миграции hello для каждого компьютера требуется toomigrate. Hello выполнения миграции действие завершения процесса миграции hello, удаляет репликации для машины hello и прекращает выставления счетов для машины hello Site Recovery.

    ![Миграция](./media/site-recovery-migrate-aws-to-azure/migration_pic6.png)

## <a name="next-steps"></a>Дальнейшие действия

- [Подготовка репликации машин в процессе миграции tooenable](site-recovery-azure-to-azure-after-migration.md) tooanother регионе для аварийного восстановления.
- Включите защиту рабочих нагрузок, [выполнив репликацию виртуальных машин Azure.](site-recovery-azure-to-azure.md)
