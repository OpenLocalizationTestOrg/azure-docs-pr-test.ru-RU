---
title: "aaaCreate группу для пользователей в Azure Active Directory | Документы Microsoft"
description: "Как toocreate группы в Azure Active Directory и добавление членов группы toohello"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cc5f232a-1e77-45c2-b28b-1fcb4621725c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fc583a7f02ce50e7f3b2c8f97a9c032a3e2dc33a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-group-and-add-members-in-azure-active-directory"></a>Создание группы и добавление в нее пользователей в Azure Active Directory
> [!div class="op_single_selector"]
> * [Портал Azure](active-directory-groups-create-azure-portal.md)
> * [Классический портал Azure](active-directory-accessmanagement-manage-groups.md)
> * [PowerShell](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

В этой статье объясняется, как toocreate и заполнить новую группу в Azure Active Directory. Используйте задачи управления tooperform группы, например назначение лицензии или разрешения tooa число пользователей или устройств одновременно.

## <a name="how-do-i-create-a-group"></a>Как создать группу?
1. Войдите в toohello [портал Azure](https://portal.azure.com) с помощью учетной записи глобального администратора каталога hello.
2. Выберите **дополнительные службы**, введите **пользователей и групп** в hello текстовое поле, а затем выберите **ввод**.

   ![Открытие страницы "Управление пользователями"](./media/active-directory-groups-create-azure-portal/search-user-management.png)
3. На hello **пользователей и групп** колонке выберите **все группы**.

   ![Открытие hello групп колонку](./media/active-directory-groups-create-azure-portal/view-groups-blade.png)
4. На hello **пользователей и групп — все группы** колонки, выберите hello **добавить** команды.

   ![При выборе команды Добавить hello](./media/active-directory-groups-create-azure-portal/add-group-command.png)
5. На hello **группы** колонки, добавьте имя и описание группы hello.
6. tooselect элементы tooadd toohello группы выберите **назначено** в hello **тип регистрации членства** поле, а затем выберите **элементы**. Дополнительные сведения о как toomanage динамически hello членство в группе, в разделе [toocreate атрибуты с помощью расширенного правила для членства в группе](active-directory-groups-dynamic-membership-azure-portal.md).

   ![При выборе tooadd элементов](./media/active-directory-groups-create-azure-portal/select-members.png)
7. На hello **элементы** колонки, выберите один или несколько пользователей или устройств группы toohello tooadd и выберите hello **выберите** кнопку внизу hello hello колонке tooadd их toohello группы. Hello **пользователя** поле фильтры Здравствуйте, отображаемое на основе сопоставления вашей записи tooany часть имени пользователя или устройства. Подстановочные знаки в поле не допускаются.
8. После добавления членов группы toohello выберите **создать** на hello **группы** колонку.    

   ![Подтверждение создания группы](./media/active-directory-groups-create-azure-portal/create-group-confirmation.png)


## <a name="next-steps"></a>Дальнейшие действия
В следующих статьях содержатся дополнительные сведения об Azure Active Directory.

* [Просмотр существующих групп](active-directory-groups-view-azure-portal.md)
* [Управление параметрами группы](active-directory-groups-settings-azure-portal.md)
* [Управление участниками группы](active-directory-groups-members-azure-portal.md)
* [Управление членством в группе](active-directory-groups-membership-azure-portal.md)
* [Управление динамическими правилами для пользователей в группе](active-directory-groups-dynamic-membership-azure-portal.md)
