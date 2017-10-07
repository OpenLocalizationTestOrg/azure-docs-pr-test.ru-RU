---
title: "Назначение доступа aaaView ресурсов Azure | Документы Microsoft"
description: "Просмотр и управление ими все назначения hello управления доступом на основе ролей для любого пользователя или группу в hello портал Azure"
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
editor: jeffsta
ms.assetid: e6f9e657-8ee3-4eec-a21c-78fe1b52a005
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: andredm
ms.openlocfilehash: ec96c9d4b9e2cb4925949b8bac78767bd564c8ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="view-access-assignments-for-users-and-groups-in-hello-azure-portal"></a>Просмотр назначений доступ для пользователей и групп в hello портал Azure
> [!div class="op_single_selector"]
> * [Управление доступом по пользователям или группам](role-based-access-control-manage-assignments.md)
> * [Управление доступом по ресурсам](role-based-access-control-configure.md)

Управление доступом на основе ролей (RBAC) в hello Azure Active Directory (Azure AD), позволяет управлять доступом tooyour Azure ресурсы. 

Доступ, которым назначена RBAC детально настроенные так, как можно ограничить разрешения hello двумя способами:

* **Область:** RBAC назначения ролей, с областью tooa конкретной подписки, группы ресурсов или ресурсов. Пользователь получает доступ tooa одного ресурса не может получить доступ к другие ресурсы в hello одной подписке.
* **Роль:** внутри области hello назначения hello сведена доступ назначение роли еще продолжается. Роль может быть общей, например "Владелец", или более конкретной, например "Модуль чтения виртуальной машины".

Роли могут назначаться только из внутри hello подписки, группы ресурсов или ресурс, который является областью hello для назначения hello. Однако можно просмотреть все назначения hello доступа для данного пользователя или группы в одном месте. Можно создать до назначения ролей too2000 в каждой подписке. 

Получить дополнительные сведения о том, как слишком[использовать tooyour роли назначения toomanage доступ к ресурсам подписки Azure](role-based-access-control-configure.md).

## <a name="view-access-assignments"></a>Просмотр назначений доступа
toolook копирование hello доступа назначений для одного пользователя или группы, запуск в Azure Active Directory в hello [портал Azure](http://portal.azure.com).

1. Выберите **Azure Active Directory**. Если этот параметр не отображается в списке навигации, выберите **более служб** и прокрутите вниз toofind **Azure Active Directory**.
2. Выберите **Пользователи и группы**, а затем щелкните **Все пользователи** или **Все группы**. В этом примере мы рассмотрим отдельных пользователей.
    ![Снимок экрана: управление пользователями и группами в Azure Active Directory](./media/role-based-access-control-manage-assignments/rbac_users_groups.png)
3. Поиск hello пользователя по имени или имени пользователя.
4. Выберите **ресурсы Azure** колонке hello пользователя. Отображаются все назначения hello доступа для этого пользователя.

### <a name="read-permissions-tooview-assignments"></a>Разрешения на чтение tooview назначений
На этой странице отображаются только назначения доступа hello наличие tooread разрешение. Например имеют доступ на чтение toosubscription A и перейти toocheck колонки ресурсов Azure toohello назначений пользователя. Вы увидите назначения доступа для подписки A, но имеющиеся у пользователя назначения доступа для подписки Б не будут отображаться.

## <a name="delete-access-assignments"></a>Удаление назначений доступа
Из этой колонки можно удалить назначения доступа, которые назначаются напрямую tooa пользователя или группы. Если назначение доступа hello было унаследовано из родительской группы, требуется toogo toohello ресурсов или подписки и управление назначением hello существует.

1. Выберите из списка hello среди всех назначений hello доступа для пользователя или группы hello один требуется toodelete.
2. Выберите **удалить** и затем **Да** tooconfirm.
    ![Снимок экрана: удаление назначения доступа](./media/role-based-access-control-manage-assignments/delete_assignment.png)

## <a name="next-steps"></a>Дальнейшие действия

* Приступая к работе с управление доступом на основе ролей слишком[использовать tooyour роли назначения toomanage доступ к ресурсам подписки Azure](role-based-access-control-configure.md)
* В разделе hello [RBAC встроенные роли](role-based-access-built-in-roles.md)

