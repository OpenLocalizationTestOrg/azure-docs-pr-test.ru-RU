---
title: "aaaInstall службы Mobility Service (VMware или физических tooAzure) | Документы Microsoft"
description: "Узнайте, как tooinstall hello tooprotect агент службы Mobility Service на локальных компьютерах."
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
ms.workload: backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: f7836e6b35d3838bae1eff927838ce4b245b9f56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-mobility-service-vmware-or-physical-tooazure"></a>Установка службы Mobility Service (VMware или физических tooAzure)
Мобильность службе Azure Site Recovery захватывает записи данных на компьютере и пересылает их toohello сервер обработки. Развертывание компьютер tooevery службы Mobility Service (виртуальной Машины VMware или физических серверов), которые должны tooreplicate tooAzure. Можно развернуть серверы toohello службы Mobility Service требуется tooprotect с помощью hello следующие методы:


* [Установка с помощью инструментов развертывания программного обеспечения, таких как System Center Configuration Manager](site-recovery-install-mobility-service-using-sccm.md).
* [Установка с помощью службы автоматизации Azure и настройки требуемого состояния (DSC службы автоматизации)](site-recovery-automate-mobility-service-install.md).
* [Установка службы Mobility Service вручную с помощью hello графический интерфейс пользователя (GUI)](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui)
* [Установка Mobility Service в командной строке вручную](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).
* [Принудительная установка Mobility Service из Azure Site Recovery](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery).


>[!IMPORTANT]
> Начиная с версии 9.7.0.0, на виртуальных машинах (ВМ), программу установки службы Mobility hello также устанавливает hello последние доступные [агент ВМ Azure](../virtual-machines/windows/extensions-features.md#azure-vm-agent). При сбое компьютера через tooAzure, hello компьютер соответствует необходимым компонентом для любого расширения виртуальной Машины с помощью установки агента hello.

## <a name="prerequisites"></a>Предварительные требования
Перед установкой службы Mobility Service вручную на сервере выполните следующие обязательные действия:
1. Войдите в сервер tooyour конфигурации, а затем откройте окно командной строки с правами администратора.
2. Перейдите в папку bin toohello hello каталога и создайте файл с парольной фразой:

    ```
    cd %ProgramData%\ASR\home\svsystems\bin
    genpassphrase.exe -v > MobSvc.passphrase
    ```
3. Сохраните файл hello парольную фразу в безопасном месте. Файл hello используется во время установки службы Mobility hello.
4. Мобильные службы установщики для всех поддерживаемых операционных системах, в папке %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository hello.

### <a name="mobility-service-installer-to-operating-system-mapping"></a>Сопоставление установщика Mobility Service с операционной системой

| Имя шаблона файла установщика| операционная система |
|---|--|
|Microsoft-ASR\_UA\*Windows\*release.exe | Windows Server 2008 R2 с пакетом обновления 1 (64-разрядная версия) </br> Windows Server 2012 (64-разрядная версия) </br> Windows Server 2012 R2 (64-разрядная версия) |
|Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz| Red Hat Enterprise Linux (RHEL) 6.4, 6.5, 6.6, 6.7, 6.8 (только 64-разрядная версия) </br> CentOS 6.4, 6.5, 6.6, 6.7, 6.8 (только 64-разрядная версия) |
|Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz | Red Hat Enterprise Linux (RHEL) 7.1, 7.2 (только 64-разрядная версия) </br> CentOS 7.0, 7.1, 7.2 (только 64-разрядная версия)</br> CentOs 7.3 (только миграция) |
|Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz| SUSE Linux Enterprise Server 11 SP3 (только 64-разрядная версия)|
|Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz| SUSE Linux Enterprise Server 11 SP4 (только 64-разрядная версия)|
|Microsoft-ASR\_UA\*OL6-64\*release.tar.gz | Oracle Enterprise Linux 6.4, 6.5 (только 64-разрядная версия)|
|Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz | Ubuntu Linux 14.04 (только 64-разрядная версия)|


## <a name="install-mobility-service-manually-by-using-hello-gui"></a>Установка службы Mobility Service вручную с помощью графического интерфейса пользователя hello

>[!IMPORTANT]
> Если вы используете **сервер конфигурации** tooreplicate **виртуальные машины Azure IaaS** из одной подписки Azure или регион tooanother, затем **использовать установки из командной строки на основе hello**  метод

[!INCLUDE [site-recovery-install-mob-svc-gui](../../includes/site-recovery-install-mob-svc-gui.md)]

## <a name="install-mobility-service-manually-at-a-command-prompt"></a>Установка Mobility Service в командной строке вручную

### <a name="command-line-installation-on-a-windows-computer"></a>Установка из командной строки на компьютере с Windows
[!INCLUDE [site-recovery-install-mob-svc-win-cmd](../../includes/site-recovery-install-mob-svc-win-cmd.md)]

### <a name="command-line-installation-on-a-linux-computer"></a>Установка из командной строки на компьютере Linux
[!INCLUDE [site-recovery-install-mob-svc-lin-cmd](../../includes/site-recovery-install-mob-svc-lin-cmd.md)]


## <a name="install-mobility-service-by-push-installation-from-azure-site-recovery"></a>Принудительная установка Mobility Service из Azure Site Recovery
toodo принудительной установки службы Mobility Service с помощью Site Recovery, все целевые компьютеры должны удовлетворять hello следующие необходимые условия.

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-win](../../includes/site-recovery-prepare-push-install-mob-svc-win.md)]

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-lin](../../includes/site-recovery-prepare-push-install-mob-svc-lin.md)]


> [!NOTE]
После установки службы Mobility Service в hello портал Azure, выберите hello **реплицировать** toostart кнопку Защита этих виртуальных машинах.

## <a name="uninstall-mobility-service-on-a-windows-server-computer"></a>Удаление Mobility Service с компьютера Windows Server
Используйте одну из hello следующие методы toouninstall службы Mobility Service на компьютере Windows Server.

### <a name="uninstall-by-using-hello-gui"></a>Удаление с помощью графического интерфейса пользователя hello
1. На панели управления выберите **Программы**.
2. Выберите **Microsoft Azure Site Recovery Mobility Service / главный целевой сервер** и нажмите кнопку **Удалить**.

### <a name="uninstall-at-a-command-prompt"></a>Удаление из командной строки
1. Откройте окно командной строки с правами администратора.
2. toouninstall службы Mobility Service, запустите hello следующую команду:

```
MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
```

## <a name="uninstall-mobility-service-on-a-linux-computer"></a>Удаление службы Mobility на компьютере Linux
1. На сервере Linux войдите как **привилегированный** пользователь.
2. В конечном перейдите слишком/пользователя/локальной/ASR.
3. toouninstall службы Mobility Service, запустите hello следующую команду:

```
uninstall.sh -Y
```
