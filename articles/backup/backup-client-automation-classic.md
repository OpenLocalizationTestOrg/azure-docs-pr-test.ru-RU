---
title: "Использование PowerShell для управления резервными копиями Windows Server в Azure | Документация Майкрософт"
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
ms.openlocfilehash: a8e20356ae383ee4fa2158ea544d5d0905028124
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-and-manage-backup-to-azure-for-windows-serverwindows-client-using-powershell"></a><span data-ttu-id="f437e-103">Развертывание резервного копирования в Azure для Windows Server или клиента Windows и управление им с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="f437e-103">Deploy and manage backup to Azure for Windows Server/Windows Client using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f437e-104">ARM</span><span class="sxs-lookup"><span data-stu-id="f437e-104">ARM</span></span>](backup-client-automation.md)
> * [<span data-ttu-id="f437e-105">Классический</span><span class="sxs-lookup"><span data-stu-id="f437e-105">Classic</span></span>](backup-client-automation-classic.md)
>
>

<span data-ttu-id="f437e-106">В этой статье объясняется, как архивировать данные Windows Server или рабочей станции Windows в резервное хранилище с использованием PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f437e-106">This article explains how to use PowerShell to back up Windows Server or Windows workstation data to a backup vault.</span></span> <span data-ttu-id="f437e-107">Мы рекомендуем использовать хранилища служб восстановления для всех новых развертываний.</span><span class="sxs-lookup"><span data-stu-id="f437e-107">Microsoft recommends using Recovery Services vaults for all new deployments.</span></span> <span data-ttu-id="f437e-108">Если вы только приступили к работе со службой Azure Backup и еще не создали резервное хранилище в своей подписке, ознакомьтесь со статьей [Развертывание резервного копирования в Azure для Windows Server или клиента Windows и управление им с помощью PowerShell](backup-client-automation.md), чтобы узнать, как хранить данные в хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="f437e-108">If you are a new Azure Backup user and have not created a backup vault in your subscription, use the article, [Deploy and manage Data Protection Manager data to Azure using PowerShell](backup-client-automation.md) so you store your data in a Recovery Services vault.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="f437e-109">Теперь вы можете обновить свои резервные хранилища до хранилищ служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="f437e-109">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="f437e-110">См. дополнительные сведения об [обновлении резервного хранилища до хранилища служб восстановления](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="f437e-110">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="f437e-111">Корпорация Майкрософт рекомендует обновить резервные хранилища до хранилищ служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="f437e-111">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="f437e-112">После 15 октября 2017 года вы не сможете использовать PowerShell для создания резервных хранилищ.</span><span class="sxs-lookup"><span data-stu-id="f437e-112">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="f437e-113">**К 1 ноября 2017 года**:</span><span class="sxs-lookup"><span data-stu-id="f437e-113">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="f437e-114">Все остальные резервные хранилища будут автоматически обновлены до хранилищ служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="f437e-114">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="f437e-115">Вы не сможете получить доступ к данным резервных копий на классическом портале.</span><span class="sxs-lookup"><span data-stu-id="f437e-115">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="f437e-116">Вместо этого для доступа к данным резервных копий в хранилищах служб восстановления используйте портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f437e-116">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="install-azure-powershell"></a><span data-ttu-id="f437e-117">Установка Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f437e-117">Install Azure PowerShell</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="f437e-118">Версия Azure PowerShell 1.0 была выпущена в октябре 2015 г.</span><span class="sxs-lookup"><span data-stu-id="f437e-118">In October 2015, Azure PowerShell 1.0 was released.</span></span> <span data-ttu-id="f437e-119">Следуя после версии 0.9.8, она содержит несколько существенных изменений, которые в основном касаются шаблона именования командлетов.</span><span class="sxs-lookup"><span data-stu-id="f437e-119">This release succeeded the 0.9.8 release and brought about some significant changes, especially in the naming pattern of the cmdlets.</span></span> <span data-ttu-id="f437e-120">В командлетах выпуска 1.0 используется шаблон именования {глагол}-AzureRm{существительное}, тогда как в командлетах выпуска 0.9.8 суффикс **Rm** не используется (например, New-AzureRmResourceGroup вместо New-AzureResourceGroup).</span><span class="sxs-lookup"><span data-stu-id="f437e-120">1.0 cmdlets follow the naming pattern {verb}-AzureRm{noun}; whereas, the 0.9.8 names do not include **Rm** (for example, New-AzureRmResourceGroup instead of New-AzureResourceGroup).</span></span> <span data-ttu-id="f437e-121">При использовании Azure PowerShell 0.9.8 необходимо сначала включить режим диспетчера ресурсов, выполнив команду **Switch-AzureMode AzureResourceManager** .</span><span class="sxs-lookup"><span data-stu-id="f437e-121">When using Azure PowerShell 0.9.8, you must first enable the Resource Manager mode by running the **Switch-AzureMode AzureResourceManager** command.</span></span> <span data-ttu-id="f437e-122">Эта команда не требуется в версии 1.0 и более поздних версиях.</span><span class="sxs-lookup"><span data-stu-id="f437e-122">This command is not necessary in 1.0 or later.</span></span>

<span data-ttu-id="f437e-123">Если вы хотите использовать сценарии, написанные для PowerShell 0.9.8, в среде 1.0 и более поздних версий, следует тщательно протестировать эти сценарии в подготовительной среде, прежде чем использовать их в рабочей среде. Это позволит избежать непредвиденных последствий.</span><span class="sxs-lookup"><span data-stu-id="f437e-123">If you want to use your scripts written for the 0.9.8 environment, in the 1.0 or later environment, you should carefully test the scripts in a pre-production environment before using them in production to avoid unexpected impact.</span></span>

