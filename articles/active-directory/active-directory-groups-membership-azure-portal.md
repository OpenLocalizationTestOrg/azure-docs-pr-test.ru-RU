---
title: "группы hello aaaManage группе принадлежит tooin Azure Active Directory | Документы Microsoft"
description: "В Azure Active Directory группы могут содержать другие группы. Вот как toomanage членство в этих группах."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e785c2d0-7724-47d4-a56e-c58280c08a14
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0a0a1967084de0968e1e802559f9cdfd7ca6ae4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-toowhich-groups-a-group-belongs-in-your-azure-active-directory-tenant"></a>Управление группами toowhich, который принадлежит группа в клиенте Azure Active Directory
В Azure Active Directory группы могут содержать другие группы. Вот как toomanage членство в этих группах.

## <a name="how-do-i-find-hello-groups-my-group-is-a-member-of"></a>Как найти hello Моя группа является членом группы?
1. Войдите в toohello [портал Azure](https://portal.azure.com) с помощью учетной записи глобального администратора каталога hello.
2. Выберите **дополнительные службы**, введите **пользователей и групп** в hello текстовое поле, а затем выберите **ввод**.

   ![Открытие страницы "Управление пользователями"](./media/active-directory-groups-membership-azure-portal/search-user-management.png)
3. На hello **пользователей и групп** колонке выберите **все группы**.

   ![Открытие hello групп колонку](./media/active-directory-groups-membership-azure-portal/view-groups-blade.png)
4. На hello **пользователей и групп — все группы** колонки, выберите группу.
5. На hello **группа — *groupname***  колонке выберите **членство в группе**.

   ![Открытие hello группы членства колонку](./media/active-directory-groups-membership-azure-portal/group-membership-blade.png)
6. tooadd вашей группы в качестве члена другой группы, на hello **групповой - членство в группе** колонки, выберите hello **добавить** команды.
7. Выберите группу из hello **Выбор группы** и, при необходимости выберите hello **выберите** кнопку в нижней части hello колонка hello. Одновременно можно добавить одну группу tooonly группы. Hello **пользователя** поле фильтры Здравствуйте, отображаемое на основе сопоставления вашей записи tooany часть имени пользователя или устройства. Подстановочные знаки в поле не допускаются.

   ![Добавление членства в группе](./media/active-directory-groups-membership-azure-portal/add-group-membership.png)
8. tooremove вашей группы в качестве члена другой группы, на hello **групповой - членство в группе** колонки, выберите группу.
9. На hello ***groupname*** колонки, выберите hello **удалить** команду и подтвердите перемещение в строке приветствия.

   ![Команда "Удаление членства"](./media/active-directory-groups-membership-azure-portal/remove-group-membership.png)
10. Завершив изменение членства группы в других группах, щелкните **Сохранить**.

## <a name="additional-information"></a>Дополнительная информация
В следующих статьях содержатся дополнительные сведения об Azure Active Directory.

* [Просмотр существующих групп](active-directory-groups-view-azure-portal.md)
* [Создание группы и добавление участников](active-directory-groups-create-azure-portal.md)
* [Управление параметрами группы](active-directory-groups-settings-azure-portal.md)
* [Управление участниками группы](active-directory-groups-members-azure-portal.md)
* [Управление динамическими правилами для пользователей в группе](active-directory-groups-dynamic-membership-azure-portal.md)
