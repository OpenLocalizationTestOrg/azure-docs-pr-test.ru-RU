---
title: "Руководство. Интеграция Azure Active Directory с Veritas Enterprise Vault.cloud SSO | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Veritas Enterprise Vault.cloud SSO."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: c47894b1-f5df-4755-845d-f12f4c602dc4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: fbec2cee6e1ecd23b34fd879d978a05bd5a04ac4
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-veritas-enterprise-vaultcloud-sso"></a>Руководство. Интеграция Azure Active Directory с Veritas Enterprise Vault.cloud SSO

В этом руководстве описано, как интегрировать Veritas Enterprise Vault.cloud SSO с Azure Active Directory (Azure AD).

Интеграция Veritas Enterprise Vault.cloud SSO с Azure AD обеспечивает следующие преимущества:

- С помощью Azure AD можно контролировать доступ к Veritas Enterprise Vault.cloud SSO.
- Вы можете включить автоматический вход пользователей в Veritas Enterprise Vault.cloud SSO (единый вход) с учетной записью Azure AD.
- Вы можете управлять учетными записями централизованно — через портал Azure.

Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Технические условия

Чтобы настроить интеграцию Azure AD с Veritas Enterprise Vault.cloud SSO, вам потребуется следующее:

- подписка Azure AD;
- подписка Veritas Enterprise Vault.cloud SSO с поддержкой единого входа.

> [!NOTE]
> Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.

При проверке действий в этом учебнике соблюдайте следующие рекомендации:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Сценарий, описанный в этом учебнике, состоит из двух стандартных блоков.

1. Добавление Veritas Enterprise Vault.cloud SSO из коллекции.
2. настройка и проверка единого входа в Azure AD.

## <a name="adding-veritas-enterprise-vaultcloud-sso-from-the-gallery"></a>Добавление Veritas Enterprise Vault.cloud SSO из коллекции
Чтобы настроить интеграцию Veritas Enterprise Vault.cloud SSO c Azure AD, необходимо добавить Veritas Enterprise Vault.cloud SSO из коллекции в список управляемых приложений SaaS.

**Чтобы добавить Veritas Enterprise Vault.cloud SSO из коллекции, выполните следующие действия.**

1. На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**. 

    ![Active Directory][1]

2. Перейдите к разделу **Корпоративные приложения**. Затем выберите **Все приложения**.

    ![ПРИЛОЖЕНИЯ][2]
    
3. Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.

    ![ПРИЛОЖЕНИЯ][3]

4. В поле поиска введите **Veritas Enterprise Vault.cloud SSO**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-veritas-tutorial/tutorial_veritas_search.png)

5. В области результатов выберите **Veritas Enterprise Vault.cloud SSO**, а затем нажмите кнопку **Добавить**, чтобы добавить приложение.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-veritas-tutorial/tutorial_veritas_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>настройка и проверка единого входа в Azure AD.
В этом разделе описывается настройка и проверка единого входа Azure AD в Veritas Enterprise Vault.cloud SSO с использованием тестового пользователя Britta Simon.

Для работы единого входа в Azure AD необходимо указать, какой пользователь в Veritas Enterprise Vault.cloud SSO соответствует пользователю в Azure AD. Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Veritas Enterprise Vault.cloud SSO.

Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Veritas Enterprise Vault.cloud SSO.

