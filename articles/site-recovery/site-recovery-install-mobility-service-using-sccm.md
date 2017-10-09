---
title: "aaaAutomate установки службы Mobility Service для Azure Site Recovery с помощью средства развертывания программного обеспечения | Документы Microsoft"
description: "Эта статья поможет вам автоматизировать установку Mobility Service с помощью инструментов развертывания программного обеспечения, таких как System Center Configuration Manager."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 6c883c6d5308dcec6e0628b0c2196b3a12e08ebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="automate-mobility-service-installation-by-using-software-deployment-tools"></a>Автоматизация установки Mobility Service с использованием средств развертывания программного обеспечения

>[!IMPORTANT]
В этом документе предполагается, что вы используете версию **9.9.4510.1** или более позднюю.

В этой статье приведен пример того, как можно использовать System Center Configuration Manager toodeploy hello службе Azure Site Recovery Mobility в центре обработки данных. С помощью средства развертывания программного обеспечения как Configuration Manager имеет hello следующие преимущества:
* планирование развертывания свежих обновлений на выделенный период обслуживания для обновления программного обеспечения;
* Масштабирование toohundreds развертывания серверов одновременно


> [!NOTE]
> В этой статье используется действием развертывания hello toodemonstrate System Center Configuration Manager 2012 R2. Автоматизировать установку Mobility Service можно также с помощью [службы автоматизации Azure и настройки требуемого состояния](site-recovery-automate-mobility-service-install.md).

