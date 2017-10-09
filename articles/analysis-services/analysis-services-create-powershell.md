---
title: "aaaCreate сервер служб Azure Analysis Services с помощью PowerShell | Документы Microsoft"
description: "Узнайте, как toocreate служб Azure Analysis Services с помощью PowerShell"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 08/01/2017
ms.author: owend
ms.custom: mvc
ms.openlocfilehash: 269b78983410f773d47c4cea34d6d353b19f9e91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-analysis-services-server-by-using-powershell"></a>Создание сервера Azure Analysis Services с помощью PowerShell

Это краткое руководство содержит сведения об использовании PowerShell из командной строки toocreate hello сервер служб Azure Analysis Services в [группы ресурсов Azure](../azure-resource-manager/resource-group-overview.md) в вашей подписке Azure.

Для этой задачи требуется модуль Azure PowerShell 4.0 или более поздней версии. версия toofind hello, запустите ` Get-Module -ListAvailable AzureRM`. tooinstall или обновления, см. в [установите Azure PowerShell модуль](/powershell/azure/install-azurerm-ps). 

> [!NOTE]
> При создании сервера вам могут выставляться счета за новую службу. toolearn более, в разделе [цены служб Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).

## <a name="prerequisites"></a>Предварительные требования
toocomplete краткого руководства, необходимо:

* **Подписка Azure**: посетите [бесплатная пробная версия](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate учетную запись.
* **Azure Active Directory**: ваша подписка должна быть связана с клиентом Azure Active Directory, а учетная запись настроена в этом каталоге. toolearn более, в разделе [проверки подлинности и пользовательские разрешения](analysis-services-manage-users.md).

## <a name="import-azurermanalysisservices-module"></a>Импорт модуля AzureRm.AnalysisServices
toocreate сервера в вашей подписке, используйте hello [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices) компонент модуля. Загрузите модуль AzureRm.AnalysisServices hello в сеансе PowerShell.

```powershell
Import-Module AzureRM.AnalysisServices
```

## <a name="sign-in-tooazure"></a>Войдите в tooAzure

Войти в tooyour подписки Azure, используя hello [AzureRmAccount добавить](/powershell/module/azurerm.profile/add-azurermaccount) команды. Выполните hello на экране инструкциям.

```powershell
Add-AzureRmAccount
```

## <a name="create-a-resource-group"></a>Создание группы ресурсов
 
[Группа ресурсов Azure](../azure-resource-manager/resource-group-overview.md) — это логический контейнер, в котором ресурсы Azure развертываются и администрируются как группа. При создании сервера необходимо указать группу ресурсов в вашей подписке. Если вы еще нет группы ресурсов, можно создать новую с помощью hello [New AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) команды. Hello следующий пример создает группу ресурсов с именем `myResourceGroup` в hello Запад США.

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
```

## <a name="create-a-server"></a>Создание сервера

Создание нового сервера с помощью hello [New AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) команды. Hello следующий пример создает на сервере MyServer в myResourceGroup в регионе hello Запад США, на уровне hello D1 и указывает philipc@adventureworks.com администратор сервера.

```powershell
New-AzureRmAnalysisServicesServer -ResourceGroupName "myResourceGroup" -Name "myServer" -Location West US -Sku D1 -Administrator "philipc@adventure-works.com"
```

## <a name="clean-up-resources"></a>Очистка ресурсов

Можно удалить сервер hello из подписки с помощью hello [AzureRmAnalysisServicesServer удаление](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) команды. Не удаляйте сервер, если вы планируете использовать другие шаблоны для быстрого начала работы и руководства в этой коллекции. Hello следующий пример удаляет hello server на предыдущем шаге hello.


```powershell
Remove-AzureRmAnalysisServicesServer -Name "myServer" -ResourceGroupName "myResourceGroup"
```

## <a name="next-steps"></a>Дальнейшие действия
[Управление службами Azure Analysis Services с помощью PowerShell](analysis-services-powershell.md)   
[Развертывание модели из SSDT](analysis-services-deploy.md)   
[Создание модели на портале Azure](analysis-services-create-model-portal.md)