---
title: "Office 365 aaaUse клиента с подпиской Azure | Документы Microsoft"
description: "Узнайте, как tooadd Office 365 directory (клиент) tooan подписки Azure."
services: 
documentationcenter: 
author: JiangChen79
manager: jlian
editor: 
tags: billing,top-support-issue
ms.assetid: cc9c57c6-7bfd-4dea-9027-c75ef3737589
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: cjiang
ms.openlocfilehash: e560370417bd074a7e37ceb7c60da45dbbbcf775
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="associate-an-office-365-tenant-tooan-azure-subscription"></a>Связать tooan клиента Office 365 подписки Azure
Свяжите отдельные подписки Azure и Office 365, чтобы доступ к Office 365 hello клиента из подписки Azure. toolink подписок, вход tooAzure с hello учетной записи администратора службы Azure, добавьте каталог и добавить клиент Azure Active Directory toohello учетные записи организации hello Office 365.

Если вам необходима подписка Office 365 для пользователей в экземпляре Azure Active Directory, или у вас есть учетная запись Office 365, но нет учетной записи Azure, то см. статью [Регистрация в Azure с помощью учетной записи Office 365](billing-use-existing-office-365-account-azure-subscription.md). 

## <a name="before-you-begin"></a>Перед началом работы
* Необходимо иметь учетные данные администратора службы подписки Azure hello hello. Учетные записи соадминистратора нельзя выполнить некоторые шаги hello в этой статье. toochange администратором службы, в разделе [как tooadd или изменение роли администратора Azure](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription).
* Необходимо иметь учетные данные глобального администратора клиента Office 365 hello hello.
* адрес электронной почты администратора службы hello Hello должен отсутствовать в hello клиента Office 365.
* адрес электронной почты администратора службы hello Hello не может совпадать с любым глобальным администратором Office 365 hello клиента.
* Если вы используете адрес электронной почты учетной записи Майкрософт и учетная запись организации, временно измените администратора службы hello из вашей подписки Azure toouse другой учетной записи Майкрософт. Можно создать учетную запись Майкрософт на hello [страницу регистрации учетной записи Майкрософт](https://signup.live.com/).

## <a name="link-office-365-tenant-tooazure-subscription"></a>Привязка подписки tooAzure клиента Office 365
toohello клиента Office 365 hello tooassociate подписки Azure, выполните следующие действия.

### <a name="step-1-add-office-365-tenant-tooyour-azure-subscription"></a>Шаг 1: Добавление tooyour клиента Office 365 подписки Azure

1. Войдите в toohello [классический портал Azure](https://manage.windowsazure.com/) с учетными данными администратора службы hello.

    ![Снимок экрана входа в Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)

2. Выберите в левой области hello **ACTIVE DIRECTORY**. Не должны видеть клиента hello Office 365. Если вы видите его, пропустите слишком[шаг 2: изменение hello каталог, связанный с hello подписки Azure](#Step2).
   
   ![Снимок экрана записи Active Directory](./media/billing-add-office-365-tenant-to-azure-subscription/s35-classic-portal-active-directory-entry.png)

3. Выберите **Создать** > **Каталог** > **Настраиваемое создание**.
   
    ![Снимок экрана создания настраиваемого каталога Azure Active Directory](./media/billing-add-office-365-tenant-to-azure-subscription/s37-aad-custom-create.png)
   
4. На hello **добавить каталог** в разделе **КАТАЛОГА**выберите **использовать существующий каталог**. Выберите **я готов toobe выходу из системы**и выберите **завершить** ![завершения значок](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).
   
    ![Снимок экрана с параметром "Использовать существующий каталог"](./media/billing-add-office-365-tenant-to-azure-subscription/s39_add-directory-use-existing.png)
   
5. После выхода, войдите с использованием учетных данных глобального администратора hello вашего клиента Office 365.
   
    ![Снимок экрана входа глобального администратора Office 365](./media/billing-add-office-365-tenant-to-azure-subscription/s310_sign-in-global-admin-office-365.png)
   
6. Выберите **Продолжить**.
   
    ![Снимок экрана проверки](./media/billing-add-office-365-tenant-to-azure-subscription/s311_use-contoso-directory-azure-verify.png)
   
7. Щелкните **Выйти сейчас**.
   
    ![Снимок экрана выхода](./media/billing-add-office-365-tenant-to-azure-subscription/s312_use-contoso-directory-azure-confirm-and-sign-out.png)
   
8. Войдите в toohello [классический портал Azure](https://manage.windowsazure.com/) с учетными данными администратора службы hello.
   
    ![Снимок экрана входа в Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)
   
9. Вы увидите клиента Office 365 на панели мониторинга hello.
   
    ![Снимок экрана панели мониторинга](./media/billing-add-office-365-tenant-to-azure-subscription/s314_office-365-tenant-appear-in-azure.png)

### <a name="Step2"></a>Шаг 2: Изменение каталога hello, hello подписки Azure
   
1. Выберите элемент **Параметры**.
   
    ![Снимок экрана со значком настройки на классическом портале Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s315_azure-classic-portal-settings-icon.png)
   
2. Выберите свою подписку Azure и щелкните **Изменить каталог**.

    ![Снимок экрана изменения каталога подписки Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s316_azure-subscription-edit-directory.png)
   
3. Щелкните **Далее** ![значок "Далее"](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png).
   
    ![Снимок экрана: «Изменение hello связанный каталог»](./media/billing-add-office-365-tenant-to-azure-subscription/s318_azure-change-associated-directory.png)
   
4. Просмотрите учетные записи для затронутых hello. Все соадминистраторы и [управление доступом на основе ролей (RBAC)](../active-directory/role-based-access-control-configure.md) пользователи с ограниченным доступом к в существующих группах ресурсов hello, удаляются. Предупреждение Hello упоминаются только hello удаление администраторов.
      
    ![Снимок экрана, показывающий hello toobe удалены учетные записи соадминистратора.](./media/billing-add-office-365-tenant-to-azure-subscription/s322_azure-confirm-directory-mapping.png)
   
    ![Снимок экрана, показывающий toobe учетной записи пользователя примере удаляются.](./media/billing-add-office-365-tenant-to-azure-subscription/s325_assigned-users-removed-resource-groups.png)
   
5. Щелкните **Завершить** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).

### <a name="step-3-add-your-office-365-organizational-accounts-as-co-administrators-toohello-azure-active-directory-tenant"></a>Шаг 3: Добавьте учетные записи организации Office 365 в качестве администраторов клиента Azure Active Directory toohello
   
1. Выберите hello **АДМИНИСТРАТОРЫ** , а затем выберите **добавить**.
   
    ![Снимок экрана вкладки настройки администраторов на классическом портале Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s319_azure-classic-portal-settings-administrators.png)
   
2. Укажите учетную запись организации вашего клиента Office 365, выберите hello подписки Azure и затем выберите **завершить** ![завершения значок](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).
   
    ![Снимок экрана диалогового окна добавления соадминистратора Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s320_azure-add-co-administrator.png)
   
3. Вернитесь к предыдущему окну toohello **АДМИНИСТРАТОРЫ** вкладки. Вы увидите hello учетная запись организации отображается в качестве соадминистратора.
   
    ![Снимок экрана вкладки "Администраторы"](./media/billing-add-office-365-tenant-to-azure-subscription/s321_azure-co-administrator-added.png)
4.  Тест tooAzure доступ с помощью учетной записи соадминистратора hello.
   
    а. Выйдите из hello классический портал Azure.
   
    b. Откройте hello [портал Azure](https://portal.azure.com/).
   
    c. Введите учетные данные hello hello совместного администратора, а затем выберите **входа**.
   
    ![Снимок экрана страницы входа в Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s324_azure-sign-in-with-co-admin.png)

## <a name="need-help-contact-support"></a>Требуется помощь? Обратитесь в службу поддержки.
Если вы по-прежнему нужна помощь, [обратитесь в службу поддержки](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget быстро устранить проблему.


