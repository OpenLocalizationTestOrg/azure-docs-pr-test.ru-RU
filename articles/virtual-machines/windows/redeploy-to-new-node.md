---
title: "aaaRedeploy виртуальных машинах в Azure | Документы Microsoft"
description: "Как проблемы tooredeploy виртуальных машинах в Azure toomitigate RDP-подключение."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: genlin
manager: timlt
tags: azure-resource-manager,top-support-issue
ms.assetid: 0ee456ee-4595-4a14-8916-72c9110fc8bd
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 903d9d5bf241075931ee4b746690c553d808a58f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="redeploy-windows-virtual-machine-toonew-azure-node"></a>Повторное развертывание Windows виртуальной машины toonew узла Azure
Если направлена трудностей Устранение неполадок удаленного рабочего стола (RDP) подключения или приложения доступ к tooWindows Azure виртуальной машины (VM), повторное развертывание виртуальной Машины может помочь приветствия. При повторном развертывании виртуальной Машины, он перемещает новый узел hello ВМ tooa внутри hello инфраструктуры Azure и лежащих в основе обратно на, сохраняя все параметры конфигурации и связанных ресурсов. В этой статье показано, как tooredeploy в виртуальную Машину с помощью Azure PowerShell или портал Azure hello.

> [!NOTE]
> После повторного развертывания виртуальной Машины, теряется временный диск hello и обновляются динамические IP-адреса, связанные с виртуального сетевого интерфейса. 


## <a name="using-azure-powershell"></a>Использование Azure PowerShell
Убедитесь, что у hello последнюю версию Azure PowerShell 1.x, установлены на компьютере. Дополнительные сведения см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).

Hello следующий пример выполняет развертывание виртуальной Машины с именем hello `myVM` в группе ресурсов hello с именем `myResourceGroup`:

```powershell
Set-AzureRmVM -Redeploy -ResourceGroupName "myResourceGroup" -Name "myVM"
```


[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a>Дальнейшие действия
Если возникли проблемы с подключением tooyour виртуальной Машины, можно найти справку на [Устранение неполадок подключений по протоколу RDP](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) или [подробные шаги по устранению неполадок протокола удаленного рабочего СТОЛА](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). При проблемах с доступом к приложению, выполняющемуся в виртуальной машине, ознакомьтесь со статьей [Устранение неполадок доступа к приложению, выполняющемуся в виртуальной машине Azure](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

