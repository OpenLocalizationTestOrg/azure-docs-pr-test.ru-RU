---
title: "tooset машины aaaPrepare настройки аварийного восстановления между регионами Azure после миграции tooAzure с помощью Site Recovery | Документы Microsoft"
description: "В этой статье описывается, как tooprepare машины tooset настройки аварийного восстановления между регионами Azure после миграции tooAzure с помощью Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: ponatara
manager: abhemraj
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: ponatara
ms.openlocfilehash: b6274e3df210c1d8a7b8289cc85868ee6414e523
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-tooanother-region-after-migration-tooazure-by-using-azure-site-recovery"></a>Реплицировать виртуальные машины Azure tooanother области после миграции tooAzure с помощью Azure Site Recovery

>[!NOTE]
> Репликация Azure Site Recovery для виртуальных машин Azure сейчас доступна в предварительной версии.

## <a name="overview"></a>Обзор

Эта статья поможет вам подготовить виртуальные машины Azure для репликации между двумя регионах Azure, после завершения переноса из локальной среды tooAzure этих компьютеров с помощью Azure Site Recovery.

## <a name="disaster-recovery-and-compliance"></a>Аварийное восстановление и соответствие
В настоящее время больше и больше предприятий перемещение их tooAzure рабочих нагрузок. С предприятий перемещение критически важных в локальной рабочей tooAzure рабочих нагрузок, Настройка аварийного восстановления для этих рабочих нагрузок является обязательным для обеспечения соответствия и toosafeguard от перерывов в регионе Azure.

## <a name="steps-for-preparing-migrated-machines-for-replication"></a>Шаги по подготовке перенесенных виртуальных машин для репликации
tooprepare перенести машины для настройки репликации tooanother регион Azure.

1. Завершите миграцию.
2. Установите агент Azure, при необходимости hello.
3. Удалите службу Mobility hello.  
4. Перезапустите hello виртуальной Машины.

Эти действия описаны более подробно в следующих разделах hello.

### <a name="step-1-migrate-workloads-running-on-hyper-v-vms-vmware-vms-and-physical-servers-toorun-on-azure-vms"></a>Шаг 1: Перенос рабочих нагрузок на виртуальных машин Hyper-V, виртуальных машин VMware и физических серверов toorun на виртуальных машинах Azure

tooset Настройка репликации и перенести вашей локальной Hyper-V, VMware и физических рабочих нагрузок tooAzure, приведенным ниже инструкциям hello в hello [Azure IaaS перенос виртуальных машин между регионами Azure с помощью Azure Site Recovery](site-recovery-migrate-to-azure.md) статьи. 

После миграции не требуется toocommit или удалить отработки отказа. Вместо этого выберите hello **выполнения миграции** параметр для каждого компьютера требуется toomigrate:
1. В **реплицируются элементы**, щелкните правой кнопкой мыши hello виртуальной Машины и нажмите кнопку **выполнения миграции**. Нажмите кнопку **ОК** toocomplete hello шаг. Вы можете отслеживать ход выполнения в свойствах виртуальной Машины hello по следящего задания выполнения миграции hello в **задания Site Recovery**.
2. Hello **выполнения миграции** действие завершения процесса миграции hello, удаляет репликацию для машины hello и приостанавливает выставление счетов Site Recovery для машины hello.

   ![completemigration](./media/site-recovery-hyper-v-site-to-azure/migrate.png)

### <a name="step-2-install-hello-azure-vm-agent-on-hello-virtual-machine"></a>Шаг 2: Установите агент ВМ Azure hello на виртуальной машине hello
Hello Azure [агент виртуальной Машины](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux) должны устанавливаться на виртуальной машине hello за toowork расширения hello Site Recovery и toohelp hello виртуальной Машины.

>[!IMPORTANT]
>Начиная с версии 9.7.0.0, на виртуальных машинах Windows hello установщика службы Mobility service также устанавливает hello последние доступные агент ВМ Azure. Для миграции hello виртуальной машины соответствует необходимым компонентом для любого расширения виртуальной Машины, включая расширение hello Site Recovery с помощью установки агента. Hello агента ВМ Azure потребностей toobe, установленные вручную только в том случае, если служба мобильности на hello hello перенесли машины — 9,6 или более ранней версии.

Hello Следующая таблица предоставляет дополнительные сведения об установке агента ВМ hello и проверка того, что он был установлен:

| **Операция** | **Windows** | **Linux** |
| --- | --- | --- |
| Установка агента ВМ hello |Загрузите и установите hello [MSI агента](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Требуется установка hello toocomplete права администратора. |Установить последние hello [агент Linux](../virtual-machines/linux/agent-user-guide.md). Требуется установка hello toocomplete права администратора. Мы рекомендуем установить агент hello из репозитория распространения. Мы *не рекомендует* hello агент виртуальной Машины Linux при установке непосредственно из GitHub.  |
| Проверка установки агента виртуальной Машины hello |1. Обзор папки C:\WindowsAzure\Packages toohello в hello виртуальной Машине Azure. Вы должны увидеть файл WaAppAgent.exe hello. <br>2. Правой кнопкой мыши файл hello, перейдите в слишком**свойства**и затем выберите hello **сведения** hello вкладку **версия продукта** поле должно быть 2.6.1198.718 или более поздней версии. |Недоступно |


### <a name="step-3-remove-hello-mobility-service-from-hello-migrated-virtual-machine"></a>Шаг 3: Удаление hello службы Mobility service из hello перенесенные виртуальные машины

При переносе вашей локальной машины VMware или физических серверов в Windows и Linux необходимо toomanually/uninstall удаление hello службы Mobility service из hello перенесенной виртуальной машины.

>[!IMPORTANT]
>Этот шаг не является обязательным для tooAzure перенесенных виртуальных машин Hyper-V.

#### <a name="uninstall-hello-mobility-service-on-a-windows-server-vm"></a>Удалите hello Mobility service на виртуальной Машине Windows Server
Используйте одну из hello следующие методы toouninstall hello Mobility service на компьютере Windows Server.

##### <a name="uninstall-by-using-hello-windows-ui"></a>Удаление с помощью пользовательского интерфейса Windows hello
1. В hello панели управления выберите **программы**.
2. Выберите **Microsoft Azure Site Recovery Mobility Service / главный целевой сервер** и нажмите кнопку **Удалить**.

##### <a name="uninstall-at-a-command-prompt"></a>Удаление из командной строки
1. Откройте окно командной строки с правами администратора.
2. toouninstall hello службы Mobility service, запустите hello следующую команду:

   ```
   MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
   ```

#### <a name="uninstall-hello-mobility-service-on-a-linux-computer"></a>Удалите hello Mobility service на компьютере Linux
1. На сервере Linux войдите как **привилегированный** пользователь.
2. В конечном перейдите слишком/пользователя/локальной/ASR.
3. toouninstall hello службы Mobility service, запустите hello следующую команду:

   ```
   uninstall.sh -Y
   ```

### <a name="step-4-restart-hello-vm"></a>Шаг 4: Перезапустите hello виртуальной Машины

После установки службы Mobility hello перезапуска hello виртуальной Машины, прежде чем настроить tooanother репликации регион Azure.


## <a name="next-steps"></a>Дальнейшие действия
- Включите защиту рабочих нагрузок, [выполнив репликацию виртуальных машин Azure](site-recovery-azure-to-azure.md).
- Ознакомьтесь со статьей [Руководство по организации сети для репликации виртуальных машин Azure](site-recovery-azure-to-azure-networking-guidance.md).