<span data-ttu-id="f437e-124">[Скачайте последнюю версию PowerShell](https://github.com/Azure/azure-powershell/releases) (минимальная требуемая версия — 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="f437e-124">[Download the latest PowerShell release](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>

[!INCLUDE [arm-getting-setup-powershell](../../includes/arm-getting-setup-powershell.md)]

## <a name="create-a-backup-vault"></a><span data-ttu-id="f437e-125">создать хранилище архивации;</span><span class="sxs-lookup"><span data-stu-id="f437e-125">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="f437e-126">Для клиентов, использующих службу архивации Azure впервые, необходимо зарегистрировать поставщика службы архивации для использования с вашей подпиской.</span><span class="sxs-lookup"><span data-stu-id="f437e-126">For customers using Azure Backup for the first time, you need to register the Azure Backup provider to be used with your subscription.</span></span> <span data-ttu-id="f437e-127">Для этого выполните следующую команду: Register-AzureProvider -ProviderNamespace "Microsoft.Backup"</span><span class="sxs-lookup"><span data-stu-id="f437e-127">This can be done by running the following command: Register-AzureProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="f437e-128">Вы можете создать новое хранилище службы архивации с помощью командлета **New-AzureRMBackupVault** .</span><span class="sxs-lookup"><span data-stu-id="f437e-128">You can create a new backup vault using the **New-AzureRMBackupVault** cmdlet.</span></span> <span data-ttu-id="f437e-129">Хранилище архивов представляет собой ресурс ARM, поэтому вам потребуется разместить его в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f437e-129">The backup vault is an ARM resource, so you need to place it within a Resource Group.</span></span> <span data-ttu-id="f437e-130">В консоли Azure PowerShell с повышенными привилегиями выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="f437e-130">In an elevated Azure PowerShell console, run the following commands:</span></span>

```
PS C:\> New-AzureResourceGroup –Name “test-rg” -Region “West US”
PS C:\> $backupvault = New-AzureRMBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

<span data-ttu-id="f437e-131">Для получения списка хранилищ архивации в подписке используйте командлет **Get-AzureRMBackupVault** .</span><span class="sxs-lookup"><span data-stu-id="f437e-131">Use the **Get-AzureRMBackupVault** cmdlet to list the backup vaults in a subscription.</span></span>

## <a name="installing-the-azure-backup-agent"></a><span data-ttu-id="f437e-132">Установка агента службы архивации Azure.</span><span class="sxs-lookup"><span data-stu-id="f437e-132">Installing the Azure Backup agent</span></span>
<span data-ttu-id="f437e-133">Прежде чем устанавливать агент службы архивации Azure, необходимо загрузить установщик и разместить его в системе Windows Server.</span><span class="sxs-lookup"><span data-stu-id="f437e-133">Before you install the Azure Backup agent, you need to have the installer downloaded and present on the Windows Server.</span></span> <span data-ttu-id="f437e-134">Последнюю версию установщика можно загрузить в [центре загрузки Майкрософт](http://aka.ms/azurebackup_agent) или на странице панели мониторинга хранилища архивов.</span><span class="sxs-lookup"><span data-stu-id="f437e-134">You can get the latest version of the installer from the [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from the backup vault's Dashboard page.</span></span> <span data-ttu-id="f437e-135">Сохраните установщик в удобном для вас месте, например в папке *C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="f437e-135">Save the installer to an easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="f437e-136">Чтобы установить агент, в консоли PowerShell с повышенными привилегиями выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f437e-136">To install the agent, run the following command in an elevated PowerShell console:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="f437e-137">Агент будет установлен с параметрами по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f437e-137">This installs the agent with all the default options.</span></span> <span data-ttu-id="f437e-138">Установка займет всего несколько минут и пройдет в фоновом режиме.</span><span class="sxs-lookup"><span data-stu-id="f437e-138">The installation takes a few minutes in the background.</span></span> <span data-ttu-id="f437e-139">Если параметр */nu* не будет указан, в конце установки откроется окно **Обновления Windows** для проверки наличия обновлений.</span><span class="sxs-lookup"><span data-stu-id="f437e-139">If you do not specify the */nu* option then the **Windows Update** window will open at the end of the installation to check for any updates.</span></span> <span data-ttu-id="f437e-140">После установки агент появится в списке установленных программ.</span><span class="sxs-lookup"><span data-stu-id="f437e-140">Once installed, the agent will show in the list of installed programs.</span></span>

<span data-ttu-id="f437e-141">Чтобы просмотреть список установленных программ, выберите **Панель управления** > **Программы** > **Программы и компоненты**.</span><span class="sxs-lookup"><span data-stu-id="f437e-141">To see the list of installed programs, go to **Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Агент установлен](./media/backup-client-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="f437e-143">Параметры установки</span><span class="sxs-lookup"><span data-stu-id="f437e-143">Installation options</span></span>
<span data-ttu-id="f437e-144">Чтобы просмотреть все доступные в командной строке параметры, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f437e-144">To see all the options available via the command-line, use the following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="f437e-145">Доступны следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="f437e-145">The available options include:</span></span>

| <span data-ttu-id="f437e-146">Параметр</span><span class="sxs-lookup"><span data-stu-id="f437e-146">Option</span></span> | <span data-ttu-id="f437e-147">Сведения</span><span class="sxs-lookup"><span data-stu-id="f437e-147">Details</span></span> | <span data-ttu-id="f437e-148">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="f437e-148">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f437e-149">/q</span><span class="sxs-lookup"><span data-stu-id="f437e-149">/q</span></span> |<span data-ttu-id="f437e-150">Позволяет выполнить тихую установку.</span><span class="sxs-lookup"><span data-stu-id="f437e-150">Quiet installation</span></span> |- |
| <span data-ttu-id="f437e-151">/p:"расположение"</span><span class="sxs-lookup"><span data-stu-id="f437e-151">/p:"location"</span></span> |<span data-ttu-id="f437e-152">Путь к папке установки для агента архивации Azure.</span><span class="sxs-lookup"><span data-stu-id="f437e-152">Path to the installation folder for the Azure Backup agent.</span></span> |<span data-ttu-id="f437e-153">C:\Program Files\Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="f437e-153">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="f437e-154">/s:"расположение"</span><span class="sxs-lookup"><span data-stu-id="f437e-154">/s:"location"</span></span> |<span data-ttu-id="f437e-155">Путь к папке кэша для агента архивации Azure.</span><span class="sxs-lookup"><span data-stu-id="f437e-155">Path to the cache folder for the Azure Backup agent.</span></span> |<span data-ttu-id="f437e-156">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="f437e-156">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="f437e-157">/m</span><span class="sxs-lookup"><span data-stu-id="f437e-157">/m</span></span> |<span data-ttu-id="f437e-158">Позволяет явно согласиться на использование Центра обновления Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="f437e-158">Opt-in to Microsoft Update</span></span> |- |
| <span data-ttu-id="f437e-159">/nu</span><span class="sxs-lookup"><span data-stu-id="f437e-159">/nu</span></span> |<span data-ttu-id="f437e-160">Позволяет отказаться от проверки наличия обновлений после завершения установки.</span><span class="sxs-lookup"><span data-stu-id="f437e-160">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="f437e-161">/d</span><span class="sxs-lookup"><span data-stu-id="f437e-161">/d</span></span> |<span data-ttu-id="f437e-162">Удаляет агент служб восстановления Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f437e-162">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="f437e-163">/ph</span><span class="sxs-lookup"><span data-stu-id="f437e-163">/ph</span></span> |<span data-ttu-id="f437e-164">Адрес узла прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="f437e-164">Proxy Host Address</span></span> |- |
| <span data-ttu-id="f437e-165">/po</span><span class="sxs-lookup"><span data-stu-id="f437e-165">/po</span></span> |<span data-ttu-id="f437e-166">Номер порта узла прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="f437e-166">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="f437e-167">/pu</span><span class="sxs-lookup"><span data-stu-id="f437e-167">/pu</span></span> |<span data-ttu-id="f437e-168">Имя пользователя узла прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="f437e-168">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="f437e-169">/pw</span><span class="sxs-lookup"><span data-stu-id="f437e-169">/pw</span></span> |<span data-ttu-id="f437e-170">Пароль прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="f437e-170">Proxy Password</span></span> |- |

## <a name="registering-with-the-azure-backup-service"></a><span data-ttu-id="f437e-171">Регистрация в службе архивации Azure</span><span class="sxs-lookup"><span data-stu-id="f437e-171">Registering with the Azure Backup service</span></span>
<span data-ttu-id="f437e-172">Перед регистрацией в службе резервного копирования Azure убедитесь, что соблюдены [необходимые условия](backup-configure-vault.md) .</span><span class="sxs-lookup"><span data-stu-id="f437e-172">Before you can register with the Azure Backup service, you need to ensure that the [prerequisites](backup-configure-vault.md) are met.</span></span> <span data-ttu-id="f437e-173">Необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="f437e-173">You must:</span></span>

* <span data-ttu-id="f437e-174">Действующая подписка Azure</span><span class="sxs-lookup"><span data-stu-id="f437e-174">Have a valid Azure subscription</span></span>
* <span data-ttu-id="f437e-175">Хранилище архивов</span><span class="sxs-lookup"><span data-stu-id="f437e-175">Have a backup vault</span></span>

<span data-ttu-id="f437e-176">Чтобы скачать учетные данные хранилища, выполните командлет **Get-AzureRMBackupVaultCredentials** в консоли Azure PowerShell. Сохраните данные в удобном расположении, например в папке *C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="f437e-176">To download the vault credentials, run the **Get-AzureRMBackupVaultCredentials** cmdlet in an Azure PowerShell console and store it in a convenient location like *C:\Downloads\*.</span></span>

```
PS C:\> $credspath = "C:\"
PS C:\> $credsfilename = Get-AzureRMBackupVaultCredentials -Vault $backupvault -TargetLocation $credspath
PS C:\> $credsfilename
f5303a0b-fae4-4cdb-b44d-0e4c032dde26_backuprg_backuprn_2015-08-11--06-22-35.VaultCredentials
```

<span data-ttu-id="f437e-177">Регистрация компьютера в хранилище выполняется с помощью командлета [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) :</span><span class="sxs-lookup"><span data-stu-id="f437e-177">Registering the machine with the vault is done using the [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet:</span></span>

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
> <span data-ttu-id="f437e-178">Не используйте относительные пути для указания файла с учетными данными хранилища.</span><span class="sxs-lookup"><span data-stu-id="f437e-178">Do not use relative paths to specify the vault credentials file.</span></span> <span data-ttu-id="f437e-179">Укажите абсолютный путь в качестве входных данных командлета.</span><span class="sxs-lookup"><span data-stu-id="f437e-179">You must provide an absolute path as an input to the cmdlet.</span></span>
>
>

## <a name="networking-settings"></a><span data-ttu-id="f437e-180">Параметры сети</span><span class="sxs-lookup"><span data-stu-id="f437e-180">Networking settings</span></span>
<span data-ttu-id="f437e-181">Если подключение компьютера под управлением Windows к Интернету осуществляется через прокси-сервер, параметры этого прокси-сервера могут сообщаться агенту.</span><span class="sxs-lookup"><span data-stu-id="f437e-181">When the connectivity of the Windows machine to the internet is through a proxy server, the proxy settings can also be provided to the agent.</span></span> <span data-ttu-id="f437e-182">В нашем случае прокси-сервер не используется, поэтому мы явным образом удаляем все данные прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="f437e-182">In this example, there is no proxy server, so we are explicitly clearing any proxy-related information.</span></span>

<span data-ttu-id="f437e-183">Управлять использованием пропускной способности для выбранных дней недели можно с помощью параметров ```work hour bandwidth``` и ```non-work hour bandwidth``` </span><span class="sxs-lookup"><span data-stu-id="f437e-183">Bandwidth usage can also be controlled with the options of ```work hour bandwidth``` and ```non-work hour bandwidth``` for a given set of days of the week.</span></span>

<span data-ttu-id="f437e-184">Внесение сведений о прокси-сервере и пропускной способности выполняется с помощью командлета [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) :</span><span class="sxs-lookup"><span data-stu-id="f437e-184">Setting the proxy and bandwidth details is done using the [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span></span>

```
PS C:\> Set-OBMachineSetting -NoProxy
Server properties updated successfully.

PS C:\> Set-OBMachineSetting -NoThrottle
Server properties updated successfully.
```

## <a name="encryption-settings"></a><span data-ttu-id="f437e-185">Параметры шифрования</span><span class="sxs-lookup"><span data-stu-id="f437e-185">Encryption settings</span></span>
<span data-ttu-id="f437e-186">Для защиты конфиденциальности данных резервные копии данных, отправляемые в службу архивации Azure, зашифровываются.</span><span class="sxs-lookup"><span data-stu-id="f437e-186">The backup data sent to Azure Backup is encrypted to protect the confidentiality of the data.</span></span> <span data-ttu-id="f437e-187">Используемая для шифрования парольная фраза является "паролем" для расшифровки данных во время их восстановления.</span><span class="sxs-lookup"><span data-stu-id="f437e-187">The encryption passphrase is the "password" to decrypt the data at the time of restore.</span></span>

```
PS C:\> ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force | Set-OBMachineSetting
Server properties updated successfully
```

> [!IMPORTANT]
> <span data-ttu-id="f437e-188">После создания парольной фразы надежно сохраните ее и никому не сообщайте о ней.</span><span class="sxs-lookup"><span data-stu-id="f437e-188">Keep the passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="f437e-189">Восстановить данные из Azure без парольной фразы невозможно.</span><span class="sxs-lookup"><span data-stu-id="f437e-189">You will not be able to restore data from Azure without this passphrase.</span></span>
>
>

## <a name="back-up-files-and-folders"></a><span data-ttu-id="f437e-190">Резервное копирование файлов и папок</span><span class="sxs-lookup"><span data-stu-id="f437e-190">Back up files and folders</span></span>
<span data-ttu-id="f437e-191">Для управления всеми резервными копиями с серверов и рабочих станций Windows, которые имеются в службе резервного копирования Azure, применяется соответствующая политика.</span><span class="sxs-lookup"><span data-stu-id="f437e-191">All your backups from Windows Servers and clients to Azure Backup are governed by a policy.</span></span> <span data-ttu-id="f437e-192">Политика состоит из трех частей:</span><span class="sxs-lookup"><span data-stu-id="f437e-192">The policy comprises three parts:</span></span>

1. <span data-ttu-id="f437e-193">**Расписание резервного копирования** — определяет, когда следует создавать резервные копии и синхронизировать их со службой.</span><span class="sxs-lookup"><span data-stu-id="f437e-193">A **backup schedule** that specifies when backups need to be taken and synchronized with the service.</span></span>
2. <span data-ttu-id="f437e-194">**Расписание хранения** — определяет период хранения точек восстановления в Azure.</span><span class="sxs-lookup"><span data-stu-id="f437e-194">A **retention schedule** that specifies how long to retain the recovery points in Azure.</span></span>
3. <span data-ttu-id="f437e-195">**Указания включения/исключения файлов** — определяет, для каких элементов следует создавать резервные копии.</span><span class="sxs-lookup"><span data-stu-id="f437e-195">A **file inclusion/exclusion specification** that dictates what should be backed up.</span></span>

<span data-ttu-id="f437e-196">Поскольку мы будем использовать автоматическое резервное копирование данных, в этой статье предполагается, что заданных настроек нет.</span><span class="sxs-lookup"><span data-stu-id="f437e-196">In this document, since we're automating backup, we'll assume nothing has been configured.</span></span> <span data-ttu-id="f437e-197">Начнем с создания новой политики резервного копирования с помощью командлета [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) .</span><span class="sxs-lookup"><span data-stu-id="f437e-197">We begin by creating a new backup policy using the [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet and using it.</span></span>

```
PS C:\> $newpolicy = New-OBPolicy
```

<span data-ttu-id="f437e-198">В настоящее время политика пуста, и необходимо воспользоваться другими командлетами, чтобы определить, какие элементы будут включены или исключены, когда резервное копирование будет выполняться и где будут храниться резервные копии.</span><span class="sxs-lookup"><span data-stu-id="f437e-198">At this time the policy is empty and other cmdlets are needed to define what items will be included or excluded, when backups will run, and where the backups will be stored.</span></span>

### <a name="configuring-the-backup-schedule"></a><span data-ttu-id="f437e-199">Настройка расписания резервного копирования</span><span class="sxs-lookup"><span data-stu-id="f437e-199">Configuring the backup schedule</span></span>
<span data-ttu-id="f437e-200">Первым из трех компонентов политики является расписание резервного копирования, которое создается с помощью командлета [New-OBSchedule](https://technet.microsoft.com/library/hh770401) .</span><span class="sxs-lookup"><span data-stu-id="f437e-200">The first of the 3 parts of a policy is the backup schedule, which is created using the [New-OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet.</span></span> <span data-ttu-id="f437e-201">В расписании резервного копирования указывается, когда необходимо выполнить резервное копирование.</span><span class="sxs-lookup"><span data-stu-id="f437e-201">The backup schedule defines when backups need to be taken.</span></span> <span data-ttu-id="f437e-202">При создании расписания необходимо указать 2 входных параметра:</span><span class="sxs-lookup"><span data-stu-id="f437e-202">When creating a schedule you need to specify 2 input parameters:</span></span>

* <span data-ttu-id="f437e-203">**Дни недели** , в которые необходимо выполнять резервное копирование.</span><span class="sxs-lookup"><span data-stu-id="f437e-203">**Days of the week** that the backup should run.</span></span> <span data-ttu-id="f437e-204">Можно указать, чтобы задание резервного копирования выполнялось только один день или каждый день недели либо в определенный промежуток времени.</span><span class="sxs-lookup"><span data-stu-id="f437e-204">You can run the backup job on just one day, or every day of the week, or any combination in between.</span></span>
* <span data-ttu-id="f437e-205">**Время** запуска резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="f437e-205">**Times of the day** when the backup should run.</span></span> <span data-ttu-id="f437e-206">Можно определить до трех разных значений времени дня, когда будет выполняться резервное копирование.</span><span class="sxs-lookup"><span data-stu-id="f437e-206">You can define up to 3 different times of the day when the backup will be triggered.</span></span>

<span data-ttu-id="f437e-207">Например, политику резервного копирования можно настроить таким образом, чтобы соответствующее задание выполнялось в 16:00 каждые субботу и воскресенье.</span><span class="sxs-lookup"><span data-stu-id="f437e-207">For instance, you could configure a backup policy that runs at 4PM every Saturday and Sunday.</span></span>

```
PS C:\> $sched = New-OBSchedule -DaysofWeek Saturday, Sunday -TimesofDay 16:00
```

<span data-ttu-id="f437e-208">Расписание резервного копирования должно быть связано с политикой. Этого можно добиться с помощью командлета [Set-OBSchedule](https://technet.microsoft.com/library/hh770407).</span><span class="sxs-lookup"><span data-stu-id="f437e-208">The backup schedule needs to be associated with a policy, and this can be achieved by using the [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet.</span></span>

```
PS C:> Set-OBSchedule -Policy $newpolicy -Schedule $sched
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s) DsList : PolicyName : RetentionPolicy : State : New PolicyState : Valid
```
### <a name="configuring-a-retention-policy"></a><span data-ttu-id="f437e-209">Настройка политики хранения</span><span class="sxs-lookup"><span data-stu-id="f437e-209">Configuring a retention policy</span></span>
<span data-ttu-id="f437e-210">Политика хранения определяет, как долго хранятся точки восстановления, созданные из заданий резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="f437e-210">The retention policy defines how long recovery points created from backup jobs are retained.</span></span> <span data-ttu-id="f437e-211">При создании новой политики хранения с помощью командлета [New-OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) можно указать число дней, в течение которых следует хранить точки восстановления в службе архивации Azure.</span><span class="sxs-lookup"><span data-stu-id="f437e-211">When creating a new retention policy using the [New-OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet, you can specify the number of days that the backup recovery points need to be retained with Azure Backup.</span></span> <span data-ttu-id="f437e-212">В приведенном ниже примере приведена политика хранения точек восстановления в течение 7 дней.</span><span class="sxs-lookup"><span data-stu-id="f437e-212">The example below sets a retention policy of 7 days.</span></span>

```
PS C:\> $retentionpolicy = New-OBRetentionPolicy -RetentionDays 7
```

<span data-ttu-id="f437e-213">Политику хранения следует связать с основной политикой с помощью командлета [Set-OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span><span class="sxs-lookup"><span data-stu-id="f437e-213">The retention policy must be associated with the main policy using the cmdlet [Set-OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span></span>

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
### <a name="including-and-excluding-files-to-be-backed-up"></a><span data-ttu-id="f437e-214">Включение и исключение файлов для резервного копирования</span><span class="sxs-lookup"><span data-stu-id="f437e-214">Including and excluding files to be backed up</span></span>
<span data-ttu-id="f437e-215">Объект ```OBFileSpec``` определяет файлы для включения в резервную копию или исключения из нее.</span><span class="sxs-lookup"><span data-stu-id="f437e-215">An ```OBFileSpec``` object defines the files to be included and excluded in a backup.</span></span> <span data-ttu-id="f437e-216">Это набор правил, которые определяют область защищенных файлов и папок на компьютере.</span><span class="sxs-lookup"><span data-stu-id="f437e-216">This is a set of rules that scope out the protected files and folders on a machine.</span></span> <span data-ttu-id="f437e-217">Можно создать любое количество правил включения или исключения файлов и связать их с политикой.</span><span class="sxs-lookup"><span data-stu-id="f437e-217">You can have as many file inclusion or exclusion rules as required, and associate them with a policy.</span></span> <span data-ttu-id="f437e-218">При создании нового объекта OBFileSpec, можно сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="f437e-218">When creating a new OBFileSpec object, you can:</span></span>

* <span data-ttu-id="f437e-219">указать файлы и папки для включения в резервную копию;</span><span class="sxs-lookup"><span data-stu-id="f437e-219">Specify the files and folders to be included</span></span>
* <span data-ttu-id="f437e-220">указать файлы и папки для исключения из резервной копии;</span><span class="sxs-lookup"><span data-stu-id="f437e-220">Specify the files and folders to be excluded</span></span>
* <span data-ttu-id="f437e-221">указать рекурсивное резервное копирование данных в папке либо указать, что в резервную копию следует включить только файлы верхнего уровня в указанной папке.</span><span class="sxs-lookup"><span data-stu-id="f437e-221">Specify recursive backup of data in a folder (or) whether only the top-level files in the specified folder should be backed up.</span></span>

<span data-ttu-id="f437e-222">Для выполнения последней задачи необходимо установить флаг -NonRecursive в команде New-OBFileSpec.</span><span class="sxs-lookup"><span data-stu-id="f437e-222">The latter is achieved by using the -NonRecursive flag in the New-OBFileSpec command.</span></span>

<span data-ttu-id="f437e-223">В примере ниже выполняется резервное копирование томов C: и D: с исключением двоичных файлов операционной системы в папке Windows и других временных папках.</span><span class="sxs-lookup"><span data-stu-id="f437e-223">In the example below, we'll back up volume C: and D: and exclude the OS binaries in the Windows folder and any temporary folders.</span></span> <span data-ttu-id="f437e-224">Для этого мы создадим две спецификации файлов с помощью командлета [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) — для включения и исключения.</span><span class="sxs-lookup"><span data-stu-id="f437e-224">To do so we'll create two file specifications using the [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - one for inclusion and one for exclusion.</span></span> <span data-ttu-id="f437e-225">После создания спецификации файлов связываются с политикой с помощью командлета [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) .</span><span class="sxs-lookup"><span data-stu-id="f437e-225">Once the file specifications have been created, they're associated with the policy using the [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet.</span></span>

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

### <a name="applying-the-policy"></a><span data-ttu-id="f437e-226">Применение политики</span><span class="sxs-lookup"><span data-stu-id="f437e-226">Applying the policy</span></span>
<span data-ttu-id="f437e-227">Объект политики готов и имеет связанные расписание резервного копирования, политику хранения, а также список включенных и исключенных файлов.</span><span class="sxs-lookup"><span data-stu-id="f437e-227">Now the policy object is complete and has an associated backup schedule, retention policy, and an inclusion/exclusion list of files.</span></span> <span data-ttu-id="f437e-228">На данном этапе эту политику можно зафиксировать в службе архивации Azure для использования.</span><span class="sxs-lookup"><span data-stu-id="f437e-228">This policy can now be committed for Azure Backup to use.</span></span> <span data-ttu-id="f437e-229">Перед применением новой политики убедитесь в отсутствии существующих политик резервного копирования, связанных с сервером, с помощью командлета [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) .</span><span class="sxs-lookup"><span data-stu-id="f437e-229">Before you apply the newly created policy ensure that there are no existing backup policies associated with the server by using the [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet.</span></span> <span data-ttu-id="f437e-230">При удалении политики будет запрошено соответствующее подтверждение.</span><span class="sxs-lookup"><span data-stu-id="f437e-230">Removing the policy will prompt for confirmation.</span></span> <span data-ttu-id="f437e-231">Чтобы пропустить подтверждение, используйте в командлете флаг ```-Confirm:$false``` .</span><span class="sxs-lookup"><span data-stu-id="f437e-231">To skip the confirmation use the ```-Confirm:$false``` flag with the cmdlet.</span></span>

```
PS C:> Get-OBPolicy | Remove-OBPolicy
Microsoft Azure Backup Are you sure you want to remove this backup policy? This will delete all the backed up data. [Y] Yes [A] Yes to All [N] No [L] No to All [S] Suspend [?] Help (default is "Y"):
```

<span data-ttu-id="f437e-232">Фиксация объекта политики выполняется с помощью командлета [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) .</span><span class="sxs-lookup"><span data-stu-id="f437e-232">Committing the policy object is done using the [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet.</span></span> <span data-ttu-id="f437e-233">При этом также будет запрашиваться соответствующее подтверждение.</span><span class="sxs-lookup"><span data-stu-id="f437e-233">This will also ask for confirmation.</span></span> <span data-ttu-id="f437e-234">Чтобы пропустить подтверждение, используйте в командлете флаг ```-Confirm:$false``` .</span><span class="sxs-lookup"><span data-stu-id="f437e-234">To skip the confirmation use the ```-Confirm:$false``` flag with the cmdlet.</span></span>

```
PS C:> Set-OBPolicy -Policy $newpolicy
Microsoft Azure Backup Do you want to save this backup policy ? [Y] Yes [A] Yes to All [N] No [L] No to All [S] Suspend [?] Help (default is "Y"):
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

