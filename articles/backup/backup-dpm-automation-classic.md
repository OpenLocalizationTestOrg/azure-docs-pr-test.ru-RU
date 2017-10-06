---
title: "Служба архивации Azure: С помощью PowerShell tooback копирование рабочих нагрузок DPM | Документы Microsoft"
description: "Узнайте, как toodeploy и управление резервным копированием Azure для Data Protection Manager (DPM) с помощью PowerShell"
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
ms.openlocfilehash: 48ebe6b520857836e89749ffb6fe83d1f14c5597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-data-protection-manager-dpm-servers-using-powershell"></a><span data-ttu-id="0e2e5-103">Развертывание и управление ими tooAzure резервного копирования для серверов Data Protection Manager (DPM), с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="0e2e5-103">Deploy and manage backup tooAzure for Data Protection Manager (DPM) servers using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0e2e5-104">ARM</span><span class="sxs-lookup"><span data-stu-id="0e2e5-104">ARM</span></span>](backup-dpm-automation.md)
> * [<span data-ttu-id="0e2e5-105">Классический</span><span class="sxs-lookup"><span data-stu-id="0e2e5-105">Classic</span></span>](backup-dpm-automation-classic.md)
>
>

<span data-ttu-id="0e2e5-106">В этой статье объясняется, как toouse PowerShell tooback копирование и восстановление данных DPM из резервного хранилища.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-106">This article explains how toouse PowerShell tooback up and recover DPM data from a backup vault.</span></span> <span data-ttu-id="0e2e5-107">Мы рекомендуем использовать хранилища служб восстановления для всех новых развертываний.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-107">Microsoft recommends using Recovery Services vaults for all new deployments.</span></span> <span data-ttu-id="0e2e5-108">Новый пользователь Azure Backup, с помощью статьи hello [развертывание и управление ими tooAzure данных Data Protection Manager с помощью PowerShell](backup-dpm-automation.md), поэтому при хранении данных в хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-108">If you are a new Azure Backup user, use hello article, [Deploy and manage Data Protection Manager data tooAzure using PowerShell](backup-dpm-automation.md), so you store your data in a Recovery Services vault.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0e2e5-109">Теперь можно обновить вашими хранилищами служб tooRecovery хранилища резервной копии.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-109">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="0e2e5-110">Дополнительные сведения см. в статье hello [обновление tooa хранилища резервной копии, в хранилище служб восстановления](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="0e2e5-110">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="0e2e5-111">Корпорация Майкрософт рекомендует tooupgrade вашей резервных хранилищ tooRecovery хранилищами служб.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-111">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="0e2e5-112">После 15 октября 2017 г. нельзя использовать PowerShell toocreate резервное копирование хранилищ.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-112">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="0e2e5-113">**К 1 ноября 2017 года**:</span><span class="sxs-lookup"><span data-stu-id="0e2e5-113">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="0e2e5-114">Все оставшиеся хранилища резервной копии будет автоматически обновленные tooRecovery хранилищами служб.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-114">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="0e2e5-115">Вы не будет возможности tooaccess данные резервной копии hello классического портала.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-115">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="0e2e5-116">Вместо этого используйте hello Azure портала tooaccess резервного копирования данных в хранилищах службы восстановления.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-116">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="setting-up-hello-powershell-environment"></a><span data-ttu-id="0e2e5-117">Настройка среды PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="0e2e5-117">Setting up hello PowerShell environment</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="0e2e5-118">Прежде чем использовать PowerShell toomanage из резервных копий с tooAzure Data Protection Manager, необходимо будет справа среде toohave hello в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-118">Before you can use PowerShell toomanage backups from Data Protection Manager tooAzure, you will need toohave hello right environment in PowerShell.</span></span> <span data-ttu-id="0e2e5-119">В начале сеанса PowerShell hello hello убедитесь, что запустить hello, следующая команда tooimport hello правой модули и позволяют командлеты DPM hello toocorrectly ссылку:</span><span class="sxs-lookup"><span data-stu-id="0e2e5-119">At hello start of hello PowerShell session, ensure that you run hello following command tooimport hello right modules and allow you toocorrectly reference hello DPM cmdlets:</span></span>

```
PS C:> & "C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin\DpmCliInitScript.ps1"

Welcome toohello DPM Management Shell!

Full list of cmdlets: Get-Command
Only DPM cmdlets: Get-DPMCommand
Get general help: help
Get help for a cmdlet: help <cmdlet-name> or <cmdlet-name> -?
Get definition of a cmdlet: Get-Command <cmdlet-name> -Syntax
Sample DPM scripts: Get-DPMSampleScript
```

## <a name="setup-and-registration"></a><span data-ttu-id="0e2e5-120">Настройка и регистрация</span><span class="sxs-lookup"><span data-stu-id="0e2e5-120">Setup and Registration</span></span>
<span data-ttu-id="0e2e5-121">toobegin:</span><span class="sxs-lookup"><span data-stu-id="0e2e5-121">toobegin:</span></span>

