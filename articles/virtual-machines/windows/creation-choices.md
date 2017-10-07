---
title: "способы aaaDifferent toocreate виртуальной Машине Windows в Azure | Документы Microsoft"
description: "Список способов hello toocreate виртуальной машины Windows с помощью диспетчера ресурсов."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 809ba8f4-b54e-43c5-bbe3-8e710c49971f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/02/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2928d4daa9b44c4d3a5083092a82c9a7f7c69fae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="different-ways-toocreate-a-windows-virtual-machine"></a>Различные способы toocreate виртуальной машины Windows

Azure предлагает toocreate различными способами виртуальной машины, так как виртуальные машины подходят для разных пользователей и целей. Это означает, что вы должны toomake некоторые решения о hello виртуальной машины и как toocreate его. В этой статье предоставляет сводку часть этих вариантов и связывает tooinstructions.

## <a name="azure-portal"></a>Портал Azure
С помощью портала Azure hello является tootry простым способом ожидания виртуальной машины, особенно в том случае, если только вы начинаете работать с Azure. 

[Создание виртуальной машины под управлением Windows, с помощью портала hello](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="template"></a>Шаблон
Для виртуальных машин требуется сочетание ресурсов (таких как группы доступности и учетные записи хранения). Вместо того чтобы развертывание и управление каждого ресурса отдельно, можно создать шаблон диспетчера ресурсов Azure, которая развертывает и подготавливает все ресурсы hello в один, согласованной операции.

* [Создание виртуальной машины Windows с использованием шаблона диспетчера ресурсов](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="azure-powershell"></a>Azure PowerShell
Если вы предпочитаете работать в командной строке, можно использовать Azure PowerShell.

* [Создание виртуальной машины Windows с помощью PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="visual-studio"></a>Visual Studio
Использовать toobuild Visual Studio, управление, развертывание виртуальных машин с помощью средств hello Azure для Visual Studio и hello Azure SDK.

[Инструменты Azure для Visual Studio](https://www.visualstudio.com/features/azure-tools-vs)

