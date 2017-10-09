---
title: "шаблоны aaaAuthoring с расширениями виртуальных Машин Linux | Документы Microsoft"
description: "Узнайте о разработке шаблонов Azure Resource Manager с расширениями для виртуальных машин Linux."
services: virtual-machines-linux
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 322f8f0b-6697-4acb-b5f3-b3f58d28358b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: b797e442d8706956bbc06c5be611a2b0119055d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="authoring-azure-resource-manager-templates-with-linux-vm-extensions"></a>Разработка шаблонов Azure Resource Manager с расширениями виртуальной машины Linux
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

В Azure CLI выполните следующие команды hello.

      Azure VM extension list

Это имя издателя hello Возвращает команды, имя и версия модуля следующим образом:

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

toolook в образце конфигурации для расширения Linux щелкните hello документации см. в разделе [eExtensions образцы Linux](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

После полного выполнения шаблона с расширениями ВМ tooget toohello см.

[Расширение пользовательских сценариев на виртуальной машине Linux](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/mongodb-on-ubuntu/azuredeploy.json/)

После создания шаблона hello, можно развернуть его с помощью Azure CLI hello.

