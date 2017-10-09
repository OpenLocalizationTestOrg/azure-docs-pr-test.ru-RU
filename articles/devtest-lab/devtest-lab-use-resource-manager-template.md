---
title: "aaaView и использование шаблона виртуальной машины диспетчера ресурсов Azure | Документы Microsoft"
description: "Узнайте, как toouse hello шаблона диспетчера ресурсов Azure из toocreate виртуальной машине другие виртуальные машины"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: a759d9ce-655c-4ac6-8834-cb29dd7d30dd
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: tarcher
ms.openlocfilehash: b79f7eb4171793681a0b654e6e72a83191c76bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-a-virtual-machines-azure-resource-manager-template"></a>Использование шаблона Azure Resource Manager виртуальной машины

При создании виртуальной машины (VM) в DevTest Labs через hello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040), hello шаблона диспетчера ресурсов Azure можно просмотреть перед сохранением hello виртуальной Машины. Hello шаблона может быть использован как toocreate основы более виртуальных машин лаборатории с hello одинаковые параметры.

В этой статье описывается, как tooview hello шаблона диспетчера ресурсов при создании виртуальной Машины и как toodeploy его более поздней версии tooautomate Создание hello одной виртуальной Машины.

## <a name="multi-vm-vs-single-vm-resource-manager-templates"></a>Шаблоны Resource Manager для нескольких и одной виртуальной машины
Существует два способа toocreate виртуальных машин в DevTest Labs, с помощью шаблона диспетчера ресурсов: Подготовка ресурсов Microsoft.DevTestLab/labs/virtualmachines hello и подготовить hello Microsoft.Commpute/virtualmachines ресурсов. Каждый из этих ресурсов используется в различных сценариях и требует разных разрешений.

- Шаблоны диспетчера ресурсов, использующих тип ресурса Microsoft.DevTestLab/labs/virtualmachines (как объявлено в свойстве «resource» hello в шаблоне hello) позволяет подготовить лаборатории отдельных виртуальных машин. Каждая виртуальная машина затем отображается в виде одного элемента в списке виртуальных машин DevTest Labs hello:

   ![Список виртуальных машин как одиночные элементы в списке виртуальных машин hello DevTest Labs](./media/devtest-lab-use-arm-template/devtestlab-lab-vm-single-item.png)

   Этот тип шаблона диспетчера ресурсов может предоставляться через hello команду Azure PowerShell **New AzureRmResourceGroupDeployment** или с помощью команды Azure CLI hello **создания развертывания группы az** . Требуются разрешения администратора, поэтому пользователям, связанным с ролью пользователя DevTest Labs не удается выполнить развертывание hello. 

- Шаблоны диспетчера ресурсов, использующих тип ресурса Microsoft.Compute/virtualmachines можно подготовить несколько виртуальных машин в качестве одной среды в списке виртуальных машин DevTest Labs hello:

   ![Список виртуальных машин как одиночные элементы в списке виртуальных машин hello DevTest Labs](./media/devtest-lab-use-arm-template/devtestlab-lab-vm-single-environment.png)

   Виртуальные машины в одной среде можно одновременно управлять приветствия и общая папка hello же жизненного цикла. Пользователям, связанным с ролью пользователя DevTest Labs можно создать среды, использующие эти шаблоны, при условии, что Здравствуйте, администратор настроил лаборатории hello таким образом.

Hello оставшейся части этой статьи рассматриваются шаблоны диспетчера ресурсов, использующих Mirosoft.DevTestLab/labs/virtualmachines. Они используются, создание виртуальной Машины lab tooautomate Администраторы лаборатории (например, claimable ВМ) или создание золотой изображения (например, фабрика изображения).

[Советы и рекомендации по созданию шаблонов диспетчера ресурсов Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices) предлагает множество toohelp указания и рекомендации, создание шаблонов диспетчера ресурсов Azure, надежное и легко toouse.

## <a name="view-and-save-a-virtual-machines-resource-manager-template"></a>Просмотр и сохранение шаблона Azure Resource Manager виртуальной машины
1. Выполните действия hello в [создания первой виртуальной Машины в лабораторной среде](devtest-lab-create-first-vm.md) toobegin создания виртуальной машины.
1. Введите hello необходимые сведения для виртуальной машины и добавить все артефакты, необходимые для этой виртуальной Машины.
1. Внизу hello hello настроить окно "Параметры", выберите **шаблон ARM представление**.

   ![Кнопка View ARM template (Просмотреть шаблон ARM)](./media/devtest-lab-use-arm-template/devtestlab-lab-view-rm-template.png)
1. Скопируйте и сохраните toouse шаблона диспетчера ресурсов hello более поздней версии toocreate другой виртуальной машины.

   ![Toosave шаблона диспетчера ресурсов для последующего использования](./media/devtest-lab-use-arm-template/devtestlab-lab-copy-rm-template.png)

После сохранения шаблона диспетчера ресурсов hello, необходимо обновить раздел параметров hello hello шаблона перед его использованием. Можно создать parameter.json, который настраивает просто hello параметры за пределами hello фактическое шаблона диспетчера ресурсов. 

![Настройка параметров с помощью JSON-файла](./media/devtest-lab-use-arm-template/devtestlab-lab-custom-params.png)

## <a name="deploy-a-resource-manager-template-toocreate-a-vm"></a>Развертывание toocreate шаблона диспетчера ресурсов виртуальной Машины
После сохранения шаблона диспетчера ресурсов и настроить его для личных нужд, его можно использовать tooautomate Создание виртуальной Машины. [Развертывание ресурсов с помощью шаблонов диспетчера ресурсов и Azure PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy) описывает как toouse Azure PowerShell с toodeploy шаблонов диспетчера ресурсов вашей tooAzure ресурсов. [Развертывание ресурсов с помощью шаблонов диспетчера ресурсов и Azure CLI](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy-cli) описывает как toouse Azure CLI с toodeploy шаблонов диспетчера ресурсов вашей tooAzure ресурсов.

> [!NOTE]
> Только пользователь с правами владельца лаборатории может создать виртуальные машины из шаблона Resource Manager с помощью Azure PowerShell. Если требуется tooautomate создания виртуальной Машины, с помощью шаблона диспетчера ресурсов и иметь только разрешения пользователя, можно использовать hello [ **создания виртуальной машины лаборатории az** в hello CLI](https://docs.microsoft.com/cli/azure/lab/vm#create).

### <a name="next-steps"></a>Дальнейшие действия
* Узнайте, каким образом слишком[создания нескольких виртуальных Машин сред с помощью шаблонов диспетчера ресурсов](devtest-lab-create-environment-from-arm.md).
* Обзор дополнительных шаблонов диспетчера ресурсов: быстрый запуск автоматизации DevTest Labs с hello [открытый DevTest Labs в репозитории GitHub](https://github.com/Azure/azure-quickstart-templates).
