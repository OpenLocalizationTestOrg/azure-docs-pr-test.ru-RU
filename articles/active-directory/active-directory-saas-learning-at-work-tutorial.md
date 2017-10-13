---
title: "Учебник. Интеграция Azure Active Directory с Learning at Work | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Learning at Work."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d607174-bea1-4f40-8233-54cabe02c66a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: jeedes
ms.openlocfilehash: 941832740689c583a8e857d706c35f3076fa754f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learning-at-work"></a>Руководство. Интеграция Azure Active Directory с Learning at Work

В этом руководстве описано, как интегрировать Azure Active Directory (Azure AD) с приложением Learning at Work.

Интеграция Learning at Work с Azure AD обеспечивает следующие преимущества.

- С помощью Azure AD вы можете контролировать доступ к Learning at Work.
- Вы можете включить автоматический вход пользователей в Learning at Work (единый вход) с учетной записью Azure AD.
- Вы можете управлять учетными записями централизованно — через портал Azure.

Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

Чтобы настроить интеграцию Azure AD с Learning at Work, вам потребуется:

- подписка Azure AD;
- подписка Learning at Work с поддержкой единого входа.

> [!NOTE]
> Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.

При проверке действий в этом учебнике соблюдайте следующие рекомендации:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Сценарий, описанный в этом учебнике, состоит из двух основных блоков:

1. Добавление Learning at Work из коллекции.
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-learning-at-work-from-the-gallery"></a>Добавление Learning at Work из коллекции.
Чтобы настроить интеграцию Learning at Work с Azure AD, необходимо добавить Learning at Work из коллекции в список управляемых приложений SaaS.

**Чтобы добавить Learning at Work из коллекции, сделайте следующее:**

1. На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**. 

    ![Active Directory][1]

2. Перейдите к разделу **Корпоративные приложения**. Затем выберите **Все приложения**.

    ![Приложения][2]
    
3. Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.

    ![Приложения][3]

4. В поле поиска введите **Learning at Work**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_search.png)

5. На панели результатов выберите **Learning at Work** и нажмите кнопку **Добавить**, чтобы добавить приложение.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Learning at Work с использованием тестового пользователя Britta Simon.

Для работы единого входа в Azure AD необходимо знать, какой пользователь в Learning at Work соответствует пользователю в Azure AD. Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Learning at Work.

Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Learning at Work.

Чтобы настроить и проверить единый вход Azure AD в Learning at Work, вам потребуется выполнить действия в следующих стандартных блоках.

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.
3. **[Создание тестового пользователя Learning at Work](#creating-a-learning-at-work-test-user)** требуется для создания в Learning at Work пользователя Britta Simon, связанного с соответствующим представлением в Azure AD.
4. **[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.
5. **[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Learning at Work.

**Чтобы настроить единый вход Azure AD в Learning at Work, сделайте следующее:**

1. На портале Azure на странице интеграции с приложением **Learning at Work** щелкните **Единый вход**.

    ![Настройка единого входа][4]

2. В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_samlbase.png)

3. В разделе **Домены и URL-адреса приложения Learning at Work** выполните следующие действия:

    ![Настройка единого входа](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_url.png)

    а. В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<subdomain>.sabacloud.com/Saba/Web/<company code>`

    b. В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<subdomain>.sabacloud.com/Saba/saml/SSO/alias/<company name>`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Замените эти значения фактическим URL-адресом для входа и идентификатором. Чтобы получить их, обратитесь в [службу поддержки клиентов Learning at Work](https://www.learninga-z.com/site/contact/support). 
 
4. В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.

    ![Настройка единого входа](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_400.png)

6. В разделе **Конфигурация Learning at Work** щелкните **Настроить Learning at Work**, чтобы открыть окно **Настройка единого входа**. Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.

    ![Настройка единого входа](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_configure.png) 

7. Чтобы настроить единый вход на стороне **Learning at Work**, нужно отправить скачанный **XML-файл метаданных**, **идентификатор сущности SAML**, **URL-адрес службы единого входа SAML** и **URL-адрес выхода** в [службу поддержки Learning at Work](https://www.learninga-z.com/site/contact/support).

> [!TIP]
> Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.  После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы. Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.

![Создание пользователя Azure AD][100]

**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**

1. На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_01.png) 

2. Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_02.png) 

3. Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_03.png) 

4. На странице диалогового окна **Пользователь** выполните следующие действия.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-learning-at-work-tutorial/create_aaduser_04.png) 

    а. В текстовом поле **Имя** введите **BrittaSimon**.

    b. В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение поля **Пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-learning-at-work-test-user"></a>Создание тестового пользователя Learning at Work

В этом разделе описано, как создать пользователя Britta Simon в приложении Learning at Work. Обратитесь в [службу поддержки Learning at Work](https://www.learninga-z.com/site/contact/support), чтобы добавить пользователей на платформу Learning at Work.

### <a name="assigning-the-azure-ad-test-user"></a>Назначение тестового пользователя Azure AD

В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив доступ к Learning at Work.

![Назначение пользователя][200] 

**Чтобы назначить пользователя Britta Simon в Learning at Work, сделайте следующее:**

1. На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений выберите **Learning at Work**.

    ![Настройка единого входа](./media/active-directory-saas-learning-at-work-tutorial/tutorial_learningatwork_app.png) 

3. В меню слева выберите **Пользователи и группы**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.

Щелкнув элемент Learning at Work на панели доступа, вы автоматически войдете в приложение Learning at Work.
Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по интеграции приложений SaaS с Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learning-at-work-tutorial/tutorial_general_203.png

