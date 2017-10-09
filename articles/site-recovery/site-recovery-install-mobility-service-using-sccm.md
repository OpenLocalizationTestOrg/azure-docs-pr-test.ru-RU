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
# <a name="automate-mobility-service-installation-by-using-software-deployment-tools"></a><span data-ttu-id="0b8bf-103">Автоматизация установки Mobility Service с использованием средств развертывания программного обеспечения</span><span class="sxs-lookup"><span data-stu-id="0b8bf-103">Automate Mobility Service installation by using software deployment tools</span></span>

>[!IMPORTANT]
<span data-ttu-id="0b8bf-104">В этом документе предполагается, что вы используете версию **9.9.4510.1** или более позднюю.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-104">This document assumes you are using version **9.9.4510.1** or higher.</span></span>

<span data-ttu-id="0b8bf-105">В этой статье приведен пример того, как можно использовать System Center Configuration Manager toodeploy hello службе Azure Site Recovery Mobility в центре обработки данных.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-105">This article provides you an example of how you can use System Center Configuration Manager toodeploy hello Azure Site Recovery Mobility Service in your datacenter.</span></span> <span data-ttu-id="0b8bf-106">С помощью средства развертывания программного обеспечения как Configuration Manager имеет hello следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="0b8bf-106">Using a software deployment tool like Configuration Manager has hello following advantages:</span></span>
* <span data-ttu-id="0b8bf-107">планирование развертывания свежих обновлений на выделенный период обслуживания для обновления программного обеспечения;</span><span class="sxs-lookup"><span data-stu-id="0b8bf-107">Scheduling deployment of fresh installations and upgrades, during your planned maintenance window for software updates</span></span>
* <span data-ttu-id="0b8bf-108">Масштабирование toohundreds развертывания серверов одновременно</span><span class="sxs-lookup"><span data-stu-id="0b8bf-108">Scaling deployment toohundreds of servers simultaneously</span></span>