1. <span data-ttu-id="0e2e5-122">[Скачайте последнюю версию PowerShell](https://github.com/Azure/azure-powershell/releases) (минимальная требуемая версия — 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="0e2e5-122">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>
2. <span data-ttu-id="0e2e5-123">Включения командлетов резервного копирования Azure hello переключив слишком*AzureResourceManager* режиме с помощью hello **Switch-AzureMode** командлетов для:</span><span class="sxs-lookup"><span data-stu-id="0e2e5-123">Enable hello Azure Backup commandlets by switching too*AzureResourceManager* mode by using hello **Switch-AzureMode** commandlet:</span></span>

```
PS C:\> Switch-AzureMode AzureResourceManager
```

<span data-ttu-id="0e2e5-124">Hello следующие программы установки и регистрации задачи можно автоматизировать с помощью PowerShell:</span><span class="sxs-lookup"><span data-stu-id="0e2e5-124">hello following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="0e2e5-125">создать хранилище архивации;</span><span class="sxs-lookup"><span data-stu-id="0e2e5-125">Create a backup vault</span></span>
* <span data-ttu-id="0e2e5-126">Установка агента Azure Backup hello</span><span class="sxs-lookup"><span data-stu-id="0e2e5-126">Installing hello Azure Backup agent</span></span>
* <span data-ttu-id="0e2e5-127">Регистрация hello службы архивации Azure</span><span class="sxs-lookup"><span data-stu-id="0e2e5-127">Registering with hello Azure Backup service</span></span>
* <span data-ttu-id="0e2e5-128">Параметры сети</span><span class="sxs-lookup"><span data-stu-id="0e2e5-128">Networking settings</span></span>
* <span data-ttu-id="0e2e5-129">Параметры шифрования</span><span class="sxs-lookup"><span data-stu-id="0e2e5-129">Encryption settings</span></span>

### <a name="create-a-backup-vault"></a><span data-ttu-id="0e2e5-130">создать хранилище архивации;</span><span class="sxs-lookup"><span data-stu-id="0e2e5-130">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="0e2e5-131">Для клиентов, использующих Azure Backup для hello первый раз необходимо использовать с вашей подпиской поставщика toobe tooregister hello Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-131">For customers using Azure Backup for hello first time, you need tooregister hello Azure Backup provider toobe used with your subscription.</span></span> <span data-ttu-id="0e2e5-132">Это можно сделать, выполнив следующую команду hello: Register AzureProvider - ProviderNamespace «Microsoft.Backup»</span><span class="sxs-lookup"><span data-stu-id="0e2e5-132">This can be done by running hello following command: Register-AzureProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="0e2e5-133">Можно создать новое хранилище резервных копий с помощью hello **New AzureRMBackupVault** командлетов для.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-133">You can create a new backup vault using hello **New-AzureRMBackupVault** commandlet.</span></span> <span data-ttu-id="0e2e5-134">резервное хранилище Hello является ресурс ARM, поэтому вам необходимо tooplace его в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-134">hello backup vault is an ARM resource, so you need tooplace it within a Resource Group.</span></span> <span data-ttu-id="0e2e5-135">В консоли Azure PowerShell с повышенными привилегиями выполните hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="0e2e5-135">In an elevated Azure PowerShell console, run hello following commands:</span></span>

```
PS C:\> New-AzureResourceGroup –Name “test-rg” -Region “West US”
PS C:\> $backupvault = New-AzureRMBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GRS
```

<span data-ttu-id="0e2e5-136">Можно получить список всех резервных хранилищ hello в данной подписке с помощью hello **Get AzureRMBackupVault** командлетов для.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-136">You can get a list of all hello backup vaults in a given subscription using hello **Get-AzureRMBackupVault** commandlet.</span></span>

### <a name="installing-hello-azure-backup-agent-on-a-dpm-server"></a><span data-ttu-id="0e2e5-137">Установка агента Azure Backup hello на сервере DPM</span><span class="sxs-lookup"><span data-stu-id="0e2e5-137">Installing hello Azure Backup agent on a DPM Server</span></span>
<span data-ttu-id="0e2e5-138">Перед установкой агента Azure Backup hello загружены и на приветствия Windows Server необходимо toohave hello установщика.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-138">Before you install hello Azure Backup agent, you need toohave hello installer downloaded and present on hello Windows Server.</span></span> <span data-ttu-id="0e2e5-139">Можно получить последнюю версию установщика hello hello hello [центра загрузки Майкрософт](http://aka.ms/azurebackup_agent) или со страницы панели мониторинга резервного хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-139">You can get hello latest version of hello installer from hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from hello backup vault's Dashboard page.</span></span> <span data-ttu-id="0e2e5-140">Сохранить hello установщика tooan легкодоступном месте как * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-140">Save hello installer tooan easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="0e2e5-141">агент hello tooinstall, запустите следующую команду в консоли PowerShell с повышенными hello **на сервере DPM hello**:</span><span class="sxs-lookup"><span data-stu-id="0e2e5-141">tooinstall hello agent, run hello following command in an elevated PowerShell console **on hello DPM server**:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="0e2e5-142">При этом устанавливаются hello агента со всеми параметрами по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-142">This installs hello agent with all hello default options.</span></span> <span data-ttu-id="0e2e5-143">Установка Hello занимает несколько минут в фоновом режиме hello.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-143">hello installation takes a few minutes in hello background.</span></span> <span data-ttu-id="0e2e5-144">Если вы не укажете hello */nu* hello параметр **центра обновления Windows** окно в конце hello hello toocheck установки обновлений.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-144">If you do not specify hello */nu* option hello **Windows Update** window will open at hello end of hello installation toocheck for any updates.</span></span>

<span data-ttu-id="0e2e5-145">Hello агент будет отображаться в списке установленных программ hello.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-145">hello agent will show in hello list of installed programs.</span></span> <span data-ttu-id="0e2e5-146">toosee hello список установленных программ, перейдите в слишком**панели управления** > **программы** > **программы и компоненты**.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-146">toosee hello list of installed programs, go too**Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Агент установлен](./media/backup-dpm-automation/installed-agent-listing.png)

#### <a name="installation-options"></a><span data-ttu-id="0e2e5-148">Параметры установки</span><span class="sxs-lookup"><span data-stu-id="0e2e5-148">Installation options</span></span>
<span data-ttu-id="0e2e5-149">toosee, Здравствуйте, все параметры, доступные через hello командной строки, выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-149">toosee all hello options available via hello command-line, use hello following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="0e2e5-150">Hello доступны следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-150">hello available options include:</span></span>

