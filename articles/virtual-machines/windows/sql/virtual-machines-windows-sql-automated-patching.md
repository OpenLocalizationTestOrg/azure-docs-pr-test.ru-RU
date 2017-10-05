---
title: "Автоматизированная установка исправлений для виртуальных машин SQL Server (Resource Manager) | Документация Майкрософт"
description: "Описывает функцию автоматической установки исправлений для виртуальных машин SQL Server в Azure для модели Resource Manager."
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
ms.openlocfilehash: 7d501ab45a85010a8dbfd6135d77f18f1743354e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-resource-manager"></a><span data-ttu-id="3ad05-103">Автоматическая установка исправлений SQL Server на виртуальных машинах Azure (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="3ad05-103">Automated Patching for SQL Server in Azure Virtual Machines (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3ad05-104">Диспетчер ресурсов</span><span class="sxs-lookup"><span data-stu-id="3ad05-104">Resource Manager</span></span>](virtual-machines-windows-sql-automated-patching.md)
> * [<span data-ttu-id="3ad05-105">Классический</span><span class="sxs-lookup"><span data-stu-id="3ad05-105">Classic</span></span>](../classic/sql-automated-patching.md)
> 
> 

<span data-ttu-id="3ad05-106">При автоматической установке исправлений на виртуальных машинах Azure с SQL Server задается период обслуживания.</span><span class="sxs-lookup"><span data-stu-id="3ad05-106">Automated Patching establishes a maintenance window for an Azure Virtual Machine running SQL Server.</span></span> <span data-ttu-id="3ad05-107">Установка автоматических обновлений возможна только в этот период обслуживания.</span><span class="sxs-lookup"><span data-stu-id="3ad05-107">Automated Updates can only be installed during this maintenance window.</span></span> <span data-ttu-id="3ad05-108">Для SQL Server это ограничение гарантирует, что системные обновления и связанные с ними перезапуски системы будут происходить в наиболее удобное для базы данных время.</span><span class="sxs-lookup"><span data-stu-id="3ad05-108">For SQL Server, this rescriction ensures that system updates and any associated restarts occur at the best possible time for the database.</span></span> <span data-ttu-id="3ad05-109">Автоматическая установка исправлений зависит от [Расширения агента IaaS для SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="3ad05-109">Automated Patching depends on the [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="3ad05-110">Версию этой статьи для классической модели развертывания см. здесь: [Автоматическая установка исправлений SQL Server на виртуальных машинах Azure (классическая модель)](../classic/sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="3ad05-110">To view the classic version of this article, see [Automated Patching for SQL Server in Azure Virtual Machines Classic](../classic/sql-automated-patching.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3ad05-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3ad05-111">Prerequisites</span></span>
<span data-ttu-id="3ad05-112">Для использования автоматической установки исправлений необходимо выполнить следующие предварительные требования.</span><span class="sxs-lookup"><span data-stu-id="3ad05-112">To use Automated Patching, consider the following prerequisites:</span></span>

<span data-ttu-id="3ad05-113">**Операционная система**</span><span class="sxs-lookup"><span data-stu-id="3ad05-113">**Operating System**:</span></span>

* <span data-ttu-id="3ad05-114">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="3ad05-114">Windows Server 2012</span></span>
* <span data-ttu-id="3ad05-115">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="3ad05-115">Windows Server 2012 R2</span></span>
* <span data-ttu-id="3ad05-116">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="3ad05-116">Windows Server 2016</span></span>

<span data-ttu-id="3ad05-117">**Версия SQL Server**</span><span class="sxs-lookup"><span data-stu-id="3ad05-117">**SQL Server version**:</span></span>

* <span data-ttu-id="3ad05-118">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="3ad05-118">SQL Server 2012</span></span>
* <span data-ttu-id="3ad05-119">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="3ad05-119">SQL Server 2014</span></span>
* <span data-ttu-id="3ad05-120">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="3ad05-120">SQL Server 2016</span></span>

<span data-ttu-id="3ad05-121">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="3ad05-121">**Azure PowerShell**:</span></span>

* <span data-ttu-id="3ad05-122">[Установите последние команды Azure PowerShell](/powershell/azure/overview) , если планируете настраивать автоматические исправления с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3ad05-122">[Install the latest Azure PowerShell commands](/powershell/azure/overview) if you plan to configure Automated Patching with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="3ad05-123">Автоматическая установка исправлений зависит от расширения агента IaaS для SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3ad05-123">Automated Patching relies on the SQL Server IaaS Agent Extension.</span></span> <span data-ttu-id="3ad05-124">В текущей коллекции образов виртуальных машин SQL это расширение присутствует по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="3ad05-124">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="3ad05-125">Дополнительные сведения см. в статье [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md) (Расширение агента SQL Server IaaS).</span><span class="sxs-lookup"><span data-stu-id="3ad05-125">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>
> 
> 

## <a name="settings"></a><span data-ttu-id="3ad05-126">Параметры</span><span class="sxs-lookup"><span data-stu-id="3ad05-126">Settings</span></span>
<span data-ttu-id="3ad05-127">В приведенной ниже таблице описаны параметры для настройки автоматической установки исправлений.</span><span class="sxs-lookup"><span data-stu-id="3ad05-127">The following table describes the options that can be configured for Automated Patching.</span></span> <span data-ttu-id="3ad05-128">Фактическая процедура настройки может варьироваться в зависимости от того, используете вы портал Azure или команды Azure Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3ad05-128">The actual configuration steps vary depending on whether you use the Azure portal or Azure Windows PowerShell commands.</span></span>

| <span data-ttu-id="3ad05-129">Настройка</span><span class="sxs-lookup"><span data-stu-id="3ad05-129">Setting</span></span> | <span data-ttu-id="3ad05-130">Возможные значения</span><span class="sxs-lookup"><span data-stu-id="3ad05-130">Possible values</span></span> | <span data-ttu-id="3ad05-131">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="3ad05-131">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3ad05-132">**Автоматическое исправление**</span><span class="sxs-lookup"><span data-stu-id="3ad05-132">**Automated Patching**</span></span> |<span data-ttu-id="3ad05-133">Включено/отключено (отключено)</span><span class="sxs-lookup"><span data-stu-id="3ad05-133">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="3ad05-134">Включает или отключает автоматическую установку исправлений для виртуальной машины Azure.</span><span class="sxs-lookup"><span data-stu-id="3ad05-134">Enables or disables Automated Patching for an Azure virtual machine.</span></span> |
| <span data-ttu-id="3ad05-135">**Расписание обслуживания**</span><span class="sxs-lookup"><span data-stu-id="3ad05-135">**Maintenance schedule**</span></span> |<span data-ttu-id="3ad05-136">Каждый день, понедельник, вторник, среда, четверг, пятница, суббота, воскресенье</span><span class="sxs-lookup"><span data-stu-id="3ad05-136">Everyday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday</span></span> |<span data-ttu-id="3ad05-137">Расписание для скачивания и установки обновлений Windows, SQL Server и обновлений Майкрософт для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="3ad05-137">The schedule for downloading and installing Windows, SQL Server, and Microsoft updates for your virtual machine.</span></span> |
| <span data-ttu-id="3ad05-138">**Время начала обслуживания**</span><span class="sxs-lookup"><span data-stu-id="3ad05-138">**Maintenance start hour**</span></span> |<span data-ttu-id="3ad05-139">0–24</span><span class="sxs-lookup"><span data-stu-id="3ad05-139">0-24</span></span> |<span data-ttu-id="3ad05-140">Локальное время начала обновления виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="3ad05-140">The local start time to update the virtual machine.</span></span> |
| <span data-ttu-id="3ad05-141">**Длительность периода обслуживания**</span><span class="sxs-lookup"><span data-stu-id="3ad05-141">**Maintenance window duration**</span></span> |<span data-ttu-id="3ad05-142">30–180</span><span class="sxs-lookup"><span data-stu-id="3ad05-142">30-180</span></span> |<span data-ttu-id="3ad05-143">Допустимое количество минут для скачивания и установки обновлений.</span><span class="sxs-lookup"><span data-stu-id="3ad05-143">The number of minutes permitted to complete the download and installation of updates.</span></span> |
| <span data-ttu-id="3ad05-144">**Категория исправления**</span><span class="sxs-lookup"><span data-stu-id="3ad05-144">**Patch Category**</span></span> |<span data-ttu-id="3ad05-145">Важно!</span><span class="sxs-lookup"><span data-stu-id="3ad05-145">Important</span></span> |<span data-ttu-id="3ad05-146">Категория обновлений, которые будут скачаны и установлены.</span><span class="sxs-lookup"><span data-stu-id="3ad05-146">The category of updates to download and install.</span></span> |

## <a name="configuration-in-the-portal"></a><span data-ttu-id="3ad05-147">Настройка на портале</span><span class="sxs-lookup"><span data-stu-id="3ad05-147">Configuration in the Portal</span></span>
<span data-ttu-id="3ad05-148">Для настройки автоматизированной установки исправлений во время подготовки виртуальных машин или для существующих виртуальных машин можно использовать портал Azure.</span><span class="sxs-lookup"><span data-stu-id="3ad05-148">You can use the Azure portal to configure Automated Patching during provisioning or for existing VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="3ad05-149">Новые виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="3ad05-149">New VMs</span></span>
<span data-ttu-id="3ad05-150">При создании новой виртуальной машины SQL Server с моделью развертывания с помощью Resource Manager настройте автоматизированную установку исправлений, используя портал Azure.</span><span class="sxs-lookup"><span data-stu-id="3ad05-150">Use the Azure portal to configure Automated Patching when you create a new SQL Server Virtual Machine in the Resource Manager deployment model.</span></span>

<span data-ttu-id="3ad05-151">В колонке **Параметры SQL Server** выберите **Автоматизированное исправление**.</span><span class="sxs-lookup"><span data-stu-id="3ad05-151">In the **SQL Server settings** blade, select **Automated patching**.</span></span> <span data-ttu-id="3ad05-152">Колонка **Автоматическая установка исправлений SQL** показана на следующем снимке экрана портала Azure.</span><span class="sxs-lookup"><span data-stu-id="3ad05-152">The following Azure portal screenshot shows the **SQL Automated Patching** blade.</span></span>

![Автоматизированная установка исправлений SQL на портале Azure](./media/virtual-machines-windows-sql-automated-patching/azure-sql-arm-patching.png)

<span data-ttu-id="3ad05-154">Сведения о контексте приведены в полном описании в статье [Подготовка виртуальной машины SQL Server на портале Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="3ad05-154">For context, see the complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="3ad05-155">Существующие виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="3ad05-155">Existing VMs</span></span>
<span data-ttu-id="3ad05-156">Выберите существующую виртуальную машину SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3ad05-156">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="3ad05-157">Затем в колонке **Параметры** выберите раздел **Конфигурация SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="3ad05-157">Then select the **SQL Server configuration** section of the **Settings** blade.</span></span>

![Автоматизированная установка исправлений SQL для существующих виртуальных машин](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-existing-vms.png)

<span data-ttu-id="3ad05-159">В колонке **Конфигурация SQL Server** нажмите кнопку **Изменить** в разделе "Автоматизированное исправление".</span><span class="sxs-lookup"><span data-stu-id="3ad05-159">In the **SQL Server configuration** blade, click the **Edit** button in the Automated patching section.</span></span>

![Настройка автоматизированной установки исправлений SQL для существующих виртуальных машин](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-configuration.png)

<span data-ttu-id="3ad05-161">По завершении нажмите кнопку **ОК** в нижней части колонки **Конфигурация SQL Server**, чтобы сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="3ad05-161">When finished, click the **OK** button on the bottom of the **SQL Server configuration** blade to save your changes.</span></span>

<span data-ttu-id="3ad05-162">Если автоматизированная установка исправлений включается впервые, Azure настроит агент IaaS SQL Server в фоновом режиме.</span><span class="sxs-lookup"><span data-stu-id="3ad05-162">If you are enabling Automated Patching for the first time, Azure configures the SQL Server IaaS Agent in the background.</span></span> <span data-ttu-id="3ad05-163">В течение этого времени портал Azure может не отображать информацию о том, что выполняется настройка автоматической установки исправлений.</span><span class="sxs-lookup"><span data-stu-id="3ad05-163">During this time, the Azure portal might not show that Automated Patching is configured.</span></span> <span data-ttu-id="3ad05-164">Установка и настройка агента занимают несколько минут.</span><span class="sxs-lookup"><span data-stu-id="3ad05-164">Wait several minutes for the agent to be installed, configured.</span></span> <span data-ttu-id="3ad05-165">После этого новые параметры отобразятся на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="3ad05-165">After that the Azure portal reflects the new settings.</span></span>

> [!NOTE]
> <span data-ttu-id="3ad05-166">Можно также настроить автоматизированную установку исправлений с помощью шаблона.</span><span class="sxs-lookup"><span data-stu-id="3ad05-166">You can also configure Automated Patching using a template.</span></span> <span data-ttu-id="3ad05-167">Чтобы получить дополнительные сведения, ознакомьтесь с [шаблоном быстрого запуска Azure для автоматизированной установки исправлений](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autopatching-update).</span><span class="sxs-lookup"><span data-stu-id="3ad05-167">For more information, see [Azure quickstart template for Automated Patching](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autopatching-update).</span></span>
> 
> 

## <a name="configuration-with-powershell"></a><span data-ttu-id="3ad05-168">Настройка с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="3ad05-168">Configuration with PowerShell</span></span>
<span data-ttu-id="3ad05-169">После подготовки виртуальной машины SQL используйте PowerShell для настройки автоматической установки исправлений.</span><span class="sxs-lookup"><span data-stu-id="3ad05-169">After provisioning your SQL VM, use PowerShell to configure Automated Patching.</span></span>

<span data-ttu-id="3ad05-170">В следующем примере для настройки автоматической установки исправлений на существующей виртуальной машине SQL Server используется PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3ad05-170">In the following example, PowerShell is used to configure Automated Patching on an existing SQL Server VM.</span></span> <span data-ttu-id="3ad05-171">Команда **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig** настраивает новый период обслуживания для автоматизированного обновления.</span><span class="sxs-lookup"><span data-stu-id="3ad05-171">The **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig** command configures a new maintenance window for automatic updates.</span></span>

    $vmname = "vmname"
    $resourcegroupname = "resourcegroupname"
    $aps = AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Set-AzureRmVMSqlServerExtension -AutoPatchingSettings $aps -VMName $vmname -ResourceGroupName $resourcegroupname

<span data-ttu-id="3ad05-172">В представленной ниже таблице показано фактическое воздействие на конечную виртуальную машину Azure на основе данного примера.</span><span class="sxs-lookup"><span data-stu-id="3ad05-172">Based on this example, the following table describes the practical effect on the target Azure VM:</span></span>

| <span data-ttu-id="3ad05-173">Параметр</span><span class="sxs-lookup"><span data-stu-id="3ad05-173">Parameter</span></span> | <span data-ttu-id="3ad05-174">Результат</span><span class="sxs-lookup"><span data-stu-id="3ad05-174">Effect</span></span> |
| --- | --- |
| <span data-ttu-id="3ad05-175">**DayOfWeek**</span><span class="sxs-lookup"><span data-stu-id="3ad05-175">**DayOfWeek**</span></span> |<span data-ttu-id="3ad05-176">Исправления устанавливаются каждый четверг.</span><span class="sxs-lookup"><span data-stu-id="3ad05-176">Patches installed every Thursday.</span></span> |
| <span data-ttu-id="3ad05-177">**MaintenanceWindowStartingHour**</span><span class="sxs-lookup"><span data-stu-id="3ad05-177">**MaintenanceWindowStartingHour**</span></span> |<span data-ttu-id="3ad05-178">Установка обновлений начинается в 11:00.</span><span class="sxs-lookup"><span data-stu-id="3ad05-178">Begin updates at 11:00am.</span></span> |
| <span data-ttu-id="3ad05-179">**MaintenanceWindowsDuration**</span><span class="sxs-lookup"><span data-stu-id="3ad05-179">**MaintenanceWindowsDuration**</span></span> |<span data-ttu-id="3ad05-180">Обновления должны быть установлены в течение 120 минут.</span><span class="sxs-lookup"><span data-stu-id="3ad05-180">Patches must be installed within 120 minutes.</span></span> <span data-ttu-id="3ad05-181">С учетом времени начала установка обновлений должна завершаться к 13:00.</span><span class="sxs-lookup"><span data-stu-id="3ad05-181">Based on the start time, they must complete by 1:00pm.</span></span> |
| <span data-ttu-id="3ad05-182">**PatchCategory**</span><span class="sxs-lookup"><span data-stu-id="3ad05-182">**PatchCategory**</span></span> |<span data-ttu-id="3ad05-183">Единственное возможное значение для этого параметра — **Important**.</span><span class="sxs-lookup"><span data-stu-id="3ad05-183">The only possible setting for this parameter is **Important**.</span></span> |

<span data-ttu-id="3ad05-184">Установка и настройка агента SQL Server IaaS занимают несколько минут.</span><span class="sxs-lookup"><span data-stu-id="3ad05-184">It could take several minutes to install and configure the SQL Server IaaS Agent.</span></span>

<span data-ttu-id="3ad05-185">Чтобы отключить автоматизированную установку исправлений, выполните тот же сценарий без параметра **-Enable** в команде **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig**.</span><span class="sxs-lookup"><span data-stu-id="3ad05-185">To disable Automated Patching, run the same script without the **-Enable** parameter to the **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig**.</span></span> <span data-ttu-id="3ad05-186">Отсутствие параметра **-Enable** означает, что функцию нужно отключить.</span><span class="sxs-lookup"><span data-stu-id="3ad05-186">The absence of the **-Enable** parameter signals the command to disable the feature.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ad05-187">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3ad05-187">Next steps</span></span>
<span data-ttu-id="3ad05-188">Сведения о других доступных задачах автоматизации см. в разделе [Расширение агента IaaS для SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="3ad05-188">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="3ad05-189">Дополнительные сведения о запуске SQL Server на виртуальных машинах Azure см. в [обзоре использования SQL Server на виртуальных машинах Azure](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3ad05-189">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

