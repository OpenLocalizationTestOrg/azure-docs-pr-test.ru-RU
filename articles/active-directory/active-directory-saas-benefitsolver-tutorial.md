---
title: "Руководство по интеграции Azure Active Directory с Benefitsolver | Документация Майкрософт"
description: "Узнайте, как toouse Benefitsolver с Azure Active Directory tooenable единого входа, автоматизированной подготовки и многое другое!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: cf4529b1-3fb6-4475-82b7-2ceedcb70b3c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 5bb8511ef9be1e386956188a93e899d6ebe56ed5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefitsolver"></a>Руководство. Интеграция Azure Active Directory с Benefitsolver
Цель этого учебника Hello — tooshow hello интеграцию Azure и Benefitsolver.  

Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:

* Действующая подписка на Azure
* подписка на Benefitsolver с поддержкой единого входа.

После завершения этого учебника, пользователи hello Azure AD, назначенные tooBenefitsolver будут может toosingle входа в приложение hello hello [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

Hello сценарий, описанный в этом руководстве состоит из hello следующие стандартные блоки.

1. Включение интеграции приложений hello для Benefitsolver
2. Настройка единого входа.
3. Настройка подготовки учетных записей пользователей
4. Назначение пользователей

![Сценарий](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "Сценарий")

## <a name="enabling-hello-application-integration-for-benefitsolver"></a>Включение интеграции приложений hello для Benefitsolver
Hello цель этого раздела — toooutline как интеграции приложения hello tooenable для Benefitsolver.

### <a name="tooenable-hello-application-integration-for-benefitsolver-perform-hello-following-steps"></a>интеграции приложения hello tooenable для Benefitsolver, выполните следующие шаги hello.
1. В hello классический портал Azure, hello левой области навигации, выберите **Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")
2. Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.
3. Щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.
   
   ![Приложения](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "Приложения")
4. Нажмите кнопку **добавить** hello нижней части страницы приветствия.
   
   ![Добавление приложения](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "Добавление приложения")
5. На hello **что вам требуется toodo** диалоговое окно, нажмите кнопку **добавить приложение из коллекции hello**.
   
   ![Добавление приложения из коллекции](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "Добавление приложения из коллекции")
6. В hello **поле поиска**, тип **Benefitsolver**.
   
   ![Коллекция приложений](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "Коллекция приложений")
7. В области результатов hello выберите **Benefitsolver**и нажмите кнопку **завершить** tooadd приложения hello.
   
   ![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")
   
## <a name="configure-single-sign-on"></a>Настройка единого входа

Цель этого раздела Hello — toooutline как tooBenefitsolver tooauthenticate tooenable пользователей с учетной записью в Azure AD, используя федерацию на основе hello SAML протокола.  

Приложение Benefitsolver ожидает утверждения SAML hello в определенном формате, требующий tooadd настраиваемого атрибута сопоставления tooyour **атрибутов токена saml** конфигурации. 

пример Hello следующий снимок экрана для этого.

![Атрибуты](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Атрибуты")

**tooconfigure единого входа, выполните следующие шаги hello:**

1. В классический портал Azure, на hello hello **Benefitsolver** странице интеграции приложения щелкните **настроить единый вход** tooopen hello **Настройка единого входа** диалоговое окно.
   
   ![Настройка единого входа](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "Настройка единого входа")
2. На hello **предпочитаемый как toosign пользователей на tooBenefitsolver** выберите **Microsoft Azure AD Single Sign-On**, а затем нажмите кнопку **Далее**.
   
   ![Настройка единого входа](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "Настройка единого входа")
3. На hello **Настройка параметров приложения** выполните следующие шаги hello:
   
   ![Настройка параметров приложения](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "Настройка параметров приложения")
   
   1. В hello **на URL-адрес входа** введите **http://azure.benefitsolver.com**.
   2. В hello **URL-адрес ответа** введите **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.  
   3. Щелкните **Далее**.
4. На hello **настроить единый вход в Benefitsolver** страницы, toodownload метаданные, нажмите кнопку **загрузить метаданные**, а затем сохраните файл метаданных hello на локальном компьютере.
   
   ![Настройка единого входа](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "Настройка единого входа")
5. Отправьте hello загружены метаданные файла tooyour Benefitsolver поддержки.
   
   >[!NOTE]
   >Сотрудники службы поддержки Benefitsolver имеет toodo hello фактическую настройку единого входа. Как только единый вход для вашей подписки будет включен, вы получите уведомление.
   >

6. На hello классический портал Azure, выберите Подтверждение настройки единого входа hello и нажмите кнопку **завершить** tooclose hello **Настройка единого входа** диалогового окна.
   
   ![Настройка единого входа](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "Настройка единого входа")
7. В меню в верхней части hello hello выберите **атрибуты** tooopen hello **атрибутов токена SAML** диалогового окна.
   
   ![Атрибуты](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "Атрибуты")
8. сопоставления атрибутов hello необходимые tooadd, выполните hello следующие шаги.
   
   ![Атрибуты](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Атрибуты")
   
   | Имя атрибута | Значение атрибута |
   | --- | --- |
   | ClientID |Для команды поддержки Benefitsolver это значение требуется tooget. |
   | ClientKey |Для команды поддержки Benefitsolver это значение требуется tooget. |
   | LogoutURL |Для команды поддержки Benefitsolver это значение требуется tooget. |
   | EmployeeID |Для команды поддержки Benefitsolver это значение требуется tooget. |
   
   1. Для каждой строки данных в таблице hello выше, щелкните **добавить атрибут пользователя**.
   2. В hello **имя атрибута** в текстовое поле имя атрибута типа hello, показанный для этой строки.
   3. В hello **значение атрибута** текстовое поле, значение атрибута выберите hello, показанный для этой строки.
   4. Нажмите **Завершено**.
9. Нажмите кнопку **Применить изменения**.

## <a name="configure-user-provisioning"></a>Настроить подготовку учетных записей пользователей
В порядке tooenable toolog пользователей Azure AD в Benefitsolver их необходимо подготовить в Benefitsolver.  

В случае Benefitsolver hello данные о сотрудниках — в приложении, который заполняется с использованием файла переписи населения из информационной системы Персонала системы (обычно ночное время).  

>[!NOTE]
>Можно использовать любые другие Benefitsolver пользователя средства создания учетных записей или интерфейсы API, предоставляемые Benefitsolver tooprovision учетных записей пользователей AAD. 
> 

## <a name="assigning-users"></a>Назначение пользователей
tootest конфигурацию, необходимо toogrant hello Azure AD пользователей с помощью tooit доступ вашего приложения путем назначения им tooallow.

### <a name="tooassign-users-toobenefitsolver-perform-hello-following-steps"></a>tooBenefitsolver tooassign пользователей, выполните следующие шаги hello:
1. В hello классический портал Azure создайте тестовую учетную запись.
2. На hello ** Benefitsolver ** странице интеграции приложения щелкните **назначить пользователей**.
   
   ![Назначение пользователей](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "Назначение пользователей")
3. Выберите тестового пользователя, нажмите кнопку **назначить**, а затем нажмите кнопку **Да** tooconfirm назначения.
   
   ![Да](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Да")

Tootest параметры единого входа, откройте панель доступа hello. Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

