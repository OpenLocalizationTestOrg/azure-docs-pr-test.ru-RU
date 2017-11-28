---
title: "Пример сценария Azure PowerShell. Подключение веб-приложения к базе данных SQL | Документация Майкрософт"
description: "Пример сценария Azure PowerShell для подключения веб-приложения к базе данных SQL."
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 055440a9-fff1-49b2-b964-9c95b364e533
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 5312bf6b81d1cc48490b71c3f77323cca23e1559
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="connect-a-web-app-to-a-sql-database"></a><span data-ttu-id="f30c5-103">Подключение веб-приложения к базе данных SQL</span><span class="sxs-lookup"><span data-stu-id="f30c5-103">Connect a web app to a SQL database</span></span>

<span data-ttu-id="f30c5-104">В этой статье вы узнаете, как создать базу данных SQL и веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="f30c5-104">In this scenario you will learn how to create an Azure SQL database and an Azure web app.</span></span> <span data-ttu-id="f30c5-105">Затем вы свяжете базу данных SQL с веб-приложением, используя параметры приложения.</span><span class="sxs-lookup"><span data-stu-id="f30c5-105">Then you will link the SQL database to the web app using app settings.</span></span>

<span data-ttu-id="f30c5-106">При необходимости установите Azure PowerShell с помощью инструкции, приведенной в [руководстве Azure PowerShell](/powershell/azure/overview), а затем выполните команду `Login-AzureRmAccount`, чтобы создать подключение к Azure.</span><span class="sxs-lookup"><span data-stu-id="f30c5-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="f30c5-107">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="f30c5-107">Sample script</span></span>

<span data-ttu-id="f30c5-108">[!code-powershell[main](../../../powershell_scripts/app-service/connect-to-sql/connect-to-sql.ps1?highlight=13 "Подключение веб-приложения к базе данных SQL")]</span><span class="sxs-lookup"><span data-stu-id="f30c5-108">[!code-powershell[main](../../../powershell_scripts/app-service/connect-to-sql/connect-to-sql.ps1?highlight=13 "Connect a web app to a SQL database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="f30c5-109">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="f30c5-109">Clean up deployment</span></span> 

<span data-ttu-id="f30c5-110">Выполнив пример сценария, вы можете удалить группу ресурсов, веб-приложение и все связанные ресурсы, используя следующую команду.</span><span class="sxs-lookup"><span data-stu-id="f30c5-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="f30c5-111">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="f30c5-111">Script explanation</span></span>

<span data-ttu-id="f30c5-112">Этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="f30c5-112">This script uses the following commands.</span></span> <span data-ttu-id="f30c5-113">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="f30c5-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f30c5-114">Команда</span><span class="sxs-lookup"><span data-stu-id="f30c5-114">Command</span></span> | <span data-ttu-id="f30c5-115">Примечания</span><span class="sxs-lookup"><span data-stu-id="f30c5-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f30c5-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f30c5-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="f30c5-117">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="f30c5-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f30c5-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="f30c5-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="f30c5-119">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="f30c5-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="f30c5-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="f30c5-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="f30c5-121">Создает веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="f30c5-121">Creates a web app.</span></span> |
| [<span data-ttu-id="f30c5-122">New-AzureRMSQLServer</span><span class="sxs-lookup"><span data-stu-id="f30c5-122">New-AzureRMSQLServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="f30c5-123">Создает сервер базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="f30c5-123">Creates a SQL Database server.</span></span> |
| [<span data-ttu-id="f30c5-124">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="f30c5-124">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="f30c5-125">Создает правило брандмауэра для сервера базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="f30c5-125">Creates a firewall rule for a SQL Database server.</span></span> |
| [<span data-ttu-id="f30c5-126">New-AzureRMSQLDatabase</span><span class="sxs-lookup"><span data-stu-id="f30c5-126">New-AzureRMSQLDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="f30c5-127">Создает базу данных или эластичную базу данных.</span><span class="sxs-lookup"><span data-stu-id="f30c5-127">Creates a database or an elastic database.</span></span> |
| [<span data-ttu-id="f30c5-128">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="f30c5-128">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="f30c5-129">Изменяет конфигурацию веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="f30c5-129">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f30c5-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f30c5-130">Next steps</span></span>

<span data-ttu-id="f30c5-131">Дополнительные сведения о модуле Azure PowerShell см. в [документации по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f30c5-131">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="f30c5-132">Дополнительные примеры сценариев Azure PowerShell для веб-приложений службы приложений Azure доступны [здесь](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f30c5-132">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
