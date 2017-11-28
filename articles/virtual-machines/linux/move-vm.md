---
title: "Перемещение виртуальной машины Linux в Azure | Документация Майкрософт"
description: "Из этой статьи вы узнаете, как перенести виртуальную машину Linux в другую подписку или группу ресурсов Azure в рамках модели развертывания Resource Manager."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d635f0a5-4458-4b95-a5f8-eed4f41eb4d4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 4695a9c934f97f2b2d448c4990e7ad5533e38e9f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="move-a-linux-vm-to-another-subscription-or-resource-group"></a><span data-ttu-id="93f40-103">Перемещение виртуальной машины Linux в другую подписку или группу ресурсов</span><span class="sxs-lookup"><span data-stu-id="93f40-103">Move a Linux VM to another subscription or resource group</span></span>
<span data-ttu-id="93f40-104">В этой статье описано перемещение виртуальной машины Linux между группами ресурсов или подписками.</span><span class="sxs-lookup"><span data-stu-id="93f40-104">This article walks you through how to move a Linux VM between resource groups or subscriptions.</span></span> <span data-ttu-id="93f40-105">Перемещение ВМ между подписками может понадобиться, если вы создали виртуальную машину в личной подписке и вам нужно переместить ее в корпоративную подписку.</span><span class="sxs-lookup"><span data-stu-id="93f40-105">Moving a VM between subscriptions can be handy if you created a VM in a personal subscription and now want to move it to your company's subscription.</span></span>

> [!IMPORTANT]
><span data-ttu-id="93f40-106">В настоящее время переместить управляемые диски невозможно.</span><span class="sxs-lookup"><span data-stu-id="93f40-106">You cannot move Managed Disks at this time.</span></span> 
>
><span data-ttu-id="93f40-107">Во время перемещения создаются новые идентификаторы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="93f40-107">New resource IDs are created as part of the move.</span></span> <span data-ttu-id="93f40-108">После перемещения виртуальной машины вам нужно будет обновить средства и сценарии, чтобы использовать новые идентификаторы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="93f40-108">Once the VM has been moved, you need to update your tools and scripts to use the new resource IDs.</span></span> 
> 
> 

## <a name="use-the-azure-cli-to-move-a-vm"></a><span data-ttu-id="93f40-109">Использование Azure CLI для перемещения виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="93f40-109">Use the Azure CLI to move a VM</span></span>
<span data-ttu-id="93f40-110">Для успешного перемещения виртуальной машины необходимо перенести саму виртуальную машину и все вспомогательные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="93f40-110">To successfully move a VM, you need to move the VM and all its supporting resources.</span></span> <span data-ttu-id="93f40-111">Используйте команду **azure group show** , чтобы вывести список всех ресурсов в группе ресурсов и их идентификаторы.</span><span class="sxs-lookup"><span data-stu-id="93f40-111">Use the **azure group show** command to list all the resources in a resource group and their IDs.</span></span> <span data-ttu-id="93f40-112">Желательно сохранить выходные данные этой команды в файл, чтобы позже можно было копировать и вставлять идентификаторы в командах.</span><span class="sxs-lookup"><span data-stu-id="93f40-112">It helps to pipe the output of this command to a file so you can copy and paste the IDs into later commands.</span></span>

    azure group show <resourceGroupName>

<span data-ttu-id="93f40-113">Чтобы переместить виртуальную машину и ее ресурсы в другую группу, используйте команду CLI **azure resource move** .</span><span class="sxs-lookup"><span data-stu-id="93f40-113">To move a VM and its resources to another resource group, use the **azure resource move** CLI command.</span></span> <span data-ttu-id="93f40-114">Ниже показано, как переместить ВМ и наиболее распространенные ресурсы, которые для этого понадобятся.</span><span class="sxs-lookup"><span data-stu-id="93f40-114">The following example shows how to move a VM and the most common resources it requires.</span></span> <span data-ttu-id="93f40-115">Мы используем параметр **-i** и передаем разделенный запятыми список (без пробелов) идентификаторов ресурсов для перемещения.</span><span class="sxs-lookup"><span data-stu-id="93f40-115">We use the **-i** parameter and pass in a comma-separated list (without spaces) of IDs for the resources to move.</span></span>

    vm=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Compute/virtualMachines/<vmName>
    nic=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkInterfaces/<nicName>
    nsg=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkSecurityGroups/<nsgName>
    pip=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/publicIPAddresses/<publicIPName>
    vnet=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/virtualNetworks/<vnetName>
    diag=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<diagnosticStorageAccountName>
    storage=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<storageAcountName>      

    azure resource move --ids $vm,$nic,$nsg,$pip,$vnet,$storage,$diag -d "<destinationResourceGroup>"

<span data-ttu-id="93f40-116">Если вы хотите переместить виртуальную машину и ее ресурсы в другую подписку, добавьте параметр **--destination-subscriptionId &#60;destinationSubscriptionID&#62;**, чтобы указать целевую подписку.</span><span class="sxs-lookup"><span data-stu-id="93f40-116">If you want to move the VM and its resources to a different subscription, add the **--destination-subscriptionId &#60;destinationSubscriptionID&#62;** parameter to specify the destination subscription.</span></span>

<span data-ttu-id="93f40-117">Если вы работаете на компьютере под управлением Windows, добавьте из командной строки символ **$** перед именами переменных при их объявлении.</span><span class="sxs-lookup"><span data-stu-id="93f40-117">If you are working from the Command Prompt on a Windows computer, you need to add a **$** in front of the variable names when you declare them.</span></span> <span data-ttu-id="93f40-118">В Linux это не требуется.</span><span class="sxs-lookup"><span data-stu-id="93f40-118">This isn't needed in Linux.</span></span>

<span data-ttu-id="93f40-119">Появится запрос на подтверждение перемещения указанного ресурса.</span><span class="sxs-lookup"><span data-stu-id="93f40-119">You are asked to confirm that you want to move the specified resource.</span></span> <span data-ttu-id="93f40-120">Введите **Y** , чтобы подтвердить перемещение ресурсов.</span><span class="sxs-lookup"><span data-stu-id="93f40-120">Type **Y** to confirm that you want to move the resources.</span></span>

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="next-steps"></a><span data-ttu-id="93f40-121">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="93f40-121">Next steps</span></span>
<span data-ttu-id="93f40-122">Вы можете перемещать разные типы ресурсов между группами ресурсов и подписками.</span><span class="sxs-lookup"><span data-stu-id="93f40-122">You can move many different types of resources between resource groups and subscriptions.</span></span> <span data-ttu-id="93f40-123">Дополнительные сведения см. в статье [Перемещение ресурсов в новую группу ресурсов или подписку](../../resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="93f40-123">For more information, see [Move resources to new resource group or subscription](../../resource-group-move-resources.md).</span></span>    

