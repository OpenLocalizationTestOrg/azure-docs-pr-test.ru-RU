---
title: "задачи управления aaaAutomate на виртуальных машинах SQL (диспетчера ресурсов) | Документы Microsoft"
description: "В этом разделе описывается, как toomanage hello расширения агента SQL Server, которое автоматизирует конкретных задач администрирования SQL Server. Эти задачи включают в себя автоматическую архивацию, автоматическую установку исправлений и интеграцию с хранилищем ключей Azure. В этом разделе используется режим развертывания диспетчера ресурсов hello."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: effe4e2f-35b5-490a-b5ef-b06746083da4
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ae917612c4af59f12c0b083440673bdc555e9d56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-hello-sql-server-agent-extension-resource-manager"></a><span data-ttu-id="de267-105">Автоматизация задач управления на виртуальных машинах Azure с помощью hello расширение агента SQL Server (диспетчер ресурсов)</span><span class="sxs-lookup"><span data-stu-id="de267-105">Automate management tasks on Azure Virtual Machines with hello SQL Server Agent Extension (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="de267-106">Диспетчер ресурсов</span><span class="sxs-lookup"><span data-stu-id="de267-106">Resource Manager</span></span>](virtual-machines-windows-sql-server-agent-extension.md)
> * [<span data-ttu-id="de267-107">Классический</span><span class="sxs-lookup"><span data-stu-id="de267-107">Classic</span></span>](../classic/sql-server-agent-extension.md)
> 
> 