> [!NOTE]
> <span data-ttu-id="0b8bf-109">В этой статье используется действием развертывания hello toodemonstrate System Center Configuration Manager 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-109">This article uses System Center Configuration Manager 2012 R2 toodemonstrate hello deployment activity.</span></span> <span data-ttu-id="0b8bf-110">Автоматизировать установку Mobility Service можно также с помощью [службы автоматизации Azure и настройки требуемого состояния](site-recovery-automate-mobility-service-install.md).</span><span class="sxs-lookup"><span data-stu-id="0b8bf-110">You could also automate Mobility Service installation by using [Azure Automation and Desired State Configuration](site-recovery-automate-mobility-service-install.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0b8bf-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0b8bf-111">Prerequisites</span></span>
1. <span data-ttu-id="0b8bf-112">Установленное в вашей среде средство развертывания программного обеспечения, например Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-112">A software deployment tool, like Configuration Manager, that is already deployed in your environment.</span></span>
  <span data-ttu-id="0b8bf-113">Создайте два [коллекции устройств](https://technet.microsoft.com/library/gg682169.aspx), один для всех **серверов Windows**и другой для всех **серверы Linux**, требуется tooprotect с помощью Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-113">Create two [device collections](https://technet.microsoft.com/library/gg682169.aspx), one for all **Windows servers**, and another for all **Linux servers**, that you want tooprotect by using Site Recovery.</span></span>
3. <span data-ttu-id="0b8bf-114">Сервер конфигурации, зарегистрированный в Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-114">A configuration server that is already registered with Site Recovery.</span></span>
4. <span data-ttu-id="0b8bf-115">Безопасной сетевой общей папке (общей папке Server Message Block), может осуществляться hello server Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-115">A secure network file share (Server Message Block share) that can be accessed by hello Configuration Manager server.</span></span>

## <a name="deploy-mobility-service-on-computers-running-windows"></a><span data-ttu-id="0b8bf-116">Развертывание Mobility Service на компьютерах под управлением Windows</span><span class="sxs-lookup"><span data-stu-id="0b8bf-116">Deploy Mobility Service on computers running Windows</span></span>
> [!NOTE]
> <span data-ttu-id="0b8bf-117">В этой статье предполагается, что hello IP-адрес сервера конфигурации hello 192.168.3.121, который, hello безопасной сетевой общей папке \\\ContosoSecureFS\MobilityServiceInstallers.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-117">This article assumes that hello IP address of hello configuration server is 192.168.3.121, and that hello secure network file share is \\\ContosoSecureFS\MobilityServiceInstallers.</span></span>

### <a name="step-1-prepare-for-deployment"></a><span data-ttu-id="0b8bf-118">Шаг 1. Подготовка к развертыванию</span><span class="sxs-lookup"><span data-stu-id="0b8bf-118">Step 1: Prepare for deployment</span></span>
1. <span data-ttu-id="0b8bf-119">Создайте папку на сетевом ресурсе hello и назовите его **MobSvcWindows**.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-119">Create a folder on hello network share, and name it **MobSvcWindows**.</span></span>
2. <span data-ttu-id="0b8bf-120">Войдите в сервер конфигурации tooyour и откройте командную строку администратора.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-120">Sign in tooyour configuration server, and open an administrative command prompt.</span></span>
3. <span data-ttu-id="0b8bf-121">Выполните следующие команды toogenerate файл с парольной фразой hello.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-121">Run hello following commands toogenerate a passphrase file:</span></span>

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. <span data-ttu-id="0b8bf-122">Копировать hello **MobSvc.passphrase** файла в hello **MobSvcWindows** папку на общем сетевом ресурсе.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-122">Copy hello **MobSvc.passphrase** file into hello **MobSvcWindows** folder on your network share.</span></span>
5. <span data-ttu-id="0b8bf-123">Обзор репозитория toohello установщик на сервере конфигурации hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="0b8bf-123">Browse toohello installer repository on hello configuration server by running hello following command:</span></span>

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. <span data-ttu-id="0b8bf-124">Копировать hello  **Microsoft ASR\_UA\_*версии*\_Windows\_GA\_*даты* \_ Release.exe** toohello **MobSvcWindows** папку на общем сетевом ресурсе.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-124">Copy hello **Microsoft-ASR\_UA\_*version*\_Windows\_GA\_*date*\_Release.exe** toohello **MobSvcWindows** folder on your network share.</span></span>
7. <span data-ttu-id="0b8bf-125">Скопируйте следующий код hello и сохраните его в **install.bat** в hello **MobSvcWindows** папки.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-125">Copy hello following code, and save it as **install.bat** into hello **MobSvcWindows** folder.</span></span>

   > [!NOTE]
   > <span data-ttu-id="0b8bf-126">Замените заполнители hello [CSIP] в этом скрипте hello фактические значения hello IP-адрес сервера конфигурации.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-126">Replace hello [CSIP] placeholders in this script with hello actual values of hello IP address of your configuration server.</span></span>

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

### <a name="step-2-create-a-package"></a><span data-ttu-id="0b8bf-127">Шаг 2. Создание пакета</span><span class="sxs-lookup"><span data-stu-id="0b8bf-127">Step 2: Create a package</span></span>

1. <span data-ttu-id="0b8bf-128">Войдите в консоль Configuration Manager tooyour.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-128">Sign in tooyour Configuration Manager console.</span></span>
2. <span data-ttu-id="0b8bf-129">Обзор слишком**библиотека программного обеспечения** > **управление приложениями** > **пакетов**.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-129">Browse too**Software Library** > **Application Management** > **Packages**.</span></span>
3. <span data-ttu-id="0b8bf-130">Щелкните **Пакеты** правой кнопкой мыши и выберите **Создать пакет**.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-130">Right-click **Packages**, and select **Create Package**.</span></span>
4. <span data-ttu-id="0b8bf-131">Укажите значения для hello имя, описание, изготовитель, языка и версии.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-131">Provide values for hello name, description, manufacturer, language, and version.</span></span>
5. <span data-ttu-id="0b8bf-132">Выберите hello **этот пакет содержит исходные файлы** флажок.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-132">Select hello **This package contains source files** check box.</span></span>
6. <span data-ttu-id="0b8bf-133">Нажмите кнопку **Обзор**и выберите hello сетевую папку, где хранится установщик hello (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows).</span><span class="sxs-lookup"><span data-stu-id="0b8bf-133">Click **Browse**, and select hello network share where hello installer is stored (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows).</span></span>

  ![Снимок экрана с мастером создания пакета и программы](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package.png)

7. <span data-ttu-id="0b8bf-135">На hello **тип программы hello выберите, что требуется toocreate** выберите **Стандартная программа**и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-135">On hello **Choose hello program type that you want toocreate** page, select **Standard Program**, and click **Next**.</span></span>

  ![Снимок экрана с мастером создания пакета и программы](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. <span data-ttu-id="0b8bf-137">На hello **укажите сведения об этой стандартной программе** укажите hello следующие входные данные и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-137">On hello **Specify information about this standard program** page, provide hello following inputs, and click **Next**.</span></span> <span data-ttu-id="0b8bf-138">(hello другие входные данные можно использовать значения по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="0b8bf-138">(hello other inputs can use their default values.)</span></span>

  | <span data-ttu-id="0b8bf-139">**Имя параметра**</span><span class="sxs-lookup"><span data-stu-id="0b8bf-139">**Parameter name**</span></span> | <span data-ttu-id="0b8bf-140">**Значение**</span><span class="sxs-lookup"><span data-stu-id="0b8bf-140">**Value**</span></span> |
  |--|--|
  | <span data-ttu-id="0b8bf-141">Имя</span><span class="sxs-lookup"><span data-stu-id="0b8bf-141">Name</span></span> | <span data-ttu-id="0b8bf-142">Установка Microsoft Azure Mobility Service (Windows)</span><span class="sxs-lookup"><span data-stu-id="0b8bf-142">Install Microsoft Azure Mobility Service (Windows)</span></span> |
  | <span data-ttu-id="0b8bf-143">Команда</span><span class="sxs-lookup"><span data-stu-id="0b8bf-143">Command line</span></span> | <span data-ttu-id="0b8bf-144">install.bat</span><span class="sxs-lookup"><span data-stu-id="0b8bf-144">install.bat</span></span> |
  | <span data-ttu-id="0b8bf-145">Программа может запускаться</span><span class="sxs-lookup"><span data-stu-id="0b8bf-145">Program can run</span></span> | <span data-ttu-id="0b8bf-146">Независимо от входа пользователя в систему</span><span class="sxs-lookup"><span data-stu-id="0b8bf-146">Whether or not a user is logged on</span></span> |

  ![Снимок экрана с мастером создания пакета и программы](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties.png)

9. <span data-ttu-id="0b8bf-148">На следующей странице приветствия выберите hello целевой операционной системы.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-148">On hello next page, select hello target operating systems.</span></span> <span data-ttu-id="0b8bf-149">Mobility Service можно устанавливать только на Windows Server 2012 R2, Windows Server 2012 и Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-149">Mobility Service can be installed only on Windows Server 2012 R2, Windows Server 2012, and Windows Server 2008 R2.</span></span>

  ![Снимок экрана с мастером создания пакета и программы](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2.png)

10. <span data-ttu-id="0b8bf-151">toocomplete приветствия мастера, нажмите кнопку **Далее** дважды.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-151">toocomplete hello wizard, click **Next** twice.</span></span>


> [!NOTE]
> <span data-ttu-id="0b8bf-152">сценарий Hello поддерживает оба новые установки агентов службы Mobility Service и обновляет tooagents, которые уже установлены.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-152">hello script supports both new installations of Mobility Service agents and updates tooagents that are already installed.</span></span>

### <a name="step-3-deploy-hello-package"></a><span data-ttu-id="0b8bf-153">Шаг 3: Развертывание пакета hello</span><span class="sxs-lookup"><span data-stu-id="0b8bf-153">Step 3: Deploy hello package</span></span>
1. <span data-ttu-id="0b8bf-154">В консоли Configuration Manager hello, щелкните пакет правой кнопкой мыши и выберите **распространение содержимого**.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-154">In hello Configuration Manager console, right-click your package, and select **Distribute Content**.</span></span>
  <span data-ttu-id="0b8bf-155">![Снимок экрана с консолью Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span><span class="sxs-lookup"><span data-stu-id="0b8bf-155">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span></span>
2. <span data-ttu-id="0b8bf-156">Выберите hello  **[точки распространения](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)**  на toowhich hello пакеты должны быть скопированы.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-156">Select hello **[distribution points](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** on toowhich hello packages should be copied.</span></span>
3. <span data-ttu-id="0b8bf-157">Мастер завершения hello.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-157">Complete hello wizard.</span></span> <span data-ttu-id="0b8bf-158">Hello пакета, а затем запускает репликацию toohello указан точки распространения.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-158">hello package then starts replicating toohello specified distribution points.</span></span>
4. <span data-ttu-id="0b8bf-159">После распространения пакета hello, щелкните правой кнопкой мыши пакет hello и выберите **развернуть**.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-159">After hello package distribution is done, right-click hello package, and select **Deploy**.</span></span>
  <span data-ttu-id="0b8bf-160">![Снимок экрана с консолью Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span><span class="sxs-lookup"><span data-stu-id="0b8bf-160">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span></span>
5. <span data-ttu-id="0b8bf-161">Выберите коллекцию устройств Windows Server hello, созданный в разделе предварительных требований hello как hello целевую коллекцию для развертывания.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-161">Select hello Windows Server device collection you created in hello prerequisites section as hello target collection for deployment.</span></span>

  ![Снимок экрана с мастером развертывания программного обеспечения](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection.png)

6. <span data-ttu-id="0b8bf-163">На hello **укажите места распространения содержимого hello** выберите ваш **точки распространения**.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-163">On hello **Specify hello content destination** page, select your **Distribution Points**.</span></span>
7. <span data-ttu-id="0b8bf-164">На hello **toocontrol укажите параметры, как это программное обеспечение развертывается** убедитесь, что является целью hello **необходимые**.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-164">On hello **Specify settings toocontrol how this software is deployed** page, ensure that hello purpose is **Required**.</span></span>

  ![Снимок экрана с мастером развертывания программного обеспечения](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. <span data-ttu-id="0b8bf-166">На hello **укажите hello расписание для этого развертывания** укажите расписание.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-166">On hello **Specify hello schedule for this deployment** page, specify a schedule.</span></span> <span data-ttu-id="0b8bf-167">Дополнительные сведения см. в статье [Развертывание пакетов и программ в Configuration Manager](https://technet.microsoft.com/library/gg682178.aspx).</span><span class="sxs-lookup"><span data-stu-id="0b8bf-167">For more information, see [scheduling packages](https://technet.microsoft.com/library/gg682178.aspx).</span></span>
9. <span data-ttu-id="0b8bf-168">На hello **точки распространения** настройте свойства hello в соответствии с потребностями toohello центра обработки данных.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-168">On hello **Distribution Points** page, configure hello properties according toohello needs of your datacenter.</span></span> <span data-ttu-id="0b8bf-169">Завершите мастер hello.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-169">Then complete hello wizard.</span></span>

> [!TIP]
> <span data-ttu-id="0b8bf-170">Перезагружает tooavoid ненужные расписание hello пакета установки во время вашего ежемесячного обслуживания или периода обновлений программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-170">tooavoid unnecessary reboots, schedule hello package installation during your monthly maintenance window or software updates window.</span></span>

<span data-ttu-id="0b8bf-171">С помощью консоли Configuration Manager hello можно отслеживать ход выполнения развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-171">You can monitor hello deployment progress by using hello Configuration Manager console.</span></span> <span data-ttu-id="0b8bf-172">Go слишком**мониторинг** > **развертываний** > *[имя вашего пакета]*.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-172">Go too**Monitoring** > **Deployments** > *[your package name]*.</span></span>

  ![Снимок экрана Configuration Manager параметр toomonitor развертываний](./media/site-recovery-install-mobility-service-using-sccm/report.PNG)

## <a name="deploy-mobility-service-on-computers-running-linux"></a><span data-ttu-id="0b8bf-174">Развертывание Mobility Service на компьютерах под управлением Linux</span><span class="sxs-lookup"><span data-stu-id="0b8bf-174">Deploy Mobility Service on computers running Linux</span></span>
> [!NOTE]
> <span data-ttu-id="0b8bf-175">В этой статье предполагается, что hello IP-адрес сервера конфигурации hello 192.168.3.121, который, hello безопасной сетевой общей папке \\\ContosoSecureFS\MobilityServiceInstallers.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-175">This article assumes that hello IP address of hello configuration server is 192.168.3.121, and that hello secure network file share is \\\ContosoSecureFS\MobilityServiceInstallers.</span></span>

### <a name="step-1-prepare-for-deployment"></a><span data-ttu-id="0b8bf-176">Шаг 1. Подготовка к развертыванию</span><span class="sxs-lookup"><span data-stu-id="0b8bf-176">Step 1: Prepare for deployment</span></span>
1. <span data-ttu-id="0b8bf-177">Создайте папку на сетевом ресурсе hello и назовите его как **MobSvcLinux**.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-177">Create a folder on hello network share, and name it as **MobSvcLinux**.</span></span>
2. <span data-ttu-id="0b8bf-178">Войдите в сервер конфигурации tooyour и откройте командную строку администратора.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-178">Sign in tooyour configuration server, and open an administrative command prompt.</span></span>
3. <span data-ttu-id="0b8bf-179">Выполните следующие команды toogenerate файл с парольной фразой hello.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-179">Run hello following commands toogenerate a passphrase file:</span></span>

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. <span data-ttu-id="0b8bf-180">Копировать hello **MobSvc.passphrase** файла в hello **MobSvcLinux** папку на общем сетевом ресурсе.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-180">Copy hello **MobSvc.passphrase** file into hello **MobSvcLinux** folder on your network share.</span></span>
5. <span data-ttu-id="0b8bf-181">Обзор репозитория toohello установщик на сервере конфигурации hello, выполнив команду hello:</span><span class="sxs-lookup"><span data-stu-id="0b8bf-181">Browse toohello installer repository on hello configuration server by running hello command:</span></span>

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. <span data-ttu-id="0b8bf-182">Копировать hello следующие файлы toohello **MobSvcLinux** папку на общем сетевом ресурсе:</span><span class="sxs-lookup"><span data-stu-id="0b8bf-182">Copy hello following files toohello **MobSvcLinux** folder on your network share:</span></span>
   * <span data-ttu-id="0b8bf-183">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="0b8bf-183">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span></span>
   * <span data-ttu-id="0b8bf-184">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="0b8bf-184">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span></span>
   * <span data-ttu-id="0b8bf-185">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="0b8bf-185">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span></span>
   * <span data-ttu-id="0b8bf-186">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="0b8bf-186">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span></span>
   * <span data-ttu-id="0b8bf-187">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="0b8bf-187">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span></span>
   * <span data-ttu-id="0b8bf-188">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="0b8bf-188">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span></span>


7. <span data-ttu-id="0b8bf-189">Скопируйте следующий код hello и сохраните его в **install_linux.sh** в hello **MobSvcLinux** папки.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-189">Copy hello following code, and save it as **install_linux.sh** into hello **MobSvcLinux** folder.</span></span>
   > [!NOTE]
   > <span data-ttu-id="0b8bf-190">Замените заполнители hello [CSIP] в этом скрипте hello фактические значения hello IP-адрес сервера конфигурации.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-190">Replace hello [CSIP] placeholders in this script with hello actual values of hello IP address of your configuration server.</span></span>

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

### <a name="step-2-create-a-package"></a><span data-ttu-id="0b8bf-191">Шаг 2. Создание пакета</span><span class="sxs-lookup"><span data-stu-id="0b8bf-191">Step 2: Create a package</span></span>

1. <span data-ttu-id="0b8bf-192">Войдите в консоль Configuration Manager tooyour.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-192">Sign in  tooyour Configuration Manager console.</span></span>
2. <span data-ttu-id="0b8bf-193">Обзор слишком**библиотека программного обеспечения** > **управление приложениями** > **пакетов**.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-193">Browse too**Software Library** > **Application Management** > **Packages**.</span></span>
3. <span data-ttu-id="0b8bf-194">Щелкните **Пакеты** правой кнопкой мыши и выберите **Создать пакет**.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-194">Right-click **Packages**, and select **Create Package**.</span></span>
4. <span data-ttu-id="0b8bf-195">Укажите значения для hello имя, описание, изготовитель, языка и версии.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-195">Provide values for hello name, description, manufacturer, language, and version.</span></span>
5. <span data-ttu-id="0b8bf-196">Выберите hello **этот пакет содержит исходные файлы** флажок.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-196">Select hello **This package contains source files** check box.</span></span>
6. <span data-ttu-id="0b8bf-197">Нажмите кнопку **Обзор**и выберите hello сетевую папку, где хранится установщик hello (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux).</span><span class="sxs-lookup"><span data-stu-id="0b8bf-197">Click **Browse**, and select hello network share where hello installer is stored (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux).</span></span>

  ![Снимок экрана с мастером создания пакета и программы](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package-linux.png)

7. <span data-ttu-id="0b8bf-199">На hello **тип программы hello выберите, что требуется toocreate** выберите **Стандартная программа**и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-199">On hello **Choose hello program type that you want toocreate** page, select **Standard Program**, and click **Next**.</span></span>

  ![Снимок экрана с мастером создания пакета и программы](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. <span data-ttu-id="0b8bf-201">На hello **укажите сведения об этой стандартной программе** укажите hello следующие входные данные и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-201">On hello **Specify information about this standard program** page, provide hello following inputs, and click **Next**.</span></span> <span data-ttu-id="0b8bf-202">(hello другие входные данные можно использовать значения по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="0b8bf-202">(hello other inputs can use their default values.)</span></span>

    | <span data-ttu-id="0b8bf-203">**Имя параметра**</span><span class="sxs-lookup"><span data-stu-id="0b8bf-203">**Parameter name**</span></span> | <span data-ttu-id="0b8bf-204">**Значение**</span><span class="sxs-lookup"><span data-stu-id="0b8bf-204">**Value**</span></span> |
  |--|--|
  | <span data-ttu-id="0b8bf-205">Имя</span><span class="sxs-lookup"><span data-stu-id="0b8bf-205">Name</span></span> | <span data-ttu-id="0b8bf-206">Установка Microsoft Azure Mobility Service (Linux)</span><span class="sxs-lookup"><span data-stu-id="0b8bf-206">Install Microsoft Azure Mobility Service (Linux)</span></span> |
  | <span data-ttu-id="0b8bf-207">Команда</span><span class="sxs-lookup"><span data-stu-id="0b8bf-207">Command line</span></span> | <span data-ttu-id="0b8bf-208">./install_linux.sh</span><span class="sxs-lookup"><span data-stu-id="0b8bf-208">./install_linux.sh</span></span> |
  | <span data-ttu-id="0b8bf-209">Программа может запускаться</span><span class="sxs-lookup"><span data-stu-id="0b8bf-209">Program can run</span></span> | <span data-ttu-id="0b8bf-210">Независимо от входа пользователя в систему</span><span class="sxs-lookup"><span data-stu-id="0b8bf-210">Whether or not a user is logged on</span></span> |

  ![Снимок экрана с мастером создания пакета и программы](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-linux.png)

9. <span data-ttu-id="0b8bf-212">На следующей странице приветствия установите **эта программа может запускаться на любой платформе**.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-212">On hello next page, select **This program can run on any platform**.</span></span>
  <span data-ttu-id="0b8bf-213">![Снимок экрана с мастером создания пакета и программы](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)</span><span class="sxs-lookup"><span data-stu-id="0b8bf-213">![Screenshot of Create Package and Program wizard](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)</span></span>

10. <span data-ttu-id="0b8bf-214">toocomplete приветствия мастера, нажмите кнопку **Далее** дважды.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-214">toocomplete hello wizard, click **Next** twice.</span></span>

> [!NOTE]
> <span data-ttu-id="0b8bf-215">сценарий Hello поддерживает оба новые установки агентов службы Mobility Service и обновляет tooagents, которые уже установлены.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-215">hello script supports both new installations of Mobility Service agents and updates tooagents that are already installed.</span></span>

### <a name="step-3-deploy-hello-package"></a><span data-ttu-id="0b8bf-216">Шаг 3: Развертывание пакета hello</span><span class="sxs-lookup"><span data-stu-id="0b8bf-216">Step 3: Deploy hello package</span></span>
1. <span data-ttu-id="0b8bf-217">В консоли Configuration Manager hello, щелкните пакет правой кнопкой мыши и выберите **распространение содержимого**.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-217">In hello Configuration Manager console, right-click your package, and select **Distribute Content**.</span></span>
  <span data-ttu-id="0b8bf-218">![Снимок экрана с консолью Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span><span class="sxs-lookup"><span data-stu-id="0b8bf-218">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span></span>
2. <span data-ttu-id="0b8bf-219">Выберите hello  **[точки распространения](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)**  на toowhich hello пакеты должны быть скопированы.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-219">Select hello **[distribution points](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** on toowhich hello packages should be copied.</span></span>
3. <span data-ttu-id="0b8bf-220">Мастер завершения hello.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-220">Complete hello wizard.</span></span> <span data-ttu-id="0b8bf-221">Hello пакета, а затем запускает репликацию toohello указан точки распространения.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-221">hello package then starts replicating toohello specified distribution points.</span></span>
4. <span data-ttu-id="0b8bf-222">После распространения пакета hello, щелкните правой кнопкой мыши пакет hello и выберите **развернуть**.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-222">After hello package distribution is done, right-click hello package, and select **Deploy**.</span></span>
  <span data-ttu-id="0b8bf-223">![Снимок экрана с консолью Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span><span class="sxs-lookup"><span data-stu-id="0b8bf-223">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span></span>
5. <span data-ttu-id="0b8bf-224">Выберите hello Linux Server коллекцию устройств, созданный в разделе предварительных требований hello как hello целевую коллекцию для развертывания.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-224">Select hello Linux Server device collection you created in hello prerequisites section as hello target collection for deployment.</span></span>

  ![Снимок экрана с мастером развертывания программного обеспечения](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection-linux.png)

6. <span data-ttu-id="0b8bf-226">На hello **укажите места распространения содержимого hello** выберите ваш **точки распространения**.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-226">On hello **Specify hello content destination** page, select your **Distribution Points**.</span></span>
7. <span data-ttu-id="0b8bf-227">На hello **toocontrol укажите параметры, как это программное обеспечение развертывается** убедитесь, что является целью hello **необходимые**.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-227">On hello **Specify settings toocontrol how this software is deployed** page, ensure that hello purpose is **Required**.</span></span>

  ![Снимок экрана с мастером развертывания программного обеспечения](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. <span data-ttu-id="0b8bf-229">На hello **укажите hello расписание для этого развертывания** укажите расписание.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-229">On hello **Specify hello schedule for this deployment** page, specify a schedule.</span></span> <span data-ttu-id="0b8bf-230">Дополнительные сведения см. в статье [Развертывание пакетов и программ в Configuration Manager](https://technet.microsoft.com/library/gg682178.aspx).</span><span class="sxs-lookup"><span data-stu-id="0b8bf-230">For more information, see [scheduling packages](https://technet.microsoft.com/library/gg682178.aspx).</span></span>
9. <span data-ttu-id="0b8bf-231">На hello **точки распространения** настройте свойства hello в соответствии с потребностями toohello центра обработки данных.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-231">On hello **Distribution Points** page, configure hello properties according toohello needs of your datacenter.</span></span> <span data-ttu-id="0b8bf-232">Завершите мастер hello.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-232">Then complete hello wizard.</span></span>

<span data-ttu-id="0b8bf-233">Служба Mobility Service устанавливается на коллекцию устройств сервера Linux, toohello расписание, настроенные в соответствии с hello.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-233">Mobility Service gets installed on hello Linux Server Device Collection, according toohello schedule you configured.</span></span>

## <a name="other-methods-tooinstall-mobility-service"></a><span data-ttu-id="0b8bf-234">Другие методы tooinstall службы Mobility Service</span><span class="sxs-lookup"><span data-stu-id="0b8bf-234">Other methods tooinstall Mobility Service</span></span>
<span data-ttu-id="0b8bf-235">Вот еще несколько вариантов действий для установки службы Mobility Service.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-235">Here are some other options for installing Mobility Service:</span></span>
* [<span data-ttu-id="0b8bf-236">Ручная установка с использованием графического интерфейса</span><span class="sxs-lookup"><span data-stu-id="0b8bf-236">Manual Installation using GUI</span></span>](http://aka.ms/mobsvcmanualinstall)
* [<span data-ttu-id="0b8bf-237">Ручная установка с использованием командной строки</span><span class="sxs-lookup"><span data-stu-id="0b8bf-237">Manual Installation using command-line</span></span>](http://aka.ms/mobsvcmanualinstallcli)
* [<span data-ttu-id="0b8bf-238">Принудительная установка с использованием сервера конфигурации</span><span class="sxs-lookup"><span data-stu-id="0b8bf-238">Push Installation using configuration server </span></span>](http://aka.ms/pushinstall)
* [<span data-ttu-id="0b8bf-239">Автоматическая установка с использованием службы автоматизации Azure и настройки требуемого состояния</span><span class="sxs-lookup"><span data-stu-id="0b8bf-239">Automated Installation using Azure Automation & Desired State Configuration </span></span>](http://aka.ms/mobsvcdscinstall)

## <a name="uninstall-mobility-service"></a><span data-ttu-id="0b8bf-240">Удаление службы Mobility Service</span><span class="sxs-lookup"><span data-stu-id="0b8bf-240">Uninstall Mobility Service</span></span>
<span data-ttu-id="0b8bf-241">Можно создать toouninstall пакетов Configuration Manager службы Mobility Service.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-241">You can create Configuration Manager packages toouninstall Mobility Service.</span></span> <span data-ttu-id="0b8bf-242">Используйте hello следующий скрипт toodo так:</span><span class="sxs-lookup"><span data-stu-id="0b8bf-242">Use hello following script toodo so:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="0b8bf-243">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0b8bf-243">Next steps</span></span>
<span data-ttu-id="0b8bf-244">Теперь вы готовы слишком[включить защиту](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications) для виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="0b8bf-244">You are now ready too[enable protection](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications) for your virtual machines.</span></span>
