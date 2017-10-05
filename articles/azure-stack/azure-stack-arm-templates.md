---
title: "Использование шаблонов диспетчера ресурсов Azure в стек Azure | Документы Microsoft"
description: "Узнайте, как использовать шаблоны диспетчера ресурсов Azure в стек Azure для подготовки ресурсов."
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
ms.openlocfilehash: 228e641afefd16edc7b405a2fc1d60184ce41e96
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="use-azure-resource-manager-templates-in-azure-stack"></a><span data-ttu-id="e4841-103">Использование шаблонов диспетчера ресурсов Azure в Azure Stack</span><span class="sxs-lookup"><span data-stu-id="e4841-103">Use Azure Resource Manager templates in Azure Stack</span></span>
<span data-ttu-id="e4841-104">Шаблоны диспетчера ресурсов Azure, развертывание и предоставление все ресурсы для приложения в один, согласованной операции.</span><span class="sxs-lookup"><span data-stu-id="e4841-104">Azure Resource Manager templates deploy and provision all the resources for your application in a single, coordinated operation.</span></span> <span data-ttu-id="e4841-105">Кроме того, можно повторно развернуть шаблоны вносить изменения в ресурсы в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e4841-105">You can also redeploy templates to make changes to the resources in the resource group.</span></span>

<span data-ttu-id="e4841-106">Эти шаблоны можно развертывать с помощью портала Microsoft Azure Stack, PowerShell, командной строки и Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e4841-106">These templates can be deployed with the Microsoft Azure Stack portal, PowerShell, the command line, and Visual Studio.</span></span>

