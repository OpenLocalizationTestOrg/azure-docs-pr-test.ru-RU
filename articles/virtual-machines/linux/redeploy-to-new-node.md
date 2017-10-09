---
title: "aaaRedeploy виртуальных машин Linux в Azure | Документы Microsoft"
description: "Как проблемы tooredeploy виртуальных машин Linux в Azure toomitigate SSH-подключения."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
tags: azure-resource-manager,top-support-issue
ms.assetid: e9530dd6-f5b0-4160-b36b-d75151d99eb7
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 9adfd1b11f262d362133366b2bba5e69c70c9b82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="redeploy-linux-virtual-machine-toonew-azure-node"></a>Повторное развертывание виртуальной машины Linux toonew узла Azure
Если сталкиваются с трудностями, устранение неполадок SSH или приложений доступа к tooa Linux виртуальной машины (VM) в Azure, повторное развертывание hello виртуальной Машины может помочь. При повторном развертывании виртуальной Машины, перемещает hello ВМ tooa новый узел в рамках hello инфраструктуры Azure и затем включаются. При этом сохраняются все параметры конфигурации и связанные ресурсы. В этой статье показано, как tooredeploy в виртуальную Машину с помощью Azure CLI или hello портал Azure.

> [!NOTE]
> После повторного развертывания виртуальной Машины, теряется временный диск hello и обновляются динамические IP-адреса, связанные с виртуального сетевого интерфейса. 

Можно повторно развернуть ВМ с помощью одного из следующих вариантов hello. Требуется только один параметр tooredeploy toochoose ВМ:

- [Azure CLI 2.0](#azure-cli-20)
- [Azure CLI 1.0](#azure-cli-10)
- [Портал Azure](#using-azure-portal)

## <a name="use-hello-azure-cli-20"></a>Использовать hello Azure CLI 2.0
Последняя версия hello установки [Azure CLI 2.0](/cli/azure/install-az-cli2) и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).

Повторно разверните виртуальную машину, выполнив команду [az vm redeploy](/cli/azure/vm#redeploy). Следующий пример повторно развертывает Hello hello виртуальной Машины с именем *myVM* в группе ресурсов hello с именем *myResourceGroup*:

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM 
```

## <a name="use-hello-azure-cli-10"></a>Использовать hello Azure CLI 1.0
Установка hello [последние Azure CLI 1.0](../../cli-install-nodejs.md), войдите в учетную запись Azure tooan и убедитесь, что вы находитесь в режиме диспетчера ресурсов (`azure config mode arm`).

Следующий пример повторно развертывает Hello hello виртуальной Машины с именем *myVM* в группе ресурсов hello с именем *myResourceGroup*:

```azurecli
azure vm redeploy --resource-group myResourceGroup --vm-name myVM 
```

[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a>Дальнейшие действия
Если возникли проблемы с подключением tooyour виртуальной Машины, можно найти справку на [Устранение неполадок соединений по протоколу SSH](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) или [подробные шаги по устранению неполадок SSH](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). При проблемах с доступом к приложению, выполняющемуся в виртуальной машине, ознакомьтесь со статьей [Устранение неполадок доступа к приложению, выполняющемуся в виртуальной машине Azure](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

