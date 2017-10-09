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
# <a name="create-an-azure-analysis-services-server-by-using-powershell"></a><span data-ttu-id="06e87-103">Создание сервера Azure Analysis Services с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="06e87-103">Create an Azure Analysis Services server by using PowerShell</span></span>

<span data-ttu-id="06e87-104">Это краткое руководство содержит сведения об использовании PowerShell из командной строки toocreate hello сервер служб Azure Analysis Services в [группы ресурсов Azure](../azure-resource-manager/resource-group-overview.md) в вашей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="06e87-104">This quickstart describes using PowerShell from hello command line toocreate an Azure Analysis Services server in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in your Azure subscription.</span></span>

<span data-ttu-id="06e87-105">Для этой задачи требуется модуль Azure PowerShell 4.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="06e87-105">This task requires Azure PowerShell module version 4.0 or later.</span></span> <span data-ttu-id="06e87-106">версия toofind hello, запустите ` Get-Module -ListAvailable AzureRM`.</span><span class="sxs-lookup"><span data-stu-id="06e87-106">toofind hello version, run ` Get-Module -ListAvailable AzureRM`.</span></span> <span data-ttu-id="06e87-107">tooinstall или обновления, см. в [установите Azure PowerShell модуль](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="06e87-107">tooinstall or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> 

> [!NOTE]
> <span data-ttu-id="06e87-108">При создании сервера вам могут выставляться счета за новую службу.</span><span class="sxs-lookup"><span data-stu-id="06e87-108">Creating a server might result in a new billable service.</span></span> <span data-ttu-id="06e87-109">toolearn более, в разделе [цены служб Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="06e87-109">toolearn more, see [Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="06e87-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="06e87-110">Prerequisites</span></span>
<span data-ttu-id="06e87-111">toocomplete краткого руководства, необходимо:</span><span class="sxs-lookup"><span data-stu-id="06e87-111">toocomplete this quickstart, you need:</span></span>

* <span data-ttu-id="06e87-112">**Подписка Azure**: посетите [бесплатная пробная версия](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate учетную запись.</span><span class="sxs-lookup"><span data-stu-id="06e87-112">**Azure subscription**: Visit [Azure Free Trial](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate an account.</span></span>
* <span data-ttu-id="06e87-113">**Azure Active Directory**: ваша подписка должна быть связана с клиентом Azure Active Directory, а учетная запись настроена в этом каталоге.</span><span class="sxs-lookup"><span data-stu-id="06e87-113">**Azure Active Directory**: Your subscription must be associated with an Azure Active Directory tenant and you must have an account in that directory.</span></span> <span data-ttu-id="06e87-114">toolearn более, в разделе [проверки подлинности и пользовательские разрешения](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="06e87-114">toolearn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>

## <a name="import-azurermanalysisservices-module"></a><span data-ttu-id="06e87-115">Импорт модуля AzureRm.AnalysisServices</span><span class="sxs-lookup"><span data-stu-id="06e87-115">Import AzureRm.AnalysisServices module</span></span>
<span data-ttu-id="06e87-116">toocreate сервера в вашей подписке, используйте hello [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices) компонент модуля.</span><span class="sxs-lookup"><span data-stu-id="06e87-116">toocreate a server in your subscription, you use hello [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices)  component module.</span></span> <span data-ttu-id="06e87-117">Загрузите модуль AzureRm.AnalysisServices hello в сеансе PowerShell.</span><span class="sxs-lookup"><span data-stu-id="06e87-117">Load hello AzureRm.AnalysisServices module into your PowerShell session.</span></span>

```powershell
Import-Module AzureRM.AnalysisServices
```

## <a name="sign-in-tooazure"></a><span data-ttu-id="06e87-118">Войдите в tooAzure</span><span class="sxs-lookup"><span data-stu-id="06e87-118">Sign in tooAzure</span></span>

<span data-ttu-id="06e87-119">Войти в tooyour подписки Azure, используя hello [AzureRmAccount добавить](/powershell/module/azurerm.profile/add-azurermaccount) команды.</span><span class="sxs-lookup"><span data-stu-id="06e87-119">Sign in tooyour Azure subscription by using hello [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) command.</span></span> <span data-ttu-id="06e87-120">Выполните hello на экране инструкциям.</span><span class="sxs-lookup"><span data-stu-id="06e87-120">Follow hello on-screen directions.</span></span>

```powershell
Add-AzureRmAccount
```

## <a name="create-a-resource-group"></a><span data-ttu-id="06e87-121">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="06e87-121">Create a resource group</span></span>
 
<span data-ttu-id="06e87-122">[Группа ресурсов Azure](../azure-resource-manager/resource-group-overview.md) — это логический контейнер, в котором ресурсы Azure развертываются и администрируются как группа.</span><span class="sxs-lookup"><span data-stu-id="06e87-122">An [Azure resource group](../azure-resource-manager/resource-group-overview.md) is a logical container where Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="06e87-123">При создании сервера необходимо указать группу ресурсов в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="06e87-123">When you create your server, you must specify a resource group in your subscription.</span></span> <span data-ttu-id="06e87-124">Если вы еще нет группы ресурсов, можно создать новую с помощью hello [New AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) команды.</span><span class="sxs-lookup"><span data-stu-id="06e87-124">If you do not already have a resource group, you can create a new one by using hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> <span data-ttu-id="06e87-125">Hello следующий пример создает группу ресурсов с именем `myResourceGroup` в hello Запад США.</span><span class="sxs-lookup"><span data-stu-id="06e87-125">hello following example creates a resource group named `myResourceGroup` in hello West US region.</span></span>

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
```

## <a name="create-a-server"></a><span data-ttu-id="06e87-126">Создание сервера</span><span class="sxs-lookup"><span data-stu-id="06e87-126">Create a server</span></span>

<span data-ttu-id="06e87-127">Создание нового сервера с помощью hello [New AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) команды.</span><span class="sxs-lookup"><span data-stu-id="06e87-127">Create a new server by using hello [New-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) command.</span></span> <span data-ttu-id="06e87-128">Hello следующий пример создает на сервере MyServer в myResourceGroup в регионе hello Запад США, на уровне hello D1 и указывает philipc@adventureworks.com администратор сервера.</span><span class="sxs-lookup"><span data-stu-id="06e87-128">hello following example creates a server named myServer in myResourceGroup, in hello West US region, at hello D1 tier, and specifies philipc@adventureworks.com as a server administrator.</span></span>

```powershell
New-AzureRmAnalysisServicesServer -ResourceGroupName "myResourceGroup" -Name "myServer" -Location West US -Sku D1 -Administrator "philipc@adventure-works.com"
```

## <a name="clean-up-resources"></a><span data-ttu-id="06e87-129">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="06e87-129">Clean up resources</span></span>

<span data-ttu-id="06e87-130">Можно удалить сервер hello из подписки с помощью hello [AzureRmAnalysisServicesServer удаление](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) команды.</span><span class="sxs-lookup"><span data-stu-id="06e87-130">You can remove hello server from your subscription by using hello [Remove-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) command.</span></span> <span data-ttu-id="06e87-131">Не удаляйте сервер, если вы планируете использовать другие шаблоны для быстрого начала работы и руководства в этой коллекции.</span><span class="sxs-lookup"><span data-stu-id="06e87-131">If you continue with other quickstarts and tutorials in this collection, do not remove your server.</span></span> <span data-ttu-id="06e87-132">Hello следующий пример удаляет hello server на предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="06e87-132">hello following example removes hello server created in hello previous step.</span></span>


```powershell
Remove-AzureRmAnalysisServicesServer -Name "myServer" -ResourceGroupName "myResourceGroup"
```

## <a name="next-steps"></a><span data-ttu-id="06e87-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="06e87-133">Next steps</span></span>
<span data-ttu-id="06e87-134">[Управление службами Azure Analysis Services с помощью PowerShell](analysis-services-powershell.md) </span><span class="sxs-lookup"><span data-stu-id="06e87-134">[Manage Azure Analysis Services with PowerShell](analysis-services-powershell.md) </span></span>  
<span data-ttu-id="06e87-135">[Развертывание модели из SSDT](analysis-services-deploy.md) </span><span class="sxs-lookup"><span data-stu-id="06e87-135">[Deploy a model from SSDT](analysis-services-deploy.md) </span></span>  
[<span data-ttu-id="06e87-136">Создание модели на портале Azure</span><span class="sxs-lookup"><span data-stu-id="06e87-136">Create a model in Azure portal</span></span>](analysis-services-create-model-portal.md)