---
title: "Средство заданий эластичных баз данных toouninstall aaaHow"
description: "Как toouninstall hello средство заданий эластичных баз данных"
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
ms.openlocfilehash: 3bc1e889d5042bc3eaa9fd9da89816737e0b8df8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="uninstall-elastic-database-jobs-components"></a><span data-ttu-id="38ba3-103">Удаление компонентов заданий обработки эластичных баз данных.</span><span class="sxs-lookup"><span data-stu-id="38ba3-103">Uninstall Elastic Database jobs components</span></span>
<span data-ttu-id="38ba3-104">**Заданий эластичных баз данных** компоненты можно удалить с помощью портала hello или PowerShell.</span><span class="sxs-lookup"><span data-stu-id="38ba3-104">**Elastic Database jobs** components can be uninstalled using either hello Portal or PowerShell.</span></span>

## <a name="uninstall-elastic-database-jobs-components-using-hello-azure-portal"></a><span data-ttu-id="38ba3-105">Удаление компонентов заданий эластичных баз данных с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="38ba3-105">Uninstall Elastic Database jobs components using hello Azure portal</span></span>
1. <span data-ttu-id="38ba3-106">Откройте hello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="38ba3-106">Open hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="38ba3-107">Перейдите toohello подписку, содержащую **заданий эластичных баз данных** компоненты, а именно: hello подписки, в какие эластичной базы данных были установлены компоненты заданий.</span><span class="sxs-lookup"><span data-stu-id="38ba3-107">Navigate toohello subscription that contains **Elastic Database jobs** components, namely hello subscription in which Elastic Database jobs components were installed.</span></span>
3. <span data-ttu-id="38ba3-108">Щелкните **Обзор** и **Группы ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="38ba3-108">Click **Browse** and click **Resource groups**.</span></span>
4. <span data-ttu-id="38ba3-109">Привет, выберите группу ресурсов с именем «__ElasticDatabaseJob».</span><span class="sxs-lookup"><span data-stu-id="38ba3-109">Select hello resource group named "__ElasticDatabaseJob".</span></span>
5. <span data-ttu-id="38ba3-110">Удалите группу ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="38ba3-110">Delete hello resource group.</span></span>

## <a name="uninstall--elastic-database-jobs-components-using-powershell"></a><span data-ttu-id="38ba3-111">Удаление компонентов заданий обработки эластичных баз данных с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="38ba3-111">Uninstall  Elastic Database jobs components using PowerShell</span></span>
1. <span data-ttu-id="38ba3-112">Запустите командную строку Microsoft Azure PowerShell и перейдите toohello средства вложенный каталог в папке Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x hello: тип **средства cd**.</span><span class="sxs-lookup"><span data-stu-id="38ba3-112">Launch a Microsoft Azure PowerShell command window and navigate toohello tools sub-directory under hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x folder: Type **cd tools**.</span></span>
   
     <span data-ttu-id="38ba3-113">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools</span><span class="sxs-lookup"><span data-stu-id="38ba3-113">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools</span></span>
2. <span data-ttu-id="38ba3-114">Выполните сценарий PowerShell.\UninstallElasticDatabaseJobs.ps1 hello.</span><span class="sxs-lookup"><span data-stu-id="38ba3-114">Execute hello .\UninstallElasticDatabaseJobs.ps1 PowerShell script.</span></span>
   
     <span data-ttu-id="38ba3-115">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\UninstallElasticDatabaseJobs.ps1   PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\UninstallElasticDatabaseJobs.ps1</span><span class="sxs-lookup"><span data-stu-id="38ba3-115">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\UninstallElasticDatabaseJobs.ps1   PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\UninstallElasticDatabaseJobs.ps1</span></span>

<span data-ttu-id="38ba3-116">Или выполните hello следующий сценарий, при условии, что по умолчанию значения, когда используется для установки компонентов hello:</span><span class="sxs-lookup"><span data-stu-id="38ba3-116">Or simply, execute hello following script, assuming default values where used on installation of hello components:</span></span>

        $ResourceGroupName = "__ElasticDatabaseJob"
        Switch-AzureMode AzureResourceManager

        $resourceGroup = Get-AzureResourceGroup -Name $ResourceGroupName
        if(!$resourceGroup)
        {
            Write-Host "hello Azure Resource Group: $ResourceGroupName has already been deleted.  Elastic database job components are uninstalled."
            return
        }

        Write-Host "Removing hello Azure Resource Group: $ResourceGroupName.  This may take a few minutes.”
        Remove-AzureResourceGroup -Name $ResourceGroupName -Force
        Write-Host "Completed removing hello Azure Resource Group: $ResourceGroupName.  Elastic database job compoennts are now uninstalled."

## <a name="next-steps"></a><span data-ttu-id="38ba3-117">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="38ba3-117">Next steps</span></span>
<span data-ttu-id="38ba3-118">заданий toore install эластичной базы данных, в разделе [Установка службы задания hello эластичной базы данных](sql-database-elastic-jobs-service-installation.md)</span><span class="sxs-lookup"><span data-stu-id="38ba3-118">toore-install Elastic Database jobs, see [Installing hello Elastic Database job service](sql-database-elastic-jobs-service-installation.md)</span></span>

<span data-ttu-id="38ba3-119">Общие сведения о заданиях обработки эластичных баз данных см. в статье [Управление масштабируемыми облачными базами данных](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="38ba3-119">For an overview of Elastic Database jobs, see [Elastic Database jobs overview](sql-database-elastic-jobs-overview.md).</span></span>

<!--Image references-->


