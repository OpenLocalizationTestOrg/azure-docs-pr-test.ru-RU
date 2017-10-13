---
title: "Руководство по интеграции Azure Active Directory с QuickHelp | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и QuickHelp."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 655c9ad3-2076-4e2c-8e47-9ed3bf04be56
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: jeedes
ms.openlocfilehash: 1c72b0ddee636090129dab7a5c7ec6ffd452434a
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-quickhelp"></a>Руководство. Интеграция Azure Active Directory с QuickHelp

В этом руководстве описано, как интегрировать QuickHelp с Azure Active Directory (Azure AD).

Интеграция Azure AD с приложением QuickHelp обеспечивает следующие преимущества:

- с помощью Azure AD вы можете контролировать доступ к QuickHelp;
- вы можете включить автоматический вход пользователей в QuickHelp (единый вход) под учетной записью Azure AD;
- Вы можете управлять учетными записями централизованно — через портал Azure.

Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

Чтобы настроить интеграцию Azure AD с QuickHelp, вам потребуется:

- подписка Azure AD;
- подписка QuickHelp с поддержкой единого входа.

> [!NOTE]
> Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.

При проверке действий в этом учебнике соблюдайте следующие рекомендации:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Сценарий, описанный в этом учебнике, состоит из двух основных блоков:

1. Добавление QuickHelp из коллекции
2. Настройка и проверка единого входа в Azure AD.

## <a name="adding-quickhelp-from-the-gallery"></a>Добавление QuickHelp из коллекции
Чтобы настроить интеграцию QuickHelp с Azure AD, необходимо добавить QuickHelp из коллекции в список управляемых приложений SaaS.

**Чтобы добавить QuickHelp из коллекции, выполните следующие действия.**

1. На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**. 

    ![Active Directory][1]

2. Перейдите к разделу **Корпоративные приложения**. Затем выберите **Все приложения**.

    ![Приложения][2]
    
3. Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.

    ![Приложения][3]

4. В поле поиска введите **QuickHelp**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_search.png)

5. На панели результатов выберите **QuickHelp**, а затем нажмите кнопку **Добавить**, чтобы добавить это приложение.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в QuickHelp с использованием тестового пользователя Britta Simon.

Чтобы единый вход работал, Azure AD необходима информация о том, какой пользователь в QuickHelp соответствует пользователю в Azure AD. Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в QuickHelp.

Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в QuickHelp.

Чтобы настроить и проверить единый вход Azure AD в QuickHelp, вам потребуется выполнить действия в следующих стандартных блоках:

1. **[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.
3. **[Создание тестового пользователя QuickHelp](#creating-a-quickhelp-test-user)** требуется для того, чтобы в QuickHelp существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.
4. **[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.
5. **[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении QuickHelp.

**Чтобы настроить единый вход Azure AD в QuickHelp, выполните следующие действия:**

1. На портале Azure на странице интеграции с приложением **QuickHelp** щелкните **Единый вход**.

    ![Настройка единого входа][4]

2. В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_samlbase.png)

3. В разделе **Домены и URL-адреса приложения QuickHelp** выполните следующие действия.

    ![Настройка единого входа](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_url.png)

    а. В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://quickhelp.com/<instancename>/#/Login`

    b. В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<subdomain>.quickhelp.com`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Замените эти значения фактическим URL-адресом для входа и идентификатором. Чтобы получить эти значения, обратитесь к [группе поддержки QuickHelp](https://support.quickhelp.com/). 
 
4. В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.

    ![Настройка единого входа](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-quickhelp-tutorial/tutorial_general_400.png) 

6. Выполните вход на сайт компании QuickHelp в качестве администратора.

7. В верхнем меню щелкните **Администратор**.
   
    ![Настройка единого входа][21]

8. В меню **QuickHelp Admin** (Администратор QuickHelp) щелкните **Settings** (Параметры).
   
    ![Настройка единого входа][22]

9. Щелкните **Authentication Settings**(Параметра аутентификации).

10. На странице **Параметры проверки подлинности** выполните следующие действия.
   
    ![Настройка единого входа][23]
   
    а. Для параметра **SSO Type** (Тип SSO) выберите значение **WSFederation**.
   
    b. Чтобы передать скачанный файл метаданных Azure, нажмите кнопку **Browse** (Обзор), перейдите к файлу и щелкните **Upload Metadata** (Передать метаданные).
   
    c. В текстовое поле **Email** (Электронная почта) введите `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.
   
    г) В текстовое поле **First Name** (Имя) введите `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.
   
    д. В текстовое поле **Last Name** (Фамилия) введите `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.
   
    f. На **панели действий** щелкните **Save** (Сохранить).

> [!TIP]
> Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.  После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы. Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.

![Создание пользователя Azure AD][100]

**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**

1. На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_01.png) 

2. Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_02.png) 

3. Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_03.png) 

4. На странице диалогового окна **Пользователь** выполните следующие действия.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_04.png) 

    а. В текстовом поле **Имя** введите **BrittaSimon**.

    b. В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение поля **Пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-quickhelp-test-user"></a>Создание тестового пользователя QuickHelp

Цель этого раздела — создать пользователя с именем Britta Simon в QuickHelp.
Чтобы единый вход работал, Azure AD необходима информация о том, какой пользователь в QuickHelp соответствует пользователю в Azure AD. Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в QuickHelp.

QuickHelp поддерживает JIT-подготовку. Это означает, что при необходимости учетная запись пользователя автоматически создается в QuickHelp и связывается с учетной записью Azure AD.

В этом разделе никакие действия с вашей стороны не требуются.

### <a name="assigning-the-azure-ad-test-user"></a>Назначение тестового пользователя Azure AD

В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к QuickHelp.

![Назначение пользователя][200] 

**Чтобы назначить пользователя Britta Simon в QuickHelp, выполните следующие действия.**

1. На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений выберите **QuickHelp**.

    ![Настройка единого входа](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_app.png) 

3. В меню слева выберите **Пользователи и группы**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.  

Щелкнув плитку QuickHelp на панели доступа, вы автоматически войдете в приложение QuickHelp.


## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по интеграции приложений SaaS с Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_203.png
[21]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_05.png
[22]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_06.png
[23]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_07.png
