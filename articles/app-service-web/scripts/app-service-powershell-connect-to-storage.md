---
title: "Пример сценария PowerShell - aaaAzure подключения приложения web tooa учетной записи хранилища | Документы Microsoft"
description: "Сценарий Azure PowerShell пример — подключить учетную запись хранения tooa web app"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: e4831bdc-2068-4883-9474-0b34c2e3e255
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 07693366d32fbaefe92c18df67ded81661e1a2df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-storage-account"></a><span data-ttu-id="c1bec-103">Подключение приложения web tooa учетной записи хранилища</span><span class="sxs-lookup"><span data-stu-id="c1bec-103">Connect a web app tooa storage account</span></span>

<span data-ttu-id="c1bec-104">В этом сценарии вы узнаете, как toocreate учетную запись хранилища Azure и Azure веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="c1bec-104">In this scenario you will learn how toocreate an Azure storage account and an Azure web app.</span></span> <span data-ttu-id="c1bec-105">Затем будет связан hello хранилища учетной записи toohello веб-приложения с помощью параметров приложения.</span><span class="sxs-lookup"><span data-stu-id="c1bec-105">Then you will link hello storage account toohello web app using app settings.</span></span>

<span data-ttu-id="c1bec-106">При необходимости установите Azure PowerShell с помощью инструкции hello, найденные в hello hello [руководство по Azure PowerShell](/powershell/azure/overview), а затем запустите `Login-AzureRmAccount` toocreate соединения с Azure.</span><span class="sxs-lookup"><span data-stu-id="c1bec-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="c1bec-107">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="c1bec-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/connect-to-storage/connect-to-storage.ps1 "Connect a web app tooa storage account")]

## <a name="clean-up-deployment"></a><span data-ttu-id="c1bec-108">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="c1bec-108">Clean up deployment</span></span> 

<span data-ttu-id="c1bec-109">После выполнения сценария образец hello hello, следующая команда может быть группа ресурсов используется tooremove hello, веб-приложения и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="c1bec-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="c1bec-110">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="c1bec-110">Script explanation</span></span>

<span data-ttu-id="c1bec-111">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="c1bec-111">This script uses hello following commands.</span></span> <span data-ttu-id="c1bec-112">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="c1bec-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c1bec-113">Команда</span><span class="sxs-lookup"><span data-stu-id="c1bec-113">Command</span></span> | <span data-ttu-id="c1bec-114">Примечания</span><span class="sxs-lookup"><span data-stu-id="c1bec-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c1bec-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c1bec-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="c1bec-116">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="c1bec-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c1bec-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="c1bec-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="c1bec-118">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="c1bec-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="c1bec-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="c1bec-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="c1bec-120">Создает веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="c1bec-120">Creates a web app.</span></span> |
| [<span data-ttu-id="c1bec-121">New-AzureRMStorageAccount</span><span class="sxs-lookup"><span data-stu-id="c1bec-121">New-AzureRMStorageAccount</span></span>](/powershell/module/azurerm.storage/new-azurermstorageaccount) | <span data-ttu-id="c1bec-122">Создает учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="c1bec-122">Creates a Storage account.</span></span> |
| [<span data-ttu-id="c1bec-123">Get-AzureRMStorageAccountKey</span><span class="sxs-lookup"><span data-stu-id="c1bec-123">Get-AzureRMStorageAccountKey</span></span>](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) | <span data-ttu-id="c1bec-124">Возвращает hello клавиши доступа для учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="c1bec-124">Gets hello access keys for an Azure Storage account.</span></span> |
| [<span data-ttu-id="c1bec-125">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="c1bec-125">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="c1bec-126">Изменяет конфигурацию веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="c1bec-126">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c1bec-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c1bec-127">Next steps</span></span>

<span data-ttu-id="c1bec-128">Дополнительные сведения о hello модуля Azure PowerShell см. в разделе [документация по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c1bec-128">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="c1bec-129">Дополнительные примеры Azure Powershell для веб-приложениях службы приложений Azure можно найти в hello [примеры Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c1bec-129">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
