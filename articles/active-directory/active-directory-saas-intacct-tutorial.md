---
title: "Учебник. Интеграция Azure Active Directory с Intacct | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Intacct."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 92518e02-a62c-4b1b-a8e9-2803eb2b49ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: c203b192b9da0d280cbd7f6c123219242ee4a3d1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intacct"></a>Руководство. Интеграция Azure Active Directory с Intacct

В этом руководстве описано, как интегрировать Intacct с Azure Active Directory (Azure AD).

Интеграция Azure AD с приложением Intacct обеспечивает следующие преимущества:

- С помощью Azure AD вы можете контролировать доступ к Intacct.
- Вы можете включить автоматический вход пользователей в Intacct (единый вход) с учетной записью Azure AD.
- Вы можете управлять учетными записями централизованно — через портал Azure.

Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

Чтобы настроить интеграцию Azure AD с Intacct, вам потребуется:

- подписка Azure AD;
- подписка с поддержкой единого входа Intacct.

> [!NOTE]
> Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.

При проверке действий в этом учебнике соблюдайте следующие рекомендации:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Сценарий, описанный в этом учебнике, состоит из двух основных блоков:

1. Добавление Intacct из коллекции
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-intacct-from-the-gallery"></a>Добавление Intacct из коллекции
Чтобы настроить интеграцию Intacct с Azure AD, необходимо добавить Intacct из коллекции в список управляемых приложений SaaS.

**Чтобы добавить Intacct из коллекции, выполните следующие действия.**

1. На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**. 

    ![Active Directory][1]

2. Перейдите к разделу **Корпоративные приложения**. Затем выберите **Все приложения**.

    ![Приложения][2]
    
3. Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.

    ![Приложения][3]

4. В поле поиска введите **Intacct**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_search.png)

5. На панели результатов выберите **Intacct** и нажмите кнопку **Добавить**, чтобы добавить приложение.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Intacct с использованием тестового пользователя Britta Simon.

Чтобы единый вход работал, Azure AD необходимо знать, какой пользователь в Intacct соответствует пользователю в Azure AD. Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Intacct.

Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Intacct.

Чтобы настроить и проверить единый вход Azure AD в Intacct, вам потребуется выполнить действия в следующих стандартных блоках:

1. **[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.
3. **[Создание тестового пользователя Intacct](#creating-an-intacct-test-user)** требуется для создания пользователя Britta Simon в Intacct, связанного с соответствующим представлением в Azure AD.
4. **[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.
5. **[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В данном разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Intacct.

**Чтобы настроить единый вход Azure AD в Intacct, сделайте следующее:**

1. На портале Azure на странице интеграции с приложением **Intacct** выберите **Единый вход**.

    ![Настройка единого входа][4]

2. В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_samlbase.png)

3. В разделе **Домены и URL-адреса приложения Intacct** сделайте следующее:

    ![Настройка единого входа](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_url.png)

    В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате:
    | |
    |--|
    | `https://<companyname>.intacct.com/ia/acct/sso_response.phtml`|
    | `https://www.intacct.com/ia/acct/sso_response.phtml` |

    > [!NOTE] 
    > Это значение приведено для справки. Вместо него нужно указать фактический URL-адрес ответа. Чтобы получить эти значения, обратитесь в [службу поддержки Intacct](https://us.intacct.com/support).

4. В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.

    ![Настройка единого входа](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-intacct-tutorial/tutorial_general_400.png)

6. В разделе **Конфигурация Intacct** щелкните **Настроить Intacct**, чтобы открыть окно **Настройка единого входа**. Скопируйте **идентификатор сущности SAML и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.

    ![Настройка единого входа](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_configure.png) 

7. В другом окне веб-браузера войдите на корпоративный сайт Intacct в качестве администратора.

8. Откройте вкладку **Company** (Компания) и выберите **Company Info** (Сведения о компании).

    ![Организация](./media/active-directory-saas-intacct-tutorial/ic790037.png "Организация")

9. Откройте вкладку **Security** (Безопасность) и нажмите кнопку **Edit** (Изменить).

    ![Безопасность](./media/active-directory-saas-intacct-tutorial/ic790038.png "Безопасность")

10. В разделе **Единый вход** сделайте следующее:

    ![Единый вход](./media/active-directory-saas-intacct-tutorial/ic790039.png "Единый вход")

    а. Установите флажок **Включить единый вход**.

    b. Выберите для параметра **Identity provider type** (Тип поставщика удостоверений) значение **SAML 2.0**.

    c. В текстовое поле **URL-адрес издателя** вставьте значение **идентификатора сущности SAML**, скопированное на портале Azure.
   
    г) В текстовое поле **URL-адрес входа** вставьте значение **URL-адреса службы единого входа SAML**, скопированное на портале Azure.

    д. Откройте в блокноте **сертификат в кодировке Base-64**, скопируйте его содержимое в буфер обмена, а затем вставьте его в поле **Сертификат**.
   
    f. Щелкните **Сохранить**.

> [!TIP]
> Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.  После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы. Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.

![Создание пользователя Azure AD][100]

**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**

1. На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_01.png) 

2. Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_02.png) 

3. Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_03.png) 

4. На странице диалогового окна **Пользователь** выполните следующие действия.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_04.png) 

    а. В текстовом поле **Имя** введите **BrittaSimon**.

    b. В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение поля **Пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-an-intacct-test-user"></a>Создание тестового пользователя Intacct

Чтобы пользователи Azure AD могли входить в Intacct, их необходимо подготовить для Intacct. Эта подготовка для Intacct выполняется вручную.

**Чтобы подготовить учетные записи пользователей, выполните следующие действия.**

1. Войдите в клиент **Intacct**.

2. Откройте вкладку **Company** (Компания) и выберите **Users** (Пользователи).

    ![Пользователи](./media/active-directory-saas-intacct-tutorial/ic790041.png "Пользователи")
3. Откройте вкладку **Добавить**.

    ![Добавление](./media/active-directory-saas-intacct-tutorial/ic790042.png "Добавление")
4. В разделе **Информация о пользователе** сделайте следующее:

    ![Сведения о пользователе](./media/active-directory-saas-intacct-tutorial/ic790043.png "Сведения о пользователе")

    а. В разделе **User Information** (Сведения пользователя) введите значения **User ID** (Идентификатор пользователя), **Last Name** (Фамилия), **First name** (Имя), **Email address** (Адрес электронной почты), **Title** (Обращение) и **Phone** (Телефон) учетной записи Azure AD, которую вы хотите подготовить.

    b. Выберите параметр **Полномочия администратора** для учетной записи Azure AD, которую требуется подготовить.
   
    c. Щелкните **Сохранить**. Владелец учетной записи Azure AD получит по электронной почте сообщение со ссылкой для активации учетной записи.

>[!NOTE]
>Для подготовки учетных записей пользователя Azure AD вы можете использовать любые другие средства создания учетной записи пользователя Intacct или API, предоставляемые Intacct.
        
### <a name="assigning-the-azure-ad-test-user"></a>Назначение тестового пользователя Azure AD

В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив ему доступ к Intacct.

![Назначение пользователя][200] 

**Чтобы назначить пользователя Britta Simon в Intacct, выполните следующие действия:**

1. На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений выберите **Intacct**.

    ![Настройка единого входа](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_app.png) 

3. В меню слева выберите **Пользователи и группы**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.

Если вы щелкните плитку Intacct на панели доступа, вы автоматически войдете в приложение Intacct.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по интеграции приложений SaaS с Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_203.png

