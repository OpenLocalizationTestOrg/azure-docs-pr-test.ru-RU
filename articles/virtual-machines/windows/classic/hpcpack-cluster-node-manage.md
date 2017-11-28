---
title: "Управление вычислительными узлами кластера пакета HPC | Документация Майкрософт"
description: "Узнайте о сценариях PowerShell для добавления, удаления, запуска и остановки вычислительных узлов кластера пакета HPC 2012 R2 в Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 4193f03b-94e9-4704-a7ad-379abde063a9
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: dc9f354191b9e80ff6a01bd401a874c6998bda79
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-the-number-and-availability-of-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="1d49d-103">Управление числом и доступностью вычислительных узлов в кластере пакета HPC в Azure</span><span class="sxs-lookup"><span data-stu-id="1d49d-103">Manage the number and availability of compute nodes in an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="1d49d-104">Если вы создали кластер пакета HPC 2012 R2 на виртуальных машинах Azure, вам может потребоваться простой способ добавления, удаления, запуска (подготовки) или остановки (отзыва) нескольких виртуальных машин вычислительных узлов в кластере.</span><span class="sxs-lookup"><span data-stu-id="1d49d-104">If you created an HPC Pack 2012 R2 cluster in Azure VMs, you might want ways to easily add, remove, start (provision), or stop (deprovision) some compute node VMs in the cluster.</span></span> <span data-ttu-id="1d49d-105">Для выполнения этих задач запустите сценарии Azure PowerShell, которые установлены на виртуальной машине головного узла.</span><span class="sxs-lookup"><span data-stu-id="1d49d-105">To do these tasks, run Azure PowerShell scripts that are installed on the head node VM.</span></span> <span data-ttu-id="1d49d-106">Эти сценарии позволяют контролировать количество и доступность ресурсов кластера пакета HPC, а также затраты на них.</span><span class="sxs-lookup"><span data-stu-id="1d49d-106">These scripts help you control the number and availability of your HPC Pack cluster resources so you can control costs.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="1d49d-107">Эта статья относится только к кластерам пакета HPC 2012 R2 в Azure, созданным с помощью классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="1d49d-107">This article applies only to HPC Pack 2012 R2 clusters in Azure created using the classic deployment model.</span></span> <span data-ttu-id="1d49d-108">Для большинства новых развертываний Майкрософт рекомендует использовать модель диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="1d49d-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>
> <span data-ttu-id="1d49d-109">Кроме того, сценарии PowerShell, описанные в этой статье, недоступны в пакете HPC 2016.</span><span class="sxs-lookup"><span data-stu-id="1d49d-109">In addition, the PowerShell scripts described in this article are not available in HPC Pack 2016.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1d49d-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1d49d-110">Prerequisites</span></span>
* <span data-ttu-id="1d49d-111">**Кластер пакета HPC 2012 R2 на виртуальных машинах Azure.** Создайте кластер пакета HPC 2012 R2 в классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="1d49d-111">**HPC Pack 2012 R2 cluster in Azure VMs**: Create an HPC Pack 2012 R2 cluster in the classic deployment model.</span></span> <span data-ttu-id="1d49d-112">Например, можно автоматизировать развертывание с помощью образа виртуальной машины пакета HPC 2012 R2 в Azure Marketplace и сценария Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1d49d-112">For example, you can automate the deployment by using the HPC Pack 2012 R2 VM image in the Azure Marketplace and an Azure PowerShell script.</span></span> <span data-ttu-id="1d49d-113">Дополнительные сведения и описание необходимых компонентов см. в статье [Создание кластера HPC с помощью сценария развертывания IaaS пакета HPC](hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="1d49d-113">For information and prerequisites, see [Create an HPC Cluster with the HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md).</span></span>
  
    <span data-ttu-id="1d49d-114">После развертывания найдите сценарии управления узлом в папке %CCP\_HOME%bin на головном узле.</span><span class="sxs-lookup"><span data-stu-id="1d49d-114">After deployment, find the node management scripts in the %CCP\_HOME%bin folder on the head node.</span></span> <span data-ttu-id="1d49d-115">Каждый из сценариев следует запускать от имени администратора:</span><span class="sxs-lookup"><span data-stu-id="1d49d-115">Run each of the scripts as an administrator.</span></span>
