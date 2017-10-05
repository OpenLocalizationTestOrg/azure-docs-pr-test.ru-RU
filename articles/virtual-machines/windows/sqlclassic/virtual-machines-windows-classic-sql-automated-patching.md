---
title: "Автоматизированная установка исправлений для виртуальных машин SQL Server (классическая модель) | Документация Майкрософт"
description: "Описывается функция автоматической установки исправлений для виртуальных машин SQL Server в Azure, использующих классический режим развертывания."
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
ms.openlocfilehash: 1959871141f196ba80ffd7b37e62e5ea5b42dba3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-classic"></a><span data-ttu-id="0ded3-103">Автоматическая установка исправлений SQL Server на виртуальных машинах Azure (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="0ded3-103">Automated Patching for SQL Server in Azure Virtual Machines (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0ded3-104">Диспетчер ресурсов</span><span class="sxs-lookup"><span data-stu-id="0ded3-104">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-automated-patching.md)
> * [<span data-ttu-id="0ded3-105">Классический</span><span class="sxs-lookup"><span data-stu-id="0ded3-105">Classic</span></span>](../classic/sql-automated-patching.md)
> 
> 

<span data-ttu-id="0ded3-106">При автоматической установке исправлений на виртуальных машинах Azure с SQL Server задается период обслуживания.</span><span class="sxs-lookup"><span data-stu-id="0ded3-106">Automated Patching establishes a maintenance window for an Azure Virtual Machine running SQL Server.</span></span> <span data-ttu-id="0ded3-107">Установка автоматических обновлений возможна только в этот период обслуживания.</span><span class="sxs-lookup"><span data-stu-id="0ded3-107">Automated Updates can only be installed during this maintenance window.</span></span> <span data-ttu-id="0ded3-108">Для SQL Server это гарантирует, что системные обновления и связанные с ними перезапуски системы будут происходить в наиболее удобное для базы данных время.</span><span class="sxs-lookup"><span data-stu-id="0ded3-108">For SQL Server, this ensures that system updates and any associated restarts occur at the best possible time for the database.</span></span> <span data-ttu-id="0ded3-109">Автоматическая установка исправлений зависит от [Расширения агента IaaS для SQL Server](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="0ded3-109">Automated Patching depends on the [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="0ded3-110">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="0ded3-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="0ded3-111">В этой статье рассматривается использование классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="0ded3-111">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="0ded3-112">Для большинства новых развертываний Майкрософт рекомендует использовать модель диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="0ded3-112">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="0ded3-113">Версию этой статьи для Resource Manager см. в статье [Автоматическое исправление SQL Server на виртуальных машинах Azure Resource Manager](../sql/virtual-machines-windows-sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="0ded3-113">To view the Resource Manager version of this article, see [Automated Patching for SQL Server in Azure Virtual Machines Resource Manager](../sql/virtual-machines-windows-sql-automated-patching.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0ded3-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0ded3-114">Prerequisites</span></span>
<span data-ttu-id="0ded3-115">Для использования автоматической установки исправлений необходимо выполнить следующие предварительные требования.</span><span class="sxs-lookup"><span data-stu-id="0ded3-115">To use Automated Patching, consider the following prerequisites:</span></span>

<span data-ttu-id="0ded3-116">**Операционная система**</span><span class="sxs-lookup"><span data-stu-id="0ded3-116">**Operating System**:</span></span>

* <span data-ttu-id="0ded3-117">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="0ded3-117">Windows Server 2012</span></span>
* <span data-ttu-id="0ded3-118">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="0ded3-118">Windows Server 2012 R2</span></span>
* <span data-ttu-id="0ded3-119">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="0ded3-119">Windows Server 2016</span></span>

<span data-ttu-id="0ded3-120">**Версия SQL Server**</span><span class="sxs-lookup"><span data-stu-id="0ded3-120">**SQL Server version**:</span></span>

* <span data-ttu-id="0ded3-121">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="0ded3-121">SQL Server 2012</span></span>
* <span data-ttu-id="0ded3-122">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="0ded3-122">SQL Server 2014</span></span>
* <span data-ttu-id="0ded3-123">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="0ded3-123">SQL Server 2016</span></span>

<span data-ttu-id="0ded3-124">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="0ded3-124">**Azure PowerShell**:</span></span>

* <span data-ttu-id="0ded3-125">[Установите последнюю версию команд Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0ded3-125">[Install the latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="0ded3-126">**Расширение IaaS для SQL Server**</span><span class="sxs-lookup"><span data-stu-id="0ded3-126">**SQL Server IaaS Extension**:</span></span>

* <span data-ttu-id="0ded3-127">[Установите расширение IaaS для SQL Server](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="0ded3-127">[Install the SQL Server IaaS Extension](../classic/sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="0ded3-128">Параметры</span><span class="sxs-lookup"><span data-stu-id="0ded3-128">Settings</span></span>
<span data-ttu-id="0ded3-129">В приведенной ниже таблице описаны параметры для настройки автоматической установки исправлений.</span><span class="sxs-lookup"><span data-stu-id="0ded3-129">The following table describes the options that can be configured for Automated Patching.</span></span> <span data-ttu-id="0ded3-130">Для виртуальных машин, развернутых с использованием классической модели, эти параметры необходимо настроить с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0ded3-130">For classic VMs, you must use PowerShell to configure these settings.</span></span>

| <span data-ttu-id="0ded3-131">Настройка</span><span class="sxs-lookup"><span data-stu-id="0ded3-131">Setting</span></span> | <span data-ttu-id="0ded3-132">Возможные значения</span><span class="sxs-lookup"><span data-stu-id="0ded3-132">Possible values</span></span> | <span data-ttu-id="0ded3-133">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="0ded3-133">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ded3-134">**Автоматическое исправление**</span><span class="sxs-lookup"><span data-stu-id="0ded3-134">**Automated Patching**</span></span> |<span data-ttu-id="0ded3-135">Включено/отключено (отключено)</span><span class="sxs-lookup"><span data-stu-id="0ded3-135">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="0ded3-136">Включает или отключает автоматическую установку исправлений для виртуальной машины Azure.</span><span class="sxs-lookup"><span data-stu-id="0ded3-136">Enables or disables Automated Patching for an Azure virtual machine.</span></span> |
| <span data-ttu-id="0ded3-137">**Расписание обслуживания**</span><span class="sxs-lookup"><span data-stu-id="0ded3-137">**Maintenance schedule**</span></span> |<span data-ttu-id="0ded3-138">Каждый день, понедельник, вторник, среда, четверг, пятница, суббота, воскресенье</span><span class="sxs-lookup"><span data-stu-id="0ded3-138">Everyday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday</span></span> |<span data-ttu-id="0ded3-139">Расписание для скачивания и установки обновлений Windows, SQL Server и обновлений Майкрософт для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0ded3-139">The schedule for downloading and installing Windows, SQL Server, and Microsoft updates for your virtual machine.</span></span> |
| <span data-ttu-id="0ded3-140">**Время начала обслуживания**</span><span class="sxs-lookup"><span data-stu-id="0ded3-140">**Maintenance start hour**</span></span> |<span data-ttu-id="0ded3-141">0–24</span><span class="sxs-lookup"><span data-stu-id="0ded3-141">0-24</span></span> |<span data-ttu-id="0ded3-142">Локальное время начала обновления виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0ded3-142">The local start time to update the virtual machine.</span></span> |
| <span data-ttu-id="0ded3-143">**Длительность периода обслуживания**</span><span class="sxs-lookup"><span data-stu-id="0ded3-143">**Maintenance window duration**</span></span> |<span data-ttu-id="0ded3-144">30–180</span><span class="sxs-lookup"><span data-stu-id="0ded3-144">30-180</span></span> |<span data-ttu-id="0ded3-145">Допустимое количество минут для скачивания и установки обновлений.</span><span class="sxs-lookup"><span data-stu-id="0ded3-145">The number of minutes permitted to complete the download and installation of updates.</span></span> |
| <span data-ttu-id="0ded3-146">**Категория исправления**</span><span class="sxs-lookup"><span data-stu-id="0ded3-146">**Patch Category**</span></span> |<span data-ttu-id="0ded3-147">Важно!</span><span class="sxs-lookup"><span data-stu-id="0ded3-147">Important</span></span> |<span data-ttu-id="0ded3-148">Категория обновлений, которые будут скачаны и установлены.</span><span class="sxs-lookup"><span data-stu-id="0ded3-148">The category of updates to download and install.</span></span> |

## <a name="configuration-with-powershell"></a><span data-ttu-id="0ded3-149">Настройка с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="0ded3-149">Configuration with PowerShell</span></span>
<span data-ttu-id="0ded3-150">В следующем примере для настройки автоматической установки исправлений на существующей виртуальной машине SQL Server используется PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0ded3-150">In the following example, PowerShell is used to configure Automated Patching on an existing SQL Server VM.</span></span> <span data-ttu-id="0ded3-151">Команда **New-AzureVMSqlServerAutoPatchingConfig** настраивает новый период обслуживания для автоматической установки обновлений.</span><span class="sxs-lookup"><span data-stu-id="0ded3-151">The **New-AzureVMSqlServerAutoPatchingConfig** command configures a new maintenance window for automatic updates.</span></span>

    $aps = New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoPatchingSettings $aps | Update-AzureVM

<span data-ttu-id="0ded3-152">В представленной ниже таблице показано фактическое воздействие на конечную виртуальную машину Azure на основе данного примера.</span><span class="sxs-lookup"><span data-stu-id="0ded3-152">Based on this example, the following table describes the practical effect on the target Azure VM:</span></span>

| <span data-ttu-id="0ded3-153">Параметр</span><span class="sxs-lookup"><span data-stu-id="0ded3-153">Parameter</span></span> | <span data-ttu-id="0ded3-154">Результат</span><span class="sxs-lookup"><span data-stu-id="0ded3-154">Effect</span></span> |
| --- | --- |
| <span data-ttu-id="0ded3-155">**DayOfWeek**</span><span class="sxs-lookup"><span data-stu-id="0ded3-155">**DayOfWeek**</span></span> |<span data-ttu-id="0ded3-156">Исправления устанавливаются каждый четверг.</span><span class="sxs-lookup"><span data-stu-id="0ded3-156">Patches installed every Thursday.</span></span> |
| <span data-ttu-id="0ded3-157">**MaintenanceWindowStartingHour**</span><span class="sxs-lookup"><span data-stu-id="0ded3-157">**MaintenanceWindowStartingHour**</span></span> |<span data-ttu-id="0ded3-158">Установка обновлений начинается в 11:00.</span><span class="sxs-lookup"><span data-stu-id="0ded3-158">Begin updates at 11:00am.</span></span> |
| <span data-ttu-id="0ded3-159">**MaintenanceWindowsDuration**</span><span class="sxs-lookup"><span data-stu-id="0ded3-159">**MaintenanceWindowsDuration**</span></span> |<span data-ttu-id="0ded3-160">Обновления должны быть установлены в течение 120 минут.</span><span class="sxs-lookup"><span data-stu-id="0ded3-160">Patches must be installed within 120 minutes.</span></span> <span data-ttu-id="0ded3-161">С учетом времени начала установка обновлений должна завершаться к 13:00.</span><span class="sxs-lookup"><span data-stu-id="0ded3-161">Based on the start time, they must complete by 1:00pm.</span></span> |
| <span data-ttu-id="0ded3-162">**PatchCategory**</span><span class="sxs-lookup"><span data-stu-id="0ded3-162">**PatchCategory**</span></span> |<span data-ttu-id="0ded3-163">Единственное возможное значение для этого параметра — Important (Важно).</span><span class="sxs-lookup"><span data-stu-id="0ded3-163">The only possible setting for this parameter is “Important”.</span></span> |

<span data-ttu-id="0ded3-164">Установка и настройка агента SQL Server IaaS занимают несколько минут.</span><span class="sxs-lookup"><span data-stu-id="0ded3-164">It could take several minutes to install and configure the SQL Server IaaS Agent.</span></span>

<span data-ttu-id="0ded3-165">Чтобы отключить автоматическую установку обновлений, выполните тот же скрипт без параметра -Enable в команде New-AzureVMSqlServerAutoPatchingConfig.</span><span class="sxs-lookup"><span data-stu-id="0ded3-165">To disable Automated Patching, run the same script without the -Enable parameter to the New-AzureVMSqlServerAutoPatchingConfig.</span></span> <span data-ttu-id="0ded3-166">Как и установка, отключение автоматической установки исправлений занимает несколько минут.</span><span class="sxs-lookup"><span data-stu-id="0ded3-166">As with installation, it can take several minutes to disable Automated Patching.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ded3-167">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0ded3-167">Next steps</span></span>
<span data-ttu-id="0ded3-168">Сведения о других доступных задачах автоматизации см. в разделе [Расширение агента IaaS для SQL Server](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="0ded3-168">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

<span data-ttu-id="0ded3-169">Дополнительные сведения о запуске SQL Server на виртуальных машинах Azure см. в [обзоре использования SQL Server на виртуальных машинах Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0ded3-169">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

