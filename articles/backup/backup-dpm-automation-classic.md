---
title: "Служба архивации Azure: использование PowerShell для архивации рабочих нагрузок DPM | Документация Майкрософт"
description: "Узнайте о том, как развернуть службу архивации Azure для Data Protection Manager (DPM) и управлять ей с помощью PowerShell"
services: backup
documentationcenter: 
author: Nkolli1
manager: shreeshd
editor: 
ms.assetid: bcbcef79-9d33-4e84-a558-9866614f2cae
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: nkolli;trinadhk;anuragm;markgal
ms.openlocfilehash: 943a12dcba49a114d206b9dab968da332ea99926
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-and-manage-backup-to-azure-for-data-protection-manager-dpm-servers-using-powershell"></a><span data-ttu-id="47e18-103">Развертывание резервного копирования в Azure для серверов Data Protection Manager (DPM) и управление им с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="47e18-103">Deploy and manage backup to Azure for Data Protection Manager (DPM) servers using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="47e18-104">ARM</span><span class="sxs-lookup"><span data-stu-id="47e18-104">ARM</span></span>](backup-dpm-automation.md)
> * [<span data-ttu-id="47e18-105">Классический</span><span class="sxs-lookup"><span data-stu-id="47e18-105">Classic</span></span>](backup-dpm-automation-classic.md)
>
>

