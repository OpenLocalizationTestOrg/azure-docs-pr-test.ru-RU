---
title: "отчет по aaaAccess - RBAC Azure. | Документы Microsoft"
description: "Создайте отчет о том, что список всех изменений в tooyour доступа подписки Azure с ролевого контроля доступа к hello за последние 90 дней."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 2bc68595-145e-4de3-8b71-3a21890d13d9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/17/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9ad85d3d8e66ce167032638a35e4afffb46d3892
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-access-report-for-role-based-access-control"></a><span data-ttu-id="5e036-103">Создание отчета о доступе для управления доступом на основе ролей</span><span class="sxs-lookup"><span data-stu-id="5e036-103">Create an access report for Role-Based Access Control</span></span>
<span data-ttu-id="5e036-104">Любой пользователь предоставляет или отменяет доступ в рамках вашей подписки в Azure события заносятся изменения hello.</span><span class="sxs-lookup"><span data-stu-id="5e036-104">Any time someone grants or revokes access within your subscriptions, hello changes get logged in Azure events.</span></span> <span data-ttu-id="5e036-105">Можно создать журнал отчетов access изменение toosee всех изменений для hello за последние 90 дней.</span><span class="sxs-lookup"><span data-stu-id="5e036-105">You can create access change history reports toosee all changes for hello past 90 days.</span></span>

## <a name="create-a-report-with-azure-powershell"></a><span data-ttu-id="5e036-106">Создание отчета с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5e036-106">Create a report with Azure PowerShell</span></span>
<span data-ttu-id="5e036-107">отчет по журналу в PowerShell, используйте hello изменить toocreate доступа [Get AzureRMAuthorizationChangeLog](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog) команды.</span><span class="sxs-lookup"><span data-stu-id="5e036-107">toocreate an access change history report in PowerShell, use hello [Get-AzureRMAuthorizationChangeLog](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog) command.</span></span>

<span data-ttu-id="5e036-108">При вызове этой команды можно указать, какое свойство отсутствует в списке, включая следующие hello назначения hello:</span><span class="sxs-lookup"><span data-stu-id="5e036-108">When you call this command, you can specify which property of hello assignments you want listed, including hello following:</span></span>

| <span data-ttu-id="5e036-109">Свойство</span><span class="sxs-lookup"><span data-stu-id="5e036-109">Property</span></span> | <span data-ttu-id="5e036-110">Описание</span><span class="sxs-lookup"><span data-stu-id="5e036-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5e036-111">**Действие**</span><span class="sxs-lookup"><span data-stu-id="5e036-111">**Action**</span></span> |<span data-ttu-id="5e036-112">Предоставление доступа или его отмена</span><span class="sxs-lookup"><span data-stu-id="5e036-112">Whether access was granted or revoked</span></span> |
| <span data-ttu-id="5e036-113">**Caller**</span><span class="sxs-lookup"><span data-stu-id="5e036-113">**Caller**</span></span> |<span data-ttu-id="5e036-114">Владелец Hello, ответственный за доступ hello изменить</span><span class="sxs-lookup"><span data-stu-id="5e036-114">hello owner responsible for hello access change</span></span> |
| <span data-ttu-id="5e036-115">**PrincipalId**</span><span class="sxs-lookup"><span data-stu-id="5e036-115">**PrincipalId**</span></span> | <span data-ttu-id="5e036-116">Уникальный идентификатор hello пользователя, группы или приложения, в которой была предоставлена роль hello Hello</span><span class="sxs-lookup"><span data-stu-id="5e036-116">hello unique identifier of hello user, group, or application that was assigned hello role</span></span> |
| <span data-ttu-id="5e036-117">**PrincipalName**</span><span class="sxs-lookup"><span data-stu-id="5e036-117">**PrincipalName**</span></span> |<span data-ttu-id="5e036-118">Имя Hello hello пользователя, группы или приложения</span><span class="sxs-lookup"><span data-stu-id="5e036-118">hello name of hello user, group, or application</span></span> |
| <span data-ttu-id="5e036-119">**PrincipalType**</span><span class="sxs-lookup"><span data-stu-id="5e036-119">**PrincipalType**</span></span> |<span data-ttu-id="5e036-120">Было ли для пользователя, группы или приложения hello назначения</span><span class="sxs-lookup"><span data-stu-id="5e036-120">Whether hello assignment was for a user, group, or application</span></span> |
| <span data-ttu-id="5e036-121">**RoleDefinitionId**</span><span class="sxs-lookup"><span data-stu-id="5e036-121">**RoleDefinitionId**</span></span> |<span data-ttu-id="5e036-122">Идентификатор GUID для hello роль, которая была предоставленное или отмененное Hello</span><span class="sxs-lookup"><span data-stu-id="5e036-122">hello GUID of hello role that was granted or revoked</span></span> |
| <span data-ttu-id="5e036-123">**RoleName**</span><span class="sxs-lookup"><span data-stu-id="5e036-123">**RoleName**</span></span> |<span data-ttu-id="5e036-124">Hello роль, которая была предоставление или отзыв</span><span class="sxs-lookup"><span data-stu-id="5e036-124">hello role that was granted or revoked</span></span> |
| <span data-ttu-id="5e036-125">**Область**</span><span class="sxs-lookup"><span data-stu-id="5e036-125">**Scope**</span></span> | <span data-ttu-id="5e036-126">Уникальный идентификатор Hello hello подписки, группы ресурсов или ресурсов, hello назначения также применяется</span><span class="sxs-lookup"><span data-stu-id="5e036-126">hello unique identifier of hello subscription, resource group, or resource that hello assignment applies too</span></span>| 
| <span data-ttu-id="5e036-127">**ScopeName**</span><span class="sxs-lookup"><span data-stu-id="5e036-127">**ScopeName**</span></span> |<span data-ttu-id="5e036-128">Имя Hello hello подписки, группы ресурсов или ресурсов</span><span class="sxs-lookup"><span data-stu-id="5e036-128">hello name of hello subscription, resource group, or resource</span></span> |
| <span data-ttu-id="5e036-129">**ScopeType**</span><span class="sxs-lookup"><span data-stu-id="5e036-129">**ScopeType**</span></span> |<span data-ttu-id="5e036-130">Было ли назначение hello hello подписки, области видимости ресурсов или группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="5e036-130">Whether hello assignment was at hello subscription, resource group, or resource scope</span></span> |
| <span data-ttu-id="5e036-131">**Timestamp**</span><span class="sxs-lookup"><span data-stu-id="5e036-131">**Timestamp**</span></span> |<span data-ttu-id="5e036-132">Hello дату и время изменения доступа</span><span class="sxs-lookup"><span data-stu-id="5e036-132">hello date and time that access was changed</span></span> |

