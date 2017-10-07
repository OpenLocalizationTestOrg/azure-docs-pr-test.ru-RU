---
title: "aaaAuthoring шаблоны с расширениями ВМ Windows | Документы Microsoft"
description: "Узнайте о разработке шаблонов Azure Resource Manager с расширениями для виртуальных машин Windows."
services: virtual-machines-windows
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 418dd1f7-ded8-45ab-9a5a-a59d245e2555
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: c5156cb3859f7ff86bebda942150d268e57d6486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="authoring-azure-resource-manager-templates-with-windows-vm-extensions"></a>Authoring Azure Resource Manager templates with Windows VM extensions
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

В Azure PowerShell выполните hello, выполнив командлет Azure PowerShell.

      Get-AzureVMAvailableExtension


Этот командлет возвращает hello имя издателя, имя и версия модуля следующим образом:

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

Эти три свойства сопоставляются слишком «издатель», «тип» и «typeHandlerVersion» соответственно в hello выше фрагмента шаблона.

> [!NOTE]
> Это всегда рекомендуется toouse hello последнюю версию tooget hello Большинство обновленных функциональных возможностей расширения.
> 
> 

## <a name="identifying-hello-schema-for-hello-extension-configuration-parameters"></a>Определение схемы hello для параметров конфигурации модуля hello
следующим шагом Hello разработки шаблоном расширения является формат hello tooidentify для предоставления параметров конфигурации. Каждое расширение поддерживает собственный набор параметров.

toolook в образце конфигурации для расширения Windows, в разделе [примеры расширений Windows](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

После полного выполнения шаблона с расширениями ВМ tooget toohello см.

[Расширение Custom Script на виртуальной машине Windows](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/201-list-storage-keys-windows-vm/azuredeploy.json/)

После создания шаблона hello, можно развернуть с помощью Azure PowerShell.

