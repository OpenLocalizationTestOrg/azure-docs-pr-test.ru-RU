---
title: "Руководство по интеграции Azure Active Directory с Cerner Central | Документы Майкрософт"
description: "Сведения о настройке единого входа между Azure Active Directory и Cerner Central."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: d2bc549d-d286-4679-854e-bb67c62b0475
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 391994b8df73657dc75e8c9790356f443341159d
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cerner-central"></a>Руководство. Интеграция Azure Active Directory с Cerner Central

В этом руководстве описано, как интегрировать Cerner Central с Azure Active Directory (Azure AD).

Интеграция Azure AD с приложением Cerner Central обеспечивает следующие преимущества:

- С помощью Azure AD вы можете контролировать доступ к Cerner Central.
- Вы можете включить автоматический вход пользователей в Cerner Central (единый вход) с учетной записью Azure AD.
- Вы можете управлять учетными записями централизованно — через портал Azure.

Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Технические условия

Чтобы настроить интеграцию Azure AD с Cerner Central, вам потребуется:

- подписка Azure AD;
- утвержденная системная учетная запись Cerner Central.

> [!NOTE]
> Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.

При проверке действий в этом учебнике соблюдайте следующие рекомендации:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Сценарий, описанный в этом учебнике, состоит из двух стандартных блоков.

1. Добавление Cerner Central из коллекции
2. настройка и проверка единого входа в Azure AD.

## <a name="adding-cerner-central-from-the-gallery"></a>Добавление Cerner Central из коллекции
Чтобы настроить интеграцию Cerner Central с Azure AD, необходимо добавить Cerner Central из коллекции в список управляемых приложений SaaS.

**Чтобы добавить Cerner Central из коллекции, сделайте следующее.**

1. На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**. 

    ![Active Directory][1]

2. Перейдите к разделу **Корпоративные приложения**. Затем выберите **Все приложения**.

    ![ПРИЛОЖЕНИЯ][2]
    
3. Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Новое приложение**.

    ![ПРИЛОЖЕНИЯ][3]

4. В поле поиска введите **Cerner Central**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_search.png)

5. На панели результатов выберите **Cerner Central** и нажмите кнопку **Добавить**, чтобы добавить приложение.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>настройка и проверка единого входа в Azure AD.
В этом разделе описаны настройка и проверка единого входа Azure AD в Cerner Central с использованием тестового пользователя Britta Simon.

Для работы единого входа Azure AD необходимо знать, какой пользователь в Cerner Central соответствует пользователю в Azure AD. Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Cerner Central.

Чтобы настроить и проверить единый вход Azure AD в Cerner Central, вам потребуется выполнить действия в следующих стандартных блоках.

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа в Azure AD от имени пользователя Britta Simon.
3. **[Создание тестового пользователя Cerner Central](#creating-a-cerner-central-test-user)** требуется для создания пользователя Britta Simon в Cerner Central, связанного с соответствующим представлением в Azure AD.
4. **[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD;
5. **[Проверка единого входа](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Cerner Central.

**Чтобы настроить единый вход Azure AD в Cerner Central, сделайте следующее.**

1. На портале Azure на странице интеграции с приложением **Cerner Central** щелкните **Единый вход**.

    ![Настройка единого входа][4]

2. В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_samlbase.png)

3. В разделе **Домены и URL-адреса приложения Cerner Central** сделайте следующее.

    ![Настройка единого входа](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_url.png)

    a. В текстовое поле **Идентификатор** введите значение в приведенном ниже формате.
    
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    

    Б. В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: 
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/sso` |
    | `https://<instancename>.sandboxcernercentral.com/session-api/protocol/saml2/sso` |
    

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Измените их на фактические значения идентификатора и URL-адреса ответа. Чтобы получить эти значения, обратитесь в [службу поддержки Cerner Central](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations).
 
4. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-cernercentral-tutorial/tutorial_general_400.png)

5. Для создания URL-адреса **метаданных** выполните следующие действия.

    a. Щелкните **Регистрация приложений**.
    
    ![Настройка единого входа](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appregistrations.png)
   
    Б. Щелкните **Конечные точки**, чтобы открыть диалоговое окно **Конечные точки**.  
    
    ![Настройка единого входа](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpointicon.png)

    c. Нажмите кнопку "Копировать", чтобы скопировать URL-адрес **документа метаданных федерации**, а затем вставьте его в блокнот.
    
    ![Настройка единого входа](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpoint.png)
     
    d. Теперь перейдите к странице свойств **Cerner Central** и скопируйте **идентификатор приложения** с помощью кнопки **Копировать**, а затем вставьте его в блокнот.
 
    ![Настройка единого входа](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appid.png)

    д. Создайте **URL-адрес метаданных** по следующему шаблону: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`.

6. Для настройки единого входа на стороне **Cerner Central** необходимо отправить **URL-адрес метаданных** в [службу поддержки Cerner Central](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations). Специалисты службы поддержки настроят единый вход на стороне приложения для завершения интеграции.

> [!TIP]
> Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.  После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы. Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon. 

![Создание пользователя Azure AD][100]

**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**

1. На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_01.png) 

2. Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_02.png) 

3. Щелкните **Добавить**, чтобы открыть диалоговое окно **Пользователь**.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_03.png) 

4. На странице диалогового окна **Пользователь** выполните следующие действия.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_04.png) 

    a. В текстовом поле **Имя** введите **BrittaSimon**.

    Б. В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи Britta Simon.

    c. Выберите **Показать пароль** и запишите значение поля **Пароль**.

    d. Нажмите кнопку **Создать**.
 
### <a name="creating-a-cerner-central-test-user"></a>Создание тестового пользователя Cerner Central

Приложение **Cerner Central** разрешает аутентификацию посредством любого поставщика федеративных удостоверений. Если пользователь может войти на домашнюю страницу приложения, то он является федеративным и не требует подготовки вручную.

### <a name="assigning-the-azure-ad-test-user"></a>Назначение тестового пользователя Azure AD

В этом разделе описано, как позволить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Cerner Central.

![Назначение пользователя][200] 

**Чтобы назначить пользователя Britta Simon в Cerner Central, сделайте следующее.**

1. На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений выберите **Cerner Central**.

    ![Настройка единого входа](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_app.png) 

3. В меню слева выберите **Пользователи и группы**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.

Щелкнув элемент Cerner Central на панели доступа, вы автоматически войдете в приложение Cerner Central. Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по интеграции приложений SaaS с Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_203.png

