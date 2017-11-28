---
title: "Автоматизация установки Mobility Service для Azure Site Recovery с использованием средств развертывания программного обеспечения | Документация Майкрософт"
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
ms.openlocfilehash: 49b72cd306aa91f114af7688f02d95db6f6eca05
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="automate-mobility-service-installation-by-using-software-deployment-tools"></a><span data-ttu-id="d9009-103">Автоматизация установки Mobility Service с использованием средств развертывания программного обеспечения</span><span class="sxs-lookup"><span data-stu-id="d9009-103">Automate Mobility Service installation by using software deployment tools</span></span>

>[!IMPORTANT]
<span data-ttu-id="d9009-104">В этом документе предполагается, что вы используете версию **9.9.4510.1** или более позднюю.</span><span class="sxs-lookup"><span data-stu-id="d9009-104">This document assumes you are using version **9.9.4510.1** or higher.</span></span>

<span data-ttu-id="d9009-105">В этой статье приведен пример того, как можно применить System Center Configuration Manager для развертывания Azure Site Recovery Mobility Service в центре обработки данных.</span><span class="sxs-lookup"><span data-stu-id="d9009-105">This article provides you an example of how you can use System Center Configuration Manager to deploy the Azure Site Recovery Mobility Service in your datacenter.</span></span> <span data-ttu-id="d9009-106">Такие средства развертывания программного обеспечения, как Configuration Manager, предоставляют следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="d9009-106">Using a software deployment tool like Configuration Manager has the following advantages:</span></span>
* <span data-ttu-id="d9009-107">планирование развертывания свежих обновлений на выделенный период обслуживания для обновления программного обеспечения;</span><span class="sxs-lookup"><span data-stu-id="d9009-107">Scheduling deployment of fresh installations and upgrades, during your planned maintenance window for software updates</span></span>
* <span data-ttu-id="d9009-108">масштабирование развертывания вплоть до нескольких сотен серверов.</span><span class="sxs-lookup"><span data-stu-id="d9009-108">Scaling deployment to hundreds of servers simultaneously</span></span>