<span data-ttu-id="5e036-133">В этом примере команда перечислены все изменения доступа к подписке hello для hello за последние семь дней.</span><span class="sxs-lookup"><span data-stu-id="5e036-133">This example command lists all access changes in hello subscription for hello past seven days:</span></span>

```
Get-AzureRMAuthorizationChangeLog -StartTime ([DateTime]::Now - [TimeSpan]::FromDays(7)) | FT Caller,Action,RoleName,PrincipalType,PrincipalName,ScopeType,ScopeName
```

![PowerShell Get-AzureRMAuthorizationChangeLog — снимок экрана](./media/role-based-access-control-configure/access-change-history.png)

## <a name="create-a-report-with-azure-cli"></a><span data-ttu-id="5e036-135">Создание отчета с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5e036-135">Create a report with Azure CLI</span></span>
<span data-ttu-id="5e036-136">toocreate отчета access журнал изменений в hello Azure командной строки (CLI), использовать hello `azure role assignment changelog list` команды.</span><span class="sxs-lookup"><span data-stu-id="5e036-136">toocreate an access change history report in hello Azure command-line interface (CLI), use hello `azure role assignment changelog list` command.</span></span>

## <a name="export-tooa-spreadsheet"></a><span data-ttu-id="5e036-137">Экспорт электронной таблицы tooa</span><span class="sxs-lookup"><span data-stu-id="5e036-137">Export tooa spreadsheet</span></span>
<span data-ttu-id="5e036-138">toosave hello отчета или работы с данными hello, изменяет доступа hello Экспорт в CSV-файл.</span><span class="sxs-lookup"><span data-stu-id="5e036-138">toosave hello report, or manipulate hello data, export hello access changes into a .csv file.</span></span> <span data-ttu-id="5e036-139">Затем можно просмотреть отчет hello в электронную таблицу для просмотра.</span><span class="sxs-lookup"><span data-stu-id="5e036-139">You can then view hello report in a spreadsheet for review.</span></span>

![Просмотр журнала изменений в виде электронной таблицы — снимок экрана](./media/role-based-access-control-configure/change-history-spreadsheet.png)

## <a name="next-steps"></a><span data-ttu-id="5e036-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5e036-141">Next steps</span></span>
* <span data-ttu-id="5e036-142">Работа с [пользовательскими ролями в Azure RBAC](role-based-access-control-custom-roles.md)</span><span class="sxs-lookup"><span data-stu-id="5e036-142">Work with [Custom roles in Azure RBAC](role-based-access-control-custom-roles.md)</span></span>
* <span data-ttu-id="5e036-143">Узнайте, как toomanage [RBAC Azure с помощью powershell](role-based-access-control-manage-access-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="5e036-143">Learn how toomanage [Azure RBAC with powershell](role-based-access-control-manage-access-powershell.md)</span></span>