* <span data-ttu-id="1d49d-116">**Файл параметров публикации или сертификат управления Azure.** На головном узле необходимо выполнить одно из следующих действий:</span><span class="sxs-lookup"><span data-stu-id="1d49d-116">**Azure publish settings file or management certificate**: You need to do one of the following on the head node:</span></span>
  
  * <span data-ttu-id="1d49d-117">**Импортируйте файл параметров публикации Azure**.</span><span class="sxs-lookup"><span data-stu-id="1d49d-117">**Import the Azure publish settings file**.</span></span> <span data-ttu-id="1d49d-118">Чтобы сделать это, запустите на головном узле следующие командлеты Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="1d49d-118">To do this, run the following Azure PowerShell cmdlets on the head node:</span></span>
    
    ```PowerShell
    Get-AzurePublishSettingsFile
    
    Import-AzurePublishSettingsFile –PublishSettingsFile <publish settings file>
    ```
  * <span data-ttu-id="1d49d-119">**Настройте сертификат управления Azure на головном узле**.</span><span class="sxs-lookup"><span data-stu-id="1d49d-119">**Configure the Azure management certificate on the head node**.</span></span> <span data-ttu-id="1d49d-120">При наличии CER-файла импортируйте его в CurrentUser\My certificate store, а затем запустите следующий командлет Azure PowerShell для своей среды Azure (AzureCloud или AzureChinaCloud):</span><span class="sxs-lookup"><span data-stu-id="1d49d-120">If you have the .cer file, import it in the CurrentUser\My certificate store and then run the following Azure PowerShell cmdlet for your Azure environment (either AzureCloud or AzureChinaCloud):</span></span>
    
    ```PowerShell
    Set-AzureSubscription -SubscriptionName <Sub Name> -SubscriptionId <Sub ID> -Certificate (Get-Item Cert:\CurrentUser\My\<Cert Thrumbprint>) -Environment <AzureCloud | AzureChinaCloud>
    ```

## <a name="add-compute-node-vms"></a><span data-ttu-id="1d49d-121">Добавление виртуальных машин вычислительных узлов</span><span class="sxs-lookup"><span data-stu-id="1d49d-121">Add compute node VMs</span></span>
<span data-ttu-id="1d49d-122">Добавьте вычислительные узлы с помощью сценария **Add-HpcIaaSNode.ps1** .</span><span class="sxs-lookup"><span data-stu-id="1d49d-122">Add compute nodes with the **Add-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="1d49d-123">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="1d49d-123">Syntax</span></span>
```PowerShell
Add-HPCIaaSNode.ps1 [-ServiceName] <String> [-ImageName] <String>
 [-Quantity] <Int32> [-InstanceSize] <String> [-DomainUserName] <String> [[-DomainUserPassword] <String>]
 [[-NodeNameSeries] <String>] [<CommonParameters>]

```
### <a name="parameters"></a><span data-ttu-id="1d49d-124">Параметры</span><span class="sxs-lookup"><span data-stu-id="1d49d-124">Parameters</span></span>
* <span data-ttu-id="1d49d-125">**ServiceName** — это имя облачной службы, в которую будут добавляться новые виртуальные машины вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="1d49d-125">**ServiceName**: Name of the cloud service that new compute node VMs are added to.</span></span>
* <span data-ttu-id="1d49d-126">**ImageName** — это имя образа виртуальной машины Azure, который можно получить с помощью классического портала Azure или командлета Azure PowerShell **Get-AzureVMImage**.</span><span class="sxs-lookup"><span data-stu-id="1d49d-126">**ImageName**: Azure VM image name, which can be obtained through the Azure classic portal or Azure PowerShell cmdlet **Get-AzureVMImage**.</span></span> <span data-ttu-id="1d49d-127">Этот образ должен соответствовать следующим требованиям.</span><span class="sxs-lookup"><span data-stu-id="1d49d-127">The image must meet the following requirements:</span></span>
  
  1. <span data-ttu-id="1d49d-128">Должна быть установлена операционная система Windows.</span><span class="sxs-lookup"><span data-stu-id="1d49d-128">A Windows operating system must be installed.</span></span>
  2. <span data-ttu-id="1d49d-129">В роли вычислительного узла должен быть установлен пакет HPC.</span><span class="sxs-lookup"><span data-stu-id="1d49d-129">HPC Pack must be installed in the compute node role.</span></span>
  3. <span data-ttu-id="1d49d-130">Образ должен относится к частным образам из категории пользовательских, а не к общедоступным образам виртуальной машины Azure.</span><span class="sxs-lookup"><span data-stu-id="1d49d-130">The image must be a private image in the User category, not a public Azure VM image.</span></span>
