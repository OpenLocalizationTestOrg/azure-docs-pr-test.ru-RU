---
title: "Образец скрипта PowerShell - aaaAzure подключения базы данных SQL web app tooa | Документы Microsoft"
description: "Сценарий Azure PowerShell пример — подключить приложение веб-tooa база данных SQL"
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
ms.openlocfilehash: 8f80b940378d020cbcaec2c1bbc28bae1a3ef35a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-sql-database"></a><span data-ttu-id="162bb-103">Подключение приложения веб-tooa база данных SQL</span><span class="sxs-lookup"><span data-stu-id="162bb-103">Connect a web app tooa SQL database</span></span>

<span data-ttu-id="162bb-104">В этом сценарии вы узнаете, как toocreate базы данных Azure SQL и Azure веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="162bb-104">In this scenario you will learn how toocreate an Azure SQL database and an Azure web app.</span></span> <span data-ttu-id="162bb-105">Затем будет связан hello SQL базы данных toohello веб-приложения с помощью параметров приложения.</span><span class="sxs-lookup"><span data-stu-id="162bb-105">Then you will link hello SQL database toohello web app using app settings.</span></span>

<span data-ttu-id="162bb-106">При необходимости установите Azure PowerShell с помощью инструкции hello, найденные в hello hello [руководство по Azure PowerShell](/powershell/azure/overview), а затем запустите `Login-AzureRmAccount` toocreate соединения с Azure.</span><span class="sxs-lookup"><span data-stu-id="162bb-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="162bb-107">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="162bb-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/connect-to-sql/connect-to-sql.ps1?highlight=13 "Connect a web app tooa SQL database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="162bb-108">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="162bb-108">Clean up deployment</span></span> 

<span data-ttu-id="162bb-109">После выполнения сценария образец hello hello, следующая команда может быть группа ресурсов используется tooremove hello, веб-приложения и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="162bb-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="162bb-110">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="162bb-110">Script explanation</span></span>

<span data-ttu-id="162bb-111">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="162bb-111">This script uses hello following commands.</span></span> <span data-ttu-id="162bb-112">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="162bb-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="162bb-113">Команда</span><span class="sxs-lookup"><span data-stu-id="162bb-113">Command</span></span> | <span data-ttu-id="162bb-114">Примечания</span><span class="sxs-lookup"><span data-stu-id="162bb-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="162bb-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="162bb-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="162bb-116">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="162bb-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="162bb-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="162bb-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="162bb-118">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="162bb-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="162bb-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="162bb-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="162bb-120">Создает веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="162bb-120">Creates a web app.</span></span> |
| [<span data-ttu-id="162bb-121">New-AzureRMSQLServer</span><span class="sxs-lookup"><span data-stu-id="162bb-121">New-AzureRMSQLServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="162bb-122">Создает сервер базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="162bb-122">Creates a SQL Database server.</span></span> |
| [<span data-ttu-id="162bb-123">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="162bb-123">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="162bb-124">Создает правило брандмауэра для сервера базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="162bb-124">Creates a firewall rule for a SQL Database server.</span></span> |
| [<span data-ttu-id="162bb-125">New-AzureRMSQLDatabase</span><span class="sxs-lookup"><span data-stu-id="162bb-125">New-AzureRMSQLDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="162bb-126">Создает базу данных или эластичную базу данных.</span><span class="sxs-lookup"><span data-stu-id="162bb-126">Creates a database or an elastic database.</span></span> |
| [<span data-ttu-id="162bb-127">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="162bb-127">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="162bb-128">Изменяет конфигурацию веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="162bb-128">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="162bb-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="162bb-129">Next steps</span></span>

<span data-ttu-id="162bb-130">Дополнительные сведения о hello модуля Azure PowerShell см. в разделе [документация по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="162bb-130">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="162bb-131">Дополнительные примеры Azure Powershell для веб-приложениях службы приложений Azure можно найти в hello [примеры Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="162bb-131">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
