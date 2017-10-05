---
title: "Служба архивации Azure: использование PowerShell для архивации рабочих нагрузок DPM | Документация Майкрософт"
description: "Узнайте о том, как развернуть службу архивации Azure для Data Protection Manager (DPM) и управлять ей с помощью PowerShell"
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
ms.openlocfilehash: 2e3b4a094511a59cfa02917efc2e3e053840af0c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-and-manage-backup-to-azure-for-data-protection-manager-dpm-servers-using-powershell"></a><span data-ttu-id="60db5-103">Развертывание резервного копирования в Azure для серверов Data Protection Manager (DPM) и управление им с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="60db5-103">Deploy and manage backup to Azure for Data Protection Manager (DPM) servers using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="60db5-104">ARM</span><span class="sxs-lookup"><span data-stu-id="60db5-104">ARM</span></span>](backup-dpm-automation.md)
> * [<span data-ttu-id="60db5-105">Классический</span><span class="sxs-lookup"><span data-stu-id="60db5-105">Classic</span></span>](backup-dpm-automation-classic.md)
>
>

<span data-ttu-id="60db5-106">В этой статье описано, как использовать PowerShell для настройки службы архивации Azure на сервере DPM и для управления резервным копированием и восстановлением данных.</span><span class="sxs-lookup"><span data-stu-id="60db5-106">This article shows you how to use PowerShell to setup Azure Backup on a DPM server, and to manage backup and recovery.</span></span>

## <a name="setting-up-the-powershell-environment"></a><span data-ttu-id="60db5-107">Настройка среды PowerShell</span><span class="sxs-lookup"><span data-stu-id="60db5-107">Setting up the PowerShell environment</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="60db5-108">Прежде чем использовать PowerShell для управления резервными копиями Data Protection Manager в Azure, необходимо настроить подходящую среду в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="60db5-108">Before you can use PowerShell to manage backups from Data Protection Manager to Azure, you need to have the right environment in PowerShell.</span></span> <span data-ttu-id="60db5-109">В начале сеанса PowerShell обязательно выполните следующую команду для импорта необходимых модулей, которая также позволяет правильно ссылаться на командлеты DPM:</span><span class="sxs-lookup"><span data-stu-id="60db5-109">At the start of the PowerShell session, ensure that you run the following command to import the right modules and allow you to correctly reference the DPM cmdlets:</span></span>

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

## <a name="setup-and-registration"></a><span data-ttu-id="60db5-110">Настройка и регистрация</span><span class="sxs-lookup"><span data-stu-id="60db5-110">Setup and Registration</span></span>
<span data-ttu-id="60db5-111">Чтобы начать работу, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="60db5-111">To begin:</span></span>

