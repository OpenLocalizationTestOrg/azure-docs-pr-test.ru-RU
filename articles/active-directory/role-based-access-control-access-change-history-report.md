---
title: "Доступ к отчетам с помощью Azure RBAC | Документация Майкрософт"
description: "Создайте отчет, в котором указаны все изменения доступа к подпискам Azure с управлением доступом на основе ролей за последние 90 дней."
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
ms.openlocfilehash: 4e8028ab43ed02ef0c0a1374326b07f72f97d9d9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-access-report-for-role-based-access-control"></a><span data-ttu-id="c0d8b-103">Создание отчета о доступе для управления доступом на основе ролей</span><span class="sxs-lookup"><span data-stu-id="c0d8b-103">Create an access report for Role-Based Access Control</span></span>
<span data-ttu-id="c0d8b-104">Когда кто-то предоставляет или отменяет доступ в рамках ваших подписок, изменения регистрируются в журнале событий Azure.</span><span class="sxs-lookup"><span data-stu-id="c0d8b-104">Any time someone grants or revokes access within your subscriptions, the changes get logged in Azure events.</span></span> <span data-ttu-id="c0d8b-105">Чтобы просмотреть все изменения за последние 90 дней, создайте отчет по журналу изменений доступа.</span><span class="sxs-lookup"><span data-stu-id="c0d8b-105">You can create access change history reports to see all changes for the past 90 days.</span></span>

## <a name="create-a-report-with-azure-powershell"></a><span data-ttu-id="c0d8b-106">Создание отчета с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c0d8b-106">Create a report with Azure PowerShell</span></span>
<span data-ttu-id="c0d8b-107">Чтобы создать отчет по журналу изменений доступа в PowerShell, используйте команду [Get-AzureRMAuthorizationChangeLog](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog).</span><span class="sxs-lookup"><span data-stu-id="c0d8b-107">To create an access change history report in PowerShell, use the [Get-AzureRMAuthorizationChangeLog](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog) command.</span></span>

<span data-ttu-id="c0d8b-108">При вызове этой команды можно указывать, какие свойства назначения нужно включить в список, в частности:</span><span class="sxs-lookup"><span data-stu-id="c0d8b-108">When you call this command, you can specify which property of the assignments you want listed, including the following:</span></span>

| <span data-ttu-id="c0d8b-109">Свойство</span><span class="sxs-lookup"><span data-stu-id="c0d8b-109">Property</span></span> | <span data-ttu-id="c0d8b-110">Описание</span><span class="sxs-lookup"><span data-stu-id="c0d8b-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c0d8b-111">**Действие**</span><span class="sxs-lookup"><span data-stu-id="c0d8b-111">**Action**</span></span> |<span data-ttu-id="c0d8b-112">Предоставление доступа или его отмена</span><span class="sxs-lookup"><span data-stu-id="c0d8b-112">Whether access was granted or revoked</span></span> |
| <span data-ttu-id="c0d8b-113">**Caller**</span><span class="sxs-lookup"><span data-stu-id="c0d8b-113">**Caller**</span></span> |<span data-ttu-id="c0d8b-114">Владелец, ответственный за изменение доступа</span><span class="sxs-lookup"><span data-stu-id="c0d8b-114">The owner responsible for the access change</span></span> |
| <span data-ttu-id="c0d8b-115">**PrincipalId**</span><span class="sxs-lookup"><span data-stu-id="c0d8b-115">**PrincipalId**</span></span> | <span data-ttu-id="c0d8b-116">Уникальный идентификатор пользователя, группы или приложения, которым назначена роль</span><span class="sxs-lookup"><span data-stu-id="c0d8b-116">The unique identifier of the user, group, or application that was assigned the role</span></span> |
| <span data-ttu-id="c0d8b-117">**PrincipalName**</span><span class="sxs-lookup"><span data-stu-id="c0d8b-117">**PrincipalName**</span></span> |<span data-ttu-id="c0d8b-118">Имя пользователя, группы или приложения</span><span class="sxs-lookup"><span data-stu-id="c0d8b-118">The name of the user, group, or application</span></span> |
| <span data-ttu-id="c0d8b-119">**PrincipalType**</span><span class="sxs-lookup"><span data-stu-id="c0d8b-119">**PrincipalType**</span></span> |<span data-ttu-id="c0d8b-120">Кому адресовано назначение — пользователю, группе или приложению</span><span class="sxs-lookup"><span data-stu-id="c0d8b-120">Whether the assignment was for a user, group, or application</span></span> |
| <span data-ttu-id="c0d8b-121">**RoleDefinitionId**</span><span class="sxs-lookup"><span data-stu-id="c0d8b-121">**RoleDefinitionId**</span></span> |<span data-ttu-id="c0d8b-122">Идентификатор GUID роли, которая была назначена или отменена</span><span class="sxs-lookup"><span data-stu-id="c0d8b-122">The GUID of the role that was granted or revoked</span></span> |
| <span data-ttu-id="c0d8b-123">**RoleName**</span><span class="sxs-lookup"><span data-stu-id="c0d8b-123">**RoleName**</span></span> |<span data-ttu-id="c0d8b-124">Роль, которая была назначена или отменена</span><span class="sxs-lookup"><span data-stu-id="c0d8b-124">The role that was granted or revoked</span></span> |
| <span data-ttu-id="c0d8b-125">**Область**</span><span class="sxs-lookup"><span data-stu-id="c0d8b-125">**Scope**</span></span> | <span data-ttu-id="c0d8b-126">Уникальный идентификатор подписки, группы ресурсов или ресурса, к которым применяется назначение</span><span class="sxs-lookup"><span data-stu-id="c0d8b-126">The unique identifier of the subscription, resource group, or resource that the assignment applies to</span></span> | 
| <span data-ttu-id="c0d8b-127">**ScopeName**</span><span class="sxs-lookup"><span data-stu-id="c0d8b-127">**ScopeName**</span></span> |<span data-ttu-id="c0d8b-128">Название подписки, группы ресурсов или ресурса</span><span class="sxs-lookup"><span data-stu-id="c0d8b-128">The name of the subscription, resource group, or resource</span></span> |
| <span data-ttu-id="c0d8b-129">**ScopeType**</span><span class="sxs-lookup"><span data-stu-id="c0d8b-129">**ScopeType**</span></span> |<span data-ttu-id="c0d8b-130">Область назначения: подписка, группа ресурсов или ресурс</span><span class="sxs-lookup"><span data-stu-id="c0d8b-130">Whether the assignment was at the subscription, resource group, or resource scope</span></span> |
| <span data-ttu-id="c0d8b-131">**Timestamp**</span><span class="sxs-lookup"><span data-stu-id="c0d8b-131">**Timestamp**</span></span> |<span data-ttu-id="c0d8b-132">Дата и время изменения доступа</span><span class="sxs-lookup"><span data-stu-id="c0d8b-132">The date and time that access was changed</span></span> |