Чтобы настроить и проверить единый вход Azure AD в Veritas Enterprise Vault.cloud SSO, вам потребуется выполнить действия в следующих стандартных блоках:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа в Azure AD от имени пользователя Britta Simon.
3. **[Создание тестового пользователя Veritas Enterprise Vault.cloud SSO](#creating-a-veritas-enterprise-vaultcloud-sso-test-user)** требуется для создания пользователя Britta Simon в Veritas Enterprise Vault.cloud SSO, связанного с соответствующим представлением в Azure AD.
4. **[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD;
5. **[Проверка единого входа](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Veritas Enterprise Vault.cloud SSO.

**Чтобы настроить единый вход Azure AD в Veritas Enterprise Vault.cloud SSO, выполните следующие действия.**

1. На портале Azure на странице интеграции с приложением **Veritas Enterprise Vault.cloud SSO** щелкните **Единый вход**.

    ![Настройка единого входа][4]

2. В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-veritas-tutorial/tutorial_veritas_samlbase.png)

3. В разделе **Домены и URL-адреса приложения Veritas Enterprise Vault.cloud SSO** выполните следующие действия.

    ![Настройка единого входа](./media/active-directory-saas-veritas-tutorial/tutorial_veritas_url.png)

    В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://personal.ap.archive.veritas.com/CID=<CUSTOMERID>`
    
    > [!NOTE] 
    > Это значение приведено для справки. Вместо него необходимо указать фактический URL-адрес входа. Для получения этого значения обратитесь в [службу поддержки клиентов Veritas Enterprise Vault.cloud SSO](https://www.veritas.com/support/.html). 

4. В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.

    ![Настройка единого входа](./media/active-directory-saas-veritas-tutorial/tutorial_veritas_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-veritas-tutorial/tutorial_general_400.png)

6. В разделе **Конфигурация Veritas Enterprise Vault.cloud SSO** щелкните **Настроить Veritas Enterprise Vault.cloud SSO**, чтобы открыть окно**Настройка единого входа**. Скопируйте **URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.

    ![Настройка единого входа](./media/active-directory-saas-veritas-tutorial/tutorial_veritas_configure.png) 

7. Чтобы настроить единый вход на стороне **Veritas Enterprise Vault.cloud SSO**, нужно передать скачанный **сертификат в кодировке Base64** и **URL-адрес службы единого входа SAML** в [службу поддержки Veritas Enterprise Vault.cloud SSO](https://www.veritas.com/support/.html).

> [!TIP]
> Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.  После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы. Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.

![Создание пользователя Azure AD][100]

**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**

1. На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-veritas-tutorial/create_aaduser_01.png) 

2. Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-veritas-tutorial/create_aaduser_02.png) 

3. Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-veritas-tutorial/create_aaduser_03.png) 

4. На странице диалогового окна **Пользователь** выполните следующие действия.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-veritas-tutorial/create_aaduser_04.png) 

    a. В текстовом поле **Имя** введите **BrittaSimon**.

    Б. В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение поля **Пароль**.

    d. Нажмите кнопку **Создать**.
 
### <a name="creating-a-veritas-enterprise-vaultcloud-sso-test-user"></a>Создание тестового пользователя Veritas Enterprise Vault.cloud SSO

В этом разделе описано, как создать пользователя Britta Simon в Enterprise Vault.cloud SSO. Обратитесь в [службу поддержки Veritas Enterprise Vault.cloud SSO](https://www.veritas.com/support/.html), чтобы добавить пользователей на платформу Enterprise Vault.cloud SSO. Перед использованием единого входа необходимо создать и активировать пользователей.

### <a name="assigning-the-azure-ad-test-user"></a>Назначение тестового пользователя Azure AD

В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив доступ к Veritas Enterprise Vault.cloud SSO.

![Назначение пользователя][200] 

**Чтобы назначить Britta Simon в Veritas Enterprise Vault.cloud SSO, выполните следующие действия.**

1. На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений выберите **Veritas Enterprise Vault.cloud SSO**.

    ![Настройка единого входа](./media/active-directory-saas-veritas-tutorial/tutorial_veritas_app.png) 

3. В меню слева выберите **Пользователи и группы**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.

Щелкнув плитку Veritas Enterprise Vault.cloud SSO на панели доступа, вы автоматически войдете в приложение Veritas Enterprise Vault.cloud SSO.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по интеграции приложений SaaS с Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-veritas-tutorial/tutorial_general_203.png

