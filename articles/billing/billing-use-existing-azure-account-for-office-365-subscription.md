---
title: "aaaSign для Office 365 с учетной записью Azure | Документы Microsoft"
description: "Узнайте, как Office 365 toocreate подписки с помощью учетной записи Azure"
services: 
documentationcenter: 
author: JiangChen79
manager: adpick
editor: 
tags: billing,top-support-issue
ms.assetid: 
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: cjiang
ms.openlocfilehash: d19e1c1edff0b9658b639e796a72bbf4e87b9c3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sign-up-for-an-office-365-subscription-with-your-azure-account"></a>Регистрация для подписки Office 365 с помощью учетной записи Azure
Если вы подписчик Azure, можно использовать toosign вашей учетной записи Azure для подписки Office 365. Если вы работаете в организации, которая имеет подписку Azure, то вы можете создать подписку Office 365 для пользователей в существующей службе Azure Active Directory (Azure AD). После регистрации tooOffice 365, используя учетную запись с разрешениями глобального администратора или администратором выставления счетов в клиенте Azure Active Directory. Дополнительные сведения см. в разделе [Проверка разрешений учетной записи в Azure AD](#RoleInAzureAD) и в статье [Назначение ролей администратора в Azure Active Directory](../active-directory/active-directory-assign-admin-roles.md).

При наличии учетной записи Office 365 и подписки Azure, вы можете [связать tooan клиента Office 365 подписки Azure](billing-add-office-365-tenant-to-azure-subscription.md).

## <a name="get-an-office-365-subscription-by-using-your-azure-account"></a>Оформление подписки Office 365 с помощью учетной записи Azure

1. Go toohello [страницу продукта Office 365](https://products.office.com/business)и выберите план.
2. Нажмите кнопку **входа** в правом верхнем углу hello страницы приветствия.

    ![снимок экрана со страницы пробной версии Office 365](./media/billing-use-existing-azure-account-office-365-subscription/12-office-365-trial-page.png)
3. Войдите, используя свои учетные данные Azure. При создании подписки для вашей организации, используйте учетная запись Azure, которая является членом hello глобальным администратором или администратором выставления счетов роли каталога в клиенте Azure Active Directory.

    ![Снимок экрана с входом в Office 365](./media/billing-use-existing-azure-account-office-365-subscription/13-office-365-sign-in.png)
4. Щелкните **Попробовать**.

    ![Снимок экрана, на котором показано уведомление о подтверждении заказа Office 365.](./media/billing-use-existing-azure-account-office-365-subscription/14-office-365-confirm-your-order.png)
5. На странице подтверждения заказа hello щелкните **Продолжить**.

    ![Снимок экрана получения заказа hello Office 365](./media/billing-use-existing-azure-account-office-365-subscription/15-office-365-order-receipt.png)

Теперь все готово. При создании подписки Office 365 hello для вашей организации, используйте следующие шаги toocheck, пользователи Azure AD теперь находятся в Office 365 hello.

1. Откройте Центр администрирования Office 365 hello.
2. Разверните раздел **Пользователи** и выберите **Активные пользователи**.

    ![Снимок экрана пользователей Центр администрирования Office 365 hello](./media/billing-use-existing-azure-account-office-365-subscription/16-office-365-admin-center-users.png)

После регистрации подписки Office 365 hello добавляется toohello же экземпляр Azure Active Directory, который принадлежит подписке Azure. Дополнительные сведения см. в разделе [Справочная информация о подписках Azure и Office 365](billing-use-existing-office-365-account-azure-subscription.md#more-about-subs) и в статье [Связь между подписками Azure и службой Azure Active Directory](../active-directory/active-directory-how-subscriptions-associated-directory.md).

## <a id="RoleInAzureAD"></a>Проверка разрешений учетной записи в Azure AD
1. Войдите в toohello [портал Azure](https://portal.azure.com/).
2. Щелкните **Больше служб** и найдите **Active Directory**.

    ![Снимок экрана Active Directory в hello портал Azure](./media/billing-use-existing-azure-account-office-365-subscription/billing-more-services-active-directory.png)
3. Щелкните **Пользователи и группы** > **Все пользователи**.
4. Выберите имя пользователя hello. 

    ![Снимок экрана, показывающий hello пользователей Azure Active Directory](./media/billing-use-existing-azure-account-office-365-subscription/billing-users-groups.png)

5. Щелкните **Роль каталога**.
  
    ![Снимок экрана, показывающий роли Azure портала каталога hello](./media/billing-use-existing-azure-account-office-365-subscription/billing-user-directory-role.png)
6.  роль Hello **глобального администратора** или **ограниченные Администраторы** > **администратор выставления счетов** является обязательным toocreate подписки Office 365 для пользователей в существующих Azure Active Directory.

    ![Снимок экрана, на котором показана роль каталога "Администратор выставления счетов" на портале Azure](./media/billing-use-existing-azure-account-office-365-subscription/billing-directoryrole-limited.png)

## <a name="need-help-contact-support"></a>Требуется помощь? Обратитесь в службу поддержки.
Если вы по-прежнему нужна помощь, [обратитесь в службу поддержки](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget быстро устранить проблему. 