> [!NOTE]
> <span data-ttu-id="d9009-109">В этой статье демонстрируется развертывание на примере System Center Configuration Manager 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="d9009-109">This article uses System Center Configuration Manager 2012 R2 to demonstrate the deployment activity.</span></span> <span data-ttu-id="d9009-110">Автоматизировать установку Mobility Service можно также с помощью [службы автоматизации Azure и настройки требуемого состояния](site-recovery-automate-mobility-service-install.md).</span><span class="sxs-lookup"><span data-stu-id="d9009-110">You could also automate Mobility Service installation by using [Azure Automation and Desired State Configuration](site-recovery-automate-mobility-service-install.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9009-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d9009-111">Prerequisites</span></span>
1. <span data-ttu-id="d9009-112">Установленное в вашей среде средство развертывания программного обеспечения, например Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="d9009-112">A software deployment tool, like Configuration Manager, that is already deployed in your environment.</span></span>
  <span data-ttu-id="d9009-113">Создайте две [коллекции устройств](https://technet.microsoft.com/library/gg682169.aspx) — одну для всех **серверов Windows** и другую для всех **серверов Linux**, для защиты которых вы будете применять Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="d9009-113">Create two [device collections](https://technet.microsoft.com/library/gg682169.aspx), one for all **Windows servers**, and another for all **Linux servers**, that you want to protect by using Site Recovery.</span></span>
3. <span data-ttu-id="d9009-114">Сервер конфигурации, зарегистрированный в Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="d9009-114">A configuration server that is already registered with Site Recovery.</span></span>
4. <span data-ttu-id="d9009-115">Защищенная общая сетевая папка (общая папка SMB), к которой есть доступ с сервера Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="d9009-115">A secure network file share (Server Message Block share) that can be accessed by the Configuration Manager server.</span></span>

## <a name="deploy-mobility-service-on-computers-running-windows"></a><span data-ttu-id="d9009-116">Развертывание Mobility Service на компьютерах под управлением Windows</span><span class="sxs-lookup"><span data-stu-id="d9009-116">Deploy Mobility Service on computers running Windows</span></span>
> [!NOTE]
> <span data-ttu-id="d9009-117">В этой статье предполагается, что сервер конфигурации использует IP-адрес 192.168.3.121, а защищенная общая сетевая папка имеет адрес \\\ContosoSecureFS\MobilityServiceInstallers.</span><span class="sxs-lookup"><span data-stu-id="d9009-117">This article assumes that the IP address of the configuration server is 192.168.3.121, and that the secure network file share is \\\ContosoSecureFS\MobilityServiceInstallers.</span></span>

### <a name="step-1-prepare-for-deployment"></a><span data-ttu-id="d9009-118">Шаг 1. Подготовка к развертыванию</span><span class="sxs-lookup"><span data-stu-id="d9009-118">Step 1: Prepare for deployment</span></span>
1. <span data-ttu-id="d9009-119">Создайте в общей сетевой папке каталог с именем **MobSvcWindows**.</span><span class="sxs-lookup"><span data-stu-id="d9009-119">Create a folder on the network share, and name it **MobSvcWindows**.</span></span>
2. <span data-ttu-id="d9009-120">Войдите на сервер конфигурации и откройте административную командную строку.</span><span class="sxs-lookup"><span data-stu-id="d9009-120">Sign in to your configuration server, and open an administrative command prompt.</span></span>
3. <span data-ttu-id="d9009-121">Выполните следующие команды, чтобы создать файл парольной фразы.</span><span class="sxs-lookup"><span data-stu-id="d9009-121">Run the following commands to generate a passphrase file:</span></span>

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. <span data-ttu-id="d9009-122">Скопируйте файл **MobSvc.passphrase** в каталог **MobSvcWindows**, расположенный в общей сетевой папке.</span><span class="sxs-lookup"><span data-stu-id="d9009-122">Copy the **MobSvc.passphrase** file into the **MobSvcWindows** folder on your network share.</span></span>
5. <span data-ttu-id="d9009-123">Перейдите к репозиторию установщика на сервере конфигурации, выполнив такую команду:</span><span class="sxs-lookup"><span data-stu-id="d9009-123">Browse to the installer repository on the configuration server by running the following command:</span></span>

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. <span data-ttu-id="d9009-124">Скопируйте файл **Microsoft-ASR\_UA\_*version*\_Windows\_GA\_*date*\_Release.exe** в каталог **MobSvcWindows**, расположенный в общей сетевой папке.</span><span class="sxs-lookup"><span data-stu-id="d9009-124">Copy the **Microsoft-ASR\_UA\_*version*\_Windows\_GA\_*date*\_Release.exe** to the **MobSvcWindows** folder on your network share.</span></span>
7. <span data-ttu-id="d9009-125">Скопируйте приведенный ниже код в файл и сохраните этот файл с именем **install.bat** в каталоге **MobSvcWindows**.</span><span class="sxs-lookup"><span data-stu-id="d9009-125">Copy the following code, and save it as **install.bat** into the **MobSvcWindows** folder.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d9009-126">Замените в этом скрипте заполнители [CSIP] реальными значениями IP-адреса сервера конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d9009-126">Replace the [CSIP] placeholders in this script with the actual values of the IP address of your configuration server.</span></span>

```DOS
Time /t >> C:\Temp\logfile.log
REM ==================================================
REM ==== Clean up the folders ========================
RMDIR /S /q %temp%\MobSvc
MKDIR %Temp%\MobSvc
MKDIR C:\Temp
REM ==================================================

REM ==== Copy new files ==============================
COPY M*.* %Temp%\MobSvc
CD %Temp%\MobSvc
REN Micro*.exe MobSvcInstaller.exe
REM ==================================================

REM ==== Extract the installer =======================
MobSvcInstaller.exe /q /x:%Temp%\MobSvc\Extracted
REM ==== Wait 10s for extraction to complete =========
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

### <a name="step-2-create-a-package"></a><span data-ttu-id="d9009-127">Шаг 2. Создание пакета</span><span class="sxs-lookup"><span data-stu-id="d9009-127">Step 2: Create a package</span></span>

1. <span data-ttu-id="d9009-128">Войдите в консоль Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="d9009-128">Sign in to your Configuration Manager console.</span></span>
2. <span data-ttu-id="d9009-129">Перейдите к разделу **Библиотека программного обеспечения** > **Управление приложениями** > **Пакеты**.</span><span class="sxs-lookup"><span data-stu-id="d9009-129">Browse to **Software Library** > **Application Management** > **Packages**.</span></span>
3. <span data-ttu-id="d9009-130">Щелкните **Пакеты** правой кнопкой мыши и выберите **Создать пакет**.</span><span class="sxs-lookup"><span data-stu-id="d9009-130">Right-click **Packages**, and select **Create Package**.</span></span>
4. <span data-ttu-id="d9009-131">Введите значения для параметров Имя, Описание, Изготовитель, Язык и Версия.</span><span class="sxs-lookup"><span data-stu-id="d9009-131">Provide values for the name, description, manufacturer, language, and version.</span></span>
5. <span data-ttu-id="d9009-132">Установите флажок **Этот пакет содержит исходные файлы**.</span><span class="sxs-lookup"><span data-stu-id="d9009-132">Select the **This package contains source files** check box.</span></span>
6. <span data-ttu-id="d9009-133">Щелкните **Обзор** и выберите общую сетевую папку, в которой хранится установщик (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows).</span><span class="sxs-lookup"><span data-stu-id="d9009-133">Click **Browse**, and select the network share where the installer is stored (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows).</span></span>

  ![Снимок экрана с мастером создания пакета и программы](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package.png)

7. <span data-ttu-id="d9009-135">На странице **Выберите тип создаваемой программы** выберите **Стандартная программа** и щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="d9009-135">On the **Choose the program type that you want to create** page, select **Standard Program**, and click **Next**.</span></span>

  ![Снимок экрана с мастером создания пакета и программы](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. <span data-ttu-id="d9009-137">На странице **Укажите сведения об этой стандартной программе** предоставьте следующие данные и щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="d9009-137">On the **Specify information about this standard program** page, provide the following inputs, and click **Next**.</span></span> <span data-ttu-id="d9009-138">(Для остальных параметров можно оставить значения по умолчанию.)</span><span class="sxs-lookup"><span data-stu-id="d9009-138">(The other inputs can use their default values.)</span></span>

  | <span data-ttu-id="d9009-139">**Имя параметра**</span><span class="sxs-lookup"><span data-stu-id="d9009-139">**Parameter name**</span></span> | <span data-ttu-id="d9009-140">**Значение**</span><span class="sxs-lookup"><span data-stu-id="d9009-140">**Value**</span></span> |
  |--|--|
  | <span data-ttu-id="d9009-141">Имя</span><span class="sxs-lookup"><span data-stu-id="d9009-141">Name</span></span> | <span data-ttu-id="d9009-142">Установка Microsoft Azure Mobility Service (Windows)</span><span class="sxs-lookup"><span data-stu-id="d9009-142">Install Microsoft Azure Mobility Service (Windows)</span></span> |
  | <span data-ttu-id="d9009-143">Команда</span><span class="sxs-lookup"><span data-stu-id="d9009-143">Command line</span></span> | <span data-ttu-id="d9009-144">install.bat</span><span class="sxs-lookup"><span data-stu-id="d9009-144">install.bat</span></span> |
  | <span data-ttu-id="d9009-145">Программа может запускаться</span><span class="sxs-lookup"><span data-stu-id="d9009-145">Program can run</span></span> | <span data-ttu-id="d9009-146">Независимо от входа пользователя в систему</span><span class="sxs-lookup"><span data-stu-id="d9009-146">Whether or not a user is logged on</span></span> |

  ![Снимок экрана с мастером создания пакета и программы](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties.png)

9. <span data-ttu-id="d9009-148">На следующей странице выберите целевые операционные системы.</span><span class="sxs-lookup"><span data-stu-id="d9009-148">On the next page, select the target operating systems.</span></span> <span data-ttu-id="d9009-149">Mobility Service можно устанавливать только на Windows Server 2012 R2, Windows Server 2012 и Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="d9009-149">Mobility Service can be installed only on Windows Server 2012 R2, Windows Server 2012, and Windows Server 2008 R2.</span></span>

  ![Снимок экрана с мастером создания пакета и программы](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2.png)

10. <span data-ttu-id="d9009-151">Дважды щелкните **Далее**, чтобы завершить работу мастера.</span><span class="sxs-lookup"><span data-stu-id="d9009-151">To complete the wizard, click **Next** twice.</span></span>


> [!NOTE]
> <span data-ttu-id="d9009-152">Скрипт поддерживает как новые установки агентов Mobility Service, так и обновление уже установленных агентов.</span><span class="sxs-lookup"><span data-stu-id="d9009-152">The script supports both new installations of Mobility Service agents and updates to agents that are already installed.</span></span>

### <a name="step-3-deploy-the-package"></a><span data-ttu-id="d9009-153">Шаг 3. Развертывание пакета</span><span class="sxs-lookup"><span data-stu-id="d9009-153">Step 3: Deploy the package</span></span>
1. <span data-ttu-id="d9009-154">В консоли Configuration Manager щелкните пакет правой кнопкой мыши и выберите команду **Распространить содержимое**.</span><span class="sxs-lookup"><span data-stu-id="d9009-154">In the Configuration Manager console, right-click your package, and select **Distribute Content**.</span></span>
  <span data-ttu-id="d9009-155">![Снимок экрана с консолью Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span><span class="sxs-lookup"><span data-stu-id="d9009-155">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span></span>
2. <span data-ttu-id="d9009-156">Выберите **[Точки распространения](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)**, на которые следует скопировать эти пакеты.</span><span class="sxs-lookup"><span data-stu-id="d9009-156">Select the **[distribution points](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** on to which the packages should be copied.</span></span>
3. <span data-ttu-id="d9009-157">Завершите работу мастера.</span><span class="sxs-lookup"><span data-stu-id="d9009-157">Complete the wizard.</span></span> <span data-ttu-id="d9009-158">Теперь пакет будет реплицироваться на выбранные точки распространения.</span><span class="sxs-lookup"><span data-stu-id="d9009-158">The package then starts replicating to the specified distribution points.</span></span>
4. <span data-ttu-id="d9009-159">Когда распространение пакета завершится, щелкните пакет правой кнопкой мыши и выберите **Развернуть**.</span><span class="sxs-lookup"><span data-stu-id="d9009-159">After the package distribution is done, right-click the package, and select **Deploy**.</span></span>
  <span data-ttu-id="d9009-160">![Снимок экрана с консолью Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span><span class="sxs-lookup"><span data-stu-id="d9009-160">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span></span>
5. <span data-ttu-id="d9009-161">Выберите коллекцию устройств Windows Server, созданную на этапе подготовки предварительных требований, в качестве целевой коллекции для развертывания.</span><span class="sxs-lookup"><span data-stu-id="d9009-161">Select the Windows Server device collection you created in the prerequisites section as the target collection for deployment.</span></span>

  ![Снимок экрана с мастером развертывания программного обеспечения](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection.png)

6. <span data-ttu-id="d9009-163">На странице **Укажите места распространения содержимого** выберите нужные **Точки распространения**.</span><span class="sxs-lookup"><span data-stu-id="d9009-163">On the **Specify the content destination** page, select your **Distribution Points**.</span></span>
7. <span data-ttu-id="d9009-164">На странице **Укажите параметры управления процессом развертывания этого программного обеспечения** убедитесь, что выбрана цель **Обязательно**.</span><span class="sxs-lookup"><span data-stu-id="d9009-164">On the **Specify settings to control how this software is deployed** page, ensure that the purpose is **Required**.</span></span>

  ![Снимок экрана с мастером развертывания программного обеспечения](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. <span data-ttu-id="d9009-166">Настройте расписание в разделе **Укажите расписание этого развертывания**.</span><span class="sxs-lookup"><span data-stu-id="d9009-166">On the **Specify the schedule for this deployment** page, specify a schedule.</span></span> <span data-ttu-id="d9009-167">Дополнительные сведения см. в статье [Развертывание пакетов и программ в Configuration Manager](https://technet.microsoft.com/library/gg682178.aspx).</span><span class="sxs-lookup"><span data-stu-id="d9009-167">For more information, see [scheduling packages](https://technet.microsoft.com/library/gg682178.aspx).</span></span>
9. <span data-ttu-id="d9009-168">Настройте свойства на странице **Точки распространения** в соответствии с потребностями вашего центра обработки данных.</span><span class="sxs-lookup"><span data-stu-id="d9009-168">On the **Distribution Points** page, configure the properties according to the needs of your datacenter.</span></span> <span data-ttu-id="d9009-169">Теперь завершите работу мастера.</span><span class="sxs-lookup"><span data-stu-id="d9009-169">Then complete the wizard.</span></span>

> [!TIP]
> <span data-ttu-id="d9009-170">Чтобы избежать лишних перезагрузок, запланируйте установку пакета на период ежемесячного обслуживания или обновления программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="d9009-170">To avoid unnecessary reboots, schedule the package installation during your monthly maintenance window or software updates window.</span></span>

<span data-ttu-id="d9009-171">Ход развертывания можно отслеживать с помощью консоли Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="d9009-171">You can monitor the deployment progress by using the Configuration Manager console.</span></span> <span data-ttu-id="d9009-172">Последовательно выберите пункты **Мониторинг** > **Развертывания** > *[имя пакета]*.</span><span class="sxs-lookup"><span data-stu-id="d9009-172">Go to **Monitoring** > **Deployments** > *[your package name]*.</span></span>

  ![Снимок экрана с настройкой отслеживания расписания в Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/report.PNG)

## <a name="deploy-mobility-service-on-computers-running-linux"></a><span data-ttu-id="d9009-174">Развертывание Mobility Service на компьютерах под управлением Linux</span><span class="sxs-lookup"><span data-stu-id="d9009-174">Deploy Mobility Service on computers running Linux</span></span>
> [!NOTE]
> <span data-ttu-id="d9009-175">В этой статье предполагается, что сервер конфигурации использует IP-адрес 192.168.3.121, а защищенная общая сетевая папка имеет адрес \\\ContosoSecureFS\MobilityServiceInstallers.</span><span class="sxs-lookup"><span data-stu-id="d9009-175">This article assumes that the IP address of the configuration server is 192.168.3.121, and that the secure network file share is \\\ContosoSecureFS\MobilityServiceInstallers.</span></span>

### <a name="step-1-prepare-for-deployment"></a><span data-ttu-id="d9009-176">Шаг 1. Подготовка к развертыванию</span><span class="sxs-lookup"><span data-stu-id="d9009-176">Step 1: Prepare for deployment</span></span>
1. <span data-ttu-id="d9009-177">Создайте в общей сетевой папке каталог с именем **MobSvcLinux**.</span><span class="sxs-lookup"><span data-stu-id="d9009-177">Create a folder on the network share, and name it as **MobSvcLinux**.</span></span>
2. <span data-ttu-id="d9009-178">Войдите на сервер конфигурации и откройте административную командную строку.</span><span class="sxs-lookup"><span data-stu-id="d9009-178">Sign in to your configuration server, and open an administrative command prompt.</span></span>
3. <span data-ttu-id="d9009-179">Выполните следующие команды, чтобы создать файл парольной фразы.</span><span class="sxs-lookup"><span data-stu-id="d9009-179">Run the following commands to generate a passphrase file:</span></span>

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. <span data-ttu-id="d9009-180">Скопируйте файл **MobSvc.passphrase** в каталог **MobSvcLinux**, расположенный в общей сетевой папке.</span><span class="sxs-lookup"><span data-stu-id="d9009-180">Copy the **MobSvc.passphrase** file into the **MobSvcLinux** folder on your network share.</span></span>
5. <span data-ttu-id="d9009-181">Перейдите к репозиторию установщика на сервере конфигурации, выполнив такую команду.</span><span class="sxs-lookup"><span data-stu-id="d9009-181">Browse to the installer repository on the configuration server by running the command:</span></span>

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. <span data-ttu-id="d9009-182">Скопируйте следующие файлы в каталог **MobSvcLinux**, расположенный в общей сетевой папке.</span><span class="sxs-lookup"><span data-stu-id="d9009-182">Copy the following files to the **MobSvcLinux** folder on your network share:</span></span>
   * <span data-ttu-id="d9009-183">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="d9009-183">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span></span>
   * <span data-ttu-id="d9009-184">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="d9009-184">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span></span>
   * <span data-ttu-id="d9009-185">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="d9009-185">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span></span>
   * <span data-ttu-id="d9009-186">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="d9009-186">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span></span>
   * <span data-ttu-id="d9009-187">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="d9009-187">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span></span>
   * <span data-ttu-id="d9009-188">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="d9009-188">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span></span>


7. <span data-ttu-id="d9009-189">Скопируйте приведенный ниже код в файл и сохраните этот файл с именем **install_linux.sh** в каталоге **MobSvcLinux**.</span><span class="sxs-lookup"><span data-stu-id="d9009-189">Copy the following code, and save it as **install_linux.sh** into the **MobSvcLinux** folder.</span></span>
   > [!NOTE]
   > <span data-ttu-id="d9009-190">Замените в этом скрипте заполнители [CSIP] реальными значениями IP-адреса сервера конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d9009-190">Replace the [CSIP] placeholders in this script with the actual values of the IP address of your configuration server.</span></span>

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
        echo "Installation has succeeded. Proceed to configuration." >> /tmp/MobSvc/sccm.log
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
        echo "Agent is already configured. Proceed to Upgrade." >> /tmp/MobSvc/sccm.log
        Upgrade
    else
        echo "Agent is not configured. Proceed to Configure." >> /tmp/MobSvc/sccm.log
        Configure
    fi
else
    Install
fi

cd /tmp

```

### <a name="step-2-create-a-package"></a><span data-ttu-id="d9009-191">Шаг 2. Создание пакета</span><span class="sxs-lookup"><span data-stu-id="d9009-191">Step 2: Create a package</span></span>

1. <span data-ttu-id="d9009-192">Войдите в консоль Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="d9009-192">Sign in  to your Configuration Manager console.</span></span>
2. <span data-ttu-id="d9009-193">Перейдите к разделу **Библиотека программного обеспечения** > **Управление приложениями** > **Пакеты**.</span><span class="sxs-lookup"><span data-stu-id="d9009-193">Browse to **Software Library** > **Application Management** > **Packages**.</span></span>
3. <span data-ttu-id="d9009-194">Щелкните **Пакеты** правой кнопкой мыши и выберите **Создать пакет**.</span><span class="sxs-lookup"><span data-stu-id="d9009-194">Right-click **Packages**, and select **Create Package**.</span></span>
4. <span data-ttu-id="d9009-195">Введите значения для параметров Имя, Описание, Изготовитель, Язык и Версия.</span><span class="sxs-lookup"><span data-stu-id="d9009-195">Provide values for the name, description, manufacturer, language, and version.</span></span>
5. <span data-ttu-id="d9009-196">Установите флажок **Этот пакет содержит исходные файлы**.</span><span class="sxs-lookup"><span data-stu-id="d9009-196">Select the **This package contains source files** check box.</span></span>
6. <span data-ttu-id="d9009-197">Щелкните **Обзор** и выберите общую сетевую папку, в которой хранится установщик (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux).</span><span class="sxs-lookup"><span data-stu-id="d9009-197">Click **Browse**, and select the network share where the installer is stored (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux).</span></span>

  ![Снимок экрана с мастером создания пакета и программы](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package-linux.png)

7. <span data-ttu-id="d9009-199">На странице **Выберите тип создаваемой программы** выберите **Стандартная программа** и щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="d9009-199">On the **Choose the program type that you want to create** page, select **Standard Program**, and click **Next**.</span></span>

  ![Снимок экрана с мастером создания пакета и программы](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. <span data-ttu-id="d9009-201">На странице **Укажите сведения об этой стандартной программе** предоставьте следующие данные и щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="d9009-201">On the **Specify information about this standard program** page, provide the following inputs, and click **Next**.</span></span> <span data-ttu-id="d9009-202">(Для остальных параметров можно оставить значения по умолчанию.)</span><span class="sxs-lookup"><span data-stu-id="d9009-202">(The other inputs can use their default values.)</span></span>

    | <span data-ttu-id="d9009-203">**Имя параметра**</span><span class="sxs-lookup"><span data-stu-id="d9009-203">**Parameter name**</span></span> | <span data-ttu-id="d9009-204">**Значение**</span><span class="sxs-lookup"><span data-stu-id="d9009-204">**Value**</span></span> |
  |--|--|
  | <span data-ttu-id="d9009-205">Имя</span><span class="sxs-lookup"><span data-stu-id="d9009-205">Name</span></span> | <span data-ttu-id="d9009-206">Установка Microsoft Azure Mobility Service (Linux)</span><span class="sxs-lookup"><span data-stu-id="d9009-206">Install Microsoft Azure Mobility Service (Linux)</span></span> |
  | <span data-ttu-id="d9009-207">Команда</span><span class="sxs-lookup"><span data-stu-id="d9009-207">Command line</span></span> | <span data-ttu-id="d9009-208">./install_linux.sh</span><span class="sxs-lookup"><span data-stu-id="d9009-208">./install_linux.sh</span></span> |
  | <span data-ttu-id="d9009-209">Программа может запускаться</span><span class="sxs-lookup"><span data-stu-id="d9009-209">Program can run</span></span> | <span data-ttu-id="d9009-210">Независимо от входа пользователя в систему</span><span class="sxs-lookup"><span data-stu-id="d9009-210">Whether or not a user is logged on</span></span> |

  ![Снимок экрана с мастером создания пакета и программы](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-linux.png)

9. <span data-ttu-id="d9009-212">На следующей странице выберите **Эта программа может запускаться на любой платформе**.</span><span class="sxs-lookup"><span data-stu-id="d9009-212">On the next page, select **This program can run on any platform**.</span></span>
  <span data-ttu-id="d9009-213">![Снимок экрана с мастером создания пакета и программы](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)</span><span class="sxs-lookup"><span data-stu-id="d9009-213">![Screenshot of Create Package and Program wizard](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)</span></span>

10. <span data-ttu-id="d9009-214">Дважды щелкните **Далее**, чтобы завершить работу мастера.</span><span class="sxs-lookup"><span data-stu-id="d9009-214">To complete the wizard, click **Next** twice.</span></span>

> [!NOTE]
> <span data-ttu-id="d9009-215">Скрипт поддерживает как новые установки агентов Mobility Service, так и обновление уже установленных агентов.</span><span class="sxs-lookup"><span data-stu-id="d9009-215">The script supports both new installations of Mobility Service agents and updates to agents that are already installed.</span></span>

### <a name="step-3-deploy-the-package"></a><span data-ttu-id="d9009-216">Шаг 3. Развертывание пакета</span><span class="sxs-lookup"><span data-stu-id="d9009-216">Step 3: Deploy the package</span></span>
1. <span data-ttu-id="d9009-217">В консоли Configuration Manager щелкните пакет правой кнопкой мыши и выберите команду **Распространить содержимое**.</span><span class="sxs-lookup"><span data-stu-id="d9009-217">In the Configuration Manager console, right-click your package, and select **Distribute Content**.</span></span>
  <span data-ttu-id="d9009-218">![Снимок экрана с консолью Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span><span class="sxs-lookup"><span data-stu-id="d9009-218">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span></span>
2. <span data-ttu-id="d9009-219">Выберите **[Точки распространения](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)**, на которые следует скопировать эти пакеты.</span><span class="sxs-lookup"><span data-stu-id="d9009-219">Select the **[distribution points](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** on to which the packages should be copied.</span></span>
3. <span data-ttu-id="d9009-220">Завершите работу мастера.</span><span class="sxs-lookup"><span data-stu-id="d9009-220">Complete the wizard.</span></span> <span data-ttu-id="d9009-221">Теперь пакет будет реплицироваться на выбранные точки распространения.</span><span class="sxs-lookup"><span data-stu-id="d9009-221">The package then starts replicating to the specified distribution points.</span></span>
4. <span data-ttu-id="d9009-222">Когда распространение пакета завершится, щелкните пакет правой кнопкой мыши и выберите **Развернуть**.</span><span class="sxs-lookup"><span data-stu-id="d9009-222">After the package distribution is done, right-click the package, and select **Deploy**.</span></span>
  <span data-ttu-id="d9009-223">![Снимок экрана с консолью Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span><span class="sxs-lookup"><span data-stu-id="d9009-223">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span></span>
5. <span data-ttu-id="d9009-224">Выберите коллекцию устройств Linux Server, созданную на этапе подготовки предварительных требований, в качестве целевой коллекции для развертывания.</span><span class="sxs-lookup"><span data-stu-id="d9009-224">Select the Linux Server device collection you created in the prerequisites section as the target collection for deployment.</span></span>

  ![Снимок экрана с мастером развертывания программного обеспечения](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection-linux.png)

6. <span data-ttu-id="d9009-226">На странице **Укажите места распространения содержимого** выберите нужные **Точки распространения**.</span><span class="sxs-lookup"><span data-stu-id="d9009-226">On the **Specify the content destination** page, select your **Distribution Points**.</span></span>
7. <span data-ttu-id="d9009-227">На странице **Укажите параметры управления процессом развертывания этого программного обеспечения** убедитесь, что выбрана цель **Обязательно**.</span><span class="sxs-lookup"><span data-stu-id="d9009-227">On the **Specify settings to control how this software is deployed** page, ensure that the purpose is **Required**.</span></span>

  ![Снимок экрана с мастером развертывания программного обеспечения](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. <span data-ttu-id="d9009-229">Настройте расписание в разделе **Укажите расписание этого развертывания**.</span><span class="sxs-lookup"><span data-stu-id="d9009-229">On the **Specify the schedule for this deployment** page, specify a schedule.</span></span> <span data-ttu-id="d9009-230">Дополнительные сведения см. в статье [Развертывание пакетов и программ в Configuration Manager](https://technet.microsoft.com/library/gg682178.aspx).</span><span class="sxs-lookup"><span data-stu-id="d9009-230">For more information, see [scheduling packages](https://technet.microsoft.com/library/gg682178.aspx).</span></span>
9. <span data-ttu-id="d9009-231">Настройте свойства на странице **Точки распространения** в соответствии с потребностями вашего центра обработки данных.</span><span class="sxs-lookup"><span data-stu-id="d9009-231">On the **Distribution Points** page, configure the properties according to the needs of your datacenter.</span></span> <span data-ttu-id="d9009-232">Теперь завершите работу мастера.</span><span class="sxs-lookup"><span data-stu-id="d9009-232">Then complete the wizard.</span></span>

<span data-ttu-id="d9009-233">Mobility Service устанавливается в коллекцию устройств Linux Server согласно настроенному расписанию.</span><span class="sxs-lookup"><span data-stu-id="d9009-233">Mobility Service gets installed on the Linux Server Device Collection, according to the schedule you configured.</span></span>

## <a name="other-methods-to-install-mobility-service"></a><span data-ttu-id="d9009-234">Другие методы установки службы Mobility Service</span><span class="sxs-lookup"><span data-stu-id="d9009-234">Other methods to install Mobility Service</span></span>
<span data-ttu-id="d9009-235">Вот еще несколько вариантов действий для установки службы Mobility Service.</span><span class="sxs-lookup"><span data-stu-id="d9009-235">Here are some other options for installing Mobility Service:</span></span>
* [<span data-ttu-id="d9009-236">Ручная установка с использованием графического интерфейса</span><span class="sxs-lookup"><span data-stu-id="d9009-236">Manual Installation using GUI</span></span>](http://aka.ms/mobsvcmanualinstall)
* [<span data-ttu-id="d9009-237">Ручная установка с использованием командной строки</span><span class="sxs-lookup"><span data-stu-id="d9009-237">Manual Installation using command-line</span></span>](http://aka.ms/mobsvcmanualinstallcli)
* [<span data-ttu-id="d9009-238">Принудительная установка с использованием сервера конфигурации</span><span class="sxs-lookup"><span data-stu-id="d9009-238">Push Installation using configuration server </span></span>](http://aka.ms/pushinstall)
* [<span data-ttu-id="d9009-239">Автоматическая установка с использованием службы автоматизации Azure и настройки требуемого состояния</span><span class="sxs-lookup"><span data-stu-id="d9009-239">Automated Installation using Azure Automation & Desired State Configuration </span></span>](http://aka.ms/mobsvcdscinstall)

## <a name="uninstall-mobility-service"></a><span data-ttu-id="d9009-240">Удаление службы Mobility Service</span><span class="sxs-lookup"><span data-stu-id="d9009-240">Uninstall Mobility Service</span></span>
<span data-ttu-id="d9009-241">Вы можете создать пакеты Configuration Manager для удаления службы Mobility Service.</span><span class="sxs-lookup"><span data-stu-id="d9009-241">You can create Configuration Manager packages to uninstall Mobility Service.</span></span> <span data-ttu-id="d9009-242">Для этого выполните следующий скрипт.</span><span class="sxs-lookup"><span data-stu-id="d9009-242">Use the following script to do so:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="d9009-243">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d9009-243">Next steps</span></span>
<span data-ttu-id="d9009-244">Теперь вы можете [включить защиту](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications) для виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="d9009-244">You are now ready to [enable protection](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications) for your virtual machines.</span></span>
