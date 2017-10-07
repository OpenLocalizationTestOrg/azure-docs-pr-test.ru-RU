---
title: "задачи управления aaaAutomate на виртуальных машинах SQL (классические) | Документы Microsoft"
description: "В этом разделе описывается, как toomanage hello расширения агента SQL Server, которое автоматизирует конкретных задач администрирования SQL Server. Эти задачи включают в себя автоматическую архивацию, автоматическую установку исправлений и интеграцию с хранилищем ключей Azure. В этом разделе используется режим классическое развертывание hello."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a9bda2e7-cdba-427c-bc30-77cde4376f3a
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a1dc011e0526845701eaf0c365007938f9ee32ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-hello-sql-server-agent-extension-classic"></a><span data-ttu-id="b2990-105">Автоматизация задач управления на виртуальных машинах Azure с помощью hello расширение агента SQL Server (классические)</span><span class="sxs-lookup"><span data-stu-id="b2990-105">Automate management tasks on Azure Virtual Machines with hello SQL Server Agent Extension (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b2990-106">Диспетчер ресурсов</span><span class="sxs-lookup"><span data-stu-id="b2990-106">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-server-agent-extension.md)
> * [<span data-ttu-id="b2990-107">Классический</span><span class="sxs-lookup"><span data-stu-id="b2990-107">Classic</span></span>](../classic/sql-server-agent-extension.md)
> 
>
 
