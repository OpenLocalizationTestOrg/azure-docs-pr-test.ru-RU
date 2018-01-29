---
title: "Создание сервера Azure Analysis Services с помощью PowerShell | Документация Майкрософт"
description: "Узнайте, как создать сервер Azure Analysis Services с помощью PowerShell."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: kfile
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 11/01/2017
ms.author: owend
ms.custom: mvc
ms.openlocfilehash: 2db167fd746b53e234aac3dbe2e5b76b56737e24
ms.sourcegitcommit: d41d9049625a7c9fc186ef721b8df4feeb28215f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/02/2017
---
# <a name="create-an-azure-analysis-services-server-by-using-powershell"></a>Создание сервера Azure Analysis Services с помощью PowerShell

В этом кратком руководстве объясняется, как с помощью PowerShell и командной строки создать сервер Azure Analysis Services в [группе ресурсов Azure](../azure-resource-manager/resource-group-overview.md) вашей подписки Azure.

Для этой задачи требуется модуль Azure PowerShell 4.0 или более поздней версии. Чтобы узнать версию, выполните команду ` Get-Module -ListAvailable AzureRM`. Чтобы выполнить установку или обновление, см. статью [Установка и настройка Azure PowerShell](/powershell/azure/install-azurerm-ps). 

> [!NOTE]
> При создании сервера вам могут выставляться счета за новую службу. Дополнительные сведения см. в разделе [цен на службы Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).

## <a name="prerequisites"></a>Предварительные требования
Для работы с этим кратким руководством вам понадобится:

* **Подписка Azure**: откройте ссылку на [бесплатную пробную версию Azure](https://azure.microsoft.com/offers/ms-azr-0044p/), чтобы создать учетную запись.
* **Azure Active Directory**: ваша подписка должна быть связана с клиентом Azure Active Directory, а учетная запись настроена в этом каталоге. Дополнительные сведения см. в руководстве по [аутентификации и настройке пользовательских разрешений](analysis-services-manage-users.md).

## <a name="import-azurermanalysisservices-module"></a>Импорт модуля AzureRm.AnalysisServices
Чтобы создать сервер в подписке, используйте модуль компонентов [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices). Загрузите модуль AzureRm.AnalysisServices в сеансе PowerShell.

```powershell
Import-Module AzureRM.AnalysisServices
```

## <a name="sign-in-to-azure"></a>Вход в Azure

Войдите в подписку Azure с помощью команды [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount). Выполните инструкции на экране.

```powershell
Add-AzureRmAccount
```

## <a name="create-a-resource-group"></a>Создание группы ресурсов
 
[Группа ресурсов Azure](../azure-resource-manager/resource-group-overview.md) — это логический контейнер, в котором ресурсы Azure развертываются и администрируются как группа. При создании сервера необходимо указать группу ресурсов в вашей подписке. Если у вас еще нет группы ресурсов, вы можете создать ее с помощью команды [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). В следующем примере создается группа ресурсов с именем `myResourceGroup` и в регионе "Западная часть США".

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
```

## <a name="create-a-server"></a>Создание сервера

Создайте сервер с помощью команды [New-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver). В следующем примере мы создадим сервер с именем MyServer в группе myResourceGroup, в регионе "Западная часть США", на уровне D1 и укажем philipc@adventureworks.com в качестве администратора сервера.

```powershell
New-AzureRmAnalysisServicesServer -ResourceGroupName "myResourceGroup" -Name "myServer" -Location West US -Sku D1 -Administrator "philipc@adventure-works.com"
```

## <a name="clean-up-resources"></a>Очистка ресурсов

Чтобы удалить сервер из подписки, используйте команду [AzureRmAnalysisServicesServer удаление](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver). Не удаляйте сервер, если вы планируете использовать другие шаблоны для быстрого начала работы и руководства в этой коллекции. В следующем примере показано, как удалить сервер, созданный на предыдущем шаге.


```powershell
Remove-AzureRmAnalysisServicesServer -Name "myServer" -ResourceGroupName "myResourceGroup"
```

## <a name="next-steps"></a>Дальнейшие действия
[Управление службами Azure Analysis Services с помощью PowerShell](analysis-services-powershell.md)   
[Развертывание модели из SSDT](analysis-services-deploy.md)   
[Создание модели на портале Azure](analysis-services-create-model-portal.md)