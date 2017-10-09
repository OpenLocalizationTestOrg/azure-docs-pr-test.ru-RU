---
title: "обнаружения Azure aaaPowerShell аудит угроз пример базы данных SQL | Документы Microsoft"
description: "Azure PowerShell пример сценария tooconfigure аудита и угрозы обнаружения в базе данных SQL Azure"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,security
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 97e057ac6efe5e730404ae796bc01e7e5c70df35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooconfigure-sql-database-auditing-and-threat-detection"></a><span data-ttu-id="c9cf4-103">Используйте PowerShell tooconfigure базы данных SQL аудита и угрозы определение</span><span class="sxs-lookup"><span data-stu-id="c9cf4-103">Use PowerShell tooconfigure SQL Database auditing and threat detection</span></span>

<span data-ttu-id="c9cf4-104">Этот пример сценария Azure PowerShell позволяет настроить аудит и обнаружение угроз для базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="c9cf4-104">This PowerShell script example configures SQL Database auditing and threat detection.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="c9cf4-105">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="c9cf4-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/database-auditing-and-threat-detection/database-auditing-and-threat-detection.ps1?highlight=13-14 "Configure auditing and threat detection")]

## <a name="clean-up-deployment"></a><span data-ttu-id="c9cf4-106">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="c9cf4-106">Clean up deployment</span></span>

<span data-ttu-id="c9cf4-107">После выполнения сценария образец hello hello, следующая команда может быть группы ресурсов используется tooremove hello и все ресурсы, связанные с ним.</span><span class="sxs-lookup"><span data-stu-id="c9cf4-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="c9cf4-108">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="c9cf4-108">Script explanation</span></span>

<span data-ttu-id="c9cf4-109">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="c9cf4-109">This script uses hello following commands.</span></span> <span data-ttu-id="c9cf4-110">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="c9cf4-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c9cf4-111">Команда</span><span class="sxs-lookup"><span data-stu-id="c9cf4-111">Command</span></span> | <span data-ttu-id="c9cf4-112">Примечания</span><span class="sxs-lookup"><span data-stu-id="c9cf4-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c9cf4-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c9cf4-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="c9cf4-114">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="c9cf4-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c9cf4-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="c9cf4-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="c9cf4-116">Создает логический сервер, на котором размещена база данных или эластичный пул.</span><span class="sxs-lookup"><span data-stu-id="c9cf4-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="c9cf4-117">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="c9cf4-117">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="c9cf4-118">Создает на логическом сервере отдельную базу данных или базу данных в составе пула.</span><span class="sxs-lookup"><span data-stu-id="c9cf4-118">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="c9cf4-119">New-AzureRmStorageAccount</span><span class="sxs-lookup"><span data-stu-id="c9cf4-119">New-AzureRmStorageAccount</span></span>](/powershell/module/azurerm.storage/new-azurermstorageaccount) | <span data-ttu-id="c9cf4-120">Создает учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="c9cf4-120">Creates a Storage account.</span></span> |
| [<span data-ttu-id="c9cf4-121">Set-AzureRmSqlDatabaseAuditingPolicy</span><span class="sxs-lookup"><span data-stu-id="c9cf4-121">Set-AzureRmSqlDatabaseAuditingPolicy</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabaseauditingpolicy) | <span data-ttu-id="c9cf4-122">Задает hello политику аудита для базы данных.</span><span class="sxs-lookup"><span data-stu-id="c9cf4-122">Sets hello auditing policy for a database.</span></span> |
| [<span data-ttu-id="c9cf4-123">Set-AzureRmSqlDatabaseThreatDetectionPolicy</span><span class="sxs-lookup"><span data-stu-id="c9cf4-123">Set-AzureRmSqlDatabaseThreatDetectionPolicy</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasethreatdetectionpolicy) | <span data-ttu-id="c9cf4-124">Задает политику обнаружения угроз для базы данных.</span><span class="sxs-lookup"><span data-stu-id="c9cf4-124">Sets a threat detection policy on a database.</span></span> |
| [<span data-ttu-id="c9cf4-125">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c9cf4-125">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="c9cf4-126">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="c9cf4-126">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="c9cf4-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c9cf4-127">Next steps</span></span>

<span data-ttu-id="c9cf4-128">Дополнительные сведения о hello Azure PowerShell см. в разделе [документация по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c9cf4-128">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="c9cf4-129">Дополнительные примеры скриптов PowerShell базы данных SQL можно найти в hello [скриптов базы данных SQL Azure PowerShell](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c9cf4-129">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