## <a name="prerequisites"></a>Предварительные требования
1. Установленное в вашей среде средство развертывания программного обеспечения, например Configuration Manager.
  Создайте два [коллекции устройств](https://technet.microsoft.com/library/gg682169.aspx), один для всех **серверов Windows**и другой для всех **серверы Linux**, требуется tooprotect с помощью Site Recovery.
3. Сервер конфигурации, зарегистрированный в Site Recovery.
4. Безопасной сетевой общей папке (общей папке Server Message Block), может осуществляться hello server Configuration Manager.

## <a name="deploy-mobility-service-on-computers-running-windows"></a>Развертывание Mobility Service на компьютерах под управлением Windows
> [!NOTE]
> В этой статье предполагается, что hello IP-адрес сервера конфигурации hello 192.168.3.121, который, hello безопасной сетевой общей папке \\\ContosoSecureFS\MobilityServiceInstallers.

### <a name="step-1-prepare-for-deployment"></a>Шаг 1. Подготовка к развертыванию
1. Создайте папку на сетевом ресурсе hello и назовите его **MobSvcWindows**.
2. Войдите в сервер конфигурации tooyour и откройте командную строку администратора.
3. Выполните следующие команды toogenerate файл с парольной фразой hello.

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. Копировать hello **MobSvc.passphrase** файла в hello **MobSvcWindows** папку на общем сетевом ресурсе.
5. Обзор репозитория toohello установщик на сервере конфигурации hello, выполнив следующую команду hello:

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. Копировать hello  **Microsoft ASR\_UA\_*версии*\_Windows\_GA\_*даты* \_ Release.exe** toohello **MobSvcWindows** папку на общем сетевом ресурсе.
7. Скопируйте следующий код hello и сохраните его в **install.bat** в hello **MobSvcWindows** папки.

   > [!NOTE]
   > Замените заполнители hello [CSIP] в этом скрипте hello фактические значения hello IP-адрес сервера конфигурации.

```DOS
Time /t >> C:\Temp\logfile.log
REM ==================================================
REM ==== Clean up hello folders ========================
RMDIR /S /q %temp%\MobSvc
MKDIR %Temp%\MobSvc
MKDIR C:\Temp
REM ==================================================

REM ==== Copy new files ==============================
COPY M*.* %Temp%\MobSvc
CD %Temp%\MobSvc
REN Micro*.exe MobSvcInstaller.exe
REM ==================================================

REM ==== Extract hello installer =======================
MobSvcInstaller.exe /q /x:%Temp%\MobSvc\Extracted
REM ==== Wait 10s for extraction toocomplete =========
TIMEOUT /t 10
REM =================================================

REM ==== Perform installation =======================
REM =================================================

CD %Temp%\MobSvc\Extracted
whoami >> C:\Temp\logfile.log
SET PRODKEY=HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall
REG QUERY %PRODKEY%\{275197FC-14FD-4560-A5EB-38217F80CBD1}
IF NOT %ERRORLEVEL% EQU 0 (
    echo "Product is not installed. Goto INSTALL." >> C:\Temp\logfile.log
    GOTO :INSTALL
) ELSE (
    echo "Product is installed." >> C:\Temp\logfile.log

    echo "Checking for Post-install action status." >> C:\Temp\logfile.log
    GOTO :POSTINSTALLCHECK
)

:POSTINSTALLCHECK
    REG QUERY "HKLM\SOFTWARE\Wow6432Node\InMage Systems\Installed Products\5" /v "PostInstallActions" | Find "Succeeded"
    If %ERRORLEVEL% EQU 0 (
        echo "Post-install actions succeeded. Checking for Configuration status." >> C:\Temp\logfile.log
        GOTO :CONFIGURATIONCHECK
    ) ELSE (
        echo "Post-install actions didn't succeed. Goto INSTALL." >> C:\Temp\logfile.log
        GOTO :INSTALL
    )

:CONFIGURATIONCHECK
    REG QUERY "HKLM\SOFTWARE\Wow6432Node\InMage Systems\Installed Products\5" /v "AgentConfigurationStatus" | Find "Succeeded"
    If %ERRORLEVEL% EQU 0 (
        echo "Configuration has succeeded. Goto UPGRADE." >> C:\Temp\logfile.log
        GOTO :UPGRADE
    ) ELSE (
        echo "Configuration didn't succeed. Goto CONFIGURE." >> C:\Temp\logfile.log
        GOTO :CONFIGURE
    )


:INSTALL
    echo "Perform installation." >> C:\Temp\logfile.log
    UnifiedAgent.exe /Role MS /InstallLocation "C:\Program Files (x86)\Microsoft Azure Site Recovery" /Platform "VmWare" /Silent
    IF %ERRORLEVEL% EQU 0 (
        echo "Installation has succeeded." >> C:\Temp\logfile.log
        (GOTO :CONFIGURE)
    ) ELSE (
        echo "Installation has failed." >> C:\Temp\logfile.log
        GOTO :ENDSCRIPT
    )

:CONFIGURE
    echo "Perform configuration." >> C:\Temp\logfile.log
    cd "C:\Program Files (x86)\Microsoft Azure Site Recovery\agent"
    UnifiedAgentConfigurator.exe  /CSEndPoint "[CSIP]" /PassphraseFilePath %Temp%\MobSvc\MobSvc.passphrase
    IF %ERRORLEVEL% EQU 0 (
        echo "Configuration has succeeded." >> C:\Temp\logfile.log
    ) ELSE (
        echo "Configuration has failed." >> C:\Temp\logfile.log
    )
    GOTO :ENDSCRIPT

:UPGRADE
    echo "Perform upgrade." >> C:\Temp\logfile.log
    UnifiedAgent.exe /Platform "VmWare" /Silent
    IF %ERRORLEVEL% EQU 0 (
        echo "Upgrade has succeeded." >> C:\Temp\logfile.log
    ) ELSE (
        echo "Upgrade has failed." >> C:\Temp\logfile.log
    )
    GOTO :ENDSCRIPT

:ENDSCRIPT
    echo "End of script." >> C:\Temp\logfile.log


```

### <a name="step-2-create-a-package"></a>Шаг 2. Создание пакета

1. Войдите в консоль Configuration Manager tooyour.
2. Обзор слишком**библиотека программного обеспечения** > **управление приложениями** > **пакетов**.
3. Щелкните **Пакеты** правой кнопкой мыши и выберите **Создать пакет**.
4. Укажите значения для hello имя, описание, изготовитель, языка и версии.
5. Выберите hello **этот пакет содержит исходные файлы** флажок.
6. Нажмите кнопку **Обзор**и выберите hello сетевую папку, где хранится установщик hello (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows).

  ![Снимок экрана с мастером создания пакета и программы](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package.png)

7. На hello **тип программы hello выберите, что требуется toocreate** выберите **Стандартная программа**и нажмите кнопку **Далее**.

  ![Снимок экрана с мастером создания пакета и программы](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. На hello **укажите сведения об этой стандартной программе** укажите hello следующие входные данные и нажмите кнопку **Далее**. (hello другие входные данные можно использовать значения по умолчанию).

  | **Имя параметра** | **Значение** |
  |--|--|
  | Имя | Установка Microsoft Azure Mobility Service (Windows) |
  | Команда | install.bat |
  | Программа может запускаться | Независимо от входа пользователя в систему |

  ![Снимок экрана с мастером создания пакета и программы](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties.png)

9. На следующей странице приветствия выберите hello целевой операционной системы. Mobility Service можно устанавливать только на Windows Server 2012 R2, Windows Server 2012 и Windows Server 2008 R2.

  ![Снимок экрана с мастером создания пакета и программы](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2.png)

10. toocomplete приветствия мастера, нажмите кнопку **Далее** дважды.


> [!NOTE]
> сценарий Hello поддерживает оба новые установки агентов службы Mobility Service и обновляет tooagents, которые уже установлены.

### <a name="step-3-deploy-hello-package"></a>Шаг 3: Развертывание пакета hello
1. В консоли Configuration Manager hello, щелкните пакет правой кнопкой мыши и выберите **распространение содержимого**.
  ![Снимок экрана с консолью Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)
2. Выберите hello  **[точки распространения](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)**  на toowhich hello пакеты должны быть скопированы.
3. Мастер завершения hello. Hello пакета, а затем запускает репликацию toohello указан точки распространения.
4. После распространения пакета hello, щелкните правой кнопкой мыши пакет hello и выберите **развернуть**.
  ![Снимок экрана с консолью Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)
5. Выберите коллекцию устройств Windows Server hello, созданный в разделе предварительных требований hello как hello целевую коллекцию для развертывания.

  ![Снимок экрана с мастером развертывания программного обеспечения](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection.png)

6. На hello **укажите места распространения содержимого hello** выберите ваш **точки распространения**.
7. На hello **toocontrol укажите параметры, как это программное обеспечение развертывается** убедитесь, что является целью hello **необходимые**.

  ![Снимок экрана с мастером развертывания программного обеспечения](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. На hello **укажите hello расписание для этого развертывания** укажите расписание. Дополнительные сведения см. в статье [Развертывание пакетов и программ в Configuration Manager](https://technet.microsoft.com/library/gg682178.aspx).
9. На hello **точки распространения** настройте свойства hello в соответствии с потребностями toohello центра обработки данных. Завершите мастер hello.

> [!TIP]
> Перезагружает tooavoid ненужные расписание hello пакета установки во время вашего ежемесячного обслуживания или периода обновлений программного обеспечения.

С помощью консоли Configuration Manager hello можно отслеживать ход выполнения развертывания hello. Go слишком**мониторинг** > **развертываний** > *[имя вашего пакета]*.

  ![Снимок экрана Configuration Manager параметр toomonitor развертываний](./media/site-recovery-install-mobility-service-using-sccm/report.PNG)

## <a name="deploy-mobility-service-on-computers-running-linux"></a>Развертывание Mobility Service на компьютерах под управлением Linux
> [!NOTE]
> В этой статье предполагается, что hello IP-адрес сервера конфигурации hello 192.168.3.121, который, hello безопасной сетевой общей папке \\\ContosoSecureFS\MobilityServiceInstallers.

### <a name="step-1-prepare-for-deployment"></a>Шаг 1. Подготовка к развертыванию
1. Создайте папку на сетевом ресурсе hello и назовите его как **MobSvcLinux**.
2. Войдите в сервер конфигурации tooyour и откройте командную строку администратора.
3. Выполните следующие команды toogenerate файл с парольной фразой hello.

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. Копировать hello **MobSvc.passphrase** файла в hello **MobSvcLinux** папку на общем сетевом ресурсе.
5. Обзор репозитория toohello установщик на сервере конфигурации hello, выполнив команду hello:

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. Копировать hello следующие файлы toohello **MobSvcLinux** папку на общем сетевом ресурсе:
   * Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz
   * Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz
   * Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz
   * Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz
   * Microsoft-ASR\_UA\*OL6-64\*release.tar.gz
   * Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz


7. Скопируйте следующий код hello и сохраните его в **install_linux.sh** в hello **MobSvcLinux** папки.
   > [!NOTE]
   > Замените заполнители hello [CSIP] в этом скрипте hello фактические значения hello IP-адрес сервера конфигурации.

```Bash
#!/usr/bin/env bash

rm -rf /tmp/MobSvc
mkdir -p /tmp/MobSvc
INSTALL_DIR='/usr/local/ASR'
VX_VERSION_FILE='/usr/local/.vx_version'

echo "=============================" >> /tmp/MobSvc/sccm.log
echo `date` >> /tmp/MobSvc/sccm.log
echo "=============================" >> /tmp/MobSvc/sccm.log

if [ -f /etc/oracle-release ] && [ -f /etc/redhat-release ]; then
    if grep -q 'Oracle Linux Server release 6.*' /etc/oracle-release; then
        if uname -a | grep -q x86_64; then
            OS="OL6-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *OL6*.tar.gz /tmp/MobSvc
        fi
    fi
elif [ -f /etc/redhat-release ]; then
    if grep -q 'Red Hat Enterprise Linux Server release 6.* (Santiago)' /etc/redhat-release || \
        grep -q 'CentOS Linux release 6.* (Final)' /etc/redhat-release || \
        grep -q 'CentOS release 6.* (Final)' /etc/redhat-release; then
        if uname -a | grep -q x86_64; then
            OS="RHEL6-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *RHEL6*.tar.gz /tmp/MobSvc
        fi
    elif grep -q 'Red Hat Enterprise Linux Server release 7.* (Maipo)' /etc/redhat-release || \
        grep -q 'CentOS Linux release 7.* (Core)' /etc/redhat-release; then
        if uname -a | grep -q x86_64; then
            OS="RHEL7-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *RHEL7*.tar.gz /tmp/MobSvc
                fi
    fi
elif [ -f /etc/SuSE-release ] && grep -q 'VERSION = 11' /etc/SuSE-release; then
    if grep -q "SUSE Linux Enterprise Server 11" /etc/SuSE-release && grep -q 'PATCHLEVEL = 3' /etc/SuSE-release; then
        if uname -a | grep -q x86_64; then
            OS="SLES11-SP3-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *SLES11-SP3*.tar.gz /tmp/MobSvc
        fi
    elif grep -q "SUSE Linux Enterprise Server 11" /etc/SuSE-release && grep -q 'PATCHLEVEL = 4' /etc/SuSE-release; then
        if uname -a | grep -q x86_64; then
            OS="SLES11-SP4-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *SLES11-SP4*.tar.gz /tmp/MobSvc
        fi
    fi
elif [ -f /etc/lsb-release ] ; then
    if grep -q 'DISTRIB_RELEASE=14.04' /etc/lsb-release ; then
       if uname -a | grep -q x86_64; then
           OS="UBUNTU-14.04-64"
           echo $OS >> /tmp/MobSvc/sccm.log
           cp *UBUNTU-14*.tar.gz /tmp/MobSvc
       fi
    fi
else
    exit 1
fi

if [ -z "$OS" ]; then
    exit 1
fi

Install()
{
    echo "Perform Installation." >> /tmp/MobSvc/sccm.log
    ./install -q -d ${INSTALL_DIR} -r MS -v VmWare
    RET_VAL=$?
    echo "Installation Returncode: $RET_VAL" >> /tmp/MobSvc/sccm.log
    if [ $RET_VAL -eq 0 ]; then
        echo "Installation has succeeded. Proceed tooconfiguration." >> /tmp/MobSvc/sccm.log
        Configure
    else
        echo "Installation has failed." >> /tmp/MobSvc/sccm.log
        exit $RET_VAL
    fi
}

Configure()
{
    echo "Perform configuration." >> /tmp/MobSvc/sccm.log
    ${INSTALL_DIR}/Vx/bin/UnifiedAgentConfigurator.sh -i [CSIP] -P MobSvc.passphrase
    RET_VAL=$?
    echo "Configuration Returncode: $RET_VAL" >> /tmp/MobSvc/sccm.log
    if [ $RET_VAL -eq 0 ]; then
        echo "Configuration has succeeded." >> /tmp/MobSvc/sccm.log
    else
        echo "Configuration has failed." >> /tmp/MobSvc/sccm.log
        exit $RET_VAL
    fi
}

Upgrade()
{
    echo "Perform Upgrade." >> /tmp/MobSvc/sccm.log
    ./install -q -v VmWare
    RET_VAL=$?
    echo "Upgrade Returncode: $RET_VAL" >> /tmp/MobSvc/sccm.log
    if [ $RET_VAL -eq 0 ]; then
        echo "Upgrade has succeeded." >> /tmp/MobSvc/sccm.log
    else
        echo "Upgrade has failed." >> /tmp/MobSvc/sccm.log
        exit $RET_VAL
    fi
}

cp MobSvc.passphrase /tmp/MobSvc
cd /tmp/MobSvc

tar -zxvf *.tar.gz

if [ -e ${VX_VERSION_FILE} ]; then
    echo "${VX_VERSION_FILE} exists. Checking for configuration status." >> /tmp/MobSvc/sccm.log
    agent_configuration=$(grep ^AGENT_CONFIGURATION_STATUS "${VX_VERSION_FILE}" | cut -d"=" -f2 | tr -d " ")
    echo "agent_configuration=$agent_configuration" >> /tmp/MobSvc/sccm.log
     if [ "$agent_configuration" == "Succeeded" ]; then
        echo "Agent is already configured. Proceed tooUpgrade." >> /tmp/MobSvc/sccm.log
        Upgrade
    else
        echo "Agent is not configured. Proceed tooConfigure." >> /tmp/MobSvc/sccm.log
        Configure
    fi
else
    Install
fi

cd /tmp

```

### <a name="step-2-create-a-package"></a>Шаг 2. Создание пакета

1. Войдите в консоль Configuration Manager tooyour.
2. Обзор слишком**библиотека программного обеспечения** > **управление приложениями** > **пакетов**.
3. Щелкните **Пакеты** правой кнопкой мыши и выберите **Создать пакет**.
4. Укажите значения для hello имя, описание, изготовитель, языка и версии.
5. Выберите hello **этот пакет содержит исходные файлы** флажок.
6. Нажмите кнопку **Обзор**и выберите hello сетевую папку, где хранится установщик hello (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux).

  ![Снимок экрана с мастером создания пакета и программы](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package-linux.png)

7. На hello **тип программы hello выберите, что требуется toocreate** выберите **Стандартная программа**и нажмите кнопку **Далее**.

  ![Снимок экрана с мастером создания пакета и программы](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. На hello **укажите сведения об этой стандартной программе** укажите hello следующие входные данные и нажмите кнопку **Далее**. (hello другие входные данные можно использовать значения по умолчанию).

    | **Имя параметра** | **Значение** |
  |--|--|
  | Имя | Установка Microsoft Azure Mobility Service (Linux) |
  | Команда | ./install_linux.sh |
  | Программа может запускаться | Независимо от входа пользователя в систему |

  ![Снимок экрана с мастером создания пакета и программы](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-linux.png)

9. На следующей странице приветствия установите **эта программа может запускаться на любой платформе**.
  ![Снимок экрана с мастером создания пакета и программы](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)

10. toocomplete приветствия мастера, нажмите кнопку **Далее** дважды.

> [!NOTE]
> сценарий Hello поддерживает оба новые установки агентов службы Mobility Service и обновляет tooagents, которые уже установлены.

### <a name="step-3-deploy-hello-package"></a>Шаг 3: Развертывание пакета hello
1. В консоли Configuration Manager hello, щелкните пакет правой кнопкой мыши и выберите **распространение содержимого**.
  ![Снимок экрана с консолью Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)
2. Выберите hello  **[точки распространения](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)**  на toowhich hello пакеты должны быть скопированы.
3. Мастер завершения hello. Hello пакета, а затем запускает репликацию toohello указан точки распространения.
4. После распространения пакета hello, щелкните правой кнопкой мыши пакет hello и выберите **развернуть**.
  ![Снимок экрана с консолью Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)
5. Выберите hello Linux Server коллекцию устройств, созданный в разделе предварительных требований hello как hello целевую коллекцию для развертывания.

  ![Снимок экрана с мастером развертывания программного обеспечения](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection-linux.png)

6. На hello **укажите места распространения содержимого hello** выберите ваш **точки распространения**.
7. На hello **toocontrol укажите параметры, как это программное обеспечение развертывается** убедитесь, что является целью hello **необходимые**.

  ![Снимок экрана с мастером развертывания программного обеспечения](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. На hello **укажите hello расписание для этого развертывания** укажите расписание. Дополнительные сведения см. в статье [Развертывание пакетов и программ в Configuration Manager](https://technet.microsoft.com/library/gg682178.aspx).
9. На hello **точки распространения** настройте свойства hello в соответствии с потребностями toohello центра обработки данных. Завершите мастер hello.

Служба Mobility Service устанавливается на коллекцию устройств сервера Linux, toohello расписание, настроенные в соответствии с hello.

## <a name="other-methods-tooinstall-mobility-service"></a>Другие методы tooinstall службы Mobility Service
Вот еще несколько вариантов действий для установки службы Mobility Service.
* [Ручная установка с использованием графического интерфейса](http://aka.ms/mobsvcmanualinstall)
* [Ручная установка с использованием командной строки](http://aka.ms/mobsvcmanualinstallcli)
* [Принудительная установка с использованием сервера конфигурации](http://aka.ms/pushinstall)
* [Автоматическая установка с использованием службы автоматизации Azure и настройки требуемого состояния](http://aka.ms/mobsvcdscinstall)

## <a name="uninstall-mobility-service"></a>Удаление службы Mobility Service
Можно создать toouninstall пакетов Configuration Manager службы Mobility Service. Используйте hello следующий скрипт toodo так:

```
Time /t >> C:\logfile.log
REM ==================================================
REM ==== Check if Mob Svc is already installed =======
REM ==== If not installed no operation required ========
REM ==== Else run uninstall command =====================
REM ==== {275197FC-14FD-4560-A5EB-38217F80CBD1} is ====
REM ==== guid for Mob Svc Installer ====================
whoami >> C:\logfile.log
NET START | FIND "InMage Scout Application Service"
IF  %ERRORLEVEL% EQU 1 (GOTO :INSTALL) ELSE GOTO :UNINSTALL
:NOOPERATION
                echo "No Operation Required." >> c:\logfile.log
                GOTO :ENDSCRIPT
:UNINSTALL
                echo "Uninstall" >> C:\logfile.log
                MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
:ENDSCRIPT

```

## <a name="next-steps"></a>Дальнейшие действия
Теперь вы готовы слишком[включить защиту](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications) для виртуальных машин.
