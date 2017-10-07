---
title: "Azure управляемые диск для резервного копирования aaaCopy | Документы Microsoft"
description: "Узнайте, как toocreate копию toouse Azure управляемого диска для диска обратно вверх или устранения неполадок проблемы."
documentationcenter: 
author: squillace
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 2/6/2017
ms.author: rasquill
ms.openlocfilehash: 41b91c2d68eb5be9c493a66be5f7d085a70450d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a>Создание копии виртуального жесткого диска, хранящегося в виде управляемого диска Azure, с помощью управляемых моментальных снимков
Снимок управляемые диск для резервного копирования или создать диск управляемых из моментального снимка hello и присоединить ее tootroubleshoot виртуальной машины для теста tooa. Управляемый моментальный снимок — это полная копия управляемого диска виртуальной машины на определенный момент времени. Он создает копию виртуального жесткого диска только для чтения и по умолчанию сохраняет ее в качестве управляемого диска уровня "Стандартный". 

Дополнительные сведения о ценах см. на странице [с ценами на службу хранилища Azure](https://azure.microsoft.com/pricing/details/managed-disks/). <!--Add link tootopic or blog post that explains managed disks. -->

Используйте либо hello Azure portal или hello Azure CLI 2.0 tootake моментальный снимок hello управляемого диска.

## <a name="use-azure-cli-20-tootake-a-snapshot"></a>Использование Azure CLI 2.0 tootake моментального снимка

> [!NOTE] 
> Hello следующий пример требует hello Azure CLI 2.0 установлена и выполнил вход в учетную запись Azure.

Hello следующие шаги показывают, как tooobtain и сделайте снимок управляемого ОС диска при использовании hello `az snapshot create` с hello `--source-disk` параметра. Hello в примере предполагается наличие виртуальной Машины, которая называется `myVM` создан с использованием управляемого диска ОС в hello `myResourceGroup` группы ресурсов.

```azure-cli
# take hello disk id with which toocreate a snapshot
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create -g myResourceGroup --source "$osDiskId" --name osDisk-backup
```

Hello вывод должен выглядеть примерно так:

```json
{
  "accountType": "Standard_LRS",
  "creationData": {
    "createOption": "Copy",
    "imageReference": null,
    "sourceResourceId": null,
    "sourceUri": "/subscriptions/<guid>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/disks/osdisk_6NexYgkFQU",
    "storageAccountId": null
  },
  "diskSizeGb": 30,
  "encryptionSettings": null,
  "id": "/subscriptions/<guid>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/snapshots/osDisk-backup",
  "location": "westus",
  "name": "osDisk-backup",
  "osType": "Linux",
  "ownerId": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "tags": null,
  "timeCreated": "2017-02-06T21:27:10.172980+00:00",
  "type": "Microsoft.Compute/snapshots"
}
```

## <a name="use-azure-portal-tootake-a-snapshot"></a>Использование Azure портала tootake моментального снимка 

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Начиная с левого верхнего hello, нажмите кнопку **New** и выполните поиск **моментального снимка**.
3. В колонке hello моментального снимка, щелкните **создать**.
4. Введите **имя** для hello моментального снимка.
5. Выберите существующую [группы ресурсов](../../azure-resource-manager/resource-group-overview.md#resource-groups) или имя типа hello новую. 
6. Выберите расположение центра обработки данных Azure.  
7. Для **исходный диск**, выберите hello toosnapshot управляемого диска.
8. Выберите hello **тип счета** toouse toostore hello снимка. Мы рекомендуем тип **Standard_LRS**, если вам не требуется хранить моментальный снимок на высокопроизводительном диске.
9. Щелкните **Создать**.

Если план toouse hello моментального снимка toocreate диск управляемых и присоединить ее к виртуальной Машине, должен toobe высокопроизводительной, используйте параметр hello `--sku Premium_LRS` с hello `az snapshot create` команды. Это создает hello моментального снимка, он сохранится как диск управляемых Premium. Управляемые диски уровня "Премиум" работают быстрее, так как это твердотельные накопители (SSD), однако их использование обойдется дороже, чем диски уровня "Стандартный" (жесткие диски).


