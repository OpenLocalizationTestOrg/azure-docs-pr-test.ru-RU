---
title: "aaaAutomated резервного копирования для SQL Server 2014 виртуальных машин Azure | Документы Microsoft"
description: "Описывается функция hello автоматического резервного копирования для SQL Server 2014 работающих виртуальных машин в Azure. Эта статья содержит определенные tooVMs, с помощью диспетчера ресурсов hello."
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
ms.openlocfilehash: c6803d8ef9f80e44a2f87918d87e099f1b562483
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-for-sql-server-2014-virtual-machines-resource-manager"></a><span data-ttu-id="cf8e5-104">Автоматическая архивация для виртуальных машин SQL Server 2014 (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="cf8e5-104">Automated Backup for SQL Server 2014 Virtual Machines (Resource Manager)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="cf8e5-105">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="cf8e5-105">SQL Server 2014</span></span>](virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="cf8e5-106">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="cf8e5-106">SQL Server 2016</span></span>](virtual-machines-windows-sql-automated-backup-v2.md)

<span data-ttu-id="cf8e5-107">Автоматическое резервное копирование автоматически настраивает [tooMicrosoft управляемого резервного копирования Azure](https://msdn.microsoft.com/library/dn449496.aspx) для всех существующих и новых баз данных на виртуальной Машине Azure под управлением SQL Server 2014 Standard или Enterprise.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-107">Automated Backup automatically configures [Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> <span data-ttu-id="cf8e5-108">Это позволяет tooconfigure регулярные резервные копии, использовать устойчивые Azure BLOB-объекта хранилища.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-108">This enables you tooconfigure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="cf8e5-109">Автоматическая архивация зависит от hello [расширения агента SQL Server IaaS](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="cf8e5-109">Automated Backup depends on hello [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="cf8e5-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="cf8e5-110">Prerequisites</span></span>
<span data-ttu-id="cf8e5-111">toouse автоматическое резервное копирование, примите во внимание следующие предварительные требования hello.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-111">toouse Automated Backup, consider hello following prerequisites:</span></span>

<span data-ttu-id="cf8e5-112">**Операционная система**</span><span class="sxs-lookup"><span data-stu-id="cf8e5-112">**Operating System**:</span></span>

- <span data-ttu-id="cf8e5-113">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="cf8e5-113">Windows Server 2012</span></span>
- <span data-ttu-id="cf8e5-114">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="cf8e5-114">Windows Server 2012 R2</span></span>
- <span data-ttu-id="cf8e5-115">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="cf8e5-115">Windows Server 2016</span></span>

<span data-ttu-id="cf8e5-116">**Версия/выпуск SQL Server**</span><span class="sxs-lookup"><span data-stu-id="cf8e5-116">**SQL Server version/edition**:</span></span>

- <span data-ttu-id="cf8e5-117">SQL Server 2014 Standard</span><span class="sxs-lookup"><span data-stu-id="cf8e5-117">SQL Server 2014 Standard</span></span>
- <span data-ttu-id="cf8e5-118">SQL Server 2014 Enterprise</span><span class="sxs-lookup"><span data-stu-id="cf8e5-118">SQL Server 2014 Enterprise</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cf8e5-119">Автоматическая архивация работает с SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-119">Automated Backup works with SQL Server 2014.</span></span> <span data-ttu-id="cf8e5-120">При использовании SQL Server 2016 можно использовать автоматическое резервное копирование v2 tooback копии баз данных.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-120">If you are using SQL Server 2016, you can use Automated Backup v2 tooback up your databases.</span></span> <span data-ttu-id="cf8e5-121">Дополнительную информацию см. в статье [Автоматическая архивация версии 2 для виртуальных машин SQL Server 2016 в Azure](virtual-machines-windows-sql-automated-backup-v2.md).</span><span class="sxs-lookup"><span data-stu-id="cf8e5-121">For more information, see [Automated Backup v2 for SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).</span></span>

<span data-ttu-id="cf8e5-122">**Конфигурация базы данных**</span><span class="sxs-lookup"><span data-stu-id="cf8e5-122">**Database configuration**:</span></span>

- <span data-ttu-id="cf8e5-123">Целевые базы данных должна использовать модель полного восстановления hello.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-123">Target databases must use hello full recovery model.</span></span> <span data-ttu-id="cf8e5-124">Дополнительные сведения о влиянии hello hello модель полного восстановления резервных копий см. в разделе [hello резервного копирования в модели полного восстановления](https://technet.microsoft.com/library/ms190217.aspx).</span><span class="sxs-lookup"><span data-stu-id="cf8e5-124">For more information about hello impact of hello full recovery model on backups, see [Backup Under hello Full Recovery Model](https://technet.microsoft.com/library/ms190217.aspx).</span></span>
- <span data-ttu-id="cf8e5-125">Целевые базы данных должен быть на экземпляре SQL Server по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-125">Target databases must be on hello default SQL Server instance.</span></span> <span data-ttu-id="cf8e5-126">Hello расширения IaaS SQL Server не поддерживает именованные экземпляры.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-126">hello SQL Server IaaS Extension does not support named instances.</span></span>

<span data-ttu-id="cf8e5-127">**Модель развертывания Azure**</span><span class="sxs-lookup"><span data-stu-id="cf8e5-127">**Azure deployment model**:</span></span>

- <span data-ttu-id="cf8e5-128">Диспетчер ресурсов</span><span class="sxs-lookup"><span data-stu-id="cf8e5-128">Resource Manager</span></span>

<span data-ttu-id="cf8e5-129">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="cf8e5-129">**Azure PowerShell**:</span></span>

- <span data-ttu-id="cf8e5-130">[Установка последних команд Azure PowerShell hello](/powershell/azure/overview) при планировании tooconfigure автоматическое резервное копирование с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-130">[Install hello latest Azure PowerShell commands](/powershell/azure/overview) if you plan tooconfigure Automated Backup with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="cf8e5-131">Автоматическая архивация зависит от расширения агента SQL Server IaaS hello.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-131">Automated Backup relies on hello SQL Server IaaS Agent Extension.</span></span> <span data-ttu-id="cf8e5-132">В текущей коллекции образов виртуальных машин SQL это расширение присутствует по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-132">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="cf8e5-133">Дополнительные сведения см. в статье [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md) (Расширение агента SQL Server IaaS).</span><span class="sxs-lookup"><span data-stu-id="cf8e5-133">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="cf8e5-134">данных</span><span class="sxs-lookup"><span data-stu-id="cf8e5-134">Settings</span></span>

<span data-ttu-id="cf8e5-135">Hello следующей таблице описаны параметры hello, которые могут быть настроены для автоматического резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-135">hello following table describes hello options that can be configured for Automated Backup.</span></span> <span data-ttu-id="cf8e5-136">Hello фактические шаги настройки отличаются в зависимости от того, используются ли hello портал Azure или команд Windows PowerShell для Azure.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-136">hello actual configuration steps vary depending on whether you use hello Azure portal or Azure Windows PowerShell commands.</span></span>

| <span data-ttu-id="cf8e5-137">Настройка</span><span class="sxs-lookup"><span data-stu-id="cf8e5-137">Setting</span></span> | <span data-ttu-id="cf8e5-138">Диапазон (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="cf8e5-138">Range (Default)</span></span> | <span data-ttu-id="cf8e5-139">Описание</span><span class="sxs-lookup"><span data-stu-id="cf8e5-139">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cf8e5-140">**Автоматическая архивация**</span><span class="sxs-lookup"><span data-stu-id="cf8e5-140">**Automated Backup**</span></span> | <span data-ttu-id="cf8e5-141">Включено/отключено (отключено)</span><span class="sxs-lookup"><span data-stu-id="cf8e5-141">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="cf8e5-142">Включает или отключает автоматическую архивацию для виртуальной машины Azure под управлением SQL Server 2014 Standard или Enterprise.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-142">Enables or disables Automated Backup for an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> |
| <span data-ttu-id="cf8e5-143">**Срок хранения**</span><span class="sxs-lookup"><span data-stu-id="cf8e5-143">**Retention Period**</span></span> | <span data-ttu-id="cf8e5-144">1–30 дней (30 дней)</span><span class="sxs-lookup"><span data-stu-id="cf8e5-144">1-30 days (30 days)</span></span> | <span data-ttu-id="cf8e5-145">Hello количество дней tooretain резервной копии.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-145">hello number of days tooretain a backup.</span></span> |
| <span data-ttu-id="cf8e5-146">**Учетная запись хранения**</span><span class="sxs-lookup"><span data-stu-id="cf8e5-146">**Storage Account**</span></span> | <span data-ttu-id="cf8e5-147">Учетная запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-147">Azure storage account</span></span> | <span data-ttu-id="cf8e5-148">Toouse учетной записи хранилища Azure для хранения файлов автоматического резервного копирования в хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-148">An Azure storage account toouse for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="cf8e5-149">Контейнер создается в этом toostore расположение всех файлов резервных копий.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-149">A container is created at this location toostore all backup files.</span></span> <span data-ttu-id="cf8e5-150">файл резервной копии Hello соглашение об именах включает hello Дата, время и имя компьютера.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-150">hello backup file naming convention includes hello date, time, and machine name.</span></span> |
| <span data-ttu-id="cf8e5-151">**Шифрование**</span><span class="sxs-lookup"><span data-stu-id="cf8e5-151">**Encryption**</span></span> | <span data-ttu-id="cf8e5-152">Включено/отключено (отключено)</span><span class="sxs-lookup"><span data-stu-id="cf8e5-152">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="cf8e5-153">Включает или отключает шифрование.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-153">Enables or disables encryption.</span></span> <span data-ttu-id="cf8e5-154">При включено шифрование, сертификаты, используемые toorestore hello hello-резервной копии находятся в hello указан учетную запись хранилища в hello же `automaticbackup` контейнер с помощью hello же соглашение об именовании.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-154">When encryption is enabled, hello certificates used toorestore hello backup are located in hello specified storage account in hello same `automaticbackup` container using hello same naming convention.</span></span> <span data-ttu-id="cf8e5-155">При изменении пароля hello, новый сертификат создается с этим паролем, но Здравствуй, старый сертификат остается toorestore предыдущих резервных копий.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-155">If hello password changes, a new certificate is generated with that password, but hello old certificate remains toorestore prior backups.</span></span> |
| <span data-ttu-id="cf8e5-156">**Пароль**</span><span class="sxs-lookup"><span data-stu-id="cf8e5-156">**Password**</span></span> | <span data-ttu-id="cf8e5-157">Текст пароля</span><span class="sxs-lookup"><span data-stu-id="cf8e5-157">Password text</span></span> | <span data-ttu-id="cf8e5-158">Пароль для ключей шифрования.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-158">A password for encryption keys.</span></span> <span data-ttu-id="cf8e5-159">Требуется, только если шифрование включено.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-159">This is only required if encryption is enabled.</span></span> <span data-ttu-id="cf8e5-160">В порядке toorestore зашифрованной резервной копии, необходимо иметь правильный пароль hello и связанные сертификата, который был использован в hello время, когда была создана резервная копия hello.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-160">In order toorestore an encrypted backup, you must have hello correct password and related certificate that was used at hello time hello backup was taken.</span></span> |

## <a name="configuration-in-hello-portal"></a><span data-ttu-id="cf8e5-161">Конфигурация в hello портала</span><span class="sxs-lookup"><span data-stu-id="cf8e5-161">Configuration in hello Portal</span></span>

<span data-ttu-id="cf8e5-162">Во время инициализации или для существующих виртуальных машинах SQL Server 2014 можно использовать hello Azure портала tooconfigure автоматическое резервное копирование.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-162">You can use hello Azure portal tooconfigure Automated Backup during provisioning or for existing SQL Server 2014 VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="cf8e5-163">Новые виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="cf8e5-163">New VMs</span></span>

<span data-ttu-id="cf8e5-164">При создании новой виртуальной машины 2014 SQL Server в модели развертывания диспетчера ресурсов hello, используйте hello Azure портала tooconfigure автоматическое резервное копирование.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-164">Use hello Azure portal tooconfigure Automated Backup when you create a new SQL Server 2014 Virtual Machine in hello Resource Manager deployment model.</span></span>

<span data-ttu-id="cf8e5-165">В hello **параметры SQL Server** колонке выберите **автоматическое резервное копирование**.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-165">In hello **SQL Server settings** blade, select **Automated backup**.</span></span> <span data-ttu-id="cf8e5-166">Hello следующие Azure портала снимке экрана показано hello **автоматическое резервное копирование SQL** колонку.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-166">hello following Azure portal screenshot shows hello **SQL Automated Backup** blade.</span></span>

![Настройка автоматической архивации SQL на портале Azure](./media/virtual-machines-windows-sql-automated-backup/azure-sql-arm-autobackup.png)

<span data-ttu-id="cf8e5-168">Контекст, в разделе hello полный на [подготовку виртуальной машины SQL Server в Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="cf8e5-168">For context, see hello complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="cf8e5-169">Существующие виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="cf8e5-169">Existing VMs</span></span>

<span data-ttu-id="cf8e5-170">Выберите существующую виртуальную машину SQL Server.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-170">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="cf8e5-171">Затем выберите hello **конфигурации SQL Server** раздел hello **параметры** колонку.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-171">Then select hello **SQL Server configuration** section of hello **Settings** blade.</span></span>

![Автоматизированная архивация SQL для существующих виртуальных машин](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-existing-vms.png)

<span data-ttu-id="cf8e5-173">В hello **конфигурации SQL Server** колонка, щелкните hello **изменить** кнопку в hello автоматического резервного копирования раздела.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-173">In hello **SQL Server configuration** blade, click hello **Edit** button in hello Automated backup section.</span></span>

![Настройка автоматизированной архивации SQL для существующих виртуальных машин](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-configuration.png)

<span data-ttu-id="cf8e5-175">По завершении нажмите кнопку hello **ОК** кнопку внизу hello hello **конфигурации SQL Server** toosave колонке изменения.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-175">When finished, click hello **OK** button on hello bottom of hello **SQL Server configuration** blade toosave your changes.</span></span>

<span data-ttu-id="cf8e5-176">При включении автоматического резервного копирования для hello первый раз Azure настраивает hello агента SQL Server IaaS в фоновом режиме hello.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-176">If you are enabling Automated Backup for hello first time, Azure configures hello SQL Server IaaS Agent in hello background.</span></span> <span data-ttu-id="cf8e5-177">В течение этого времени hello Azure портала может показывать, что автоматическая архивация настроена.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-177">During this time, hello Azure portal might not show that Automated Backup is configured.</span></span> <span data-ttu-id="cf8e5-178">Подождите несколько минут для hello агента toobe установлены, настроены.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-178">Wait several minutes for hello agent toobe installed, configured.</span></span> <span data-ttu-id="cf8e5-179">После этого hello Azure портале будут отображаться новые параметры hello.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-179">After that hello Azure portal will reflect hello new settings.</span></span>

> [!NOTE]
> <span data-ttu-id="cf8e5-180">Можно также настроить автоматизированную архивацию с помощью шаблона.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-180">You can also configure Automated Backup using a template.</span></span> <span data-ttu-id="cf8e5-181">Чтобы получить дополнительные сведения, ознакомьтесь с [шаблоном быстрого запуска Azure для автоматизированной архивации](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update).</span><span class="sxs-lookup"><span data-stu-id="cf8e5-181">For more information, see [Azure quickstart template for Automated Backup](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update).</span></span>

## <a name="configuration-with-powershell"></a><span data-ttu-id="cf8e5-182">Настройка с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="cf8e5-182">Configuration with PowerShell</span></span>

<span data-ttu-id="cf8e5-183">Можно использовать PowerShell tooconfigure автоматическое резервное копирование.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-183">You can use PowerShell tooconfigure Automated Backup.</span></span> <span data-ttu-id="cf8e5-184">Предварительно необходимо выполнить следующее.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-184">Before you begin, you must:</span></span>

- <span data-ttu-id="cf8e5-185">[Загрузите и установите последнюю версию Azure PowerShell hello](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="cf8e5-185">[Download and install hello latest Azure PowerShell](http://aka.ms/webpi-azps).</span></span>
- <span data-ttu-id="cf8e5-186">Откройте компонент Windows PowerShell и свяжите его со своей учетной записью.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-186">Open Windows PowerShell and associate it with your account.</span></span> <span data-ttu-id="cf8e5-187">Это можно сделать с помощью инструкции hello в hello [настроить подписку](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) раздел hello подготовки раздела.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-187">You can do this by following hello steps in hello [Configure your subscription](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) section of hello provisioning topic.</span></span>

### <a name="install-hello-sql-iaas-extension"></a><span data-ttu-id="cf8e5-188">Установка расширения SQL IaaS hello</span><span class="sxs-lookup"><span data-stu-id="cf8e5-188">Install hello SQL IaaS Extension</span></span>
<span data-ttu-id="cf8e5-189">При подготовке виртуальной машины SQL Server из портала Azure hello hello расширения IaaS SQL Server должны быть уже настроены.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-189">If you provisioned a SQL Server virtual machine from hello Azure portal, hello SQL Server IaaS Extension should already be installed.</span></span> <span data-ttu-id="cf8e5-190">Можно определить, если оно устанавливается для виртуальной Машины путем вызова **Get AzureRmVM** и проверив hello **расширения** свойство.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-190">You can determine if it is installed for your VM by calling **Get-AzureRmVM** command and examining hello **Extensions** property.</span></span>

```powershell
$vmname = "vmname"
$resourcegroupname = "resourcegroupname"

(Get-AzureRmVM -Name $vmname -ResourceGroupName $resourcegroupname).Extensions
```

<span data-ttu-id="cf8e5-191">Если установлен hello расширения агента IaaS SQL Server, вы увидите, что оно указано как «SqlIaaSAgent» или «SQLIaaSExtension».</span><span class="sxs-lookup"><span data-stu-id="cf8e5-191">If hello SQL Server IaaS Agent extension is installed, you should see it listed as “SqlIaaSAgent” or “SQLIaaSExtension”.</span></span> <span data-ttu-id="cf8e5-192">**ProvisioningState** для расширения hello также должен быть «Succeeded».</span><span class="sxs-lookup"><span data-stu-id="cf8e5-192">**ProvisioningState** for hello extension should also show “Succeeded”.</span></span>

<span data-ttu-id="cf8e5-193">Если он не установлен или не удалось подготовить toobe, его можно установить с hello следующую команду.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-193">If it is not installed or failed toobe provisioned, you can install it with hello following command.</span></span> <span data-ttu-id="cf8e5-194">В дополнение toohello ВМ имя и группе ресурсов, необходимо также указать область hello (**$region**), расположенных в ВМ.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-194">In addition toohello VM name and resource group, you must also specify hello region (**$region**) that your VM is located in.</span></span>

```powershell
$region = “EASTUS2”
Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region
```

### <span data-ttu-id="cf8e5-195"><a id="verifysettings"></a> Проверка текущих параметров</span><span class="sxs-lookup"><span data-stu-id="cf8e5-195"><a id="verifysettings"></a> Verify current settings</span></span>

<span data-ttu-id="cf8e5-196">Если вы включили автоматическое резервное копирование во время подготовки, можно использовать PowerShell toocheck текущей конфигурации.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-196">If you enabled automated backup during provisioning, you can use PowerShell toocheck your current configuration.</span></span> <span data-ttu-id="cf8e5-197">Запустите hello **Get AzureRmVMSqlServerExtension** команды и изучить hello **AutoBackupSettings** свойства:</span><span class="sxs-lookup"><span data-stu-id="cf8e5-197">Run hello **Get-AzureRmVMSqlServerExtension** command and examine hello **AutoBackupSettings** property:</span></span>

```powershell
(Get-AzureRmVMSqlServerExtension -VMName $vmname -ResourceGroupName $resourcegroupname).AutoBackupSettings
```

<span data-ttu-id="cf8e5-198">Вы должны получить аналогичные toohello следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="cf8e5-198">You should get output similar toohello following:</span></span>

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

<span data-ttu-id="cf8e5-199">Если выходных данных показано, что **включить** задано слишком**False**, то у вас есть tooenable автоматическое резервное копирование.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-199">If your output shows that **Enable** is set too**False**, then you have tooenable automated backup.</span></span> <span data-ttu-id="cf8e5-200">Hello хорошие новости — Включение и настройка автоматического резервного копирования в hello таким же образом.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-200">hello good news is that you enable and configure Automated Backup in hello same way.</span></span> <span data-ttu-id="cf8e5-201">Hello следующем разделе для получения этих сведений.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-201">See hello next section for this information.</span></span>

> [!NOTE] 
> <span data-ttu-id="cf8e5-202">Проверьте параметры hello сразу же после внесения изменений, возможно, вы получите обратно hello старые значения конфигурации.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-202">If you check hello settings immediately after making a change, it is possible that you will get back hello old configuration values.</span></span> <span data-ttu-id="cf8e5-203">Подождите несколько минут и проверить параметры hello снова toomake том, что изменения были применены.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-203">Wait a few minutes and check hello settings again toomake sure that your changes were applied.</span></span>

### <a name="configure-automated-backup"></a><span data-ttu-id="cf8e5-204">Настройка автоматической архивации</span><span class="sxs-lookup"><span data-stu-id="cf8e5-204">Configure Automated Backup</span></span>
<span data-ttu-id="cf8e5-205">PowerShell tooenable автоматическое резервное копирование, а также toomodify можно использовать его параметров и поведения в любое время.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-205">You can use PowerShell tooenable Automated Backup as well as toomodify its configuration and behavior at any time.</span></span>

<span data-ttu-id="cf8e5-206">Во-первых выберите или создайте учетную запись хранения hello файлов резервных копий.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-206">First, select or create a storage account for hello backup files.</span></span> <span data-ttu-id="cf8e5-207">Hello следующий скрипт выбирает учетную запись хранения или создает ее, если она не существует.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-207">hello following script selects a storage account or creates it if it does not exist.</span></span>

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
> <span data-ttu-id="cf8e5-208">Служба автоматической архивации не поддерживает хранение резервных копий в хранилище уровня "Премиум", но может создавать резервные копии дисков виртуальных машин, которые используют хранилище уровня "Премиум".</span><span class="sxs-lookup"><span data-stu-id="cf8e5-208">Automated Backup does not support storing backups in premium storage, but it can take backups from VM disks which use Premium Storage.</span></span>

<span data-ttu-id="cf8e5-209">Затем с помощью hello **New AzureRmVMSqlServerAutoBackupConfig** команды tooenable и настроить автоматическое резервное копирование параметров hello toostore-резервные копии в hello учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-209">Then use hello **New-AzureRmVMSqlServerAutoBackupConfig** command tooenable and configure hello Automated Backup settings toostore backups in hello Azure storage account.</span></span> <span data-ttu-id="cf8e5-210">В этом примере hello копии создаются toobe сохраняются в течение 10 дней.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-210">In this example, hello backups are set toobe retained for 10 days.</span></span> <span data-ttu-id="cf8e5-211">Здравствуйте, вторая команда **AzureRmVMSqlServerExtension набор**, hello обновления указано ВМ Azure с помощью этих параметров.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-211">hello second command, **Set-AzureRmVMSqlServerExtension**, updates hello specified Azure VM with these settings.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

<span data-ttu-id="cf8e5-212">Он может занять несколько минут tooinstall и настроить агент SQL Server IaaS hello.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-212">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span>

> [!NOTE]
> <span data-ttu-id="cf8e5-213">Существуют другие параметры для **New AzureRmVMSqlServerAutoBackupConfig** , применяемые только tooSQL Server 2016 и v2 автоматического резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-213">There are other settings for **New-AzureRmVMSqlServerAutoBackupConfig** that apply only tooSQL Server 2016 and Automated Backup v2.</span></span> <span data-ttu-id="cf8e5-214">SQL Server 2014 не поддерживает следующие параметры hello: **BackupSystemDbs**, **BackupScheduleType**, **FullBackupFrequency**,  **FullBackupStartHour**, **FullBackupWindowInHours**, и **LogBackupFrequencyInMinutes**.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-214">SQL Server 2014 does not support hello following settings: **BackupSystemDbs**, **BackupScheduleType**, **FullBackupFrequency**, **FullBackupStartHour**, **FullBackupWindowInHours**, and **LogBackupFrequencyInMinutes**.</span></span> <span data-ttu-id="cf8e5-215">При попытке tooconfigure эти параметры на виртуальной машине SQL Server 2014, не содержит ошибок, но параметры hello не применяется.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-215">If you attempt tooconfigure these settings on a SQL Server 2014 virtual machine, there is no error, but hello settings do not get applied.</span></span> <span data-ttu-id="cf8e5-216">Если требуется toouse эти параметры на виртуальной машине SQL Server 2016, см. раздел [v2 автоматического резервного копирования для SQL Server 2016 виртуальных машин Azure](virtual-machines-windows-sql-automated-backup-v2.md).</span><span class="sxs-lookup"><span data-stu-id="cf8e5-216">If you want toouse these settings on a SQL Server 2016 virtual machine, see [Automated Backup v2 for SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).</span></span>

<span data-ttu-id="cf8e5-217">шифрование tooenable изменить hello предыдущего сценария toopass hello **EnableEncryption** параметра вместе с паролем (защищенной строки) для hello **CertificatePassword** параметра.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-217">tooenable encryption, modify hello previous script toopass hello **EnableEncryption** parameter along with a password (secure string) for hello **CertificatePassword** parameter.</span></span> <span data-ttu-id="cf8e5-218">Hello следующий сценарий включает параметры автоматической архивации hello в предыдущем примере hello и добавляет шифрование.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-218">hello following script enables hello Automated Backup settings in hello previous example and adds encryption.</span></span>

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

<span data-ttu-id="cf8e5-219">параметры применяются, tooconfirm [Проверка конфигурации автоматического резервного копирования hello](#verifysettings).</span><span class="sxs-lookup"><span data-stu-id="cf8e5-219">tooconfirm your settings are applied, [verify hello Automated Backup configuration](#verifysettings).</span></span>

### <a name="disable-automated-backup"></a><span data-ttu-id="cf8e5-220">Отключение автоматической архивации</span><span class="sxs-lookup"><span data-stu-id="cf8e5-220">Disable Automated Backup</span></span>

<span data-ttu-id="cf8e5-221">Автоматическое резервное копирование, выполнения hello же сценарий, не hello toodisable **-включить** toohello параметр **New AzureRmVMSqlServerAutoBackupConfig** команды.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-221">toodisable Automated Backup, run hello same script without hello **-Enable** parameter toohello **New-AzureRmVMSqlServerAutoBackupConfig** command.</span></span> <span data-ttu-id="cf8e5-222">Здравствуйте, отсутствие hello **-включить** функции hello toodisable команда hello параметров сигналы.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-222">hello absence of hello **-Enable** parameter signals hello command toodisable hello feature.</span></span> <span data-ttu-id="cf8e5-223">Как и установка, может занять несколько минут toodisable автоматическое резервное копирование.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-223">As with installation, it can take several minutes toodisable Automated Backup.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

### <a name="example-script"></a><span data-ttu-id="cf8e5-224">Пример сценария</span><span class="sxs-lookup"><span data-stu-id="cf8e5-224">Example script</span></span>

<span data-ttu-id="cf8e5-225">Hello следующий скрипт предоставляет набор переменных, можно настроить tooenable и настройки автоматического резервного копирования для виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-225">hello following script provides a set of variables that you can customize tooenable and configure Automated Backup for your VM.</span></span> <span data-ttu-id="cf8e5-226">В вашем случае может потребоваться toocustomize hello скрипт на основе требований.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-226">In your case, you might need toocustomize hello script based on your requirements.</span></span> <span data-ttu-id="cf8e5-227">Например можно иметь toomake изменения, если требуется, чтобы toodisable hello резервное копирование системных баз данных или включить шифрование.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-227">For example, you would have toomake changes if you wanted toodisable hello backup of system databases or enable encryption.</span></span>

```powershell
$vmname = "yourvmname"
$resourcegroupname = "vmresourcegroupname"
$region = “Azure region name such as EASTUS2”
$storage_accountname = “storageaccountname”
$storage_resourcegroupname = $resourcegroupname
$retentionperiod = 10

# ResourceGroupName is hello resource group which is hosting hello VM where you are deploying hello SQL IaaS Extension

Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region

# Creates/use a storage account toostore hello backups

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }

# Configure Automated Backup settings

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays $retentionperiod -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

# Apply hello Automated Backup settings toohello VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="cf8e5-228">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cf8e5-228">Next steps</span></span>

<span data-ttu-id="cf8e5-229">Автоматическая архивация настраивает управляемое резервное копирование на виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-229">Automated Backup configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="cf8e5-230">Поэтому важно слишком[документации hello управляемого резервного копирования](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello влияние и поведение.</span><span class="sxs-lookup"><span data-stu-id="cf8e5-230">So it is important too[review hello documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello behavior and implications.</span></span>

<span data-ttu-id="cf8e5-231">Можно найти созданием резервных копий и восстановление руководство по SQL Server на виртуальных машинах Azure в разделе hello: [резервное копирование и восстановление для SQL Server в виртуальных машинах Azure](virtual-machines-windows-sql-backup-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="cf8e5-231">You can find additional backup and restore guidance for SQL Server on Azure VMs in hello following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span></span>

<span data-ttu-id="cf8e5-232">Сведения о других доступных задачах автоматизации см. в разделе [Расширение агента IaaS для SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="cf8e5-232">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="cf8e5-233">Дополнительные сведения о запуске SQL Server на виртуальных машинах Azure см. в [обзоре использования SQL Server на виртуальных машинах Azure](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cf8e5-233">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

