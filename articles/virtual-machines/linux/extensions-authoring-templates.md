---
title: "Разработка шаблонов с расширениями виртуальной машины Linux | Документация Майкрософт"
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
ms.openlocfilehash: 8b017306474670bf8dde1440128e16ec35146f24
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="authoring-azure-resource-manager-templates-with-linux-vm-extensions"></a>Разработка шаблонов Azure Resource Manager с расширениями виртуальной машины Linux
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

В Azure CLI выполните следующую команду.

      Azure VM extension list

Эта команда возвращает имя издателя, имя расширения и версию в следующем виде.

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

Эти три свойства сопоставляются со значениями publisher, type и typeHandlerVersion в приведенном выше фрагменте шаблона.

> [!NOTE]
> Рекомендуется всегда использовать самую последнюю версию расширения для обеспечения максимальной функциональности.
> 
> 

## <a name="identifying-the-schema-for-the-extension-configuration-parameters"></a>Определение схемы для параметров конфигурации расширения
Следующий шаг при создании шаблона расширения заключается в определении формата для предоставления параметров конфигурации. Каждое расширение поддерживает собственный набор параметров.

Чтобы ознакомиться с примерами конфигураций для расширений Linux, откройте документацию [с примерами расширений Linux](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Ознакомьтесь со следующими разделами, чтобы получить полноценный шаблон с расширениями виртуальной машины.

[Расширение пользовательских сценариев на виртуальной машине Linux](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/mongodb-on-ubuntu/azuredeploy.json/)

После разработки шаблон можно развернуть с помощью Azure CLI.