<span data-ttu-id="de267-108">Hello расширения агента IaaS SQL Server (SQLIaaSExtension) работает на виртуальных машинах Azure tooautomate административных задач.</span><span class="sxs-lookup"><span data-stu-id="de267-108">hello SQL Server IaaS Agent Extension (SQLIaaSExtension) runs on Azure virtual machines tooautomate administration tasks.</span></span> <span data-ttu-id="de267-109">Здесь представлен обзор служб hello, поддерживаемые расширения hello, а также инструкции по установке, состояния и удаления.</span><span class="sxs-lookup"><span data-stu-id="de267-109">This topic provides an overview of hello services supported by hello extension as well as instructions for installation, status, and removal.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="de267-110">tooview hello классической версии данной статьи, в разделе [расширение агента SQL Server для классических виртуальных машин SQL Server](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="de267-110">tooview hello classic version of this article, see [SQL Server Agent Extension for SQL Server VMs Classic](../classic/sql-server-agent-extension.md).</span></span>

## <a name="supported-services"></a><span data-ttu-id="de267-111">Поддерживаемые службы</span><span class="sxs-lookup"><span data-stu-id="de267-111">Supported services</span></span>
<span data-ttu-id="de267-112">Hello расширения агента IaaS SQL Server поддерживает следующие задачи администрирования hello:</span><span class="sxs-lookup"><span data-stu-id="de267-112">hello SQL Server IaaS Agent Extension supports hello following administration tasks:</span></span>

| <span data-ttu-id="de267-113">Функция администрирования</span><span class="sxs-lookup"><span data-stu-id="de267-113">Administration feature</span></span> | <span data-ttu-id="de267-114">Описание</span><span class="sxs-lookup"><span data-stu-id="de267-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="de267-115">**Автоматическая архивация SQL**</span><span class="sxs-lookup"><span data-stu-id="de267-115">**SQL Automated Backup**</span></span> |<span data-ttu-id="de267-116">Автоматизирует hello планирования резервного копирования для всех баз данных для экземпляра по умолчанию hello объекта SQL Server в hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="de267-116">Automates hello scheduling of backups for all databases for hello default instance of SQL Server in hello VM.</span></span> <span data-ttu-id="de267-117">Дополнительные сведения см. в статье [Автоматическая архивация SQL Server на виртуальных машинах Azure (Resource Manager)](virtual-machines-windows-sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="de267-117">For more information, see [Automated backup for SQL Server in Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-backup.md).</span></span> |
| <span data-ttu-id="de267-118">**Автоматическая установка исправлений SQL**</span><span class="sxs-lookup"><span data-stu-id="de267-118">**SQL Automated Patching**</span></span> |<span data-ttu-id="de267-119">Настраивает периода обслуживания, во время обновления, которые размещаются tooyour предпринять виртуальной Машины, чтобы избежать обновления рабочее время для рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="de267-119">Configures a maintenance window during which updates tooyour VM can take place, so  you can avoid updates during peak times for your workload.</span></span> <span data-ttu-id="de267-120">Дополнительные сведения см. в статье [Автоматическая установка исправлений SQL Server на виртуальных машинах Azure (Resource Manager)](virtual-machines-windows-sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="de267-120">For more information, see [Automated patching for SQL Server in Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-patching.md).</span></span> |
| <span data-ttu-id="de267-121">**Интеграция с хранилищем ключей Azure**</span><span class="sxs-lookup"><span data-stu-id="de267-121">**Azure Key Vault Integration**</span></span> |<span data-ttu-id="de267-122">Включает tooautomatically можно установить и настроить хранилище ключей Azure в вашей виртуальной Машине SQL Server.</span><span class="sxs-lookup"><span data-stu-id="de267-122">Enables you tooautomatically install and configure Azure Key Vault on your SQL Server VM.</span></span> <span data-ttu-id="de267-123">Дополнительные сведения см. в статье [Настройка интеграции хранилища ключей Azure для SQL Server на виртуальных машинах Azure (диспетчер ресурсов)](virtual-machines-windows-ps-sql-keyvault.md).</span><span class="sxs-lookup"><span data-stu-id="de267-123">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs (Resource Manager)](virtual-machines-windows-ps-sql-keyvault.md).</span></span> |

<span data-ttu-id="de267-124">После установки и запуска, hello расширения агента IaaS SQL Server создает эти функции администрирования на панели SQL Server hello hello виртуальной машины в hello портала Azure и Azure PowerShell для SQL Server marketplace образов и через Azure PowerShell для установки в ручном режиме hello расширения.</span><span class="sxs-lookup"><span data-stu-id="de267-124">Once installed and running, hello SQL Server IaaS Agent Extension makes these administration features available on hello SQL Server panel of hello virtual machine in hello Azure Portal and through Azure PowerShell for SQL Server marketplace images, and through Azure PowerShell for manual installations of hello extension.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="de267-125">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="de267-125">Prerequisites</span></span>
<span data-ttu-id="de267-126">Требования к toouse hello расширение агента IaaS SQL Server на виртуальной Машине:</span><span class="sxs-lookup"><span data-stu-id="de267-126">Requirements toouse hello SQL Server IaaS Agent Extension on your VM:</span></span>

<span data-ttu-id="de267-127">**Операционная система**</span><span class="sxs-lookup"><span data-stu-id="de267-127">**Operating System**:</span></span>

* <span data-ttu-id="de267-128">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="de267-128">Windows Server 2012</span></span>
* <span data-ttu-id="de267-129">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="de267-129">Windows Server 2012 R2</span></span>
* <span data-ttu-id="de267-130">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="de267-130">Windows Server 2016</span></span>

<span data-ttu-id="de267-131">**Версии SQL Server**</span><span class="sxs-lookup"><span data-stu-id="de267-131">**SQL Server versions**:</span></span>

* <span data-ttu-id="de267-132">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="de267-132">SQL Server 2012</span></span>
* <span data-ttu-id="de267-133">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="de267-133">SQL Server 2014</span></span>
* <span data-ttu-id="de267-134">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="de267-134">SQL Server 2016</span></span>

<span data-ttu-id="de267-135">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="de267-135">**Azure PowerShell**:</span></span>

* [<span data-ttu-id="de267-136">Загрузить и настроить hello последних команд Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="de267-136">Download and configure hello latest Azure PowerShell commands</span></span>](/powershell/azure/overview)

## <a name="installation"></a><span data-ttu-id="de267-137">Установка</span><span class="sxs-lookup"><span data-stu-id="de267-137">Installation</span></span>
<span data-ttu-id="de267-138">Расширения агента SQL Server IaaS Hello устанавливается автоматически при подготовке образов коллекции виртуальных машин SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="de267-138">hello SQL Server IaaS Agent Extension is automatically installed when you provision one of hello SQL Server virtual machine gallery images.</span></span> <span data-ttu-id="de267-139">Если расширение hello tooreinstall вручную на одном из этих виртуальных машин SQL Server требуется, используйте следующую команду PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="de267-139">If you need tooreinstall hello extension manually on one of these SQL Server VMs, use hello following PowerShell command:</span></span>

```powershell
Set-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension" -Version "1.2" -Location "East US 2"
```

<span data-ttu-id="de267-140">Это также возможно tooinstall hello расширения агента IaaS SQL Server на виртуальной машине только для ОС Windows Server.</span><span class="sxs-lookup"><span data-stu-id="de267-140">It is also possible tooinstall hello SQL Server IaaS Agent Extension on an OS-only Windows Server virtual machine.</span></span> <span data-ttu-id="de267-141">Это возможно, если вы вручную установили SQL Server на этом компьютере.</span><span class="sxs-lookup"><span data-stu-id="de267-141">This is only supported if you have also manually installed SQL Server on that machine.</span></span> <span data-ttu-id="de267-142">А затем установить расширение hello вручную с помощью hello же **AzureVMSqlServerExtension набор** командлета PowerShell.</span><span class="sxs-lookup"><span data-stu-id="de267-142">Then install hello extension manually by using hello same **Set-AzureVMSqlServerExtension** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="de267-143">При установке вручную hello расширения агента IaaS SQL Server на виртуальной Машине Windows Server только для операционной системы, вы можете управлять не hello параметров конфигурации SQL Server через портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="de267-143">If you manually install hello SQL Server IaaS Agent Extension on an OS-only Windows Server VM, you can not manage hello SQL Server configuration settings through hello Azure portal.</span></span> <span data-ttu-id="de267-144">В этом случае все изменения нужно вносить с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="de267-144">In this scenario, you must make all changes with PowerShell.</span></span>

## <a name="status"></a><span data-ttu-id="de267-145">Состояние</span><span class="sxs-lookup"><span data-stu-id="de267-145">Status</span></span>
<span data-ttu-id="de267-146">Одним из способов tooverify, что расширение hello установлено — состояние агента hello tooview hello портала Azure.</span><span class="sxs-lookup"><span data-stu-id="de267-146">One way tooverify that hello extension is installed is tooview hello agent status in hello Azure Portal.</span></span> <span data-ttu-id="de267-147">Выберите **все параметры** в hello колонке виртуальной машины и выберите команду **расширения**.</span><span class="sxs-lookup"><span data-stu-id="de267-147">Select **All settings** in hello virtual machine blade, and then click on **Extensions**.</span></span> <span data-ttu-id="de267-148">Вы увидите hello **SQLIaaSExtension** расширение.</span><span class="sxs-lookup"><span data-stu-id="de267-148">You should see hello **SQLIaaSExtension** extension listed.</span></span>

![Расширение агента IaaS для SQL Server на портале Azure](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-portal.png)

<span data-ttu-id="de267-150">Можно также использовать hello **Get AzureVMSqlServerExtension** командлет Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="de267-150">You can also use hello **Get-AzureVMSqlServerExtension** Azure Powershell cmdlet.</span></span>

    Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"

<span data-ttu-id="de267-151">Предыдущая команда Hello подтверждает hello агент установлен и предоставляет общие сведения о состоянии сведения.</span><span class="sxs-lookup"><span data-stu-id="de267-151">hello previous command confirms hello agent is installed and provides general status information.</span></span> <span data-ttu-id="de267-152">Также можно получить сведения о состоянии автоматического резервного копирования и исправления с hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="de267-152">You can also get specific status information about Automated Backup and Patching with hello following commands.</span></span>

    $sqlext = Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"
    $sqlext.AutoPatchingSettings
    $sqlext.AutoBackupSettings

## <a name="removal"></a><span data-ttu-id="de267-153">Удаление</span><span class="sxs-lookup"><span data-stu-id="de267-153">Removal</span></span>
<span data-ttu-id="de267-154">В hello портал Azure, можно удалить расширение hello, нажав кнопку многоточия hello hello **расширения** колонку свойств виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="de267-154">In hello Azure Portal, you can uninstall hello extension by clicking hello ellipsis on hello **Extensions** blade of your virtual machine properties.</span></span> <span data-ttu-id="de267-155">Затем щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="de267-155">Then click **Delete**.</span></span>

![Удаление hello расширения агента IaaS SQL Server на портале Azure](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-uninstall.png)

<span data-ttu-id="de267-157">Можно также использовать hello **AzureRmVMSqlServerExtension удаление** командлета Powershell.</span><span class="sxs-lookup"><span data-stu-id="de267-157">You can also use hello **Remove-AzureRmVMSqlServerExtension** Powershell cmdlet.</span></span>

    Remove-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension"

## <a name="next-steps"></a><span data-ttu-id="de267-158">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="de267-158">Next Steps</span></span>
<span data-ttu-id="de267-159">Начать использовать одну из служб hello, поддерживаемого расширением hello.</span><span class="sxs-lookup"><span data-stu-id="de267-159">Begin using one of hello services supported by hello extension.</span></span> <span data-ttu-id="de267-160">Дополнительные сведения см. в разделе hello разделы, на которые ссылается hello [поддерживается служб](#supported-services) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="de267-160">For more details, see hello topics referenced in hello [Supported services](#supported-services) section of this article.</span></span>

<span data-ttu-id="de267-161">Подробные сведения о работе SQL Server на виртуальных машинах Azure см. в разделе [Общие сведения об SQL Server на виртуальных машинах Azure](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="de267-161">For more information about running SQL Server on Azure Virtual Machines, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

