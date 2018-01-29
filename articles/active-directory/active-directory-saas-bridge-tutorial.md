---
title: "Руководство по интеграции Azure Active Directory с Bridge | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Bridge."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 3dbb6499-80c1-4d00-a0b4-e0ad5522cf0f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: e268169da774596f1bd5eaa8f97071de9c7cf63f
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bridge"></a>Руководство. Интеграция Azure Active Directory с Bridge

В этом руководстве описано, как интегрировать Bridge с Azure Active Directory (Azure AD).

Интеграция Bridge с Azure AD обеспечивает следующие преимущества.

- С помощью Azure AD вы можете контролировать доступ к Bridge.
- Вы можете включить автоматический вход пользователей в Bridge (единый вход) с учетной записью Azure AD.
- Вы можете управлять учетными записями централизованно — через портал Azure.

Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Технические условия

Чтобы настроить интеграцию Azure AD с Bridge, вам потребуется следующее:

- подписка Azure AD;
- подписка Bridge с поддержкой единого входа.

> [!NOTE]
> Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.

При проверке действий в этом учебнике соблюдайте следующие рекомендации:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Сценарий, описанный в этом учебнике, состоит из двух стандартных блоков.

1. Добавление Bridge из коллекции
2. настройка и проверка единого входа в Azure AD.

## <a name="adding-bridge-from-the-gallery"></a>Добавление Bridge из коллекции
Чтобы настроить интеграцию Bridge с Azure AD, необходимо добавить Bridge из коллекции в список управляемых приложений SaaS.

**Чтобы добавить Bridge из коллекции, выполните следующее.**

1. На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**. 

    ![Active Directory][1]

2. Перейдите к разделу **Корпоративные приложения**. Затем выберите **Все приложения**.

    ![ПРИЛОЖЕНИЯ][2]
    
3. Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.

    ![ПРИЛОЖЕНИЯ][3]

4. В поле поиска введите **Bridge**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_search.png)

5. На панели результатов выберите **Bridge** и нажмите кнопку **Добавить**, чтобы добавить это приложение.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>настройка и проверка единого входа в Azure AD.
В этом разделе описана настройка и проверка единого входа Azure AD в Bridge с использованием тестового пользователя Britta Simon.

Чтобы единый вход работал, Azure AD необходимо знать, какой пользователь в Bridge соответствует пользователю в Azure AD. Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Bridge.

Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Bridge.

Чтобы настроить и проверить единый вход Azure AD в Bridge, вам потребуется выполнить действия в следующих стандартных блоках.

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа в Azure AD от имени пользователя Britta Simon.
3. **[Создание тестового пользователя Bridge](#creating-a-bridge-test-user)** нужно для того, чтобы в Bridge также существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.
4. **[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD;
5. **[Проверка единого входа](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Bridge.

**Чтобы настроить единый вход Azure AD в Bridge, выполните следующее.**

1. На портале Azure на странице интеграции с приложением **Bridge** щелкните **Единый вход**.

    ![Настройка единого входа][4]

2. В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_samlbase.png)

3. В разделе **Домены и URL-адреса приложения Bridge** выполните следующие действия.

    ![Настройка единого входа](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_url.png)

    a. В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<company name>.bridgeapp.com`

    Б. В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<company name>.bridgeapp.com`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Замените эти значения фактическим URL-адресом для входа и идентификатором. Чтобы получить эти значения, обратитесь к [группе поддержки Bridge](https://community.bridgeapp.com/community/help). 
 
4. В разделе **Сертификат подписи SAML** щелкните **Сертификат (необработанный)**, а затем сохраните файл сертификата на компьютере.

    ![Настройка единого входа](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-bridge-tutorial/tutorial_general_400.png)

6. В разделе **Конфигурация Bridge** щелкните **Настроить Bridge**, чтобы открыть окно **Настройка единого входа**. Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.

    ![Настройка единого входа](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_configure.png) 

7. Чтобы настроить единый вход на стороне **Bridge**, нужно отправить скачанный **сертификат (необработанный)**, **идентификатор сущности SAML, URL-адрес службы единого входа SAML и URL-адрес выхода** [группе поддержки Bridge](https://community.bridgeapp.com/community/help). 

> [!TIP]
> Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.  После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы. Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.

![Создание пользователя Azure AD][100]

**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**

1. На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bridge-tutorial/create_aaduser_01.png) 

2. Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bridge-tutorial/create_aaduser_02.png) 

3. Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bridge-tutorial/create_aaduser_03.png) 

4. На странице диалогового окна **Пользователь** выполните следующие действия.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bridge-tutorial/create_aaduser_04.png) 

    a. В текстовом поле **Имя** введите **BrittaSimon**.

    Б. В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение поля **Пароль**.

    d. Нажмите кнопку **Создать**.
 
### <a name="creating-a-bridge-test-user"></a>Создание тестового пользователя Bridge

В этом разделе описано, как создать пользователя Britta Simon в Bridge. Чтобы создать пользователя на платформе, обратитесь к [группе поддержки Bridge](https://community.bridgeapp.com/community/help). Чтобы добавить пользователей на платформу Bridge, <a href="https://community.bridgeapp.com/community/help">на этой странице</a> вы можете отправить запрос в службу поддержки Bridge.

### <a name="assigning-the-azure-ad-test-user"></a>Назначение тестового пользователя Azure AD

В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Bridge.

![Назначение пользователя][200] 

**Чтобы назначить пользователя Britta Simon в Bridge, выполните следующее.**

1. На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.

    ![Назначение пользователя][201] 

2. Из списка приложений выберите **Bridge**.

    ![Настройка единого входа](./media/active-directory-saas-bridge-tutorial/tutorial_bridge_app.png) 

3. В меню слева выберите **Пользователи и группы**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.

Щелкнув элемент "Bridge" на панели доступа, вы автоматически войдете в приложение Bridge.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по интеграции приложений SaaS с Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bridge-tutorial/tutorial_general_203.png

