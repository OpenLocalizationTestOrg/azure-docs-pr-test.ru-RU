---
title: "aaaUse PowerShell toomanage Windows Server резервных копий в Azure | Документы Microsoft"
description: "Развертывание резервных копий Windows Server и управление ими с помощью PowerShell."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: e7e269e2-1f11-41a9-957b-a2155de6a1e0
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: saurse;markgal;nkolli;trinadhk
ms.openlocfilehash: 72292e510b0f059102440bd49a195be4ef700a6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-windows-serverwindows-client-using-powershell"></a><span data-ttu-id="7d4f0-103">Развертывание и управление ими tooAzure резервного копирования для клиента Windows Server и Windows с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="7d4f0-103">Deploy and manage backup tooAzure for Windows Server/Windows Client using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7d4f0-104">ARM</span><span class="sxs-lookup"><span data-stu-id="7d4f0-104">ARM</span></span>](backup-client-automation.md)
> * [<span data-ttu-id="7d4f0-105">Классический</span><span class="sxs-lookup"><span data-stu-id="7d4f0-105">Classic</span></span>](backup-client-automation-classic.md)
>
>

<span data-ttu-id="7d4f0-106">В этой статье объясняется, как хранилище резервного копирования toouse tooback PowerShell Windows Server или tooa данные рабочей станции Windows.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-106">This article explains how toouse PowerShell tooback up Windows Server or Windows workstation data tooa backup vault.</span></span> <span data-ttu-id="7d4f0-107">Мы рекомендуем использовать хранилища служб восстановления для всех новых развертываний.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-107">Microsoft recommends using Recovery Services vaults for all new deployments.</span></span> <span data-ttu-id="7d4f0-108">Если новый пользователь резервного копирования Azure и не созданы резервного хранилища в подписке, используйте статьи hello [развертывание и управление ими tooAzure данных Data Protection Manager с помощью PowerShell](backup-client-automation.md) , хранении данных в хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-108">If you are a new Azure Backup user and have not created a backup vault in your subscription, use hello article, [Deploy and manage Data Protection Manager data tooAzure using PowerShell](backup-client-automation.md) so you store your data in a Recovery Services vault.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="7d4f0-109">Теперь можно обновить вашими хранилищами служб tooRecovery хранилища резервной копии.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-109">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="7d4f0-110">Дополнительные сведения см. в статье hello [обновление tooa хранилища резервной копии, в хранилище служб восстановления](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="7d4f0-110">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="7d4f0-111">Корпорация Майкрософт рекомендует tooupgrade вашей резервных хранилищ tooRecovery хранилищами служб.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-111">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="7d4f0-112">После 15 октября 2017 г. нельзя использовать PowerShell toocreate резервное копирование хранилищ.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-112">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="7d4f0-113">**К 1 ноября 2017 года**:</span><span class="sxs-lookup"><span data-stu-id="7d4f0-113">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="7d4f0-114">Все оставшиеся хранилища резервной копии будет автоматически обновленные tooRecovery хранилищами служб.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-114">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="7d4f0-115">Вы не будет возможности tooaccess данные резервной копии hello классического портала.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-115">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="7d4f0-116">Вместо этого используйте hello Azure портала tooaccess резервного копирования данных в хранилищах службы восстановления.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-116">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="install-azure-powershell"></a><span data-ttu-id="7d4f0-117">Установка Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7d4f0-117">Install Azure PowerShell</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="7d4f0-118">Версия Azure PowerShell 1.0 была выпущена в октябре 2015 г.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-118">In October 2015, Azure PowerShell 1.0 was released.</span></span> <span data-ttu-id="7d4f0-119">В этом выпуске успешно hello 0.9.8 выпуска и приводящими существенные изменения, особенно в шаблон именования hello hello командлетов.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-119">This release succeeded hello 0.9.8 release and brought about some significant changes, especially in hello naming pattern of hello cmdlets.</span></span> <span data-ttu-id="7d4f0-120">1.0 выполните командлеты hello шаблону именования {глагол}-AzureRm {существительное}; в то время как hello 0.9.8 имена не включают **Rm** (например, New-AzureRmResourceGroup вместо New AzureResourceGroup).</span><span class="sxs-lookup"><span data-stu-id="7d4f0-120">1.0 cmdlets follow hello naming pattern {verb}-AzureRm{noun}; whereas, hello 0.9.8 names do not include **Rm** (for example, New-AzureRmResourceGroup instead of New-AzureResourceGroup).</span></span> <span data-ttu-id="7d4f0-121">При использовании Azure PowerShell 0.9.8, необходимо сначала включить режим диспетчера ресурсов hello, запустив hello **AzureResourceManager Switch-AzureMode** команды.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-121">When using Azure PowerShell 0.9.8, you must first enable hello Resource Manager mode by running hello **Switch-AzureMode AzureResourceManager** command.</span></span> <span data-ttu-id="7d4f0-122">Эта команда не требуется в версии 1.0 и более поздних версиях.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-122">This command is not necessary in 1.0 or later.</span></span>

<span data-ttu-id="7d4f0-123">Если требуется toouse в сценарии, написанные для среды hello 0.9.8, hello 1.0 или более поздней версии среды следует тщательно проверить сценарии hello в предварительной рабочей среде перед их использованием в рабочей среде tooavoid непредвиденного влияния.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-123">If you want toouse your scripts written for hello 0.9.8 environment, in hello 1.0 or later environment, you should carefully test hello scripts in a pre-production environment before using them in production tooavoid unexpected impact.</span></span>

<span data-ttu-id="7d4f0-124">[Загрузка последней версии PowerShell hello](https://github.com/Azure/azure-powershell/releases) (Минимальная требуемая версия —: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="7d4f0-124">[Download hello latest PowerShell release](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>

[!INCLUDE [arm-getting-setup-powershell](../../includes/arm-getting-setup-powershell.md)]

## <a name="create-a-backup-vault"></a><span data-ttu-id="7d4f0-125">создать хранилище архивации;</span><span class="sxs-lookup"><span data-stu-id="7d4f0-125">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="7d4f0-126">Для клиентов, использующих Azure Backup для hello первый раз необходимо использовать с вашей подпиской поставщика toobe tooregister hello Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-126">For customers using Azure Backup for hello first time, you need tooregister hello Azure Backup provider toobe used with your subscription.</span></span> <span data-ttu-id="7d4f0-127">Это можно сделать, выполнив следующую команду hello: Register AzureProvider - ProviderNamespace «Microsoft.Backup»</span><span class="sxs-lookup"><span data-stu-id="7d4f0-127">This can be done by running hello following command: Register-AzureProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="7d4f0-128">Можно создать новое хранилище резервных копий с помощью hello **New AzureRMBackupVault** командлета.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-128">You can create a new backup vault using hello **New-AzureRMBackupVault** cmdlet.</span></span> <span data-ttu-id="7d4f0-129">резервное хранилище Hello является ресурс ARM, поэтому вам необходимо tooplace его в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-129">hello backup vault is an ARM resource, so you need tooplace it within a Resource Group.</span></span> <span data-ttu-id="7d4f0-130">В консоли Azure PowerShell с повышенными привилегиями выполните hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="7d4f0-130">In an elevated Azure PowerShell console, run hello following commands:</span></span>

```
PS C:\> New-AzureResourceGroup –Name “test-rg” -Region “West US”
PS C:\> $backupvault = New-AzureRMBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

<span data-ttu-id="7d4f0-131">Используйте hello **Get AzureRMBackupVault** хранилищ архивации hello toolist командлета в подписке.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-131">Use hello **Get-AzureRMBackupVault** cmdlet toolist hello backup vaults in a subscription.</span></span>

## <a name="installing-hello-azure-backup-agent"></a><span data-ttu-id="7d4f0-132">Установка агента Azure Backup hello</span><span class="sxs-lookup"><span data-stu-id="7d4f0-132">Installing hello Azure Backup agent</span></span>
<span data-ttu-id="7d4f0-133">Перед установкой агента Azure Backup hello загружены и на приветствия Windows Server необходимо toohave hello установщика.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-133">Before you install hello Azure Backup agent, you need toohave hello installer downloaded and present on hello Windows Server.</span></span> <span data-ttu-id="7d4f0-134">Можно получить последнюю версию установщика hello hello hello [центра загрузки Майкрософт](http://aka.ms/azurebackup_agent) или со страницы панели мониторинга резервного хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-134">You can get hello latest version of hello installer from hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from hello backup vault's Dashboard page.</span></span> <span data-ttu-id="7d4f0-135">Сохранить hello установщика tooan легкодоступном месте как * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-135">Save hello installer tooan easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="7d4f0-136">tooinstall агент hello, запустите следующую команду в консоли PowerShell с повышенными hello:</span><span class="sxs-lookup"><span data-stu-id="7d4f0-136">tooinstall hello agent, run hello following command in an elevated PowerShell console:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="7d4f0-137">При этом устанавливаются hello агента со всеми параметрами по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-137">This installs hello agent with all hello default options.</span></span> <span data-ttu-id="7d4f0-138">Установка Hello занимает несколько минут в фоновом режиме hello.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-138">hello installation takes a few minutes in hello background.</span></span> <span data-ttu-id="7d4f0-139">Если вы не укажете hello */nu* параметр, а затем hello **центра обновления Windows** окно в конце hello hello toocheck установки обновлений.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-139">If you do not specify hello */nu* option then hello **Windows Update** window will open at hello end of hello installation toocheck for any updates.</span></span> <span data-ttu-id="7d4f0-140">После установки агент hello будет отображаться в списке установленных программ hello.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-140">Once installed, hello agent will show in hello list of installed programs.</span></span>

<span data-ttu-id="7d4f0-141">toosee hello список установленных программ, перейдите в слишком**панели управления** > **программы** > **программы и компоненты**.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-141">toosee hello list of installed programs, go too**Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Агент установлен](./media/backup-client-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="7d4f0-143">Параметры установки</span><span class="sxs-lookup"><span data-stu-id="7d4f0-143">Installation options</span></span>
<span data-ttu-id="7d4f0-144">toosee, Здравствуйте, все параметры, доступные через hello командной строки, выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-144">toosee all hello options available via hello command-line, use hello following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="7d4f0-145">Hello доступны следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-145">hello available options include:</span></span>

| <span data-ttu-id="7d4f0-146">Параметр</span><span class="sxs-lookup"><span data-stu-id="7d4f0-146">Option</span></span> | <span data-ttu-id="7d4f0-147">Сведения</span><span class="sxs-lookup"><span data-stu-id="7d4f0-147">Details</span></span> | <span data-ttu-id="7d4f0-148">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="7d4f0-148">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7d4f0-149">/q</span><span class="sxs-lookup"><span data-stu-id="7d4f0-149">/q</span></span> |<span data-ttu-id="7d4f0-150">Позволяет выполнить тихую установку.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-150">Quiet installation</span></span> |- |
| <span data-ttu-id="7d4f0-151">/p:"расположение"</span><span class="sxs-lookup"><span data-stu-id="7d4f0-151">/p:"location"</span></span> |<span data-ttu-id="7d4f0-152">Путь toohello папку для установки агента Azure Backup hello.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-152">Path toohello installation folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="7d4f0-153">C:\Program Files\Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="7d4f0-153">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="7d4f0-154">/s:"расположение"</span><span class="sxs-lookup"><span data-stu-id="7d4f0-154">/s:"location"</span></span> |<span data-ttu-id="7d4f0-155">Путь toohello для папки кэша hello Azure Backup agent.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-155">Path toohello cache folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="7d4f0-156">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="7d4f0-156">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="7d4f0-157">/m</span><span class="sxs-lookup"><span data-stu-id="7d4f0-157">/m</span></span> |<span data-ttu-id="7d4f0-158">Участие в tooMicrosoft обновления</span><span class="sxs-lookup"><span data-stu-id="7d4f0-158">Opt-in tooMicrosoft Update</span></span> |- |
| <span data-ttu-id="7d4f0-159">/nu</span><span class="sxs-lookup"><span data-stu-id="7d4f0-159">/nu</span></span> |<span data-ttu-id="7d4f0-160">Позволяет отказаться от проверки наличия обновлений после завершения установки.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-160">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="7d4f0-161">/d</span><span class="sxs-lookup"><span data-stu-id="7d4f0-161">/d</span></span> |<span data-ttu-id="7d4f0-162">Удаляет агент служб восстановления Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-162">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="7d4f0-163">/ph</span><span class="sxs-lookup"><span data-stu-id="7d4f0-163">/ph</span></span> |<span data-ttu-id="7d4f0-164">Адрес узла прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-164">Proxy Host Address</span></span> |- |
| <span data-ttu-id="7d4f0-165">/po</span><span class="sxs-lookup"><span data-stu-id="7d4f0-165">/po</span></span> |<span data-ttu-id="7d4f0-166">Номер порта узла прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-166">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="7d4f0-167">/pu</span><span class="sxs-lookup"><span data-stu-id="7d4f0-167">/pu</span></span> |<span data-ttu-id="7d4f0-168">Имя пользователя узла прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-168">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="7d4f0-169">/pw</span><span class="sxs-lookup"><span data-stu-id="7d4f0-169">/pw</span></span> |<span data-ttu-id="7d4f0-170">Пароль прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-170">Proxy Password</span></span> |- |

## <a name="registering-with-hello-azure-backup-service"></a><span data-ttu-id="7d4f0-171">Регистрация hello службы архивации Azure</span><span class="sxs-lookup"><span data-stu-id="7d4f0-171">Registering with hello Azure Backup service</span></span>
<span data-ttu-id="7d4f0-172">Прежде чем выполнять регистрацию с hello службы архивации Azure, необходимо tooensure, hello [необходимые компоненты](backup-configure-vault.md) соблюдены.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-172">Before you can register with hello Azure Backup service, you need tooensure that hello [prerequisites](backup-configure-vault.md) are met.</span></span> <span data-ttu-id="7d4f0-173">Необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="7d4f0-173">You must:</span></span>

* <span data-ttu-id="7d4f0-174">Действующая подписка Azure</span><span class="sxs-lookup"><span data-stu-id="7d4f0-174">Have a valid Azure subscription</span></span>
* <span data-ttu-id="7d4f0-175">Хранилище архивов</span><span class="sxs-lookup"><span data-stu-id="7d4f0-175">Have a backup vault</span></span>

<span data-ttu-id="7d4f0-176">toodownload hello учетные данные хранилища, запустите hello **Get AzureRMBackupVaultCredentials** командлет в консоли Azure PowerShell и хранилище его в удобном расположении, например * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-176">toodownload hello vault credentials, run hello **Get-AzureRMBackupVaultCredentials** cmdlet in an Azure PowerShell console and store it in a convenient location like *C:\Downloads\*.</span></span>

```
PS C:\> $credspath = "C:\"
PS C:\> $credsfilename = Get-AzureRMBackupVaultCredentials -Vault $backupvault -TargetLocation $credspath
PS C:\> $credsfilename
f5303a0b-fae4-4cdb-b44d-0e4c032dde26_backuprg_backuprn_2015-08-11--06-22-35.VaultCredentials
```

<span data-ttu-id="7d4f0-177">Регистрации hello машины с хранилищем hello осуществляется с помощью hello [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) командлета:</span><span class="sxs-lookup"><span data-stu-id="7d4f0-177">Registering hello machine with hello vault is done using hello [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet:</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration -VaultCredentials $cred -Confirm:$false

CertThumbprint      : 7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName : test-vault
Region              : West US

Machine registration succeeded.
```

> [!IMPORTANT]
> <span data-ttu-id="7d4f0-178">Не используйте файл учетных данных хранилища hello toospecify относительные пути.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-178">Do not use relative paths toospecify hello vault credentials file.</span></span> <span data-ttu-id="7d4f0-179">Необходимо указать абсолютный путь в качестве входного toohello командлета.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-179">You must provide an absolute path as an input toohello cmdlet.</span></span>
>
>

## <a name="networking-settings"></a><span data-ttu-id="7d4f0-180">Параметры сети</span><span class="sxs-lookup"><span data-stu-id="7d4f0-180">Networking settings</span></span>
<span data-ttu-id="7d4f0-181">Если подключение hello hello Windows компьютера toohello является Интернет через прокси-сервер, параметры прокси-сервера hello также можно указать toohello агента.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-181">When hello connectivity of hello Windows machine toohello internet is through a proxy server, hello proxy settings can also be provided toohello agent.</span></span> <span data-ttu-id="7d4f0-182">В нашем случае прокси-сервер не используется, поэтому мы явным образом удаляем все данные прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-182">In this example, there is no proxy server, so we are explicitly clearing any proxy-related information.</span></span>

<span data-ttu-id="7d4f0-183">Использование пропускной способности также можно управлять с помощью параметров hello ```work hour bandwidth``` и ```non-work hour bandwidth``` для заданного набора дней недели hello.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-183">Bandwidth usage can also be controlled with hello options of ```work hour bandwidth``` and ```non-work hour bandwidth``` for a given set of days of hello week.</span></span>

<span data-ttu-id="7d4f0-184">Задания параметров прокси-сервера и пропускной способности hello осуществляется с помощью hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) командлета:</span><span class="sxs-lookup"><span data-stu-id="7d4f0-184">Setting hello proxy and bandwidth details is done using hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span></span>

```
PS C:\> Set-OBMachineSetting -NoProxy
Server properties updated successfully.

PS C:\> Set-OBMachineSetting -NoThrottle
Server properties updated successfully.
```

## <a name="encryption-settings"></a><span data-ttu-id="7d4f0-185">Параметры шифрования</span><span class="sxs-lookup"><span data-stu-id="7d4f0-185">Encryption settings</span></span>
<span data-ttu-id="7d4f0-186">tooAzure Hello резервного копирования данных, отправляемых резервной копии является зашифрованным tooprotect hello конфиденциальность данных hello.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-186">hello backup data sent tooAzure Backup is encrypted tooprotect hello confidentiality of hello data.</span></span> <span data-ttu-id="7d4f0-187">Парольная фраза для шифрования Hello — hello «password» toodecrypt hello данные во время восстановления hello.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-187">hello encryption passphrase is hello "password" toodecrypt hello data at hello time of restore.</span></span>

```
PS C:\> ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force | Set-OBMachineSetting
Server properties updated successfully
```

> [!IMPORTANT]
> <span data-ttu-id="7d4f0-188">Обновление сведений парольную фразу hello надежным и безопасным, после ее установки.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-188">Keep hello passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="7d4f0-189">Данные могут toorestore из Azure без этой парольной фразы не будет.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-189">You will not be able toorestore data from Azure without this passphrase.</span></span>
>
>

## <a name="back-up-files-and-folders"></a><span data-ttu-id="7d4f0-190">Резервное копирование файлов и папок</span><span class="sxs-lookup"><span data-stu-id="7d4f0-190">Back up files and folders</span></span>
<span data-ttu-id="7d4f0-191">Для политики определены резервных копий из серверов и клиентов Windows tooAzure резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-191">All your backups from Windows Servers and clients tooAzure Backup are governed by a policy.</span></span> <span data-ttu-id="7d4f0-192">Hello политики состоит из трех частей:</span><span class="sxs-lookup"><span data-stu-id="7d4f0-192">hello policy comprises three parts:</span></span>

1. <span data-ttu-id="7d4f0-193">Объект **расписание резервного копирования** , указывающий, когда архивы toobe выполнены и синхронизируются с hello службой.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-193">A **backup schedule** that specifies when backups need toobe taken and synchronized with hello service.</span></span>
2. <span data-ttu-id="7d4f0-194">Объект **расписание хранения** , указывающее, как долго точки восстановления tooretain hello в Azure.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-194">A **retention schedule** that specifies how long tooretain hello recovery points in Azure.</span></span>
3. <span data-ttu-id="7d4f0-195">**Указания включения/исключения файлов** — определяет, для каких элементов следует создавать резервные копии.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-195">A **file inclusion/exclusion specification** that dictates what should be backed up.</span></span>

<span data-ttu-id="7d4f0-196">Поскольку мы будем использовать автоматическое резервное копирование данных, в этой статье предполагается, что заданных настроек нет.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-196">In this document, since we're automating backup, we'll assume nothing has been configured.</span></span> <span data-ttu-id="7d4f0-197">Мы сначала необходимо создать новую политику резервного копирования, с помощью hello [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) командлет и его использования.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-197">We begin by creating a new backup policy using hello [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet and using it.</span></span>

```
PS C:\> $newpolicy = New-OBPolicy
```

<span data-ttu-id="7d4f0-198">В это время hello политики является пустым и другие командлеты, необходимые toodefine какие элементы будут включены или исключены, при резервные копии выполняются и Здравствуйте, где будут храниться резервные копии.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-198">At this time hello policy is empty and other cmdlets are needed toodefine what items will be included or excluded, when backups will run, and where hello backups will be stored.</span></span>

### <a name="configuring-hello-backup-schedule"></a><span data-ttu-id="7d4f0-199">Настройка расписания резервного копирования hello</span><span class="sxs-lookup"><span data-stu-id="7d4f0-199">Configuring hello backup schedule</span></span>
<span data-ttu-id="7d4f0-200">Здравствуйте, сначала hello состоит из трех частей политики — расписание архивации hello, которое создается с помощью hello [New OBSchedule](https://technet.microsoft.com/library/hh770401) командлета.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-200">hello first of hello 3 parts of a policy is hello backup schedule, which is created using hello [New-OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet.</span></span> <span data-ttu-id="7d4f0-201">расписание резервного копирования Hello определяет, когда архивы toobe копии.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-201">hello backup schedule defines when backups need toobe taken.</span></span> <span data-ttu-id="7d4f0-202">При создании расписания необходимые toospecify 2 входных параметров.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-202">When creating a schedule you need toospecify 2 input parameters:</span></span>

* <span data-ttu-id="7d4f0-203">**Дни недели hello** следует запускать эту резервную копию hello.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-203">**Days of hello week** that hello backup should run.</span></span> <span data-ttu-id="7d4f0-204">Можно запустить задание резервного копирования hello только один день, или каждый день недели hello или любую комбинацию между ними.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-204">You can run hello backup job on just one day, or every day of hello week, or any combination in between.</span></span>
* <span data-ttu-id="7d4f0-205">**Время суток hello** когда должно выполняться резервное копирование hello.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-205">**Times of hello day** when hello backup should run.</span></span> <span data-ttu-id="7d4f0-206">Определяется too3 разное время суток hello, когда будут создаваться hello резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-206">You can define up too3 different times of hello day when hello backup will be triggered.</span></span>

<span data-ttu-id="7d4f0-207">Например, политику резервного копирования можно настроить таким образом, чтобы соответствующее задание выполнялось в 16:00 каждые субботу и воскресенье.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-207">For instance, you could configure a backup policy that runs at 4PM every Saturday and Sunday.</span></span>

```
PS C:\> $sched = New-OBSchedule -DaysofWeek Saturday, Sunday -TimesofDay 16:00
```

<span data-ttu-id="7d4f0-208">расписание резервного копирования Hello требуется toobe, связанных с политикой, но это можно сделать с помощью hello [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) командлета.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-208">hello backup schedule needs toobe associated with a policy, and this can be achieved by using hello [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet.</span></span>

```
PS C:> Set-OBSchedule -Policy $newpolicy -Schedule $sched
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s) DsList : PolicyName : RetentionPolicy : State : New PolicyState : Valid
```
### <a name="configuring-a-retention-policy"></a><span data-ttu-id="7d4f0-209">Настройка политики хранения</span><span class="sxs-lookup"><span data-stu-id="7d4f0-209">Configuring a retention policy</span></span>
<span data-ttu-id="7d4f0-210">Политика хранения Hello определяет продолжительность восстановления сохраняются точки, созданные из задания резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-210">hello retention policy defines how long recovery points created from backup jobs are retained.</span></span> <span data-ttu-id="7d4f0-211">При создании новой политики хранения с помощью hello [New OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) командлета, можно указать hello, сколько дней hello точки восстановления резервной копии должны toobe сохранило резервного копирования Azure.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-211">When creating a new retention policy using hello [New-OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet, you can specify hello number of days that hello backup recovery points need toobe retained with Azure Backup.</span></span> <span data-ttu-id="7d4f0-212">пример Hello задана политика сохранения 7 дней.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-212">hello example below sets a retention policy of 7 days.</span></span>

```
PS C:\> $retentionpolicy = New-OBRetentionPolicy -RetentionDays 7
```

<span data-ttu-id="7d4f0-213">Hello политика хранения должна быть связана hello основной политики с помощью командлета hello [OBRetentionPolicy набор](https://technet.microsoft.com/library/hh770405):</span><span class="sxs-lookup"><span data-stu-id="7d4f0-213">hello retention policy must be associated with hello main policy using hello cmdlet [Set-OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span></span>

```
PS C:\> Set-OBRetentionPolicy -Policy $newpolicy -RetentionPolicy $retentionpolicy

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          :
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid
```
### <a name="including-and-excluding-files-toobe-backed-up"></a><span data-ttu-id="7d4f0-214">Включение и исключение файлов toobe резервного копирования</span><span class="sxs-lookup"><span data-stu-id="7d4f0-214">Including and excluding files toobe backed up</span></span>
<span data-ttu-id="7d4f0-215">```OBFileSpec``` Объект определяет hello файлы toobe включен и исключен из резервной копии.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-215">An ```OBFileSpec``` object defines hello files toobe included and excluded in a backup.</span></span> <span data-ttu-id="7d4f0-216">Это набор правил, что область out hello защищенных файлов и папок на компьютере.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-216">This is a set of rules that scope out hello protected files and folders on a machine.</span></span> <span data-ttu-id="7d4f0-217">Можно создать любое количество правил включения или исключения файлов и связать их с политикой.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-217">You can have as many file inclusion or exclusion rules as required, and associate them with a policy.</span></span> <span data-ttu-id="7d4f0-218">При создании нового объекта OBFileSpec, можно сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="7d4f0-218">When creating a new OBFileSpec object, you can:</span></span>

* <span data-ttu-id="7d4f0-219">Укажите hello файлов и папок toobe включены</span><span class="sxs-lookup"><span data-stu-id="7d4f0-219">Specify hello files and folders toobe included</span></span>
* <span data-ttu-id="7d4f0-220">Укажите hello файлов и папок toobe исключены</span><span class="sxs-lookup"><span data-stu-id="7d4f0-220">Specify hello files and folders toobe excluded</span></span>
* <span data-ttu-id="7d4f0-221">Укажите рекурсивные резервного копирования данных в папке (или) ли следует копировать только hello верхнего уровня файлы в указанной папке hello вверх.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-221">Specify recursive backup of data in a folder (or) whether only hello top-level files in hello specified folder should be backed up.</span></span>

<span data-ttu-id="7d4f0-222">Hello последний достигается с помощью флага - нерекурсивных hello в команде New-OBFileSpec hello.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-222">hello latter is achieved by using hello -NonRecursive flag in hello New-OBFileSpec command.</span></span>

<span data-ttu-id="7d4f0-223">В следующем примере hello мы резервное копирование тома C: и D: и исключить hello двоичных файлов операционной системы в папке Windows hello и любые временные папки.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-223">In hello example below, we'll back up volume C: and D: and exclude hello OS binaries in hello Windows folder and any temporary folders.</span></span> <span data-ttu-id="7d4f0-224">toodo, поэтому мы создадим две спецификации файла с помощью hello [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) командлет - для включения и исключения.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-224">toodo so we'll create two file specifications using hello [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - one for inclusion and one for exclusion.</span></span> <span data-ttu-id="7d4f0-225">После создания спецификации файла hello они связаны hello политики с помощью hello [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) командлета.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-225">Once hello file specifications have been created, they're associated with hello policy using hello [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet.</span></span>

```
PS C:\> $inclusions = New-OBFileSpec -FileSpec @("C:\", "D:\")

PS C:\> $exclusions = New-OBFileSpec -FileSpec @("C:\windows", "C:\temp") -Exclude

PS C:\> Add-OBFileSpec -Policy $newpolicy -FileSpec $inclusions

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          : {DataSource
                  DatasourceId:0
                  Name:C:\
                  FileSpec:FileSpec
                  FileSpec:C:\
                  IsExclude:False
                  IsRecursive:True

                  , DataSource
                  DatasourceId:0
                  Name:D:\
                  FileSpec:FileSpec
                  FileSpec:D:\
                  IsExclude:False
                  IsRecursive:True

                  }
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid


PS C:\> Add-OBFileSpec -Policy $newpolicy -FileSpec $exclusions

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          : {DataSource
                  DatasourceId:0
                  Name:C:\
                  FileSpec:FileSpec
                  FileSpec:C:\
                  IsExclude:False
                  IsRecursive:True
                  ,FileSpec
                  FileSpec:C:\windows
                  IsExclude:True
                  IsRecursive:True
                  ,FileSpec
                  FileSpec:C:\temp
                  IsExclude:True
                  IsRecursive:True

                  , DataSource
                  DatasourceId:0
                  Name:D:\
                  FileSpec:FileSpec
                  FileSpec:D:\
                  IsExclude:False
                  IsRecursive:True

                  }
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid
```

### <a name="applying-hello-policy"></a><span data-ttu-id="7d4f0-226">Применение политики hello</span><span class="sxs-lookup"><span data-stu-id="7d4f0-226">Applying hello policy</span></span>
<span data-ttu-id="7d4f0-227">Теперь hello объекта политики завершена и имеет связанное расписание резервного копирования, политика хранения и список включения и исключения файлов.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-227">Now hello policy object is complete and has an associated backup schedule, retention policy, and an inclusion/exclusion list of files.</span></span> <span data-ttu-id="7d4f0-228">Эта политика теперь могут быть зафиксированы для toouse резервного копирования Azure.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-228">This policy can now be committed for Azure Backup toouse.</span></span> <span data-ttu-id="7d4f0-229">Перед установкой hello вновь созданные политики убедитесь, что нет существующие политики резервного копирования, связанных с сервером hello с помощью hello [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) командлета.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-229">Before you apply hello newly created policy ensure that there are no existing backup policies associated with hello server by using hello [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet.</span></span> <span data-ttu-id="7d4f0-230">Удаление политики hello выдаст запрос на подтверждение.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-230">Removing hello policy will prompt for confirmation.</span></span> <span data-ttu-id="7d4f0-231">Подтверждение hello tooskip использовать hello ```-Confirm:$false``` флаг с командлетом hello.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-231">tooskip hello confirmation use hello ```-Confirm:$false``` flag with hello cmdlet.</span></span>

```
PS C:> Get-OBPolicy | Remove-OBPolicy
Microsoft Azure Backup Are you sure you want tooremove this backup policy? This will delete all hello backed up data. [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
```

<span data-ttu-id="7d4f0-232">Слишком большой объем выделяемой объект политики hello выполняется с помощью hello [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) командлета.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-232">Committing hello policy object is done using hello [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet.</span></span> <span data-ttu-id="7d4f0-233">При этом также будет запрашиваться соответствующее подтверждение.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-233">This will also ask for confirmation.</span></span> <span data-ttu-id="7d4f0-234">Подтверждение hello tooskip использовать hello ```-Confirm:$false``` флаг с командлетом hello.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-234">tooskip hello confirmation use hello ```-Confirm:$false``` flag with hello cmdlet.</span></span>

```
PS C:> Set-OBPolicy -Policy $newpolicy
Microsoft Azure Backup Do you want toosave this backup policy ? [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s)
DsList : {DataSource
         DatasourceId:4508156004108672185
         Name:C:\
         FileSpec:FileSpec
         FileSpec:C:\
         IsExclude:False
         IsRecursive:True,

         FileSpec
         FileSpec:C:\windows
         IsExclude:True
         IsRecursive:True,

         FileSpec
         FileSpec:C:\temp
         IsExclude:True
         IsRecursive:True,

         DataSource
         DatasourceId:4508156005178868542
         Name:D:\
         FileSpec:FileSpec
         FileSpec:D:\
         IsExclude:False
         IsRecursive:True
    }
PolicyName : c2eb6568-8a06-49f4-a20e-3019ae411bac
RetentionPolicy : Retention Days : 7
              WeeklyLTRSchedule :
              Weekly schedule is not set

              MonthlyLTRSchedule :
              Monthly schedule is not set

              YearlyLTRSchedule :
              Yearly schedule is not set
State : Existing PolicyState : Valid
```

<span data-ttu-id="7d4f0-235">Вы можете просмотреть сведения hello hello существующие политики резервного копирования с помощью hello [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) командлета.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-235">You can view hello details of hello existing backup policy using hello [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet.</span></span> <span data-ttu-id="7d4f0-236">Можно выполнять детализацию дальше с помощью hello [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) командлет расписание резервного копирования hello и hello [Get OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) командлета для политики хранения hello</span><span class="sxs-lookup"><span data-stu-id="7d4f0-236">You can drill-down further using hello [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet for hello backup schedule and hello [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) cmdlet for hello retention policies</span></span>

```
PS C:> Get-OBPolicy | Get-OBSchedule
SchedulePolicyName : 71944081-9950-4f7e-841d-32f0a0a1359a
ScheduleRunDays : {Saturday, Sunday}
ScheduleRunTimes : {16:00:00}
State : Existing

PS C:> Get-OBPolicy | Get-OBRetentionPolicy
RetentionDays : 7
RetentionPolicyName : ca3574ec-8331-46fd-a605-c01743a5265e
State : Existing

PS C:> Get-OBPolicy | Get-OBFileSpec
FileName : *
FilePath : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
FileSpec : D:\
IsExclude : False
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\
FileSpec : C:\
IsExclude : False
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\windows
FileSpec : C:\windows
IsExclude : True
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\temp
FileSpec : C:\temp
IsExclude : True
IsRecursive : True
```

### <a name="performing-an-ad-hoc-backup"></a><span data-ttu-id="7d4f0-237">Выполнение нерегламентированного резервного копирования</span><span class="sxs-lookup"><span data-stu-id="7d4f0-237">Performing an ad-hoc backup</span></span>
<span data-ttu-id="7d4f0-238">После настройки политики резервного копирования резервных копий hello будет выполняться по расписанию hello.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-238">Once a backup policy has been set hello backups will occur per hello schedule.</span></span> <span data-ttu-id="7d4f0-239">Резервное копирование ad-hoc запуска можно также с помощью hello [OBBackup начала](https://technet.microsoft.com/library/hh770426) командлета:</span><span class="sxs-lookup"><span data-stu-id="7d4f0-239">Triggering an ad-hoc backup is also possible using hello [Start-OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:</span></span>

```
PS C:> Get-OBPolicy | Start-OBBackup
Taking snapshot of volumes...
Preparing storage...
Estimating size of backup items...
Estimating size of backup items...
Transferring data...
Verifying backup...
Job completed.
hello backup operation completed successfully.
```

## <a name="restore-data-from-azure-backup"></a><span data-ttu-id="7d4f0-240">Восстановление данных из службы архивации Azure</span><span class="sxs-lookup"><span data-stu-id="7d4f0-240">Restore data from Azure Backup</span></span>
<span data-ttu-id="7d4f0-241">Этот раздел поможет выполнить шаги hello для автоматического восстановления данных из резервной копии Azure.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-241">This section will guide you through hello steps for automating recovery of data from Azure Backup.</span></span> <span data-ttu-id="7d4f0-242">Это включает в себя таким образом hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="7d4f0-242">Doing so involves hello following steps:</span></span>

1. <span data-ttu-id="7d4f0-243">Выберите исходный том hello</span><span class="sxs-lookup"><span data-stu-id="7d4f0-243">Pick hello source volume</span></span>
2. <span data-ttu-id="7d4f0-244">Выберите резервного копирования toorestore точки</span><span class="sxs-lookup"><span data-stu-id="7d4f0-244">Choose a backup point toorestore</span></span>
3. <span data-ttu-id="7d4f0-245">Выберите элемент toorestore</span><span class="sxs-lookup"><span data-stu-id="7d4f0-245">Choose an item toorestore</span></span>
4. <span data-ttu-id="7d4f0-246">Инициирующий процесс восстановления hello</span><span class="sxs-lookup"><span data-stu-id="7d4f0-246">Trigger hello restore process</span></span>

### <a name="picking-hello-source-volume"></a><span data-ttu-id="7d4f0-247">Комплектации hello исходного тома</span><span class="sxs-lookup"><span data-stu-id="7d4f0-247">Picking hello source volume</span></span>
<span data-ttu-id="7d4f0-248">В порядке toorestore элемент из резервного копирования Azure необходимо сначала tooidentify hello источник элемента hello.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-248">In order toorestore an item from Azure Backup, you first need tooidentify hello source of hello item.</span></span> <span data-ttu-id="7d4f0-249">Поскольку команды hello выполнении в контексте сервера или клиента Windows hello, hello машины уже определен.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-249">Since we're executing hello commands in hello context of a Windows Server or a Windows client, hello machine is already identified.</span></span> <span data-ttu-id="7d4f0-250">Hello следующим шагом в определение исходного hello — tooidentify hello том, содержащий его.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-250">hello next step in identifying hello source is tooidentify hello volume containing it.</span></span> <span data-ttu-id="7d4f0-251">Список томов или источников резервного копирования с этого компьютера можно получить, выполнив hello [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) командлета.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-251">A list of volumes or sources being backed up from this machine can be retrieved by executing hello [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet.</span></span> <span data-ttu-id="7d4f0-252">Эта команда возвращает массив всех источников hello, полученные с сервера и клиента.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-252">This command returns an array of all hello sources backed up from this server/client.</span></span>

```
PS C:> $source = Get-OBRecoverableSource
PS C:> $source
FriendlyName : C:\
RecoverySourceName : C:\
ServerName : myserver.microsoft.com

FriendlyName : D:\
RecoverySourceName : D:\
ServerName : myserver.microsoft.com
```

### <a name="choosing-a-backup-point-toorestore"></a><span data-ttu-id="7d4f0-253">Выбор резервного копирования toorestore точки</span><span class="sxs-lookup"><span data-stu-id="7d4f0-253">Choosing a backup point toorestore</span></span>
<span data-ttu-id="7d4f0-254">Hello список точек резервного копирования, можно получить, выполнив hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) командлет с соответствующими параметрами.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-254">hello list of backup points can be retrieved by executing hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet with appropriate parameters.</span></span> <span data-ttu-id="7d4f0-255">В нашем примере мы выберем hello последней резервной копии точки для исходного тома hello *D:* и использовать его toorecover определенного файла.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-255">In our example, we’ll choose hello latest backup point for hello source volume *D:* and use it toorecover a specific file.</span></span>

```
PS C:> $rps = Get-OBRecoverableItem -Source $source[1]
IsDir : False
ItemNameFriendly : D:\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
LocalMountPoint : D:\
MountPointName : D:\
Name : D:\
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime :

IsDir : False
ItemNameFriendly : D:\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
LocalMountPoint : D:\
MountPointName : D:\
Name : D:\
PointInTime : 17-Jun-15 6:31:31 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime :
```
<span data-ttu-id="7d4f0-256">Hello объекта ```$rps``` является массивом точек резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-256">hello object ```$rps``` is an array of backup points.</span></span> <span data-ttu-id="7d4f0-257">Hello первый элемент является последней точки hello и n-й элемент hello — самая старая точка hello.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-257">hello first element is hello latest point and hello Nth element is hello oldest point.</span></span> <span data-ttu-id="7d4f0-258">Последняя точка toochoose hello, мы будем использовать ```$rps[0]```.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-258">toochoose hello latest point, we will use ```$rps[0]```.</span></span>

### <a name="choosing-an-item-toorestore"></a><span data-ttu-id="7d4f0-259">Выбор элемента toorestore</span><span class="sxs-lookup"><span data-stu-id="7d4f0-259">Choosing an item toorestore</span></span>
<span data-ttu-id="7d4f0-260">использовать tooidentify hello точное файл или папка toorestore, рекурсивно hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) командлета.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-260">tooidentify hello exact file or folder toorestore, recursively use hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet.</span></span> <span data-ttu-id="7d4f0-261">Иерархии папок hello этот способ можно просматривать только с помощью hello ```Get-OBRecoverableItem```.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-261">That way hello folder hierarchy can be browsed solely using hello ```Get-OBRecoverableItem```.</span></span>

<span data-ttu-id="7d4f0-262">В этом примере, если мы хотим файл hello toorestore *finances.xls* мы ссылаться, используя hello объекта ```$filesFolders[1]```.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-262">In this example, if we want toorestore hello file *finances.xls* we can reference that using hello object ```$filesFolders[1]```.</span></span>

```
PS C:> $filesFolders = Get-OBRecoverableItem $rps[0]
PS C:> $filesFolders
IsDir : True
ItemNameFriendly : D:\MyData\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\
LocalMountPoint : D:\
MountPointName : D:\
Name : MyData
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime : 15-Jun-15 8:49:29 AM

PS C:> $filesFolders = Get-OBRecoverableItem $filesFolders[0]
PS C:> $filesFolders
IsDir : False
ItemNameFriendly : D:\MyData\screenshot.oxps
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\screenshot.oxps
LocalMountPoint : D:\
MountPointName : D:\
Name : screenshot.oxps
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize : 228313
ItemLastModifiedTime : 21-Jun-14 6:45:09 AM

IsDir : False
ItemNameFriendly : D:\MyData\finances.xls
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\finances.xls
LocalMountPoint : D:\
MountPointName : D:\
Name : finances.xls
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize : 96256
ItemLastModifiedTime : 21-Jun-14 6:43:02 AM
```

<span data-ttu-id="7d4f0-263">Можно также выполнить поиск toorestore элементов с помощью hello ```Get-OBRecoverableItem``` командлета.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-263">You can also search for items toorestore using hello ```Get-OBRecoverableItem``` cmdlet.</span></span> <span data-ttu-id="7d4f0-264">В нашем примере toosearch для *finances.xls* удалось получить дескриптор файла hello, запустив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7d4f0-264">In our example, toosearch for *finances.xls* we could get a handle on hello file by running this command:</span></span>

```
PS C:\> $item = Get-OBRecoverableItem -RecoveryPoint $rps[0] -Location "D:\MyData" -SearchString "finance*"
```

### <a name="triggering-hello-restore-process"></a><span data-ttu-id="7d4f0-265">Запуск процесса восстановления hello</span><span class="sxs-lookup"><span data-stu-id="7d4f0-265">Triggering hello restore process</span></span>
<span data-ttu-id="7d4f0-266">процесс восстановления tootrigger hello, необходимо сначала параметры восстановления toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-266">tootrigger hello restore process, we first need toospecify hello recovery options.</span></span> <span data-ttu-id="7d4f0-267">Это можно сделать с помощью hello [New OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) командлета.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-267">This can be done by using hello [New-OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet.</span></span> <span data-ttu-id="7d4f0-268">Например, предположим, что файлы hello toorestore мы хотим слишком*C:\temp*. Также предположим, что мы хотим tooskip существующие файлы в папку назначения hello *C:\temp*. toocreate такой вариант восстановления, используйте hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7d4f0-268">For this example, let's assume that we want toorestore hello files too*C:\temp*. Let's also assume that we want tooskip files that already exist on hello destination folder *C:\temp*. toocreate such a recovery option, use hello following command:</span></span>

```
PS C:\> $recovery_option = New-OBRecoveryOption -DestinationPath "C:\temp" -OverwriteType Skip
```

<span data-ttu-id="7d4f0-269">Теперь запускать восстановление с помощью hello [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) на выбранных hello ```$item``` из вывода hello hello ```Get-OBRecoverableItem``` командлета:</span><span class="sxs-lookup"><span data-stu-id="7d4f0-269">Now trigger restore by using hello [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) command on hello selected ```$item``` from hello output of hello ```Get-OBRecoverableItem``` cmdlet:</span></span>

```
PS C:\> Start-OBRecovery -RecoverableItem $item -RecoveryOption $recover_option
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Job completed.
hello recovery operation completed successfully.
```


## <a name="uninstalling-hello-azure-backup-agent"></a><span data-ttu-id="7d4f0-270">Удаление агента Azure Backup hello</span><span class="sxs-lookup"><span data-stu-id="7d4f0-270">Uninstalling hello Azure Backup agent</span></span>
<span data-ttu-id="7d4f0-271">Удаление агента Azure Backup hello можно сделать с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7d4f0-271">Uninstalling hello Azure Backup agent can be done by using hello following command:</span></span>

```
PS C:\> .\MARSAgentInstaller.exe /d /q
```

<span data-ttu-id="7d4f0-272">При удалении hello двоичные файлы агента с компьютера hello имеет некоторые последствия tooconsider:</span><span class="sxs-lookup"><span data-stu-id="7d4f0-272">Uninstalling hello agent binaries from hello machine has some consequences tooconsider:</span></span>

* <span data-ttu-id="7d4f0-273">Удаляет фильтр файлов hello из машины hello и остановить отслеживание изменений.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-273">It removes hello file-filter from hello machine, and tracking of changes is stopped.</span></span>
* <span data-ttu-id="7d4f0-274">Все данные политики удаляется с компьютера hello, но сведения о политике hello продолжается toobe хранятся в службе hello.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-274">All policy information is removed from hello machine, but hello policy information continues toobe stored in hello service.</span></span>
* <span data-ttu-id="7d4f0-275">Удаляются все расписания резервного копирования, и последующие операции резервного копирования больше не выполняются.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-275">All backup schedules are removed, and no further backups are taken.</span></span>

<span data-ttu-id="7d4f0-276">Однако hello данные хранятся в Azure остается и сохраняются согласно установки политики хранения hello вами.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-276">However, hello data stored in Azure remains and is retained as per hello retention policy setup by you.</span></span> <span data-ttu-id="7d4f0-277">Предыдущие точки восстановления автоматически рассматриваются как устаревшие.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-277">Older points are automatically aged out.</span></span>

## <a name="remote-management"></a><span data-ttu-id="7d4f0-278">Удаленное управление</span><span class="sxs-lookup"><span data-stu-id="7d4f0-278">Remote management</span></span>
<span data-ttu-id="7d4f0-279">Все управление hello вокруг hello Azure Backup agent, политики и источников данных может быть выполнена удаленно с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-279">All hello management around hello Azure Backup agent, policies, and data sources can be done remotely through PowerShell.</span></span> <span data-ttu-id="7d4f0-280">Привет, удаленное управление компьютеру toobe правильно подготовлен.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-280">hello machine that will be managed remotely needs toobe prepared correctly.</span></span>

<span data-ttu-id="7d4f0-281">По умолчанию служба удаленного управления Windows hello настроена на запуск вручную.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-281">By default, hello WinRM service is configured for manual startup.</span></span> <span data-ttu-id="7d4f0-282">Тип запуска Hello должен быть установлен слишком*автоматического* и hello служба должна быть запущена.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-282">hello startup type must be set too*Automatic* and hello service should be started.</span></span> <span data-ttu-id="7d4f0-283">tooverify, hello служба WinRM запущена, значение свойства Status hello hello должно быть *под управлением*.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-283">tooverify that hello WinRM service is running, hello value of hello Status property should be *Running*.</span></span>

```
PS C:\> Get-Service WinRM

Status   Name               DisplayName
------   ----               -----------
Running  winrm              Windows Remote Management (WS-Manag...
```

<span data-ttu-id="7d4f0-284">Для удаленного взаимодействия необходимо настроить PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-284">PowerShell should be configured for remoting.</span></span>

```
PS C:\> Enable-PSRemoting -force
WinRM is already set up tooreceive requests on this computer.
WinRM has been updated for remote management.
WinRM firewall exception enabled.

PS C:\> Set-ExecutionPolicy unrestricted -force
```

<span data-ttu-id="7d4f0-285">машины Hello теперь можно управлять удаленно — начиная с установки hello hello агента.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-285">hello machine can now be managed remotely - starting from hello installation of hello agent.</span></span> <span data-ttu-id="7d4f0-286">Например следующий скрипт hello копирует hello агента toohello удаленный компьютер и устанавливает его.</span><span class="sxs-lookup"><span data-stu-id="7d4f0-286">For example, hello following script copies hello agent toohello remote machine and installs it.</span></span>

```
PS C:\> $dloc = "\\REMOTESERVER01\c$\Windows\Temp"
PS C:\> $agent = "\\REMOTESERVER01\c$\Windows\Temp\MARSAgentInstaller.exe"
PS C:\> $args = "/q"
PS C:\> Copy-Item "C:\Downloads\MARSAgentInstaller.exe" -Destination $dloc - force

PS C:\> $s = New-PSSession -ComputerName REMOTESERVER01
PS C:\> Invoke-Command -Session $s -Script { param($d, $a) Start-Process -FilePath $d $a -Wait } -ArgumentList $agent $args
```

## <a name="next-steps"></a><span data-ttu-id="7d4f0-287">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7d4f0-287">Next steps</span></span>
<span data-ttu-id="7d4f0-288">Дополнительная информация о службе архивации Azure для сервера или клиента Windows</span><span class="sxs-lookup"><span data-stu-id="7d4f0-288">For more information about Azure Backup for Windows Server/Client see</span></span>

* [<span data-ttu-id="7d4f0-289">Введение tooAzure резервной копии</span><span class="sxs-lookup"><span data-stu-id="7d4f0-289">Introduction tooAzure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="7d4f0-290">Резервное копирование серверов Windows</span><span class="sxs-lookup"><span data-stu-id="7d4f0-290">Back up Windows Servers</span></span>](backup-configure-vault.md)
