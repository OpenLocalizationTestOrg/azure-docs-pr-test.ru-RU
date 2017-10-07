---
title: "aaaManage hello членов группы в Azure Active Directory | Документы Microsoft"
description: "Как tooadd или удаление пользователей и устройств из группы в Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d399a97d-fd2a-4b2d-b73d-0975db83f41b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4cb16ee63828003da251423a04736f7174dd4896
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-group-membership-for-users-in-your-azure-active-directory-tenant"></a>Управление участниками групп в клиенте Azure Active Directory
В этой статье объясняется, как toomanage hello членов группы в Azure Active Directory (Azure AD).

## <a name="how-do-i-find-hello-members-and-manage-them"></a>Как найти члены hello и управлять ими?
1. Войдите в toohello [портал Azure](https://portal.azure.com) с помощью учетной записи глобального администратора каталога hello.
2. Выберите **дополнительные службы**, введите **пользователей и групп** в hello текстовое поле, а затем выберите **ввод**.

   ![Открытие страницы "Управление пользователями"](./media/active-directory-groups-members-azure-portal/search-user-management.png)
3. На hello **пользователей и групп** колонке выберите **все группы**.

   ![Открытие hello групп колонку](./media/active-directory-groups-members-azure-portal/view-groups-blade.png)
4. На hello **пользователей и групп — все группы** колонки, выберите группу.
5. На hello **группа — *groupname***  колонке выберите **элементы**.

   ![Открытие hello члены колонку](./media/active-directory-groups-members-azure-portal/view-group-members.png)
6. группы toohello элементы tooadd на hello **группы - члены** колонке выберите **добавить членов**.

   ![Команда "Добавить участников"](./media/active-directory-groups-members-azure-portal/add-group-members-command.png)
7. На hello **элементы** колонки, выберите один или несколько пользователей или устройств группы toohello tooadd и выберите hello **выберите** кнопку внизу hello hello колонке tooadd их toohello группы. Hello **пользователя** поле фильтры Здравствуйте, отображаемое на основе сопоставления вашей записи tooany часть имени пользователя или устройства. Подстановочные знаки в поле не допускаются.
8. tooremove членов из группы hello на hello **группы - члены** колонке выберите член.
9. На hello ***membername*** колонки, выберите hello **удалить** команду и подтвердите перемещение в строке приветствия.

   ![Команда "Удалить участников"](./media/active-directory-groups-members-azure-portal/remove-group-members-command.png)
10. Завершив изменение состава группы hello, выберите **Сохранить**.

## <a name="additional-information"></a>Дополнительная информация
В следующих статьях содержатся дополнительные сведения об Azure Active Directory.

* [Просмотр существующих групп](active-directory-groups-view-azure-portal.md)
* [Создание группы и добавление участников](active-directory-groups-create-azure-portal.md)
* [Управление параметрами группы](active-directory-groups-settings-azure-portal.md)
* [Управление членством в группе](active-directory-groups-membership-azure-portal.md)
* [Управление динамическими правилами для пользователей в группе](active-directory-groups-dynamic-membership-azure-portal.md)