<span data-ttu-id="47e18-106">В этой статье объясняется, как создавать резервные копии и восстанавливать данные DPM из хранилища резервных копий с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="47e18-106">This article explains how to use PowerShell to back up and recover DPM data from a backup vault.</span></span> <span data-ttu-id="47e18-107">Мы рекомендуем использовать хранилища служб восстановления для всех новых развертываний.</span><span class="sxs-lookup"><span data-stu-id="47e18-107">Microsoft recommends using Recovery Services vaults for all new deployments.</span></span> <span data-ttu-id="47e18-108">Если вы только приступили к работе со службой Azure Backup, ознакомьтесь со статьей [Развертывание резервного копирования в Azure для серверов Data Protection Manager (DPM) и управление им с помощью PowerShell](backup-dpm-automation.md), чтобы узнать, как хранить данные в хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="47e18-108">If you are a new Azure Backup user, use the article, [Deploy and manage Data Protection Manager data to Azure using PowerShell](backup-dpm-automation.md), so you store your data in a Recovery Services vault.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="47e18-109">Теперь вы можете обновить свои резервные хранилища до хранилищ служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="47e18-109">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="47e18-110">См. дополнительные сведения об [обновлении резервного хранилища до хранилища служб восстановления](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="47e18-110">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="47e18-111">Корпорация Майкрософт рекомендует обновить резервные хранилища до хранилищ служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="47e18-111">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="47e18-112">После 15 октября 2017 года вы не сможете использовать PowerShell для создания резервных хранилищ.</span><span class="sxs-lookup"><span data-stu-id="47e18-112">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="47e18-113">**К 1 ноября 2017 года**:</span><span class="sxs-lookup"><span data-stu-id="47e18-113">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="47e18-114">Все остальные резервные хранилища будут автоматически обновлены до хранилищ служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="47e18-114">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="47e18-115">Вы не сможете получить доступ к данным резервных копий на классическом портале.</span><span class="sxs-lookup"><span data-stu-id="47e18-115">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="47e18-116">Вместо этого для доступа к данным резервных копий в хранилищах служб восстановления используйте портал Azure.</span><span class="sxs-lookup"><span data-stu-id="47e18-116">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="setting-up-the-powershell-environment"></a><span data-ttu-id="47e18-117">Настройка среды PowerShell</span><span class="sxs-lookup"><span data-stu-id="47e18-117">Setting up the PowerShell environment</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="47e18-118">Прежде чем использовать PowerShell для управления резервными копиями Data Protection Manager в Azure, необходимо создать подходящую среду в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="47e18-118">Before you can use PowerShell to manage backups from Data Protection Manager to Azure, you will need to have the right environment in PowerShell.</span></span> <span data-ttu-id="47e18-119">В начале сеанса PowerShell обязательно выполните следующую команду для импорта необходимых модулей, которая также позволяет правильно ссылаться на командлеты DPM:</span><span class="sxs-lookup"><span data-stu-id="47e18-119">At the start of the PowerShell session, ensure that you run the following command to import the right modules and allow you to correctly reference the DPM cmdlets:</span></span>

```
PS C:> & "C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin\DpmCliInitScript.ps1"

Welcome to the DPM Management Shell!

Full list of cmdlets: Get-Command
Only DPM cmdlets: Get-DPMCommand
Get general help: help
Get help for a cmdlet: help <cmdlet-name> or <cmdlet-name> -?
Get definition of a cmdlet: Get-Command <cmdlet-name> -Syntax
Sample DPM scripts: Get-DPMSampleScript
```

## <a name="setup-and-registration"></a><span data-ttu-id="47e18-120">Настройка и регистрация</span><span class="sxs-lookup"><span data-stu-id="47e18-120">Setup and Registration</span></span>
<span data-ttu-id="47e18-121">Чтобы начать работу, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="47e18-121">To begin:</span></span>

1. <span data-ttu-id="47e18-122">[Скачайте последнюю версию PowerShell](https://github.com/Azure/azure-powershell/releases) (минимальная требуемая версия — 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="47e18-122">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>
2. <span data-ttu-id="47e18-123">Включите командлеты службы архивации Azure. Для этого перейдите в режим *AzureResourceManager* с помощью командлета **Switch-AzureMode**.</span><span class="sxs-lookup"><span data-stu-id="47e18-123">Enable the Azure Backup commandlets by switching to *AzureResourceManager* mode by using the **Switch-AzureMode** commandlet:</span></span>

```
PS C:\> Switch-AzureMode AzureResourceManager
```

<span data-ttu-id="47e18-124">С помощью PowerShell можно автоматизировать указанные ниже задачи по настройке и регистрации.</span><span class="sxs-lookup"><span data-stu-id="47e18-124">The following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="47e18-125">создать хранилище архивации;</span><span class="sxs-lookup"><span data-stu-id="47e18-125">Create a backup vault</span></span>
* <span data-ttu-id="47e18-126">Установка агента службы архивации Azure.</span><span class="sxs-lookup"><span data-stu-id="47e18-126">Installing the Azure Backup agent</span></span>
* <span data-ttu-id="47e18-127">Регистрация в службе архивации Azure</span><span class="sxs-lookup"><span data-stu-id="47e18-127">Registering with the Azure Backup service</span></span>
* <span data-ttu-id="47e18-128">Параметры сети</span><span class="sxs-lookup"><span data-stu-id="47e18-128">Networking settings</span></span>
* <span data-ttu-id="47e18-129">Параметры шифрования</span><span class="sxs-lookup"><span data-stu-id="47e18-129">Encryption settings</span></span>

### <a name="create-a-backup-vault"></a><span data-ttu-id="47e18-130">создать хранилище архивации;</span><span class="sxs-lookup"><span data-stu-id="47e18-130">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="47e18-131">Для клиентов, использующих службу архивации Azure впервые, необходимо зарегистрировать поставщика службы архивации для использования с вашей подпиской.</span><span class="sxs-lookup"><span data-stu-id="47e18-131">For customers using Azure Backup for the first time, you need to register the Azure Backup provider to be used with your subscription.</span></span> <span data-ttu-id="47e18-132">Для этого выполните следующую команду: Register-AzureProvider -ProviderNamespace "Microsoft.Backup"</span><span class="sxs-lookup"><span data-stu-id="47e18-132">This can be done by running the following command: Register-AzureProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="47e18-133">Вы можете создать новое хранилище архивации с помощью командлета **New-AzureRMBackupVault** .</span><span class="sxs-lookup"><span data-stu-id="47e18-133">You can create a new backup vault using the **New-AzureRMBackupVault** commandlet.</span></span> <span data-ttu-id="47e18-134">Хранилище архивов представляет собой ресурс ARM, поэтому вам потребуется разместить его в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="47e18-134">The backup vault is an ARM resource, so you need to place it within a Resource Group.</span></span> <span data-ttu-id="47e18-135">В консоли Azure PowerShell с повышенными привилегиями выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="47e18-135">In an elevated Azure PowerShell console, run the following commands:</span></span>

```
PS C:\> New-AzureResourceGroup –Name “test-rg” -Region “West US”
PS C:\> $backupvault = New-AzureRMBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GRS
```

<span data-ttu-id="47e18-136">Чтобы получить список всех хранилищ архивации в данной подписке, используйте командлет **Get-AzureRMBackupVault** .</span><span class="sxs-lookup"><span data-stu-id="47e18-136">You can get a list of all the backup vaults in a given subscription using the **Get-AzureRMBackupVault** commandlet.</span></span>

### <a name="installing-the-azure-backup-agent-on-a-dpm-server"></a><span data-ttu-id="47e18-137">Установка агента службы архивации Azure на сервер DPM</span><span class="sxs-lookup"><span data-stu-id="47e18-137">Installing the Azure Backup agent on a DPM Server</span></span>
<span data-ttu-id="47e18-138">Прежде чем устанавливать агент службы архивации Azure, необходимо загрузить установщик и разместить его в системе Windows Server.</span><span class="sxs-lookup"><span data-stu-id="47e18-138">Before you install the Azure Backup agent, you need to have the installer downloaded and present on the Windows Server.</span></span> <span data-ttu-id="47e18-139">Последнюю версию установщика можно загрузить в [центре загрузки Майкрософт](http://aka.ms/azurebackup_agent) или на странице панели мониторинга хранилища архивов.</span><span class="sxs-lookup"><span data-stu-id="47e18-139">You can get the latest version of the installer from the [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from the backup vault's Dashboard page.</span></span> <span data-ttu-id="47e18-140">Сохраните установщик в удобном для вас месте, например в папке *C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="47e18-140">Save the installer to an easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="47e18-141">Чтобы установить агент, в консоли PowerShell с повышенными привилегиями **на сервере DPM**выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="47e18-141">To install the agent, run the following command in an elevated PowerShell console **on the DPM server**:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="47e18-142">Агент будет установлен с параметрами по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="47e18-142">This installs the agent with all the default options.</span></span> <span data-ttu-id="47e18-143">Установка займет всего несколько минут и пройдет в фоновом режиме.</span><span class="sxs-lookup"><span data-stu-id="47e18-143">The installation takes a few minutes in the background.</span></span> <span data-ttu-id="47e18-144">Если параметр */nu* не будет указан, в конце установки откроется окно **Обновления Windows** для проверки наличия обновлений.</span><span class="sxs-lookup"><span data-stu-id="47e18-144">If you do not specify the */nu* option the **Windows Update** window will open at the end of the installation to check for any updates.</span></span>

<span data-ttu-id="47e18-145">Агент появится в списке установленных программ.</span><span class="sxs-lookup"><span data-stu-id="47e18-145">The agent will show in the list of installed programs.</span></span> <span data-ttu-id="47e18-146">Чтобы просмотреть список установленных программ, выберите **Панель управления** > **Программы** > **Программы и компоненты**.</span><span class="sxs-lookup"><span data-stu-id="47e18-146">To see the list of installed programs, go to **Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Агент установлен](./media/backup-dpm-automation/installed-agent-listing.png)

#### <a name="installation-options"></a><span data-ttu-id="47e18-148">Параметры установки</span><span class="sxs-lookup"><span data-stu-id="47e18-148">Installation options</span></span>
<span data-ttu-id="47e18-149">Чтобы просмотреть все доступные в командной строке параметры, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="47e18-149">To see all the options available via the command-line, use the following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="47e18-150">Доступны следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="47e18-150">The available options include:</span></span>

| <span data-ttu-id="47e18-151">Параметр</span><span class="sxs-lookup"><span data-stu-id="47e18-151">Option</span></span> | <span data-ttu-id="47e18-152">Сведения</span><span class="sxs-lookup"><span data-stu-id="47e18-152">Details</span></span> | <span data-ttu-id="47e18-153">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="47e18-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="47e18-154">/q</span><span class="sxs-lookup"><span data-stu-id="47e18-154">/q</span></span> |<span data-ttu-id="47e18-155">Позволяет выполнить тихую установку.</span><span class="sxs-lookup"><span data-stu-id="47e18-155">Quiet installation</span></span> |- |
| <span data-ttu-id="47e18-156">/p:"расположение"</span><span class="sxs-lookup"><span data-stu-id="47e18-156">/p:"location"</span></span> |<span data-ttu-id="47e18-157">Путь к папке установки для агента архивации Azure.</span><span class="sxs-lookup"><span data-stu-id="47e18-157">Path to the installation folder for the Azure Backup agent.</span></span> |<span data-ttu-id="47e18-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="47e18-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="47e18-159">/s:"расположение"</span><span class="sxs-lookup"><span data-stu-id="47e18-159">/s:"location"</span></span> |<span data-ttu-id="47e18-160">Путь к папке кэша для агента архивации Azure.</span><span class="sxs-lookup"><span data-stu-id="47e18-160">Path to the cache folder for the Azure Backup agent.</span></span> |<span data-ttu-id="47e18-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="47e18-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="47e18-162">/m</span><span class="sxs-lookup"><span data-stu-id="47e18-162">/m</span></span> |<span data-ttu-id="47e18-163">Позволяет явно согласиться на использование Центра обновления Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="47e18-163">Opt-in to Microsoft Update</span></span> |- |
| <span data-ttu-id="47e18-164">/nu</span><span class="sxs-lookup"><span data-stu-id="47e18-164">/nu</span></span> |<span data-ttu-id="47e18-165">Позволяет отказаться от проверки наличия обновлений после завершения установки.</span><span class="sxs-lookup"><span data-stu-id="47e18-165">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="47e18-166">/d</span><span class="sxs-lookup"><span data-stu-id="47e18-166">/d</span></span> |<span data-ttu-id="47e18-167">Удаляет агент служб восстановления Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="47e18-167">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="47e18-168">/ph</span><span class="sxs-lookup"><span data-stu-id="47e18-168">/ph</span></span> |<span data-ttu-id="47e18-169">Адрес узла прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="47e18-169">Proxy Host Address</span></span> |- |
| <span data-ttu-id="47e18-170">/po</span><span class="sxs-lookup"><span data-stu-id="47e18-170">/po</span></span> |<span data-ttu-id="47e18-171">Номер порта узла прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="47e18-171">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="47e18-172">/pu</span><span class="sxs-lookup"><span data-stu-id="47e18-172">/pu</span></span> |<span data-ttu-id="47e18-173">Имя пользователя узла прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="47e18-173">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="47e18-174">/pw</span><span class="sxs-lookup"><span data-stu-id="47e18-174">/pw</span></span> |<span data-ttu-id="47e18-175">Пароль прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="47e18-175">Proxy Password</span></span> |- |

### <a name="registering-with-the-azure-backup-service"></a><span data-ttu-id="47e18-176">Регистрация в службе архивации Azure</span><span class="sxs-lookup"><span data-stu-id="47e18-176">Registering with the Azure Backup service</span></span>
<span data-ttu-id="47e18-177">Перед регистрацией в службе резервного копирования Azure убедитесь, что соблюдены [необходимые условия](backup-azure-dpm-introduction.md) .</span><span class="sxs-lookup"><span data-stu-id="47e18-177">Before you can register with the Azure Backup service, you need to ensure that the [prerequisites](backup-azure-dpm-introduction.md) are met.</span></span> <span data-ttu-id="47e18-178">Необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="47e18-178">You must:</span></span>

* <span data-ttu-id="47e18-179">Действующая подписка Azure</span><span class="sxs-lookup"><span data-stu-id="47e18-179">Have a valid Azure subscription</span></span>
* <span data-ttu-id="47e18-180">Хранилище архивов</span><span class="sxs-lookup"><span data-stu-id="47e18-180">Have a backup vault</span></span>

<span data-ttu-id="47e18-181">Чтобы скачать учетные данные хранилища, выполните командлет **Get-AzureBackupVaultCredentials** в консоли Azure PowerShell и сохраните их в удобном месте, например в папке *C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="47e18-181">To download the vault credentials, run the **Get-AzureBackupVaultCredentials** commandlet in an Azure PowerShell console and store it in a convenient location like *C:\Downloads\*.</span></span>

```
PS C:\> $credspath = "C:\"
PS C:\> $credsfilename = Get-AzureRMBackupVaultCredentials -Vault $backupvault -TargetLocation $credspath
PS C:\> $credsfilename
f5303a0b-fae4-4cdb-b44d-0e4c032dde26_backuprg_backuprn_2015-08-11--06-22-35.VaultCredentials
```

<span data-ttu-id="47e18-182">Регистрация компьютера в хранилище выполняется с помощью командлета [Start-DPMCloudRegistration](https://technet.microsoft.com/library/jj612787) :</span><span class="sxs-lookup"><span data-stu-id="47e18-182">Registering the machine with the vault is done using the [Start-DPMCloudRegistration](https://technet.microsoft.com/library/jj612787) cmdlet:</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-DPMCloudRegistration -DPMServerName "TestingServer" -VaultCredentialsFilePath $cred
```

<span data-ttu-id="47e18-183">Как видно, сервер с именем "TestingServer" регистрируется в хранилище Microsoft Azure на основании указанных учетных данных хранилища.</span><span class="sxs-lookup"><span data-stu-id="47e18-183">This will register the DPM Server named “TestingServer” with Microsoft Azure Vault using the specified vault credentials.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="47e18-184">Не используйте относительные пути для указания файла с учетными данными хранилища.</span><span class="sxs-lookup"><span data-stu-id="47e18-184">Do not use relative paths to specify the vault credentials file.</span></span> <span data-ttu-id="47e18-185">Укажите абсолютный путь в качестве входных данных командлета.</span><span class="sxs-lookup"><span data-stu-id="47e18-185">You must provide an absolute path as an input to the cmdlet.</span></span>
>
>

### <a name="initial-configuration-settings"></a><span data-ttu-id="47e18-186">Исходные параметры конфигурации</span><span class="sxs-lookup"><span data-stu-id="47e18-186">Initial configuration settings</span></span>
<span data-ttu-id="47e18-187">После регистрации сервера DPM в хранилище службы архивации Azure он будет запущен с параметрами подписки, используемыми по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="47e18-187">Once the DPM Server is registered with the Azure Backup vault, it will start with default subscription settings.</span></span> <span data-ttu-id="47e18-188">Эти параметры подписки включают настройки сети, шифрования и промежуточной области.</span><span class="sxs-lookup"><span data-stu-id="47e18-188">These subscription settings include Networking, Encryption and the Staging area.</span></span> <span data-ttu-id="47e18-189">Чтобы приступить к изменению параметров подписки, сначала получите дескриптор существующих параметров (по умолчанию) с помощью командлета [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) .</span><span class="sxs-lookup"><span data-stu-id="47e18-189">To begin changing the subscription settings you need to first get a handle on the existing (default) settings using the [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span></span>

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

<span data-ttu-id="47e18-190">Все изменения вносятся в этот локальный объект PowerShell ```$setting```, а затем полный объект фиксируется в DPM и службе архивации Azure с помощью командлета [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791). Таким образом он сохраняется.</span><span class="sxs-lookup"><span data-stu-id="47e18-190">All modifications are made to this local PowerShell object ```$setting```  and then the full object is committed to DPM and Azure Backup to save them using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="47e18-191">Чтобы гарантировать, что изменения будут сохранены, необходимо использовать флаг ```–Commit```.</span><span class="sxs-lookup"><span data-stu-id="47e18-191">You need to use the ```–Commit``` flag to ensure that the changes are persisted.</span></span> <span data-ttu-id="47e18-192">Параметры не будут применяться и использоваться службой архивации Azure до тех пор, пока они не будут зафиксированы.</span><span class="sxs-lookup"><span data-stu-id="47e18-192">The settings will not be applied and used by Azure Backup unless committed.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

### <a name="networking"></a><span data-ttu-id="47e18-193">Сеть</span><span class="sxs-lookup"><span data-stu-id="47e18-193">Networking</span></span>
<span data-ttu-id="47e18-194">Если компьютер DPM подключен к службе архивации Azure в Интернете через прокси-сервер, то для успешного резервного копирования следует указать параметры прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="47e18-194">If the connectivity of the DPM machine to the Azure Backup service on the internet is through a proxy server, then the proxy server settings should be provided for backups to succeed.</span></span> <span data-ttu-id="47e18-195">Для этого используются параметры ```-ProxyServer```, ```-ProxyPort```, ```-ProxyUsername``` и ```ProxyPassword``` для командлета [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791).</span><span class="sxs-lookup"><span data-stu-id="47e18-195">This is done by using the ```-ProxyServer```, ```-ProxyPort```, ```-ProxyUsername``` and the ```ProxyPassword``` parameters with the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="47e18-196">В нашем случае прокси-сервер не используется, поэтому мы явным образом удаляем все данные прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="47e18-196">In this example, there is no proxy server so we are explicitly clearing any proxy-related information.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

<span data-ttu-id="47e18-197">Управлять использованием пропускной способности для выбранных дней недели можно с помощью параметров ```-WorkHourBandwidth``` и ```-NonWorkHourBandwidth``` </span><span class="sxs-lookup"><span data-stu-id="47e18-197">Bandwidth usage can also be controlled with options of ```-WorkHourBandwidth``` and ```-NonWorkHourBandwidth``` for a given set of days of the week.</span></span> <span data-ttu-id="47e18-198">В данном случае мы не будем настраивать регулирование.</span><span class="sxs-lookup"><span data-stu-id="47e18-198">In this example we are not setting any throttling.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

### <a name="configuring-the-staging-area"></a><span data-ttu-id="47e18-199">Настройка промежуточной области</span><span class="sxs-lookup"><span data-stu-id="47e18-199">Configuring the staging Area</span></span>
<span data-ttu-id="47e18-200">Для агента службы архивации Azure, работающего на сервере DPM, необходимо предоставить временное хранилище для восстановленных из облака данных (локальная промежуточная область).</span><span class="sxs-lookup"><span data-stu-id="47e18-200">The Azure Backup agent running on the DPM server needs temporary storage for data restored from the cloud (local staging area).</span></span> <span data-ttu-id="47e18-201">Настройте промежуточную область с помощью командлета [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) с параметром ```-StagingAreaPath```.</span><span class="sxs-lookup"><span data-stu-id="47e18-201">Configure the staging area using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet and the ```-StagingAreaPath``` parameter.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

<span data-ttu-id="47e18-202">В примере выше задается промежуточная область *C:\StagingArea* в объекте PowerShell ```$setting```.</span><span class="sxs-lookup"><span data-stu-id="47e18-202">In the example above, the staging area will be set to *C:\StagingArea* in the PowerShell object ```$setting```.</span></span> <span data-ttu-id="47e18-203">Убедитесь, что указанная папка уже существует, иначе финальная фиксация параметров подписки завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="47e18-203">Ensure that the specified folder already exists, or else the final commit of the subscription settings will fail.</span></span>

### <a name="encryption-settings"></a><span data-ttu-id="47e18-204">Параметры шифрования</span><span class="sxs-lookup"><span data-stu-id="47e18-204">Encryption settings</span></span>
<span data-ttu-id="47e18-205">Для защиты конфиденциальности данных резервные копии данных, отправляемые в службу архивации Azure, зашифровываются.</span><span class="sxs-lookup"><span data-stu-id="47e18-205">The backup data sent to Azure Backup is encrypted to protect the confidentiality of the data.</span></span> <span data-ttu-id="47e18-206">Используемая для шифрования парольная фраза является "паролем" для расшифровки данных во время их восстановления.</span><span class="sxs-lookup"><span data-stu-id="47e18-206">The encryption passphrase is the "password" to decrypt the data at the time of restore.</span></span> <span data-ttu-id="47e18-207">После создания фразы надежно сохраните ее и никому не сообщайте о ней.</span><span class="sxs-lookup"><span data-stu-id="47e18-207">It is important to keep this information safe and secure once it is set.</span></span>

<span data-ttu-id="47e18-208">В следующем примере первая команда преобразует строку ```passphrase123456789``` в защищенную строку и присваивает ее переменной ```$Passphrase```.</span><span class="sxs-lookup"><span data-stu-id="47e18-208">In the example below, the first command converts the string ```passphrase123456789``` to a secure string and assigns the secure string to the variable named ```$Passphrase```.</span></span> <span data-ttu-id="47e18-209">Вторая команда задает защищенную строку в ```$Passphrase``` в качестве пароля для шифрования резервных копий.</span><span class="sxs-lookup"><span data-stu-id="47e18-209">the second command sets the secure string in ```$Passphrase``` as the password for encrypting backups.</span></span>

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> <span data-ttu-id="47e18-210">После создания парольной фразы надежно сохраните ее и никому не сообщайте о ней.</span><span class="sxs-lookup"><span data-stu-id="47e18-210">Keep the passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="47e18-211">Восстановить данные из Azure без парольной фразы невозможно.</span><span class="sxs-lookup"><span data-stu-id="47e18-211">You will not be able to restore data from Azure without this passphrase.</span></span>
>
>

<span data-ttu-id="47e18-212">На этом этапе следует внести все необходимые изменения в объект ```$setting``` .</span><span class="sxs-lookup"><span data-stu-id="47e18-212">At this point, you should have made all the required changes to the ```$setting``` object.</span></span> <span data-ttu-id="47e18-213">Не забудьте зафиксировать изменения.</span><span class="sxs-lookup"><span data-stu-id="47e18-213">Remember to commit the changes.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-to-azure-backup"></a><span data-ttu-id="47e18-214">Защита данных в службе архивации Azure</span><span class="sxs-lookup"><span data-stu-id="47e18-214">Protect data to Azure Backup</span></span>
<span data-ttu-id="47e18-215">В этом разделе мы добавим рабочий сервер в DPM, а затем включим защиту данных в локальном хранилище DPM и службе архивации Azure.</span><span class="sxs-lookup"><span data-stu-id="47e18-215">In this section, you will add a production server to DPM and then protect the data to local DPM storage and then to Azure Backup.</span></span> <span data-ttu-id="47e18-216">С помощью примеров мы покажем, как создавать резервные копии файлов и папок.</span><span class="sxs-lookup"><span data-stu-id="47e18-216">In the examples we will demonstrate how to back up files and folders.</span></span> <span data-ttu-id="47e18-217">Таким же способом можно создавать резервные копии любых поддерживаемых DPM источников данных.</span><span class="sxs-lookup"><span data-stu-id="47e18-217">The logic can easily be extended to backup any DPM-supported data source.</span></span> <span data-ttu-id="47e18-218">Все резервные копии DPM находятся под управлением группы защиты (ГЗ), которая состоит из четырех частей.</span><span class="sxs-lookup"><span data-stu-id="47e18-218">All your DPM backups are governed by a Protection Group (PG) with four parts:</span></span>

1. <span data-ttu-id="47e18-219">**Члены группы защиты** — это список всех защищаемых объектов (также называемых *источниками данных* в DPM), которые вы хотите защитить в рамках одной группы защиты.</span><span class="sxs-lookup"><span data-stu-id="47e18-219">**Group members** is a list of all the protectable objects (also known as *Datasources* in DPM) that you want to protect in the same protection group.</span></span> <span data-ttu-id="47e18-220">Например, вы можете защитить рабочие виртуальные машины в одной группе защиты, а базы данных SQL Server — в другой группе защиты, так как у них могут быть разные требования к резервному копированию.</span><span class="sxs-lookup"><span data-stu-id="47e18-220">For example, you may want to protect production VMs in one protection group and SQL Server databases in another protection group as they may have different backup requirements.</span></span> <span data-ttu-id="47e18-221">Перед созданием резервных копий данных на рабочем сервере убедитесь, что на рабочем сервере установлен агент DPM, который управляется с помощью DPM.</span><span class="sxs-lookup"><span data-stu-id="47e18-221">Before you can back up any datasource on a production server you need to make sure the DPM Agent is installed on the server and is managed by DPM.</span></span> <span data-ttu-id="47e18-222">Выполните шаги по [установке агента DPM](https://technet.microsoft.com/library/bb870935.aspx) и связыванию его с соответствующим сервером DPM.</span><span class="sxs-lookup"><span data-stu-id="47e18-222">Follow the steps for [installing the DPM Agent](https://technet.microsoft.com/library/bb870935.aspx) and linking it to the appropriate DPM Server.</span></span>
2. <span data-ttu-id="47e18-223">**Метод защиты данных** — определяет расположения резервных копий (магнитная лента, диск и облако).</span><span class="sxs-lookup"><span data-stu-id="47e18-223">**Data protection method** specifies the target backup locations - tape, disk, and cloud.</span></span> <span data-ttu-id="47e18-224">В нашем примере мы организуем защиту данных на локальный диск и в облако.</span><span class="sxs-lookup"><span data-stu-id="47e18-224">In our example we will protect data to the local disk and to the cloud.</span></span>
3. <span data-ttu-id="47e18-225">**Расписание резервного копирования** — указывает, когда необходимо выполнять резервное копирование и как часто следует синхронизировать данные между сервером DPM и рабочим сервером.</span><span class="sxs-lookup"><span data-stu-id="47e18-225">A **backup schedule** that specifies when backups need to be taken and how often the data should be synchronized between the DPM Server and the production server.</span></span>
4. <span data-ttu-id="47e18-226">**Расписание хранения** — определяет период хранения точек восстановления в Azure.</span><span class="sxs-lookup"><span data-stu-id="47e18-226">A **retention schedule** that specifies how long to retain the recovery points in Azure.</span></span>

### <a name="creating-a-protection-group"></a><span data-ttu-id="47e18-227">Создание группы защиты</span><span class="sxs-lookup"><span data-stu-id="47e18-227">Creating a protection group</span></span>
<span data-ttu-id="47e18-228">Начните с создания новой группы защиты с помощью командлета [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) .</span><span class="sxs-lookup"><span data-stu-id="47e18-228">Start by creating a new Protection Group using the [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span></span>

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

<span data-ttu-id="47e18-229">Указанный выше командлет создает группу защиты с именем *ProtectGroup01*.</span><span class="sxs-lookup"><span data-stu-id="47e18-229">The above cmdlet will create a Protection Group named *ProtectGroup01*.</span></span> <span data-ttu-id="47e18-230">Существующую группу защиты можно изменить позднее, чтобы добавить резервную копию в облако Azure.</span><span class="sxs-lookup"><span data-stu-id="47e18-230">An existing protection group can also be modified later to add backup to the Azure cloud.</span></span> <span data-ttu-id="47e18-231">Тем не менее, чтобы получить возможность вносить изменения в группу защиты (новую или существующую), необходимо получить дескриптор *изменяемого* объекта с помощью командлета [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) .</span><span class="sxs-lookup"><span data-stu-id="47e18-231">However, to make any changes to the Protection Group - new or existing - we need to get a handle on a *modifiable* object using the [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span></span>

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-to-the-protection-group"></a><span data-ttu-id="47e18-232">Добавление членов группы в группу защиты</span><span class="sxs-lookup"><span data-stu-id="47e18-232">Adding group members to the Protection Group</span></span>
<span data-ttu-id="47e18-233">Каждому агенту DPM известен список источников данных на сервере, на котором он установлен.</span><span class="sxs-lookup"><span data-stu-id="47e18-233">Each DPM Agent knows the list of datasources on the server that it is installed on.</span></span> <span data-ttu-id="47e18-234">Чтобы добавить источник данных в группу защиты, агент DPM должен сначала отправить список источников данных обратно на сервер DPM.</span><span class="sxs-lookup"><span data-stu-id="47e18-234">To add a datasource to the Protection Group, the DPM Agent needs to first send a list of the datasources back to the DPM server.</span></span> <span data-ttu-id="47e18-235">Затем выбирается один или несколько источников данных, которые добавляются в группу защиты.</span><span class="sxs-lookup"><span data-stu-id="47e18-235">One or more datasources are then selected and added to the Protection Group.</span></span> <span data-ttu-id="47e18-236">Ниже представлены действия, которые необходимо выполнить в PowerShell, чтобы добавить членов группы в группу защиты.</span><span class="sxs-lookup"><span data-stu-id="47e18-236">The PowerShell steps needed to get achieve this are:</span></span>

1. <span data-ttu-id="47e18-237">Получите список всех серверов, управляемых DPM через агент DPM.</span><span class="sxs-lookup"><span data-stu-id="47e18-237">Fetch a list of all servers managed by DPM through the DPM Agent.</span></span>
2. <span data-ttu-id="47e18-238">Выберите определенный сервер.</span><span class="sxs-lookup"><span data-stu-id="47e18-238">Choose a specific server.</span></span>
3. <span data-ttu-id="47e18-239">Получите список всех источников данных на сервере.</span><span class="sxs-lookup"><span data-stu-id="47e18-239">Fetch a list of all datasources on the server.</span></span>
4. <span data-ttu-id="47e18-240">Выберите один или несколько источников данных и добавьте их в группу защиты.</span><span class="sxs-lookup"><span data-stu-id="47e18-240">Choose one or more datasources and add them to the Protection Group</span></span>

<span data-ttu-id="47e18-241">Чтобы получить список серверов, на которых установлен агент DPM и которые управляются сервером DPM, воспользуйтесь командлетом [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) .</span><span class="sxs-lookup"><span data-stu-id="47e18-241">The list of servers on which the DPM Agent is installed and is being managed by the DPM Server is acquired with the [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span></span> <span data-ttu-id="47e18-242">В этом примере мы отфильтруем и настроим для резервного копирования только сервер с именем *productionserver01* .</span><span class="sxs-lookup"><span data-stu-id="47e18-242">In this example we will filter and only configure PS with name *productionserver01* for backup.</span></span>

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

<span data-ttu-id="47e18-243">Теперь получим список источников данных на ```$server``` с помощью командлета [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605).</span><span class="sxs-lookup"><span data-stu-id="47e18-243">Now fetch the list of datasources on ```$server``` using the [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span></span> <span data-ttu-id="47e18-244">В этом примере мы применяем фильтрацию для тома *D:\*, который нужно настроить для резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="47e18-244">In this example we are filtering for the volume *D:\* which we want to configure for backup.</span></span> <span data-ttu-id="47e18-245">Затем этот источник данных добавляется в группу защиты с помощью командлета [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732).</span><span class="sxs-lookup"><span data-stu-id="47e18-245">This datasource is then added to the Protection Group using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span></span> <span data-ttu-id="47e18-246">Не забывайте использовать *изменяемый* объект группы защиты ```$MPG```, чтобы вносить дополнения.</span><span class="sxs-lookup"><span data-stu-id="47e18-246">Remember to use the *modifable* protection group object ```$MPG``` to make the additions.</span></span>

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

<span data-ttu-id="47e18-247">При необходимости повторите этот шаг несколько раз, пока все выбранные источники данных не будут добавлены в группу защиты.</span><span class="sxs-lookup"><span data-stu-id="47e18-247">Repeat this step as many times as required, until you have added all the chosen datasources to the protection group.</span></span> <span data-ttu-id="47e18-248">Для начала можно выполнить рабочий процесс создания группы защиты только для одного источника данных, а затем позже добавить в эту группу дополнительные источники данных.</span><span class="sxs-lookup"><span data-stu-id="47e18-248">You can also start with just one datasource, and complete the workflow for creating the Protection Group, and at a later point add more datasources to the Protection Group.</span></span>

### <a name="selecting-the-data-protection-method"></a><span data-ttu-id="47e18-249">Выбор способа защиты данных</span><span class="sxs-lookup"><span data-stu-id="47e18-249">Selecting the data protection method</span></span>
<span data-ttu-id="47e18-250">После добавления в группу защиты источников данных необходимо указать метод защиты, воспользовавшись для этого командлетом [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) .</span><span class="sxs-lookup"><span data-stu-id="47e18-250">Once the datasources have been added to the Protection Group, the next step is to specify the protection method using the [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span></span> <span data-ttu-id="47e18-251">В этом примере группа защиты будет настроена для резервного копирования на локальный диск и в облако.</span><span class="sxs-lookup"><span data-stu-id="47e18-251">In this example, the Protection Group will be setup for local disk and cloud backup.</span></span> <span data-ttu-id="47e18-252">Необходимо также с помощью командлета [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) с флагом -Online указать источник данных, который нужно защитить в облаке.</span><span class="sxs-lookup"><span data-stu-id="47e18-252">You also need to specify the datasource that you want to protect to cloud using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet with -Online flag.</span></span>

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-the-retention-range"></a><span data-ttu-id="47e18-253">Настройка диапазона хранения</span><span class="sxs-lookup"><span data-stu-id="47e18-253">Setting the retention range</span></span>
<span data-ttu-id="47e18-254">Задайте период хранения для точек резервного копирования с помощью командлета [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) .</span><span class="sxs-lookup"><span data-stu-id="47e18-254">Set the retention for the backup points using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span> <span data-ttu-id="47e18-255">Несмотря на то что задание периода хранения до определения расписания резервного копирования может показаться странным, командлет ```Set-DPMPolicyObjective``` автоматически задает расписание резервного копирования по умолчанию, которое в последствии можно изменить.</span><span class="sxs-lookup"><span data-stu-id="47e18-255">While it might seem odd to set the retention before the backup schedule has been defined, using the ```Set-DPMPolicyObjective``` cmdlet automatically sets a default backup schedule that can then be modified.</span></span> <span data-ttu-id="47e18-256">Вы всегда можете сначала определить расписание резервного копирования, а затем задать политику хранения.</span><span class="sxs-lookup"><span data-stu-id="47e18-256">It is always possible to set the backup schedule first and the retention policy after.</span></span>

<span data-ttu-id="47e18-257">В примере ниже командлет задает параметры хранения для резервного копирования на диск.</span><span class="sxs-lookup"><span data-stu-id="47e18-257">In the example below, the cmdlet sets the retention parameters for disk backups.</span></span> <span data-ttu-id="47e18-258">Резервные копии будут храниться 10 дней, а данные будут синхронизироваться между рабочим сервером и сервером DPM каждые 6 часов.</span><span class="sxs-lookup"><span data-stu-id="47e18-258">This will retain backups for 10 days, and sync data every 6 hours between the production server and the DPM server.</span></span> <span data-ttu-id="47e18-259">```SynchronizationFrequencyMinutes``` определяет не частоту создания точек резервного копирования, а то, как часто данные копируются на сервер DPM; это предотвращает создание резервных копий слишком большого размера.</span><span class="sxs-lookup"><span data-stu-id="47e18-259">The ```SynchronizationFrequencyMinutes``` doesn't define how often a backup point is created, but how often data is copied to the DPM server; this prevents backups from becoming too large.</span></span>

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

<span data-ttu-id="47e18-260">Для резервных копий, сохраняемых в Azure (в DPM это называется Online Backup), диапазоны хранения можно настроить для [долгосрочное хранение с использованием трехуровневой схемы (GFS)](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="47e18-260">For backups going to Azure (DPM refers to these as Online backups) the retention ranges can be configured for [long term retention using a Grandfather-Father-Son scheme (GFS)](backup-azure-backup-cloud-as-tape.md).</span></span> <span data-ttu-id="47e18-261">То есть можно определить политику объединенного хранения, включающую политики ежедневного, еженедельного, ежемесячного и ежегодного хранения.</span><span class="sxs-lookup"><span data-stu-id="47e18-261">That is, you can define a combined retention policy involving daily, weekly, monthly and yearly retention policies.</span></span> <span data-ttu-id="47e18-262">В этом примере мы создаем массив, представляющий сложную схему хранения, которая нам необходима, а затем настраиваем диапазон хранения с помощью командлета [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) .</span><span class="sxs-lookup"><span data-stu-id="47e18-262">In this example, we create an array representing the complex retention scheme that we want, and then configure the retention range using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span>

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-the-backup-schedule"></a><span data-ttu-id="47e18-263">Настройка расписания резервного копирования</span><span class="sxs-lookup"><span data-stu-id="47e18-263">Set the backup schedule</span></span>
<span data-ttu-id="47e18-264">При указании цели защиты с помощью командлета ```Set-DPMPolicyObjective``` DPM автоматически задаст расписание резервного копирования по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="47e18-264">DPM sets a default backup schedule automatically if you specify the protection objective using the ```Set-DPMPolicyObjective``` cmdlet.</span></span> <span data-ttu-id="47e18-265">Для изменения расписания по умолчанию используйте командлет [Get DPMPolicySchedule](https://technet.microsoft.com/library/hh881749), а затем командлет [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723).</span><span class="sxs-lookup"><span data-stu-id="47e18-265">To change the default schedules, use the [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet followed by the [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span></span>

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

<span data-ttu-id="47e18-266">В приведенном выше примере ```$onlineSch``` является массивом с четырьмя элементами, содержащий существующее расписание оперативной защиты для группы защиты в схеме GFS:</span><span class="sxs-lookup"><span data-stu-id="47e18-266">In the example above, ```$onlineSch``` is an array with four elements that contains the existing online protection schedule for the Protection Group in the GFS scheme:</span></span>

1. <span data-ttu-id="47e18-267">```$onlineSch[0]``` будет содержать ежедневное расписание</span><span class="sxs-lookup"><span data-stu-id="47e18-267">```$onlineSch[0]``` will contain the daily schedule</span></span>
2. <span data-ttu-id="47e18-268">```$onlineSch[1]``` будет содержать еженедельное расписание</span><span class="sxs-lookup"><span data-stu-id="47e18-268">```$onlineSch[1]``` will contain the weekly schedule</span></span>
3. <span data-ttu-id="47e18-269">```$onlineSch[2]``` будет содержать ежемесячное расписание</span><span class="sxs-lookup"><span data-stu-id="47e18-269">```$onlineSch[2]``` will contain the monthly schedule</span></span>
4. <span data-ttu-id="47e18-270">```$onlineSch[3]``` будет содержать ежегодное расписание</span><span class="sxs-lookup"><span data-stu-id="47e18-270">```$onlineSch[3]``` will contain the yearly schedule</span></span>

<span data-ttu-id="47e18-271">Поэтому если необходимо изменить еженедельное расписание, необходимо ссылаться на ```$onlineSch[1]```.</span><span class="sxs-lookup"><span data-stu-id="47e18-271">So if you need to modify the weekly schedule, you need to refer to the ```$onlineSch[1]```.</span></span>

### <a name="initial-backup"></a><span data-ttu-id="47e18-272">Начальное резервное копирование</span><span class="sxs-lookup"><span data-stu-id="47e18-272">Initial backup</span></span>
<span data-ttu-id="47e18-273">Если вы создаете резервные копии источника данных впервые, DPM создаст исходную реплику, которая создаст в томе реплики DPM копию защищаемого источника данных.</span><span class="sxs-lookup"><span data-stu-id="47e18-273">When backing up a datasource for the first time, DPM needs to create an initial replica which will create a copy of the datasource to be protected on DPM replica volume.</span></span> <span data-ttu-id="47e18-274">Это действие можно запланировать на определенное время или выполнить вручную с помощью командлета [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) с параметром ```-NOW```.</span><span class="sxs-lookup"><span data-stu-id="47e18-274">This activity can either be scheduled for a specific time, or can be triggered manually, using the [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet with the parameter ```-NOW```.</span></span>

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-the-size-of-dpm-replica--recovery-point-volume"></a><span data-ttu-id="47e18-275">Изменение размера реплики DPM и тома точек восстановления</span><span class="sxs-lookup"><span data-stu-id="47e18-275">Changing the size of DPM Replica & recovery point volume</span></span>
<span data-ttu-id="47e18-276">Также можно изменить размер тома реплики DPM и тома теневых копий с помощью командлета [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) , как показано в следующем примере: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span><span class="sxs-lookup"><span data-stu-id="47e18-276">You can also change the size of DPM Replica volume as well as Shadow Copy volume using [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet as in the below example: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span></span>

### <a name="committing-the-changes-to-the-protection-group"></a><span data-ttu-id="47e18-277">Фиксация изменений в группу защиты</span><span class="sxs-lookup"><span data-stu-id="47e18-277">Committing the changes to the Protection Group</span></span>
<span data-ttu-id="47e18-278">Наконец, необходимо зафиксировать изменения до того, как DPM выполнит резервное копирование в соответствии с новой конфигурацией группы защиты.</span><span class="sxs-lookup"><span data-stu-id="47e18-278">Finally, the changes need to be committed before DPM can take the backup per the new Protection Group configuration.</span></span> <span data-ttu-id="47e18-279">Для этого воспользуйтесь командлетом [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) .</span><span class="sxs-lookup"><span data-stu-id="47e18-279">This is done using the [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span></span>

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-the-backup-points"></a><span data-ttu-id="47e18-280">Просмотр точек резервного копирования</span><span class="sxs-lookup"><span data-stu-id="47e18-280">View the backup points</span></span>
<span data-ttu-id="47e18-281">Чтобы получить список всех точек восстановления для источника данных, можно использовать командлет [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) .</span><span class="sxs-lookup"><span data-stu-id="47e18-281">You can use the [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet to get a list of all recovery points for a datasource.</span></span> <span data-ttu-id="47e18-282">В этом примере мы:</span><span class="sxs-lookup"><span data-stu-id="47e18-282">In this example, we will:</span></span>

* <span data-ttu-id="47e18-283">отправим данные из всех групп защиты на сервер DPM; данные будут храниться в массиве ```$PG```</span><span class="sxs-lookup"><span data-stu-id="47e18-283">fetch all the PGs on the DPM server which will be stored in an array ```$PG```</span></span>
* <span data-ttu-id="47e18-284">получим источники данных, соответствующие ```$PG[0]```</span><span class="sxs-lookup"><span data-stu-id="47e18-284">get the datasources corresponding to the ```$PG[0]```</span></span>
* <span data-ttu-id="47e18-285">получим все точки восстановления для источника данных.</span><span class="sxs-lookup"><span data-stu-id="47e18-285">get all the recovery points for a datasource.</span></span>

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a><span data-ttu-id="47e18-286">Восстановление данных, защищенных в Azure</span><span class="sxs-lookup"><span data-stu-id="47e18-286">Restore data protected on Azure</span></span>
<span data-ttu-id="47e18-287">Восстановление данных представляет собой сочетание объектов ```RecoverableItem``` и ```RecoveryOption```.</span><span class="sxs-lookup"><span data-stu-id="47e18-287">Restoring data is a combination of a ```RecoverableItem``` object and a ```RecoveryOption``` object.</span></span> <span data-ttu-id="47e18-288">В предыдущем разделе мы получили список точек резервного копирования для источника данных.</span><span class="sxs-lookup"><span data-stu-id="47e18-288">In the previous section, we got a list of the backup points for a datasource.</span></span>

<span data-ttu-id="47e18-289">В примере ниже демонстрируется восстановление виртуальной машины Hyper-V из службы архивации Azure путем объединения резервных точек с целевым объектом для восстановления.</span><span class="sxs-lookup"><span data-stu-id="47e18-289">In the example below, we demonstrate how to restore a Hyper-V virtual machine from Azure Backup by combining backup points with the target for recovery.</span></span> <span data-ttu-id="47e18-290">А именно:</span><span class="sxs-lookup"><span data-stu-id="47e18-290">This includes:</span></span>

* <span data-ttu-id="47e18-291">Создадим параметр восстановления, используя командлет [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592).</span><span class="sxs-lookup"><span data-stu-id="47e18-291">Creating a recovery option using the  [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span></span>
* <span data-ttu-id="47e18-292">Выполним выборку массива точек резервного копирования с помощью командлета ```Get-DPMRecoveryPoint``` .</span><span class="sxs-lookup"><span data-stu-id="47e18-292">Fetching the array of backup points using the ```Get-DPMRecoveryPoint``` cmdlet.</span></span>
* <span data-ttu-id="47e18-293">Выберем точку резервного копирования для восстановления.</span><span class="sxs-lookup"><span data-stu-id="47e18-293">Choosing a backup point to restore from.</span></span>

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

<span data-ttu-id="47e18-294">Команды можно с легкостью расширить для любого типа источника данных.</span><span class="sxs-lookup"><span data-stu-id="47e18-294">The commands can easily be extended for any datasource type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="47e18-295">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="47e18-295">Next steps</span></span>
* <span data-ttu-id="47e18-296">Дополнительные сведения о службе архивации Azure для DPM см. в разделе [Введение в службу архивации DPM](backup-azure-dpm-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="47e18-296">For more information about Azure Backup for DPM see [Introduction to DPM Backup](backup-azure-dpm-introduction.md)</span></span>