1. <span data-ttu-id="60db5-112">[Скачайте последнюю версию PowerShell](https://github.com/Azure/azure-powershell/releases) (минимальная требуемая версия: 1.0.0).</span><span class="sxs-lookup"><span data-stu-id="60db5-112">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is: 1.0.0)</span></span>
2. <span data-ttu-id="60db5-113">Включите командлеты службы архивации Azure. Для этого перейдите в режим *AzureResourceManager* с помощью командлета **Switch-AzureMode**.</span><span class="sxs-lookup"><span data-stu-id="60db5-113">Enable the Azure Backup commandlets by switching to *AzureResourceManager* mode by using the **Switch-AzureMode** commandlet:</span></span>

```
PS C:\> Switch-AzureMode AzureResourceManager
```

<span data-ttu-id="60db5-114">С помощью PowerShell можно автоматизировать указанные ниже задачи по настройке и регистрации.</span><span class="sxs-lookup"><span data-stu-id="60db5-114">The following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="60db5-115">Создание хранилища служб восстановления</span><span class="sxs-lookup"><span data-stu-id="60db5-115">Create a Recovery Services vault</span></span>
* <span data-ttu-id="60db5-116">Установка агента службы архивации Azure.</span><span class="sxs-lookup"><span data-stu-id="60db5-116">Installing the Azure Backup agent</span></span>
* <span data-ttu-id="60db5-117">Регистрация в службе архивации Azure</span><span class="sxs-lookup"><span data-stu-id="60db5-117">Registering with the Azure Backup service</span></span>
* <span data-ttu-id="60db5-118">Параметры сети</span><span class="sxs-lookup"><span data-stu-id="60db5-118">Networking settings</span></span>
* <span data-ttu-id="60db5-119">Параметры шифрования</span><span class="sxs-lookup"><span data-stu-id="60db5-119">Encryption settings</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="60db5-120">Создание хранилища служб восстановления</span><span class="sxs-lookup"><span data-stu-id="60db5-120">Create a recovery services vault</span></span>
<span data-ttu-id="60db5-121">Чтобы создать хранилище служб восстановления, выполните описанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="60db5-121">The following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="60db5-122">Хранилище служб восстановления отличается от хранилища службы архивации.</span><span class="sxs-lookup"><span data-stu-id="60db5-122">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="60db5-123">Если вы используете службу архивации Azure впервые, выполните командлет **Register-AzureRMResourceProvider** , чтобы зарегистрировать поставщик служб восстановления Azure в своей подписке.</span><span class="sxs-lookup"><span data-stu-id="60db5-123">If you are using Azure Backup for the first time, you must use the **Register-AzureRMResourceProvider** cmdlet to register the Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="60db5-124">Хранилище служб восстановления представляет собой ресурс ARM, поэтому вам потребуется разместить его в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="60db5-124">The Recovery Services vault is an ARM resource, so you need to place it within a Resource Group.</span></span> <span data-ttu-id="60db5-125">Вы можете выбрать существующую группу ресурсов или создать новую.</span><span class="sxs-lookup"><span data-stu-id="60db5-125">You can use an existing resource group, or create a new one.</span></span> <span data-ttu-id="60db5-126">При создании группы ресурсов укажите ее имя и расположение.</span><span class="sxs-lookup"><span data-stu-id="60db5-126">When creating a new resource group, specify the name and location for the resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. <span data-ttu-id="60db5-127">Выполните командлет **New-AzureRmRecoveryServicesVault** , чтобы создать хранилище.</span><span class="sxs-lookup"><span data-stu-id="60db5-127">Use the **New-AzureRmRecoveryServicesVault** cmdlet to create a new vault.</span></span> <span data-ttu-id="60db5-128">Разместите хранилище там же, где находится группа ресурсов.</span><span class="sxs-lookup"><span data-stu-id="60db5-128">Be sure to specify the same location for the vault as was used for the resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. <span data-ttu-id="60db5-129">Укажите необходимый тип избыточности хранилища: [локально избыточное (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) или [геоизбыточное (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="60db5-129">Specify the type of storage redundancy to use; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="60db5-130">В следующем примере показано, что для параметра BackupStorageRedundancy для testVault задано значение GeoRedundant.</span><span class="sxs-lookup"><span data-stu-id="60db5-130">The following example shows the -BackupStorageRedundancy option for testVault is set to GeoRedundant.</span></span>

   > [!TIP]
   > <span data-ttu-id="60db5-131">Для многих командлетов службы архивации Azure требуется объект хранилища служб восстановления в качестве входных данных.</span><span class="sxs-lookup"><span data-stu-id="60db5-131">Many Azure Backup cmdlets require the Recovery Services vault object as an input.</span></span> <span data-ttu-id="60db5-132">По этой причине объект хранилища служб восстановления резервных копий удобно хранить в переменной.</span><span class="sxs-lookup"><span data-stu-id="60db5-132">For this reason, it is convenient to store the Backup Recovery Services vault object in a variable.</span></span>
   >
   >

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

## <a name="view-the-vaults-in-a-subscription"></a><span data-ttu-id="60db5-133">Просмотр хранилищ в подписке</span><span class="sxs-lookup"><span data-stu-id="60db5-133">View the vaults in a subscription</span></span>
<span data-ttu-id="60db5-134">Чтобы получить список всех хранилищ в текущей подписке, используйте командлет **Get AzureRmRecoveryServicesVault** .</span><span class="sxs-lookup"><span data-stu-id="60db5-134">Use **Get-AzureRmRecoveryServicesVault** to view the list of all vaults in the current subscription.</span></span> <span data-ttu-id="60db5-135">Он позволяет убедиться в том, что хранилище создано, и увидеть, какие хранилища доступны в подписке.</span><span class="sxs-lookup"><span data-stu-id="60db5-135">You can use this command to check that a new  vault was created, or to see what vaults are available in the subscription.</span></span>

<span data-ttu-id="60db5-136">Выполнив команду Get-AzureRmRecoveryServicesVault, вы получите список всех хранилищ в подписке.</span><span class="sxs-lookup"><span data-stu-id="60db5-136">Run the command, Get-AzureRmRecoveryServicesVault, and all vaults in the subscription are listed.</span></span>

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


## <a name="installing-the-azure-backup-agent-on-a-dpm-server"></a><span data-ttu-id="60db5-137">Установка агента службы архивации Azure на сервер DPM</span><span class="sxs-lookup"><span data-stu-id="60db5-137">Installing the Azure Backup agent on a DPM Server</span></span>
<span data-ttu-id="60db5-138">Прежде чем устанавливать агент службы архивации Azure, необходимо загрузить установщик и разместить его в системе Windows Server.</span><span class="sxs-lookup"><span data-stu-id="60db5-138">Before you install the Azure Backup agent, you need to have the installer downloaded and present on the Windows Server.</span></span> <span data-ttu-id="60db5-139">Последнюю версию установщика можно загрузить в [центре загрузки Майкрософт](http://aka.ms/azurebackup_agent) или на странице панели мониторинга для хранилища служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="60db5-139">You can get the latest version of the installer from the [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from the Recovery Services vault's Dashboard page.</span></span> <span data-ttu-id="60db5-140">Сохраните установщик в удобном для вас месте, например в папке *C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="60db5-140">Save the installer to an easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="60db5-141">Чтобы установить агент, в консоли PowerShell с повышенными привилегиями **на сервере DPM**выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="60db5-141">To install the agent, run the following command in an elevated PowerShell console **on the DPM server**:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="60db5-142">Агент будет установлен с параметрами по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="60db5-142">This installs the agent with all the default options.</span></span> <span data-ttu-id="60db5-143">Установка займет всего несколько минут и пройдет в фоновом режиме.</span><span class="sxs-lookup"><span data-stu-id="60db5-143">The installation takes a few minutes in the background.</span></span> <span data-ttu-id="60db5-144">Если параметр */nu* не будет указан, в конце установки откроется окно **Обновления Windows** для проверки наличия обновлений.</span><span class="sxs-lookup"><span data-stu-id="60db5-144">If you do not specify the */nu* option the **Windows Update** window opens at the end of the installation to check for any updates.</span></span>

<span data-ttu-id="60db5-145">Агент появится в списке установленных программ.</span><span class="sxs-lookup"><span data-stu-id="60db5-145">The agent shows up in the list of installed programs.</span></span> <span data-ttu-id="60db5-146">Чтобы просмотреть список установленных программ, выберите **Панель управления** > **Программы** > **Программы и компоненты**.</span><span class="sxs-lookup"><span data-stu-id="60db5-146">To see the list of installed programs, go to **Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Агент установлен](./media/backup-dpm-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="60db5-148">Параметры установки</span><span class="sxs-lookup"><span data-stu-id="60db5-148">Installation options</span></span>
<span data-ttu-id="60db5-149">Чтобы просмотреть все доступные в командной строке параметры, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="60db5-149">To see all the options available via the commandline, use the following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="60db5-150">Доступны следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="60db5-150">The available options include:</span></span>

| <span data-ttu-id="60db5-151">Параметр</span><span class="sxs-lookup"><span data-stu-id="60db5-151">Option</span></span> | <span data-ttu-id="60db5-152">Сведения</span><span class="sxs-lookup"><span data-stu-id="60db5-152">Details</span></span> | <span data-ttu-id="60db5-153">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="60db5-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="60db5-154">/q</span><span class="sxs-lookup"><span data-stu-id="60db5-154">/q</span></span> |<span data-ttu-id="60db5-155">Позволяет выполнить тихую установку.</span><span class="sxs-lookup"><span data-stu-id="60db5-155">Quiet installation</span></span> |- |
| <span data-ttu-id="60db5-156">/p:"расположение"</span><span class="sxs-lookup"><span data-stu-id="60db5-156">/p:"location"</span></span> |<span data-ttu-id="60db5-157">Путь к папке установки для агента архивации Azure.</span><span class="sxs-lookup"><span data-stu-id="60db5-157">Path to the installation folder for the Azure Backup agent.</span></span> |<span data-ttu-id="60db5-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="60db5-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="60db5-159">/s:"расположение"</span><span class="sxs-lookup"><span data-stu-id="60db5-159">/s:"location"</span></span> |<span data-ttu-id="60db5-160">Путь к папке кэша для агента архивации Azure.</span><span class="sxs-lookup"><span data-stu-id="60db5-160">Path to the cache folder for the Azure Backup agent.</span></span> |<span data-ttu-id="60db5-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="60db5-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="60db5-162">/m</span><span class="sxs-lookup"><span data-stu-id="60db5-162">/m</span></span> |<span data-ttu-id="60db5-163">Позволяет явно согласиться на использование Центра обновления Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="60db5-163">Opt-in to Microsoft Update</span></span> |- |
| <span data-ttu-id="60db5-164">/nu</span><span class="sxs-lookup"><span data-stu-id="60db5-164">/nu</span></span> |<span data-ttu-id="60db5-165">Позволяет отказаться от проверки наличия обновлений после завершения установки.</span><span class="sxs-lookup"><span data-stu-id="60db5-165">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="60db5-166">/d</span><span class="sxs-lookup"><span data-stu-id="60db5-166">/d</span></span> |<span data-ttu-id="60db5-167">Удаляет агент служб восстановления Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="60db5-167">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="60db5-168">/ph</span><span class="sxs-lookup"><span data-stu-id="60db5-168">/ph</span></span> |<span data-ttu-id="60db5-169">Адрес узла прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="60db5-169">Proxy Host Address</span></span> |- |
| <span data-ttu-id="60db5-170">/po</span><span class="sxs-lookup"><span data-stu-id="60db5-170">/po</span></span> |<span data-ttu-id="60db5-171">Номер порта узла прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="60db5-171">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="60db5-172">/pu</span><span class="sxs-lookup"><span data-stu-id="60db5-172">/pu</span></span> |<span data-ttu-id="60db5-173">Имя пользователя узла прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="60db5-173">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="60db5-174">/pw</span><span class="sxs-lookup"><span data-stu-id="60db5-174">/pw</span></span> |<span data-ttu-id="60db5-175">Пароль прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="60db5-175">Proxy Password</span></span> |- |

## <a name="registering-dpm-to-a-recovery-services-vault"></a><span data-ttu-id="60db5-176">Регистрация DPM в хранилище служб восстановления</span><span class="sxs-lookup"><span data-stu-id="60db5-176">Registering DPM to a Recovery Services Vault</span></span>
<span data-ttu-id="60db5-177">После создания хранилища служб восстановления скачайте последнюю версию агента и учетные данные хранилища и сохраните их в удобном расположении, например C:\Downloads.</span><span class="sxs-lookup"><span data-stu-id="60db5-177">After you created the Recovery Services vault, download the latest agent and the vault credentials and store it in a convenient location like C:\Downloads.</span></span>

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
PS C:\> $credsfilename
C:\downloads\testvault\_Sun Apr 10 2016.VaultCredentials
```

<span data-ttu-id="60db5-178">На сервере DPM запустите командлет [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) , чтобы зарегистрировать компьютер в хранилище.</span><span class="sxs-lookup"><span data-stu-id="60db5-178">On the DPM server, run the [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet to register the machine with the vault.</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration-VaultCredentials $cred -Confirm:$false
CertThumbprint      :7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName: testvault
Region              :West US
Machine registration succeeded.
```

### <a name="initial-configuration-settings"></a><span data-ttu-id="60db5-179">Исходные параметры конфигурации</span><span class="sxs-lookup"><span data-stu-id="60db5-179">Initial configuration settings</span></span>
<span data-ttu-id="60db5-180">Зарегистрированный в хранилище служб восстановления сервер DPM запускается с параметрами подписки, используемыми по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="60db5-180">Once the DPM Server is registered with the Recovery Services vault, it starts with default subscription settings.</span></span> <span data-ttu-id="60db5-181">Эти параметры подписки включают настройки сети, шифрования и промежуточной области.</span><span class="sxs-lookup"><span data-stu-id="60db5-181">These subscription settings include Networking, Encryption and the Staging area.</span></span> <span data-ttu-id="60db5-182">Чтобы изменить параметры подписки, сначала получите дескриптор существующих параметров (по умолчанию) с помощью командлета [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) :</span><span class="sxs-lookup"><span data-stu-id="60db5-182">To change subscription settings you need to first get a handle on the existing (default) settings using the [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span></span>

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

<span data-ttu-id="60db5-183">Все изменения вносятся в этот локальный объект PowerShell ```$setting```, а затем полный объект фиксируется в DPM и службе архивации Azure с помощью командлета [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791). Таким образом он сохраняется.</span><span class="sxs-lookup"><span data-stu-id="60db5-183">All modifications are made to this local PowerShell object ```$setting```  and then the full object is committed to DPM and Azure Backup to save them using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="60db5-184">Чтобы гарантировать, что изменения будут сохранены, необходимо использовать флаг ```–Commit```.</span><span class="sxs-lookup"><span data-stu-id="60db5-184">You need to use the ```–Commit``` flag to ensure that the changes are persisted.</span></span> <span data-ttu-id="60db5-185">Параметры не будут применяться и использоваться службой архивации Azure до тех пор, пока они не будут зафиксированы.</span><span class="sxs-lookup"><span data-stu-id="60db5-185">The settings will not be applied and used by Azure Backup unless committed.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="networking"></a><span data-ttu-id="60db5-186">Сеть</span><span class="sxs-lookup"><span data-stu-id="60db5-186">Networking</span></span>
<span data-ttu-id="60db5-187">Если компьютер DPM подключен к службе архивации Azure в Интернете через прокси-сервер, для успешного резервного копирования следует указать параметры прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="60db5-187">If the connectivity of the DPM machine to the Azure Backup service on the internet is through a proxy server, then the proxy server settings should be provided for successful backups.</span></span> <span data-ttu-id="60db5-188">Для этого используются параметры ```-ProxyServer```, ```-ProxyPort```, ```-ProxyUsername``` и ```ProxyPassword``` для командлета [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791).</span><span class="sxs-lookup"><span data-stu-id="60db5-188">This is done by using the ```-ProxyServer```and ```-ProxyPort```, ```-ProxyUsername``` and the ```ProxyPassword``` parameters with the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="60db5-189">В нашем случае прокси-сервер не используется, поэтому мы явным образом удаляем все данные прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="60db5-189">In this example, there is no proxy server so we are explicitly clearing any proxy-related information.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

<span data-ttu-id="60db5-190">Управлять использованием пропускной способности для выбранных дней недели можно с помощью параметров ```-WorkHourBandwidth``` и ```-NonWorkHourBandwidth``` </span><span class="sxs-lookup"><span data-stu-id="60db5-190">Bandwidth usage can also be controlled with options of ```-WorkHourBandwidth``` and ```-NonWorkHourBandwidth``` for a given set of days of the week.</span></span> <span data-ttu-id="60db5-191">В этом примере мы не настраиваем регулирование.</span><span class="sxs-lookup"><span data-stu-id="60db5-191">In this example, we are not setting any throttling.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

## <a name="configuring-the-staging-area"></a><span data-ttu-id="60db5-192">Настройка промежуточной области</span><span class="sxs-lookup"><span data-stu-id="60db5-192">Configuring the staging Area</span></span>
<span data-ttu-id="60db5-193">Для агента службы архивации Azure, работающего на сервере DPM, необходимо предоставить временное хранилище для восстановленных из облака данных (локальная промежуточная область).</span><span class="sxs-lookup"><span data-stu-id="60db5-193">The Azure Backup agent running on the DPM server needs temporary storage for data restored from the cloud (local staging area).</span></span> <span data-ttu-id="60db5-194">Настройте промежуточную область с помощью командлета [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) с параметром ```-StagingAreaPath```.</span><span class="sxs-lookup"><span data-stu-id="60db5-194">Configure the staging area using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet and the ```-StagingAreaPath``` parameter.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

<span data-ttu-id="60db5-195">В примере выше задается промежуточная область *C:\StagingArea* в объекте PowerShell ```$setting```.</span><span class="sxs-lookup"><span data-stu-id="60db5-195">In the example above, the staging area will be set to *C:\StagingArea* in the PowerShell object ```$setting```.</span></span> <span data-ttu-id="60db5-196">Убедитесь, что указанная папка уже существует, иначе финальная фиксация параметров подписки завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="60db5-196">Ensure that the specified folder already exists, or else the final commit of the subscription settings will fail.</span></span>

### <a name="encryption-settings"></a><span data-ttu-id="60db5-197">Параметры шифрования</span><span class="sxs-lookup"><span data-stu-id="60db5-197">Encryption settings</span></span>
<span data-ttu-id="60db5-198">Для защиты конфиденциальности данных резервные копии данных, отправляемые в службу архивации Azure, зашифровываются.</span><span class="sxs-lookup"><span data-stu-id="60db5-198">The backup data sent to Azure Backup is encrypted to protect the confidentiality of the data.</span></span> <span data-ttu-id="60db5-199">Используемая для шифрования парольная фраза является "паролем" для расшифровки данных во время их восстановления.</span><span class="sxs-lookup"><span data-stu-id="60db5-199">The encryption passphrase is the "password" to decrypt the data at the time of restore.</span></span> <span data-ttu-id="60db5-200">После создания фразы надежно сохраните ее и никому не сообщайте о ней.</span><span class="sxs-lookup"><span data-stu-id="60db5-200">It is important to keep this information safe and secure once it is set.</span></span>

<span data-ttu-id="60db5-201">В следующем примере первая команда преобразует строку ```passphrase123456789``` в защищенную строку и присваивает ее переменной ```$Passphrase```.</span><span class="sxs-lookup"><span data-stu-id="60db5-201">In the example below, the first command converts the string ```passphrase123456789``` to a secure string and assigns the secure string to the variable named ```$Passphrase```.</span></span> <span data-ttu-id="60db5-202">Вторая команда задает защищенную строку в ```$Passphrase``` в качестве пароля для шифрования резервных копий.</span><span class="sxs-lookup"><span data-stu-id="60db5-202">the second command sets the secure string in ```$Passphrase``` as the password for encrypting backups.</span></span>

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> <span data-ttu-id="60db5-203">После создания парольной фразы надежно сохраните ее и никому не сообщайте о ней.</span><span class="sxs-lookup"><span data-stu-id="60db5-203">Keep the passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="60db5-204">Восстановить данные из Azure без парольной фразы невозможно.</span><span class="sxs-lookup"><span data-stu-id="60db5-204">You will not be able to restore data from Azure without this passphrase.</span></span>
>
>

<span data-ttu-id="60db5-205">На этом этапе следует внести все необходимые изменения в объект ```$setting``` .</span><span class="sxs-lookup"><span data-stu-id="60db5-205">At this point, you should have made all the required changes to the ```$setting``` object.</span></span> <span data-ttu-id="60db5-206">Не забудьте зафиксировать изменения.</span><span class="sxs-lookup"><span data-stu-id="60db5-206">Remember to commit the changes.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-to-azure-backup"></a><span data-ttu-id="60db5-207">Защита данных в службе архивации Azure</span><span class="sxs-lookup"><span data-stu-id="60db5-207">Protect data to Azure Backup</span></span>
<span data-ttu-id="60db5-208">В этом разделе мы добавим рабочий сервер в DPM, а затем включим защиту данных в локальном хранилище DPM и службе архивации Azure.</span><span class="sxs-lookup"><span data-stu-id="60db5-208">In this section, you will add a production server to DPM and then protect the data to local DPM storage and then to Azure Backup.</span></span> <span data-ttu-id="60db5-209">На примерах мы покажем, как создавать резервные копии файлов и папок.</span><span class="sxs-lookup"><span data-stu-id="60db5-209">In the examples, we will demonstrate how to back up files and folders.</span></span> <span data-ttu-id="60db5-210">Таким же способом можно создавать резервные копии любых поддерживаемых DPM источников данных.</span><span class="sxs-lookup"><span data-stu-id="60db5-210">The logic can easily be extended to backup any DPM-supported data source.</span></span> <span data-ttu-id="60db5-211">Все резервные копии DPM находятся под управлением группы защиты (ГЗ), которая состоит из четырех частей.</span><span class="sxs-lookup"><span data-stu-id="60db5-211">All your DPM backups are governed by a Protection Group (PG) with four parts:</span></span>

1. <span data-ttu-id="60db5-212">**Члены группы защиты** — это список всех защищаемых объектов (также называемых *источниками данных* в DPM), которые вы хотите защитить в рамках одной группы защиты.</span><span class="sxs-lookup"><span data-stu-id="60db5-212">**Group members** is a list of all the protectable objects (also known as *Datasources* in DPM) that you want to protect in the same protection group.</span></span> <span data-ttu-id="60db5-213">Например, вы можете защитить рабочие виртуальные машины в одной группе защиты, а базы данных SQL Server — в другой группе защиты, так как у них могут быть разные требования к резервному копированию.</span><span class="sxs-lookup"><span data-stu-id="60db5-213">For example, you may want to protect production VMs in one protection group and SQL Server databases in another protection group as they may have different backup requirements.</span></span> <span data-ttu-id="60db5-214">Перед созданием резервных копий данных на рабочем сервере убедитесь, что на рабочем сервере установлен агент DPM, который управляется с помощью DPM.</span><span class="sxs-lookup"><span data-stu-id="60db5-214">Before you can back up any datasource on a production server you need to make sure the DPM Agent is installed on the server and is managed by DPM.</span></span> <span data-ttu-id="60db5-215">Выполните шаги по [установке агента DPM](https://technet.microsoft.com/library/bb870935.aspx) и связыванию его с соответствующим сервером DPM.</span><span class="sxs-lookup"><span data-stu-id="60db5-215">Follow the steps for [installing the DPM Agent](https://technet.microsoft.com/library/bb870935.aspx) and linking it to the appropriate DPM Server.</span></span>
2. <span data-ttu-id="60db5-216">**Метод защиты данных** — определяет расположения резервных копий (магнитная лента, диск и облако).</span><span class="sxs-lookup"><span data-stu-id="60db5-216">**Data protection method** specifies the target backup locations - tape, disk, and cloud.</span></span> <span data-ttu-id="60db5-217">В нашем примере мы организуем защиту данных на локальный диск и в облако.</span><span class="sxs-lookup"><span data-stu-id="60db5-217">In our example we will protect data to the local disk and to the cloud.</span></span>
3. <span data-ttu-id="60db5-218">**Расписание резервного копирования** — указывает, когда необходимо выполнять резервное копирование и как часто следует синхронизировать данные между сервером DPM и рабочим сервером.</span><span class="sxs-lookup"><span data-stu-id="60db5-218">A **backup schedule** that specifies when backups need to be taken and how often the data should be synchronized between the DPM Server and the production server.</span></span>
4. <span data-ttu-id="60db5-219">**Расписание хранения** — определяет период хранения точек восстановления в Azure.</span><span class="sxs-lookup"><span data-stu-id="60db5-219">A **retention schedule** that specifies how long to retain the recovery points in Azure.</span></span>

### <a name="creating-a-protection-group"></a><span data-ttu-id="60db5-220">Создание группы защиты</span><span class="sxs-lookup"><span data-stu-id="60db5-220">Creating a protection group</span></span>
<span data-ttu-id="60db5-221">Начните с создания новой группы защиты с помощью командлета [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) .</span><span class="sxs-lookup"><span data-stu-id="60db5-221">Start by creating a new Protection Group using the [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span></span>

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

<span data-ttu-id="60db5-222">Указанный выше командлет создает группу защиты с именем *ProtectGroup01*.</span><span class="sxs-lookup"><span data-stu-id="60db5-222">The above cmdlet will create a Protection Group named *ProtectGroup01*.</span></span> <span data-ttu-id="60db5-223">Существующую группу защиты можно изменить позднее, чтобы добавить резервную копию в облако Azure.</span><span class="sxs-lookup"><span data-stu-id="60db5-223">An existing protection group can also be modified later to add backup to the Azure cloud.</span></span> <span data-ttu-id="60db5-224">Тем не менее, чтобы получить возможность вносить изменения в группу защиты (новую или существующую), необходимо получить дескриптор *изменяемого* объекта с помощью командлета [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) .</span><span class="sxs-lookup"><span data-stu-id="60db5-224">However, to make any changes to the Protection Group - new or existing - we need to get a handle on a *modifiable* object using the [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span></span>

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-to-the-protection-group"></a><span data-ttu-id="60db5-225">Добавление членов группы в группу защиты</span><span class="sxs-lookup"><span data-stu-id="60db5-225">Adding group members to the Protection Group</span></span>
<span data-ttu-id="60db5-226">Каждому агенту DPM известен список источников данных на сервере, на котором он установлен.</span><span class="sxs-lookup"><span data-stu-id="60db5-226">Each DPM Agent knows the list of datasources on the server that it is installed on.</span></span> <span data-ttu-id="60db5-227">Чтобы добавить источник данных в группу защиты, агент DPM должен сначала отправить список источников данных обратно на сервер DPM.</span><span class="sxs-lookup"><span data-stu-id="60db5-227">To add a datasource to the Protection Group, the DPM Agent needs to first send a list of the datasources back to the DPM server.</span></span> <span data-ttu-id="60db5-228">Затем выбирается один или несколько источников данных, которые добавляются в группу защиты.</span><span class="sxs-lookup"><span data-stu-id="60db5-228">One or more datasources are then selected and added to the Protection Group.</span></span> <span data-ttu-id="60db5-229">Ниже представлены действия, которые необходимо выполнить в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="60db5-229">The PowerShell steps needed to achieve this are:</span></span>

1. <span data-ttu-id="60db5-230">Получите список всех серверов, управляемых DPM через агент DPM.</span><span class="sxs-lookup"><span data-stu-id="60db5-230">Fetch a list of all servers managed by DPM through the DPM Agent.</span></span>
2. <span data-ttu-id="60db5-231">Выберите определенный сервер.</span><span class="sxs-lookup"><span data-stu-id="60db5-231">Choose a specific server.</span></span>
3. <span data-ttu-id="60db5-232">Получите список всех источников данных на сервере.</span><span class="sxs-lookup"><span data-stu-id="60db5-232">Fetch a list of all datasources on the server.</span></span>
4. <span data-ttu-id="60db5-233">Выберите один или несколько источников данных и добавьте их в группу защиты.</span><span class="sxs-lookup"><span data-stu-id="60db5-233">Choose one or more datasources and add them to the Protection Group</span></span>

<span data-ttu-id="60db5-234">Чтобы получить список серверов, на которых установлен агент DPM и которые управляются сервером DPM, воспользуйтесь командлетом [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) .</span><span class="sxs-lookup"><span data-stu-id="60db5-234">The list of servers on which the DPM Agent is installed and is being managed by the DPM Server is acquired with the [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span></span> <span data-ttu-id="60db5-235">В этом примере мы отфильтруем и настроим для резервного копирования только сервер с именем *productionserver01* .</span><span class="sxs-lookup"><span data-stu-id="60db5-235">In this example we will filter and only configure PS with name *productionserver01* for backup.</span></span>

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

<span data-ttu-id="60db5-236">Теперь получим список источников данных на ```$server``` с помощью командлета [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605).</span><span class="sxs-lookup"><span data-stu-id="60db5-236">Now fetch the list of datasources on ```$server``` using the [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span></span> <span data-ttu-id="60db5-237">В этом примере мы применяем фильтрацию для тома *D:\*, который нужно настроить для резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="60db5-237">In this example we are filtering for the volume *D:\* that we want to configure for backup.</span></span> <span data-ttu-id="60db5-238">Затем этот источник данных добавляется в группу защиты с помощью командлета [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732).</span><span class="sxs-lookup"><span data-stu-id="60db5-238">This datasource is then added to the Protection Group using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span></span> <span data-ttu-id="60db5-239">Не забывайте использовать *изменяемый* объект группы защиты ```$MPG```, чтобы вносить дополнения.</span><span class="sxs-lookup"><span data-stu-id="60db5-239">Remember to use the *modifiable* protection group object ```$MPG``` to make the additions.</span></span>

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

<span data-ttu-id="60db5-240">При необходимости повторите этот шаг несколько раз, пока все выбранные источники данных не будут добавлены в группу защиты.</span><span class="sxs-lookup"><span data-stu-id="60db5-240">Repeat this step as many times as required, until you have added all the chosen datasources to the protection group.</span></span> <span data-ttu-id="60db5-241">Для начала можно выполнить рабочий процесс создания группы защиты только для одного источника данных, а затем позже добавить в эту группу дополнительные источники данных.</span><span class="sxs-lookup"><span data-stu-id="60db5-241">You can also start with just one datasource, and complete the workflow for creating the Protection Group, and at a later point add more datasources to the Protection Group.</span></span>

### <a name="selecting-the-data-protection-method"></a><span data-ttu-id="60db5-242">Выбор способа защиты данных</span><span class="sxs-lookup"><span data-stu-id="60db5-242">Selecting the data protection method</span></span>
<span data-ttu-id="60db5-243">После добавления в группу защиты источников данных необходимо указать метод защиты, воспользовавшись для этого командлетом [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) .</span><span class="sxs-lookup"><span data-stu-id="60db5-243">Once the datasources have been added to the Protection Group, the next step is to specify the protection method using the [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span></span> <span data-ttu-id="60db5-244">В этом примере группа защиты настроена для резервного копирования на локальный диск и в облако.</span><span class="sxs-lookup"><span data-stu-id="60db5-244">In this example, the Protection Group is setup for local disk and cloud backup.</span></span> <span data-ttu-id="60db5-245">Необходимо также с помощью командлета [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) с флагом -Online указать источник данных, который нужно защитить в облаке.</span><span class="sxs-lookup"><span data-stu-id="60db5-245">You also need to specify the datasource that you want to protect to cloud using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet with -Online flag.</span></span>

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-the-retention-range"></a><span data-ttu-id="60db5-246">Настройка диапазона хранения</span><span class="sxs-lookup"><span data-stu-id="60db5-246">Setting the retention range</span></span>
<span data-ttu-id="60db5-247">Задайте период хранения для точек резервного копирования с помощью командлета [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) .</span><span class="sxs-lookup"><span data-stu-id="60db5-247">Set the retention for the backup points using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span> <span data-ttu-id="60db5-248">Несмотря на то что задание периода хранения до определения расписания резервного копирования может показаться странным, командлет ```Set-DPMPolicyObjective``` автоматически задает расписание резервного копирования по умолчанию, которое в последствии можно изменить.</span><span class="sxs-lookup"><span data-stu-id="60db5-248">While it might seem odd to set the retention before the backup schedule has been defined, using the ```Set-DPMPolicyObjective``` cmdlet automatically sets a default backup schedule that can then be modified.</span></span> <span data-ttu-id="60db5-249">Вы всегда можете сначала определить расписание резервного копирования, а затем задать политику хранения.</span><span class="sxs-lookup"><span data-stu-id="60db5-249">It is always possible to set the backup schedule first and the retention policy after.</span></span>

<span data-ttu-id="60db5-250">В примере ниже командлет задает параметры хранения для резервного копирования на диск.</span><span class="sxs-lookup"><span data-stu-id="60db5-250">In the example below, the cmdlet sets the retention parameters for disk backups.</span></span> <span data-ttu-id="60db5-251">Резервные копии будут храниться 10 дней, а данные будут синхронизироваться между рабочим сервером и сервером DPM каждые 6 часов.</span><span class="sxs-lookup"><span data-stu-id="60db5-251">This will retain backups for 10 days, and sync data every 6 hours between the production server and the DPM server.</span></span> <span data-ttu-id="60db5-252">```SynchronizationFrequencyMinutes``` определяет не частоту создания точек резервного копирования, а частоту копирования данных на сервер DPM.</span><span class="sxs-lookup"><span data-stu-id="60db5-252">The ```SynchronizationFrequencyMinutes``` doesn't define how often a backup point is created, but how often data is copied to the DPM server.</span></span>  <span data-ttu-id="60db5-253">Это предотвращает создание слишком крупных резервных копий.</span><span class="sxs-lookup"><span data-stu-id="60db5-253">This setting prevents backups from becoming too large.</span></span>

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

<span data-ttu-id="60db5-254">Для резервных копий, сохраняемых в Azure (в DPM это называется Online Backup), диапазоны хранения можно настроить для [долгосрочного хранения с использованием трехуровневой схемы (GFS)](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="60db5-254">For backups going to Azure (DPM refers to them as Online backups) the retention ranges can be configured for [long term retention using a Grandfather-Father-Son scheme (GFS)](backup-azure-backup-cloud-as-tape.md).</span></span> <span data-ttu-id="60db5-255">То есть можно определить политику объединенного хранения, включающую политики ежедневного, еженедельного, ежемесячного и ежегодного хранения.</span><span class="sxs-lookup"><span data-stu-id="60db5-255">That is, you can define a combined retention policy involving daily, weekly, monthly and yearly retention policies.</span></span> <span data-ttu-id="60db5-256">В этом примере мы создаем массив, представляющий сложную схему хранения, которая нам необходима, а затем настраиваем диапазон хранения с помощью командлета [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) .</span><span class="sxs-lookup"><span data-stu-id="60db5-256">In this example, we create an array representing the complex retention scheme that we want, and then configure the retention range using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span>

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-the-backup-schedule"></a><span data-ttu-id="60db5-257">Настройка расписания резервного копирования</span><span class="sxs-lookup"><span data-stu-id="60db5-257">Set the backup schedule</span></span>
<span data-ttu-id="60db5-258">При указании цели защиты с помощью командлета ```Set-DPMPolicyObjective``` DPM автоматически задаст расписание резервного копирования по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="60db5-258">DPM sets a default backup schedule automatically if you specify the protection objective using the ```Set-DPMPolicyObjective``` cmdlet.</span></span> <span data-ttu-id="60db5-259">Для изменения расписания по умолчанию используйте командлет [Get DPMPolicySchedule](https://technet.microsoft.com/library/hh881749), а затем командлет [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723).</span><span class="sxs-lookup"><span data-stu-id="60db5-259">To change the default schedules, use the [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet followed by the [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span></span>

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

<span data-ttu-id="60db5-260">В приведенном выше примере ```$onlineSch``` — это массив с четырьмя элементами, содержащий существующее расписание оперативной защиты для группы защиты в схеме GFS:</span><span class="sxs-lookup"><span data-stu-id="60db5-260">In the above example, ```$onlineSch``` is an array with four elements that contains the existing online protection schedule for the Protection Group in the GFS scheme:</span></span>

1. <span data-ttu-id="60db5-261">```$onlineSch[0]``` содержит ежедневное расписание.</span><span class="sxs-lookup"><span data-stu-id="60db5-261">```$onlineSch[0]``` contains the daily schedule</span></span>
2. <span data-ttu-id="60db5-262">```$onlineSch[1]``` содержит еженедельное расписание.</span><span class="sxs-lookup"><span data-stu-id="60db5-262">```$onlineSch[1]``` contains the weekly schedule</span></span>
3. <span data-ttu-id="60db5-263">```$onlineSch[2]``` содержит ежемесячное расписание.</span><span class="sxs-lookup"><span data-stu-id="60db5-263">```$onlineSch[2]``` contains the monthly schedule</span></span>
4. <span data-ttu-id="60db5-264">```$onlineSch[3]``` содержит ежегодное расписание.</span><span class="sxs-lookup"><span data-stu-id="60db5-264">```$onlineSch[3]``` contains the yearly schedule</span></span>

<span data-ttu-id="60db5-265">Поэтому если необходимо изменить еженедельное расписание, необходимо ссылаться на ```$onlineSch[1]```.</span><span class="sxs-lookup"><span data-stu-id="60db5-265">So if you need to modify the weekly schedule, you need to refer to the ```$onlineSch[1]```.</span></span>

### <a name="initial-backup"></a><span data-ttu-id="60db5-266">Начальное резервное копирование</span><span class="sxs-lookup"><span data-stu-id="60db5-266">Initial backup</span></span>
<span data-ttu-id="60db5-267">Если вы создаете резервные копии источника данных впервые, DPM создаст исходную реплику, которая, в свою очередь, создаст в томе реплики DPM полную копию защищаемого источника данных.</span><span class="sxs-lookup"><span data-stu-id="60db5-267">When backing up a datasource for the first time, DPM needs creates initial replica that creates a full copy of the datasource to be protected on DPM replica volume.</span></span> <span data-ttu-id="60db5-268">Это действие можно запланировать на определенное время или выполнить вручную с помощью командлета [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) с параметром ```-NOW```.</span><span class="sxs-lookup"><span data-stu-id="60db5-268">This activity can either be scheduled for a specific time, or can be triggered manually, using the [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet with the parameter ```-NOW```.</span></span>

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-the-size-of-dpm-replica--recovery-point-volume"></a><span data-ttu-id="60db5-269">Изменение размера реплики DPM и тома точек восстановления</span><span class="sxs-lookup"><span data-stu-id="60db5-269">Changing the size of DPM Replica & recovery point volume</span></span>
<span data-ttu-id="60db5-270">Кроме того, можно изменить размер тома реплики DPM и тома теневых копий с помощью командлета [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) , как показано в следующем примере: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb).</span><span class="sxs-lookup"><span data-stu-id="60db5-270">You can also change the size of DPM Replica volume and Shadow Copy volume using [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet as in the following example: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span></span>

### <a name="committing-the-changes-to-the-protection-group"></a><span data-ttu-id="60db5-271">Фиксация изменений в группу защиты</span><span class="sxs-lookup"><span data-stu-id="60db5-271">Committing the changes to the Protection Group</span></span>
<span data-ttu-id="60db5-272">Наконец, необходимо зафиксировать изменения до того, как DPM выполнит резервное копирование в соответствии с новой конфигурацией группы защиты.</span><span class="sxs-lookup"><span data-stu-id="60db5-272">Finally, the changes need to be committed before DPM can take the backup per the new Protection Group configuration.</span></span> <span data-ttu-id="60db5-273">Для этого воспользуйтесь командлетом [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) .</span><span class="sxs-lookup"><span data-stu-id="60db5-273">This can be achieved using the [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span></span>

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-the-backup-points"></a><span data-ttu-id="60db5-274">Просмотр точек резервного копирования</span><span class="sxs-lookup"><span data-stu-id="60db5-274">View the backup points</span></span>
<span data-ttu-id="60db5-275">Чтобы получить список всех точек восстановления для источника данных, можно использовать командлет [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) .</span><span class="sxs-lookup"><span data-stu-id="60db5-275">You can use the [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet to get a list of all recovery points for a datasource.</span></span> <span data-ttu-id="60db5-276">В этом примере мы:</span><span class="sxs-lookup"><span data-stu-id="60db5-276">In this example, we will:</span></span>

* <span data-ttu-id="60db5-277">выгрузим данные из всех групп защиты на сервер DPM, которые будут храниться в массиве ```$PG```</span><span class="sxs-lookup"><span data-stu-id="60db5-277">fetch all the PGs on the DPM server and stored in an array ```$PG```</span></span>
* <span data-ttu-id="60db5-278">получим источники данных, соответствующие ```$PG[0]```</span><span class="sxs-lookup"><span data-stu-id="60db5-278">get the datasources corresponding to the ```$PG[0]```</span></span>
* <span data-ttu-id="60db5-279">получим все точки восстановления для источника данных.</span><span class="sxs-lookup"><span data-stu-id="60db5-279">get all the recovery points for a datasource.</span></span>

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a><span data-ttu-id="60db5-280">Восстановление данных, защищенных в Azure</span><span class="sxs-lookup"><span data-stu-id="60db5-280">Restore data protected on Azure</span></span>
<span data-ttu-id="60db5-281">Восстановление данных представляет собой сочетание объектов ```RecoverableItem``` и ```RecoveryOption```.</span><span class="sxs-lookup"><span data-stu-id="60db5-281">Restoring data is a combination of a ```RecoverableItem``` object and a ```RecoveryOption``` object.</span></span> <span data-ttu-id="60db5-282">В предыдущем разделе мы получили список точек резервного копирования для источника данных.</span><span class="sxs-lookup"><span data-stu-id="60db5-282">In the previous section, we got a list of the backup points for a datasource.</span></span>

<span data-ttu-id="60db5-283">В примере ниже демонстрируется восстановление виртуальной машины Hyper-V из службы архивации Azure путем объединения резервных точек с целевым объектом для восстановления.</span><span class="sxs-lookup"><span data-stu-id="60db5-283">In the example below, we demonstrate how to restore a Hyper-V virtual machine from Azure Backup by combining backup points with the target for recovery.</span></span> <span data-ttu-id="60db5-284">В этом примере мы:</span><span class="sxs-lookup"><span data-stu-id="60db5-284">This example includes:</span></span>

* <span data-ttu-id="60db5-285">Создадим параметр восстановления, используя командлет [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592).</span><span class="sxs-lookup"><span data-stu-id="60db5-285">Creating a recovery option using the  [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span></span>
* <span data-ttu-id="60db5-286">Выполним выборку массива точек резервного копирования с помощью командлета ```Get-DPMRecoveryPoint``` .</span><span class="sxs-lookup"><span data-stu-id="60db5-286">Fetching the array of backup points using the ```Get-DPMRecoveryPoint``` cmdlet.</span></span>
* <span data-ttu-id="60db5-287">Выберем точку резервного копирования для восстановления.</span><span class="sxs-lookup"><span data-stu-id="60db5-287">Choosing a backup point to restore from.</span></span>

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

<span data-ttu-id="60db5-288">Команды можно с легкостью расширить для любого типа источника данных.</span><span class="sxs-lookup"><span data-stu-id="60db5-288">The commands can easily be extended for any datasource type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="60db5-289">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="60db5-289">Next steps</span></span>
* <span data-ttu-id="60db5-290">Дополнительные сведения о службе архивации Azure для DPM см. в статье [Подготовка к архивированию рабочих нагрузок в Azure с помощью DPM](backup-azure-dpm-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="60db5-290">For more information about DPM to Azure Backup see [Introduction to DPM Backup](backup-azure-dpm-introduction.md)</span></span>
