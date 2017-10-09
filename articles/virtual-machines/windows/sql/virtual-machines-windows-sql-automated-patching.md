---
title: "aaaAutomated исправления для виртуальных машин SQL Server (диспетчер ресурсов) | Документы Microsoft"
description: "Описывается функция автоматического исправления hello для SQL Server виртуальных машин, работающих в Azure с помощью диспетчера ресурсов."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 58232e92-318f-456b-8f0a-2201a541e08d
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 8bb8d0fb265e69d7bbf1fa047f5ceef02e7c56fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-resource-manager"></a><span data-ttu-id="08e1a-103">Автоматическая установка исправлений SQL Server на виртуальных машинах Azure (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="08e1a-103">Automated Patching for SQL Server in Azure Virtual Machines (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="08e1a-104">Диспетчер ресурсов</span><span class="sxs-lookup"><span data-stu-id="08e1a-104">Resource Manager</span></span>](virtual-machines-windows-sql-automated-patching.md)
> * [<span data-ttu-id="08e1a-105">Классический</span><span class="sxs-lookup"><span data-stu-id="08e1a-105">Classic</span></span>](../classic/sql-automated-patching.md)
> 
> 

<span data-ttu-id="08e1a-106">При автоматической установке исправлений на виртуальных машинах Azure с SQL Server задается период обслуживания.</span><span class="sxs-lookup"><span data-stu-id="08e1a-106">Automated Patching establishes a maintenance window for an Azure Virtual Machine running SQL Server.</span></span> <span data-ttu-id="08e1a-107">Установка автоматических обновлений возможна только в этот период обслуживания.</span><span class="sxs-lookup"><span data-stu-id="08e1a-107">Automated Updates can only be installed during this maintenance window.</span></span> <span data-ttu-id="08e1a-108">Для SQL Server это rescriction гарантирует, что системные обновления и перезапуски, связанный в hello наиболее сроки для hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="08e1a-108">For SQL Server, this rescriction ensures that system updates and any associated restarts occur at hello best possible time for hello database.</span></span> <span data-ttu-id="08e1a-109">Автоматические исправления выполняются зависит от hello [расширения агента SQL Server IaaS](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="08e1a-109">Automated Patching depends on hello [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="08e1a-110">tooview hello классической версии данной статьи, в разделе [автоматическое применение исправлений для SQL Server в виртуальных машин Azure Classic](../classic/sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="08e1a-110">tooview hello classic version of this article, see [Automated Patching for SQL Server in Azure Virtual Machines Classic](../classic/sql-automated-patching.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="08e1a-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="08e1a-111">Prerequisites</span></span>
<span data-ttu-id="08e1a-112">toouse автоматическое применение исправлений, рассмотрите возможность hello следующие предварительные требования:</span><span class="sxs-lookup"><span data-stu-id="08e1a-112">toouse Automated Patching, consider hello following prerequisites:</span></span>

<span data-ttu-id="08e1a-113">**Операционная система**</span><span class="sxs-lookup"><span data-stu-id="08e1a-113">**Operating System**:</span></span>

* <span data-ttu-id="08e1a-114">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="08e1a-114">Windows Server 2012</span></span>
* <span data-ttu-id="08e1a-115">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="08e1a-115">Windows Server 2012 R2</span></span>
* <span data-ttu-id="08e1a-116">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="08e1a-116">Windows Server 2016</span></span>

<span data-ttu-id="08e1a-117">**Версия SQL Server**</span><span class="sxs-lookup"><span data-stu-id="08e1a-117">**SQL Server version**:</span></span>

* <span data-ttu-id="08e1a-118">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="08e1a-118">SQL Server 2012</span></span>
* <span data-ttu-id="08e1a-119">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="08e1a-119">SQL Server 2014</span></span>
* <span data-ttu-id="08e1a-120">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="08e1a-120">SQL Server 2016</span></span>

<span data-ttu-id="08e1a-121">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="08e1a-121">**Azure PowerShell**:</span></span>

* <span data-ttu-id="08e1a-122">[Установка последних команд Azure PowerShell hello](/powershell/azure/overview) при планировании tooconfigure автоматических исправлений с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="08e1a-122">[Install hello latest Azure PowerShell commands](/powershell/azure/overview) if you plan tooconfigure Automated Patching with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="08e1a-123">Автоматические исправления выполняются полагается на hello расширения агента IaaS SQL Server.</span><span class="sxs-lookup"><span data-stu-id="08e1a-123">Automated Patching relies on hello SQL Server IaaS Agent Extension.</span></span> <span data-ttu-id="08e1a-124">В текущей коллекции образов виртуальных машин SQL это расширение присутствует по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="08e1a-124">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="08e1a-125">Дополнительные сведения см. в статье [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md) (Расширение агента SQL Server IaaS).</span><span class="sxs-lookup"><span data-stu-id="08e1a-125">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>
> 
> 

## <a name="settings"></a><span data-ttu-id="08e1a-126">данных</span><span class="sxs-lookup"><span data-stu-id="08e1a-126">Settings</span></span>
<span data-ttu-id="08e1a-127">Hello следующей таблице описаны параметры hello, которые могут быть настроены для автоматического исправления.</span><span class="sxs-lookup"><span data-stu-id="08e1a-127">hello following table describes hello options that can be configured for Automated Patching.</span></span> <span data-ttu-id="08e1a-128">Hello фактические шаги настройки отличаются в зависимости от того, используются ли hello портал Azure или команд Windows PowerShell для Azure.</span><span class="sxs-lookup"><span data-stu-id="08e1a-128">hello actual configuration steps vary depending on whether you use hello Azure portal or Azure Windows PowerShell commands.</span></span>

| <span data-ttu-id="08e1a-129">Настройка</span><span class="sxs-lookup"><span data-stu-id="08e1a-129">Setting</span></span> | <span data-ttu-id="08e1a-130">Возможные значения</span><span class="sxs-lookup"><span data-stu-id="08e1a-130">Possible values</span></span> | <span data-ttu-id="08e1a-131">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="08e1a-131">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="08e1a-132">**Автоматическое исправление**</span><span class="sxs-lookup"><span data-stu-id="08e1a-132">**Automated Patching**</span></span> |<span data-ttu-id="08e1a-133">Включено/отключено (отключено)</span><span class="sxs-lookup"><span data-stu-id="08e1a-133">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="08e1a-134">Включает или отключает автоматическую установку исправлений для виртуальной машины Azure.</span><span class="sxs-lookup"><span data-stu-id="08e1a-134">Enables or disables Automated Patching for an Azure virtual machine.</span></span> |
| <span data-ttu-id="08e1a-135">**Расписание обслуживания**</span><span class="sxs-lookup"><span data-stu-id="08e1a-135">**Maintenance schedule**</span></span> |<span data-ttu-id="08e1a-136">Каждый день, понедельник, вторник, среда, четверг, пятница, суббота, воскресенье</span><span class="sxs-lookup"><span data-stu-id="08e1a-136">Everyday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday</span></span> |<span data-ttu-id="08e1a-137">расписание Hello загрузку и установку обновлений Windows, SQL Server и Microsoft для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="08e1a-137">hello schedule for downloading and installing Windows, SQL Server, and Microsoft updates for your virtual machine.</span></span> |
| <span data-ttu-id="08e1a-138">**Время начала обслуживания**</span><span class="sxs-lookup"><span data-stu-id="08e1a-138">**Maintenance start hour**</span></span> |<span data-ttu-id="08e1a-139">0–24</span><span class="sxs-lookup"><span data-stu-id="08e1a-139">0-24</span></span> |<span data-ttu-id="08e1a-140">Hello локальном запуске время tooupdate hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="08e1a-140">hello local start time tooupdate hello virtual machine.</span></span> |
| <span data-ttu-id="08e1a-141">**Длительность периода обслуживания**</span><span class="sxs-lookup"><span data-stu-id="08e1a-141">**Maintenance window duration**</span></span> |<span data-ttu-id="08e1a-142">30–180</span><span class="sxs-lookup"><span data-stu-id="08e1a-142">30-180</span></span> |<span data-ttu-id="08e1a-143">Hello количество минут, разрешенных toocomplete hello загрузки и установки обновлений.</span><span class="sxs-lookup"><span data-stu-id="08e1a-143">hello number of minutes permitted toocomplete hello download and installation of updates.</span></span> |
| <span data-ttu-id="08e1a-144">**Категория исправления**</span><span class="sxs-lookup"><span data-stu-id="08e1a-144">**Patch Category**</span></span> |<span data-ttu-id="08e1a-145">Важно!</span><span class="sxs-lookup"><span data-stu-id="08e1a-145">Important</span></span> |<span data-ttu-id="08e1a-146">Категория Hello toodownload обновлений и установить.</span><span class="sxs-lookup"><span data-stu-id="08e1a-146">hello category of updates toodownload and install.</span></span> |

## <a name="configuration-in-hello-portal"></a><span data-ttu-id="08e1a-147">Конфигурация в hello портала</span><span class="sxs-lookup"><span data-stu-id="08e1a-147">Configuration in hello Portal</span></span>
<span data-ttu-id="08e1a-148">Можно использовать hello Azure портала tooconfigure автоматических исправлений во время инициализации или для существующих виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="08e1a-148">You can use hello Azure portal tooconfigure Automated Patching during provisioning or for existing VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="08e1a-149">Новые виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="08e1a-149">New VMs</span></span>
<span data-ttu-id="08e1a-150">Используйте hello Azure портала tooconfigure автоматических исправлений при создании новой виртуальной машины SQL Server в модели развертывания диспетчера ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="08e1a-150">Use hello Azure portal tooconfigure Automated Patching when you create a new SQL Server Virtual Machine in hello Resource Manager deployment model.</span></span>

<span data-ttu-id="08e1a-151">В hello **параметры SQL Server** колонке выберите **автоматическую установку исправлений**.</span><span class="sxs-lookup"><span data-stu-id="08e1a-151">In hello **SQL Server settings** blade, select **Automated patching**.</span></span> <span data-ttu-id="08e1a-152">Hello следующие Azure портала снимке экрана показано hello **автоматических исправлений SQL** колонку.</span><span class="sxs-lookup"><span data-stu-id="08e1a-152">hello following Azure portal screenshot shows hello **SQL Automated Patching** blade.</span></span>

![Автоматизированная установка исправлений SQL на портале Azure](./media/virtual-machines-windows-sql-automated-patching/azure-sql-arm-patching.png)

<span data-ttu-id="08e1a-154">Контекст, в разделе hello полный на [подготовку виртуальной машины SQL Server в Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="08e1a-154">For context, see hello complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="08e1a-155">Существующие виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="08e1a-155">Existing VMs</span></span>
<span data-ttu-id="08e1a-156">Выберите существующую виртуальную машину SQL Server.</span><span class="sxs-lookup"><span data-stu-id="08e1a-156">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="08e1a-157">Затем выберите hello **конфигурации SQL Server** раздел hello **параметры** колонку.</span><span class="sxs-lookup"><span data-stu-id="08e1a-157">Then select hello **SQL Server configuration** section of hello **Settings** blade.</span></span>

![Автоматизированная установка исправлений SQL для существующих виртуальных машин](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-existing-vms.png)

<span data-ttu-id="08e1a-159">В hello **конфигурации SQL Server** колонка, щелкните hello **изменить** кнопку в hello автоматического исправления раздела.</span><span class="sxs-lookup"><span data-stu-id="08e1a-159">In hello **SQL Server configuration** blade, click hello **Edit** button in hello Automated patching section.</span></span>

![Настройка автоматизированной установки исправлений SQL для существующих виртуальных машин](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-configuration.png)

<span data-ttu-id="08e1a-161">По завершении нажмите кнопку hello **ОК** кнопку внизу hello hello **конфигурации SQL Server** toosave колонке изменения.</span><span class="sxs-lookup"><span data-stu-id="08e1a-161">When finished, click hello **OK** button on hello bottom of hello **SQL Server configuration** blade toosave your changes.</span></span>

<span data-ttu-id="08e1a-162">При включении автоматического исправления для hello первый раз, Azure настраивает hello агента SQL Server IaaS в фоновом режиме hello.</span><span class="sxs-lookup"><span data-stu-id="08e1a-162">If you are enabling Automated Patching for hello first time, Azure configures hello SQL Server IaaS Agent in hello background.</span></span> <span data-ttu-id="08e1a-163">В течение этого времени hello портал Azure может показывать, что выполняется настройка автоматического исправления.</span><span class="sxs-lookup"><span data-stu-id="08e1a-163">During this time, hello Azure portal might not show that Automated Patching is configured.</span></span> <span data-ttu-id="08e1a-164">Подождите несколько минут для hello агента toobe установлены, настроены.</span><span class="sxs-lookup"><span data-stu-id="08e1a-164">Wait several minutes for hello agent toobe installed, configured.</span></span> <span data-ttu-id="08e1a-165">После этого hello Azure portal отражает hello новые параметры.</span><span class="sxs-lookup"><span data-stu-id="08e1a-165">After that hello Azure portal reflects hello new settings.</span></span>

> [!NOTE]
> <span data-ttu-id="08e1a-166">Можно также настроить автоматизированную установку исправлений с помощью шаблона.</span><span class="sxs-lookup"><span data-stu-id="08e1a-166">You can also configure Automated Patching using a template.</span></span> <span data-ttu-id="08e1a-167">Чтобы получить дополнительные сведения, ознакомьтесь с [шаблоном быстрого запуска Azure для автоматизированной установки исправлений](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autopatching-update).</span><span class="sxs-lookup"><span data-stu-id="08e1a-167">For more information, see [Azure quickstart template for Automated Patching](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autopatching-update).</span></span>
> 
> 

## <a name="configuration-with-powershell"></a><span data-ttu-id="08e1a-168">Настройка с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="08e1a-168">Configuration with PowerShell</span></span>
<span data-ttu-id="08e1a-169">После подготовки виртуальной Машины SQL, используйте PowerShell tooconfigure автоматических исправлений.</span><span class="sxs-lookup"><span data-stu-id="08e1a-169">After provisioning your SQL VM, use PowerShell tooconfigure Automated Patching.</span></span>

<span data-ttu-id="08e1a-170">В следующем примере hello, PowerShell — используется tooconfigure автоматического исправления на существующей виртуальной Машины SQL Server.</span><span class="sxs-lookup"><span data-stu-id="08e1a-170">In hello following example, PowerShell is used tooconfigure Automated Patching on an existing SQL Server VM.</span></span> <span data-ttu-id="08e1a-171">Hello **AzureRM.Compute\New AzureVMSqlServerAutoPatchingConfig** команда настраивает новый период обслуживания для автоматических обновлений.</span><span class="sxs-lookup"><span data-stu-id="08e1a-171">hello **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig** command configures a new maintenance window for automatic updates.</span></span>

    $vmname = "vmname"
    $resourcegroupname = "resourcegroupname"
    $aps = AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Set-AzureRmVMSqlServerExtension -AutoPatchingSettings $aps -VMName $vmname -ResourceGroupName $resourcegroupname

<span data-ttu-id="08e1a-172">На основании этого примера hello следующей таблице описаны результаты применения hello на hello целевой виртуальной Машине Azure.</span><span class="sxs-lookup"><span data-stu-id="08e1a-172">Based on this example, hello following table describes hello practical effect on hello target Azure VM:</span></span>

| <span data-ttu-id="08e1a-173">Параметр</span><span class="sxs-lookup"><span data-stu-id="08e1a-173">Parameter</span></span> | <span data-ttu-id="08e1a-174">Результат</span><span class="sxs-lookup"><span data-stu-id="08e1a-174">Effect</span></span> |
| --- | --- |
| <span data-ttu-id="08e1a-175">**DayOfWeek**</span><span class="sxs-lookup"><span data-stu-id="08e1a-175">**DayOfWeek**</span></span> |<span data-ttu-id="08e1a-176">Исправления устанавливаются каждый четверг.</span><span class="sxs-lookup"><span data-stu-id="08e1a-176">Patches installed every Thursday.</span></span> |
| <span data-ttu-id="08e1a-177">**MaintenanceWindowStartingHour**</span><span class="sxs-lookup"><span data-stu-id="08e1a-177">**MaintenanceWindowStartingHour**</span></span> |<span data-ttu-id="08e1a-178">Установка обновлений начинается в 11:00.</span><span class="sxs-lookup"><span data-stu-id="08e1a-178">Begin updates at 11:00am.</span></span> |
| <span data-ttu-id="08e1a-179">**MaintenanceWindowsDuration**</span><span class="sxs-lookup"><span data-stu-id="08e1a-179">**MaintenanceWindowsDuration**</span></span> |<span data-ttu-id="08e1a-180">Обновления должны быть установлены в течение 120 минут.</span><span class="sxs-lookup"><span data-stu-id="08e1a-180">Patches must be installed within 120 minutes.</span></span> <span data-ttu-id="08e1a-181">На основании времени начала hello, они должны выполнить с 1:00 pm.</span><span class="sxs-lookup"><span data-stu-id="08e1a-181">Based on hello start time, they must complete by 1:00pm.</span></span> |
| <span data-ttu-id="08e1a-182">**PatchCategory**</span><span class="sxs-lookup"><span data-stu-id="08e1a-182">**PatchCategory**</span></span> |<span data-ttu-id="08e1a-183">Здравствуйте, единственное возможное значение для этого параметра можно **важно**.</span><span class="sxs-lookup"><span data-stu-id="08e1a-183">hello only possible setting for this parameter is **Important**.</span></span> |

<span data-ttu-id="08e1a-184">Он может занять несколько минут tooinstall и настроить агент SQL Server IaaS hello.</span><span class="sxs-lookup"><span data-stu-id="08e1a-184">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span>

<span data-ttu-id="08e1a-185">toodisable автоматического исправления выполнения hello же сценарий, не hello **-включить** toohello параметр **AzureRM.Compute\New AzureVMSqlServerAutoPatchingConfig**.</span><span class="sxs-lookup"><span data-stu-id="08e1a-185">toodisable Automated Patching, run hello same script without hello **-Enable** parameter toohello **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig**.</span></span> <span data-ttu-id="08e1a-186">Здравствуйте, отсутствие hello **-включить** функции hello toodisable команда hello параметров сигналы.</span><span class="sxs-lookup"><span data-stu-id="08e1a-186">hello absence of hello **-Enable** parameter signals hello command toodisable hello feature.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08e1a-187">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="08e1a-187">Next steps</span></span>
<span data-ttu-id="08e1a-188">Сведения о других доступных задачах автоматизации см. в разделе [Расширение агента IaaS для SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="08e1a-188">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="08e1a-189">Дополнительные сведения о запуске SQL Server на виртуальных машинах Azure см. в [обзоре использования SQL Server на виртуальных машинах Azure](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="08e1a-189">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