<span data-ttu-id="e4841-107">Следующие примеры использования шаблоны доступны для [GitHub](http://aka.ms/azurestackgithub):</span><span class="sxs-lookup"><span data-stu-id="e4841-107">The following quickstart templates are available on [GitHub](http://aka.ms/azurestackgithub):</span></span>

## <a name="deploy-sharepoint-non-high-availability"></a><span data-ttu-id="e4841-108">Развертывание SharePoint (с обычным уровнем доступности)</span><span class="sxs-lookup"><span data-stu-id="e4841-108">Deploy SharePoint (non-high availability)</span></span>
<span data-ttu-id="e4841-109">Используйте расширение PowerShell DSC для создания фермы SharePoint 2013, включает следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="e4841-109">Use the PowerShell DSC extension to create a SharePoint 2013 farm that includes the following resources:</span></span>

* <span data-ttu-id="e4841-110">виртуальную сеть;</span><span class="sxs-lookup"><span data-stu-id="e4841-110">A virtual network</span></span>
* <span data-ttu-id="e4841-111">три учетные записи хранения;</span><span class="sxs-lookup"><span data-stu-id="e4841-111">Three storage accounts</span></span>
* <span data-ttu-id="e4841-112">два внешних балансировщика нагрузки;</span><span class="sxs-lookup"><span data-stu-id="e4841-112">Two external load balancers</span></span>
* <span data-ttu-id="e4841-113">Одна виртуальная машина настроен в качестве контроллера домена для нового леса с одним доменом</span><span class="sxs-lookup"><span data-stu-id="e4841-113">One VM configured as a domain controller for a new forest with a single domain</span></span>
* <span data-ttu-id="e4841-114">одну виртуальную машину, настроенную в качестве изолированного сервера SQL Server 2014;</span><span class="sxs-lookup"><span data-stu-id="e4841-114">One VM configured as a SQL Server 2014 stand-alone server</span></span>
* <span data-ttu-id="e4841-115">одну виртуальную машину, настроенную в качестве фермы SharePoint 2013 с одним компьютером.</span><span class="sxs-lookup"><span data-stu-id="e4841-115">One VM configured as a one machine SharePoint 2013 farm</span></span>

## <a name="deploy-ad-non-high-availability"></a><span data-ttu-id="e4841-116">Развертывание AD (без высокой доступности)</span><span class="sxs-lookup"><span data-stu-id="e4841-116">Deploy AD (non-high availability)</span></span>
<span data-ttu-id="e4841-117">Используйте расширение PowerShell DSC для создания сервера контроллера домена AD, включает следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="e4841-117">Use the PowerShell DSC extension to create an AD domain controller server that includes the following resources:</span></span>

* <span data-ttu-id="e4841-118">виртуальную сеть;</span><span class="sxs-lookup"><span data-stu-id="e4841-118">A virtual network</span></span>
* <span data-ttu-id="e4841-119">одна учетная запись хранения;</span><span class="sxs-lookup"><span data-stu-id="e4841-119">One storage account</span></span>
* <span data-ttu-id="e4841-120">один внешний балансировщик нагрузки;</span><span class="sxs-lookup"><span data-stu-id="e4841-120">One external load balancer</span></span>
* <span data-ttu-id="e4841-121">Одна виртуальная машина настроен в качестве контроллера домена для нового леса с одним доменом</span><span class="sxs-lookup"><span data-stu-id="e4841-121">One VM configured as a domain controller for a new forest with a single domain</span></span>

## <a name="deploy-adsql-non-high-availability"></a><span data-ttu-id="e4841-122">Развертывание AD или SQL (с обычным уровнем доступности)</span><span class="sxs-lookup"><span data-stu-id="e4841-122">Deploy AD/SQL (non-high availability)</span></span>
<span data-ttu-id="e4841-123">Используйте расширение PowerShell DSC для создания изолированного сервера SQL Server 2014, включает следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="e4841-123">Use the PowerShell DSC extension to create a SQL Server 2014 stand-alone server that includes the following resources:</span></span>

* <span data-ttu-id="e4841-124">виртуальную сеть;</span><span class="sxs-lookup"><span data-stu-id="e4841-124">A virtual network</span></span>
* <span data-ttu-id="e4841-125">две учетные записи хранения;</span><span class="sxs-lookup"><span data-stu-id="e4841-125">Two storage accounts</span></span>
* <span data-ttu-id="e4841-126">один внешний балансировщик нагрузки;</span><span class="sxs-lookup"><span data-stu-id="e4841-126">One external load balancer</span></span>
* <span data-ttu-id="e4841-127">Одна виртуальная машина настроен в качестве контроллера домена для нового леса с одним доменом</span><span class="sxs-lookup"><span data-stu-id="e4841-127">One VM configured as a domain controller for a new forest with a single domain</span></span>
* <span data-ttu-id="e4841-128">одну виртуальную машину, настроенную в качестве изолированного сервера SQL Server 2014;</span><span class="sxs-lookup"><span data-stu-id="e4841-128">One VM configured as a SQL Server 2014 stand-alone server</span></span>

## <a name="vm-dsc-extension-azure-automation-pull-server"></a><span data-ttu-id="e4841-129">VM-DSC-Extension-Azure-Automation-Pull-Server</span><span class="sxs-lookup"><span data-stu-id="e4841-129">VM-DSC-Extension-Azure-Automation-Pull-Server</span></span>
<span data-ttu-id="e4841-130">Используйте расширение PowerShell DSC, чтобы настроить локальный диспетчер конфигурации (LCM) существующей виртуальной машины и зарегистрировать ее на опрашивающем сервере DSC учетных записей службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="e4841-130">Use the PowerShell DSC extension to configure an existing virtual machine Local Configuration Manager (LCM) and register it to an Azure Automation Account DSC Pull Server.</span></span>

## <a name="create-a-virtual-machine-from-a-user-image"></a><span data-ttu-id="e4841-131">Создание виртуальной машины из пользовательского образа</span><span class="sxs-lookup"><span data-stu-id="e4841-131">Create a virtual machine from a user image</span></span>
<span data-ttu-id="e4841-132">Можно создать виртуальную машину из настраиваемого пользовательского образа.</span><span class="sxs-lookup"><span data-stu-id="e4841-132">Create a virtual machine from a custom user image.</span></span> <span data-ttu-id="e4841-133">Этот шаблон также развертывает виртуальную сеть (с DNS), общедоступный IP-адрес и сетевой интерфейс.</span><span class="sxs-lookup"><span data-stu-id="e4841-133">This template also deploys a virtual network (with DNS), public IP address, and a network interface.</span></span>

## <a name="simple-vm"></a><span data-ttu-id="e4841-134">Простая виртуальная машина</span><span class="sxs-lookup"><span data-stu-id="e4841-134">Simple VM</span></span>
<span data-ttu-id="e4841-135">Развертывание Windows виртуальной Машины, включающий виртуальной сети (с помощью DNS), общедоступный IP-адрес и сетевого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e4841-135">Deploy a Windows VM that includes a virtual network (with DNS), public IP address, and a network interface.</span></span>

## <a name="cancel-a-running-template-deployment"></a><span data-ttu-id="e4841-136">Отмена выполняющегося развертывания шаблона</span><span class="sxs-lookup"><span data-stu-id="e4841-136">Cancel a running template deployment</span></span>
<span data-ttu-id="e4841-137">Чтобы отменить выполнение шаблона-развертывания, используйте `Stop-AzureRmResourceGroupDeployment` командлета PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e4841-137">To cancel a running template deployment, use the `Stop-AzureRmResourceGroupDeployment` PowerShell cmdlet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4841-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e4841-138">Next steps</span></span>
[<span data-ttu-id="e4841-139">Развертывание шаблонов с помощью портала</span><span class="sxs-lookup"><span data-stu-id="e4841-139">Deploy templates with the portal</span></span>](azure-stack-deploy-template-portal.md)

[<span data-ttu-id="e4841-140">Общие сведения об Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e4841-140">Azure Resource Manager overview</span></span>](../azure-resource-manager/resource-group-overview.md)

