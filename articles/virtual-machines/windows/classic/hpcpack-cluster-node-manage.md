---
title: "кластер HPC Pack aaaManage вычислительных узлов | Документы Microsoft"
description: "Дополнительные сведения о tooadd средства сценария PowerShell, удаление, запуск и остановка узлов вычислительного кластера HPC Pack 2012 R2 в Azure"
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
ms.openlocfilehash: 5ac1142cc5da984020779434fbb7cba5ad7c14bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-number-and-availability-of-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="11085-103">Управление числом hello и доступностью вычислительных узлов в кластере HPC Pack в Azure</span><span class="sxs-lookup"><span data-stu-id="11085-103">Manage hello number and availability of compute nodes in an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="11085-104">При создании кластера HPC Pack 2012 R2 в виртуальных машинах Azure, может понадобиться способов tooeasily добавления, удаления, запускать (подготавливать) или некоторые остановку (отзыв) виртуальных машин вычислительных узлов в кластере.</span><span class="sxs-lookup"><span data-stu-id="11085-104">If you created an HPC Pack 2012 R2 cluster in Azure VMs, you might want ways tooeasily add, remove, start (provision), or stop (deprovision) some compute node VMs in the cluster.</span></span> <span data-ttu-id="11085-105">toodo эти задачи выполняются скрипты Azure PowerShell, которые установлены на ВМ головного узла hello.</span><span class="sxs-lookup"><span data-stu-id="11085-105">toodo these tasks, run Azure PowerShell scripts that are installed on hello head node VM.</span></span> <span data-ttu-id="11085-106">Эти скрипты помогают контролировать количество hello и доступности ресурсов кластера HPC Pack, благодаря чему можно контролировать затраты.</span><span class="sxs-lookup"><span data-stu-id="11085-106">These scripts help you control hello number and availability of your HPC Pack cluster resources so you can control costs.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="11085-107">Эта статья относится tooHPC кластеры Pack 2012 R2 в Azure, созданные с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="11085-107">This article applies only tooHPC Pack 2012 R2 clusters in Azure created using hello classic deployment model.</span></span> <span data-ttu-id="11085-108">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="11085-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> <span data-ttu-id="11085-109">Кроме того в HPC Pack 2016 hello сценариев PowerShell, описанных в этой статье недоступны.</span><span class="sxs-lookup"><span data-stu-id="11085-109">In addition, hello PowerShell scripts described in this article are not available in HPC Pack 2016.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="11085-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="11085-110">Prerequisites</span></span>
* <span data-ttu-id="11085-111">**Кластер HPC Pack 2012 R2 в виртуальных машинах Azure**: создать кластер HPC Pack 2012 R2 в hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="11085-111">**HPC Pack 2012 R2 cluster in Azure VMs**: Create an HPC Pack 2012 R2 cluster in hello classic deployment model.</span></span> <span data-ttu-id="11085-112">Например можно автоматизировать развертывание hello, используя образ hello HPC Pack 2012 R2 ВМ в Azure Marketplace hello и скрипт Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="11085-112">For example, you can automate hello deployment by using hello HPC Pack 2012 R2 VM image in hello Azure Marketplace and an Azure PowerShell script.</span></span> <span data-ttu-id="11085-113">Сведения и необходимые условия см. в разделе [создание кластера HPC с помощью скрипта развертывания IaaS пакета HPC hello](hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="11085-113">For information and prerequisites, see [Create an HPC Cluster with hello HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md).</span></span>
  
    <span data-ttu-id="11085-114">После развертывания, найти hello сценарии управления узла в hello % CCP\_ДОМАШНЯЯ папка bin % на головном узле hello.</span><span class="sxs-lookup"><span data-stu-id="11085-114">After deployment, find hello node management scripts in hello %CCP\_HOME%bin folder on hello head node.</span></span> <span data-ttu-id="11085-115">Запустите каждый из скриптов hello с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="11085-115">Run each of hello scripts as an administrator.</span></span>
* <span data-ttu-id="11085-116">**Параметры файла или управления сертификата публикации Azure**: требуется одно из следующих hello toodo на головном узле hello:</span><span class="sxs-lookup"><span data-stu-id="11085-116">**Azure publish settings file or management certificate**: You need toodo one of hello following on hello head node:</span></span>
  
  * <span data-ttu-id="11085-117">**Файл параметров публикации импорта hello Azure**.</span><span class="sxs-lookup"><span data-stu-id="11085-117">**Import hello Azure publish settings file**.</span></span> <span data-ttu-id="11085-118">toodo, выполнения hello следующие командлеты Azure PowerShell на головном узле hello:</span><span class="sxs-lookup"><span data-stu-id="11085-118">toodo this, run hello following Azure PowerShell cmdlets on hello head node:</span></span>
    
    ```PowerShell
    Get-AzurePublishSettingsFile
    
    Import-AzurePublishSettingsFile –PublishSettingsFile <publish settings file>
    ```
  * <span data-ttu-id="11085-119">**Настройка сертификата управления Azure hello на головном узле hello**.</span><span class="sxs-lookup"><span data-stu-id="11085-119">**Configure hello Azure management certificate on hello head node**.</span></span> <span data-ttu-id="11085-120">Если у вас есть hello CER-файл, импортируйте его в хранилище сертификатов CurrentUser\My hello, а затем запустите hello, выполнив командлет Azure PowerShell для среды Azure (облачной или AzureChinaCloud):</span><span class="sxs-lookup"><span data-stu-id="11085-120">If you have hello .cer file, import it in hello CurrentUser\My certificate store and then run hello following Azure PowerShell cmdlet for your Azure environment (either AzureCloud or AzureChinaCloud):</span></span>
    
    ```PowerShell
    Set-AzureSubscription -SubscriptionName <Sub Name> -SubscriptionId <Sub ID> -Certificate (Get-Item Cert:\CurrentUser\My\<Cert Thrumbprint>) -Environment <AzureCloud | AzureChinaCloud>
    ```

## <a name="add-compute-node-vms"></a><span data-ttu-id="11085-121">Добавление виртуальных машин вычислительных узлов</span><span class="sxs-lookup"><span data-stu-id="11085-121">Add compute node VMs</span></span>
<span data-ttu-id="11085-122">Добавление вычислительных узлов с hello **Add-HpcIaaSNode.ps1** сценария.</span><span class="sxs-lookup"><span data-stu-id="11085-122">Add compute nodes with hello **Add-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="11085-123">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="11085-123">Syntax</span></span>
```PowerShell
Add-HPCIaaSNode.ps1 [-ServiceName] <String> [-ImageName] <String>
 [-Quantity] <Int32> [-InstanceSize] <String> [-DomainUserName] <String> [[-DomainUserPassword] <String>]
 [[-NodeNameSeries] <String>] [<CommonParameters>]

```
### <a name="parameters"></a><span data-ttu-id="11085-124">Параметры</span><span class="sxs-lookup"><span data-stu-id="11085-124">Parameters</span></span>
* <span data-ttu-id="11085-125">**ServiceName**: добавляются имя облачной службы hello, новых виртуальных машин вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="11085-125">**ServiceName**: Name of hello cloud service that new compute node VMs are added to.</span></span>
* <span data-ttu-id="11085-126">**ImageName**: имя образа виртуальной Машины Azure, который можно получить с помощью hello классический портал Azure или командлета Azure PowerShell **Get-AzureVMImage**.</span><span class="sxs-lookup"><span data-stu-id="11085-126">**ImageName**: Azure VM image name, which can be obtained through hello Azure classic portal or Azure PowerShell cmdlet **Get-AzureVMImage**.</span></span> <span data-ttu-id="11085-127">изображение Hello должно соответствовать hello следующие требования:</span><span class="sxs-lookup"><span data-stu-id="11085-127">hello image must meet hello following requirements:</span></span>
  
  1. <span data-ttu-id="11085-128">Должна быть установлена операционная система Windows.</span><span class="sxs-lookup"><span data-stu-id="11085-128">A Windows operating system must be installed.</span></span>
  2. <span data-ttu-id="11085-129">Необходимо установить пакет HPC в роли вычислительного узла hello.</span><span class="sxs-lookup"><span data-stu-id="11085-129">HPC Pack must be installed in hello compute node role.</span></span>
  3. <span data-ttu-id="11085-130">Hello изображение должно быть частным образом в категории User hello, а не общедоступным образом ВМ Azure.</span><span class="sxs-lookup"><span data-stu-id="11085-130">hello image must be a private image in hello User category, not a public Azure VM image.</span></span>
* <span data-ttu-id="11085-131">**Количество**: количество вычислительных узлов виртуальных машин toobe добавлен.</span><span class="sxs-lookup"><span data-stu-id="11085-131">**Quantity**: Number of compute node VMs toobe added.</span></span>
* <span data-ttu-id="11085-132">**InstanceSize**: hello размер ВМ вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="11085-132">**InstanceSize**: Size of hello compute node VMs.</span></span>
* <span data-ttu-id="11085-133">**DomainUserName**: имя пользователя домена, которое является toohello домена используется toojoin hello новые виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="11085-133">**DomainUserName**: Domain user name, which is used toojoin hello new VMs toohello domain.</span></span>
* <span data-ttu-id="11085-134">**DomainUserPassword**: пароль пользователя домена hello.</span><span class="sxs-lookup"><span data-stu-id="11085-134">**DomainUserPassword**: Password of hello domain user.</span></span>
* <span data-ttu-id="11085-135">**NodeNameSeries** (необязательно): шаблону именования для hello вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="11085-135">**NodeNameSeries** (optional): Naming pattern for hello compute nodes.</span></span> <span data-ttu-id="11085-136">необходимо использовать формат Hello &lt; *корневой\_имя*&gt;&lt;*запустить\_номер*&gt;%.</span><span class="sxs-lookup"><span data-stu-id="11085-136">hello format must be &lt;*Root\_Name*&gt;&lt;*Start\_Number*&gt;%.</span></span> <span data-ttu-id="11085-137">Например MyCN % 10% означает ряд hello расчет имен узлов, начиная с MyCN11.</span><span class="sxs-lookup"><span data-stu-id="11085-137">For example, MyCN%10% means a series of hello compute node names starting from MyCN11.</span></span> <span data-ttu-id="11085-138">Если не указан, hello скрипт использует hello настроен серия имен узла в кластере HPC hello.</span><span class="sxs-lookup"><span data-stu-id="11085-138">If not specified, hello script uses hello configured node naming series in hello HPC cluster.</span></span>

### <a name="example"></a><span data-ttu-id="11085-139">Пример</span><span class="sxs-lookup"><span data-stu-id="11085-139">Example</span></span>
<span data-ttu-id="11085-140">Hello следующем примере добавляется 20 узлов большого размера виртуальных машин в облачной службе hello *hpcservice1*, основываясь на образ виртуальной Машины hello *ВМ hpccnimage1*.</span><span class="sxs-lookup"><span data-stu-id="11085-140">hello following example adds 20 size Large compute node VMs in hello cloud service *hpcservice1*, based on hello VM image *hpccnimage1*.</span></span>

```PowerShell
Add-HPCIaaSNode.ps1 –ServiceName hpcservice1 –ImageName hpccniamge1
–Quantity 20 –InstanceSize Large –DomainUserName <username>
-DomainUserPassword <password>
```


## <a name="remove-compute-node-vms"></a><span data-ttu-id="11085-141">Удаление виртуальных машин вычислительных узлов</span><span class="sxs-lookup"><span data-stu-id="11085-141">Remove compute node VMs</span></span>
<span data-ttu-id="11085-142">Удаление вычислительных узлов с hello **Remove-HpcIaaSNode.ps1** сценария.</span><span class="sxs-lookup"><span data-stu-id="11085-142">Remove compute nodes with hello **Remove-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="11085-143">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="11085-143">Syntax</span></span>
```PowerShell
Remove-HPCIaaSNode.ps1 -Name <String[]> [-DeleteVHD] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]

Remove-HPCIaaSNode.ps1 -Node <Object> [-DeleteVHD] [-Force] [-Confirm] [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="11085-144">Параметры</span><span class="sxs-lookup"><span data-stu-id="11085-144">Parameters</span></span>
* <span data-ttu-id="11085-145">**Имя**: удалить имена toobe узлов кластера.</span><span class="sxs-lookup"><span data-stu-id="11085-145">**Name**: Names of cluster nodes toobe removed.</span></span> <span data-ttu-id="11085-146">Поддерживаются подстановочные знаки.</span><span class="sxs-lookup"><span data-stu-id="11085-146">Wildcards are supported.</span></span> <span data-ttu-id="11085-147">Имя набора параметров Hello — имя.</span><span class="sxs-lookup"><span data-stu-id="11085-147">hello parameter set name is Name.</span></span> <span data-ttu-id="11085-148">Невозможно указать оба hello **имя** и **узел** параметров.</span><span class="sxs-lookup"><span data-stu-id="11085-148">You can't specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="11085-149">**Узел**: объект HpcNode hello для hello узлы toobe удалены, который может быть получен с помощью командлета HPC PowerShell hello [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span><span class="sxs-lookup"><span data-stu-id="11085-149">**Node**: hello HpcNode object for hello nodes toobe removed, which can be obtained through hello HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="11085-150">Имя набора параметров Hello является узлом.</span><span class="sxs-lookup"><span data-stu-id="11085-150">hello parameter set name is Node.</span></span> <span data-ttu-id="11085-151">Невозможно указать оба hello **имя** и **узел** параметров.</span><span class="sxs-lookup"><span data-stu-id="11085-151">You can't specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="11085-152">**DeleteVHD** (необязательно): Установка toodelete hello связанные диски для hello виртуальных машин, которые будут удалены.</span><span class="sxs-lookup"><span data-stu-id="11085-152">**DeleteVHD** (optional): Setting toodelete hello associated disks for hello VMs that are removed.</span></span>
* <span data-ttu-id="11085-153">**Force** (необязательно): Установка tooforce узлы HPC в автономный режим перед их удалением.</span><span class="sxs-lookup"><span data-stu-id="11085-153">**Force** (optional): Setting tooforce HPC nodes offline before removing them.</span></span>
* <span data-ttu-id="11085-154">**Подтвердите** (необязательно): запрашивать подтверждение перед выполнением команды hello.</span><span class="sxs-lookup"><span data-stu-id="11085-154">**Confirm** (optional): Prompt for confirmation before executing hello command.</span></span>
* <span data-ttu-id="11085-155">**WhatIf**: параметр toodescribe, что произойдет при выполнении команды hello без фактического выполнения команды hello.</span><span class="sxs-lookup"><span data-stu-id="11085-155">**WhatIf**: Setting toodescribe what would happen if you executed hello command without actually executing hello command.</span></span>

### <a name="example"></a><span data-ttu-id="11085-156">Пример</span><span class="sxs-lookup"><span data-stu-id="11085-156">Example</span></span>
<span data-ttu-id="11085-157">Hello следующий пример принудительно устанавливает hello автономные узлы, имена которых начинаются *HPCNode-CN -* и их удаляет узлы hello и связанными дисками.</span><span class="sxs-lookup"><span data-stu-id="11085-157">hello following example forces offline hello nodes with names beginning *HPCNode-CN-* and them removes hello nodes and their associated disks.</span></span>

```PowerShell
Remove-HPCIaaSNode.ps1 –Name HPCNodeCN-* –DeleteVHD -Force
```

## <a name="start-compute-node-vms"></a><span data-ttu-id="11085-158">Запуск виртуальных машин вычислительных узлов</span><span class="sxs-lookup"><span data-stu-id="11085-158">Start compute node VMs</span></span>
<span data-ttu-id="11085-159">Начало вычислительных узлов с hello **Start-HpcIaaSNode.ps1** сценария.</span><span class="sxs-lookup"><span data-stu-id="11085-159">Start compute nodes with hello **Start-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="11085-160">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="11085-160">Syntax</span></span>
```PowerShell
Start-HPCIaaSNode.ps1 -Name <String[]> [<CommonParameters>]

Start-HPCIaaSNode.ps1 -Node <Object> [<CommonParameters>]
```
### <a name="parameters"></a><span data-ttu-id="11085-161">Параметры</span><span class="sxs-lookup"><span data-stu-id="11085-161">Parameters</span></span>
* <span data-ttu-id="11085-162">**Имя**: имена toobe узлы кластера hello работы.</span><span class="sxs-lookup"><span data-stu-id="11085-162">**Name**: Names of hello cluster nodes toobe started.</span></span> <span data-ttu-id="11085-163">Поддерживаются подстановочные знаки.</span><span class="sxs-lookup"><span data-stu-id="11085-163">Wildcards are supported.</span></span> <span data-ttu-id="11085-164">Имя набора параметров Hello — имя.</span><span class="sxs-lookup"><span data-stu-id="11085-164">hello parameter set name is Name.</span></span> <span data-ttu-id="11085-165">Невозможно указать оба hello **имя** и **узел** параметров.</span><span class="sxs-lookup"><span data-stu-id="11085-165">You cannot specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="11085-166">**Узел**-объект HpcNode hello для hello узлы toobe работы, который может быть получен с помощью командлета HPC PowerShell hello [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span><span class="sxs-lookup"><span data-stu-id="11085-166">**Node**- hello HpcNode object for hello nodes toobe started, which can be obtained through hello HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="11085-167">Имя набора параметров Hello является узлом.</span><span class="sxs-lookup"><span data-stu-id="11085-167">hello parameter set name is Node.</span></span> <span data-ttu-id="11085-168">Невозможно указать оба hello **имя** и **узел** параметров.</span><span class="sxs-lookup"><span data-stu-id="11085-168">You cannot specify both hello **Name** and **Node** parameters.</span></span>

### <a name="example"></a><span data-ttu-id="11085-169">Пример</span><span class="sxs-lookup"><span data-stu-id="11085-169">Example</span></span>
<span data-ttu-id="11085-170">Hello следующий пример запускает узлы, имена которых начинаются *HPCNode-CN -*.</span><span class="sxs-lookup"><span data-stu-id="11085-170">hello following example starts nodes with names beginning *HPCNode-CN-*.</span></span>

```PowerShell
Start-HPCIaaSNode.ps1 –Name HPCNodeCN-*
```

## <a name="stop-compute-node-vms"></a><span data-ttu-id="11085-171">Остановка виртуальных машин вычислительных узлов</span><span class="sxs-lookup"><span data-stu-id="11085-171">Stop compute node VMs</span></span>
<span data-ttu-id="11085-172">Остановить вычислительных узлов с hello **Stop-HpcIaaSNode.ps1** сценария.</span><span class="sxs-lookup"><span data-stu-id="11085-172">Stop compute nodes with hello **Stop-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="11085-173">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="11085-173">Syntax</span></span>
```PowerShell
Stop-HPCIaaSNode.ps1 -Name <String[]> [-Force] [<CommonParameters>]

Stop-HPCIaaSNode.ps1 -Node <Object> [-Force] [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="11085-174">Параметры</span><span class="sxs-lookup"><span data-stu-id="11085-174">Parameters</span></span>
* <span data-ttu-id="11085-175">**Имя**-имена toobe узлы кластера hello остановлена.</span><span class="sxs-lookup"><span data-stu-id="11085-175">**Name**- Names of hello cluster nodes toobe stopped.</span></span> <span data-ttu-id="11085-176">Поддерживаются подстановочные знаки.</span><span class="sxs-lookup"><span data-stu-id="11085-176">Wildcards are supported.</span></span> <span data-ttu-id="11085-177">Имя набора параметров Hello — имя.</span><span class="sxs-lookup"><span data-stu-id="11085-177">hello parameter set name is Name.</span></span> <span data-ttu-id="11085-178">Невозможно указать оба hello **имя** и **узел** параметров.</span><span class="sxs-lookup"><span data-stu-id="11085-178">You cannot specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="11085-179">**Узел**: объект HpcNode hello для toobe узлов hello остановлена, который может быть получен с помощью командлета HPC PowerShell hello [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span><span class="sxs-lookup"><span data-stu-id="11085-179">**Node**: hello HpcNode object for hello nodes toobe stopped, which can be obtained through hello HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="11085-180">Имя набора параметров Hello является узлом.</span><span class="sxs-lookup"><span data-stu-id="11085-180">hello parameter set name is Node.</span></span> <span data-ttu-id="11085-181">Невозможно указать оба hello **имя** и **узел** параметров.</span><span class="sxs-lookup"><span data-stu-id="11085-181">You cannot specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="11085-182">**Force** (необязательно): Установка tooforce узлы HPC в автономный режим перед их остановкой.</span><span class="sxs-lookup"><span data-stu-id="11085-182">**Force** (optional): Setting tooforce HPC nodes offline before stopping them.</span></span>

### <a name="example"></a><span data-ttu-id="11085-183">Пример</span><span class="sxs-lookup"><span data-stu-id="11085-183">Example</span></span>
<span data-ttu-id="11085-184">Hello следующий пример принудительно устанавливает узлы, имена которых начинаются *HPCNode-CN -* и затем останавливается hello узлов.</span><span class="sxs-lookup"><span data-stu-id="11085-184">hello following example forces offline nodes with names beginning *HPCNode-CN-* and then stops hello nodes.</span></span>

```PowerShell
Stop-HPCIaaSNode.ps1 –Name HPCNodeCN-* -Force
```

## <a name="next-steps"></a><span data-ttu-id="11085-185">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="11085-185">Next steps</span></span>
* <span data-ttu-id="11085-186">tooautomatically увеличения или сжатия hello узлы кластера в соответствии с текущей рабочей нагрузкой заданий и задач в кластере hello hello см. в разделе [автоматически увеличиваться и уменьшаться hello ресурсы кластера HPC Pack в Azure соответствующим toohello рабочая нагрузка кластера](hpcpack-cluster-node-autogrowshrink.md).</span><span class="sxs-lookup"><span data-stu-id="11085-186">tooautomatically grow or shrink hello cluster nodes according to hello current workload of jobs and tasks on hello cluster, see [Automatically grow and shrink hello HPC Pack cluster resources in Azure according toohello cluster workload](hpcpack-cluster-node-autogrowshrink.md).</span></span>