<span data-ttu-id="b2990-108">Hello расширения агента IaaS SQL Server (SQLIaaSAgent) работает на виртуальных машинах Azure tooautomate административных задач.</span><span class="sxs-lookup"><span data-stu-id="b2990-108">hello SQL Server IaaS Agent Extension (SQLIaaSAgent) runs on Azure virtual machines tooautomate administration tasks.</span></span> <span data-ttu-id="b2990-109">Здесь представлен обзор служб hello, поддерживаемые расширения hello, а также инструкции по установке, состояния и удаления.</span><span class="sxs-lookup"><span data-stu-id="b2990-109">This topic provides an overview of hello services supported by hello extension as well as instructions for installation, status, and removal.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="b2990-110">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="b2990-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="b2990-111">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="b2990-111">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="b2990-112">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b2990-112">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="b2990-113">tooview hello диспетчера ресурсов версию этой статьи в разделе [расширение агента SQL Server для SQL Server виртуальных машин диспетчера ресурсов](../sql/virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="b2990-113">tooview hello Resource Manager version of this article, see [SQL Server Agent Extension for SQL Server VMs Resource Manager](../sql/virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="supported-services"></a><span data-ttu-id="b2990-114">Поддерживаемые службы</span><span class="sxs-lookup"><span data-stu-id="b2990-114">Supported services</span></span>
<span data-ttu-id="b2990-115">Hello расширения агента IaaS SQL Server поддерживает следующие задачи администрирования hello:</span><span class="sxs-lookup"><span data-stu-id="b2990-115">hello SQL Server IaaS Agent Extension supports hello following administration tasks:</span></span>

| <span data-ttu-id="b2990-116">Функция администрирования</span><span class="sxs-lookup"><span data-stu-id="b2990-116">Administration feature</span></span> | <span data-ttu-id="b2990-117">Описание</span><span class="sxs-lookup"><span data-stu-id="b2990-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b2990-118">**Автоматическая архивация SQL**</span><span class="sxs-lookup"><span data-stu-id="b2990-118">**SQL Automated Backup**</span></span> |<span data-ttu-id="b2990-119">Автоматизирует hello планирования резервного копирования для всех баз данных для экземпляра по умолчанию hello объекта SQL Server в hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="b2990-119">Automates hello scheduling of backups for all databases for hello default instance of SQL Server in hello VM.</span></span> <span data-ttu-id="b2990-120">Дополнительные сведения см. в статье [Автоматическая архивация SQL Server на виртуальных машинах Azure (классическая модель)](../classic/sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="b2990-120">For more information, see [Automated backup for SQL Server in Azure Virtual Machines (Classic)](../classic/sql-automated-backup.md).</span></span> |
| <span data-ttu-id="b2990-121">**Автоматическая установка исправлений SQL**</span><span class="sxs-lookup"><span data-stu-id="b2990-121">**SQL Automated Patching**</span></span> |<span data-ttu-id="b2990-122">Настраивает периода обслуживания, во время обновления, которые размещаются tooyour предпринять виртуальной Машины, чтобы избежать обновления рабочее время для рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="b2990-122">Configures a maintenance window during which updates tooyour VM can take place, so  you can avoid updates during peak times for your workload.</span></span> <span data-ttu-id="b2990-123">Дополнительные сведения см. в статье [Автоматическая установка исправлений SQL Server на виртуальных машинах Azure (классическая модель)](../classic/sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="b2990-123">For more information, see [Automated patching for SQL Server in Azure Virtual Machines (Classic)](../classic/sql-automated-patching.md).</span></span> |
| <span data-ttu-id="b2990-124">**Интеграция с хранилищем ключей Azure**</span><span class="sxs-lookup"><span data-stu-id="b2990-124">**Azure Key Vault Integration**</span></span> |<span data-ttu-id="b2990-125">Включает tooautomatically можно установить и настроить хранилище ключей Azure в вашей виртуальной Машине SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b2990-125">Enables you tooautomatically install and configure Azure Key Vault on your SQL Server VM.</span></span> <span data-ttu-id="b2990-126">Дополнительные сведения см. в статье [Настройка интеграции хранилища ключей Azure для SQL Server на виртуальных машинах Azure (классическая модель)](../classic/ps-sql-keyvault.md).</span><span class="sxs-lookup"><span data-stu-id="b2990-126">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs (Classic)](../classic/ps-sql-keyvault.md).</span></span> |

## <a name="prerequisites"></a><span data-ttu-id="b2990-127">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b2990-127">Prerequisites</span></span>
<span data-ttu-id="b2990-128">Требования к toouse hello расширение агента IaaS SQL Server на виртуальной Машине:</span><span class="sxs-lookup"><span data-stu-id="b2990-128">Requirements toouse hello SQL Server IaaS Agent Extension on your VM:</span></span>

### <a name="operating-system"></a><span data-ttu-id="b2990-129">Операционная система:</span><span class="sxs-lookup"><span data-stu-id="b2990-129">Operating System:</span></span>
* <span data-ttu-id="b2990-130">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="b2990-130">Windows Server 2012</span></span>
* <span data-ttu-id="b2990-131">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="b2990-131">Windows Server 2012 R2</span></span>
* <span data-ttu-id="b2990-132">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="b2990-132">Windows Server 2016</span></span>

### <a name="sql-server-versions"></a><span data-ttu-id="b2990-133">Версии SQL Server:</span><span class="sxs-lookup"><span data-stu-id="b2990-133">SQL Server versions:</span></span>
* <span data-ttu-id="b2990-134">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="b2990-134">SQL Server 2012</span></span>
* <span data-ttu-id="b2990-135">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="b2990-135">SQL Server 2014</span></span>
* <span data-ttu-id="b2990-136">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="b2990-136">SQL Server 2016</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="b2990-137">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b2990-137">Azure PowerShell:</span></span>
<span data-ttu-id="b2990-138">[Загрузить и настроить hello последних команд Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b2990-138">[Download and configure hello latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="b2990-139">Запустите Windows PowerShell и подключите его tooyour подписки Azure с hello **Add-AzureAccount** команды.</span><span class="sxs-lookup"><span data-stu-id="b2990-139">Start Windows PowerShell, and connect it tooyour Azure subscription with hello **Add-AzureAccount** command.</span></span>

    Add-AzureAccount

<span data-ttu-id="b2990-140">Если у вас несколько подписок, используйте **Select-AzureSubscription** tooselect hello подписки, содержащей целевой классической виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="b2990-140">If you have multiple subscriptions, use **Select-AzureSubscription** tooselect hello subscription that contains your target classic VM.</span></span>

    Select-AzureSubscription -SubscriptionName <subscriptionname>

<span data-ttu-id="b2990-141">На этом этапе можно получить список hello классических виртуальных машин и их имена связанная служба с hello **Get-AzureVM** команды.</span><span class="sxs-lookup"><span data-stu-id="b2990-141">At this point, you can get a list of hello classic virtual machines and their associated service names with hello **Get-AzureVM** command.</span></span>

    Get-AzureVM

## <a name="installation"></a><span data-ttu-id="b2990-142">Установка</span><span class="sxs-lookup"><span data-stu-id="b2990-142">Installation</span></span>
<span data-ttu-id="b2990-143">Для классических виртуальных машин необходимо использовать PowerShell tooinstall hello расширения агента IaaS SQL Server и настроить связанные с ними службы.</span><span class="sxs-lookup"><span data-stu-id="b2990-143">For classic VMs, you must use PowerShell tooinstall hello SQL Server IaaS Agent Extension and configure its associated services.</span></span> <span data-ttu-id="b2990-144">Используйте hello **AzureVMSqlServerExtension набор** расширения hello tooinstall командлета PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b2990-144">Use hello **Set-AzureVMSqlServerExtension** PowerShell cmdlet tooinstall hello extension.</span></span> <span data-ttu-id="b2990-145">Например hello, следующая команда устанавливает расширение hello на ВМ Windows Server (классические) и называет ее «SQLIaaSExtension».</span><span class="sxs-lookup"><span data-stu-id="b2990-145">For example, hello following command installs hello extension on a Windows Server VM (classic) and names it "SQLIaaSExtension".</span></span>

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -ReferenceName "SQLIaasExtension" -Version "1.2" | Update-AzureVM

<span data-ttu-id="b2990-146">При обновлении toohello последнюю версию агента расширения SQL IaaS hello, необходимо перезапустить виртуальную машину после обновления расширения hello.</span><span class="sxs-lookup"><span data-stu-id="b2990-146">If you update toohello latest version of hello SQL IaaS Agent Extension, you must restart your virtual machine after updating hello extension.</span></span>

> [!NOTE]
> <span data-ttu-id="b2990-147">Классических виртуальных машин не имеют параметр tooinstall и настроить hello агента расширения SQL IaaS через портал hello.</span><span class="sxs-lookup"><span data-stu-id="b2990-147">Classic virtual machines do not have an option tooinstall and configure hello SQL IaaS Agent Extension through hello portal.</span></span>
> 
> 

## <a name="status"></a><span data-ttu-id="b2990-148">Состояние</span><span class="sxs-lookup"><span data-stu-id="b2990-148">Status</span></span>
<span data-ttu-id="b2990-149">Одним из способов tooverify, что расширение hello установлено — состояние агента hello tooview hello портала Azure.</span><span class="sxs-lookup"><span data-stu-id="b2990-149">One way tooverify that hello extension is installed is tooview hello agent status in hello Azure Portal.</span></span> <span data-ttu-id="b2990-150">Выберите виртуальную машину, перечисленных в колонке hello виртуальной машины и выберите команду **расширения**.</span><span class="sxs-lookup"><span data-stu-id="b2990-150">Select a virtual machine listed in hello virtual machine blade, and then click on **Extensions**.</span></span> <span data-ttu-id="b2990-151">Вы увидите hello **SQLIaaSAgent** расширение.</span><span class="sxs-lookup"><span data-stu-id="b2990-151">You should see hello **SQLIaaSAgent** extension listed.</span></span>

![Расширение агента IaaS для SQL Server на портале Azure](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-portal.png)

<span data-ttu-id="b2990-153">Можно также использовать hello **Get AzureVMSqlServerExtension** командлет Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="b2990-153">You can also use hello **Get-AzureVMSqlServerExtension** Azure Powershell cmdlet.</span></span>

    Get-AzureVM –ServiceName "service" –Name "vmname" | Get-AzureVMSqlServerExtension

## <a name="removal"></a><span data-ttu-id="b2990-154">Удаление</span><span class="sxs-lookup"><span data-stu-id="b2990-154">Removal</span></span>
<span data-ttu-id="b2990-155">В hello портал Azure, можно удалить расширение hello, нажав кнопку многоточия hello hello **расширения** колонку свойств виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b2990-155">In hello Azure Portal, you can uninstall hello extension by clicking hello ellipsis on hello **Extensions** blade of your virtual machine properties.</span></span> <span data-ttu-id="b2990-156">Щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="b2990-156">Then click **Uninstall**.</span></span>

![Удаление hello расширения агента IaaS SQL Server на портале Azure](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-uninstall.png)

<span data-ttu-id="b2990-158">Можно также использовать hello **AzureVMSqlServerExtension удаление** командлета Powershell.</span><span class="sxs-lookup"><span data-stu-id="b2990-158">You can also use hello **Remove-AzureVMSqlServerExtension** Powershell cmdlet.</span></span>

    Get-AzureVM –ServiceName "service" –Name "vmname" | Remove-AzureVMSqlServerExtension | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="b2990-159">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b2990-159">Next Steps</span></span>
<span data-ttu-id="b2990-160">Начать использовать одну из служб hello, поддерживаемого расширением hello.</span><span class="sxs-lookup"><span data-stu-id="b2990-160">Begin using one of hello services supported by hello extension.</span></span> <span data-ttu-id="b2990-161">Дополнительные сведения см. в разделе hello разделы, на которые ссылается hello [поддерживается служб](#supported-services) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="b2990-161">For more details, see hello topics referenced in hello [Supported services](#supported-services) section of this article.</span></span>

<span data-ttu-id="b2990-162">Подробные сведения о работе SQL Server на виртуальных машинах Azure см. в разделе [Общие сведения об SQL Server на виртуальных машинах Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b2990-162">For more information about running SQL Server on Azure Virtual Machines, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

