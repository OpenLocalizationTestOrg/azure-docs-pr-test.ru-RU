---
title: "aaaMove ресурс виртуальной Машины Windows в Azure | Документы Microsoft"
description: "Переместите tooanother виртуальной Машины Windows Azure подписка или группа ресурсов в модели развертывания диспетчера ресурсов hello."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4e383427-4aff-4bf3-a0f4-dbff5c6f0c81
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 859e78dce9acf1168780d4ee8e9f6dac0e3c11cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-windows-vm-tooanother-azure-subscription-or-resource-group"></a><span data-ttu-id="d0325-103">Перемещение виртуальной Машины Windows tooanother подписки Azure или группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="d0325-103">Move a Windows VM tooanother Azure subscription or resource group</span></span>
<span data-ttu-id="d0325-104">В этой статье описано, как toomove ВМ Windows между группами ресурсов или подписок.</span><span class="sxs-lookup"><span data-stu-id="d0325-104">This article walks you through how toomove a Windows VM between resource groups or subscriptions.</span></span> <span data-ttu-id="d0325-105">Перемещение между подписками может оказаться удобным, которые использовались при создании виртуальной Машины в личные подписки, а теперь нужно toomove его toocontinue подписки компании tooyour свою работу.</span><span class="sxs-lookup"><span data-stu-id="d0325-105">Moving between subscriptions can be handy if you originally created a VM in a personal subscription and now want toomove it tooyour company's subscription toocontinue your work.</span></span>

> [!IMPORTANT]
><span data-ttu-id="d0325-106">В настоящее время переместить управляемые диски невозможно.</span><span class="sxs-lookup"><span data-stu-id="d0325-106">You cannot move Managed Disks at this time.</span></span> 
>
><span data-ttu-id="d0325-107">В процессе перемещения hello создаются новые идентификаторы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d0325-107">New resource IDs are created as part of hello move.</span></span> <span data-ttu-id="d0325-108">После hello ВМ был перемещен, вам потребуется tooupdate вашей средства и сценарии toouse hello новые идентификаторы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d0325-108">Once hello VM has been moved, you need tooupdate your tools and scripts toouse hello new resource IDs.</span></span> 
> 
> 

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="use-powershell-toomove-a-vm"></a><span data-ttu-id="d0325-109">Используйте Powershell toomove виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="d0325-109">Use Powershell toomove a VM</span></span>
<span data-ttu-id="d0325-110">toomove tooanother группы ресурсов виртуальной машины, необходимо убедиться, что также переместить все зависимые ресурсы hello toomake.</span><span class="sxs-lookup"><span data-stu-id="d0325-110">toomove a virtual machine tooanother resource group, you need toomake sure that you also move all of hello dependent resources.</span></span> <span data-ttu-id="d0325-111">командлет Move-AzureRMResource toouse hello, нужны имя ресурса hello и hello тип ресурса.</span><span class="sxs-lookup"><span data-stu-id="d0325-111">toouse hello Move-AzureRMResource cmdlet, you need hello resource name and hello type of resource.</span></span> <span data-ttu-id="d0325-112">Можно получить из командлета Find-AzureRMResource hello.</span><span class="sxs-lookup"><span data-stu-id="d0325-112">You can get both from hello Find-AzureRMResource cmdlet.</span></span>

    Find-AzureRMResource -ResourceGroupNameContains "<sourceResourceGroupName>"


<span data-ttu-id="d0325-113">toomove мы должны toomove несколько ресурсов виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="d0325-113">toomove a VM we need toomove multiple resources.</span></span> <span data-ttu-id="d0325-114">Можно просто создать для каждого ресурса отдельные переменные, а затем перечислить их.</span><span class="sxs-lookup"><span data-stu-id="d0325-114">We can just create separate variables for each resource and then list them.</span></span> <span data-ttu-id="d0325-115">В этом примере включает большую часть hello основные ресурсы для виртуальной Машины, но можно добавить несколько при необходимости.</span><span class="sxs-lookup"><span data-stu-id="d0325-115">This example includes most of hello basic resources for a VM, but you can add more as needed.</span></span>

    $sourceRG = "<sourceResourceGroupName>"
    $destinationRG = "<destinationResourceGroupName>"

    $vm = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Compute/virtualMachines" -ResourceName "<vmName>"
    $storageAccount = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Storage/storageAccounts" -ResourceName "<storageAccountName>"
    $diagStorageAccount = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Storage/storageAccounts" -ResourceName "<diagnosticStorageAccountName>"
    $vNet = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/virtualNetworks" -ResourceName "<vNetName>"
    $nic = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/networkInterfaces" -ResourceName "<nicName>"
    $ip = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/publicIPAddresses" -ResourceName "<ipName>"
    $nsg = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/networkSecurityGroups" -ResourceName "<nsgName>"

    Move-AzureRmResource -DestinationResourceGroupName $destinationRG -ResourceId $vm.ResourceId, $storageAccount.ResourceId, $diagStorageAccount.ResourceId, $vNet.ResourceId, $nic.ResourceId, $ip.ResourceId, $nsg.ResourceId

<span data-ttu-id="d0325-116">toomove Здравствуйте подписки toodifferent ресурсы, включают hello **- DestinationSubscriptionId** параметра.</span><span class="sxs-lookup"><span data-stu-id="d0325-116">toomove hello resources toodifferent subscription, include hello **-DestinationSubscriptionId** parameter.</span></span> 

    Move-AzureRmResource -DestinationSubscriptionId "<destinationSubscriptionID>" -DestinationResourceGroupName $destinationRG -ResourceId $vm.ResourceId, $storageAccount.ResourceId, $diagStorageAccount.ResourceId, $vNet.ResourceId, $nic.ResourceId, $ip.ResourceId, $nsg.ResourceId



<span data-ttu-id="d0325-117">Будет выведено ресурсов, указанных tooconfirm, что требуется toomove hello.</span><span class="sxs-lookup"><span data-stu-id="d0325-117">You will be asked tooconfirm that you want toomove hello specified resources.</span></span> <span data-ttu-id="d0325-118">Тип **Y** tooconfirm, что требуется toomove hello ресурсы.</span><span class="sxs-lookup"><span data-stu-id="d0325-118">Type **Y** tooconfirm that you want toomove hello resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0325-119">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d0325-119">Next steps</span></span>
<span data-ttu-id="d0325-120">Вы можете перемещать разные типы ресурсов между группами ресурсов и подписками.</span><span class="sxs-lookup"><span data-stu-id="d0325-120">You can move many different types of resources between resource groups and subscriptions.</span></span> <span data-ttu-id="d0325-121">Дополнительные сведения см. в разделе [переместить группу ресурсов toonew ресурсов или подписку](../../resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="d0325-121">For more information, see [Move resources toonew resource group or subscription](../../resource-group-move-resources.md).</span></span>    

