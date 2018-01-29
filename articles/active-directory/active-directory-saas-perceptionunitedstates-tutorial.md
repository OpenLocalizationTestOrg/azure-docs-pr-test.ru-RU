---
title: "Руководство по интеграции Azure Active Directory с Perception United States (Non-UltiPro) | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Perception United States (Non-UltiPro)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: b4a8f026-cb5f-41eb-9680-68eddc33565e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: d94d233a12e51bf851a791fda481b91c513d64b7
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-perception-united-states-non-ultipro"></a>Руководство по интеграции Azure Active Directory с Perception United States (Non-UltiPro)

В этом руководстве вы узнаете, как интегрировать Perception United States (Non-UltiPro) с Azure Active Directory (Azure AD).

Интеграция Perception United States (Non-UltiPro) с Azure AD обеспечивает следующие преимущества:

- С помощью Azure AD вы можете контролировать доступ к Perception United States (Non-UltiPro).
- Вы можете включить автоматический вход пользователей в Perception United States (Non-UltiPro) (единый вход) с использованием их учетных записей Azure AD.
- Вы можете управлять учетными записями централизованно — на портале Azure.

Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Технические условия

Чтобы настроить интеграцию Azure AD с United States (Non-UltiPro) необходимо следующее:

- подписка Azure AD;
- подписка Perception United States (Non-UltiPro) с поддержкой единого входа.

> [!NOTE]
> Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.

При проверке действий в этом учебнике соблюдайте следующие рекомендации:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Сценарий, описанный в этом учебнике, состоит из двух стандартных блоков.

1. Добавление Perception United States (Non-UltiPro) из коллекции.
2. настройка и проверка единого входа в Azure AD.

## <a name="adding-perception-united-states-non-ultipro-from-the-gallery"></a>Добавление Perception United States (Non-UltiPro) из коллекции
Чтобы настроить интеграцию Perception United States (Non-UltiPro) с Azure AD, необходимо добавить Perception United States (Non-UltiPro) из коллекции в список управляемых приложений SaaS.

**Чтобы добавить Perception United States (Non-UltiPro) из коллекции, выполните следующие действия:**

1. На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**. 

    ![Кнопка "Azure Active Directory"][1]

2. Перейдите к разделу **Корпоративные приложения**. Затем выберите **Все приложения**.

    ![Колонка "Корпоративные приложения"][2]
    
3. Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.

    ![Кнопка "Новое приложение"][3]