<span data-ttu-id="f437e-235">Чтобы просмотреть сведения о существующей политике резервного копирования, воспользуйтесь командлетом [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) .</span><span class="sxs-lookup"><span data-stu-id="f437e-235">You can view the details of the existing backup policy using the [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet.</span></span> <span data-ttu-id="f437e-236">Чтобы получить подробные сведения, воспользуйтесь командлетом [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) для расписания архивации и командлетом [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) для политик хранения.</span><span class="sxs-lookup"><span data-stu-id="f437e-236">You can drill-down further using the [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet for the backup schedule and the [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) cmdlet for the retention policies</span></span>

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

### <a name="performing-an-ad-hoc-backup"></a><span data-ttu-id="f437e-237">Выполнение нерегламентированного резервного копирования</span><span class="sxs-lookup"><span data-stu-id="f437e-237">Performing an ad-hoc backup</span></span>
<span data-ttu-id="f437e-238">После настройки соответствующей политики резервное копирование будет выполняться по расписанию.</span><span class="sxs-lookup"><span data-stu-id="f437e-238">Once a backup policy has been set the backups will occur per the schedule.</span></span> <span data-ttu-id="f437e-239">Кроме того, можно выполнить резервное копирование вне регламента с помощью командлета [Start-OBBackup](https://technet.microsoft.com/library/hh770426) :</span><span class="sxs-lookup"><span data-stu-id="f437e-239">Triggering an ad-hoc backup is also possible using the [Start-OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:</span></span>

```
PS C:> Get-OBPolicy | Start-OBBackup
Taking snapshot of volumes...
Preparing storage...
Estimating size of backup items...
Estimating size of backup items...
Transferring data...
Verifying backup...
Job completed.
The backup operation completed successfully.
```

## <a name="restore-data-from-azure-backup"></a><span data-ttu-id="f437e-240">Восстановление данных из службы архивации Azure</span><span class="sxs-lookup"><span data-stu-id="f437e-240">Restore data from Azure Backup</span></span>
<span data-ttu-id="f437e-241">В этом разделе представлены шаги по настройке автоматического восстановления данных из службы архивации Azure.</span><span class="sxs-lookup"><span data-stu-id="f437e-241">This section will guide you through the steps for automating recovery of data from Azure Backup.</span></span> <span data-ttu-id="f437e-242">Выполнение настройки предполагает указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="f437e-242">Doing so involves the following steps:</span></span>

1. <span data-ttu-id="f437e-243">Выбор исходного тома</span><span class="sxs-lookup"><span data-stu-id="f437e-243">Pick the source volume</span></span>
2. <span data-ttu-id="f437e-244">Выбор точки резервного копирования для восстановления</span><span class="sxs-lookup"><span data-stu-id="f437e-244">Choose a backup point to restore</span></span>
3. <span data-ttu-id="f437e-245">Выбор элемента для восстановления</span><span class="sxs-lookup"><span data-stu-id="f437e-245">Choose an item to restore</span></span>
4. <span data-ttu-id="f437e-246">Запуск процесса восстановления</span><span class="sxs-lookup"><span data-stu-id="f437e-246">Trigger the restore process</span></span>

### <a name="picking-the-source-volume"></a><span data-ttu-id="f437e-247">Выбор исходного тома</span><span class="sxs-lookup"><span data-stu-id="f437e-247">Picking the source volume</span></span>
<span data-ttu-id="f437e-248">Чтобы восстановить элемент из службы архивации Azure, сначала необходимо определить его источник.</span><span class="sxs-lookup"><span data-stu-id="f437e-248">In order to restore an item from Azure Backup, you first need to identify the source of the item.</span></span> <span data-ttu-id="f437e-249">Поскольку мы выполняем команды в контексте Windows Server или клиента Windows, компьютер уже определен.</span><span class="sxs-lookup"><span data-stu-id="f437e-249">Since we're executing the commands in the context of a Windows Server or a Windows client, the machine is already identified.</span></span> <span data-ttu-id="f437e-250">Далее необходимо определить том, на котором находится источник элемента.</span><span class="sxs-lookup"><span data-stu-id="f437e-250">The next step in identifying the source is to identify the volume containing it.</span></span> <span data-ttu-id="f437e-251">Список томов или источников, для которых на данном компьютере выполнено резервное копирование, можно получить, выполнив командлет [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) .</span><span class="sxs-lookup"><span data-stu-id="f437e-251">A list of volumes or sources being backed up from this machine can be retrieved by executing the [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet.</span></span> <span data-ttu-id="f437e-252">Эта команда возвращает массив всех источников на сервере или клиенте, для которых созданы резервные копии.</span><span class="sxs-lookup"><span data-stu-id="f437e-252">This command returns an array of all the sources backed up from this server/client.</span></span>

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

### <a name="choosing-a-backup-point-to-restore"></a><span data-ttu-id="f437e-253">Выбор точки резервного копирования для восстановления</span><span class="sxs-lookup"><span data-stu-id="f437e-253">Choosing a backup point to restore</span></span>
<span data-ttu-id="f437e-254">Список точек резервного копирования можно получить, выполнив командлет [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) с соответствующими параметрами.</span><span class="sxs-lookup"><span data-stu-id="f437e-254">The list of backup points can be retrieved by executing the [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet with appropriate parameters.</span></span> <span data-ttu-id="f437e-255">В нашем примере мы выберем последнюю точку резервного копирования для исходного тома *D:* и используем его для восстановления определенного файла.</span><span class="sxs-lookup"><span data-stu-id="f437e-255">In our example, we’ll choose the latest backup point for the source volume *D:* and use it to recover a specific file.</span></span>

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
<span data-ttu-id="f437e-256">Объект ```$rps``` представляет собой массив точек резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="f437e-256">The object ```$rps``` is an array of backup points.</span></span> <span data-ttu-id="f437e-257">Первый элемент является последней точкой, а n-й элемент — самой старой.</span><span class="sxs-lookup"><span data-stu-id="f437e-257">The first element is the latest point and the Nth element is the oldest point.</span></span> <span data-ttu-id="f437e-258">Чтобы выбрать последнюю точку, мы будем использовать ```$rps[0]```.</span><span class="sxs-lookup"><span data-stu-id="f437e-258">To choose the latest point, we will use ```$rps[0]```.</span></span>

### <a name="choosing-an-item-to-restore"></a><span data-ttu-id="f437e-259">Выбор элемента для восстановления</span><span class="sxs-lookup"><span data-stu-id="f437e-259">Choosing an item to restore</span></span>
<span data-ttu-id="f437e-260">Чтобы определить точный файл или папку для восстановления, рекурсивно воспользуйтесь командлетом [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) .</span><span class="sxs-lookup"><span data-stu-id="f437e-260">To identify the exact file or folder to restore, recursively use the [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet.</span></span> <span data-ttu-id="f437e-261">В этом случае иерархию папок можно просматривать только с помощью ```Get-OBRecoverableItem```.</span><span class="sxs-lookup"><span data-stu-id="f437e-261">That way the folder hierarchy can be browsed solely using the ```Get-OBRecoverableItem```.</span></span>

<span data-ttu-id="f437e-262">В этом примере, если нужно восстановить файл *finances.xls*, его можно найти, используя объект ```$filesFolders[1]```.</span><span class="sxs-lookup"><span data-stu-id="f437e-262">In this example, if we want to restore the file *finances.xls* we can reference that using the object ```$filesFolders[1]```.</span></span>

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

<span data-ttu-id="f437e-263">Для поиска элементов для восстановления также можно использовать командлет ```Get-OBRecoverableItem``` .</span><span class="sxs-lookup"><span data-stu-id="f437e-263">You can also search for items to restore using the ```Get-OBRecoverableItem``` cmdlet.</span></span> <span data-ttu-id="f437e-264">В нашем примере, чтобы найти файл *finances.xls* можно получить его дескриптор, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f437e-264">In our example, to search for *finances.xls* we could get a handle on the file by running this command:</span></span>

```
PS C:\> $item = Get-OBRecoverableItem -RecoveryPoint $rps[0] -Location "D:\MyData" -SearchString "finance*"
```

### <a name="triggering-the-restore-process"></a><span data-ttu-id="f437e-265">Запуск процесса восстановления</span><span class="sxs-lookup"><span data-stu-id="f437e-265">Triggering the restore process</span></span>
<span data-ttu-id="f437e-266">Чтобы запустить процесс восстановления, необходимо сначала указать параметры восстановления.</span><span class="sxs-lookup"><span data-stu-id="f437e-266">To trigger the restore process, we first need to specify the recovery options.</span></span> <span data-ttu-id="f437e-267">Это можно сделать с помощью командлета [New-OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) .</span><span class="sxs-lookup"><span data-stu-id="f437e-267">This can be done by using the [New-OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet.</span></span> <span data-ttu-id="f437e-268">В этом примере предположим, что нужно восстановить файлы в папку *C:\temp*.</span><span class="sxs-lookup"><span data-stu-id="f437e-268">For this example, let's assume that we want to restore the files to *C:\temp*.</span></span> <span data-ttu-id="f437e-269">Предположим также, что нужно пропустить файлы, которые уже существуют в целевой папке *C:\temp*.</span><span class="sxs-lookup"><span data-stu-id="f437e-269">Let's also assume that we want to skip files that already exist on the destination folder *C:\temp*.</span></span> <span data-ttu-id="f437e-270">Для создания такого параметра восстановления используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f437e-270">To create such a recovery option, use the following command:</span></span>

```
PS C:\> $recovery_option = New-OBRecoveryOption -DestinationPath "C:\temp" -OverwriteType Skip
```

<span data-ttu-id="f437e-271">Теперь запустите восстановление с помощью команды [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) для выбранного свойства ```$item``` из выходных данных командлета ```Get-OBRecoverableItem```:</span><span class="sxs-lookup"><span data-stu-id="f437e-271">Now trigger restore by using the [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) command on the selected ```$item``` from the output of the ```Get-OBRecoverableItem``` cmdlet:</span></span>

```
PS C:\> Start-OBRecovery -RecoverableItem $item -RecoveryOption $recover_option
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Job completed.
The recovery operation completed successfully.
```


## <a name="uninstalling-the-azure-backup-agent"></a><span data-ttu-id="f437e-272">Удаление агента службы архивации Azure.</span><span class="sxs-lookup"><span data-stu-id="f437e-272">Uninstalling the Azure Backup agent</span></span>
<span data-ttu-id="f437e-273">Удалить агент службы архивации Azure можно с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="f437e-273">Uninstalling the Azure Backup agent can be done by using the following command:</span></span>

```
PS C:\> .\MARSAgentInstaller.exe /d /q
```

<span data-ttu-id="f437e-274">Удаление с компьютера двоичных файлов агента имеет некоторые последствия, которые следует учитывать.</span><span class="sxs-lookup"><span data-stu-id="f437e-274">Uninstalling the agent binaries from the machine has some consequences to consider:</span></span>

* <span data-ttu-id="f437e-275">С компьютера удаляется фильтр файлов, а также останавливается отслеживание изменений.</span><span class="sxs-lookup"><span data-stu-id="f437e-275">It removes the file-filter from the machine, and tracking of changes is stopped.</span></span>
* <span data-ttu-id="f437e-276">Все данные политики удаляются с компьютера, однако сведения о политике по-прежнему хранятся в службе.</span><span class="sxs-lookup"><span data-stu-id="f437e-276">All policy information is removed from the machine, but the policy information continues to be stored in the service.</span></span>
* <span data-ttu-id="f437e-277">Удаляются все расписания резервного копирования, и последующие операции резервного копирования больше не выполняются.</span><span class="sxs-lookup"><span data-stu-id="f437e-277">All backup schedules are removed, and no further backups are taken.</span></span>

<span data-ttu-id="f437e-278">Тем не менее, данные, хранящиеся в Azure, останутся там в течение установленного политикой хранения периода времени.</span><span class="sxs-lookup"><span data-stu-id="f437e-278">However, the data stored in Azure remains and is retained as per the retention policy setup by you.</span></span> <span data-ttu-id="f437e-279">Предыдущие точки восстановления автоматически рассматриваются как устаревшие.</span><span class="sxs-lookup"><span data-stu-id="f437e-279">Older points are automatically aged out.</span></span>

## <a name="remote-management"></a><span data-ttu-id="f437e-280">Удаленное управление</span><span class="sxs-lookup"><span data-stu-id="f437e-280">Remote management</span></span>
<span data-ttu-id="f437e-281">PowerShell обеспечивает удаленное управление агентом службы архивации Azure, политикой и источниками данных.</span><span class="sxs-lookup"><span data-stu-id="f437e-281">All the management around the Azure Backup agent, policies, and data sources can be done remotely through PowerShell.</span></span> <span data-ttu-id="f437e-282">Компьютер, который будет управляться удаленно, необходимо специально подготовить.</span><span class="sxs-lookup"><span data-stu-id="f437e-282">The machine that will be managed remotely needs to be prepared correctly.</span></span>

<span data-ttu-id="f437e-283">По умолчанию служба WinRM настроена на запуск вручную.</span><span class="sxs-lookup"><span data-stu-id="f437e-283">By default, the WinRM service is configured for manual startup.</span></span> <span data-ttu-id="f437e-284">Установите тип запуска *Automatic*. Служба запустится.</span><span class="sxs-lookup"><span data-stu-id="f437e-284">The startup type must be set to *Automatic* and the service should be started.</span></span> <span data-ttu-id="f437e-285">Чтобы проверить работу службы WinRM, присвойте свойству Status значение *Running*.</span><span class="sxs-lookup"><span data-stu-id="f437e-285">To verify that the WinRM service is running, the value of the Status property should be *Running*.</span></span>

```
PS C:\> Get-Service WinRM

Status   Name               DisplayName
------   ----               -----------
Running  winrm              Windows Remote Management (WS-Manag...
```

<span data-ttu-id="f437e-286">Для удаленного взаимодействия необходимо настроить PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f437e-286">PowerShell should be configured for remoting.</span></span>

```
PS C:\> Enable-PSRemoting -force
WinRM is already set up to receive requests on this computer.
WinRM has been updated for remote management.
WinRM firewall exception enabled.

PS C:\> Set-ExecutionPolicy unrestricted -force
```

<span data-ttu-id="f437e-287">Теперь компьютером можно управлять удаленно. Начните с установки агента.</span><span class="sxs-lookup"><span data-stu-id="f437e-287">The machine can now be managed remotely - starting from the installation of the agent.</span></span> <span data-ttu-id="f437e-288">Например, следующий сценарий копирует агент на удаленный компьютер и устанавливает его.</span><span class="sxs-lookup"><span data-stu-id="f437e-288">For example, the following script copies the agent to the remote machine and installs it.</span></span>

```
PS C:\> $dloc = "\\REMOTESERVER01\c$\Windows\Temp"
PS C:\> $agent = "\\REMOTESERVER01\c$\Windows\Temp\MARSAgentInstaller.exe"
PS C:\> $args = "/q"
PS C:\> Copy-Item "C:\Downloads\MARSAgentInstaller.exe" -Destination $dloc - force

PS C:\> $s = New-PSSession -ComputerName REMOTESERVER01
PS C:\> Invoke-Command -Session $s -Script { param($d, $a) Start-Process -FilePath $d $a -Wait } -ArgumentList $agent $args
```

## <a name="next-steps"></a><span data-ttu-id="f437e-289">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f437e-289">Next steps</span></span>
<span data-ttu-id="f437e-290">Дополнительная информация о службе архивации Azure для сервера или клиента Windows</span><span class="sxs-lookup"><span data-stu-id="f437e-290">For more information about Azure Backup for Windows Server/Client see</span></span>

* [<span data-ttu-id="f437e-291">Общие сведения о службе архивации Azure</span><span class="sxs-lookup"><span data-stu-id="f437e-291">Introduction to Azure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="f437e-292">Резервное копирование серверов Windows</span><span class="sxs-lookup"><span data-stu-id="f437e-292">Back up Windows Servers</span></span>](backup-configure-vault.md)
