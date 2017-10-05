---
title: "Учебник. Интеграция Azure Active Directory с EverBridge | Документы Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в EverBridge."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 58d7cd22-98c0-4606-9ce5-8bdb22ee8b3e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: f5a97fc8df978dd55a73ae53516a82f884c14bec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-everbridge"></a>Руководство по интеграции Azure Active Directory с Everbridge

В этом руководстве описано, как интегрировать EverBridge с Azure Active Directory (Azure AD).

Интеграция EverBridge с Azure AD обеспечивает следующие преимущества.

- С помощью Azure AD можно управлять доступом к EverBridge.
- Вы можете включить автоматический вход пользователей в EverBridge (единый вход) с учетной записью Azure AD.
- Вы можете управлять учетными записями централизованно — через портал Azure.

Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

Чтобы настроить интеграцию Azure AD с EverBridge, вам потребуется:

- подписка Azure AD;
- подписка EverBridge с поддержкой единого входа.

> [!NOTE]
> Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.

При проверке действий в этом учебнике соблюдайте следующие рекомендации:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Сценарий, описанный в этом учебнике, состоит из двух основных блоков:

1. Добавление EverBridge из коллекции
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-everbridge-from-the-gallery"></a>Добавление EverBridge из коллекции
Чтобы настроить интеграцию EverBridge с Azure AD, необходимо добавить EverBridge из коллекции в список управляемых приложений SaaS.

**Чтобы добавить EverBridge из коллекции, выполните следующие действия.**

1. На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**. 

    ![Active Directory][1]

2. Перейдите к разделу **Корпоративные приложения**. Затем выберите **Все приложения**.

    ![Приложения][2]
    
3. Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.

    ![Приложения][3]

4. В поле поиска введите **EverBridge**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_search.png)

5. На панели результатов выберите **EverBridge** и нажмите кнопку **Добавить**, чтобы добавить приложение.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в приложение EverBridge с использованием тестового пользователя Britta Simon.

Для работы единого входа в Azure AD необходимо знать, какой пользователь в EverBridge соответствует пользователю в Azure AD. Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в EverBridge.

Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в EverBridge.

Чтобы настроить и проверить единый вход Azure AD в EverBridge, необходимо выполнить действия в следующих стандартных блоках.

1. **[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.
3. **[Создание тестового пользователя EverBridge](#creating-an-everbridge-test-user)** требуется для создания в EverBridge пользователя Britta Simon, связанного с представлением этого же пользователя в Azure AD.
4. **[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.
5. **[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении EverBridge.

**Чтобы настроить единый вход Azure AD в EverBridge, выполните следующие действия.**

1. На портале Azure на странице интеграции с приложением **EverBridge** щелкните **Единый вход**.

    ![Настройка единого входа][4]

2. В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_samlbase.png)

3. В разделе **Домен и URL-адреса приложения EverBridge** выполните следующие действия.

    ![Настройка единого входа](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_url.png)

    а. В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://sso.everbridge.net/<companyname>`

    b. В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://manager.everbridge.net/saml/SSO/<companyname>/alias/defaultAlias`.

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Измените их на фактические значения идентификатора и URL-адреса ответа. Чтобы получить эти значения, обратитесь в [службу поддержки EverBridge](mailto:support@everbridge.com).
 
4. В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.

    ![Настройка единого входа](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-everbridge-tutorial/tutorial_general_400.png)

6. В разделе **Настройка EverBridge** щелкните **Настроить EverBridge**, чтобы открыть окно **Настройка единого входа**. Скопируйте **URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.

    ![Настройка единого входа](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_configure.png) 

6. Чтобы настроить для приложения единый вход, нужно войти в клиент приложения Everbridge с правами администратора.

7. В меню в верхней части страницы откройте вкладку **Settings** (Параметры) и выберите пункт **Single Sign-On** (Единый вход) в разделе **Security** (Безопасность).
   
    ![Настройка единого входа](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_002.png)
   
    а. В текстовом поле **Name** (Имя) введите имя поставщика идентификаторов (например, название своей компании).
   
    b. В текстовом поле **API Name** (Имя API) введите имя API.
   
    c. Чтобы отправить файл метаданных, скачанный на портале Azure, нажмите кнопку **Выбрать файл**.
   
    г) В поле "Расположение удостоверения SAML" выберите значение **Identity is in the NameIdentifier element of the Subject statement** (Удостоверение находится в элементе NameIdentifier оператора Subject).
   
    д. В текстовом поле **URL-адрес для входа поставщика удостоверений** вставьте значение URL-адреса единого входа SAML из Azure AD.
   
    ![Настройка единого входа](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_003.png)
   
    Е. В поле "Service Provider Initiated Request Binding" (Связывание запросов, инициированных поставщиком услуг) выберите **HTTP Redirect** (Перенаправление HTTP).

    g. Нажмите кнопку **Сохранить**

> [!TIP]
> Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.  После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы. Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.

![Создание пользователя Azure AD][100]

**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**

1. На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-everbridge-tutorial/create_aaduser_01.png) 

2. Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-everbridge-tutorial/create_aaduser_02.png) 

3. Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-everbridge-tutorial/create_aaduser_03.png) 

4. На странице диалогового окна **Пользователь** выполните следующие действия.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-everbridge-tutorial/create_aaduser_04.png) 

    а. В текстовом поле **Имя** введите **BrittaSimon**.

    b. В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение поля **Пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-an-everbridge-test-user"></a>Создание тестового пользователя EverBridge

В этом разделе описано, как создать пользователя Britta Simon в приложении Everbridge. Чтобы добавить пользователей на платформу EverBridge, обратитесь в [службу поддержки Everbridge](mailto:support@everbridge.com).

### <a name="assigning-the-azure-ad-test-user"></a>Назначение тестового пользователя Azure AD

В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к EverBridge.

![Назначение пользователя][200] 

**Чтобы назначить пользователя Britta Simon в EverBridge, выполните следующие действия.**

1. На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений выберите **EverBridge**.

    ![Настройка единого входа](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_app.png) 

3. В меню слева выберите **Пользователи и группы**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.

Щелкнув элемент "Everbridge" на панели доступа, вы автоматически войдете в приложение Everbridge.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по интеграции приложений SaaS с Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_203.png

