---
title: "tooAzure aaaMigrate с Site Recovery | Документы Microsoft"
description: "Это статье представлен обзор миграции виртуальных машин и физических серверов tooAzure с Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/05/2017
ms.author: raynew
ms.openlocfilehash: 6e65deee337c5371d441812ddb820dc8bc233684
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-tooazure-with-site-recovery"></a>Перенос tooAzure с Site Recovery

Эта статья Общие сведения об использовании служб Azure Site Recovery hello для миграции виртуальных машин и физических серверов.

Site Recovery — это служба Azure, вклада tooyour BCDR стратегии, управляя операциями репликации локальных физических серверов и облако виртуальных машин toohello (Azure) или tooa дополнительный центр обработки данных. При возникновении сбоев в расположении первичной, переключением toohello вторичное расположение tookeep приложений и рабочих нагрузок доступны. При возвращается операций toonormal сбой задней tooyour первичного расположения. Дополнительные сведения см. в статье [Что такое Site Recovery?](site-recovery-overview.md) Также можно использовать Site Recovery toomigrate существующие локальные вашей облачной пути и свободно hello возможностям Azure предлагает tooexpedite tooAzure рабочих нагрузок.

Краткий обзор того, как tooperform миграции, см. видео toothis.
>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/ASRHowTo-Video2-Migrate-Virtual-Machines-to-Azure/player]

В этой статье описывается развертывание в hello [портал Azure](https://portal.azure.com). Hello [классический портал Azure](https://manage.windowsazure.com/) может быть toomaintain используется существующая хранилищ Site Recovery, но нельзя создать новые хранилища.

Отправлять все комментарии hello нижней части этой статьи. Задавайте технические вопросы на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="what-do-we-mean-by-migration"></a>Что подразумевает собой перенос?

Вы можете развернуть Site Recovery для репликации локальных виртуальных машин и физических серверов, tooAzure или tooa вторичного сайта. Реплицировать машины, при сбое их hello основного сайта при происходят сбои в работе и ошибкой задней toohello первичного сайта, когда он восстанавливает. Toothis сложение, чтобы пользователи могли обращаться к ним как виртуальные машины Azure можно использовать виртуальные машины toomigrate Site Recovery и tooAzure физических серверов. Миграция влечет за собой репликации и отработки отказа с основного сайта tooAzure hello и жестов выполнения миграции.

## <a name="what-can-site-recovery-migrate"></a>Что можно перенести с помощью службы Site Recovery?

Вы можете:

- Перенос рабочих нагрузок на локальных виртуальных машин Hyper-V, виртуальных машин VMware и физических серверов, toorun на виртуальных машинах Azure. Этот сценарий также поддерживает полную репликацию и восстановление размещения.
- Перенос [виртуальных машин IaaS](site-recovery-migrate-azure-to-azure.md) Azure между регионами Azure. Сейчас в этом сценарии поддерживается только перенос, а это означает, что восстановление размещения не поддерживается.
- Перенос [экземпляров AWS Windows](site-recovery-migrate-aws-to-azure.md) tooAzure ВМ IaaS. Сейчас в этом сценарии поддерживается только перенос, а это означает, что восстановление размещения не поддерживается.

## <a name="migrate-on-premises-vms-and-physical-servers"></a>Перенос локальных виртуальных машин и физических серверов

toomigrate локальных виртуальных машин Hyper-V, виртуальных машин VMware и физических серверов, выполните практически hello же шаги, которые используются для обычной репликации.

1. Настройка хранилища служб восстановления
2. Настройка серверов управления требуется hello (VMware, VMM, Hyper-V — в зависимости от того, какие действия следует toomigrate), добавьте их в хранилище toohello и указать параметры репликации.
3. Включение репликации для hello машины, которые требуется toomigrate
4. После первоначальной миграции hello запустите tooensure быстрой проверки отработки отказа, что все работает правильно.
5. После проверки работоспособности среды репликации запустите плановую или внеплановую отработку отказа ([поддерживаемую](site-recovery-failover.md) для вашего сценария). Мы рекомендуем использовать плановую отработку отказа, когда это возможно.
6. Для миграции не требуется toocommit отработки отказа или удалить. Вместо этого выберите hello **выполнения миграции** параметр для каждого компьютера требуется toomigrate.
     - В **реплицируются элементы**, щелкните правой кнопкой мыши hello виртуальной Машины и нажмите кнопку **выполнения миграции**. Нажмите кнопку **ОК** toocomplete. Для отслеживания хода в свойствах виртуальной Машины hello в в следящего задания выполнения миграции hello в **задания Site Recovery**.
     - Hello **выполнения миграции** действие завершения процесса миграции hello, удаляет репликацию для машины hello и приостанавливает выставление счетов Site Recovery для машины hello.

![completemigration](./media/site-recovery-hyper-v-site-to-azure/migrate.png)

## <a name="migrate-between-azure-regions"></a>Перенос между регионами Azure

Служба Site Recovery позволяет переносить виртуальные машины Azure между регионами. В этом сценарии поддерживается только перенос. Другими словами можно реплицировать виртуальные машины Azure hello и сбое tooanother области, но не могут переключаться обратно. В этом сценарии, которые вы настроили хранилище служб восстановления развертывания в локальной конфигурации сервера toomanage репликации, добавьте его toohello хранилище и укажите параметры репликации. Включить репликацию для машин hello требуется toomigrate и быстро запустить тест отработки отказа. Затем запустите незапланированной отработки отказа с hello **выполнения миграции** параметр.

## <a name="migrate-aws-tooazure"></a>Перенос AWS tooAzure

Можно перенести tooAzure AWS экземпляров виртуальных машин. В этом сценарии поддерживается только перенос. Другими словами можно реплицировать экземпляров AWS hello и переключение tooAzure, но не могут переключаться обратно. Экземпляры AWS, обрабатываются в hello таким же образом, как физические серверы для целей миграции. Настроить хранилище служб восстановления, развертывание в локальной конфигурации сервера toomanage репликации, добавьте его toohello хранилище и укажите параметры репликации. Включить репликацию для машин hello требуется toomigrate и быстро запустить тест отработки отказа. Затем запустите незапланированной отработки отказа с hello **выполнения миграции** параметр.




## <a name="next-steps"></a>Дальнейшие действия

- [Перенос виртуальных машин VMware tooAzure](site-recovery-vmware-to-azure.md)
- [Перенос виртуальных машин Hyper-V в tooAzure облаков VMM](site-recovery-vmm-to-azure.md)
- [Перенос виртуальных машин Hyper-V без VMM tooAzure](site-recovery-hyper-v-site-to-azure.md)
- [Перенос виртуальных машин IaaS Azure между регионами Azure с помощью Azure Site Recovery](site-recovery-migrate-azure-to-azure.md)
- [Перенос экземпляров tooAzure AWS](site-recovery-migrate-aws-to-azure.md)
- [Подготовка репликации машин в процессе миграции tooenable](site-recovery-azure-to-azure-after-migration.md) tooanother регионе для аварийного восстановления.
- Включите защиту рабочих нагрузок, [выполнив репликацию виртуальных машин Azure.](site-recovery-azure-to-azure.md)
