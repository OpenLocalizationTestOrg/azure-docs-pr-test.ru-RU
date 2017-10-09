---
title: "резервное копирование - с помощью PowerShell tooback копирование рабочих нагрузок DPM aaaAzure | Документы Microsoft"
description: "Узнайте, как toodeploy и управление резервным копированием Azure для Data Protection Manager (DPM) с помощью PowerShell"
services: backup
documentationcenter: 
author: NKolli1
manager: shreeshd
editor: 
ms.assetid: e9bd223c-2398-4eb1-9bf3-50e08970fea7
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 1/23/2017
ms.author: adigan;anuragm;trinadhk;markgal
ms.openlocfilehash: 27d2b4b3127b68c9da564697eb61dc3ccbc34b3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-data-protection-manager-dpm-servers-using-powershell"></a><span data-ttu-id="6a428-103">Развертывание и управление ими tooAzure резервного копирования для серверов Data Protection Manager (DPM), с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="6a428-103">Deploy and manage backup tooAzure for Data Protection Manager (DPM) servers using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6a428-104">ARM</span><span class="sxs-lookup"><span data-stu-id="6a428-104">ARM</span></span>](backup-dpm-automation.md)
> * [<span data-ttu-id="6a428-105">Классический</span><span class="sxs-lookup"><span data-stu-id="6a428-105">Classic</span></span>](backup-dpm-automation-classic.md)
>
>

<span data-ttu-id="6a428-106">В этой статье показано, как toouse toosetup PowerShell Azure Backup на сервере DPM и toomanage резервного копирования и восстановления.</span><span class="sxs-lookup"><span data-stu-id="6a428-106">This article shows you how toouse PowerShell toosetup Azure Backup on a DPM server, and toomanage backup and recovery.</span></span>

## <a name="setting-up-hello-powershell-environment"></a><span data-ttu-id="6a428-107">Настройка среды PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="6a428-107">Setting up hello PowerShell environment</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="6a428-108">Прежде чем использовать PowerShell toomanage из резервных копий с tooAzure Data Protection Manager, необходимо справа среде toohave hello в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6a428-108">Before you can use PowerShell toomanage backups from Data Protection Manager tooAzure, you need toohave hello right environment in PowerShell.</span></span> <span data-ttu-id="6a428-109">В начале сеанса PowerShell hello hello убедитесь, что запустить hello, следующая команда tooimport hello правой модули и позволяют командлеты DPM hello toocorrectly ссылку:</span><span class="sxs-lookup"><span data-stu-id="6a428-109">At hello start of hello PowerShell session, ensure that you run hello following command tooimport hello right modules and allow you toocorrectly reference hello DPM cmdlets:</span></span>

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

## <a name="setup-and-registration"></a><span data-ttu-id="6a428-110">Настройка и регистрация</span><span class="sxs-lookup"><span data-stu-id="6a428-110">Setup and Registration</span></span>
<span data-ttu-id="6a428-111">toobegin:</span><span class="sxs-lookup"><span data-stu-id="6a428-111">toobegin:</span></span>

