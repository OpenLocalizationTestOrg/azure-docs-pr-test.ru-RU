---
title: "aaaCreate или изменить labs, автоматически, используя шаблоны Azure Resource Manager с помощью PowerShell | Документы Microsoft"
description: "Узнайте, как шаблоны Azure Resource Manager toouse с PowerShell toocreate или изменить labs автоматически в лаборатории DevTest"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: dad9944c-0b20-48be-ba80-8f4aa0950903
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/21/2017
ms.author: tarcher
ms.openlocfilehash: 29c8bc67caaec17b1f8926dde4e5d9d314b06600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-or-modify-labs-automatically-using-azure-resource-manager-templates-and-powershell"></a>Автоматическое создание и изменение лабораторий помощью шаблонов Azure Resource Manager и PowerShell

DevTest Labs предоставляет множество шаблонов Azure Resource Manager и сценариев PowerShell, которые позволяют быстро и автоматически создавать новые или изменять существующие лаборатории и затем развертывать эти ресурсы.

Эта статья поможет hello процесс использования этих шаблонов и сценариев создания tooautomate hello, изменения и развертывания лабораториях. В этой статье также показано, где можно найти дополнительные сведения о том, как toouse PowerShell tooperform некоторые наиболее распространенные задачи в DevTest Labs.

## <a name="step-1-gather-your-templates-and-scripts"></a>Шаг 1. Сбор шаблонов и сценариев
Вы можете найти готовые [шаблоны Azure Resource Manager](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates) и [сценарии PowerShell](https://github.com/Azure/azure-devtestlab/tree/master/Scripts) в нашем общедоступном [репозитории Github](https://github.com/Azure/azure-devtestlab). Используйте их в исходном виде или настраивайте их и сохраняйте в своем [частном репозитории Git](devtest-lab-add-artifact-repo.md). 

## <a name="step-2-modify-your-azure-resource-manager-template"></a>Шаг 2. Изменение шаблона Azure Resource Manager
Можно выполнить инструкции раздела hello [создание первого шаблона диспетчера ресурсов Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-create-first-template) Если не был создан шаблон до.

Кроме того [советы и рекомендации по созданию шаблонов диспетчера ресурсов Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices) предлагает множество toohelp указания и рекомендации, создание шаблонов диспетчера ресурсов Azure, надежное и легко toouse. Как правило используется один из подходов hello разновидность или примеры исключительно и изменить шаблон вашим потребностям.

## <a name="step-3-deploy-resources-with-powershell"></a>Шаг 3. Развертывание ресурсов с помощью PowerShell
После настройки шаблонов и сценариев, выполните необходимые действия hello слишком[развертывания ресурсов с помощью шаблонов диспетчера ресурсов и Azure PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy). Hello статья содержит общие сведения об использовании Azure PowerShell с toodeploy шаблоны Azure Resource Manager вашей tooAzure ресурсов.


## <a name="common-tasks-you-can-perform-in-devtest-labs-using-powershell"></a>Общие задачи, которые можно выполнять в DevTest Labs с помощью PowerShell
Существует множество других распространенных задач, которые можно автоматизировать с помощью PowerShell. Hello в следующих разделах документации hello структуры tooperform необходимые шаги hello этих задач.

* [Создание пользовательского образа из VHD-файла с помощью PowerShell](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
* [Отправка VHD файл toolab учетной записи хранилища с помощью PowerShell](devtest-lab-upload-vhd-using-powershell.md)
* [Добавить лаборатории tooa внешнего пользователя, с помощью PowerShell](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell)
* [Создание пользовательской роли лаборатории с помощью PowerShell](devtest-lab-grant-user-permissions-to-specific-lab-policies.md#creating-a-lab-custom-role-using-powershell)

### <a name="next-steps"></a>Дальнейшие действия
* Узнайте, как toocreate [закрытом репозитории Git](devtest-lab-add-artifact-repo.md) для хранения настраиваемых шаблонов или сценарии.
* Просмотр hello [шаблоны диспетчера ресурсов Azure из коллекции шаблонов быстрый запуск Azure](https://github.com/Azure/azure-quickstart-templates).
