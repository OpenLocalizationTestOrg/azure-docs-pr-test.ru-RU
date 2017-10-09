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
# <a name="move-a-linux-vm-tooanother-subscription-or-resource-group"></a>Перемещение виртуальной Машины с Linux tooanother подписка или группа ресурсов
В этой статье описано, как toomove ВМ Linux между группами ресурсов или подписок. Перемещение ВМ между подписками может оказаться удобным, если вы создали виртуальную Машину в личные подписки, а теперь нужно toomove его tooyour компании подписки.

> [!IMPORTANT]
>В настоящее время переместить управляемые диски невозможно. 
>
>В процессе перемещения hello создаются новые идентификаторы ресурсов. После hello ВМ был перемещен, вам потребуется tooupdate вашей средства и сценарии toouse hello новые идентификаторы ресурсов. 
> 
> 

## <a name="use-hello-azure-cli-toomove-a-vm"></a>Использовать toomove hello Azure CLI виртуальной Машины
toosuccessfully перемещение виртуальной Машины, необходимо toomove hello виртуальной Машины и ее вспомогательные ресурсы. Используйте hello **Показать группу azure** команды toolist все ресурсы hello в группу ресурсов и их идентификаторы. Она помогает toopipe hello выходные данные tooa этот командный файл, можно скопировать и вставьте hello идентификаторы в более поздней версии команды.

    azure group show <resourceGroupName>

toomove виртуальной Машины и ее группа ресурсов tooanother ресурсы используют hello **перемещение ресурсов azure** команду CLI. Hello в следующем примере показано, как toomove виртуальной Машины и hello наиболее общим ресурсам требуется. Мы используем hello **-i** параметра и передайте его в разделенных запятыми список (без пробелов) идентификаторов для toomove ресурсы hello.

    vm=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Compute/virtualMachines/<vmName>
    nic=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkInterfaces/<nicName>
    nsg=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkSecurityGroups/<nsgName>
    pip=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/publicIPAddresses/<publicIPName>
    vnet=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/virtualNetworks/<vnetName>
    diag=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<diagnosticStorageAccountName>
    storage=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<storageAcountName>      

    azure resource move --ids $vm,$nic,$nsg,$pip,$vnet,$storage,$diag -d "<destinationResourceGroup>"

Если требуется, чтобы toomove Здравствуйте виртуальной Машины и ее ресурсы tooa другую подписку, добавить hello **--назначения subscriptionId &#60; destinationSubscriptionID &#62;** параметр toospecify hello конечная подписка.

Если вы работаете с hello командной строки на компьютере Windows, необходимо tooadd  **$**  перед именами переменных hello при их объявлении. В Linux это не требуется.

Будет предложено нужных toomove hello tooconfirm указанный ресурс. Тип **Y** tooconfirm, что требуется toomove hello ресурсы.

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="next-steps"></a>Дальнейшие действия
Вы можете перемещать разные типы ресурсов между группами ресурсов и подписками. Дополнительные сведения см. в разделе [переместить группу ресурсов toonew ресурсов или подписку](../../resource-group-move-resources.md).    

