---
title: "tooback PowerShell aaaUse копии Windows Server tooAzure | Документы Microsoft"
description: "Узнайте, как toodeploy и управление резервным копированием Azure с помощью PowerShell"
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 65218095-2996-44d9-917b-8c84fc9ac415
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: saurse;markgal;jimpark;nkolli;trinadhk
ms.openlocfilehash: f13224f53abd6fbd132fee4347b0b99e8f5e2678
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-windows-serverwindows-client-using-powershell"></a><span data-ttu-id="1f4df-103">Развертывание и управление ими tooAzure резервного копирования для клиента Windows Server и Windows с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="1f4df-103">Deploy and manage backup tooAzure for Windows Server/Windows Client using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1f4df-104">ARM</span><span class="sxs-lookup"><span data-stu-id="1f4df-104">ARM</span></span>](backup-client-automation.md)
> * [<span data-ttu-id="1f4df-105">Классический</span><span class="sxs-lookup"><span data-stu-id="1f4df-105">Classic</span></span>](backup-client-automation-classic.md)
>
>

<span data-ttu-id="1f4df-106">В этой статье показано, как toouse PowerShell для настройки резервного копирования Azure на Windows Server или на клиенте Windows и управление резервного копирования и восстановления.</span><span class="sxs-lookup"><span data-stu-id="1f4df-106">This article shows you how toouse PowerShell for setting up Azure Backup on Windows Server or a Windows client, and managing backup and recovery.</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="1f4df-107">Установка Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1f4df-107">Install Azure PowerShell</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="1f4df-108">Эта статья посвящена hello диспетчера ресурсов Azure (ARM) и hello MS Online Backup PowerShell командлеты, позволяющие toouse хранилище служб восстановления в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="1f4df-108">This article focuses on hello Azure Resource Manager (ARM) and hello MS Online Backup PowerShell cmdlets that enable you toouse a Recovery Services vault in a resource group.</span></span>

<span data-ttu-id="1f4df-109">Версия Azure PowerShell 1.0 была выпущена в октябре 2015 г.</span><span class="sxs-lookup"><span data-stu-id="1f4df-109">In October 2015, Azure PowerShell 1.0 was released.</span></span> <span data-ttu-id="1f4df-110">В этом выпуске успешно hello 0.9.8 выпуска и приводящими существенные изменения, особенно в шаблон именования hello hello командлетов.</span><span class="sxs-lookup"><span data-stu-id="1f4df-110">This release succeeded hello 0.9.8 release and brought about some significant changes, especially in hello naming pattern of hello cmdlets.</span></span> <span data-ttu-id="1f4df-111">1.0 выполните командлеты hello шаблону именования {глагол}-AzureRm {существительное}; в то время как hello 0.9.8 имена не включают **Rm** (например, New-AzureRmResourceGroup вместо New AzureResourceGroup).</span><span class="sxs-lookup"><span data-stu-id="1f4df-111">1.0 cmdlets follow hello naming pattern {verb}-AzureRm{noun}; whereas, hello 0.9.8 names do not include **Rm** (for example, New-AzureRmResourceGroup instead of New-AzureResourceGroup).</span></span> <span data-ttu-id="1f4df-112">При использовании Azure PowerShell 0.9.8, необходимо сначала включить режим диспетчера ресурсов hello, запустив hello **AzureResourceManager Switch-AzureMode** команды.</span><span class="sxs-lookup"><span data-stu-id="1f4df-112">When using Azure PowerShell 0.9.8, you must first enable hello Resource Manager mode by running hello **Switch-AzureMode AzureResourceManager** command.</span></span> <span data-ttu-id="1f4df-113">Эта команда не требуется в версии 1.0 и более поздних версиях.</span><span class="sxs-lookup"><span data-stu-id="1f4df-113">This command is not necessary in 1.0 or later.</span></span>

<span data-ttu-id="1f4df-114">Если требуется toouse в сценарии, написанные для среды hello 0.9.8, hello 1.0 или более поздней версии среды следует тщательно обновления и тестировать сценарии hello в тестовой среде перед их использованием в рабочей среде tooavoid непредвиденного влияния.</span><span class="sxs-lookup"><span data-stu-id="1f4df-114">If you want toouse your scripts written for hello 0.9.8 environment, in hello 1.0 or later environment, you should carefully update and test hello scripts in a pre-production environment before using them in production tooavoid unexpected impact.</span></span>

