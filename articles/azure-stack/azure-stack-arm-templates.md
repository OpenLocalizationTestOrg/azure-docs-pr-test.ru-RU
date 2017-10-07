---
title: "шаблоны Azure Resource Manager aaaUse стека Azure | Документы Microsoft"
description: "Узнайте, как шаблоны Azure Resource Manager toouse в стек Azure tooprovision ресурсы."
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: 2022dbe5-47fd-457d-9af3-6c01688171d7
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: bcc73756fa712ecff9791301d43d227112be8362
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-resource-manager-templates-in-azure-stack"></a>Использование шаблонов диспетчера ресурсов Azure в Azure Stack
Шаблоны диспетчера ресурсов Azure, развертывание и предоставление всех hello ресурсы для приложения в один, согласованной операции. Кроме того, можно повторно развернуть шаблоны toomake изменения toohello ресурсы в группе ресурсов hello.

Эти шаблоны можно развернуть с помощью портала hello стека Microsoft Azure, PowerShell, Командная строка hello и Visual Studio.

Следующие примеры использования шаблонов Hello доступны на [GitHub](http://aka.ms/azurestackgithub):

## <a name="deploy-sharepoint-non-high-availability"></a>Развертывание SharePoint (с обычным уровнем доступности)
Используйте для hello PowerShell DSC расширения toocreate SharePoint 2013 фермы, включающей hello следующие ресурсы:

* виртуальную сеть;
* три учетные записи хранения;
* два внешних балансировщика нагрузки;
* Одна виртуальная машина настроен в качестве контроллера домена для нового леса с одним доменом
* одну виртуальную машину, настроенную в качестве изолированного сервера SQL Server 2014;
* одну виртуальную машину, настроенную в качестве фермы SharePoint 2013 с одним компьютером.

## <a name="deploy-ad-non-high-availability"></a>Развертывание AD (без высокой доступности)
Используйте toocreate расширение PowerShell DSC hello адрес сервера контроллера домена AD, включающий hello следующие ресурсы:

* виртуальную сеть;
* одна учетная запись хранения;
* один внешний балансировщик нагрузки;
* Одна виртуальная машина настроен в качестве контроллера домена для нового леса с одним доменом

## <a name="deploy-adsql-non-high-availability"></a>Развертывание AD или SQL (с обычным уровнем доступности)
Используйте hello PowerShell DSC расширения toocreate SQL Server 2014 изолированного сервера, включая hello следующие ресурсы:

* виртуальную сеть;
* две учетные записи хранения;
* один внешний балансировщик нагрузки;
* Одна виртуальная машина настроен в качестве контроллера домена для нового леса с одним доменом
* одну виртуальную машину, настроенную в качестве изолированного сервера SQL Server 2014;

## <a name="vm-dsc-extension-azure-automation-pull-server"></a>VM-DSC-Extension-Azure-Automation-Pull-Server
Использовать tooconfigure расширение PowerShell DSC hello существующая виртуальная машина локальный диспетчер конфигураций (LCM) и зарегистрируйте его tooan Azure Automation учетной записи DSC опрашивающего сервера.

## <a name="create-a-virtual-machine-from-a-user-image"></a>Создание виртуальной машины из пользовательского образа
Можно создать виртуальную машину из настраиваемого пользовательского образа. Этот шаблон также развертывает виртуальную сеть (с DNS), общедоступный IP-адрес и сетевой интерфейс.

## <a name="simple-vm"></a>Простая виртуальная машина
Развертывание Windows виртуальной Машины, включающий виртуальной сети (с помощью DNS), общедоступный IP-адрес и сетевого интерфейса.

## <a name="cancel-a-running-template-deployment"></a>Отмена выполняющегося развертывания шаблона
использовать toocancel в выполняющееся развертывание шаблона hello `Stop-AzureRmResourceGroupDeployment` командлета PowerShell.

## <a name="next-steps"></a>Дальнейшие действия
[Развертывание шаблонов с портала hello](azure-stack-deploy-template-portal.md)

[Общие сведения об Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)