* <span data-ttu-id="1d49d-131">**Quantity** — это число добавляемых виртуальных машин вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="1d49d-131">**Quantity**: Number of compute node VMs to be added.</span></span>
* <span data-ttu-id="1d49d-132">**InstanceSize** — это размер виртуальных машин вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="1d49d-132">**InstanceSize**: Size of the compute node VMs.</span></span>
* <span data-ttu-id="1d49d-133">**DomainUserName** — это имя пользователя домена, которое будет использоваться для присоединения новых виртуальных машин к домену.</span><span class="sxs-lookup"><span data-stu-id="1d49d-133">**DomainUserName**: Domain user name, which is used to join the new VMs to the domain.</span></span>
* <span data-ttu-id="1d49d-134">**DomainUserPassword** — это пароль пользователя домена.</span><span class="sxs-lookup"><span data-stu-id="1d49d-134">**DomainUserPassword**: Password of the domain user.</span></span>
* <span data-ttu-id="1d49d-135">**NodeNameSeries** (необязательно) — это шаблон именования для вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="1d49d-135">**NodeNameSeries** (optional): Naming pattern for the compute nodes.</span></span> <span data-ttu-id="1d49d-136">Требуемый формат: &lt;*Root\_Name*&gt;&lt;*Start\_Number*&gt;%.</span><span class="sxs-lookup"><span data-stu-id="1d49d-136">The format must be &lt;*Root\_Name*&gt;&lt;*Start\_Number*&gt;%.</span></span> <span data-ttu-id="1d49d-137">Например, MyCN%10% означает последовательность имен вычислительных узлов, начинающуюся с MyCN11.</span><span class="sxs-lookup"><span data-stu-id="1d49d-137">For example, MyCN%10% means a series of the compute node names starting from MyCN11.</span></span> <span data-ttu-id="1d49d-138">Если не указано, сценарий использует настроенную последовательность имен узлов в кластере HPC.</span><span class="sxs-lookup"><span data-stu-id="1d49d-138">If not specified, the script uses the configured node naming series in the HPC cluster.</span></span>

### <a name="example"></a><span data-ttu-id="1d49d-139">Пример</span><span class="sxs-lookup"><span data-stu-id="1d49d-139">Example</span></span>
<span data-ttu-id="1d49d-140">В следующем примере 20 виртуальных машин вычислительных узлов большого размера добавляются в облачную службу *hpcservice1* на основе образа виртуальной машины *hpccnimage1*.</span><span class="sxs-lookup"><span data-stu-id="1d49d-140">The following example adds 20 size Large compute node VMs in the cloud service *hpcservice1*, based on the VM image *hpccnimage1*.</span></span>

```PowerShell
Add-HPCIaaSNode.ps1 –ServiceName hpcservice1 –ImageName hpccniamge1
–Quantity 20 –InstanceSize Large –DomainUserName <username>
-DomainUserPassword <password>
```