<span data-ttu-id="1f4df-115">[Загрузка последней версии PowerShell hello](https://github.com/Azure/azure-powershell/releases) (Минимальная требуемая версия —: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="1f4df-115">[Download hello latest PowerShell release](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>

[!INCLUDE [arm-getting-setup-powershell](../../includes/arm-getting-setup-powershell.md)]

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="1f4df-116">Создание хранилища служб восстановления</span><span class="sxs-lookup"><span data-stu-id="1f4df-116">Create a recovery services vault</span></span>
<span data-ttu-id="1f4df-117">Привет, следующие шаги, чтобы привести по созданию хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="1f4df-117">hello following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="1f4df-118">Хранилище служб восстановления отличается от хранилища службы архивации.</span><span class="sxs-lookup"><span data-stu-id="1f4df-118">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="1f4df-119">При использовании резервного копирования Azure для hello первый раз, необходимо использовать hello **AzureRMResourceProvider регистра** поставщика службы восстановления Azure hello tooregister командлетов с вашей подпиской.</span><span class="sxs-lookup"><span data-stu-id="1f4df-119">If you are using Azure Backup for hello first time, you must use hello **Register-AzureRMResourceProvider** cmdlet tooregister hello Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="1f4df-120">Hello хранилище служб восстановления это ARM ресурс, поэтому требуется tooplace его в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="1f4df-120">hello Recovery Services vault is an ARM resource, so you need tooplace it within a Resource Group.</span></span> <span data-ttu-id="1f4df-121">Вы можете выбрать существующую группу ресурсов или создать новую.</span><span class="sxs-lookup"><span data-stu-id="1f4df-121">You can use an existing resource group, or create a new one.</span></span> <span data-ttu-id="1f4df-122">При создании новой группы ресурсов, укажите hello имя и расположение для группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="1f4df-122">When creating a new resource group, specify hello name and location for hello resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "WestUS"
    ```
3. <span data-ttu-id="1f4df-123">Используйте hello **New AzureRmRecoveryServicesVault** командлет toocreate hello новое хранилище.</span><span class="sxs-lookup"><span data-stu-id="1f4df-123">Use hello **New-AzureRmRecoveryServicesVault** cmdlet toocreate hello new vault.</span></span> <span data-ttu-id="1f4df-124">Убедитесь, что toospecify hello одинаковое расположение для hello хранилище, которое использовалось для группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="1f4df-124">Be sure toospecify hello same location for hello vault as was used for hello resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "WestUS"
    ```
4. <span data-ttu-id="1f4df-125">Укажите тип hello toouse избыточности хранилища; можно использовать [локально избыточное хранилище (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) или [географически избыточное хранилище (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="1f4df-125">Specify hello type of storage redundancy toouse; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="1f4df-126">Hello следующий пример демонстрирует hello - BackupStorageRedundancy для testVault был установлен tooGeoRedundant.</span><span class="sxs-lookup"><span data-stu-id="1f4df-126">hello following example shows hello -BackupStorageRedundancy option for testVault is set tooGeoRedundant.</span></span>

   > [!TIP]
   > <span data-ttu-id="1f4df-127">Многие командлеты службы архивации Azure в качестве входных данных необходим объект хранилища служб восстановления hello.</span><span class="sxs-lookup"><span data-stu-id="1f4df-127">Many Azure Backup cmdlets require hello Recovery Services vault object as an input.</span></span> <span data-ttu-id="1f4df-128">По этой причине — это объект хранилища служб восстановления резервной копии удобный toostore hello в переменной.</span><span class="sxs-lookup"><span data-stu-id="1f4df-128">For this reason, it is convenient toostore hello Backup Recovery Services vault object in a variable.</span></span>
   >
   >

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

## <a name="view-hello-vaults-in-a-subscription"></a><span data-ttu-id="1f4df-129">Представление hello хранилища в подписке</span><span class="sxs-lookup"><span data-stu-id="1f4df-129">View hello vaults in a subscription</span></span>
<span data-ttu-id="1f4df-130">Используйте **Get AzureRmRecoveryServicesVault** tooview hello список всех хранилищ в текущей подписке hello.</span><span class="sxs-lookup"><span data-stu-id="1f4df-130">Use **Get-AzureRmRecoveryServicesVault** tooview hello list of all vaults in hello current subscription.</span></span> <span data-ttu-id="1f4df-131">Можно использовать этот toocheck команды создания нового хранилища или toosee какие хранилищами доступны в подписке hello.</span><span class="sxs-lookup"><span data-stu-id="1f4df-131">You can use this command toocheck that a new  vault was created, or toosee what vaults are available in hello subscription.</span></span>

<span data-ttu-id="1f4df-132">Выполните команду hello **Get AzureRmRecoveryServicesVault**, и перечислены все хранилища в подписке hello.</span><span class="sxs-lookup"><span data-stu-id="1f4df-132">Run hello command, **Get-AzureRmRecoveryServicesVault**, and all vaults in hello subscription are listed.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesVault
Name              : Contoso-vault
ID                : /subscriptions/1234
Type              : Microsoft.RecoveryServices/vaults
Location          : WestUS
ResourceGroupName : Contoso-docs-rg
SubscriptionId    : 1234-567f-8910-abc
Properties        : Microsoft.Azure.Commands.RecoveryServices.ARSVaultProperties
```


## <a name="installing-hello-azure-backup-agent"></a><span data-ttu-id="1f4df-133">Установка агента Azure Backup hello</span><span class="sxs-lookup"><span data-stu-id="1f4df-133">Installing hello Azure Backup agent</span></span>
<span data-ttu-id="1f4df-134">Перед установкой агента Azure Backup hello загружены и на приветствия Windows Server необходимо toohave hello установщика.</span><span class="sxs-lookup"><span data-stu-id="1f4df-134">Before you install hello Azure Backup agent, you need toohave hello installer downloaded and present on hello Windows Server.</span></span> <span data-ttu-id="1f4df-135">Можно получить последнюю версию установщика hello hello hello [центра загрузки Майкрософт](http://aka.ms/azurebackup_agent) или хранилище служб восстановления hello страницы панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="1f4df-135">You can get hello latest version of hello installer from hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from hello Recovery Services vault's Dashboard page.</span></span> <span data-ttu-id="1f4df-136">Сохранить hello установщика tooan легкодоступном месте как * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="1f4df-136">Save hello installer tooan easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="1f4df-137">Кроме того используйте загрузчик программы hello tooget PowerShell:</span><span class="sxs-lookup"><span data-stu-id="1f4df-137">Alternatively, use PowerShell tooget hello downloader:</span></span>
 
 ```
 $MarsAURL = 'Http://Aka.Ms/Azurebackup_Agent'
 $WC = New-Object System.Net.WebClient
 $WC.DownloadFile($MarsAURL,'C:\downloads\MARSAgentInstaller.EXE')
 C:\Downloads\MARSAgentInstaller.EXE /q
 ```

<span data-ttu-id="1f4df-138">tooinstall агент hello, запустите следующую команду в консоли PowerShell с повышенными hello:</span><span class="sxs-lookup"><span data-stu-id="1f4df-138">tooinstall hello agent, run hello following command in an elevated PowerShell console:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="1f4df-139">При этом устанавливаются hello агента со всеми параметрами по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="1f4df-139">This installs hello agent with all hello default options.</span></span> <span data-ttu-id="1f4df-140">Установка Hello занимает несколько минут в фоновом режиме hello.</span><span class="sxs-lookup"><span data-stu-id="1f4df-140">hello installation takes a few minutes in hello background.</span></span> <span data-ttu-id="1f4df-141">Если вы не укажете hello */nu* параметр, а затем hello **центра обновления Windows** окно в конце hello hello toocheck установки обновлений.</span><span class="sxs-lookup"><span data-stu-id="1f4df-141">If you do not specify hello */nu* option then hello **Windows Update** window will open at hello end of hello installation toocheck for any updates.</span></span> <span data-ttu-id="1f4df-142">После установки агент hello будет отображаться в списке установленных программ hello.</span><span class="sxs-lookup"><span data-stu-id="1f4df-142">Once installed, hello agent will show in hello list of installed programs.</span></span>

<span data-ttu-id="1f4df-143">toosee hello список установленных программ, перейдите в слишком**панели управления** > **программы** > **программы и компоненты**.</span><span class="sxs-lookup"><span data-stu-id="1f4df-143">toosee hello list of installed programs, go too**Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Агент установлен](./media/backup-client-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="1f4df-145">Параметры установки</span><span class="sxs-lookup"><span data-stu-id="1f4df-145">Installation options</span></span>
<span data-ttu-id="1f4df-146">toosee, Здравствуйте, все параметры, доступные через hello командной строки, выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="1f4df-146">toosee all hello options available via hello command-line, use hello following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="1f4df-147">Hello доступны следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="1f4df-147">hello available options include:</span></span>

| <span data-ttu-id="1f4df-148">Параметр</span><span class="sxs-lookup"><span data-stu-id="1f4df-148">Option</span></span> | <span data-ttu-id="1f4df-149">Сведения</span><span class="sxs-lookup"><span data-stu-id="1f4df-149">Details</span></span> | <span data-ttu-id="1f4df-150">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="1f4df-150">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1f4df-151">/q</span><span class="sxs-lookup"><span data-stu-id="1f4df-151">/q</span></span> |<span data-ttu-id="1f4df-152">Позволяет выполнить тихую установку.</span><span class="sxs-lookup"><span data-stu-id="1f4df-152">Quiet installation</span></span> |- |
| <span data-ttu-id="1f4df-153">/p:"расположение"</span><span class="sxs-lookup"><span data-stu-id="1f4df-153">/p:"location"</span></span> |<span data-ttu-id="1f4df-154">Путь toohello папку для установки агента Azure Backup hello.</span><span class="sxs-lookup"><span data-stu-id="1f4df-154">Path toohello installation folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="1f4df-155">C:\Program Files\Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="1f4df-155">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="1f4df-156">/s:"расположение"</span><span class="sxs-lookup"><span data-stu-id="1f4df-156">/s:"location"</span></span> |<span data-ttu-id="1f4df-157">Путь toohello для папки кэша hello Azure Backup agent.</span><span class="sxs-lookup"><span data-stu-id="1f4df-157">Path toohello cache folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="1f4df-158">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="1f4df-158">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="1f4df-159">/m</span><span class="sxs-lookup"><span data-stu-id="1f4df-159">/m</span></span> |<span data-ttu-id="1f4df-160">Участие в tooMicrosoft обновления</span><span class="sxs-lookup"><span data-stu-id="1f4df-160">Opt-in tooMicrosoft Update</span></span> |- |
| <span data-ttu-id="1f4df-161">/nu</span><span class="sxs-lookup"><span data-stu-id="1f4df-161">/nu</span></span> |<span data-ttu-id="1f4df-162">Позволяет отказаться от проверки наличия обновлений после завершения установки.</span><span class="sxs-lookup"><span data-stu-id="1f4df-162">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="1f4df-163">/d</span><span class="sxs-lookup"><span data-stu-id="1f4df-163">/d</span></span> |<span data-ttu-id="1f4df-164">Удаляет агент служб восстановления Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="1f4df-164">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="1f4df-165">/ph</span><span class="sxs-lookup"><span data-stu-id="1f4df-165">/ph</span></span> |<span data-ttu-id="1f4df-166">Адрес узла прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="1f4df-166">Proxy Host Address</span></span> |- |
| <span data-ttu-id="1f4df-167">/po</span><span class="sxs-lookup"><span data-stu-id="1f4df-167">/po</span></span> |<span data-ttu-id="1f4df-168">Номер порта узла прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="1f4df-168">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="1f4df-169">/pu</span><span class="sxs-lookup"><span data-stu-id="1f4df-169">/pu</span></span> |<span data-ttu-id="1f4df-170">Имя пользователя узла прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="1f4df-170">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="1f4df-171">/pw</span><span class="sxs-lookup"><span data-stu-id="1f4df-171">/pw</span></span> |<span data-ttu-id="1f4df-172">Пароль прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="1f4df-172">Proxy Password</span></span> |- |

## <a name="registering-windows-server-or-windows-client-machine-tooa-recovery-services-vault"></a><span data-ttu-id="1f4df-173">Регистрация Windows Server или Windows клиентского компьютера tooa хранилище служб восстановления</span><span class="sxs-lookup"><span data-stu-id="1f4df-173">Registering Windows Server or Windows client machine tooa Recovery Services Vault</span></span>
<span data-ttu-id="1f4df-174">После создания хранилище служб восстановления hello, загрузите последнюю версию агента hello и учетные данные хранилища hello и сохранить его в удобном месте, например C:\Downloads.</span><span class="sxs-lookup"><span data-stu-id="1f4df-174">After you created hello Recovery Services vault, download hello latest agent and hello vault credentials and store it in a convenient location like C:\Downloads.</span></span>

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
```

<span data-ttu-id="1f4df-175">На приветствия Windows Server или клиентский компьютер Windows, запустите hello [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) командлет tooregister hello машины с хранилищем hello.</span><span class="sxs-lookup"><span data-stu-id="1f4df-175">On hello Windows Server or Windows client machine, run hello [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet tooregister hello machine with hello vault.</span></span>
<span data-ttu-id="1f4df-176">Этот и другие командлеты, используемые для резервного копирования, являются модуль MSONLINE hello какие hello установщика агента Mars добавляется как часть процесса установки hello.</span><span class="sxs-lookup"><span data-stu-id="1f4df-176">This, and other cmdlets used for backup, are from hello MSONLINE module which hello Mars AgentInstaller added as part of hello installation process.</span></span> 

<span data-ttu-id="1f4df-177">Установка агента Hello не обновляет hello $Env: PSModulePath переменной.</span><span class="sxs-lookup"><span data-stu-id="1f4df-177">hello Agent installer does not update hello $Env:PSModulePath variable.</span></span> <span data-ttu-id="1f4df-178">Это означает, что автоматическая загрузка модуля завершается ошибкой.</span><span class="sxs-lookup"><span data-stu-id="1f4df-178">This means module auto-load fails.</span></span> <span data-ttu-id="1f4df-179">tooresolve это можно сделать hello следующее:</span><span class="sxs-lookup"><span data-stu-id="1f4df-179">tooresolve this you can do hello following:</span></span>

```
PS C:\>  $Env:psmodulepath += ';C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules
```

<span data-ttu-id="1f4df-180">Кроме того можно вручную загрузить модуль hello в скрипте следующим образом:</span><span class="sxs-lookup"><span data-stu-id="1f4df-180">Alternatively, you can manually load hello module in your script as follows:</span></span>

```
PS C:\>  Import-Module  'C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules\MSOnlineBackup'

```

<span data-ttu-id="1f4df-181">После загрузки командлеты оперативной архивации hello регистрации hello учетные данные хранилища:</span><span class="sxs-lookup"><span data-stu-id="1f4df-181">Once you load hello Online Backup cmdlets, you register hello vault credentials:</span></span>


```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration-VaultCredentials $cred -Confirm:$false
CertThumbprint      :7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName: testvault
Region              :WestUS
Machine registration succeeded.
```

> [!IMPORTANT]
> <span data-ttu-id="1f4df-182">Не используйте файл учетных данных хранилища hello toospecify относительные пути.</span><span class="sxs-lookup"><span data-stu-id="1f4df-182">Do not use relative paths toospecify hello vault credentials file.</span></span> <span data-ttu-id="1f4df-183">Необходимо указать абсолютный путь в качестве входного toohello командлета.</span><span class="sxs-lookup"><span data-stu-id="1f4df-183">You must provide an absolute path as an input toohello cmdlet.</span></span>
>
>

## <a name="networking-settings"></a><span data-ttu-id="1f4df-184">Параметры сети</span><span class="sxs-lookup"><span data-stu-id="1f4df-184">Networking settings</span></span>
<span data-ttu-id="1f4df-185">Если подключение hello hello Windows компьютера toohello является Интернет через прокси-сервер, параметры прокси-сервера hello также можно указать toohello агента.</span><span class="sxs-lookup"><span data-stu-id="1f4df-185">When hello connectivity of hello Windows machine toohello internet is through a proxy server, hello proxy settings can also be provided toohello agent.</span></span> <span data-ttu-id="1f4df-186">В нашем случае прокси-сервер не используется, поэтому мы явным образом удаляем все данные прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="1f4df-186">In this example, there is no proxy server, so we are explicitly clearing any proxy-related information.</span></span>

<span data-ttu-id="1f4df-187">Использование пропускной способности также можно управлять с помощью параметров hello ```work hour bandwidth``` и ```non-work hour bandwidth``` для заданного набора дней недели hello.</span><span class="sxs-lookup"><span data-stu-id="1f4df-187">Bandwidth usage can also be controlled with hello options of ```work hour bandwidth``` and ```non-work hour bandwidth``` for a given set of days of hello week.</span></span>

<span data-ttu-id="1f4df-188">Задания параметров прокси-сервера и пропускной способности hello осуществляется с помощью hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) командлета:</span><span class="sxs-lookup"><span data-stu-id="1f4df-188">Setting hello proxy and bandwidth details is done using hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span></span>

```
PS C:\> Set-OBMachineSetting -NoProxy
Server properties updated successfully.

PS C:\> Set-OBMachineSetting -NoThrottle
Server properties updated successfully.
```

## <a name="encryption-settings"></a><span data-ttu-id="1f4df-189">Параметры шифрования</span><span class="sxs-lookup"><span data-stu-id="1f4df-189">Encryption settings</span></span>
<span data-ttu-id="1f4df-190">tooAzure Hello резервного копирования данных, отправляемых резервной копии является зашифрованным tooprotect hello конфиденциальность данных hello.</span><span class="sxs-lookup"><span data-stu-id="1f4df-190">hello backup data sent tooAzure Backup is encrypted tooprotect hello confidentiality of hello data.</span></span> <span data-ttu-id="1f4df-191">Парольная фраза для шифрования Hello — hello «password» toodecrypt hello данные во время восстановления hello.</span><span class="sxs-lookup"><span data-stu-id="1f4df-191">hello encryption passphrase is hello "password" toodecrypt hello data at hello time of restore.</span></span>

```
PS C:\> ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force | Set-OBMachineSetting
PS C:\> $PassPhrase = ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force 
PS C:\> $PassCode   = 'AzureR0ckx'
PS C:\> Set-OBMachineSetting -EncryptionPassPhrase $PassPhrase
Server properties updated successfully
```

> [!IMPORTANT]
> <span data-ttu-id="1f4df-192">Обновление сведений парольную фразу hello надежным и безопасным, после ее установки.</span><span class="sxs-lookup"><span data-stu-id="1f4df-192">Keep hello passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="1f4df-193">Не быть может toorestore данные из Azure без этой парольной фразы.</span><span class="sxs-lookup"><span data-stu-id="1f4df-193">You are not be able toorestore data from Azure without this passphrase.</span></span>
>
>

## <a name="back-up-files-and-folders"></a><span data-ttu-id="1f4df-194">Резервное копирование файлов и папок</span><span class="sxs-lookup"><span data-stu-id="1f4df-194">Back up files and folders</span></span>
<span data-ttu-id="1f4df-195">Для политики определены все резервные копии из серверов и клиентов Windows tooAzure резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="1f4df-195">All backups from Windows Servers and clients tooAzure Backup are governed by a policy.</span></span> <span data-ttu-id="1f4df-196">Hello политики состоит из трех частей:</span><span class="sxs-lookup"><span data-stu-id="1f4df-196">hello policy comprises three parts:</span></span>

1. <span data-ttu-id="1f4df-197">Объект **расписание резервного копирования** , указывающий, когда архивы toobe выполнены и синхронизируются с hello службой.</span><span class="sxs-lookup"><span data-stu-id="1f4df-197">A **backup schedule** that specifies when backups need toobe taken and synchronized with hello service.</span></span>
2. <span data-ttu-id="1f4df-198">Объект **расписание хранения** , указывающее, как долго точки восстановления tooretain hello в Azure.</span><span class="sxs-lookup"><span data-stu-id="1f4df-198">A **retention schedule** that specifies how long tooretain hello recovery points in Azure.</span></span>
3. <span data-ttu-id="1f4df-199">**Указания включения/исключения файлов** — определяет, для каких элементов следует создавать резервные копии.</span><span class="sxs-lookup"><span data-stu-id="1f4df-199">A **file inclusion/exclusion specification** that dictates what should be backed up.</span></span>

<span data-ttu-id="1f4df-200">Поскольку мы будем использовать автоматическое резервное копирование данных, в этой статье предполагается, что заданных настроек нет.</span><span class="sxs-lookup"><span data-stu-id="1f4df-200">In this document, since we're automating backup, we'll assume nothing has been configured.</span></span> <span data-ttu-id="1f4df-201">Мы сначала необходимо создать новую политику резервного копирования, с помощью hello [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) командлета.</span><span class="sxs-lookup"><span data-stu-id="1f4df-201">We begin by creating a new backup policy using hello [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet.</span></span>

```
PS C:\> $newpolicy = New-OBPolicy
```

<span data-ttu-id="1f4df-202">В это время hello политики является пустым и другие командлеты, необходимые toodefine какие элементы будут включены или исключены, при резервные копии выполняются и Здравствуйте, где будут храниться резервные копии.</span><span class="sxs-lookup"><span data-stu-id="1f4df-202">At this time hello policy is empty and other cmdlets are needed toodefine what items will be included or excluded, when backups will run, and where hello backups will be stored.</span></span>

### <a name="configuring-hello-backup-schedule"></a><span data-ttu-id="1f4df-203">Настройка расписания резервного копирования hello</span><span class="sxs-lookup"><span data-stu-id="1f4df-203">Configuring hello backup schedule</span></span>
<span data-ttu-id="1f4df-204">Здравствуйте, сначала hello состоит из трех частей политики — расписание архивации hello, которое создается с помощью hello [New OBSchedule](https://technet.microsoft.com/library/hh770401) командлета.</span><span class="sxs-lookup"><span data-stu-id="1f4df-204">hello first of hello 3 parts of a policy is hello backup schedule, which is created using hello [New-OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet.</span></span> <span data-ttu-id="1f4df-205">расписание резервного копирования Hello определяет, когда архивы toobe копии.</span><span class="sxs-lookup"><span data-stu-id="1f4df-205">hello backup schedule defines when backups need toobe taken.</span></span> <span data-ttu-id="1f4df-206">При создании расписания необходимые toospecify 2 входных параметров.</span><span class="sxs-lookup"><span data-stu-id="1f4df-206">When creating a schedule you need toospecify 2 input parameters:</span></span>

* <span data-ttu-id="1f4df-207">**Дни недели hello** следует запускать эту резервную копию hello.</span><span class="sxs-lookup"><span data-stu-id="1f4df-207">**Days of hello week** that hello backup should run.</span></span> <span data-ttu-id="1f4df-208">Можно запустить задание резервного копирования hello только один день, или каждый день недели hello или любую комбинацию между ними.</span><span class="sxs-lookup"><span data-stu-id="1f4df-208">You can run hello backup job on just one day, or every day of hello week, or any combination in between.</span></span>
* <span data-ttu-id="1f4df-209">**Время суток hello** когда должно выполняться резервное копирование hello.</span><span class="sxs-lookup"><span data-stu-id="1f4df-209">**Times of hello day** when hello backup should run.</span></span> <span data-ttu-id="1f4df-210">Определяется too3 разное время суток hello, когда будут создаваться hello резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="1f4df-210">You can define up too3 different times of hello day when hello backup will be triggered.</span></span>

<span data-ttu-id="1f4df-211">Например, политику резервного копирования можно настроить таким образом, чтобы соответствующее задание выполнялось в 16:00 каждые субботу и воскресенье.</span><span class="sxs-lookup"><span data-stu-id="1f4df-211">For instance, you could configure a backup policy that runs at 4PM every Saturday and Sunday.</span></span>

```
PS C:\> $sched = New-OBSchedule -DaysofWeek Saturday, Sunday -TimesofDay 16:00
```

<span data-ttu-id="1f4df-212">расписание резервного копирования Hello требуется toobe, связанных с политикой, но это можно сделать с помощью hello [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) командлета.</span><span class="sxs-lookup"><span data-stu-id="1f4df-212">hello backup schedule needs toobe associated with a policy, and this can be achieved by using hello [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet.</span></span>

```
PS C:> Set-OBSchedule -Policy $newpolicy -Schedule $sched
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s) DsList : PolicyName : RetentionPolicy : State : New PolicyState : Valid
```
### <a name="configuring-a-retention-policy"></a><span data-ttu-id="1f4df-213">Настройка политики хранения</span><span class="sxs-lookup"><span data-stu-id="1f4df-213">Configuring a retention policy</span></span>
<span data-ttu-id="1f4df-214">Политика хранения Hello определяет продолжительность восстановления сохраняются точки, созданные из задания резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="1f4df-214">hello retention policy defines how long recovery points created from backup jobs are retained.</span></span> <span data-ttu-id="1f4df-215">При создании новой политики хранения с помощью hello [New OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) командлета, можно указать hello, сколько дней hello точки восстановления резервной копии должны toobe сохранило резервного копирования Azure.</span><span class="sxs-lookup"><span data-stu-id="1f4df-215">When creating a new retention policy using hello [New-OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet, you can specify hello number of days that hello backup recovery points need toobe retained with Azure Backup.</span></span> <span data-ttu-id="1f4df-216">пример Hello задана политика сохранения 7 дней.</span><span class="sxs-lookup"><span data-stu-id="1f4df-216">hello example below sets a retention policy of 7 days.</span></span>

```
PS C:\> $retentionpolicy = New-OBRetentionPolicy -RetentionDays 7
```

<span data-ttu-id="1f4df-217">Hello политика хранения должна быть связана hello основной политики с помощью командлета hello [OBRetentionPolicy набор](https://technet.microsoft.com/library/hh770405):</span><span class="sxs-lookup"><span data-stu-id="1f4df-217">hello retention policy must be associated with hello main policy using hello cmdlet [Set-OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span></span>

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
### <a name="including-and-excluding-files-toobe-backed-up"></a><span data-ttu-id="1f4df-218">Включение и исключение файлов toobe резервного копирования</span><span class="sxs-lookup"><span data-stu-id="1f4df-218">Including and excluding files toobe backed up</span></span>
<span data-ttu-id="1f4df-219">```OBFileSpec``` Объект определяет hello файлы toobe включен и исключен из резервной копии.</span><span class="sxs-lookup"><span data-stu-id="1f4df-219">An ```OBFileSpec``` object defines hello files toobe included and excluded in a backup.</span></span> <span data-ttu-id="1f4df-220">Это набор правил, что область out hello защищенных файлов и папок на компьютере.</span><span class="sxs-lookup"><span data-stu-id="1f4df-220">This is a set of rules that scope out hello protected files and folders on a machine.</span></span> <span data-ttu-id="1f4df-221">Можно создать любое количество правил включения или исключения файлов и связать их с политикой.</span><span class="sxs-lookup"><span data-stu-id="1f4df-221">You can have as many file inclusion or exclusion rules as required, and associate them with a policy.</span></span> <span data-ttu-id="1f4df-222">При создании нового объекта OBFileSpec, можно сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="1f4df-222">When creating a new OBFileSpec object, you can:</span></span>

* <span data-ttu-id="1f4df-223">Укажите hello файлов и папок toobe включены</span><span class="sxs-lookup"><span data-stu-id="1f4df-223">Specify hello files and folders toobe included</span></span>
* <span data-ttu-id="1f4df-224">Укажите hello файлов и папок toobe исключены</span><span class="sxs-lookup"><span data-stu-id="1f4df-224">Specify hello files and folders toobe excluded</span></span>
* <span data-ttu-id="1f4df-225">Укажите рекурсивные резервного копирования данных в папке (или) ли следует копировать только hello верхнего уровня файлы в указанной папке hello вверх.</span><span class="sxs-lookup"><span data-stu-id="1f4df-225">Specify recursive backup of data in a folder (or) whether only hello top-level files in hello specified folder should be backed up.</span></span>

<span data-ttu-id="1f4df-226">Hello последний достигается с помощью флага - нерекурсивных hello в команде New-OBFileSpec hello.</span><span class="sxs-lookup"><span data-stu-id="1f4df-226">hello latter is achieved by using hello -NonRecursive flag in hello New-OBFileSpec command.</span></span>

<span data-ttu-id="1f4df-227">В следующем примере hello мы резервное копирование тома C: и D: и исключить hello двоичных файлов операционной системы в папке Windows hello и любые временные папки.</span><span class="sxs-lookup"><span data-stu-id="1f4df-227">In hello example below, we'll back up volume C: and D: and exclude hello OS binaries in hello Windows folder and any temporary folders.</span></span> <span data-ttu-id="1f4df-228">toodo, поэтому мы создадим две спецификации файла с помощью hello [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) командлет - для включения и исключения.</span><span class="sxs-lookup"><span data-stu-id="1f4df-228">toodo so we'll create two file specifications using hello [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - one for inclusion and one for exclusion.</span></span> <span data-ttu-id="1f4df-229">После создания спецификации файла hello они связаны hello политики с помощью hello [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) командлета.</span><span class="sxs-lookup"><span data-stu-id="1f4df-229">Once hello file specifications have been created, they're associated with hello policy using hello [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet.</span></span>

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

### <a name="applying-hello-policy"></a><span data-ttu-id="1f4df-230">Применение политики hello</span><span class="sxs-lookup"><span data-stu-id="1f4df-230">Applying hello policy</span></span>
<span data-ttu-id="1f4df-231">Теперь hello объекта политики завершена и имеет связанное расписание резервного копирования, политика хранения и список включения и исключения файлов.</span><span class="sxs-lookup"><span data-stu-id="1f4df-231">Now hello policy object is complete and has an associated backup schedule, retention policy, and an inclusion/exclusion list of files.</span></span> <span data-ttu-id="1f4df-232">Эта политика теперь могут быть зафиксированы для toouse резервного копирования Azure.</span><span class="sxs-lookup"><span data-stu-id="1f4df-232">This policy can now be committed for Azure Backup toouse.</span></span> <span data-ttu-id="1f4df-233">Перед установкой hello вновь созданные политики убедитесь, что нет существующие политики резервного копирования, связанных с сервером hello с помощью hello [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) командлета.</span><span class="sxs-lookup"><span data-stu-id="1f4df-233">Before you apply hello newly created policy ensure that there are no existing backup policies associated with hello server by using hello [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet.</span></span> <span data-ttu-id="1f4df-234">Удаление политики hello выдаст запрос на подтверждение.</span><span class="sxs-lookup"><span data-stu-id="1f4df-234">Removing hello policy will prompt for confirmation.</span></span> <span data-ttu-id="1f4df-235">Подтверждение hello tooskip использовать hello ```-Confirm:$false``` флаг с командлетом hello.</span><span class="sxs-lookup"><span data-stu-id="1f4df-235">tooskip hello confirmation use hello ```-Confirm:$false``` flag with hello cmdlet.</span></span>

```
PS C:> Get-OBPolicy | Remove-OBPolicy
Microsoft Azure Backup Are you sure you want tooremove this backup policy? This will delete all hello backed up data. [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
```

<span data-ttu-id="1f4df-236">Слишком большой объем выделяемой объект политики hello выполняется с помощью hello [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) командлета.</span><span class="sxs-lookup"><span data-stu-id="1f4df-236">Committing hello policy object is done using hello [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet.</span></span> <span data-ttu-id="1f4df-237">При этом также будет запрашиваться соответствующее подтверждение.</span><span class="sxs-lookup"><span data-stu-id="1f4df-237">This will also ask for confirmation.</span></span> <span data-ttu-id="1f4df-238">Подтверждение hello tooskip использовать hello ```-Confirm:$false``` флаг с командлетом hello.</span><span class="sxs-lookup"><span data-stu-id="1f4df-238">tooskip hello confirmation use hello ```-Confirm:$false``` flag with hello cmdlet.</span></span>

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

<span data-ttu-id="1f4df-239">Вы можете просмотреть сведения hello hello существующие политики резервного копирования с помощью hello [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) командлета.</span><span class="sxs-lookup"><span data-stu-id="1f4df-239">You can view hello details of hello existing backup policy using hello [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet.</span></span> <span data-ttu-id="1f4df-240">Можно выполнять детализацию дальше с помощью hello [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) командлет расписание резервного копирования hello и hello [Get OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) командлета для политики хранения hello</span><span class="sxs-lookup"><span data-stu-id="1f4df-240">You can drill-down further using hello [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet for hello backup schedule and hello [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) cmdlet for hello retention policies</span></span>

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

### <a name="performing-an-ad-hoc-backup"></a><span data-ttu-id="1f4df-241">Выполнение нерегламентированного резервного копирования</span><span class="sxs-lookup"><span data-stu-id="1f4df-241">Performing an ad-hoc backup</span></span>
<span data-ttu-id="1f4df-242">После настройки политики резервного копирования резервных копий hello будет выполняться по расписанию hello.</span><span class="sxs-lookup"><span data-stu-id="1f4df-242">Once a backup policy has been set hello backups will occur per hello schedule.</span></span> <span data-ttu-id="1f4df-243">Резервное копирование ad-hoc запуска можно также с помощью hello [OBBackup начала](https://technet.microsoft.com/library/hh770426) командлета:</span><span class="sxs-lookup"><span data-stu-id="1f4df-243">Triggering an ad-hoc backup is also possible using hello [Start-OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:</span></span>

```
PS C:> Get-OBPolicy | Start-OBBackup
Initializing
Taking snapshot of volumes...
Preparing storage...
Generating backup metadata information and preparing hello metadata VHD...
Data transfer is in progress. It might take longer since it is hello first backup and all data needs toobe transferred...
Data transfer completed and all backed up data is in hello cloud. Verifying data integrity...
Data transfer completed
In progress...
Job completed.
hello backup operation completed successfully.
```

## <a name="restore-data-from-azure-backup"></a><span data-ttu-id="1f4df-244">Восстановление данных из службы архивации Azure</span><span class="sxs-lookup"><span data-stu-id="1f4df-244">Restore data from Azure Backup</span></span>
<span data-ttu-id="1f4df-245">Этот раздел поможет выполнить шаги hello для автоматического восстановления данных из резервной копии Azure.</span><span class="sxs-lookup"><span data-stu-id="1f4df-245">This section will guide you through hello steps for automating recovery of data from Azure Backup.</span></span> <span data-ttu-id="1f4df-246">Это включает в себя таким образом hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="1f4df-246">Doing so involves hello following steps:</span></span>

1. <span data-ttu-id="1f4df-247">Выберите исходный том hello</span><span class="sxs-lookup"><span data-stu-id="1f4df-247">Pick hello source volume</span></span>
2. <span data-ttu-id="1f4df-248">Выберите резервного копирования toorestore точки</span><span class="sxs-lookup"><span data-stu-id="1f4df-248">Choose a backup point toorestore</span></span>
3. <span data-ttu-id="1f4df-249">Выберите элемент toorestore</span><span class="sxs-lookup"><span data-stu-id="1f4df-249">Choose an item toorestore</span></span>
4. <span data-ttu-id="1f4df-250">Инициирующий процесс восстановления hello</span><span class="sxs-lookup"><span data-stu-id="1f4df-250">Trigger hello restore process</span></span>

### <a name="picking-hello-source-volume"></a><span data-ttu-id="1f4df-251">Комплектации hello исходного тома</span><span class="sxs-lookup"><span data-stu-id="1f4df-251">Picking hello source volume</span></span>
<span data-ttu-id="1f4df-252">В порядке toorestore элемент из резервного копирования Azure необходимо сначала tooidentify hello источник элемента hello.</span><span class="sxs-lookup"><span data-stu-id="1f4df-252">In order toorestore an item from Azure Backup, you first need tooidentify hello source of hello item.</span></span> <span data-ttu-id="1f4df-253">Поскольку команды hello выполнении в контексте сервера или клиента Windows hello, hello машины уже определен.</span><span class="sxs-lookup"><span data-stu-id="1f4df-253">Since we're executing hello commands in hello context of a Windows Server or a Windows client, hello machine is already identified.</span></span> <span data-ttu-id="1f4df-254">Hello следующим шагом в определение исходного hello — tooidentify hello том, содержащий его.</span><span class="sxs-lookup"><span data-stu-id="1f4df-254">hello next step in identifying hello source is tooidentify hello volume containing it.</span></span> <span data-ttu-id="1f4df-255">Список томов или источников резервного копирования с этого компьютера можно получить, выполнив hello [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) командлета.</span><span class="sxs-lookup"><span data-stu-id="1f4df-255">A list of volumes or sources being backed up from this machine can be retrieved by executing hello [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet.</span></span> <span data-ttu-id="1f4df-256">Эта команда возвращает массив всех источников hello, полученные с сервера и клиента.</span><span class="sxs-lookup"><span data-stu-id="1f4df-256">This command returns an array of all hello sources backed up from this server/client.</span></span>

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

### <a name="choosing-a-backup-point-from-which-toorestore"></a><span data-ttu-id="1f4df-257">Выбрав какие toorestore точки резервного копирования</span><span class="sxs-lookup"><span data-stu-id="1f4df-257">Choosing a backup point from which toorestore</span></span>
<span data-ttu-id="1f4df-258">Получить список точек резервного копирования, выполнив hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) командлет с соответствующими параметрами.</span><span class="sxs-lookup"><span data-stu-id="1f4df-258">You retreive a list of backup points by executing hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet with appropriate parameters.</span></span> <span data-ttu-id="1f4df-259">В нашем примере мы выберем hello последней резервной копии точки для исходного тома hello *D:* и использовать его toorecover определенного файла.</span><span class="sxs-lookup"><span data-stu-id="1f4df-259">In our example, we’ll choose hello latest backup point for hello source volume *D:* and use it toorecover a specific file.</span></span>

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
<span data-ttu-id="1f4df-260">Hello объекта ```$rps``` является массивом точек резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="1f4df-260">hello object ```$rps``` is an array of backup points.</span></span> <span data-ttu-id="1f4df-261">Hello первый элемент является последней точки hello и n-й элемент hello — самая старая точка hello.</span><span class="sxs-lookup"><span data-stu-id="1f4df-261">hello first element is hello latest point and hello Nth element is hello oldest point.</span></span> <span data-ttu-id="1f4df-262">Последняя точка toochoose hello, мы будем использовать ```$rps[0]```.</span><span class="sxs-lookup"><span data-stu-id="1f4df-262">toochoose hello latest point, we will use ```$rps[0]```.</span></span>

### <a name="choosing-an-item-toorestore"></a><span data-ttu-id="1f4df-263">Выбор элемента toorestore</span><span class="sxs-lookup"><span data-stu-id="1f4df-263">Choosing an item toorestore</span></span>
<span data-ttu-id="1f4df-264">использовать tooidentify hello точное файл или папка toorestore, рекурсивно hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) командлета.</span><span class="sxs-lookup"><span data-stu-id="1f4df-264">tooidentify hello exact file or folder toorestore, recursively use hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet.</span></span> <span data-ttu-id="1f4df-265">Иерархии папок hello этот способ можно просматривать только с помощью hello ```Get-OBRecoverableItem```.</span><span class="sxs-lookup"><span data-stu-id="1f4df-265">That way hello folder hierarchy can be browsed solely using hello ```Get-OBRecoverableItem```.</span></span>

<span data-ttu-id="1f4df-266">В этом примере, если мы хотим файл hello toorestore *finances.xls* мы ссылаться, используя hello объекта ```$filesFolders[1]```.</span><span class="sxs-lookup"><span data-stu-id="1f4df-266">In this example, if we want toorestore hello file *finances.xls* we can reference that using hello object ```$filesFolders[1]```.</span></span>

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

<span data-ttu-id="1f4df-267">Можно также выполнить поиск toorestore элементов с помощью hello ```Get-OBRecoverableItem``` командлета.</span><span class="sxs-lookup"><span data-stu-id="1f4df-267">You can also search for items toorestore using hello ```Get-OBRecoverableItem``` cmdlet.</span></span> <span data-ttu-id="1f4df-268">В нашем примере toosearch для *finances.xls* удалось получить дескриптор файла hello, запустив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="1f4df-268">In our example, toosearch for *finances.xls* we could get a handle on hello file by running this command:</span></span>

```
PS C:\> $item = Get-OBRecoverableItem -RecoveryPoint $rps[0] -Location "D:\MyData" -SearchString "finance*"
```

### <a name="triggering-hello-restore-process"></a><span data-ttu-id="1f4df-269">Запуск процесса восстановления hello</span><span class="sxs-lookup"><span data-stu-id="1f4df-269">Triggering hello restore process</span></span>
<span data-ttu-id="1f4df-270">процесс восстановления tootrigger hello, необходимо сначала параметры восстановления toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="1f4df-270">tootrigger hello restore process, we first need toospecify hello recovery options.</span></span> <span data-ttu-id="1f4df-271">Это можно сделать с помощью hello [New OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) командлета.</span><span class="sxs-lookup"><span data-stu-id="1f4df-271">This can be done by using hello [New-OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet.</span></span> <span data-ttu-id="1f4df-272">Например, предположим, что файлы hello toorestore мы хотим слишком*C:\temp*. Также предположим, что мы хотим tooskip существующие файлы в папку назначения hello *C:\temp*. toocreate такой вариант восстановления, используйте hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="1f4df-272">For this example, let's assume that we want toorestore hello files too*C:\temp*. Let's also assume that we want tooskip files that already exist on hello destination folder *C:\temp*. toocreate such a recovery option, use hello following command:</span></span>

```
PS C:\> $recovery_option = New-OBRecoveryOption -DestinationPath "C:\temp" -OverwriteType Skip
```

<span data-ttu-id="1f4df-273">Теперь запускать hello процесса восстановления с помощью hello [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) на выбранных hello ```$item``` из вывода hello hello ```Get-OBRecoverableItem``` командлета:</span><span class="sxs-lookup"><span data-stu-id="1f4df-273">Now trigger hello restore process by using hello [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) command on hello selected ```$item``` from hello output of hello ```Get-OBRecoverableItem``` cmdlet:</span></span>

```
PS C:\> Start-OBRecovery -RecoverableItem $item -RecoveryOption $recover_option
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Job completed.
hello recovery operation completed successfully.
```


## <a name="uninstalling-hello-azure-backup-agent"></a><span data-ttu-id="1f4df-274">Удаление агента Azure Backup hello</span><span class="sxs-lookup"><span data-stu-id="1f4df-274">Uninstalling hello Azure Backup agent</span></span>
<span data-ttu-id="1f4df-275">Удаление агента Azure Backup hello можно сделать с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="1f4df-275">Uninstalling hello Azure Backup agent can be done by using hello following command:</span></span>

```
PS C:\> .\MARSAgentInstaller.exe /d /q
```

<span data-ttu-id="1f4df-276">При удалении hello двоичные файлы агента с компьютера hello имеет некоторые последствия tooconsider:</span><span class="sxs-lookup"><span data-stu-id="1f4df-276">Uninstalling hello agent binaries from hello machine has some consequences tooconsider:</span></span>

* <span data-ttu-id="1f4df-277">Удаляет фильтр файлов hello из машины hello и остановить отслеживание изменений.</span><span class="sxs-lookup"><span data-stu-id="1f4df-277">It removes hello file-filter from hello machine, and tracking of changes is stopped.</span></span>
* <span data-ttu-id="1f4df-278">Все данные политики удаляется с компьютера hello, но сведения о политике hello продолжается toobe хранятся в службе hello.</span><span class="sxs-lookup"><span data-stu-id="1f4df-278">All policy information is removed from hello machine, but hello policy information continues toobe stored in hello service.</span></span>
* <span data-ttu-id="1f4df-279">Удаляются все расписания резервного копирования, и последующие операции резервного копирования больше не выполняются.</span><span class="sxs-lookup"><span data-stu-id="1f4df-279">All backup schedules are removed, and no further backups are taken.</span></span>

<span data-ttu-id="1f4df-280">Однако hello данные хранятся в Azure остается и сохраняются согласно установки политики хранения hello вами.</span><span class="sxs-lookup"><span data-stu-id="1f4df-280">However, hello data stored in Azure remains and is retained as per hello retention policy setup by you.</span></span> <span data-ttu-id="1f4df-281">Предыдущие точки восстановления автоматически рассматриваются как устаревшие.</span><span class="sxs-lookup"><span data-stu-id="1f4df-281">Older points are automatically aged out.</span></span>

## <a name="remote-management"></a><span data-ttu-id="1f4df-282">Удаленное управление</span><span class="sxs-lookup"><span data-stu-id="1f4df-282">Remote management</span></span>
<span data-ttu-id="1f4df-283">Все управление hello вокруг hello Azure Backup agent, политики и источников данных может быть выполнена удаленно с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1f4df-283">All hello management around hello Azure Backup agent, policies, and data sources can be done remotely through PowerShell.</span></span> <span data-ttu-id="1f4df-284">Привет, удаленное управление компьютеру toobe правильно подготовлен.</span><span class="sxs-lookup"><span data-stu-id="1f4df-284">hello machine that will be managed remotely needs toobe prepared correctly.</span></span>

<span data-ttu-id="1f4df-285">По умолчанию служба удаленного управления Windows hello настроена на запуск вручную.</span><span class="sxs-lookup"><span data-stu-id="1f4df-285">By default, hello WinRM service is configured for manual startup.</span></span> <span data-ttu-id="1f4df-286">Тип запуска Hello должен быть установлен слишком*автоматического* и hello служба должна быть запущена.</span><span class="sxs-lookup"><span data-stu-id="1f4df-286">hello startup type must be set too*Automatic* and hello service should be started.</span></span> <span data-ttu-id="1f4df-287">tooverify, hello служба WinRM запущена, значение свойства Status hello hello должно быть *под управлением*.</span><span class="sxs-lookup"><span data-stu-id="1f4df-287">tooverify that hello WinRM service is running, hello value of hello Status property should be *Running*.</span></span>

```
PS C:\> Get-Service WinRM

Status   Name               DisplayName
------   ----               -----------
Running  winrm              Windows Remote Management (WS-Manag...
```

<span data-ttu-id="1f4df-288">Для удаленного взаимодействия необходимо настроить PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1f4df-288">PowerShell should be configured for remoting.</span></span>

```
PS C:\> Enable-PSRemoting -force
WinRM is already set up tooreceive requests on this computer.
WinRM has been updated for remote management.
WinRM firewall exception enabled.

PS C:\> Set-ExecutionPolicy unrestricted -force
```

<span data-ttu-id="1f4df-289">машины Hello теперь можно управлять удаленно — начиная с установки hello hello агента.</span><span class="sxs-lookup"><span data-stu-id="1f4df-289">hello machine can now be managed remotely - starting from hello installation of hello agent.</span></span> <span data-ttu-id="1f4df-290">Например следующий скрипт hello копирует hello агента toohello удаленный компьютер и устанавливает его.</span><span class="sxs-lookup"><span data-stu-id="1f4df-290">For example, hello following script copies hello agent toohello remote machine and installs it.</span></span>

```
PS C:\> $dloc = "\\REMOTESERVER01\c$\Windows\Temp"
PS C:\> $agent = "\\REMOTESERVER01\c$\Windows\Temp\MARSAgentInstaller.exe"
PS C:\> $args = "/q"
PS C:\> Copy-Item "C:\Downloads\MARSAgentInstaller.exe" -Destination $dloc - force

PS C:\> $s = New-PSSession -ComputerName REMOTESERVER01
PS C:\> Invoke-Command -Session $s -Script { param($d, $a) Start-Process -FilePath $d $a -Wait } -ArgumentList $agent $args
```

## <a name="next-steps"></a><span data-ttu-id="1f4df-291">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1f4df-291">Next steps</span></span>
<span data-ttu-id="1f4df-292">Дополнительная информация о службе архивации Azure для сервера или клиента Windows</span><span class="sxs-lookup"><span data-stu-id="1f4df-292">For more information about Azure Backup for Windows Server/Client see</span></span>

* [<span data-ttu-id="1f4df-293">Введение tooAzure резервной копии</span><span class="sxs-lookup"><span data-stu-id="1f4df-293">Introduction tooAzure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="1f4df-294">Резервное копирование серверов Windows</span><span class="sxs-lookup"><span data-stu-id="1f4df-294">Back up Windows Servers</span></span>](backup-configure-vault.md)