<span data-ttu-id="c0d8b-133">Следующий пример команды создает список всех изменений доступа в подписке за последние семь дней.</span><span class="sxs-lookup"><span data-stu-id="c0d8b-133">This example command lists all access changes in the subscription for the past seven days:</span></span>

```
Get-AzureRMAuthorizationChangeLog -StartTime ([DateTime]::Now - [TimeSpan]::FromDays(7)) | FT Caller,Action,RoleName,PrincipalType,PrincipalName,ScopeType,ScopeName
```

![PowerShell Get-AzureRMAuthorizationChangeLog — снимок экрана](./media/role-based-access-control-configure/access-change-history.png)

## <a name="create-a-report-with-azure-cli"></a><span data-ttu-id="c0d8b-135">Создание отчета с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c0d8b-135">Create a report with Azure CLI</span></span>
<span data-ttu-id="c0d8b-136">Чтобы создать отчет по журналу изменений доступа с помощью интерфейса командной строки (CLI) Azure, используйте команду `azure role assignment changelog list` .</span><span class="sxs-lookup"><span data-stu-id="c0d8b-136">To create an access change history report in the Azure command-line interface (CLI), use the `azure role assignment changelog list` command.</span></span>

## <a name="export-to-a-spreadsheet"></a><span data-ttu-id="c0d8b-137">Экспорт в электронную таблицу</span><span class="sxs-lookup"><span data-stu-id="c0d8b-137">Export to a spreadsheet</span></span>
<span data-ttu-id="c0d8b-138">Для сохранения отчета или работы с данными экспортируйте сведения об изменениях доступа в CSV-файл.</span><span class="sxs-lookup"><span data-stu-id="c0d8b-138">To save the report, or manipulate the data, export the access changes into a .csv file.</span></span> <span data-ttu-id="c0d8b-139">Так вы можете просмотреть отчет в виде электронной таблицы.</span><span class="sxs-lookup"><span data-stu-id="c0d8b-139">You can then view the report in a spreadsheet for review.</span></span>

![Просмотр журнала изменений в виде электронной таблицы — снимок экрана](./media/role-based-access-control-configure/change-history-spreadsheet.png)

## <a name="next-steps"></a><span data-ttu-id="c0d8b-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c0d8b-141">Next steps</span></span>
* <span data-ttu-id="c0d8b-142">Работа с [пользовательскими ролями в Azure RBAC](role-based-access-control-custom-roles.md)</span><span class="sxs-lookup"><span data-stu-id="c0d8b-142">Work with [Custom roles in Azure RBAC](role-based-access-control-custom-roles.md)</span></span>
* <span data-ttu-id="c0d8b-143">Узнайте, как управлять [Azure RBAC с помощью PowerShell](role-based-access-control-manage-access-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c0d8b-143">Learn how to manage [Azure RBAC with powershell](role-based-access-control-manage-access-powershell.md)</span></span>

