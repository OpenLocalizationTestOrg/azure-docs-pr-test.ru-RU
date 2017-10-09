---
title: "aaaAdd tooAzure новых пользователей Active Directory | Документы Microsoft"
description: "Объясняет, как tooadd новых пользователей в Azure Active Directory."
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jeffgilb
ms.reviewer: jsnow
ms.custom: it-pro
ms.openlocfilehash: 6ca413c84a7a5238a30fd26fc751d687d827b24a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-add-new-users-tooazure-active-directory"></a>Краткое руководство: Добавление новых пользователей tooAzure Active Directory
В этой статье объясняется, как tooadd новых пользователей в вашей организации в Azure Active Directory (Azure AD) hello один одновременно с помощью hello портал Azure или путем синхронизации локальных пользователей Windows Server AD учетной записи данных. 

## <a name="add-cloud-based-users"></a>Добавление облачных пользователей
1. Войдите в toohello [Центр администрирования Azure Active Directory](https://aad.portal.azure.com) с помощью учетной записи глобального администратора каталога hello.
2. Выберите **Azure Active Directory**, а затем щелкните **Пользователи и группы**.
3. На hello **пользователей и групп** колонке выберите **всех пользователей**, а затем выберите **нового пользователя**.
   ![При выборе команды Добавить hello](./media/add-users-azure-active-directory/add-user.png)
4. Введите сведения для пользователя hello, таких как **имя** и **имя пользователя**. Hello часть имени домена имя пользователя hello должны быть hello начальное значение по умолчанию домена имя «[домен].onmicrosoft.com» или проверенных, не являющихся федеративными [пользовательское имя домена](add-custom-domain.md) например «contoso.com».
5. Копирование или в противном случае Примечание hello создать пароль пользователя, таким образом, чтобы можно предоставить его toohello пользователя после завершения этого процесса.
6. При необходимости можно открыть и заполните сведения hello в hello **профиль** колонки, hello **группы** колонке или hello **роли каталога** колонку для пользователя hello. Дополнительные сведения о ролях пользователей и администраторов см. в статье [Назначение ролей администратора в Azure AD](active-directory-assign-admin-roles.md).
7. На hello **пользователя** колонке выберите **создать**.
8. Безопасно распространите hello созданный пароль toohello нового пользователя, чтобы hello пользователь сможет войти в.

> [!TIP]
> Вы также можете синхронизировать данные учетной записи пользователя из локальной среды Windows Server AD. Решения по управлению удостоверениями корпорации Майкрософт используют локальных и облачных, возможности создания удостоверения одного пользователя для проверки подлинности и авторизации tooall ресурсов, независимо от расположения. Мы называем это гибридной идентификацией. [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) может быть используется toointegrate локальных каталогов с Azure Active Directory для гибридных удостоверений сценариев. Это позволяет tooprovide общего удостоверения для пользователей для приложений Office 365, Azure и SaaS интегрированы с Azure AD. 

## <a name="delete-users-from-azure-ad"></a>Удалить пользователей из Azure AD
1. Войдите в toohello [Центр администрирования Azure Active Directory](https://aad.portal.azure.com) с помощью учетной записи глобального администратора каталога hello.
2. Выберите **Пользователи и группы**.
3. На hello **пользователей и групп** колонки, toodelete hello выберите пользователя из списка hello. 
4. В колонке hello для выбранного пользователя hello, выберите **Обзор**и выберите в панели команд hello, **удалить**.
   ![При выборе команды Добавить hello](./media/add-users-azure-active-directory/delete-user.png)


### <a name="learn-more"></a>Подробнее 
* [Добавление внешнего пользователя](active-directory-users-create-external-azure-portal.md)

* [Назначьте роль tooa пользователя в Azure AD](active-directory-users-assign-role-azure-portal.md)

## <a name="next-steps"></a>Дальнейшие действия
В этом кратком руководстве вы узнали, как новый tooadd tooAzure пользователей AD Premium. 

Можно использовать следующую ссылку toocreate нового пользователя в Azure AD из портала Azure hello hello.

> [!div class="nextstepaction"]
> [Добавление пользователей tooAzure AD](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All users) 