## <a name="remove-compute-node-vms"></a><span data-ttu-id="1d49d-141">Удаление виртуальных машин вычислительных узлов</span><span class="sxs-lookup"><span data-stu-id="1d49d-141">Remove compute node VMs</span></span>
<span data-ttu-id="1d49d-142">Удалите вычислительные узлы с помощью сценария **Remove-HpcIaaSNode.ps1** .</span><span class="sxs-lookup"><span data-stu-id="1d49d-142">Remove compute nodes with the **Remove-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="1d49d-143">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="1d49d-143">Syntax</span></span>
```PowerShell
Remove-HPCIaaSNode.ps1 -Name <String[]> [-DeleteVHD] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]

Remove-HPCIaaSNode.ps1 -Node <Object> [-DeleteVHD] [-Force] [-Confirm] [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="1d49d-144">Параметры</span><span class="sxs-lookup"><span data-stu-id="1d49d-144">Parameters</span></span>
* <span data-ttu-id="1d49d-145">**Name** — это имена узлов кластера для удаления.</span><span class="sxs-lookup"><span data-stu-id="1d49d-145">**Name**: Names of cluster nodes to be removed.</span></span> <span data-ttu-id="1d49d-146">Поддерживаются подстановочные знаки.</span><span class="sxs-lookup"><span data-stu-id="1d49d-146">Wildcards are supported.</span></span> <span data-ttu-id="1d49d-147">Для параметра задано имя Name.</span><span class="sxs-lookup"><span data-stu-id="1d49d-147">The parameter set name is Name.</span></span> <span data-ttu-id="1d49d-148">Нельзя одновременно задать параметры **Name** и **Node**.</span><span class="sxs-lookup"><span data-stu-id="1d49d-148">You can't specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="1d49d-149">**Node** — это объект HpcNode для удаляемых узлов, который можно получить с помощью командлета PowerShell HPC [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span><span class="sxs-lookup"><span data-stu-id="1d49d-149">**Node**: The HpcNode object for the nodes to be removed, which can be obtained through the HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="1d49d-150">Для параметра задано имя Node.</span><span class="sxs-lookup"><span data-stu-id="1d49d-150">The parameter set name is Node.</span></span> <span data-ttu-id="1d49d-151">Нельзя одновременно задать параметры **Name** и **Node**.</span><span class="sxs-lookup"><span data-stu-id="1d49d-151">You can't specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="1d49d-152">**DeleteVHD** (необязательно) — это параметр удаления связанных дисков для удаляемых виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="1d49d-152">**DeleteVHD** (optional): Setting to delete the associated disks for the VMs that are removed.</span></span>
* <span data-ttu-id="1d49d-153">**Force** (необязательно) — это параметр принудительного отключения узлов HPC перед их удалением.</span><span class="sxs-lookup"><span data-stu-id="1d49d-153">**Force** (optional): Setting to force HPC nodes offline before removing them.</span></span>
* <span data-ttu-id="1d49d-154">**Confirm** (необязательно) — это запрос подтверждения перед выполнением команды.</span><span class="sxs-lookup"><span data-stu-id="1d49d-154">**Confirm** (optional): Prompt for confirmation before executing the command.</span></span>
* <span data-ttu-id="1d49d-155">**WhatIf** — это параметр описания последствий выполнения команды без фактического выполнения этой команды.</span><span class="sxs-lookup"><span data-stu-id="1d49d-155">**WhatIf**: Setting to describe what would happen if you executed the command without actually executing the command.</span></span>

### <a name="example"></a><span data-ttu-id="1d49d-156">Пример</span><span class="sxs-lookup"><span data-stu-id="1d49d-156">Example</span></span>
<span data-ttu-id="1d49d-157">В следующем примере принудительно отключаются узлы, имена которых начинаются с *HPCNode-CN-*, после чего эти узлы и связанные с ними диски удаляются.</span><span class="sxs-lookup"><span data-stu-id="1d49d-157">The following example forces offline the nodes with names beginning *HPCNode-CN-* and them removes the nodes and their associated disks.</span></span>

```PowerShell
Remove-HPCIaaSNode.ps1 –Name HPCNodeCN-* –DeleteVHD -Force
```

## <a name="start-compute-node-vms"></a><span data-ttu-id="1d49d-158">Запуск виртуальных машин вычислительных узлов</span><span class="sxs-lookup"><span data-stu-id="1d49d-158">Start compute node VMs</span></span>
<span data-ttu-id="1d49d-159">Запустите вычислительные узлы с помощью сценария **Start-HpcIaaSNode.ps1** .</span><span class="sxs-lookup"><span data-stu-id="1d49d-159">Start compute nodes with the **Start-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="1d49d-160">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="1d49d-160">Syntax</span></span>
```PowerShell
Start-HPCIaaSNode.ps1 -Name <String[]> [<CommonParameters>]

Start-HPCIaaSNode.ps1 -Node <Object> [<CommonParameters>]
```
### <a name="parameters"></a><span data-ttu-id="1d49d-161">Параметры</span><span class="sxs-lookup"><span data-stu-id="1d49d-161">Parameters</span></span>
* <span data-ttu-id="1d49d-162">**Name** — это имена узлов кластера для запуска.</span><span class="sxs-lookup"><span data-stu-id="1d49d-162">**Name**: Names of the cluster nodes to be started.</span></span> <span data-ttu-id="1d49d-163">Поддерживаются подстановочные знаки.</span><span class="sxs-lookup"><span data-stu-id="1d49d-163">Wildcards are supported.</span></span> <span data-ttu-id="1d49d-164">Для параметра задано имя Name.</span><span class="sxs-lookup"><span data-stu-id="1d49d-164">The parameter set name is Name.</span></span> <span data-ttu-id="1d49d-165">Нельзя одновременно задать параметры **Name** и **Node**.</span><span class="sxs-lookup"><span data-stu-id="1d49d-165">You cannot specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="1d49d-166">**Node**— объект HpcNode для запускаемых узлов, который можно получить с помощью командлета PowerShell HPC [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span><span class="sxs-lookup"><span data-stu-id="1d49d-166">**Node**- The HpcNode object for the nodes to be started, which can be obtained through the HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="1d49d-167">Для параметра задано имя Node.</span><span class="sxs-lookup"><span data-stu-id="1d49d-167">The parameter set name is Node.</span></span> <span data-ttu-id="1d49d-168">Нельзя одновременно задать параметры **Name** и **Node**.</span><span class="sxs-lookup"><span data-stu-id="1d49d-168">You cannot specify both the **Name** and **Node** parameters.</span></span>

### <a name="example"></a><span data-ttu-id="1d49d-169">Пример</span><span class="sxs-lookup"><span data-stu-id="1d49d-169">Example</span></span>
<span data-ttu-id="1d49d-170">В следующем примере запускаются узлы, имена которых начинаются с *HPCNode-CN-*.</span><span class="sxs-lookup"><span data-stu-id="1d49d-170">The following example starts nodes with names beginning *HPCNode-CN-*.</span></span>

```PowerShell
Start-HPCIaaSNode.ps1 –Name HPCNodeCN-*
```

## <a name="stop-compute-node-vms"></a><span data-ttu-id="1d49d-171">Остановка виртуальных машин вычислительных узлов</span><span class="sxs-lookup"><span data-stu-id="1d49d-171">Stop compute node VMs</span></span>
<span data-ttu-id="1d49d-172">Остановите вычислительные узлы с помощью сценария **Stop-HpcIaaSNode.ps1** .</span><span class="sxs-lookup"><span data-stu-id="1d49d-172">Stop compute nodes with the **Stop-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="1d49d-173">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="1d49d-173">Syntax</span></span>
```PowerShell
Stop-HPCIaaSNode.ps1 -Name <String[]> [-Force] [<CommonParameters>]