1. <span data-ttu-id="6a428-112">[Скачайте последнюю версию PowerShell](https://github.com/Azure/azure-powershell/releases) (минимальная требуемая версия: 1.0.0).</span><span class="sxs-lookup"><span data-stu-id="6a428-112">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is: 1.0.0)</span></span>
2. <span data-ttu-id="6a428-113">Включения командлетов резервного копирования Azure hello переключив слишком*AzureResourceManager* режиме с помощью hello **Switch-AzureMode** командлетов для:</span><span class="sxs-lookup"><span data-stu-id="6a428-113">Enable hello Azure Backup commandlets by switching too*AzureResourceManager* mode by using hello **Switch-AzureMode** commandlet:</span></span>

```
PS C:\> Switch-AzureMode AzureResourceManager
```

<span data-ttu-id="6a428-114">Hello следующие программы установки и регистрации задачи можно автоматизировать с помощью PowerShell:</span><span class="sxs-lookup"><span data-stu-id="6a428-114">hello following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="6a428-115">Создание хранилища служб восстановления</span><span class="sxs-lookup"><span data-stu-id="6a428-115">Create a Recovery Services vault</span></span>
* <span data-ttu-id="6a428-116">Установка агента Azure Backup hello</span><span class="sxs-lookup"><span data-stu-id="6a428-116">Installing hello Azure Backup agent</span></span>
* <span data-ttu-id="6a428-117">Регистрация hello службы архивации Azure</span><span class="sxs-lookup"><span data-stu-id="6a428-117">Registering with hello Azure Backup service</span></span>
* <span data-ttu-id="6a428-118">Параметры сети</span><span class="sxs-lookup"><span data-stu-id="6a428-118">Networking settings</span></span>
* <span data-ttu-id="6a428-119">Параметры шифрования</span><span class="sxs-lookup"><span data-stu-id="6a428-119">Encryption settings</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="6a428-120">Создание хранилища служб восстановления</span><span class="sxs-lookup"><span data-stu-id="6a428-120">Create a recovery services vault</span></span>
<span data-ttu-id="6a428-121">Привет, следующие шаги, чтобы привести по созданию хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="6a428-121">hello following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="6a428-122">Хранилище служб восстановления отличается от хранилища службы архивации.</span><span class="sxs-lookup"><span data-stu-id="6a428-122">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="6a428-123">При использовании резервного копирования Azure для hello первый раз, необходимо использовать hello **AzureRMResourceProvider регистра** поставщика службы восстановления Azure hello tooregister командлетов с вашей подпиской.</span><span class="sxs-lookup"><span data-stu-id="6a428-123">If you are using Azure Backup for hello first time, you must use hello **Register-AzureRMResourceProvider** cmdlet tooregister hello Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="6a428-124">Hello хранилище служб восстановления это ARM ресурс, поэтому требуется tooplace его в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6a428-124">hello Recovery Services vault is an ARM resource, so you need tooplace it within a Resource Group.</span></span> <span data-ttu-id="6a428-125">Вы можете выбрать существующую группу ресурсов или создать новую.</span><span class="sxs-lookup"><span data-stu-id="6a428-125">You can use an existing resource group, or create a new one.</span></span> <span data-ttu-id="6a428-126">При создании новой группы ресурсов, укажите hello имя и расположение для группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="6a428-126">When creating a new resource group, specify hello name and location for hello resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. <span data-ttu-id="6a428-127">Используйте hello **New AzureRmRecoveryServicesVault** toocreate командлет новое хранилище.</span><span class="sxs-lookup"><span data-stu-id="6a428-127">Use hello **New-AzureRmRecoveryServicesVault** cmdlet toocreate a new vault.</span></span> <span data-ttu-id="6a428-128">Убедитесь, что toospecify hello одинаковое расположение для hello хранилище, которое использовалось для группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="6a428-128">Be sure toospecify hello same location for hello vault as was used for hello resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. <span data-ttu-id="6a428-129">Укажите тип hello toouse избыточности хранилища; можно использовать [локально избыточное хранилище (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) или [географически избыточное хранилище (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="6a428-129">Specify hello type of storage redundancy toouse; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="6a428-130">Hello следующий пример демонстрирует hello - BackupStorageRedundancy для testVault был установлен tooGeoRedundant.</span><span class="sxs-lookup"><span data-stu-id="6a428-130">hello following example shows hello -BackupStorageRedundancy option for testVault is set tooGeoRedundant.</span></span>

   > [!TIP]
   > <span data-ttu-id="6a428-131">Многие командлеты службы архивации Azure в качестве входных данных необходим объект хранилища служб восстановления hello.</span><span class="sxs-lookup"><span data-stu-id="6a428-131">Many Azure Backup cmdlets require hello Recovery Services vault object as an input.</span></span> <span data-ttu-id="6a428-132">По этой причине — это объект хранилища служб восстановления резервной копии удобный toostore hello в переменной.</span><span class="sxs-lookup"><span data-stu-id="6a428-132">For this reason, it is convenient toostore hello Backup Recovery Services vault object in a variable.</span></span>
   >
   >

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

## <a name="view-hello-vaults-in-a-subscription"></a><span data-ttu-id="6a428-133">Представление hello хранилища в подписке</span><span class="sxs-lookup"><span data-stu-id="6a428-133">View hello vaults in a subscription</span></span>
<span data-ttu-id="6a428-134">Используйте **Get AzureRmRecoveryServicesVault** tooview hello список всех хранилищ в текущей подписке hello.</span><span class="sxs-lookup"><span data-stu-id="6a428-134">Use **Get-AzureRmRecoveryServicesVault** tooview hello list of all vaults in hello current subscription.</span></span> <span data-ttu-id="6a428-135">Можно использовать этот toocheck команды создания нового хранилища или toosee какие хранилищами доступны в подписке hello.</span><span class="sxs-lookup"><span data-stu-id="6a428-135">You can use this command toocheck that a new  vault was created, or toosee what vaults are available in hello subscription.</span></span>

<span data-ttu-id="6a428-136">Отображаются все хранилища в подписке hello и выполните команду hello, Get-AzureRmRecoveryServicesVault.</span><span class="sxs-lookup"><span data-stu-id="6a428-136">Run hello command, Get-AzureRmRecoveryServicesVault, and all vaults in hello subscription are listed.</span></span>

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


## <a name="installing-hello-azure-backup-agent-on-a-dpm-server"></a><span data-ttu-id="6a428-137">Установка агента Azure Backup hello на сервере DPM</span><span class="sxs-lookup"><span data-stu-id="6a428-137">Installing hello Azure Backup agent on a DPM Server</span></span>
<span data-ttu-id="6a428-138">Перед установкой агента Azure Backup hello загружены и на приветствия Windows Server необходимо toohave hello установщика.</span><span class="sxs-lookup"><span data-stu-id="6a428-138">Before you install hello Azure Backup agent, you need toohave hello installer downloaded and present on hello Windows Server.</span></span> <span data-ttu-id="6a428-139">Можно получить последнюю версию установщика hello hello hello [центра загрузки Майкрософт](http://aka.ms/azurebackup_agent) или хранилище служб восстановления hello страницы панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="6a428-139">You can get hello latest version of hello installer from hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from hello Recovery Services vault's Dashboard page.</span></span> <span data-ttu-id="6a428-140">Сохранить hello установщика tooan легкодоступном месте как * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="6a428-140">Save hello installer tooan easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="6a428-141">агент hello tooinstall, запустите следующую команду в консоли PowerShell с повышенными hello **на сервере DPM hello**:</span><span class="sxs-lookup"><span data-stu-id="6a428-141">tooinstall hello agent, run hello following command in an elevated PowerShell console **on hello DPM server**:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="6a428-142">При этом устанавливаются hello агента со всеми параметрами по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="6a428-142">This installs hello agent with all hello default options.</span></span> <span data-ttu-id="6a428-143">Установка Hello занимает несколько минут в фоновом режиме hello.</span><span class="sxs-lookup"><span data-stu-id="6a428-143">hello installation takes a few minutes in hello background.</span></span> <span data-ttu-id="6a428-144">Если вы не укажете hello */nu* hello параметр **центра обновления Windows** открывается окно в конце hello hello toocheck установки обновлений.</span><span class="sxs-lookup"><span data-stu-id="6a428-144">If you do not specify hello */nu* option hello **Windows Update** window opens at hello end of hello installation toocheck for any updates.</span></span>

<span data-ttu-id="6a428-145">Hello агента отображается в списке установленных программ hello.</span><span class="sxs-lookup"><span data-stu-id="6a428-145">hello agent shows up in hello list of installed programs.</span></span> <span data-ttu-id="6a428-146">toosee hello список установленных программ, перейдите в слишком**панели управления** > **программы** > **программы и компоненты**.</span><span class="sxs-lookup"><span data-stu-id="6a428-146">toosee hello list of installed programs, go too**Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Агент установлен](./media/backup-dpm-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="6a428-148">Параметры установки</span><span class="sxs-lookup"><span data-stu-id="6a428-148">Installation options</span></span>
<span data-ttu-id="6a428-149">toosee все параметры hello, доступные через командную строку hello, hello используйте следующие команды:</span><span class="sxs-lookup"><span data-stu-id="6a428-149">toosee all hello options available via hello commandline, use hello following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="6a428-150">Hello доступны следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="6a428-150">hello available options include:</span></span>

| <span data-ttu-id="6a428-151">Параметр</span><span class="sxs-lookup"><span data-stu-id="6a428-151">Option</span></span> | <span data-ttu-id="6a428-152">Сведения</span><span class="sxs-lookup"><span data-stu-id="6a428-152">Details</span></span> | <span data-ttu-id="6a428-153">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="6a428-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6a428-154">/q</span><span class="sxs-lookup"><span data-stu-id="6a428-154">/q</span></span> |<span data-ttu-id="6a428-155">Позволяет выполнить тихую установку.</span><span class="sxs-lookup"><span data-stu-id="6a428-155">Quiet installation</span></span> |- |
| <span data-ttu-id="6a428-156">/p:"расположение"</span><span class="sxs-lookup"><span data-stu-id="6a428-156">/p:"location"</span></span> |<span data-ttu-id="6a428-157">Путь toohello папку для установки агента Azure Backup hello.</span><span class="sxs-lookup"><span data-stu-id="6a428-157">Path toohello installation folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="6a428-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="6a428-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="6a428-159">/s:"расположение"</span><span class="sxs-lookup"><span data-stu-id="6a428-159">/s:"location"</span></span> |<span data-ttu-id="6a428-160">Путь toohello для папки кэша hello Azure Backup agent.</span><span class="sxs-lookup"><span data-stu-id="6a428-160">Path toohello cache folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="6a428-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="6a428-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="6a428-162">/m</span><span class="sxs-lookup"><span data-stu-id="6a428-162">/m</span></span> |<span data-ttu-id="6a428-163">Участие в tooMicrosoft обновления</span><span class="sxs-lookup"><span data-stu-id="6a428-163">Opt-in tooMicrosoft Update</span></span> |- |
| <span data-ttu-id="6a428-164">/nu</span><span class="sxs-lookup"><span data-stu-id="6a428-164">/nu</span></span> |<span data-ttu-id="6a428-165">Позволяет отказаться от проверки наличия обновлений после завершения установки.</span><span class="sxs-lookup"><span data-stu-id="6a428-165">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="6a428-166">/d</span><span class="sxs-lookup"><span data-stu-id="6a428-166">/d</span></span> |<span data-ttu-id="6a428-167">Удаляет агент служб восстановления Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="6a428-167">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="6a428-168">/ph</span><span class="sxs-lookup"><span data-stu-id="6a428-168">/ph</span></span> |<span data-ttu-id="6a428-169">Адрес узла прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="6a428-169">Proxy Host Address</span></span> |- |
| <span data-ttu-id="6a428-170">/po</span><span class="sxs-lookup"><span data-stu-id="6a428-170">/po</span></span> |<span data-ttu-id="6a428-171">Номер порта узла прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="6a428-171">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="6a428-172">/pu</span><span class="sxs-lookup"><span data-stu-id="6a428-172">/pu</span></span> |<span data-ttu-id="6a428-173">Имя пользователя узла прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="6a428-173">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="6a428-174">/pw</span><span class="sxs-lookup"><span data-stu-id="6a428-174">/pw</span></span> |<span data-ttu-id="6a428-175">Пароль прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="6a428-175">Proxy Password</span></span> |- |

## <a name="registering-dpm-tooa-recovery-services-vault"></a><span data-ttu-id="6a428-176">Регистрация DPM tooa хранилище служб восстановления</span><span class="sxs-lookup"><span data-stu-id="6a428-176">Registering DPM tooa Recovery Services Vault</span></span>
<span data-ttu-id="6a428-177">После создания хранилище служб восстановления hello, загрузите последнюю версию агента hello и учетные данные хранилища hello и сохранить его в удобном месте, например C:\Downloads.</span><span class="sxs-lookup"><span data-stu-id="6a428-177">After you created hello Recovery Services vault, download hello latest agent and hello vault credentials and store it in a convenient location like C:\Downloads.</span></span>

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
PS C:\> $credsfilename
C:\downloads\testvault\_Sun Apr 10 2016.VaultCredentials
```

<span data-ttu-id="6a428-178">На сервере DPM hello выполните hello [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) командлет tooregister hello машины с хранилищем hello.</span><span class="sxs-lookup"><span data-stu-id="6a428-178">On hello DPM server, run hello [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet tooregister hello machine with hello vault.</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration-VaultCredentials $cred -Confirm:$false
CertThumbprint      :7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName: testvault
Region              :West US
Machine registration succeeded.
```

### <a name="initial-configuration-settings"></a><span data-ttu-id="6a428-179">Исходные параметры конфигурации</span><span class="sxs-lookup"><span data-stu-id="6a428-179">Initial configuration settings</span></span>
<span data-ttu-id="6a428-180">После регистрации сервера DPM hello с hello хранилище служб восстановления, он запускается с параметрами по умолчанию подписки.</span><span class="sxs-lookup"><span data-stu-id="6a428-180">Once hello DPM Server is registered with hello Recovery Services vault, it starts with default subscription settings.</span></span> <span data-ttu-id="6a428-181">Эти параметры подписки включают сетью, шифрования и hello промежуточной области.</span><span class="sxs-lookup"><span data-stu-id="6a428-181">These subscription settings include Networking, Encryption and hello Staging area.</span></span> <span data-ttu-id="6a428-182">Параметры подписки toochange необходимо toofirst справиться с hello существующие (по умолчанию), параметры с помощью hello [Get DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) командлета:</span><span class="sxs-lookup"><span data-stu-id="6a428-182">toochange subscription settings you need toofirst get a handle on hello existing (default) settings using hello [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span></span>

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

<span data-ttu-id="6a428-183">Локальный объект PowerShell toothis сделанных изменений, которые ```$setting``` и hello полный объект будет зафиксирована tooDPM и резервного копирования Azure toosave их с помощью hello [DPMCloudSubscriptionSetting набор](https://technet.microsoft.com/library/jj612791) командлета.</span><span class="sxs-lookup"><span data-stu-id="6a428-183">All modifications are made toothis local PowerShell object ```$setting```  and then hello full object is committed tooDPM and Azure Backup toosave them using hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="6a428-184">Требуется toouse hello ```–Commit``` tooensure флаг, который hello изменения сохраняются.</span><span class="sxs-lookup"><span data-stu-id="6a428-184">You need toouse hello ```–Commit``` flag tooensure that hello changes are persisted.</span></span> <span data-ttu-id="6a428-185">Параметры Hello не будет применяться и используемые резервного копирования Azure, пока не зафиксирована.</span><span class="sxs-lookup"><span data-stu-id="6a428-185">hello settings will not be applied and used by Azure Backup unless committed.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="networking"></a><span data-ttu-id="6a428-186">Сеть</span><span class="sxs-lookup"><span data-stu-id="6a428-186">Networking</span></span>
<span data-ttu-id="6a428-187">Если подключение hello toohello машины hello DPM служба архивации Azure на hello Интернет через прокси-сервер, параметры прокси-сервера hello должны быть предоставлены для успешного резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="6a428-187">If hello connectivity of hello DPM machine toohello Azure Backup service on hello internet is through a proxy server, then hello proxy server settings should be provided for successful backups.</span></span> <span data-ttu-id="6a428-188">Это делается с помощью hello ```-ProxyServer```и ```-ProxyPort```, ```-ProxyUsername``` и hello ```ProxyPassword``` параметры с hello [DPMCloudSubscriptionSetting набор](https://technet.microsoft.com/library/jj612791) командлета.</span><span class="sxs-lookup"><span data-stu-id="6a428-188">This is done by using hello ```-ProxyServer```and ```-ProxyPort```, ```-ProxyUsername``` and hello ```ProxyPassword``` parameters with hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="6a428-189">В нашем случае прокси-сервер не используется, поэтому мы явным образом удаляем все данные прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="6a428-189">In this example, there is no proxy server so we are explicitly clearing any proxy-related information.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

<span data-ttu-id="6a428-190">Пропускная способность также можно управлять с помощью параметров ```-WorkHourBandwidth``` и ```-NonWorkHourBandwidth``` для заданного набора дней недели hello.</span><span class="sxs-lookup"><span data-stu-id="6a428-190">Bandwidth usage can also be controlled with options of ```-WorkHourBandwidth``` and ```-NonWorkHourBandwidth``` for a given set of days of hello week.</span></span> <span data-ttu-id="6a428-191">В этом примере мы не настраиваем регулирование.</span><span class="sxs-lookup"><span data-stu-id="6a428-191">In this example, we are not setting any throttling.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

## <a name="configuring-hello-staging-area"></a><span data-ttu-id="6a428-192">Настройка hello промежуточной области</span><span class="sxs-lookup"><span data-stu-id="6a428-192">Configuring hello staging Area</span></span>
<span data-ttu-id="6a428-193">Агент архивации Azure Hello, выполняется на сервере DPM hello должен временное хранилище для данных, восстанавливаемых из облака hello (локальную область промежуточного хранения).</span><span class="sxs-lookup"><span data-stu-id="6a428-193">hello Azure Backup agent running on hello DPM server needs temporary storage for data restored from hello cloud (local staging area).</span></span> <span data-ttu-id="6a428-194">Настройка hello промежуточной области хранения с помощью hello [набор DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) командлета и hello ```-StagingAreaPath``` параметра.</span><span class="sxs-lookup"><span data-stu-id="6a428-194">Configure hello staging area using hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet and hello ```-StagingAreaPath``` parameter.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

<span data-ttu-id="6a428-195">В приведенном выше примере hello, hello промежуточной области устанавливается слишком*C:\StagingArea* hello объекта PowerShell ```$setting```.</span><span class="sxs-lookup"><span data-stu-id="6a428-195">In hello example above, hello staging area will be set too*C:\StagingArea* in hello PowerShell object ```$setting```.</span></span> <span data-ttu-id="6a428-196">Убедитесь, что hello указанная папка уже существует, иначе hello окончательная фиксация параметров подписки hello завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="6a428-196">Ensure that hello specified folder already exists, or else hello final commit of hello subscription settings will fail.</span></span>

### <a name="encryption-settings"></a><span data-ttu-id="6a428-197">Параметры шифрования</span><span class="sxs-lookup"><span data-stu-id="6a428-197">Encryption settings</span></span>
<span data-ttu-id="6a428-198">tooAzure Hello резервного копирования данных, отправляемых резервной копии является зашифрованным tooprotect hello конфиденциальность данных hello.</span><span class="sxs-lookup"><span data-stu-id="6a428-198">hello backup data sent tooAzure Backup is encrypted tooprotect hello confidentiality of hello data.</span></span> <span data-ttu-id="6a428-199">Парольная фраза для шифрования Hello — hello «password» toodecrypt hello данные во время восстановления hello.</span><span class="sxs-lookup"><span data-stu-id="6a428-199">hello encryption passphrase is hello "password" toodecrypt hello data at hello time of restore.</span></span> <span data-ttu-id="6a428-200">Он tookeep важные безопасный этой информации и защиты после ее установки.</span><span class="sxs-lookup"><span data-stu-id="6a428-200">It is important tookeep this information safe and secure once it is set.</span></span>

<span data-ttu-id="6a428-201">В следующем примере hello, hello первая команда преобразует строку hello ```passphrase123456789``` tooa безопасной строки и присваивает hello защищенной строки toohello переменную с именем ```$Passphrase```.</span><span class="sxs-lookup"><span data-stu-id="6a428-201">In hello example below, hello first command converts hello string ```passphrase123456789``` tooa secure string and assigns hello secure string toohello variable named ```$Passphrase```.</span></span> <span data-ttu-id="6a428-202">Вторая команда Hello задает защищенную строку hello в ```$Passphrase``` как hello пароль для шифрования резервных копий.</span><span class="sxs-lookup"><span data-stu-id="6a428-202">hello second command sets hello secure string in ```$Passphrase``` as hello password for encrypting backups.</span></span>

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> <span data-ttu-id="6a428-203">Обновление сведений парольную фразу hello надежным и безопасным, после ее установки.</span><span class="sxs-lookup"><span data-stu-id="6a428-203">Keep hello passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="6a428-204">Данные могут toorestore из Azure без этой парольной фразы не будет.</span><span class="sxs-lookup"><span data-stu-id="6a428-204">You will not be able toorestore data from Azure without this passphrase.</span></span>
>
>

<span data-ttu-id="6a428-205">На этом этапе должны были внесены все необходимые hello изменения toohello ```$setting``` объекта.</span><span class="sxs-lookup"><span data-stu-id="6a428-205">At this point, you should have made all hello required changes toohello ```$setting``` object.</span></span> <span data-ttu-id="6a428-206">Не забывайте toocommit hello изменения.</span><span class="sxs-lookup"><span data-stu-id="6a428-206">Remember toocommit hello changes.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-tooazure-backup"></a><span data-ttu-id="6a428-207">Защита данных tooAzure резервной копии</span><span class="sxs-lookup"><span data-stu-id="6a428-207">Protect data tooAzure Backup</span></span>
<span data-ttu-id="6a428-208">В этом разделе будет добавьте tooDPM производственного сервера и затем включите защиту hello toolocal DPM хранилища данных и затем tooAzure резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="6a428-208">In this section, you will add a production server tooDPM and then protect hello data toolocal DPM storage and then tooAzure Backup.</span></span> <span data-ttu-id="6a428-209">В примерах hello мы покажем, как tooback копирования файлов и папок.</span><span class="sxs-lookup"><span data-stu-id="6a428-209">In hello examples, we will demonstrate how tooback up files and folders.</span></span> <span data-ttu-id="6a428-210">Hello логику можно легко быть расширенные toobackup любой источник данных, поддерживаемых DPM.</span><span class="sxs-lookup"><span data-stu-id="6a428-210">hello logic can easily be extended toobackup any DPM-supported data source.</span></span> <span data-ttu-id="6a428-211">Все резервные копии DPM находятся под управлением группы защиты (ГЗ), которая состоит из четырех частей.</span><span class="sxs-lookup"><span data-stu-id="6a428-211">All your DPM backups are governed by a Protection Group (PG) with four parts:</span></span>

1. <span data-ttu-id="6a428-212">**Членов группы** приведен список все защищаемые объекты hello (также называется *Datasources* в DPM), которые должны tooprotect в hello одной группе защиты.</span><span class="sxs-lookup"><span data-stu-id="6a428-212">**Group members** is a list of all hello protectable objects (also known as *Datasources* in DPM) that you want tooprotect in hello same protection group.</span></span> <span data-ttu-id="6a428-213">Например можно tooprotect производственный виртуальных машин в одну группу защиты и баз данных SQL Server в другую группу защиты как они могут иметь различные требования для резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="6a428-213">For example, you may want tooprotect production VMs in one protection group and SQL Server databases in another protection group as they may have different backup requirements.</span></span> <span data-ttu-id="6a428-214">Перед любой источник данных можно архивировать на рабочем сервере необходимо убедиться, что hello toomake агент DPM устанавливается на сервере hello и под управлением DPM.</span><span class="sxs-lookup"><span data-stu-id="6a428-214">Before you can back up any datasource on a production server you need toomake sure hello DPM Agent is installed on hello server and is managed by DPM.</span></span> <span data-ttu-id="6a428-215">Выполните действия hello для [Установка hello агент DPM](https://technet.microsoft.com/library/bb870935.aspx) , связав ее toohello соответствующие сервера DPM.</span><span class="sxs-lookup"><span data-stu-id="6a428-215">Follow hello steps for [installing hello DPM Agent](https://technet.microsoft.com/library/bb870935.aspx) and linking it toohello appropriate DPM Server.</span></span>
2. <span data-ttu-id="6a428-216">**Метод защиты данных** указывает hello резервного расположения целей - ленту, диск и облака.</span><span class="sxs-lookup"><span data-stu-id="6a428-216">**Data protection method** specifies hello target backup locations - tape, disk, and cloud.</span></span> <span data-ttu-id="6a428-217">В нашем примере мы будет защищать данные toohello локального диска и toohello облака.</span><span class="sxs-lookup"><span data-stu-id="6a428-217">In our example we will protect data toohello local disk and toohello cloud.</span></span>
3. <span data-ttu-id="6a428-218">Объект **расписание резервного копирования** , указывающий при архивы toobe выполнить и как часто hello данные должны быть синхронизированы между hello сервера DPM и hello рабочего сервера.</span><span class="sxs-lookup"><span data-stu-id="6a428-218">A **backup schedule** that specifies when backups need toobe taken and how often hello data should be synchronized between hello DPM Server and hello production server.</span></span>
4. <span data-ttu-id="6a428-219">Объект **расписание хранения** , указывающее, как долго точки восстановления tooretain hello в Azure.</span><span class="sxs-lookup"><span data-stu-id="6a428-219">A **retention schedule** that specifies how long tooretain hello recovery points in Azure.</span></span>

### <a name="creating-a-protection-group"></a><span data-ttu-id="6a428-220">Создание группы защиты</span><span class="sxs-lookup"><span data-stu-id="6a428-220">Creating a protection group</span></span>
<span data-ttu-id="6a428-221">Начните с создания новой группы защиты с помощью hello [New DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) командлета.</span><span class="sxs-lookup"><span data-stu-id="6a428-221">Start by creating a new Protection Group using hello [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span></span>

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

<span data-ttu-id="6a428-222">Hello выше командлет будет создана группа защиты с именем *ProtectGroup01*.</span><span class="sxs-lookup"><span data-stu-id="6a428-222">hello above cmdlet will create a Protection Group named *ProtectGroup01*.</span></span> <span data-ttu-id="6a428-223">Можно изменять существующую группу защиты более поздней версии tooadd резервного копирования toohello облако Azure.</span><span class="sxs-lookup"><span data-stu-id="6a428-223">An existing protection group can also be modified later tooadd backup toohello Azure cloud.</span></span> <span data-ttu-id="6a428-224">Тем не менее toomake любые изменения toohello группа защиты — новые или существующие - мы должны tooget дескриптор на *изменяемой* объекта с помощью hello [Get DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) командлета.</span><span class="sxs-lookup"><span data-stu-id="6a428-224">However, toomake any changes toohello Protection Group - new or existing - we need tooget a handle on a *modifiable* object using hello [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span></span>

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-toohello-protection-group"></a><span data-ttu-id="6a428-225">Добавление членов группы toohello группы защиты</span><span class="sxs-lookup"><span data-stu-id="6a428-225">Adding group members toohello Protection Group</span></span>
<span data-ttu-id="6a428-226">Каждый агент DPM знает hello список источников данных на сервере hello, установленной на.</span><span class="sxs-lookup"><span data-stu-id="6a428-226">Each DPM Agent knows hello list of datasources on hello server that it is installed on.</span></span> <span data-ttu-id="6a428-227">tooadd toohello источник данных группы защиты, hello toofirst потребностей агент DPM Отправить список сервер DPM задней toohello hello источников данных.</span><span class="sxs-lookup"><span data-stu-id="6a428-227">tooadd a datasource toohello Protection Group, hello DPM Agent needs toofirst send a list of hello datasources back toohello DPM server.</span></span> <span data-ttu-id="6a428-228">Одного или нескольких источников данных, а затем и добавлены toohello группы защиты.</span><span class="sxs-lookup"><span data-stu-id="6a428-228">One or more datasources are then selected and added toohello Protection Group.</span></span> <span data-ttu-id="6a428-229">Это — tooachieve требуются действия Hello PowerShell:</span><span class="sxs-lookup"><span data-stu-id="6a428-229">hello PowerShell steps needed tooachieve this are:</span></span>

1. <span data-ttu-id="6a428-230">Получить список всех серверов, управляемых с помощью DPM с помощью hello агент DPM.</span><span class="sxs-lookup"><span data-stu-id="6a428-230">Fetch a list of all servers managed by DPM through hello DPM Agent.</span></span>
2. <span data-ttu-id="6a428-231">Выберите определенный сервер.</span><span class="sxs-lookup"><span data-stu-id="6a428-231">Choose a specific server.</span></span>
3. <span data-ttu-id="6a428-232">Получить список всех источников данных на сервере hello.</span><span class="sxs-lookup"><span data-stu-id="6a428-232">Fetch a list of all datasources on hello server.</span></span>
4. <span data-ttu-id="6a428-233">Выберите один или несколько источников данных и добавить их toohello группы защиты</span><span class="sxs-lookup"><span data-stu-id="6a428-233">Choose one or more datasources and add them toohello Protection Group</span></span>

<span data-ttu-id="6a428-234">список серверов, на какие hello агента DPM установлена, а управляется hello сервер DPM Hello приобретается вместе с hello [Get DPMProductionServer](https://technet.microsoft.com/library/hh881600) командлета.</span><span class="sxs-lookup"><span data-stu-id="6a428-234">hello list of servers on which hello DPM Agent is installed and is being managed by hello DPM Server is acquired with hello [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span></span> <span data-ttu-id="6a428-235">В этом примере мы отфильтруем и настроим для резервного копирования только сервер с именем *productionserver01* .</span><span class="sxs-lookup"><span data-stu-id="6a428-235">In this example we will filter and only configure PS with name *productionserver01* for backup.</span></span>

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

<span data-ttu-id="6a428-236">Теперь извлечь hello список источников данных на ```$server``` с помощью hello [Get DPMDatasource](https://technet.microsoft.com/library/hh881605) командлета.</span><span class="sxs-lookup"><span data-stu-id="6a428-236">Now fetch hello list of datasources on ```$server``` using hello [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span></span> <span data-ttu-id="6a428-237">В этом примере мы фильтрации для тома hello * D:\* , мы хотим tooconfigure для резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="6a428-237">In this example we are filtering for hello volume *D:\* that we want tooconfigure for backup.</span></span> <span data-ttu-id="6a428-238">Этот источник данных добавляется toohello группы защиты с помощью hello [DPMChildDatasource добавить](https://technet.microsoft.com/library/hh881732) командлета.</span><span class="sxs-lookup"><span data-stu-id="6a428-238">This datasource is then added toohello Protection Group using hello [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span></span> <span data-ttu-id="6a428-239">Запомнить toouse hello *изменяемой* объект группы защиты ```$MPG``` toomake hello дополнения.</span><span class="sxs-lookup"><span data-stu-id="6a428-239">Remember toouse hello *modifiable* protection group object ```$MPG``` toomake hello additions.</span></span>

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

<span data-ttu-id="6a428-240">Повторите этот шаг столько раз, по мере необходимости, пока не будут добавлены все hello выбранной группы защиты toohello источники данных.</span><span class="sxs-lookup"><span data-stu-id="6a428-240">Repeat this step as many times as required, until you have added all hello chosen datasources toohello protection group.</span></span> <span data-ttu-id="6a428-241">Также можно только один источник данных и hello полный рабочий процесс для создания группы защиты hello и позднее добавить несколько источников данных toohello группы защиты.</span><span class="sxs-lookup"><span data-stu-id="6a428-241">You can also start with just one datasource, and complete hello workflow for creating hello Protection Group, and at a later point add more datasources toohello Protection Group.</span></span>

### <a name="selecting-hello-data-protection-method"></a><span data-ttu-id="6a428-242">Выбор метода защиты данных hello</span><span class="sxs-lookup"><span data-stu-id="6a428-242">Selecting hello data protection method</span></span>
<span data-ttu-id="6a428-243">После hello источники данных будут добавлены toohello группы защиты, hello следующим шагом является hello с помощью метода защиты hello toospecify [DPMProtectionType набор](https://technet.microsoft.com/library/hh881725) командлета.</span><span class="sxs-lookup"><span data-stu-id="6a428-243">Once hello datasources have been added toohello Protection Group, hello next step is toospecify hello protection method using hello [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span></span> <span data-ttu-id="6a428-244">В этом примере hello группы защиты настроена для локального диска и резервное копирование в облако.</span><span class="sxs-lookup"><span data-stu-id="6a428-244">In this example, hello Protection Group is setup for local disk and cloud backup.</span></span> <span data-ttu-id="6a428-245">Необходимо также toospecify hello datasource, необходимо с помощью hello toocloud tooprotect [DPMChildDatasource добавить](https://technet.microsoft.com/library/hh881732.aspx) командлет с флагом - сети.</span><span class="sxs-lookup"><span data-stu-id="6a428-245">You also need toospecify hello datasource that you want tooprotect toocloud using hello [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet with -Online flag.</span></span>

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-hello-retention-range"></a><span data-ttu-id="6a428-246">Установка диапазона хранения hello</span><span class="sxs-lookup"><span data-stu-id="6a428-246">Setting hello retention range</span></span>
<span data-ttu-id="6a428-247">Задать политику хранения hello точки hello резервного копирования с помощью hello [DPMPolicyObjective набор](https://technet.microsoft.com/library/hh881762) командлета.</span><span class="sxs-lookup"><span data-stu-id="6a428-247">Set hello retention for hello backup points using hello [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span> <span data-ttu-id="6a428-248">Хотя может показаться нечетное tooset hello хранения перед расписание резервного копирования hello определен, с помощью hello ```Set-DPMPolicyObjective``` автоматически задает расписание резервного копирования по умолчанию, который затем может быть изменен.</span><span class="sxs-lookup"><span data-stu-id="6a428-248">While it might seem odd tooset hello retention before hello backup schedule has been defined, using hello ```Set-DPMPolicyObjective``` cmdlet automatically sets a default backup schedule that can then be modified.</span></span> <span data-ttu-id="6a428-249">Он всегда расписание резервного копирования hello возможных tooset сначала и hello политики хранения после.</span><span class="sxs-lookup"><span data-stu-id="6a428-249">It is always possible tooset hello backup schedule first and hello retention policy after.</span></span>

<span data-ttu-id="6a428-250">В следующем примере hello hello командлет задает параметры хранения hello для резервного копирования на диск.</span><span class="sxs-lookup"><span data-stu-id="6a428-250">In hello example below, hello cmdlet sets hello retention parameters for disk backups.</span></span> <span data-ttu-id="6a428-251">Это будет хранить архивы 10 дней и синхронизировать данные каждые 6 часов между hello рабочий сервер и сервер DPM hello.</span><span class="sxs-lookup"><span data-stu-id="6a428-251">This will retain backups for 10 days, and sync data every 6 hours between hello production server and hello DPM server.</span></span> <span data-ttu-id="6a428-252">Hello ```SynchronizationFrequencyMinutes``` не определяет, как часто точки резервного копирования создается, но как данных часто является скопированный toohello сервера DPM.</span><span class="sxs-lookup"><span data-stu-id="6a428-252">hello ```SynchronizationFrequencyMinutes``` doesn't define how often a backup point is created, but how often data is copied toohello DPM server.</span></span>  <span data-ttu-id="6a428-253">Это предотвращает создание слишком крупных резервных копий.</span><span class="sxs-lookup"><span data-stu-id="6a428-253">This setting prevents backups from becoming too large.</span></span>

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

<span data-ttu-id="6a428-254">Для резервного копирования будет tooAzure (DPM называется toothem оперативного резервного копирования) hello диапазонов хранения можно настроить для [Долгосрочное хранение с использованием Деда отец ов схемы (GFS)](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="6a428-254">For backups going tooAzure (DPM refers toothem as Online backups) hello retention ranges can be configured for [long term retention using a Grandfather-Father-Son scheme (GFS)](backup-azure-backup-cloud-as-tape.md).</span></span> <span data-ttu-id="6a428-255">То есть можно определить политику объединенного хранения, включающую политики ежедневного, еженедельного, ежемесячного и ежегодного хранения.</span><span class="sxs-lookup"><span data-stu-id="6a428-255">That is, you can define a combined retention policy involving daily, weekly, monthly and yearly retention policies.</span></span> <span data-ttu-id="6a428-256">В этом примере мы массив, представляющий схему сложных хранения hello, нам нужно создать, а затем настройте hello диапазон хранения, с помощью hello [DPMPolicyObjective набор](https://technet.microsoft.com/library/hh881762) командлета.</span><span class="sxs-lookup"><span data-stu-id="6a428-256">In this example, we create an array representing hello complex retention scheme that we want, and then configure hello retention range using hello [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span>

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-hello-backup-schedule"></a><span data-ttu-id="6a428-257">Расписание резервного копирования набор hello</span><span class="sxs-lookup"><span data-stu-id="6a428-257">Set hello backup schedule</span></span>
<span data-ttu-id="6a428-258">DPM задает расписание резервного копирования по умолчанию автоматически при указании цели защиты hello, с помощью hello ```Set-DPMPolicyObjective``` командлета.</span><span class="sxs-lookup"><span data-stu-id="6a428-258">DPM sets a default backup schedule automatically if you specify hello protection objective using hello ```Set-DPMPolicyObjective``` cmdlet.</span></span> <span data-ttu-id="6a428-259">расписания по умолчанию hello toochange, использовать hello [Get DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) командлет следуют hello [DPMPolicySchedule набор](https://technet.microsoft.com/library/hh881723) командлета.</span><span class="sxs-lookup"><span data-stu-id="6a428-259">toochange hello default schedules, use hello [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet followed by hello [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span></span>

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

<span data-ttu-id="6a428-260">В hello выше примере ```$onlineSch``` является массивом с четырьмя элементами, содержащий hello существующее расписание оперативной защиты для hello группы защиты в схеме GFS hello:</span><span class="sxs-lookup"><span data-stu-id="6a428-260">In hello above example, ```$onlineSch``` is an array with four elements that contains hello existing online protection schedule for hello Protection Group in hello GFS scheme:</span></span>

1. <span data-ttu-id="6a428-261">```$onlineSch[0]```содержит hello ежедневное расписание</span><span class="sxs-lookup"><span data-stu-id="6a428-261">```$onlineSch[0]``` contains hello daily schedule</span></span>
2. <span data-ttu-id="6a428-262">```$onlineSch[1]```содержит hello еженедельного расписания</span><span class="sxs-lookup"><span data-stu-id="6a428-262">```$onlineSch[1]``` contains hello weekly schedule</span></span>
3. <span data-ttu-id="6a428-263">```$onlineSch[2]```содержит hello ежемесячного расписания</span><span class="sxs-lookup"><span data-stu-id="6a428-263">```$onlineSch[2]``` contains hello monthly schedule</span></span>
4. <span data-ttu-id="6a428-264">```$onlineSch[3]```содержит расписание годовой hello</span><span class="sxs-lookup"><span data-stu-id="6a428-264">```$onlineSch[3]``` contains hello yearly schedule</span></span>

<span data-ttu-id="6a428-265">Поэтому если вам требуется toomodify hello Еженедельное расписание, toorefer toohello ```$onlineSch[1]```.</span><span class="sxs-lookup"><span data-stu-id="6a428-265">So if you need toomodify hello weekly schedule, you need toorefer toohello ```$onlineSch[1]```.</span></span>

### <a name="initial-backup"></a><span data-ttu-id="6a428-266">Начальное резервное копирование</span><span class="sxs-lookup"><span data-stu-id="6a428-266">Initial backup</span></span>
<span data-ttu-id="6a428-267">При резервном копировании datasource для hello, впервые, DPM потребностей создает начальной реплики, создает полную копию объекта datasource toobe hello, защищены на томе реплики DPM.</span><span class="sxs-lookup"><span data-stu-id="6a428-267">When backing up a datasource for hello first time, DPM needs creates initial replica that creates a full copy of hello datasource toobe protected on DPM replica volume.</span></span> <span data-ttu-id="6a428-268">Это действие может быть запланированной на определенное время или можно запустить вручную, используя hello [набор DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) командлет с параметром hello ```-NOW```.</span><span class="sxs-lookup"><span data-stu-id="6a428-268">This activity can either be scheduled for a specific time, or can be triggered manually, using hello [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet with hello parameter ```-NOW```.</span></span>

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-hello-size-of-dpm-replica--recovery-point-volume"></a><span data-ttu-id="6a428-269">Изменение размера hello реплики DPM и тома точек восстановления</span><span class="sxs-lookup"><span data-stu-id="6a428-269">Changing hello size of DPM Replica & recovery point volume</span></span>
<span data-ttu-id="6a428-270">Можно также изменить размер тома реплики DPM и теневого копирования тома с помощью hello [DPMDatasourceDiskAllocation набор](https://technet.microsoft.com/library/hh881618.aspx) командлет как hello в следующем примере: Get-DatasourceDiskAllocation - Datasource $DS SET-DatasourceDiskAllocation - Datasource $DS - ProtectionGroup $MPG-вручную - ReplicaArea (2 ГБ) — ShadowCopyArea (2 ГБ)</span><span class="sxs-lookup"><span data-stu-id="6a428-270">You can also change hello size of DPM Replica volume and Shadow Copy volume using [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet as in hello following example: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span></span>

### <a name="committing-hello-changes-toohello-protection-group"></a><span data-ttu-id="6a428-271">Фиксация hello изменяет toohello группы защиты</span><span class="sxs-lookup"><span data-stu-id="6a428-271">Committing hello changes toohello Protection Group</span></span>
<span data-ttu-id="6a428-272">Наконец hello изменения должны toobe, зафиксированные до DPM можно использовать резервную копию hello каждой новой конфигурации группы защиты hello.</span><span class="sxs-lookup"><span data-stu-id="6a428-272">Finally, hello changes need toobe committed before DPM can take hello backup per hello new Protection Group configuration.</span></span> <span data-ttu-id="6a428-273">Это можно сделать с помощью hello [DPMProtectionGroup набор](https://technet.microsoft.com/library/hh881758) командлета.</span><span class="sxs-lookup"><span data-stu-id="6a428-273">This can be achieved using hello [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span></span>

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-hello-backup-points"></a><span data-ttu-id="6a428-274">Просматривать hello резервного копирования точки</span><span class="sxs-lookup"><span data-stu-id="6a428-274">View hello backup points</span></span>
<span data-ttu-id="6a428-275">Можно использовать hello [Get DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) tooget командлет список всех точек восстановления для источника данных.</span><span class="sxs-lookup"><span data-stu-id="6a428-275">You can use hello [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet tooget a list of all recovery points for a datasource.</span></span> <span data-ttu-id="6a428-276">В этом примере мы:</span><span class="sxs-lookup"><span data-stu-id="6a428-276">In this example, we will:</span></span>

* <span data-ttu-id="6a428-277">FETCH все hello PGs на сервере DPM hello и сохранить в массиве```$PG```</span><span class="sxs-lookup"><span data-stu-id="6a428-277">fetch all hello PGs on hello DPM server and stored in an array ```$PG```</span></span>
* <span data-ttu-id="6a428-278">получить соответствующий toohello hello источников данных```$PG[0]```</span><span class="sxs-lookup"><span data-stu-id="6a428-278">get hello datasources corresponding toohello ```$PG[0]```</span></span>
* <span data-ttu-id="6a428-279">Получите все hello точки восстановления для источника данных.</span><span class="sxs-lookup"><span data-stu-id="6a428-279">get all hello recovery points for a datasource.</span></span>

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a><span data-ttu-id="6a428-280">Восстановление данных, защищенных в Azure</span><span class="sxs-lookup"><span data-stu-id="6a428-280">Restore data protected on Azure</span></span>
<span data-ttu-id="6a428-281">Восстановление данных представляет собой сочетание объектов ```RecoverableItem``` и ```RecoveryOption```.</span><span class="sxs-lookup"><span data-stu-id="6a428-281">Restoring data is a combination of a ```RecoverableItem``` object and a ```RecoveryOption``` object.</span></span> <span data-ttu-id="6a428-282">В предыдущем разделе hello нас есть список точек hello резервного копирования для источника данных.</span><span class="sxs-lookup"><span data-stu-id="6a428-282">In hello previous section, we got a list of hello backup points for a datasource.</span></span>

<span data-ttu-id="6a428-283">В следующем примере hello демонстрируют, как toorestore Hyper-V виртуальной машины из резервного копирования Azure точками объединение резервного копирования с hello целевого объекта для восстановления.</span><span class="sxs-lookup"><span data-stu-id="6a428-283">In hello example below, we demonstrate how toorestore a Hyper-V virtual machine from Azure Backup by combining backup points with hello target for recovery.</span></span> <span data-ttu-id="6a428-284">В этом примере мы:</span><span class="sxs-lookup"><span data-stu-id="6a428-284">This example includes:</span></span>

* <span data-ttu-id="6a428-285">Создание параметра восстановления, используя hello [New DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) командлета.</span><span class="sxs-lookup"><span data-stu-id="6a428-285">Creating a recovery option using hello  [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span></span>
* <span data-ttu-id="6a428-286">Извлечение hello массивом точек резервного копирования, с помощью hello ```Get-DPMRecoveryPoint``` командлета.</span><span class="sxs-lookup"><span data-stu-id="6a428-286">Fetching hello array of backup points using hello ```Get-DPMRecoveryPoint``` cmdlet.</span></span>
* <span data-ttu-id="6a428-287">Выбор резервного копирования toorestore точки из.</span><span class="sxs-lookup"><span data-stu-id="6a428-287">Choosing a backup point toorestore from.</span></span>

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

<span data-ttu-id="6a428-288">Hello команды можно легко расширить для любого типа источника данных.</span><span class="sxs-lookup"><span data-stu-id="6a428-288">hello commands can easily be extended for any datasource type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a428-289">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6a428-289">Next steps</span></span>
* <span data-ttu-id="6a428-290">Дополнительные сведения о DPM см. резервное копирование tooAzure [tooDPM введение резервного копирования](backup-azure-dpm-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="6a428-290">For more information about DPM tooAzure Backup see [Introduction tooDPM Backup](backup-azure-dpm-introduction.md)</span></span>
