---
title: "aaaMove виртуальной Машины Linux в Azure | Документы Microsoft"
description: "Перемещение виртуальной Машины с Linux tooanother подписки Azure или группы ресурсов в модели развертывания диспетчера ресурсов hello."
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
ms.openlocfilehash: 938d04234059111912f03e72d14dabd338bc0678
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-linux-vm-tooanother-subscription-or-resource-group"></a><span data-ttu-id="8056f-103">Перемещение виртуальной Машины с Linux tooanother подписка или группа ресурсов</span><span class="sxs-lookup"><span data-stu-id="8056f-103">Move a Linux VM tooanother subscription or resource group</span></span>
<span data-ttu-id="8056f-104">В этой статье описано, как toomove ВМ Linux между группами ресурсов или подписок.</span><span class="sxs-lookup"><span data-stu-id="8056f-104">This article walks you through how toomove a Linux VM between resource groups or subscriptions.</span></span> <span data-ttu-id="8056f-105">Перемещение ВМ между подписками может оказаться удобным, если вы создали виртуальную Машину в личные подписки, а теперь нужно toomove его tooyour компании подписки.</span><span class="sxs-lookup"><span data-stu-id="8056f-105">Moving a VM between subscriptions can be handy if you created a VM in a personal subscription and now want toomove it tooyour company's subscription.</span></span>

> [!IMPORTANT]
><span data-ttu-id="8056f-106">В настоящее время переместить управляемые диски невозможно.</span><span class="sxs-lookup"><span data-stu-id="8056f-106">You cannot move Managed Disks at this time.</span></span> 
>
><span data-ttu-id="8056f-107">В процессе перемещения hello создаются новые идентификаторы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="8056f-107">New resource IDs are created as part of hello move.</span></span> <span data-ttu-id="8056f-108">После hello ВМ был перемещен, вам потребуется tooupdate вашей средства и сценарии toouse hello новые идентификаторы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="8056f-108">Once hello VM has been moved, you need tooupdate your tools and scripts toouse hello new resource IDs.</span></span> 
> 
> 

## <a name="use-hello-azure-cli-toomove-a-vm"></a><span data-ttu-id="8056f-109">Использовать toomove hello Azure CLI виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="8056f-109">Use hello Azure CLI toomove a VM</span></span>
<span data-ttu-id="8056f-110">toosuccessfully перемещение виртуальной Машины, необходимо toomove hello виртуальной Машины и ее вспомогательные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="8056f-110">toosuccessfully move a VM, you need toomove hello VM and all its supporting resources.</span></span> <span data-ttu-id="8056f-111">Используйте hello **Показать группу azure** команды toolist все ресурсы hello в группу ресурсов и их идентификаторы.</span><span class="sxs-lookup"><span data-stu-id="8056f-111">Use hello **azure group show** command toolist all hello resources in a resource group and their IDs.</span></span> <span data-ttu-id="8056f-112">Она помогает toopipe hello выходные данные tooa этот командный файл, можно скопировать и вставьте hello идентификаторы в более поздней версии команды.</span><span class="sxs-lookup"><span data-stu-id="8056f-112">It helps toopipe hello output of this command tooa file so you can copy and paste hello IDs into later commands.</span></span>

    azure group show <resourceGroupName>

<span data-ttu-id="8056f-113">toomove виртуальной Машины и ее группа ресурсов tooanother ресурсы используют hello **перемещение ресурсов azure** команду CLI.</span><span class="sxs-lookup"><span data-stu-id="8056f-113">toomove a VM and its resources tooanother resource group, use hello **azure resource move** CLI command.</span></span> <span data-ttu-id="8056f-114">Hello в следующем примере показано, как toomove виртуальной Машины и hello наиболее общим ресурсам требуется.</span><span class="sxs-lookup"><span data-stu-id="8056f-114">hello following example shows how toomove a VM and hello most common resources it requires.</span></span> <span data-ttu-id="8056f-115">Мы используем hello **-i** параметра и передайте его в разделенных запятыми список (без пробелов) идентификаторов для toomove ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="8056f-115">We use hello **-i** parameter and pass in a comma-separated list (without spaces) of IDs for hello resources toomove.</span></span>

    vm=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Compute/virtualMachines/<vmName>
    nic=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkInterfaces/<nicName>
    nsg=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkSecurityGroups/<nsgName>
    pip=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/publicIPAddresses/<publicIPName>
    vnet=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/virtualNetworks/<vnetName>
    diag=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<diagnosticStorageAccountName>
    storage=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<storageAcountName>      

    azure resource move --ids $vm,$nic,$nsg,$pip,$vnet,$storage,$diag -d "<destinationResourceGroup>"

<span data-ttu-id="8056f-116">Если требуется, чтобы toomove Здравствуйте виртуальной Машины и ее ресурсы tooa другую подписку, добавить hello **--назначения subscriptionId &#60; destinationSubscriptionID &#62;** параметр toospecify hello конечная подписка.</span><span class="sxs-lookup"><span data-stu-id="8056f-116">If you want toomove hello VM and its resources tooa different subscription, add hello **--destination-subscriptionId &#60;destinationSubscriptionID&#62;** parameter toospecify hello destination subscription.</span></span>

<span data-ttu-id="8056f-117">Если вы работаете с hello командной строки на компьютере Windows, необходимо tooadd  **$**  перед именами переменных hello при их объявлении.</span><span class="sxs-lookup"><span data-stu-id="8056f-117">If you are working from hello Command Prompt on a Windows computer, you need tooadd a **$** in front of hello variable names when you declare them.</span></span> <span data-ttu-id="8056f-118">В Linux это не требуется.</span><span class="sxs-lookup"><span data-stu-id="8056f-118">This isn't needed in Linux.</span></span>

<span data-ttu-id="8056f-119">Будет предложено нужных toomove hello tooconfirm указанный ресурс.</span><span class="sxs-lookup"><span data-stu-id="8056f-119">You are asked tooconfirm that you want toomove hello specified resource.</span></span> <span data-ttu-id="8056f-120">Тип **Y** tooconfirm, что требуется toomove hello ресурсы.</span><span class="sxs-lookup"><span data-stu-id="8056f-120">Type **Y** tooconfirm that you want toomove hello resources.</span></span>

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="next-steps"></a><span data-ttu-id="8056f-121">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8056f-121">Next steps</span></span>
<span data-ttu-id="8056f-122">Вы можете перемещать разные типы ресурсов между группами ресурсов и подписками.</span><span class="sxs-lookup"><span data-stu-id="8056f-122">You can move many different types of resources between resource groups and subscriptions.</span></span> <span data-ttu-id="8056f-123">Дополнительные сведения см. в разделе [переместить группу ресурсов toonew ресурсов или подписку](../../resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="8056f-123">For more information, see [Move resources toonew resource group or subscription](../../resource-group-move-resources.md).</span></span>    

