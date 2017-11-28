---
title: "шаблоны Azure Resource Manager aaaUse стека Azure | Документы Microsoft"
description: "Узнайте, как шаблоны Azure Resource Manager toouse в стек Azure tooprovision ресурсы."
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: 2022dbe5-47fd-457d-9af3-6c01688171d7
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: bcc73756fa712ecff9791301d43d227112be8362
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-resource-manager-templates-in-azure-stack"></a><span data-ttu-id="692ab-103">Использование шаблонов диспетчера ресурсов Azure в Azure Stack</span><span class="sxs-lookup"><span data-stu-id="692ab-103">Use Azure Resource Manager templates in Azure Stack</span></span>
<span data-ttu-id="692ab-104">Шаблоны диспетчера ресурсов Azure, развертывание и предоставление всех hello ресурсы для приложения в один, согласованной операции.</span><span class="sxs-lookup"><span data-stu-id="692ab-104">Azure Resource Manager templates deploy and provision all hello resources for your application in a single, coordinated operation.</span></span> <span data-ttu-id="692ab-105">Кроме того, можно повторно развернуть шаблоны toomake изменения toohello ресурсы в группе ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="692ab-105">You can also redeploy templates toomake changes toohello resources in hello resource group.</span></span>

<span data-ttu-id="692ab-106">Эти шаблоны можно развернуть с помощью портала hello стека Microsoft Azure, PowerShell, Командная строка hello и Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="692ab-106">These templates can be deployed with hello Microsoft Azure Stack portal, PowerShell, hello command line, and Visual Studio.</span></span>