| <span data-ttu-id="0e2e5-151">Параметр</span><span class="sxs-lookup"><span data-stu-id="0e2e5-151">Option</span></span> | <span data-ttu-id="0e2e5-152">Сведения</span><span class="sxs-lookup"><span data-stu-id="0e2e5-152">Details</span></span> | <span data-ttu-id="0e2e5-153">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="0e2e5-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0e2e5-154">/q</span><span class="sxs-lookup"><span data-stu-id="0e2e5-154">/q</span></span> |<span data-ttu-id="0e2e5-155">Позволяет выполнить тихую установку.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-155">Quiet installation</span></span> |- |
| <span data-ttu-id="0e2e5-156">/p:"расположение"</span><span class="sxs-lookup"><span data-stu-id="0e2e5-156">/p:"location"</span></span> |<span data-ttu-id="0e2e5-157">Путь toohello папку для установки агента Azure Backup hello.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-157">Path toohello installation folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="0e2e5-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="0e2e5-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="0e2e5-159">/s:"расположение"</span><span class="sxs-lookup"><span data-stu-id="0e2e5-159">/s:"location"</span></span> |<span data-ttu-id="0e2e5-160">Путь toohello для папки кэша hello Azure Backup agent.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-160">Path toohello cache folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="0e2e5-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="0e2e5-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="0e2e5-162">/m</span><span class="sxs-lookup"><span data-stu-id="0e2e5-162">/m</span></span> |<span data-ttu-id="0e2e5-163">Участие в tooMicrosoft обновления</span><span class="sxs-lookup"><span data-stu-id="0e2e5-163">Opt-in tooMicrosoft Update</span></span> |- |
| <span data-ttu-id="0e2e5-164">/nu</span><span class="sxs-lookup"><span data-stu-id="0e2e5-164">/nu</span></span> |<span data-ttu-id="0e2e5-165">Позволяет отказаться от проверки наличия обновлений после завершения установки.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-165">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="0e2e5-166">/d</span><span class="sxs-lookup"><span data-stu-id="0e2e5-166">/d</span></span> |<span data-ttu-id="0e2e5-167">Удаляет агент служб восстановления Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-167">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="0e2e5-168">/ph</span><span class="sxs-lookup"><span data-stu-id="0e2e5-168">/ph</span></span> |<span data-ttu-id="0e2e5-169">Адрес узла прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-169">Proxy Host Address</span></span> |- |
| <span data-ttu-id="0e2e5-170">/po</span><span class="sxs-lookup"><span data-stu-id="0e2e5-170">/po</span></span> |<span data-ttu-id="0e2e5-171">Номер порта узла прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-171">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="0e2e5-172">/pu</span><span class="sxs-lookup"><span data-stu-id="0e2e5-172">/pu</span></span> |<span data-ttu-id="0e2e5-173">Имя пользователя узла прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-173">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="0e2e5-174">/pw</span><span class="sxs-lookup"><span data-stu-id="0e2e5-174">/pw</span></span> |<span data-ttu-id="0e2e5-175">Пароль прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-175">Proxy Password</span></span> |- |

### <a name="registering-with-hello-azure-backup-service"></a><span data-ttu-id="0e2e5-176">Регистрация hello службы архивации Azure</span><span class="sxs-lookup"><span data-stu-id="0e2e5-176">Registering with hello Azure Backup service</span></span>
<span data-ttu-id="0e2e5-177">Прежде чем выполнять регистрацию с hello службы архивации Azure, необходимо tooensure, hello [необходимые компоненты](backup-azure-dpm-introduction.md) соблюдены.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-177">Before you can register with hello Azure Backup service, you need tooensure that hello [prerequisites](backup-azure-dpm-introduction.md) are met.</span></span> <span data-ttu-id="0e2e5-178">Необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="0e2e5-178">You must:</span></span>

* <span data-ttu-id="0e2e5-179">Действующая подписка Azure</span><span class="sxs-lookup"><span data-stu-id="0e2e5-179">Have a valid Azure subscription</span></span>
* <span data-ttu-id="0e2e5-180">Хранилище архивов</span><span class="sxs-lookup"><span data-stu-id="0e2e5-180">Have a backup vault</span></span>

<span data-ttu-id="0e2e5-181">toodownload hello учетные данные хранилища, запустите hello **Get AzureBackupVaultCredentials** командлет в консоли Azure PowerShell и хранилище его в удобном расположении, например * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-181">toodownload hello vault credentials, run hello **Get-AzureBackupVaultCredentials** commandlet in an Azure PowerShell console and store it in a convenient location like *C:\Downloads\*.</span></span>

```
PS C:\> $credspath = "C:\"
PS C:\> $credsfilename = Get-AzureRMBackupVaultCredentials -Vault $backupvault -TargetLocation $credspath
PS C:\> $credsfilename
f5303a0b-fae4-4cdb-b44d-0e4c032dde26_backuprg_backuprn_2015-08-11--06-22-35.VaultCredentials
```

