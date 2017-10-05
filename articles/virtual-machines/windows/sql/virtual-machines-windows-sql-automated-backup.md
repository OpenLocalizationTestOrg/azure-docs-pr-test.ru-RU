---
title: "Автоматическая архивация для виртуальных машин SQL Server 2014 в Azure | Документация Майкрософт"
description: "Описывает функцию автоматической архивации для виртуальных машин SQL Server 2014 в Azure. Данная статья относится к виртуальным машинам, использующим модель развертывания с помощью Resource Manager."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: bdc63fd1-db49-4e76-87d5-b5c6a890e53c
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 91aab896dd5f06c950ee0ed8f36cc6a953d91611
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="automated-backup-for-sql-server-2014-virtual-machines-resource-manager"></a><span data-ttu-id="2cf9a-104">Автоматическая архивация для виртуальных машин SQL Server 2014 (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="2cf9a-104">Automated Backup for SQL Server 2014 Virtual Machines (Resource Manager)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2cf9a-105">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="2cf9a-105">SQL Server 2014</span></span>](virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="2cf9a-106">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="2cf9a-106">SQL Server 2016</span></span>](virtual-machines-windows-sql-automated-backup-v2.md)

<span data-ttu-id="2cf9a-107">Служба автоматической архивации автоматически настраивает [управляемое резервное копирование на портал Microsoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) для всех существующих и новых баз данных на виртуальной машине Azure c SQL Server 2014 Standard или Enterprise.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-107">Automated Backup automatically configures [Managed Backup to Microsoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> <span data-ttu-id="2cf9a-108">Это позволяет настроить регулярную архивацию базы данных с использованием надежного хранилища больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-108">This enables you to configure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="2cf9a-109">Автоматическая архивация зависит от [Расширения агента IaaS для SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="2cf9a-109">Automated Backup depends on the [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="2cf9a-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2cf9a-110">Prerequisites</span></span>
<span data-ttu-id="2cf9a-111">Для использования автоматической архивации необходимо выполнить следующие предварительные требования.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-111">To use Automated Backup, consider the following prerequisites:</span></span>

<span data-ttu-id="2cf9a-112">**Операционная система**</span><span class="sxs-lookup"><span data-stu-id="2cf9a-112">**Operating System**:</span></span>

- <span data-ttu-id="2cf9a-113">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="2cf9a-113">Windows Server 2012</span></span>
- <span data-ttu-id="2cf9a-114">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="2cf9a-114">Windows Server 2012 R2</span></span>
- <span data-ttu-id="2cf9a-115">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="2cf9a-115">Windows Server 2016</span></span>

<span data-ttu-id="2cf9a-116">**Версия/выпуск SQL Server**</span><span class="sxs-lookup"><span data-stu-id="2cf9a-116">**SQL Server version/edition**:</span></span>

- <span data-ttu-id="2cf9a-117">SQL Server 2014 Standard</span><span class="sxs-lookup"><span data-stu-id="2cf9a-117">SQL Server 2014 Standard</span></span>
- <span data-ttu-id="2cf9a-118">SQL Server 2014 Enterprise</span><span class="sxs-lookup"><span data-stu-id="2cf9a-118">SQL Server 2014 Enterprise</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2cf9a-119">Автоматическая архивация работает с SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-119">Automated Backup works with SQL Server 2014.</span></span> <span data-ttu-id="2cf9a-120">Если используется SQL Server 2016, то для архивации баз данных можно применять автоматическую архивацию версии 2.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-120">If you are using SQL Server 2016, you can use Automated Backup v2 to back up your databases.</span></span> <span data-ttu-id="2cf9a-121">Дополнительную информацию см. в статье [Автоматическая архивация версии 2 для виртуальных машин SQL Server 2016 в Azure](virtual-machines-windows-sql-automated-backup-v2.md).</span><span class="sxs-lookup"><span data-stu-id="2cf9a-121">For more information, see [Automated Backup v2 for SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).</span></span>

<span data-ttu-id="2cf9a-122">**Конфигурация базы данных**</span><span class="sxs-lookup"><span data-stu-id="2cf9a-122">**Database configuration**:</span></span>

- <span data-ttu-id="2cf9a-123">В конечных базах данных должна использоваться модель полного восстановления.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-123">Target databases must use the full recovery model.</span></span> <span data-ttu-id="2cf9a-124">Дополнительные сведения о влиянии модели полного восстановления на резервные копии см. в разделе [Резервное копирование в модели полного восстановления](https://technet.microsoft.com/library/ms190217.aspx).</span><span class="sxs-lookup"><span data-stu-id="2cf9a-124">For more information about the impact of the full recovery model on backups, see [Backup Under the Full Recovery Model](https://technet.microsoft.com/library/ms190217.aspx).</span></span>
- <span data-ttu-id="2cf9a-125">Конечные базы данных должны находиться в экземпляре SQL Server по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-125">Target databases must be on the default SQL Server instance.</span></span> <span data-ttu-id="2cf9a-126">Расширение IaaS SQL Server не поддерживает именованные экземпляры.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-126">The SQL Server IaaS Extension does not support named instances.</span></span>

<span data-ttu-id="2cf9a-127">**Модель развертывания Azure**</span><span class="sxs-lookup"><span data-stu-id="2cf9a-127">**Azure deployment model**:</span></span>

- <span data-ttu-id="2cf9a-128">Диспетчер ресурсов</span><span class="sxs-lookup"><span data-stu-id="2cf9a-128">Resource Manager</span></span>

<span data-ttu-id="2cf9a-129">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="2cf9a-129">**Azure PowerShell**:</span></span>

- <span data-ttu-id="2cf9a-130">[Установите последнюю версию Azure PowerShell](/powershell/azure/overview) , если планируете настраивать автоматизированную архивацию с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-130">[Install the latest Azure PowerShell commands](/powershell/azure/overview) if you plan to configure Automated Backup with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="2cf9a-131">Автоматическая архивация зависит от расширения агента IaaS для SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-131">Automated Backup relies on the SQL Server IaaS Agent Extension.</span></span> <span data-ttu-id="2cf9a-132">В текущей коллекции образов виртуальных машин SQL это расширение присутствует по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-132">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="2cf9a-133">Дополнительные сведения см. в статье [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md) (Расширение агента SQL Server IaaS).</span><span class="sxs-lookup"><span data-stu-id="2cf9a-133">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="2cf9a-134">Параметры</span><span class="sxs-lookup"><span data-stu-id="2cf9a-134">Settings</span></span>

<span data-ttu-id="2cf9a-135">В приведенной ниже таблице описаны параметры настройки автоматической архивации.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-135">The following table describes the options that can be configured for Automated Backup.</span></span> <span data-ttu-id="2cf9a-136">Фактическая процедура настройки может варьироваться в зависимости от того, используете вы портал Azure или команды Azure Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-136">The actual configuration steps vary depending on whether you use the Azure portal or Azure Windows PowerShell commands.</span></span>

| <span data-ttu-id="2cf9a-137">Настройка</span><span class="sxs-lookup"><span data-stu-id="2cf9a-137">Setting</span></span> | <span data-ttu-id="2cf9a-138">Диапазон (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="2cf9a-138">Range (Default)</span></span> | <span data-ttu-id="2cf9a-139">Описание</span><span class="sxs-lookup"><span data-stu-id="2cf9a-139">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2cf9a-140">**Автоматическая архивация**</span><span class="sxs-lookup"><span data-stu-id="2cf9a-140">**Automated Backup**</span></span> | <span data-ttu-id="2cf9a-141">Включено/отключено (отключено)</span><span class="sxs-lookup"><span data-stu-id="2cf9a-141">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="2cf9a-142">Включает или отключает автоматическую архивацию для виртуальной машины Azure под управлением SQL Server 2014 Standard или Enterprise.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-142">Enables or disables Automated Backup for an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> |
| <span data-ttu-id="2cf9a-143">**Срок хранения**</span><span class="sxs-lookup"><span data-stu-id="2cf9a-143">**Retention Period**</span></span> | <span data-ttu-id="2cf9a-144">1–30 дней (30 дней)</span><span class="sxs-lookup"><span data-stu-id="2cf9a-144">1-30 days (30 days)</span></span> | <span data-ttu-id="2cf9a-145">Число дней хранения резервной копии.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-145">The number of days to retain a backup.</span></span> |
| <span data-ttu-id="2cf9a-146">**Учетная запись хранения**</span><span class="sxs-lookup"><span data-stu-id="2cf9a-146">**Storage Account**</span></span> | <span data-ttu-id="2cf9a-147">Учетная запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-147">Azure storage account</span></span> | <span data-ttu-id="2cf9a-148">Учетная запись хранения Azure для хранения файлов автоматической архивации в хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-148">An Azure storage account to use for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="2cf9a-149">Там же создается контейнер для хранения всех файлов резервных копий.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-149">A container is created at this location to store all backup files.</span></span> <span data-ttu-id="2cf9a-150">Имя файла резервной копии содержит дату, время и имя компьютера.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-150">The backup file naming convention includes the date, time, and machine name.</span></span> |
| <span data-ttu-id="2cf9a-151">**Шифрование**</span><span class="sxs-lookup"><span data-stu-id="2cf9a-151">**Encryption**</span></span> | <span data-ttu-id="2cf9a-152">Включено/отключено (отключено)</span><span class="sxs-lookup"><span data-stu-id="2cf9a-152">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="2cf9a-153">Включает или отключает шифрование.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-153">Enables or disables encryption.</span></span> <span data-ttu-id="2cf9a-154">Если шифрование включено, то сертификаты, используемые для восстановления резервной копии, сохраняются в указанной учетной записи хранения в том же контейнере `automaticbackup` с использованием того же соглашения об именовании файлов.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-154">When encryption is enabled, the certificates used to restore the backup are located in the specified storage account in the same `automaticbackup` container using the same naming convention.</span></span> <span data-ttu-id="2cf9a-155">При изменении пароля создается новый сертификат; при этом старый сертификат сохраняется для восстановления предыдущих резервных копий.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-155">If the password changes, a new certificate is generated with that password, but the old certificate remains to restore prior backups.</span></span> |
| <span data-ttu-id="2cf9a-156">**Пароль**</span><span class="sxs-lookup"><span data-stu-id="2cf9a-156">**Password**</span></span> | <span data-ttu-id="2cf9a-157">Текст пароля</span><span class="sxs-lookup"><span data-stu-id="2cf9a-157">Password text</span></span> | <span data-ttu-id="2cf9a-158">Пароль для ключей шифрования.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-158">A password for encryption keys.</span></span> <span data-ttu-id="2cf9a-159">Требуется, только если шифрование включено.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-159">This is only required if encryption is enabled.</span></span> <span data-ttu-id="2cf9a-160">Для восстановления зашифрованной резервной копии требуется правильный пароль и соответствующий сертификат, который использовался при создании резервной копии.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-160">In order to restore an encrypted backup, you must have the correct password and related certificate that was used at the time the backup was taken.</span></span> |

## <a name="configuration-in-the-portal"></a><span data-ttu-id="2cf9a-161">Настройка на портале</span><span class="sxs-lookup"><span data-stu-id="2cf9a-161">Configuration in the Portal</span></span>

<span data-ttu-id="2cf9a-162">Для настройки автоматической архивации при подготовке виртуальных машин SQL Server 2014 или для существующих виртуальных машин SQL Server 2016 можно использовать портал Azure.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-162">You can use the Azure portal to configure Automated Backup during provisioning or for existing SQL Server 2014 VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="2cf9a-163">Новые виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="2cf9a-163">New VMs</span></span>

<span data-ttu-id="2cf9a-164">При создании новой виртуальной машины SQL Server 2014 с моделью развертывания с помощью Resource Manager настройте автоматическую архивацию, используя портал Azure.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-164">Use the Azure portal to configure Automated Backup when you create a new SQL Server 2014 Virtual Machine in the Resource Manager deployment model.</span></span>

<span data-ttu-id="2cf9a-165">В колонке **Параметры SQL Server** выберите **Автоматизированная архивация**.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-165">In the **SQL Server settings** blade, select **Automated backup**.</span></span> <span data-ttu-id="2cf9a-166">Колонка **Автоматизированная архивация SQL** показана на следующем снимке экрана портала Azure.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-166">The following Azure portal screenshot shows the **SQL Automated Backup** blade.</span></span>

![Настройка автоматической архивации SQL на портале Azure](./media/virtual-machines-windows-sql-automated-backup/azure-sql-arm-autobackup.png)

<span data-ttu-id="2cf9a-168">Сведения о контексте приведены в полном описании в статье [Подготовка виртуальной машины SQL Server на портале Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="2cf9a-168">For context, see the complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="2cf9a-169">Существующие виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="2cf9a-169">Existing VMs</span></span>

<span data-ttu-id="2cf9a-170">Выберите существующую виртуальную машину SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-170">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="2cf9a-171">Затем в колонке **Параметры** выберите раздел **Конфигурация SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-171">Then select the **SQL Server configuration** section of the **Settings** blade.</span></span>

![Автоматизированная архивация SQL для существующих виртуальных машин](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-existing-vms.png)

<span data-ttu-id="2cf9a-173">В колонке **Конфигурация SQL Server** нажмите кнопку **Изменить** в разделе "Автоматизированная архивация".</span><span class="sxs-lookup"><span data-stu-id="2cf9a-173">In the **SQL Server configuration** blade, click the **Edit** button in the Automated backup section.</span></span>

![Настройка автоматизированной архивации SQL для существующих виртуальных машин](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-configuration.png)

<span data-ttu-id="2cf9a-175">По завершении нажмите кнопку **ОК** в нижней части колонки **Конфигурация SQL Server**, чтобы сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-175">When finished, click the **OK** button on the bottom of the **SQL Server configuration** blade to save your changes.</span></span>

<span data-ttu-id="2cf9a-176">Если автоматизированная архивация включается впервые, Azure настроит агент IaaS SQL Server в фоновом режиме.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-176">If you are enabling Automated Backup for the first time, Azure configures the SQL Server IaaS Agent in the background.</span></span> <span data-ttu-id="2cf9a-177">При этом портал Azure может не сообщать о том, что выполняется настройка автоматической архивации.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-177">During this time, the Azure portal might not show that Automated Backup is configured.</span></span> <span data-ttu-id="2cf9a-178">Установка и настройка агента занимают несколько минут.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-178">Wait several minutes for the agent to be installed, configured.</span></span> <span data-ttu-id="2cf9a-179">После этого новые параметры отобразятся на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-179">After that the Azure portal will reflect the new settings.</span></span>

> [!NOTE]
> <span data-ttu-id="2cf9a-180">Можно также настроить автоматизированную архивацию с помощью шаблона.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-180">You can also configure Automated Backup using a template.</span></span> <span data-ttu-id="2cf9a-181">Чтобы получить дополнительные сведения, ознакомьтесь с [шаблоном быстрого запуска Azure для автоматизированной архивации](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update).</span><span class="sxs-lookup"><span data-stu-id="2cf9a-181">For more information, see [Azure quickstart template for Automated Backup](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update).</span></span>

## <a name="configuration-with-powershell"></a><span data-ttu-id="2cf9a-182">Настройка с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="2cf9a-182">Configuration with PowerShell</span></span>

<span data-ttu-id="2cf9a-183">Для настройки автоматической архивации можно также использовать PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-183">You can use PowerShell to configure Automated Backup.</span></span> <span data-ttu-id="2cf9a-184">Предварительно необходимо выполнить следующее.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-184">Before you begin, you must:</span></span>

- <span data-ttu-id="2cf9a-185">[Скачайте и установите последнюю версию Azure PowerShell](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="2cf9a-185">[Download and install the latest Azure PowerShell](http://aka.ms/webpi-azps).</span></span>
- <span data-ttu-id="2cf9a-186">Откройте компонент Windows PowerShell и свяжите его со своей учетной записью.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-186">Open Windows PowerShell and associate it with your account.</span></span> <span data-ttu-id="2cf9a-187">Это можно сделать, выполнив действия, описанные в посвященном подготовке разделе [Настройка подписки](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription).</span><span class="sxs-lookup"><span data-stu-id="2cf9a-187">You can do this by following the steps in the [Configure your subscription](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) section of the provisioning topic.</span></span>

### <a name="install-the-sql-iaas-extension"></a><span data-ttu-id="2cf9a-188">Установка расширения IaaS для SQL Server</span><span class="sxs-lookup"><span data-stu-id="2cf9a-188">Install the SQL IaaS Extension</span></span>
<span data-ttu-id="2cf9a-189">Если виртуальная машина SQL Server подготовлена на портале Azure, то на ней уже должно быть установлено расширение IaaS для SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-189">If you provisioned a SQL Server virtual machine from the Azure portal, the SQL Server IaaS Extension should already be installed.</span></span> <span data-ttu-id="2cf9a-190">Выяснить, установлено ли оно на виртуальной машины, можно, выполнив команду **Get-AzureRmVM** и изучив свойство **Extensions**.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-190">You can determine if it is installed for your VM by calling **Get-AzureRmVM** command and examining the **Extensions** property.</span></span>

```powershell
$vmname = "vmname"
$resourcegroupname = "resourcegroupname"

(Get-AzureRmVM -Name $vmname -ResourceGroupName $resourcegroupname).Extensions
```

<span data-ttu-id="2cf9a-191">Если расширение агента IaaS для SQL Server установлено, вы увидите его в списке как SqlIaaSAgent или SQLIaaSExtension.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-191">If the SQL Server IaaS Agent extension is installed, you should see it listed as “SqlIaaSAgent” or “SQLIaaSExtension”.</span></span> <span data-ttu-id="2cf9a-192">Значением **ProvisioningState** для расширения также должно быть "Succeeded".</span><span class="sxs-lookup"><span data-stu-id="2cf9a-192">**ProvisioningState** for the extension should also show “Succeeded”.</span></span>

<span data-ttu-id="2cf9a-193">Если расширение не установлено или его не удалось подготовить, то для его установки можно выполнить приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-193">If it is not installed or failed to be provisioned, you can install it with the following command.</span></span> <span data-ttu-id="2cf9a-194">Кроме имени и группы ресурсов виртуальной машины, необходимо указать регион (**$region**), в котором она расположена.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-194">In addition to the VM name and resource group, you must also specify the region (**$region**) that your VM is located in.</span></span>

```powershell
$region = “EASTUS2”
Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region
```

### <span data-ttu-id="2cf9a-195"><a id="verifysettings"></a> Проверка текущих параметров</span><span class="sxs-lookup"><span data-stu-id="2cf9a-195"><a id="verifysettings"></a> Verify current settings</span></span>

<span data-ttu-id="2cf9a-196">Если вы включили автоматическую архивацию во время подготовки, то можете использовать PowerShell для проверки текущей конфигурации.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-196">If you enabled automated backup during provisioning, you can use PowerShell to check your current configuration.</span></span> <span data-ttu-id="2cf9a-197">Выполните команду **Get-AzureRmVMSqlServerExtension** и изучите свойство **AutoBackupSettings**.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-197">Run the **Get-AzureRmVMSqlServerExtension** command and examine the **AutoBackupSettings** property:</span></span>

```powershell
(Get-AzureRmVMSqlServerExtension -VMName $vmname -ResourceGroupName $resourcegroupname).AutoBackupSettings
```

<span data-ttu-id="2cf9a-198">Должен отобразиться результат, аналогичный приведенному ниже.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-198">You should get output similar to the following:</span></span>

```
Enable                      : False
EnableEncryption            : False
RetentionPeriod             : -1
StorageUrl                  : NOTSET
StorageAccessKey            : 
Password                    : 
BackupSystemDbs             : False
BackupScheduleType          : 
FullBackupFrequency         : 
FullBackupStartTime         : 
FullBackupWindowHours       : 
LogBackupFrequency          : 
```

<span data-ttu-id="2cf9a-199">Если выходные данные показывают, что значение **Enable** равно **False**, то необходимо включить автоматическую архивацию.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-199">If your output shows that **Enable** is set to **False**, then you have to enable automated backup.</span></span> <span data-ttu-id="2cf9a-200">Хорошая новость состоит в том, что включить и настроить автоматическую архивацию можно точно так же.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-200">The good news is that you enable and configure Automated Backup in the same way.</span></span> <span data-ttu-id="2cf9a-201">Этот процесс описан в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-201">See the next section for this information.</span></span>

> [!NOTE] 
> <span data-ttu-id="2cf9a-202">Если вы проверяете параметры сразу же после внесения изменений, возможно, вы увидите старые значения конфигурации.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-202">If you check the settings immediately after making a change, it is possible that you will get back the old configuration values.</span></span> <span data-ttu-id="2cf9a-203">Подождите несколько минут и проверьте параметры, чтобы убедиться, что изменения были применены.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-203">Wait a few minutes and check the settings again to make sure that your changes were applied.</span></span>

### <a name="configure-automated-backup"></a><span data-ttu-id="2cf9a-204">Настройка автоматической архивации</span><span class="sxs-lookup"><span data-stu-id="2cf9a-204">Configure Automated Backup</span></span>
<span data-ttu-id="2cf9a-205">Чтобы включить автоматическую архивацию, а также в любое время изменить ее конфигурацию и поведение, можно использовать PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-205">You can use PowerShell to enable Automated Backup as well as to modify its configuration and behavior at any time.</span></span>

<span data-ttu-id="2cf9a-206">Сначала выберите или создайте учетную запись хранения для файлов резервных копий.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-206">First, select or create a storage account for the backup files.</span></span> <span data-ttu-id="2cf9a-207">Приведенный ниже сценарий выбирает учетную запись хранения или создает ее, если она не существует.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-207">The following script selects a storage account or creates it if it does not exist.</span></span>

```powershell
$storage_accountname = “yourstorageaccount”
$storage_resourcegroupname = $resourcegroupname

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }
```

> [!NOTE]
> <span data-ttu-id="2cf9a-208">Служба автоматической архивации не поддерживает хранение резервных копий в хранилище уровня "Премиум", но может создавать резервные копии дисков виртуальных машин, которые используют хранилище уровня "Премиум".</span><span class="sxs-lookup"><span data-stu-id="2cf9a-208">Automated Backup does not support storing backups in premium storage, but it can take backups from VM disks which use Premium Storage.</span></span>

<span data-ttu-id="2cf9a-209">Затем выполните команду **New-AzureRmVMSqlServerAutoBackupConfig**, чтобы включить и настроить параметры автоматической архивации для хранения архивных копий в учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-209">Then use the **New-AzureRmVMSqlServerAutoBackupConfig** command to enable and configure the Automated Backup settings to store backups in the Azure storage account.</span></span> <span data-ttu-id="2cf9a-210">В этом примере резервные копии хранятся в течение 10 дней.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-210">In this example, the backups are set to be retained for 10 days.</span></span> <span data-ttu-id="2cf9a-211">Вторая команда, **Set-AzureRmVMSqlServerExtension**, обновляет указанную виртуальную машину Azure в соответствии с заданными параметрами.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-211">The second command, **Set-AzureRmVMSqlServerExtension**, updates the specified Azure VM with these settings.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

<span data-ttu-id="2cf9a-212">Установка и настройка агента SQL Server IaaS занимают несколько минут.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-212">It could take several minutes to install and configure the SQL Server IaaS Agent.</span></span>

> [!NOTE]
> <span data-ttu-id="2cf9a-213">Существуют и другие параметры для **New-AzureRmVMSqlServerAutoBackupConfig**, которые применяются только для SQL Server 2016 и автоматической архивации версии 2.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-213">There are other settings for **New-AzureRmVMSqlServerAutoBackupConfig** that apply only to SQL Server 2016 and Automated Backup v2.</span></span> <span data-ttu-id="2cf9a-214">SQL Server 2014 не поддерживает следующие параметры: **BackupSystemDbs**, **BackupScheduleType**, **FullBackupFrequency**, **FullBackupStartHour**, **FullBackupWindowInHours** и **LogBackupFrequencyInMinutes**.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-214">SQL Server 2014 does not support the following settings: **BackupSystemDbs**, **BackupScheduleType**, **FullBackupFrequency**, **FullBackupStartHour**, **FullBackupWindowInHours**, and **LogBackupFrequencyInMinutes**.</span></span> <span data-ttu-id="2cf9a-215">При попытке настроить эти параметры на виртуальной машине SQL Server 2014 ошибки не возникают, но параметры не применяется.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-215">If you attempt to configure these settings on a SQL Server 2014 virtual machine, there is no error, but the settings do not get applied.</span></span> <span data-ttu-id="2cf9a-216">Если вы хотите использовать эти параметры на виртуальной машине SQL Server 2016, см. раздел [Автоматическая архивация версии 2 для виртуальных машин Azure SQL Server 2016](virtual-machines-windows-sql-automated-backup-v2.md).</span><span class="sxs-lookup"><span data-stu-id="2cf9a-216">If you want to use these settings on a SQL Server 2016 virtual machine, see [Automated Backup v2 for SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).</span></span>

<span data-ttu-id="2cf9a-217">Чтобы включить шифрование, измените предыдущий сценарий таким образом, чтобы он передавал параметр **EnableEncryption** вместе с паролем (защищенной строкой) для параметра **CertificatePassword**.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-217">To enable encryption, modify the previous script to pass the **EnableEncryption** parameter along with a password (secure string) for the **CertificatePassword** parameter.</span></span> <span data-ttu-id="2cf9a-218">Следующий скрипт активирует параметры автоматической архивации их предыдущего примера и добавляет шифрование.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-218">The following script enables the Automated Backup settings in the previous example and adds encryption.</span></span>

```powershell
$password = "P@ssw0rd"
$encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -EnableEncryption -CertificatePassword $encryptionpassword `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

<span data-ttu-id="2cf9a-219">Чтобы убедиться, что параметры были применены, [проверьте конфигурацию автоматической архивации](#verifysettings).</span><span class="sxs-lookup"><span data-stu-id="2cf9a-219">To confirm your settings are applied, [verify the Automated Backup configuration](#verifysettings).</span></span>

### <a name="disable-automated-backup"></a><span data-ttu-id="2cf9a-220">Отключение автоматической архивации</span><span class="sxs-lookup"><span data-stu-id="2cf9a-220">Disable Automated Backup</span></span>

<span data-ttu-id="2cf9a-221">Чтобы отключить автоматическую архивацию, выполните тот же сценарий без параметра **-Enable** в команде **New-AzureRmVMSqlServerAutoBackupConfig**.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-221">To disable Automated Backup, run the same script without the **-Enable** parameter to the **New-AzureRmVMSqlServerAutoBackupConfig** command.</span></span> <span data-ttu-id="2cf9a-222">Отсутствие параметра **-Enable** означает, что функцию нужно отключить.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-222">The absence of the **-Enable** parameter signals the command to disable the feature.</span></span> <span data-ttu-id="2cf9a-223">Как и установка, отключение автоматической архивации занимает несколько минут.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-223">As with installation, it can take several minutes to disable Automated Backup.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

### <a name="example-script"></a><span data-ttu-id="2cf9a-224">Пример сценария</span><span class="sxs-lookup"><span data-stu-id="2cf9a-224">Example script</span></span>

<span data-ttu-id="2cf9a-225">Ниже приведен сценарий, предоставляющий набор переменных, которые можно задать для включения и настройки автоматической архивации для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-225">The following script provides a set of variables that you can customize to enable and configure Automated Backup for your VM.</span></span> <span data-ttu-id="2cf9a-226">Может потребоваться настроить этот сценарий в зависимости от ваших требований.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-226">In your case, you might need to customize the script based on your requirements.</span></span> <span data-ttu-id="2cf9a-227">Например, его нужно будет изменить, если вы захотите включить шифрование или отключить архивацию системных баз данных.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-227">For example, you would have to make changes if you wanted to disable the backup of system databases or enable encryption.</span></span>

```powershell
$vmname = "yourvmname"
$resourcegroupname = "vmresourcegroupname"
$region = “Azure region name such as EASTUS2”
$storage_accountname = “storageaccountname”
$storage_resourcegroupname = $resourcegroupname
$retentionperiod = 10

# ResourceGroupName is the resource group which is hosting the VM where you are deploying the SQL IaaS Extension

Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region

# Creates/use a storage account to store the backups

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }

# Configure Automated Backup settings

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays $retentionperiod -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

# Apply the Automated Backup settings to the VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="2cf9a-228">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2cf9a-228">Next steps</span></span>

<span data-ttu-id="2cf9a-229">Автоматическая архивация настраивает управляемое резервное копирование на виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-229">Automated Backup configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="2cf9a-230">В связи с этим важно изучить [документацию по управляемой архивации](https://msdn.microsoft.com/library/dn449496.aspx) и понять, как она работает.</span><span class="sxs-lookup"><span data-stu-id="2cf9a-230">So it is important to [review the documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) to understand the behavior and implications.</span></span>

<span data-ttu-id="2cf9a-231">Дополнительные сведения об архивации и восстановлении SQL Server на виртуальных машинах Azure см. в статье [Архивация и восстановление SQL Server на виртуальных машинах Azure](virtual-machines-windows-sql-backup-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="2cf9a-231">You can find additional backup and restore guidance for SQL Server on Azure VMs in the following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span></span>

<span data-ttu-id="2cf9a-232">Сведения о других доступных задачах автоматизации см. в разделе [Расширение агента IaaS для SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="2cf9a-232">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="2cf9a-233">Дополнительные сведения о запуске SQL Server на виртуальных машинах Azure см. в [обзоре использования SQL Server на виртуальных машинах Azure](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2cf9a-233">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

