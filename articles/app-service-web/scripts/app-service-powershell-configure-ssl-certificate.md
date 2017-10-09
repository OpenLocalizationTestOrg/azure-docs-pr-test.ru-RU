---
title: "Образец скрипта PowerShell - aaaAzure привязки пользовательских веб-приложения tooa SSL сертификат | Документы Microsoft"
description: "Azure образец скрипта PowerShell - привязка пользовательского приложения web tooa сертификат SSL"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 23e83b74-614a-49a0-bc08-7542120eeec5
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 6e249ceedb9e2b8872dd0bc8b0aea0d718b28dab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="bind-a-custom-ssl-certificate-tooa-web-app"></a><span data-ttu-id="42d36-103">Привязка пользовательских веб-приложения tooa SSL сертификата</span><span class="sxs-lookup"><span data-stu-id="42d36-103">Bind a custom SSL certificate tooa web app</span></span>

<span data-ttu-id="42d36-104">Этот образец скрипта создает веб-приложения в службе приложений с его связанные ресурсы, а затем привязывает hello SSL-сертификат tooit имя пользовательского домена.</span><span class="sxs-lookup"><span data-stu-id="42d36-104">This sample script creates a web app in App Service with its related resources, then binds hello SSL certificate of a custom domain name tooit.</span></span> 

<span data-ttu-id="42d36-105">При необходимости установите Azure PowerShell с помощью инструкции hello, найденные в hello hello [руководство по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="42d36-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="42d36-106">Кроме того, убедитесь в следующем.</span><span class="sxs-lookup"><span data-stu-id="42d36-106">Also, ensure that:</span></span>

- <span data-ttu-id="42d36-107">Соединение с Azure был создан с помощью hello `az login` команды.</span><span class="sxs-lookup"><span data-stu-id="42d36-107">A connection with Azure has been created using hello `az login` command.</span></span>
- <span data-ttu-id="42d36-108">У вас есть страница настройки регистратора домена доступ tooyour DNS.</span><span class="sxs-lookup"><span data-stu-id="42d36-108">You have access tooyour domain registrar's DNS configuration page.</span></span>
- <span data-ttu-id="42d36-109">Получив допустимый. Сертификата PFX-файла и пароль для hello SSL требуется tooupload и привязку.</span><span class="sxs-lookup"><span data-stu-id="42d36-109">You have a valid .PFX file and its password for hello SSL certificate you want tooupload and bind.</span></span>

## <a name="sample-script"></a><span data-ttu-id="42d36-110">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="42d36-110">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate tooa web app")]

## <a name="clean-up-deployment"></a><span data-ttu-id="42d36-111">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="42d36-111">Clean up deployment</span></span> 

<span data-ttu-id="42d36-112">После выполнения сценария образец hello hello, следующая команда может быть группа ресурсов используется tooremove hello, веб-приложения и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="42d36-112">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="42d36-113">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="42d36-113">Script explanation</span></span>

<span data-ttu-id="42d36-114">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="42d36-114">This script uses hello following commands.</span></span> <span data-ttu-id="42d36-115">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="42d36-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="42d36-116">Команда</span><span class="sxs-lookup"><span data-stu-id="42d36-116">Command</span></span> | <span data-ttu-id="42d36-117">Примечания</span><span class="sxs-lookup"><span data-stu-id="42d36-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="42d36-118">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="42d36-118">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="42d36-119">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="42d36-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="42d36-120">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="42d36-120">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="42d36-121">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="42d36-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="42d36-122">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="42d36-122">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="42d36-123">Создает веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="42d36-123">Creates a web app.</span></span> |
| [<span data-ttu-id="42d36-124">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="42d36-124">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="42d36-125">Изменяет его цен toochange плана служб приложений.</span><span class="sxs-lookup"><span data-stu-id="42d36-125">Modifies an App Service plan toochange its pricing tier.</span></span> |
| [<span data-ttu-id="42d36-126">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="42d36-126">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="42d36-127">Изменяет конфигурацию веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="42d36-127">Modifies a web app's configuration.</span></span> |
| [<span data-ttu-id="42d36-128">New-AzureRmWebAppSSLBinding</span><span class="sxs-lookup"><span data-stu-id="42d36-128">New-AzureRmWebAppSSLBinding</span></span>](/powershell/module/azurerm.websites/new-azurermwebappsslbinding) | <span data-ttu-id="42d36-129">Создает привязку SSL-сертификата к веб-приложению.</span><span class="sxs-lookup"><span data-stu-id="42d36-129">Creates an SSL certificate binding for a web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="42d36-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="42d36-130">Next steps</span></span>

<span data-ttu-id="42d36-131">Дополнительные сведения о hello модуля Azure PowerShell см. в разделе [документация по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="42d36-131">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="42d36-132">Дополнительные примеры Azure Powershell для веб-приложениях службы приложений Azure можно найти в hello [примеры Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="42d36-132">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
