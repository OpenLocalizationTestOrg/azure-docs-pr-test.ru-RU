---
title: "Пример сценария PowerShell - передача файлов tooa веб-приложения с помощью протокола FTP aaaAzure | Документы Microsoft"
description: "Azure образец скрипта PowerShell - передача файлов tooa веб-приложения с помощью протокола FTP"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: b7d46d6f-44fd-454c-8008-87dab6eefbc1
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 32a0a529e94c1315cc6730faf23fca2693c50ffb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-tooa-web-app-using-ftp"></a><span data-ttu-id="88d22-103">Отправка файлов tooa веб-приложения с помощью протокола FTP</span><span class="sxs-lookup"><span data-stu-id="88d22-103">Upload files tooa web app using FTP</span></span>

<span data-ttu-id="88d22-104">Этот пример сценария создает веб-приложение со связанными ресурсами в службе приложений, а затем развертывает код веб-приложения с помощью протокола FTP (посредством [WebClient.UploadFile()](https://msdn.microsoft.com/library/ms144229.aspx)).</span><span class="sxs-lookup"><span data-stu-id="88d22-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code using FTP (via [WebClient.UploadFile()](https://msdn.microsoft.com/library/ms144229.aspx)).</span></span>

<span data-ttu-id="88d22-105">При необходимости установите Azure PowerShell с помощью инструкции hello, найденные в hello hello [руководство по Azure PowerShell](/powershell/azure/overview), а затем запустите `Login-AzureRmAccount` toocreate соединения с Azure.</span><span class="sxs-lookup"><span data-stu-id="88d22-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="88d22-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="88d22-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-ftp/deploy-ftp.ps1?highlight=1 "Upload files tooa web app using FTP")]

## <a name="clean-up-deployment"></a><span data-ttu-id="88d22-107">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="88d22-107">Clean up deployment</span></span> 

<span data-ttu-id="88d22-108">После выполнения сценария образец hello hello, следующая команда может быть группа ресурсов используется tooremove hello, веб-приложения и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="88d22-108">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name $webappname -Force
```

## <a name="script-explanation"></a><span data-ttu-id="88d22-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="88d22-109">Script explanation</span></span>

<span data-ttu-id="88d22-110">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="88d22-110">This script uses hello following commands.</span></span> <span data-ttu-id="88d22-111">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="88d22-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="88d22-112">Команда</span><span class="sxs-lookup"><span data-stu-id="88d22-112">Command</span></span> | <span data-ttu-id="88d22-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="88d22-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="88d22-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="88d22-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="88d22-115">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="88d22-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="88d22-116">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="88d22-116">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="88d22-117">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="88d22-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="88d22-118">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="88d22-118">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="88d22-119">Создает веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="88d22-119">Creates a web app.</span></span> |
| [<span data-ttu-id="88d22-120">Get-AzureRmWebAppPublishingProfile</span><span class="sxs-lookup"><span data-stu-id="88d22-120">Get-AzureRmWebAppPublishingProfile</span></span>](/powershell/module/azurerm.websites/get-azurermwebapppublishingprofile) | <span data-ttu-id="88d22-121">Получает профиль публикации веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="88d22-121">Get a web app's publishing profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="88d22-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="88d22-122">Next steps</span></span>

<span data-ttu-id="88d22-123">Дополнительные сведения о hello модуля Azure PowerShell см. в разделе [документация по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="88d22-123">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="88d22-124">Дополнительные примеры Azure Powershell для веб-приложениях службы приложений Azure можно найти в hello [примеры Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="88d22-124">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
