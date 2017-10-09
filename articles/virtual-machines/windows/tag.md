---
title: "aaaHow tootag ресурс виртуальной Машины Windows в Azure | Документы Microsoft"
description: "Дополнительные сведения о виртуальной машине Windows, созданные в Azure с помощью модели развертывания диспетчера ресурсов hello тегов"
services: virtual-machines-windows
documentationcenter: 
author: mmccrory
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 56d17f45-e4a7-4d84-8022-b40334ae49d2
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2016
ms.author: memccror
ms.openlocfilehash: 160416ddc35998b3c98c6e579668a6a5eb6de6e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootag-a-windows-virtual-machine-in-azure"></a>Как tootag виртуальной машине в Azure
Этой статье описываются различные способы tootag виртуальной машине в Azure через hello модели развертывания диспетчера ресурсов. Теги — это определяемые пользователем пары "ключ-значение", которые можно помещать непосредственно в ресурс или группу ресурсов. В настоящее время Azure поддерживает теги too15 каждого ресурса и группы ресурсов. Теги можно поместить в ресурс во время создания hello или добавлены tooan существующий ресурс. Обратите внимание, что теги поддерживаются для ресурсов, созданные с помощью модели развертывания диспетчера ресурсов hello только. Если tootag виртуальной машины Linux, см. [как tootag виртуальной машины Linux в Azure](../linux/tag.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-powershell"></a>Маркировка с помощью PowerShell
toocreate, добавление и удаление тегов с помощью PowerShell, сначала необходимо tooset вверх к [среды PowerShell с помощью диспетчера ресурсов Azure][PowerShell environment with Azure Resource Manager]. После завершения установки hello теги можно разместить на вычисления, сети и хранилища ресурсов при создании или после создания ресурса hello через PowerShell. Эта статья в основном посвящена просмотру и редактированию тегов виртуальных машин.

Во-первых, перейдите tooa виртуальной машины через hello `Get-AzureRmVM` командлета.

        PS C:\> Get-AzureRmVM -ResourceGroupName "MyResourceGroup" -Name "MyTestVM"

Если виртуальная машина уже содержит теги, вы увидите все теги hello для ресурса:

        Tags : {
                "Application": "MyApp1",
                "Created By": "MyName",
                "Department": "MyDepartment",
                "Environment": "Production"
               }

Если вы хотите tooadd теги с помощью PowerShell, можно использовать hello `Set-AzureRmResource` команды. Обратите внимание, что при изменении тегов с помощью PowerShell обновляются все теги. Поэтому при добавлении один ресурс tooa тег, который уже имеет теги, необходимо будет tooinclude все теги hello, которые нужно разместить на ресурс hello toobe. Ниже приведен пример как tooadd дополнительные теги tooa ресурса с помощью командлетов PowerShell.

Этот первый командлет задает все теги hello разместить на *MyTestVM* toohello *$tags* переменной, используя hello `Get-AzureRmResource` и `Tags` свойства.

        PS C:\> $tags = (Get-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM).Tags

Вторая команда Hello отображает hello теги для hello, заданному переменной.

        PS C:\> $tags

        Name        Value
        ----                           -----
        Value        MyDepartment
        Name        Department
        Value        MyApp1
        Name        Application
        Value        MyName
        Name        Created By
        Value        Production
        Name        Environment

Третья команда Hello добавляет дополнительный тег toohello *$tags* переменной. Обратите внимание на использование hello hello  **+=**  tooappend hello новый toohello пары ключ значение *$tags* списка.

        PS C:\> $tags += @{Name="Location";Value="MyLocation"}

Четвертая команда Hello задает все теги hello, определенные в hello *$tags* переменных toohello заданного ресурса. В нашем примере это MyTestVM.

        PS C:\> Set-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM -ResourceType "Microsoft.Compute/VirtualMachines" -Tag $tags

Hello пятая команда отображает все теги hello hello ресурса. Как видите, *расположение* определен как тег *MyLocation* как значение hello.

        PS C:\> (Get-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM).Tags

        Name        Value
        ----                           -----
        Value        MyDepartment
        Name        Department
        Value        MyApp1
        Name        Application
        Value        MyName
        Name        Created By
        Value        Production
        Name        Environment
        Value        MyLocation
        Name        Location

Дополнительные сведения о toolearn тегов с помощью PowerShell извлекать hello [командлеты ресурса Azure][Azure Resource Cmdlets].

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a>Дальнейшие действия
* toolearn Дополнительные сведения о тегов ресурсам Azure в разделе [Обзор диспетчера ресурсов Azure] [ Azure Resource Manager Overview] и [tooorganize с помощью тегов ресурсов Azure] [ Using Tags tooorganize your Azure Resources].
* toosee теги помогают управлять использование ресурсов Azure разделе [основные сведения о счете Azure] [ Understanding your Azure Bill] и [анализировать потребления ресурсов Microsoft Azure] [Gain insights into your Microsoft Azure resource consumption].

[PowerShell environment with Azure Resource Manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
[Azure Resource Cmdlets]: https://msdn.microsoft.com/library/azure/dn757692.aspx
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags tooorganize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
