---
title: "Управление доступом на основе aaaRole в hello портал Azure | Документы Microsoft"
description: "Начало работы в управление доступом с элементом управления доступом на основе ролей в hello портала Azure. Используйте роль назначения tooassign разрешения tooyour ресурсы."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 8078f366-a2c4-4fbb-a44b-fc39fd89df81
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/17/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: b87e00089b0fc93fb212b318330a6f22bfbf59e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-role-based-access-control-toomanage-access-tooyour-azure-subscription-resources"></a>Подписка Azure tooyour ресурсы для управления доступом на основе ролей toomanage доступа
> [!div class="op_single_selector"]
> * [Управление доступом по пользователям или группам](role-based-access-control-manage-assignments.md)
> * [Управление доступом по ресурсам](role-based-access-control-configure.md)

Контроль доступа на основе ролей (RBAC) Azure обеспечивает точное управление доступом для Azure. С помощью RBAC, можно предоставить только hello уровень доступа, пользователи должны tooperform свою работу. Эта статья поможет вам приступить к работе с RBAC в hello портал Azure. Дополнительные сведения о том, как RBAC помогает управлять доступом, см. в статье [Начало работы с управлением доступом на портале Azure](role-based-access-control-what-is.md).

В пределах каждой подписки можно предоставить копию too2000 назначения ролей. 

## <a name="view-access"></a>Просмотр прав доступа
Можно увидеть, кто имеет доступ tooa ресурсов, группы ресурсов или подписки в главной колонке в hello [портал Azure](https://portal.azure.com). Например мы хотим toosee, кто имеет доступ tooone нашей групп ресурсов:

1. Выберите **групп ресурсов** hello панели навигации слева hello.  
    ![Группы ресурсов — значок](./media/role-based-access-control-configure/resourcegroups_icon.png)
2. Привет, выберите имя группы ресурсов hello из hello **групп ресурсов** колонку.
3. Выберите **(IAM) управления доступом к** из меню слева hello.  
4. колонке управления доступом Hello список всех пользователей, групп и приложений, которые были предоставлены группе ресурсов toohello доступа.  
   
    ![Колонка "Пользователи" — унаследованные и назначенные права доступа — снимок экрана](./media/role-based-access-control-configure/view-access.png)

Обратите внимание, что некоторые роли находятся в области видимости слишком**этот ресурс** а другие представляют собой **Inherited** его из другой области. Доступа специально toohello группу ресурсов или унаследовано из родительского подписки toohello назначения.

> [!NOTE]
> Администраторы классический подписки и соадминистраторам считаются владельцев подписки hello в новой модели RBAC hello.

## <a name="add-access"></a>Добавление доступа
Разрешить доступ из внутри hello ресурсов, группы ресурсов или подписку, которая является областью hello hello назначение ролей.

1. Выберите **добавить** колонке управления доступом hello.  
2. Обратиться в tooassign из hello роли выберите hello **выберите роль** колонку.
3. Выберите в каталоге, из которого будут toogrant доступ к hello пользователя, группы или приложения. Можно выполнить поиск каталога hello отображаемые имена, адреса электронной почты и идентификаторов объектов.  
   
    ![Колонка "Добавить пользователей" — "Поиск" — снимок экрана](./media/role-based-access-control-configure/grant-access2.png)
4. Выберите **ОК** toocreate hello назначения. Hello **Добавление пользователя** всплывающее окно отслеживает ход выполнения hello.  
    ![Индикатор выполнения при добавлении пользователя — снимок экрана](./media/role-based-access-control-configure/addinguser_popup.png)

После успешного добавления назначение ролей, оно будет отображаться для hello **пользователей** колонку.

## <a name="remove-access"></a>Запрет доступа
1. Наведите указатель на имя hello hello назначения, которое следует tooremove. Флажок отображается имя следующего toohello.
2. Использовать флажки tooselect hello один или несколько назначений ролей.
2. Щелкните **Удалить**.  
3. Выберите **Да** tooconfirm hello удаления.

Унаследованные назначения нельзя удалить. Если требуется tooremove наследуемые назначения необходимо toodo его в параметре hello области, где создавался hello назначение ролей. В hello **область** столбец, далее слишком**Inherited** есть ссылка, которое знакомит вас toohello ресурсы которой было назначено этой роли. Перейдите в списке ресурсов toohello назначение ролей tooremove hello.

![Колонка "Пользователи" — унаследованные права доступа отключают кнопку "Удалить" — снимок экрана](./media/role-based-access-control-configure/remove-access2.png)

## <a name="other-tools-toomanage-access"></a>Другие средства доступа toomanage
Можно назначать роли и управление доступом с помощью Azure RBAC команды в средствах, отличные от hello портал Azure.  Выполните дополнительные о предварительных требованиях hello toolearn ссылки hello и приступить к работе с командами hello Azure RBAC.

* [Azure PowerShell](role-based-access-control-manage-access-powershell.md)
* [Интерфейс командной строки Azure](role-based-access-control-manage-access-azure-cli.md)
* [ИНТЕРФЕЙС REST API](role-based-access-control-manage-access-rest.md)

## <a name="next-steps"></a>Дальнейшие действия
* [Создание отчета по журналу изменений доступа](role-based-access-control-access-change-history-report.md)
* В разделе hello [RBAC встроенные роли](role-based-access-built-in-roles.md)
* Определите собственные [пользовательские роли в RBAC Azure](role-based-access-control-custom-roles.md)