Stop-HPCIaaSNode.ps1 -Node <Object> [-Force] [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="1d49d-174">Параметры</span><span class="sxs-lookup"><span data-stu-id="1d49d-174">Parameters</span></span>
* <span data-ttu-id="1d49d-175">**Name**— имена узлов кластера для остановки.</span><span class="sxs-lookup"><span data-stu-id="1d49d-175">**Name**- Names of the cluster nodes to be stopped.</span></span> <span data-ttu-id="1d49d-176">Поддерживаются подстановочные знаки.</span><span class="sxs-lookup"><span data-stu-id="1d49d-176">Wildcards are supported.</span></span> <span data-ttu-id="1d49d-177">Для параметра задано имя Name.</span><span class="sxs-lookup"><span data-stu-id="1d49d-177">The parameter set name is Name.</span></span> <span data-ttu-id="1d49d-178">Нельзя одновременно задать параметры **Name** и **Node**.</span><span class="sxs-lookup"><span data-stu-id="1d49d-178">You cannot specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="1d49d-179">**Node** — это объект HpcNode для останавливаемых узлов, который можно получить с помощью командлета PowerShell HPC [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span><span class="sxs-lookup"><span data-stu-id="1d49d-179">**Node**: The HpcNode object for the nodes to be stopped, which can be obtained through the HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="1d49d-180">Для параметра задано имя Node.</span><span class="sxs-lookup"><span data-stu-id="1d49d-180">The parameter set name is Node.</span></span> <span data-ttu-id="1d49d-181">Нельзя одновременно задать параметры **Name** и **Node**.</span><span class="sxs-lookup"><span data-stu-id="1d49d-181">You cannot specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="1d49d-182">**Force** (необязательно) — это параметр принудительного отключения узлов HPC перед их остановкой.</span><span class="sxs-lookup"><span data-stu-id="1d49d-182">**Force** (optional): Setting to force HPC nodes offline before stopping them.</span></span>

### <a name="example"></a><span data-ttu-id="1d49d-183">Пример</span><span class="sxs-lookup"><span data-stu-id="1d49d-183">Example</span></span>
<span data-ttu-id="1d49d-184">В следующем примере принудительно отключаются узлы, имена которых начинаются с *HPCNode-CN-* , после чего эти узлы останавливаются.</span><span class="sxs-lookup"><span data-stu-id="1d49d-184">The following example forces offline nodes with names beginning *HPCNode-CN-* and then stops the nodes.</span></span>

```PowerShell
Stop-HPCIaaSNode.ps1 –Name HPCNodeCN-* -Force
```

## <a name="next-steps"></a><span data-ttu-id="1d49d-185">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1d49d-185">Next steps</span></span>
* <span data-ttu-id="1d49d-186">Если вам требуется, чтобы число узлов кластера автоматически увеличивалось или уменьшалось в соответствии с текущей рабочей нагрузкой заданий и задач в кластере, см. статью [Автоматическое изменение размера ресурсов кластера пакета HPC в Azure в соответствии с рабочей нагрузкой кластера](hpcpack-cluster-node-autogrowshrink.md).</span><span class="sxs-lookup"><span data-stu-id="1d49d-186">To automatically grow or shrink the cluster nodes according to the current workload of jobs and tasks on the cluster, see [Automatically grow and shrink the HPC Pack cluster resources in Azure according to the cluster workload](hpcpack-cluster-node-autogrowshrink.md).</span></span>