<span data-ttu-id="0e2e5-182">Регистрации hello машины с хранилищем hello осуществляется с помощью hello [DPMCloudRegistration начала](https://technet.microsoft.com/library/jj612787) командлета:</span><span class="sxs-lookup"><span data-stu-id="0e2e5-182">Registering hello machine with hello vault is done using hello [Start-DPMCloudRegistration](https://technet.microsoft.com/library/jj612787) cmdlet:</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-DPMCloudRegistration -DPMServerName "TestingServer" -VaultCredentialsFilePath $cred
```

<span data-ttu-id="0e2e5-183">Регистрирует сервер DPM, с именем «TestingServer» hello хранилище Microsoft Azure с помощью hello указанное хранилище учетных данных.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-183">This will register hello DPM Server named “TestingServer” with Microsoft Azure Vault using hello specified vault credentials.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0e2e5-184">Не используйте файл учетных данных хранилища hello toospecify относительные пути.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-184">Do not use relative paths toospecify hello vault credentials file.</span></span> <span data-ttu-id="0e2e5-185">Необходимо указать абсолютный путь в качестве входного toohello командлета.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-185">You must provide an absolute path as an input toohello cmdlet.</span></span>
>
>

### <a name="initial-configuration-settings"></a><span data-ttu-id="0e2e5-186">Исходные параметры конфигурации</span><span class="sxs-lookup"><span data-stu-id="0e2e5-186">Initial configuration settings</span></span>
<span data-ttu-id="0e2e5-187">После hello сервер DPM зарегистрирован hello резервное хранилище, он будет запускаться с параметрами по умолчанию подписки.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-187">Once hello DPM Server is registered with hello Azure Backup vault, it will start with default subscription settings.</span></span> <span data-ttu-id="0e2e5-188">Эти параметры подписки включают сетью, шифрования и hello промежуточной области.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-188">These subscription settings include Networking, Encryption and hello Staging area.</span></span> <span data-ttu-id="0e2e5-189">toobegin изменение hello подписки параметров необходимо toofirst справиться с hello существующие (по умолчанию), параметры с помощью hello [Get DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) командлета:</span><span class="sxs-lookup"><span data-stu-id="0e2e5-189">toobegin changing hello subscription settings you need toofirst get a handle on hello existing (default) settings using hello [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span></span>

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

<span data-ttu-id="0e2e5-190">Локальный объект PowerShell toothis сделанных изменений, которые ```$setting``` и hello полный объект будет зафиксирована tooDPM и резервного копирования Azure toosave их с помощью hello [DPMCloudSubscriptionSetting набор](https://technet.microsoft.com/library/jj612791) командлета.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-190">All modifications are made toothis local PowerShell object ```$setting```  and then hello full object is committed tooDPM and Azure Backup toosave them using hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="0e2e5-191">Требуется toouse hello ```–Commit``` tooensure флаг, который hello изменения сохраняются.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-191">You need toouse hello ```–Commit``` flag tooensure that hello changes are persisted.</span></span> <span data-ttu-id="0e2e5-192">Параметры Hello не будет применяться и используемые резервного копирования Azure, пока не зафиксирована.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-192">hello settings will not be applied and used by Azure Backup unless committed.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

### <a name="networking"></a><span data-ttu-id="0e2e5-193">Сеть</span><span class="sxs-lookup"><span data-stu-id="0e2e5-193">Networking</span></span>
<span data-ttu-id="0e2e5-194">Если подключение hello toohello машины hello DPM служба архивации Azure на hello Интернет через прокси-сервер, параметры прокси-сервера hello должны быть предоставлены для toosucceed резервных копий.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-194">If hello connectivity of hello DPM machine toohello Azure Backup service on hello internet is through a proxy server, then hello proxy server settings should be provided for backups toosucceed.</span></span> <span data-ttu-id="0e2e5-195">Это делается с помощью hello ```-ProxyServer```, ```-ProxyPort```, ```-ProxyUsername``` и hello ```ProxyPassword``` параметры с hello [DPMCloudSubscriptionSetting набор](https://technet.microsoft.com/library/jj612791) командлета.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-195">This is done by using hello ```-ProxyServer```, ```-ProxyPort```, ```-ProxyUsername``` and hello ```ProxyPassword``` parameters with hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="0e2e5-196">В нашем случае прокси-сервер не используется, поэтому мы явным образом удаляем все данные прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-196">In this example, there is no proxy server so we are explicitly clearing any proxy-related information.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

<span data-ttu-id="0e2e5-197">Пропускная способность также можно управлять с помощью параметров ```-WorkHourBandwidth``` и ```-NonWorkHourBandwidth``` для заданного набора дней недели hello.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-197">Bandwidth usage can also be controlled with options of ```-WorkHourBandwidth``` and ```-NonWorkHourBandwidth``` for a given set of days of hello week.</span></span> <span data-ttu-id="0e2e5-198">В данном случае мы не будем настраивать регулирование.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-198">In this example we are not setting any throttling.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

### <a name="configuring-hello-staging-area"></a><span data-ttu-id="0e2e5-199">Настройка hello промежуточной области</span><span class="sxs-lookup"><span data-stu-id="0e2e5-199">Configuring hello staging Area</span></span>
<span data-ttu-id="0e2e5-200">Агент архивации Azure Hello, выполняется на сервере DPM hello должен временное хранилище для данных, восстанавливаемых из облака hello (локальную область промежуточного хранения).</span><span class="sxs-lookup"><span data-stu-id="0e2e5-200">hello Azure Backup agent running on hello DPM server needs temporary storage for data restored from hello cloud (local staging area).</span></span> <span data-ttu-id="0e2e5-201">Настройка hello промежуточной области хранения с помощью hello [набор DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) командлета и hello ```-StagingAreaPath``` параметра.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-201">Configure hello staging area using hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet and hello ```-StagingAreaPath``` parameter.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

<span data-ttu-id="0e2e5-202">В приведенном выше примере hello, hello промежуточной области устанавливается слишком*C:\StagingArea* hello объекта PowerShell ```$setting```.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-202">In hello example above, hello staging area will be set too*C:\StagingArea* in hello PowerShell object ```$setting```.</span></span> <span data-ttu-id="0e2e5-203">Убедитесь, что hello указанная папка уже существует, иначе hello окончательная фиксация параметров подписки hello завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-203">Ensure that hello specified folder already exists, or else hello final commit of hello subscription settings will fail.</span></span>

### <a name="encryption-settings"></a><span data-ttu-id="0e2e5-204">Параметры шифрования</span><span class="sxs-lookup"><span data-stu-id="0e2e5-204">Encryption settings</span></span>
<span data-ttu-id="0e2e5-205">tooAzure Hello резервного копирования данных, отправляемых резервной копии является зашифрованным tooprotect hello конфиденциальность данных hello.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-205">hello backup data sent tooAzure Backup is encrypted tooprotect hello confidentiality of hello data.</span></span> <span data-ttu-id="0e2e5-206">Парольная фраза для шифрования Hello — hello «password» toodecrypt hello данные во время восстановления hello.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-206">hello encryption passphrase is hello "password" toodecrypt hello data at hello time of restore.</span></span> <span data-ttu-id="0e2e5-207">Он tookeep важные безопасный этой информации и защиты после ее установки.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-207">It is important tookeep this information safe and secure once it is set.</span></span>

<span data-ttu-id="0e2e5-208">В следующем примере hello, hello первая команда преобразует строку hello ```passphrase123456789``` tooa безопасной строки и присваивает hello защищенной строки toohello переменную с именем ```$Passphrase```.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-208">In hello example below, hello first command converts hello string ```passphrase123456789``` tooa secure string and assigns hello secure string toohello variable named ```$Passphrase```.</span></span> <span data-ttu-id="0e2e5-209">Вторая команда Hello задает защищенную строку hello в ```$Passphrase``` как hello пароль для шифрования резервных копий.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-209">hello second command sets hello secure string in ```$Passphrase``` as hello password for encrypting backups.</span></span>

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> <span data-ttu-id="0e2e5-210">Обновление сведений парольную фразу hello надежным и безопасным, после ее установки.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-210">Keep hello passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="0e2e5-211">Данные могут toorestore из Azure без этой парольной фразы не будет.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-211">You will not be able toorestore data from Azure without this passphrase.</span></span>
>
>

<span data-ttu-id="0e2e5-212">На этом этапе должны были внесены все необходимые hello изменения toohello ```$setting``` объекта.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-212">At this point, you should have made all hello required changes toohello ```$setting``` object.</span></span> <span data-ttu-id="0e2e5-213">Не забывайте toocommit hello изменения.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-213">Remember toocommit hello changes.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-tooazure-backup"></a><span data-ttu-id="0e2e5-214">Защита данных tooAzure резервной копии</span><span class="sxs-lookup"><span data-stu-id="0e2e5-214">Protect data tooAzure Backup</span></span>
<span data-ttu-id="0e2e5-215">В этом разделе будет добавьте tooDPM производственного сервера и затем включите защиту hello toolocal DPM хранилища данных и затем tooAzure резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-215">In this section, you will add a production server tooDPM and then protect hello data toolocal DPM storage and then tooAzure Backup.</span></span> <span data-ttu-id="0e2e5-216">В примерах hello мы покажем, как tooback копирования файлов и папок.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-216">In hello examples we will demonstrate how tooback up files and folders.</span></span> <span data-ttu-id="0e2e5-217">Hello логику можно легко быть расширенные toobackup любой источник данных, поддерживаемых DPM.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-217">hello logic can easily be extended toobackup any DPM-supported data source.</span></span> <span data-ttu-id="0e2e5-218">Все резервные копии DPM находятся под управлением группы защиты (ГЗ), которая состоит из четырех частей.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-218">All your DPM backups are governed by a Protection Group (PG) with four parts:</span></span>

1. <span data-ttu-id="0e2e5-219">**Членов группы** приведен список все защищаемые объекты hello (также называется *Datasources* в DPM), которые должны tooprotect в hello одной группе защиты.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-219">**Group members** is a list of all hello protectable objects (also known as *Datasources* in DPM) that you want tooprotect in hello same protection group.</span></span> <span data-ttu-id="0e2e5-220">Например можно tooprotect производственный виртуальных машин в одну группу защиты и баз данных SQL Server в другую группу защиты как они могут иметь различные требования для резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-220">For example, you may want tooprotect production VMs in one protection group and SQL Server databases in another protection group as they may have different backup requirements.</span></span> <span data-ttu-id="0e2e5-221">Перед любой источник данных можно архивировать на рабочем сервере необходимо убедиться, что hello toomake агент DPM устанавливается на сервере hello и под управлением DPM.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-221">Before you can back up any datasource on a production server you need toomake sure hello DPM Agent is installed on hello server and is managed by DPM.</span></span> <span data-ttu-id="0e2e5-222">Выполните действия hello для [Установка hello агент DPM](https://technet.microsoft.com/library/bb870935.aspx) , связав ее toohello соответствующие сервера DPM.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-222">Follow hello steps for [installing hello DPM Agent](https://technet.microsoft.com/library/bb870935.aspx) and linking it toohello appropriate DPM Server.</span></span>
2. <span data-ttu-id="0e2e5-223">**Метод защиты данных** указывает hello резервного расположения целей - ленту, диск и облака.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-223">**Data protection method** specifies hello target backup locations - tape, disk, and cloud.</span></span> <span data-ttu-id="0e2e5-224">В нашем примере мы будет защищать данные toohello локального диска и toohello облака.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-224">In our example we will protect data toohello local disk and toohello cloud.</span></span>
3. <span data-ttu-id="0e2e5-225">Объект **расписание резервного копирования** , указывающий при архивы toobe выполнить и как часто hello данные должны быть синхронизированы между hello сервера DPM и hello рабочего сервера.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-225">A **backup schedule** that specifies when backups need toobe taken and how often hello data should be synchronized between hello DPM Server and hello production server.</span></span>
4. <span data-ttu-id="0e2e5-226">Объект **расписание хранения** , указывающее, как долго точки восстановления tooretain hello в Azure.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-226">A **retention schedule** that specifies how long tooretain hello recovery points in Azure.</span></span>

### <a name="creating-a-protection-group"></a><span data-ttu-id="0e2e5-227">Создание группы защиты</span><span class="sxs-lookup"><span data-stu-id="0e2e5-227">Creating a protection group</span></span>
<span data-ttu-id="0e2e5-228">Начните с создания новой группы защиты с помощью hello [New DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) командлета.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-228">Start by creating a new Protection Group using hello [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span></span>

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

<span data-ttu-id="0e2e5-229">Hello выше командлет будет создана группа защиты с именем *ProtectGroup01*.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-229">hello above cmdlet will create a Protection Group named *ProtectGroup01*.</span></span> <span data-ttu-id="0e2e5-230">Можно изменять существующую группу защиты более поздней версии tooadd резервного копирования toohello облако Azure.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-230">An existing protection group can also be modified later tooadd backup toohello Azure cloud.</span></span> <span data-ttu-id="0e2e5-231">Тем не менее toomake любые изменения toohello группа защиты — новые или существующие - мы должны tooget дескриптор на *изменяемой* объекта с помощью hello [Get DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) командлета.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-231">However, toomake any changes toohello Protection Group - new or existing - we need tooget a handle on a *modifiable* object using hello [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span></span>

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-toohello-protection-group"></a><span data-ttu-id="0e2e5-232">Добавление членов группы toohello группы защиты</span><span class="sxs-lookup"><span data-stu-id="0e2e5-232">Adding group members toohello Protection Group</span></span>
<span data-ttu-id="0e2e5-233">Каждый агент DPM знает hello список источников данных на сервере hello, установленной на.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-233">Each DPM Agent knows hello list of datasources on hello server that it is installed on.</span></span> <span data-ttu-id="0e2e5-234">tooadd toohello источник данных группы защиты, hello toofirst потребностей агент DPM Отправить список сервер DPM задней toohello hello источников данных.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-234">tooadd a datasource toohello Protection Group, hello DPM Agent needs toofirst send a list of hello datasources back toohello DPM server.</span></span> <span data-ttu-id="0e2e5-235">Одного или нескольких источников данных, а затем и добавлены toohello группы защиты.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-235">One or more datasources are then selected and added toohello Protection Group.</span></span> <span data-ttu-id="0e2e5-236">шаги, которые необходимы tooget Hello PowerShell достичь указаны:</span><span class="sxs-lookup"><span data-stu-id="0e2e5-236">hello PowerShell steps needed tooget achieve this are:</span></span>

1. <span data-ttu-id="0e2e5-237">Получить список всех серверов, управляемых с помощью DPM с помощью hello агент DPM.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-237">Fetch a list of all servers managed by DPM through hello DPM Agent.</span></span>
2. <span data-ttu-id="0e2e5-238">Выберите определенный сервер.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-238">Choose a specific server.</span></span>
3. <span data-ttu-id="0e2e5-239">Получить список всех источников данных на сервере hello.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-239">Fetch a list of all datasources on hello server.</span></span>
4. <span data-ttu-id="0e2e5-240">Выберите один или несколько источников данных и добавить их toohello группы защиты</span><span class="sxs-lookup"><span data-stu-id="0e2e5-240">Choose one or more datasources and add them toohello Protection Group</span></span>

<span data-ttu-id="0e2e5-241">список серверов, на какие hello агента DPM установлена, а управляется hello сервер DPM Hello приобретается вместе с hello [Get DPMProductionServer](https://technet.microsoft.com/library/hh881600) командлета.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-241">hello list of servers on which hello DPM Agent is installed and is being managed by hello DPM Server is acquired with hello [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span></span> <span data-ttu-id="0e2e5-242">В этом примере мы отфильтруем и настроим для резервного копирования только сервер с именем *productionserver01* .</span><span class="sxs-lookup"><span data-stu-id="0e2e5-242">In this example we will filter and only configure PS with name *productionserver01* for backup.</span></span>

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

<span data-ttu-id="0e2e5-243">Теперь извлечь hello список источников данных на ```$server``` с помощью hello [Get DPMDatasource](https://technet.microsoft.com/library/hh881605) командлета.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-243">Now fetch hello list of datasources on ```$server``` using hello [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span></span> <span data-ttu-id="0e2e5-244">В этом примере мы фильтрации для тома hello * D:\* которой мы хотим tooconfigure для резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-244">In this example we are filtering for hello volume *D:\* which we want tooconfigure for backup.</span></span> <span data-ttu-id="0e2e5-245">Этот источник данных добавляется toohello группы защиты с помощью hello [DPMChildDatasource добавить](https://technet.microsoft.com/library/hh881732) командлета.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-245">This datasource is then added toohello Protection Group using hello [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span></span> <span data-ttu-id="0e2e5-246">Запомнить toouse hello *modifable* объект группы защиты ```$MPG``` toomake hello дополнения.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-246">Remember toouse hello *modifable* protection group object ```$MPG``` toomake hello additions.</span></span>

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

<span data-ttu-id="0e2e5-247">Повторите этот шаг столько раз, по мере необходимости, пока не будут добавлены все hello выбранной группы защиты toohello источники данных.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-247">Repeat this step as many times as required, until you have added all hello chosen datasources toohello protection group.</span></span> <span data-ttu-id="0e2e5-248">Также можно только один источник данных и hello полный рабочий процесс для создания группы защиты hello и позднее добавить несколько источников данных toohello группы защиты.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-248">You can also start with just one datasource, and complete hello workflow for creating hello Protection Group, and at a later point add more datasources toohello Protection Group.</span></span>

### <a name="selecting-hello-data-protection-method"></a><span data-ttu-id="0e2e5-249">Выбор метода защиты данных hello</span><span class="sxs-lookup"><span data-stu-id="0e2e5-249">Selecting hello data protection method</span></span>
<span data-ttu-id="0e2e5-250">После hello источники данных будут добавлены toohello группы защиты, hello следующим шагом является hello с помощью метода защиты hello toospecify [DPMProtectionType набор](https://technet.microsoft.com/library/hh881725) командлета.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-250">Once hello datasources have been added toohello Protection Group, hello next step is toospecify hello protection method using hello [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span></span> <span data-ttu-id="0e2e5-251">В этом примере hello группы защиты будет настроен для локального диска и резервное копирование в облако.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-251">In this example, hello Protection Group will be setup for local disk and cloud backup.</span></span> <span data-ttu-id="0e2e5-252">Необходимо также toospecify hello datasource, необходимо с помощью hello toocloud tooprotect [DPMChildDatasource добавить](https://technet.microsoft.com/library/hh881732.aspx) командлет с флагом - сети.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-252">You also need toospecify hello datasource that you want tooprotect toocloud using hello [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet with -Online flag.</span></span>

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-hello-retention-range"></a><span data-ttu-id="0e2e5-253">Установка диапазона хранения hello</span><span class="sxs-lookup"><span data-stu-id="0e2e5-253">Setting hello retention range</span></span>
<span data-ttu-id="0e2e5-254">Задать политику хранения hello точки hello резервного копирования с помощью hello [DPMPolicyObjective набор](https://technet.microsoft.com/library/hh881762) командлета.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-254">Set hello retention for hello backup points using hello [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span> <span data-ttu-id="0e2e5-255">Хотя может показаться нечетное tooset hello хранения перед расписание резервного копирования hello определен, с помощью hello ```Set-DPMPolicyObjective``` автоматически задает расписание резервного копирования по умолчанию, который затем может быть изменен.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-255">While it might seem odd tooset hello retention before hello backup schedule has been defined, using hello ```Set-DPMPolicyObjective``` cmdlet automatically sets a default backup schedule that can then be modified.</span></span> <span data-ttu-id="0e2e5-256">Он всегда расписание резервного копирования hello возможных tooset сначала и hello политики хранения после.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-256">It is always possible tooset hello backup schedule first and hello retention policy after.</span></span>

<span data-ttu-id="0e2e5-257">В следующем примере hello hello командлет задает параметры хранения hello для резервного копирования на диск.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-257">In hello example below, hello cmdlet sets hello retention parameters for disk backups.</span></span> <span data-ttu-id="0e2e5-258">Это будет хранить архивы 10 дней и синхронизировать данные каждые 6 часов между hello рабочий сервер и сервер DPM hello.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-258">This will retain backups for 10 days, and sync data every 6 hours between hello production server and hello DPM server.</span></span> <span data-ttu-id="0e2e5-259">Hello ```SynchronizationFrequencyMinutes``` не определяет, как часто точки резервного копирования создается, но, как часто данные копируются toohello сервера DPM; это предотвращает чрезмерного увеличения размера резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-259">hello ```SynchronizationFrequencyMinutes``` doesn't define how often a backup point is created, but how often data is copied toohello DPM server; this prevents backups from becoming too large.</span></span>

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

<span data-ttu-id="0e2e5-260">Для резервного копирования будет tooAzure (DPM называется toothese оперативного резервного копирования) hello диапазонов хранения можно настроить для [Долгосрочное хранение с использованием Деда отец ов схемы (GFS)](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="0e2e5-260">For backups going tooAzure (DPM refers toothese as Online backups) hello retention ranges can be configured for [long term retention using a Grandfather-Father-Son scheme (GFS)](backup-azure-backup-cloud-as-tape.md).</span></span> <span data-ttu-id="0e2e5-261">То есть можно определить политику объединенного хранения, включающую политики ежедневного, еженедельного, ежемесячного и ежегодного хранения.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-261">That is, you can define a combined retention policy involving daily, weekly, monthly and yearly retention policies.</span></span> <span data-ttu-id="0e2e5-262">В этом примере мы массив, представляющий схему сложных хранения hello, нам нужно создать, а затем настройте hello диапазон хранения, с помощью hello [DPMPolicyObjective набор](https://technet.microsoft.com/library/hh881762) командлета.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-262">In this example, we create an array representing hello complex retention scheme that we want, and then configure hello retention range using hello [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span>

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-hello-backup-schedule"></a><span data-ttu-id="0e2e5-263">Расписание резервного копирования набор hello</span><span class="sxs-lookup"><span data-stu-id="0e2e5-263">Set hello backup schedule</span></span>
<span data-ttu-id="0e2e5-264">DPM задает расписание резервного копирования по умолчанию автоматически при указании цели защиты hello, с помощью hello ```Set-DPMPolicyObjective``` командлета.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-264">DPM sets a default backup schedule automatically if you specify hello protection objective using hello ```Set-DPMPolicyObjective``` cmdlet.</span></span> <span data-ttu-id="0e2e5-265">расписания по умолчанию hello toochange, использовать hello [Get DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) командлет следуют hello [DPMPolicySchedule набор](https://technet.microsoft.com/library/hh881723) командлета.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-265">toochange hello default schedules, use hello [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet followed by hello [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span></span>

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

<span data-ttu-id="0e2e5-266">В приведенном выше примере hello ```$onlineSch``` является массивом с четырьмя элементами, содержащий hello существующее расписание оперативной защиты для hello группы защиты в схеме GFS hello:</span><span class="sxs-lookup"><span data-stu-id="0e2e5-266">In hello example above, ```$onlineSch``` is an array with four elements that contains hello existing online protection schedule for hello Protection Group in hello GFS scheme:</span></span>

1. <span data-ttu-id="0e2e5-267">```$onlineSch[0]```будет содержать hello ежедневное расписание</span><span class="sxs-lookup"><span data-stu-id="0e2e5-267">```$onlineSch[0]``` will contain hello daily schedule</span></span>
2. <span data-ttu-id="0e2e5-268">```$onlineSch[1]```будет содержать hello еженедельного расписания</span><span class="sxs-lookup"><span data-stu-id="0e2e5-268">```$onlineSch[1]``` will contain hello weekly schedule</span></span>
3. <span data-ttu-id="0e2e5-269">```$onlineSch[2]```будет содержать hello ежемесячного расписания</span><span class="sxs-lookup"><span data-stu-id="0e2e5-269">```$onlineSch[2]``` will contain hello monthly schedule</span></span>
4. <span data-ttu-id="0e2e5-270">```$onlineSch[3]```будет содержать hello годовой расписания</span><span class="sxs-lookup"><span data-stu-id="0e2e5-270">```$onlineSch[3]``` will contain hello yearly schedule</span></span>

<span data-ttu-id="0e2e5-271">Поэтому если вам требуется toomodify hello Еженедельное расписание, toorefer toohello ```$onlineSch[1]```.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-271">So if you need toomodify hello weekly schedule, you need toorefer toohello ```$onlineSch[1]```.</span></span>

### <a name="initial-backup"></a><span data-ttu-id="0e2e5-272">Начальное резервное копирование</span><span class="sxs-lookup"><span data-stu-id="0e2e5-272">Initial backup</span></span>
<span data-ttu-id="0e2e5-273">При резервном копировании datasource для hello впервые, DPM требуется toocreate начальной реплики, которая создаст копию защищенных toobe datasource hello на томе реплики DPM.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-273">When backing up a datasource for hello first time, DPM needs toocreate an initial replica which will create a copy of hello datasource toobe protected on DPM replica volume.</span></span> <span data-ttu-id="0e2e5-274">Это действие может быть запланированной на определенное время или можно запустить вручную, используя hello [набор DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) командлет с параметром hello ```-NOW```.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-274">This activity can either be scheduled for a specific time, or can be triggered manually, using hello [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet with hello parameter ```-NOW```.</span></span>

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-hello-size-of-dpm-replica--recovery-point-volume"></a><span data-ttu-id="0e2e5-275">Изменение размера hello реплики DPM и тома точек восстановления</span><span class="sxs-lookup"><span data-stu-id="0e2e5-275">Changing hello size of DPM Replica & recovery point volume</span></span>
<span data-ttu-id="0e2e5-276">Можно также изменить размер тома реплики DPM, а также использование теневого копирования тома hello [DPMDatasourceDiskAllocation набор](https://technet.microsoft.com/library/hh881618.aspx) командлет как hello в следующем примере: Get-DatasourceDiskAllocation - Datasource $DS SET-DatasourceDiskAllocation - Datasource $DS - ProtectionGroup $MPG-вручную - ReplicaArea (2 ГБ) — ShadowCopyArea (2 ГБ)</span><span class="sxs-lookup"><span data-stu-id="0e2e5-276">You can also change hello size of DPM Replica volume as well as Shadow Copy volume using [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet as in hello below example: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span></span>

### <a name="committing-hello-changes-toohello-protection-group"></a><span data-ttu-id="0e2e5-277">Фиксация hello изменяет toohello группы защиты</span><span class="sxs-lookup"><span data-stu-id="0e2e5-277">Committing hello changes toohello Protection Group</span></span>
<span data-ttu-id="0e2e5-278">Наконец hello изменения должны toobe, зафиксированные до DPM можно использовать резервную копию hello каждой новой конфигурации группы защиты hello.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-278">Finally, hello changes need toobe committed before DPM can take hello backup per hello new Protection Group configuration.</span></span> <span data-ttu-id="0e2e5-279">Это делается с помощью hello [DPMProtectionGroup набор](https://technet.microsoft.com/library/hh881758) командлета.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-279">This is done using hello [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span></span>

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-hello-backup-points"></a><span data-ttu-id="0e2e5-280">Просматривать hello резервного копирования точки</span><span class="sxs-lookup"><span data-stu-id="0e2e5-280">View hello backup points</span></span>
<span data-ttu-id="0e2e5-281">Можно использовать hello [Get DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) tooget командлет список всех точек восстановления для источника данных.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-281">You can use hello [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet tooget a list of all recovery points for a datasource.</span></span> <span data-ttu-id="0e2e5-282">В этом примере мы:</span><span class="sxs-lookup"><span data-stu-id="0e2e5-282">In this example, we will:</span></span>

* <span data-ttu-id="0e2e5-283">извлечь все PGs hello на сервере DPM hello, который будет сохранен в виде массива```$PG```</span><span class="sxs-lookup"><span data-stu-id="0e2e5-283">fetch all hello PGs on hello DPM server which will be stored in an array ```$PG```</span></span>
* <span data-ttu-id="0e2e5-284">получить соответствующий toohello hello источников данных```$PG[0]```</span><span class="sxs-lookup"><span data-stu-id="0e2e5-284">get hello datasources corresponding toohello ```$PG[0]```</span></span>
* <span data-ttu-id="0e2e5-285">Получите все hello точки восстановления для источника данных.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-285">get all hello recovery points for a datasource.</span></span>

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a><span data-ttu-id="0e2e5-286">Восстановление данных, защищенных в Azure</span><span class="sxs-lookup"><span data-stu-id="0e2e5-286">Restore data protected on Azure</span></span>
<span data-ttu-id="0e2e5-287">Восстановление данных представляет собой сочетание объектов ```RecoverableItem``` и ```RecoveryOption```.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-287">Restoring data is a combination of a ```RecoverableItem``` object and a ```RecoveryOption``` object.</span></span> <span data-ttu-id="0e2e5-288">В предыдущем разделе hello нас есть список точек hello резервного копирования для источника данных.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-288">In hello previous section, we got a list of hello backup points for a datasource.</span></span>

<span data-ttu-id="0e2e5-289">В следующем примере hello демонстрируют, как toorestore Hyper-V виртуальной машины из резервного копирования Azure точками объединение резервного копирования с hello целевого объекта для восстановления.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-289">In hello example below, we demonstrate how toorestore a Hyper-V virtual machine from Azure Backup by combining backup points with hello target for recovery.</span></span> <span data-ttu-id="0e2e5-290">А именно:</span><span class="sxs-lookup"><span data-stu-id="0e2e5-290">This includes:</span></span>

* <span data-ttu-id="0e2e5-291">Создание параметра восстановления, используя hello [New DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) командлета.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-291">Creating a recovery option using hello  [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span></span>
* <span data-ttu-id="0e2e5-292">Извлечение hello массивом точек резервного копирования, с помощью hello ```Get-DPMRecoveryPoint``` командлета.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-292">Fetching hello array of backup points using hello ```Get-DPMRecoveryPoint``` cmdlet.</span></span>
* <span data-ttu-id="0e2e5-293">Выбор резервного копирования toorestore точки из.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-293">Choosing a backup point toorestore from.</span></span>

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

<span data-ttu-id="0e2e5-294">Hello команды можно легко расширить для любого типа источника данных.</span><span class="sxs-lookup"><span data-stu-id="0e2e5-294">hello commands can easily be extended for any datasource type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e2e5-295">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0e2e5-295">Next steps</span></span>
* <span data-ttu-id="0e2e5-296">Дополнительные сведения о службе архивации Azure для DPM в разделе [tooDPM введение резервного копирования](backup-azure-dpm-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="0e2e5-296">For more information about Azure Backup for DPM see [Introduction tooDPM Backup](backup-azure-dpm-introduction.md)</span></span>
