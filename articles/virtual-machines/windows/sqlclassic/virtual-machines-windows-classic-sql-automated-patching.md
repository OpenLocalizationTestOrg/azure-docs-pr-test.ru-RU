---
title: "aaaAutomated исправления для виртуальных машин SQL Server (классические) | Документы Microsoft"
description: "Описывается функция автоматического исправления hello для SQL Server виртуальных машин, работающих в Azure с помощью режима hello классического развертывания."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 737b2f65-08b9-4f54-b867-e987730265a8
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 2ef06b95705fc457605d6eb2fbc0afd490321843
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-classic"></a><span data-ttu-id="a5e9b-103">Автоматическая установка исправлений SQL Server на виртуальных машинах Azure (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="a5e9b-103">Automated Patching for SQL Server in Azure Virtual Machines (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a5e9b-104">Диспетчер ресурсов</span><span class="sxs-lookup"><span data-stu-id="a5e9b-104">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-automated-patching.md)
> * [<span data-ttu-id="a5e9b-105">Классический</span><span class="sxs-lookup"><span data-stu-id="a5e9b-105">Classic</span></span>](../classic/sql-automated-patching.md)
> 
> 

<span data-ttu-id="a5e9b-106">При автоматической установке исправлений на виртуальных машинах Azure с SQL Server задается период обслуживания.</span><span class="sxs-lookup"><span data-stu-id="a5e9b-106">Automated Patching establishes a maintenance window for an Azure Virtual Machine running SQL Server.</span></span> <span data-ttu-id="a5e9b-107">Установка автоматических обновлений возможна только в этот период обслуживания.</span><span class="sxs-lookup"><span data-stu-id="a5e9b-107">Automated Updates can only be installed during this maintenance window.</span></span> <span data-ttu-id="a5e9b-108">Для SQL Server это гарантирует, что системные обновления и перезапуски, связанный в hello наиболее сроки для hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="a5e9b-108">For SQL Server, this ensures that system updates and any associated restarts occur at hello best possible time for hello database.</span></span> <span data-ttu-id="a5e9b-109">Автоматические исправления выполняются зависит от hello [расширения агента SQL Server IaaS](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="a5e9b-109">Automated Patching depends on hello [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="a5e9b-110">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="a5e9b-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="a5e9b-111">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="a5e9b-111">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="a5e9b-112">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a5e9b-112">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="a5e9b-113">tooview hello диспетчера ресурсов версию этой статьи в разделе [автоматическое применение исправлений для SQL Server в диспетчере ресурсов Azure виртуальные машины](../sql/virtual-machines-windows-sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="a5e9b-113">tooview hello Resource Manager version of this article, see [Automated Patching for SQL Server in Azure Virtual Machines Resource Manager](../sql/virtual-machines-windows-sql-automated-patching.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a5e9b-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a5e9b-114">Prerequisites</span></span>
<span data-ttu-id="a5e9b-115">toouse автоматическое применение исправлений, рассмотрите возможность hello следующие предварительные требования:</span><span class="sxs-lookup"><span data-stu-id="a5e9b-115">toouse Automated Patching, consider hello following prerequisites:</span></span>

<span data-ttu-id="a5e9b-116">**Операционная система**</span><span class="sxs-lookup"><span data-stu-id="a5e9b-116">**Operating System**:</span></span>

* <span data-ttu-id="a5e9b-117">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="a5e9b-117">Windows Server 2012</span></span>
* <span data-ttu-id="a5e9b-118">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="a5e9b-118">Windows Server 2012 R2</span></span>
* <span data-ttu-id="a5e9b-119">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="a5e9b-119">Windows Server 2016</span></span>

<span data-ttu-id="a5e9b-120">**Версия SQL Server**</span><span class="sxs-lookup"><span data-stu-id="a5e9b-120">**SQL Server version**:</span></span>

* <span data-ttu-id="a5e9b-121">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="a5e9b-121">SQL Server 2012</span></span>
* <span data-ttu-id="a5e9b-122">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="a5e9b-122">SQL Server 2014</span></span>
* <span data-ttu-id="a5e9b-123">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="a5e9b-123">SQL Server 2016</span></span>

<span data-ttu-id="a5e9b-124">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="a5e9b-124">**Azure PowerShell**:</span></span>

* <span data-ttu-id="a5e9b-125">[Установка последних команд Azure PowerShell hello](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a5e9b-125">[Install hello latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="a5e9b-126">**Расширение IaaS для SQL Server**</span><span class="sxs-lookup"><span data-stu-id="a5e9b-126">**SQL Server IaaS Extension**:</span></span>

* <span data-ttu-id="a5e9b-127">[Установка расширения SQL Server IaaS hello](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="a5e9b-127">[Install hello SQL Server IaaS Extension](../classic/sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="a5e9b-128">данных</span><span class="sxs-lookup"><span data-stu-id="a5e9b-128">Settings</span></span>
<span data-ttu-id="a5e9b-129">Hello следующей таблице описаны параметры hello, которые могут быть настроены для автоматического исправления.</span><span class="sxs-lookup"><span data-stu-id="a5e9b-129">hello following table describes hello options that can be configured for Automated Patching.</span></span> <span data-ttu-id="a5e9b-130">Для классических виртуальных машин необходимо использовать PowerShell tooconfigure эти параметры.</span><span class="sxs-lookup"><span data-stu-id="a5e9b-130">For classic VMs, you must use PowerShell tooconfigure these settings.</span></span>

| <span data-ttu-id="a5e9b-131">Настройка</span><span class="sxs-lookup"><span data-stu-id="a5e9b-131">Setting</span></span> | <span data-ttu-id="a5e9b-132">Возможные значения</span><span class="sxs-lookup"><span data-stu-id="a5e9b-132">Possible values</span></span> | <span data-ttu-id="a5e9b-133">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="a5e9b-133">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a5e9b-134">**Автоматическое исправление**</span><span class="sxs-lookup"><span data-stu-id="a5e9b-134">**Automated Patching**</span></span> |<span data-ttu-id="a5e9b-135">Включено/отключено (отключено)</span><span class="sxs-lookup"><span data-stu-id="a5e9b-135">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="a5e9b-136">Включает или отключает автоматическую установку исправлений для виртуальной машины Azure.</span><span class="sxs-lookup"><span data-stu-id="a5e9b-136">Enables or disables Automated Patching for an Azure virtual machine.</span></span> |
| <span data-ttu-id="a5e9b-137">**Расписание обслуживания**</span><span class="sxs-lookup"><span data-stu-id="a5e9b-137">**Maintenance schedule**</span></span> |<span data-ttu-id="a5e9b-138">Каждый день, понедельник, вторник, среда, четверг, пятница, суббота, воскресенье</span><span class="sxs-lookup"><span data-stu-id="a5e9b-138">Everyday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday</span></span> |<span data-ttu-id="a5e9b-139">расписание Hello загрузку и установку обновлений Windows, SQL Server и Microsoft для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a5e9b-139">hello schedule for downloading and installing Windows, SQL Server, and Microsoft updates for your virtual machine.</span></span> |
| <span data-ttu-id="a5e9b-140">**Время начала обслуживания**</span><span class="sxs-lookup"><span data-stu-id="a5e9b-140">**Maintenance start hour**</span></span> |<span data-ttu-id="a5e9b-141">0–24</span><span class="sxs-lookup"><span data-stu-id="a5e9b-141">0-24</span></span> |<span data-ttu-id="a5e9b-142">Hello локальном запуске время tooupdate hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a5e9b-142">hello local start time tooupdate hello virtual machine.</span></span> |
| <span data-ttu-id="a5e9b-143">**Длительность периода обслуживания**</span><span class="sxs-lookup"><span data-stu-id="a5e9b-143">**Maintenance window duration**</span></span> |<span data-ttu-id="a5e9b-144">30–180</span><span class="sxs-lookup"><span data-stu-id="a5e9b-144">30-180</span></span> |<span data-ttu-id="a5e9b-145">Hello количество минут, разрешенных toocomplete hello загрузки и установки обновлений.</span><span class="sxs-lookup"><span data-stu-id="a5e9b-145">hello number of minutes permitted toocomplete hello download and installation of updates.</span></span> |
| <span data-ttu-id="a5e9b-146">**Категория исправления**</span><span class="sxs-lookup"><span data-stu-id="a5e9b-146">**Patch Category**</span></span> |<span data-ttu-id="a5e9b-147">Важно!</span><span class="sxs-lookup"><span data-stu-id="a5e9b-147">Important</span></span> |<span data-ttu-id="a5e9b-148">Категория Hello toodownload обновлений и установить.</span><span class="sxs-lookup"><span data-stu-id="a5e9b-148">hello category of updates toodownload and install.</span></span> |

## <a name="configuration-with-powershell"></a><span data-ttu-id="a5e9b-149">Настройка с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="a5e9b-149">Configuration with PowerShell</span></span>
<span data-ttu-id="a5e9b-150">В следующем примере hello, PowerShell — используется tooconfigure автоматического исправления на существующей виртуальной Машины SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a5e9b-150">In hello following example, PowerShell is used tooconfigure Automated Patching on an existing SQL Server VM.</span></span> <span data-ttu-id="a5e9b-151">Hello **New-AzureVMSqlServerAutoPatchingConfig** команда настраивает новый период обслуживания для автоматических обновлений.</span><span class="sxs-lookup"><span data-stu-id="a5e9b-151">hello **New-AzureVMSqlServerAutoPatchingConfig** command configures a new maintenance window for automatic updates.</span></span>

    $aps = New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoPatchingSettings $aps | Update-AzureVM

<span data-ttu-id="a5e9b-152">На основании этого примера hello следующей таблице описаны результаты применения hello на hello целевой виртуальной Машине Azure.</span><span class="sxs-lookup"><span data-stu-id="a5e9b-152">Based on this example, hello following table describes hello practical effect on hello target Azure VM:</span></span>

| <span data-ttu-id="a5e9b-153">Параметр</span><span class="sxs-lookup"><span data-stu-id="a5e9b-153">Parameter</span></span> | <span data-ttu-id="a5e9b-154">Результат</span><span class="sxs-lookup"><span data-stu-id="a5e9b-154">Effect</span></span> |
| --- | --- |
| <span data-ttu-id="a5e9b-155">**DayOfWeek**</span><span class="sxs-lookup"><span data-stu-id="a5e9b-155">**DayOfWeek**</span></span> |<span data-ttu-id="a5e9b-156">Исправления устанавливаются каждый четверг.</span><span class="sxs-lookup"><span data-stu-id="a5e9b-156">Patches installed every Thursday.</span></span> |
| <span data-ttu-id="a5e9b-157">**MaintenanceWindowStartingHour**</span><span class="sxs-lookup"><span data-stu-id="a5e9b-157">**MaintenanceWindowStartingHour**</span></span> |<span data-ttu-id="a5e9b-158">Установка обновлений начинается в 11:00.</span><span class="sxs-lookup"><span data-stu-id="a5e9b-158">Begin updates at 11:00am.</span></span> |
| <span data-ttu-id="a5e9b-159">**MaintenanceWindowsDuration**</span><span class="sxs-lookup"><span data-stu-id="a5e9b-159">**MaintenanceWindowsDuration**</span></span> |<span data-ttu-id="a5e9b-160">Обновления должны быть установлены в течение 120 минут.</span><span class="sxs-lookup"><span data-stu-id="a5e9b-160">Patches must be installed within 120 minutes.</span></span> <span data-ttu-id="a5e9b-161">На основании времени начала hello, они должны выполнить с 1:00 pm.</span><span class="sxs-lookup"><span data-stu-id="a5e9b-161">Based on hello start time, they must complete by 1:00pm.</span></span> |
| <span data-ttu-id="a5e9b-162">**PatchCategory**</span><span class="sxs-lookup"><span data-stu-id="a5e9b-162">**PatchCategory**</span></span> |<span data-ttu-id="a5e9b-163">Hello только возможных для этого параметра задается значение «Важно!».</span><span class="sxs-lookup"><span data-stu-id="a5e9b-163">hello only possible setting for this parameter is “Important”.</span></span> |

<span data-ttu-id="a5e9b-164">Он может занять несколько минут tooinstall и настроить агент SQL Server IaaS hello.</span><span class="sxs-lookup"><span data-stu-id="a5e9b-164">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span>

<span data-ttu-id="a5e9b-165">toodisable автоматического исправления выполнения hello же сценарий, не hello - toohello включить параметр New-AzureVMSqlServerAutoPatchingConfig.</span><span class="sxs-lookup"><span data-stu-id="a5e9b-165">toodisable Automated Patching, run hello same script without hello -Enable parameter toohello New-AzureVMSqlServerAutoPatchingConfig.</span></span> <span data-ttu-id="a5e9b-166">Как и установки, может занять несколько минут toodisable автоматических исправлений.</span><span class="sxs-lookup"><span data-stu-id="a5e9b-166">As with installation, it can take several minutes toodisable Automated Patching.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a5e9b-167">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a5e9b-167">Next steps</span></span>
<span data-ttu-id="a5e9b-168">Сведения о других доступных задачах автоматизации см. в разделе [Расширение агента IaaS для SQL Server](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="a5e9b-168">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

<span data-ttu-id="a5e9b-169">Дополнительные сведения о запуске SQL Server на виртуальных машинах Azure см. в [обзоре использования SQL Server на виртуальных машинах Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a5e9b-169">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

