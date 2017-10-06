---
title: "Azure доменных служб Active Directory: Создание группы администраторов hello Azure AD DC | Документы Microsoft"
description: "Включение Azure доменных служб Active Directory с помощью hello классический портал Azure"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: maheshu
ms.openlocfilehash: d629ab9632ef6a45b549630999ff9a122d60c040
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-classic-portal"></a>Включение Azure доменных служб Active Directory с помощью hello классический портал Azure
В этой статье описываются и рассматриваются задачи настройки hello, необходимые для вас tooenable Active Directory домена служб Azure (Azure AD DS) для вашего клиента Azure Active Directory (Azure AD).

> [!NOTE]
> [**Попробуйте вместо этого использовать новый интерфейс портала hello Azure (Предварительная версия)**](active-directory-ds-getting-started.md). 
>

## <a name="task-1-create-hello-azure-ad-dc-administrators-group"></a>Задача 1: Создание группы «Администраторы» контроллера домена hello Azure AD
Первая задача Hello — toocreate административной группы в клиенте Azure AD. Эта специальная административная группа называется *Администраторы контроллера домена AAD*. Члены этой группы предоставляются административные разрешения на компьютеры, присоединенные к домену toohello управляемых доменных служб Active Directory Azure. На компьютерах, присоединенных к домену эта группа добавляется toohello группы «Администраторы». Кроме того члены этой группы можно использовать машины удаленно присоединенных toodomain tooconnect удаленного рабочего стола.  

> [!NOTE]
> Нет разрешений администратора домена или администратора предприятия на hello управляемый домен, созданный с помощью доменных служб Active Directory Azure. На управляемые домены эти разрешения защищены службой hello и не становятся доступны toousers в рамках клиента hello. Тем не менее, можно использовать hello специальных административных Создание группы в этой конфигурации задачи tooperform некоторые привилегированные операции. Эти операции включают toohello компьютеров к домену, принадлежащий группы администрирования toohello на присоединенных к домену компьютерах и Настройка групповой политики.
>

В этой задаче конфигурации создать административную группу hello и добавить одного или нескольких пользователей в группе toohello каталога. toocreate hello административной группы Azure доменных служб Active Directory, hello следующие:

1. Go toohello [классический портал Azure](https://manage.windowsazure.com).
2. В левой области hello выберите hello **Active Directory** кнопки.
3. Выберите клиент Azure AD hello (каталог), для которого требуется доменных служб tooenable Azure Active Directory. Для каждого каталога Azure AD можно создать только один домен.

    ![Выбор каталога Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. На hello **Предварительный просмотр каталога** щелкните hello **группы** вкладки.
5. Щелкните клиента tooyour Azure AD группы, в области задач hello hello нижней части окна hello tooadd **добавить группу**.

    ![Кнопка Добавить группу Hello](./media/active-directory-domain-services-getting-started/add-group-button.png)
6. В hello **добавить группу** диалогового окна поле, создайте группу с именем **Администраторы контроллера домена AAD**и задайте **тип группы** слишком**безопасности**.

   > [!WARNING]
   > tooenable доступ в том же домене управляемых доменных служб Active Directory Azure, создайте группу с указанным именем точно.
   >
   >

    ![Добавить группу Hello-диалоговое окно](./media/active-directory-domain-services-getting-started/create-admin-group.png)
7. В hello **описание** введите описание, которое позволяет другим toounderstand, что эта группа предоставляет административные разрешения в доменных службах Active Directory Azure.
8. После создания группы hello, щелкните имя tooview hello группы его свойства.
9. tooadd пользователей в качестве членов группы hello hello нижней части окна hello щелкните hello **добавить членов** кнопки.

    ![Кнопка "Добавить участников"](./media/active-directory-domain-services-getting-started/add-group-members-button.png)
10. В hello **добавление членов** диалоговое окно, выберите hello пользователей, которые должны быть членами этой группы и нажмите кнопку hello значком на hello внизу справа.

    ![Добавить группу пользователей tooadministrators](./media/active-directory-domain-services-getting-started/add-group-members.png)


## <a name="next-step"></a>Дальнейшие действия
[Задача 2. Создание или выбор виртуальной сети Azure](active-directory-ds-getting-started-vnet.md)
