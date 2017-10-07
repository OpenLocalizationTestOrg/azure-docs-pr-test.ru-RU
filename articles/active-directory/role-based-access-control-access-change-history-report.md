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
# <a name="create-an-access-report-for-role-based-access-control"></a>Создание отчета о доступе для управления доступом на основе ролей
Любой пользователь предоставляет или отменяет доступ в рамках вашей подписки в Azure события заносятся изменения hello. Можно создать журнал отчетов access изменение toosee всех изменений для hello за последние 90 дней.

## <a name="create-a-report-with-azure-powershell"></a>Создание отчета с помощью Azure PowerShell
отчет по журналу в PowerShell, используйте hello изменить toocreate доступа [Get AzureRMAuthorizationChangeLog](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog) команды.

При вызове этой команды можно указать, какое свойство отсутствует в списке, включая следующие hello назначения hello:

| Свойство | Описание |
| --- | --- |
| **Действие** |Предоставление доступа или его отмена |
| **Caller** |Владелец Hello, ответственный за доступ hello изменить |
| **PrincipalId** | Уникальный идентификатор hello пользователя, группы или приложения, в которой была предоставлена роль hello Hello |
| **PrincipalName** |Имя Hello hello пользователя, группы или приложения |
| **PrincipalType** |Было ли для пользователя, группы или приложения hello назначения |
| **RoleDefinitionId** |Идентификатор GUID для hello роль, которая была предоставленное или отмененное Hello |
| **RoleName** |Hello роль, которая была предоставление или отзыв |
| **Область** | Уникальный идентификатор Hello hello подписки, группы ресурсов или ресурсов, hello назначения также применяется| 
| **ScopeName** |Имя Hello hello подписки, группы ресурсов или ресурсов |
| **ScopeType** |Было ли назначение hello hello подписки, области видимости ресурсов или группы ресурсов |
| **Timestamp** |Hello дату и время изменения доступа |

В этом примере команда перечислены все изменения доступа к подписке hello для hello за последние семь дней.

```
Get-AzureRMAuthorizationChangeLog -StartTime ([DateTime]::Now - [TimeSpan]::FromDays(7)) | FT Caller,Action,RoleName,PrincipalType,PrincipalName,ScopeType,ScopeName
```

![PowerShell Get-AzureRMAuthorizationChangeLog — снимок экрана](./media/role-based-access-control-configure/access-change-history.png)

## <a name="create-a-report-with-azure-cli"></a>Создание отчета с помощью Azure CLI
toocreate отчета access журнал изменений в hello Azure командной строки (CLI), использовать hello `azure role assignment changelog list` команды.

## <a name="export-tooa-spreadsheet"></a>Экспорт электронной таблицы tooa
toosave hello отчета или работы с данными hello, изменяет доступа hello Экспорт в CSV-файл. Затем можно просмотреть отчет hello в электронную таблицу для просмотра.

![Просмотр журнала изменений в виде электронной таблицы — снимок экрана](./media/role-based-access-control-configure/change-history-spreadsheet.png)

## <a name="next-steps"></a>Дальнейшие действия
* Работа с [пользовательскими ролями в Azure RBAC](role-based-access-control-custom-roles.md)
* Узнайте, как toomanage [RBAC Azure с помощью powershell](role-based-access-control-manage-access-powershell.md)

