---
title: "Пример сценария Azure PowerShell. Подключение веб-приложения к учетной записи хранения | Документация Майкрософт"
description: "Пример сценария Azure PowerShell для подключения веб-приложения к учетной записи хранения."
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
ms.openlocfilehash: 481f3efdb1cbbeba328183da7e320c7e5b819b3a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="connect-a-web-app-to-a-storage-account"></a><span data-ttu-id="4fb21-103">Подключение веб-приложения к учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="4fb21-103">Connect a web app to a storage account</span></span>

<span data-ttu-id="4fb21-104">В этой статье вы узнаете, как создать учетную запись хранения и веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="4fb21-104">In this scenario you will learn how to create an Azure storage account and an Azure web app.</span></span> <span data-ttu-id="4fb21-105">Затем вы свяжете учетную запись хранения с веб-приложением, используя параметры приложения.</span><span class="sxs-lookup"><span data-stu-id="4fb21-105">Then you will link the storage account to the web app using app settings.</span></span>

<span data-ttu-id="4fb21-106">При необходимости установите Azure PowerShell с помощью инструкции, приведенной в [руководстве Azure PowerShell](/powershell/azure/overview), а затем выполните команду `Login-AzureRmAccount`, чтобы создать подключение к Azure.</span><span class="sxs-lookup"><span data-stu-id="4fb21-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="4fb21-107">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="4fb21-107">Sample script</span></span>

<span data-ttu-id="4fb21-108">[!code-powershell[main](../../../powershell_scripts/app-service/connect-to-storage/connect-to-storage.ps1 "Подключение веб-приложения к учетной записи хранения")]</span><span class="sxs-lookup"><span data-stu-id="4fb21-108">[!code-powershell[main](../../../powershell_scripts/app-service/connect-to-storage/connect-to-storage.ps1 "Connect a web app to a storage account")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="4fb21-109">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="4fb21-109">Clean up deployment</span></span> 

<span data-ttu-id="4fb21-110">Выполнив пример сценария, вы можете удалить группу ресурсов, веб-приложение и все связанные ресурсы, используя следующую команду.</span><span class="sxs-lookup"><span data-stu-id="4fb21-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="4fb21-111">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="4fb21-111">Script explanation</span></span>

<span data-ttu-id="4fb21-112">Этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="4fb21-112">This script uses the following commands.</span></span> <span data-ttu-id="4fb21-113">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="4fb21-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="4fb21-114">Команда</span><span class="sxs-lookup"><span data-stu-id="4fb21-114">Command</span></span> | <span data-ttu-id="4fb21-115">Примечания</span><span class="sxs-lookup"><span data-stu-id="4fb21-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4fb21-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4fb21-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="4fb21-117">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="4fb21-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4fb21-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="4fb21-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="4fb21-119">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="4fb21-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="4fb21-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="4fb21-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="4fb21-121">Создает веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="4fb21-121">Creates a web app.</span></span> |
| [<span data-ttu-id="4fb21-122">New-AzureRMStorageAccount</span><span class="sxs-lookup"><span data-stu-id="4fb21-122">New-AzureRMStorageAccount</span></span>](/powershell/module/azurerm.storage/new-azurermstorageaccount) | <span data-ttu-id="4fb21-123">Создает учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="4fb21-123">Creates a Storage account.</span></span> |
| [<span data-ttu-id="4fb21-124">Get-AzureRMStorageAccountKey</span><span class="sxs-lookup"><span data-stu-id="4fb21-124">Get-AzureRMStorageAccountKey</span></span>](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) | <span data-ttu-id="4fb21-125">Выводит список ключей доступа для учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="4fb21-125">Gets the access keys for an Azure Storage account.</span></span> |
| [<span data-ttu-id="4fb21-126">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="4fb21-126">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="4fb21-127">Изменяет конфигурацию веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="4fb21-127">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4fb21-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4fb21-128">Next steps</span></span>

<span data-ttu-id="4fb21-129">Дополнительные сведения о модуле Azure PowerShell см. в [документации по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4fb21-129">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="4fb21-130">Дополнительные примеры сценариев Azure PowerShell для веб-приложений службы приложений Azure доступны [здесь](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4fb21-130">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