<span data-ttu-id="692ab-107">Следующие примеры использования шаблонов Hello доступны на [GitHub](http://aka.ms/azurestackgithub):</span><span class="sxs-lookup"><span data-stu-id="692ab-107">hello following quickstart templates are available on [GitHub](http://aka.ms/azurestackgithub):</span></span>

## <a name="deploy-sharepoint-non-high-availability"></a><span data-ttu-id="692ab-108">Развертывание SharePoint (с обычным уровнем доступности)</span><span class="sxs-lookup"><span data-stu-id="692ab-108">Deploy SharePoint (non-high availability)</span></span>
<span data-ttu-id="692ab-109">Используйте для hello PowerShell DSC расширения toocreate SharePoint 2013 фермы, включающей hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="692ab-109">Use hello PowerShell DSC extension toocreate a SharePoint 2013 farm that includes hello following resources:</span></span>

* <span data-ttu-id="692ab-110">виртуальную сеть;</span><span class="sxs-lookup"><span data-stu-id="692ab-110">A virtual network</span></span>
* <span data-ttu-id="692ab-111">три учетные записи хранения;</span><span class="sxs-lookup"><span data-stu-id="692ab-111">Three storage accounts</span></span>
* <span data-ttu-id="692ab-112">два внешних балансировщика нагрузки;</span><span class="sxs-lookup"><span data-stu-id="692ab-112">Two external load balancers</span></span>
* <span data-ttu-id="692ab-113">Одна виртуальная машина настроен в качестве контроллера домена для нового леса с одним доменом</span><span class="sxs-lookup"><span data-stu-id="692ab-113">One VM configured as a domain controller for a new forest with a single domain</span></span>
* <span data-ttu-id="692ab-114">одну виртуальную машину, настроенную в качестве изолированного сервера SQL Server 2014;</span><span class="sxs-lookup"><span data-stu-id="692ab-114">One VM configured as a SQL Server 2014 stand-alone server</span></span>
* <span data-ttu-id="692ab-115">одну виртуальную машину, настроенную в качестве фермы SharePoint 2013 с одним компьютером.</span><span class="sxs-lookup"><span data-stu-id="692ab-115">One VM configured as a one machine SharePoint 2013 farm</span></span>

## <a name="deploy-ad-non-high-availability"></a><span data-ttu-id="692ab-116">Развертывание AD (без высокой доступности)</span><span class="sxs-lookup"><span data-stu-id="692ab-116">Deploy AD (non-high availability)</span></span>
<span data-ttu-id="692ab-117">Используйте toocreate расширение PowerShell DSC hello адрес сервера контроллера домена AD, включающий hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="692ab-117">Use hello PowerShell DSC extension toocreate an AD domain controller server that includes hello following resources:</span></span>

* <span data-ttu-id="692ab-118">виртуальную сеть;</span><span class="sxs-lookup"><span data-stu-id="692ab-118">A virtual network</span></span>
* <span data-ttu-id="692ab-119">одна учетная запись хранения;</span><span class="sxs-lookup"><span data-stu-id="692ab-119">One storage account</span></span>
* <span data-ttu-id="692ab-120">один внешний балансировщик нагрузки;</span><span class="sxs-lookup"><span data-stu-id="692ab-120">One external load balancer</span></span>
* <span data-ttu-id="692ab-121">Одна виртуальная машина настроен в качестве контроллера домена для нового леса с одним доменом</span><span class="sxs-lookup"><span data-stu-id="692ab-121">One VM configured as a domain controller for a new forest with a single domain</span></span>

## <a name="deploy-adsql-non-high-availability"></a><span data-ttu-id="692ab-122">Развертывание AD или SQL (с обычным уровнем доступности)</span><span class="sxs-lookup"><span data-stu-id="692ab-122">Deploy AD/SQL (non-high availability)</span></span>
<span data-ttu-id="692ab-123">Используйте hello PowerShell DSC расширения toocreate SQL Server 2014 изолированного сервера, включая hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="692ab-123">Use hello PowerShell DSC extension toocreate a SQL Server 2014 stand-alone server that includes hello following resources:</span></span>

* <span data-ttu-id="692ab-124">виртуальную сеть;</span><span class="sxs-lookup"><span data-stu-id="692ab-124">A virtual network</span></span>
* <span data-ttu-id="692ab-125">две учетные записи хранения;</span><span class="sxs-lookup"><span data-stu-id="692ab-125">Two storage accounts</span></span>
* <span data-ttu-id="692ab-126">один внешний балансировщик нагрузки;</span><span class="sxs-lookup"><span data-stu-id="692ab-126">One external load balancer</span></span>
* <span data-ttu-id="692ab-127">Одна виртуальная машина настроен в качестве контроллера домена для нового леса с одним доменом</span><span class="sxs-lookup"><span data-stu-id="692ab-127">One VM configured as a domain controller for a new forest with a single domain</span></span>
* <span data-ttu-id="692ab-128">одну виртуальную машину, настроенную в качестве изолированного сервера SQL Server 2014;</span><span class="sxs-lookup"><span data-stu-id="692ab-128">One VM configured as a SQL Server 2014 stand-alone server</span></span>

## <a name="vm-dsc-extension-azure-automation-pull-server"></a><span data-ttu-id="692ab-129">VM-DSC-Extension-Azure-Automation-Pull-Server</span><span class="sxs-lookup"><span data-stu-id="692ab-129">VM-DSC-Extension-Azure-Automation-Pull-Server</span></span>
<span data-ttu-id="692ab-130">Использовать tooconfigure расширение PowerShell DSC hello существующая виртуальная машина локальный диспетчер конфигураций (LCM) и зарегистрируйте его tooan Azure Automation учетной записи DSC опрашивающего сервера.</span><span class="sxs-lookup"><span data-stu-id="692ab-130">Use hello PowerShell DSC extension tooconfigure an existing virtual machine Local Configuration Manager (LCM) and register it tooan Azure Automation Account DSC Pull Server.</span></span>

## <a name="create-a-virtual-machine-from-a-user-image"></a><span data-ttu-id="692ab-131">Создание виртуальной машины из пользовательского образа</span><span class="sxs-lookup"><span data-stu-id="692ab-131">Create a virtual machine from a user image</span></span>
<span data-ttu-id="692ab-132">Можно создать виртуальную машину из настраиваемого пользовательского образа.</span><span class="sxs-lookup"><span data-stu-id="692ab-132">Create a virtual machine from a custom user image.</span></span> <span data-ttu-id="692ab-133">Этот шаблон также развертывает виртуальную сеть (с DNS), общедоступный IP-адрес и сетевой интерфейс.</span><span class="sxs-lookup"><span data-stu-id="692ab-133">This template also deploys a virtual network (with DNS), public IP address, and a network interface.</span></span>

## <a name="simple-vm"></a><span data-ttu-id="692ab-134">Простая виртуальная машина</span><span class="sxs-lookup"><span data-stu-id="692ab-134">Simple VM</span></span>
<span data-ttu-id="692ab-135">Развертывание Windows виртуальной Машины, включающий виртуальной сети (с помощью DNS), общедоступный IP-адрес и сетевого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="692ab-135">Deploy a Windows VM that includes a virtual network (with DNS), public IP address, and a network interface.</span></span>

## <a name="cancel-a-running-template-deployment"></a><span data-ttu-id="692ab-136">Отмена выполняющегося развертывания шаблона</span><span class="sxs-lookup"><span data-stu-id="692ab-136">Cancel a running template deployment</span></span>
<span data-ttu-id="692ab-137">использовать toocancel в выполняющееся развертывание шаблона hello `Stop-AzureRmResourceGroupDeployment` командлета PowerShell.</span><span class="sxs-lookup"><span data-stu-id="692ab-137">toocancel a running template deployment, use hello `Stop-AzureRmResourceGroupDeployment` PowerShell cmdlet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="692ab-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="692ab-138">Next steps</span></span>
[<span data-ttu-id="692ab-139">Развертывание шаблонов с портала hello</span><span class="sxs-lookup"><span data-stu-id="692ab-139">Deploy templates with hello portal</span></span>](azure-stack-deploy-template-portal.md)

[<span data-ttu-id="692ab-140">Общие сведения об Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="692ab-140">Azure Resource Manager overview</span></span>](../azure-resource-manager/resource-group-overview.md)