4. В поле поиска введите **Perception United States (Non-UltiPro)**, выберите **Perception United States (Non-UltiPro)** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.

    ![Perception United States (Non-UltiPro) в списке результатов](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD

В этом разделе описана настройка и проверка единого входа Azure AD в Perception United States (Non-UltiPro) с использованием тестового пользователя Britta Simon.

Для работы единого входа в Azure AD необходимо знать, какой пользователь в Perception United States (Non-UltiPro) соответствует пользователю в Azure AD. Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Perception United States (Non-UltiPro).

Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Perception United States (Non-UltiPro).

Чтобы настроить и проверить единый вход Azure AD в Perception United States (Non-UltiPro), вам потребуется выполнить действия в следующих стандартных блоках:

1. **[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.
2. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.
3. **[Создание тестового пользователя Perception United States (Non-UltiPro)](#create-a-perception-united-states-non-ultipro-test-user)** требуется для создания пользователя Britta Simon в Perception United States (Non-UltiPro), связанного с соответствующим представлением пользователя в Azure AD.
4. **[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.
5. **[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Perception United States (Non-UltiPro).

**Чтобы настроить единый вход Azure AD в Perception United States (Non-UltiPro), выполните следующие действия:**

1. На портале Azure на странице интеграции с приложением **Perception United States (Non-UltiPro)** щелкните **Единый вход**.

    ![Ссылка "Настройка единого входа"][4]

2. В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_samlbase.png)

3. В разделе **Домены и URL-адреса приложения Perception United States (Non-UltiPro)** выполните следующие действия:

    ![Сведения о домене и URL-адресах единого входа для приложения Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_url.png)

    a. В текстовом поле **Идентификатор** введите URL-адрес `https://perception.kanjoya.com/sp`.

    Б. В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://perception.kanjoya.com/sso?idp=<entity_id>`.

    > [!NOTE] 
    > Это значение приведено для примера. Вы замените это значение на фактический URL-адрес ответа, который описывается далее в этом учебнике.
 
4. В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_400.png)

6. В разделе **Настройка Perception United States (Non-UltiPro)** щелкните **Настроить Perception United States (Non-UltiPro)**, чтобы открыть окно **Настройка единого входа**. Скопируйте значение **SAML Entity ID** (Идентификатор сущности SAML) из раздела **Краткий справочник**.

    a. Приложению **Perception United States (Non-UltiPro)** необходимо значение **идентификатора сущности SAML**, которое вы скопировали, чтобы закодировать в формате URI. Для получения значения, закодированного в формате URI, перейдите по следующей ссылке: **http://www.url-encode-decode.com/**.

    Б. Получив это значение, объедините его с **URL-адресом ответа**, как показано ниже:

    `https://perception.kanjoya.com/sso?idp=<URI encooded entity_id>`
    
    c. Вставьте значение выше в текстовое поле **URL-адрес ответа** в разделе **Домены и URL-адреса приложения Perception United States (Non-UltiPro)**.

    ![Настройка Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_configure.png) 

7. В другом окне браузера войдите на корпоративный веб-сайт Perception United States (Non-UltiPro) с правами администратора.

8. На главной панели инструментов щелкните **Account Settings** (Параметры учетной записи).

    ![Пользователь Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_user.png)

9. На странице **Account Settings** (Параметры учетной записи) выполните следующие действия:

    ![Пользователь Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_account.png)

    a. В текстовом поле **Company Name** (Название компании) введите название **компании**.
    
    Б. В текстовом поле **Account Name** (Имя учетной записи) введите имя **учетной записи**.

    c. В текстовом поле **Default Reply-To Email** (Электронная почта ответа по умолчанию) введите допустимый адрес **электронной почты**.

    d. Выберите для параметра **SSO Identity Provider** (Поставщик удостоверений единого входа) значение **SAML 2.0**.

10. На странице **настройки единого входа** сделайте следующее:

    ![Настройка единого входа Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_ssoconfig.png)

    a. Выберите для параметра **SAML NameID Type** (Тип NameID SAML) значение **EMAIL** (Электронная почта).

    Б. В текстовом поле **SSO Configuration Name** (Имя конфигурации единого входа) введите имя своей **конфигурации**.
    
    c. В текстовое поле **Identity Provider Name** (Имя поставщика удостоверений) вставьте значение **идентификатора сущности SAML**, скопированное на портале Azure. 

    d. В **текстовое поле домена SAML** введите домен, например **@contoso.com**.

    д. Нажмите кнопку **Upload Again** (Отправить еще раз), чтобы передать **XML-файл метаданных**.

    f. Нажмите кнопку **Обновить**.


> [!TIP]
> Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.  После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы. Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD

Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.

   ![Создание тестового пользователя Azure AD][100]

**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**

1. На портале Azure в области слева нажмите кнопку **Azure Active Directory**.

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_01.png)

2. Чтобы открыть список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.

    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_02.png)

3. Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна **Все пользователи** щелкните **Добавить**.

    ![Кнопка "Добавить"](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_03.png)

4. В диалоговом окне **Пользователь** сделайте следующее.

    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_04.png)

    a. В поле **Имя** введите **BrittaSimon**.

    Б. В поле **Имя пользователя** введите адрес электронной почты для пользователя Britta Simon.

    c. Установите флажок **Показать пароль** и запишите значение, которое отображается в поле **Пароль**.

    d. Нажмите кнопку **Создать**.
  
### <a name="create-a-perception-united-states-non-ultipro-test-user"></a>Создание тестового пользователя Perception United States (Non-UltiPro)

В этом разделе описано, как создать пользователя Britta Simon в приложении Perception United States (Non-UltiPro). Обратитесь в [службу поддержки Perception United States (Non-UltiPro)](http://www.ultimatesoftware.com/Contact/ContactUs), чтобы добавить пользователей на платформу Perception United States (Non-UltiPro).

### <a name="assign-the-azure-ad-test-user"></a>Назначение тестового пользователя Azure AD

В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив ему доступ к Perception United States (Non-UltiPro).

![Назначение роли пользователя][200] 

**Чтобы назначить пользователя Britta Simon в приложении Perception United States (Non-UltiPro), выполните следующие действия:**

1. На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений выберите **Perception United States (Non-UltiPro)**.

    ![Ссылка на Perception United States (Non-UltiPro) в списке "Приложения"](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_app.png)  

3. В меню слева выберите **Пользователи и группы**.

    ![Ссылка "Пользователи и группы"][202]

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Область "Добавление назначения"][203]

5. В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.

Щелкнув плитку Perception United States (Non-UltiPro) на панели доступа, вы автоматически войдете в приложение Perception United States (Non-UltiPro).
Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по интеграции приложений SaaS с Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_203.png

