---
title: "Удаление инструмента заданий обработки эластичных баз данных"
description: "Удаление инструмента заданий обработки эластичных баз данных"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: bfc9d820-edbd-4fca-bfbf-1f339cfcc448
ms.service: sql-database
ms.workload: sql-database
ms.custom: scale out apps
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: ae7f0bce452a0a86f6f1e4d9b0c93a0fa1727f21
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="uninstall-elastic-database-jobs-components"></a><span data-ttu-id="c6d00-103">Удаление компонентов заданий обработки эластичных баз данных.</span><span class="sxs-lookup"><span data-stu-id="c6d00-103">Uninstall Elastic Database jobs components</span></span>
<span data-ttu-id="c6d00-104">**заданий обработки эластичных баз данных** можно удалить с помощью портала или PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c6d00-104">**Elastic Database jobs** components can be uninstalled using either the Portal or PowerShell.</span></span>

## <a name="uninstall-elastic-database-jobs-components-using-the-azure-portal"></a><span data-ttu-id="c6d00-105">Удаление компонентов заданий обработки эластичных баз данных с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="c6d00-105">Uninstall Elastic Database jobs components using the Azure portal</span></span>
1. <span data-ttu-id="c6d00-106">Откройте [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c6d00-106">Open the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="c6d00-107">Перейдите к подписке, которая содержит компоненты **заданий обработки эластичных баз данных** , то есть подписку, в которой они были установлены.</span><span class="sxs-lookup"><span data-stu-id="c6d00-107">Navigate to the subscription that contains **Elastic Database jobs** components, namely the subscription in which Elastic Database jobs components were installed.</span></span>
3. <span data-ttu-id="c6d00-108">Щелкните **Обзор** и **Группы ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="c6d00-108">Click **Browse** and click **Resource groups**.</span></span>
4. <span data-ttu-id="c6d00-109">Выберите группу ресурсов с именем __ElasticDatabaseJob.</span><span class="sxs-lookup"><span data-stu-id="c6d00-109">Select the resource group named "__ElasticDatabaseJob".</span></span>
5. <span data-ttu-id="c6d00-110">Удалите ее.</span><span class="sxs-lookup"><span data-stu-id="c6d00-110">Delete the resource group.</span></span>

## <a name="uninstall--elastic-database-jobs-components-using-powershell"></a><span data-ttu-id="c6d00-111">Удаление компонентов заданий обработки эластичных баз данных с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="c6d00-111">Uninstall  Elastic Database jobs components using PowerShell</span></span>
1. <span data-ttu-id="c6d00-112">Откройте командную строку Microsoft Azure PowerShell и перейдите в подкаталог tools в папке Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x: введите команду **cd tools**.</span><span class="sxs-lookup"><span data-stu-id="c6d00-112">Launch a Microsoft Azure PowerShell command window and navigate to the tools sub-directory under the Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x folder: Type **cd tools**.</span></span>
   
     <span data-ttu-id="c6d00-113">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools</span><span class="sxs-lookup"><span data-stu-id="c6d00-113">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools</span></span>
2. <span data-ttu-id="c6d00-114">Запустите сценарий PowerShell .\UninstallElasticDatabaseJobs.ps1.</span><span class="sxs-lookup"><span data-stu-id="c6d00-114">Execute the .\UninstallElasticDatabaseJobs.ps1 PowerShell script.</span></span>
   
     <span data-ttu-id="c6d00-115">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\UninstallElasticDatabaseJobs.ps1   PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\UninstallElasticDatabaseJobs.ps1</span><span class="sxs-lookup"><span data-stu-id="c6d00-115">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\UninstallElasticDatabaseJobs.ps1   PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\UninstallElasticDatabaseJobs.ps1</span></span>

<span data-ttu-id="c6d00-116">Или просто запустите следующий сценарий, если для установки компонентов использовались значения по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="c6d00-116">Or simply, execute the following script, assuming default values where used on installation of the components:</span></span>

        $ResourceGroupName = "__ElasticDatabaseJob"
        Switch-AzureMode AzureResourceManager

        $resourceGroup = Get-AzureResourceGroup -Name $ResourceGroupName
        if(!$resourceGroup)
        {
            Write-Host "The Azure Resource Group: $ResourceGroupName has already been deleted.  Elastic database job components are uninstalled."
            return
        }

        Write-Host "Removing the Azure Resource Group: $ResourceGroupName.  This may take a few minutes.”
        Remove-AzureResourceGroup -Name $ResourceGroupName -Force
        Write-Host "Completed removing the Azure Resource Group: $ResourceGroupName.  Elastic database job compoennts are now uninstalled."

## <a name="next-steps"></a><span data-ttu-id="c6d00-117">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c6d00-117">Next steps</span></span>
<span data-ttu-id="c6d00-118">Сведения о повторной установке службы можно найти в статье [Установка компонентов службы заданий обработки эластичных баз данных](sql-database-elastic-jobs-service-installation.md)</span><span class="sxs-lookup"><span data-stu-id="c6d00-118">To re-install Elastic Database jobs, see [Installing the Elastic Database job service](sql-database-elastic-jobs-service-installation.md)</span></span>

<span data-ttu-id="c6d00-119">Общие сведения о заданиях обработки эластичных баз данных см. в статье [Управление масштабируемыми облачными базами данных](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c6d00-119">For an overview of Elastic Database jobs, see [Elastic Database jobs overview](sql-database-elastic-jobs-overview.md).</span></span>

<!--Image references-->


