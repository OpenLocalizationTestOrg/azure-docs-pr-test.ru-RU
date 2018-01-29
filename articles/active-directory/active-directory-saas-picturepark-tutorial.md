---
title: "Руководство по интеграции Azure Active Directory с Picturepark | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложении Picturepark."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 31c21cd4-9c00-4cad-9538-a13996dc872f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: jeedes
ms.openlocfilehash: 4d9fd7127a36e9a699a352dbe6899edd5ea99e92
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-picturepark"></a>Руководство по интеграции Azure Active Directory с Picturepark

В этом руководстве описано, как интегрировать Picturepark с Azure Active Directory (Azure AD).

Интеграция Azure AD с приложением Picturepark обеспечивает следующие преимущества:

- С помощью Azure AD вы можете контролировать доступ к Picturepark.
- Вы можете включить автоматический вход пользователей в Picturepark (единый вход) с использованием учетной записи Azure AD.
- Вы можете управлять учетными записями централизованно — через портал Azure.

Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Технические условия

Чтобы настроить интеграцию Azure AD с Picturepark, вам потребуется:

- подписка Azure AD;
- подписка Picturepark с поддержкой единого входа.

> [!NOTE]
> Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.

При проверке действий в этом учебнике соблюдайте следующие рекомендации:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Сценарий, описанный в этом учебнике, состоит из двух стандартных блоков.

1. Добавление Picturepark из коллекции.
2. настройка и проверка единого входа в Azure AD.

## <a name="adding-picturepark-from-the-gallery"></a>Добавление Picturepark из коллекции
Чтобы настроить интеграцию Picturepark с Azure AD, необходимо добавить Picturepark из коллекции в список управляемых приложений SaaS.

**Чтобы добавить Picturepark из коллекции, выполните следующие действия.**

1. На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**. 

    ![Active Directory][1]

2. Перейдите к разделу **Корпоративные приложения**. Затем выберите **Все приложения**.

    ![ПРИЛОЖЕНИЯ][2]
    
3. Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.

    ![ПРИЛОЖЕНИЯ][3]

4. В поле поиска введите **Picturepark**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_search.png)

5. На панели результатов выберите **Picturepark** и нажмите кнопку **Добавить**, чтобы добавить это приложение.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>настройка и проверка единого входа в Azure AD.
В этом разделе описана настройка и проверка единого входа Azure AD в Picturepark с использованием тестового пользователя Britta Simon.

Чтобы единый вход работал, Azure AD необходима информация о том, какой пользователь в Picturepark соответствует пользователю в Azure AD. Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Picturepark.

Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Picturepark.

Чтобы настроить и проверить единый вход Azure AD в Picturepark, вам потребуется выполнить действия в следующих стандартных блоках.

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа в Azure AD от имени пользователя Britta Simon.
3. **[Создание тестового пользователя Picturepark](#creating-a-picturepark-test-user)** требуется для того, чтобы в Picturepark существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.
4. **[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD;
5. **[Проверка единого входа](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Picturepark.

**Чтобы настроить единый вход Azure AD в Picturepark, выполните следующее.**

1. На портале Azure на странице интеграции с приложением **Picturepark** щелкните **Единый вход**.

    ![Настройка единого входа][4]

2. В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_samlbase.png)

3. В разделе **Домены и URL-адреса приложения Picturepark** выполните следующие действия.

    ![Настройка единого входа](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_url.png)

    a. В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<companyname>.picturepark.com`

    Б. В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: 
    
    |  |
    |--|
    | `https://<companyname>.current-picturepark.com`|
    | `https://<companyname>.picturepark.com`|
    | `https://<companyname>.next-picturepark.com`|
    | |

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Замените эти значения фактическим URL-адресом для входа и идентификатором. Чтобы получить эти значения, обратитесь к [группе поддержки клиентов Picturepark](https://picturepark.com/about/contact/). 
 
4. В разделе **Сертификат подписи SAML** скопируйте значение **Отпечаток**.

    ![Настройка единого входа](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-picturepark-tutorial/tutorial_general_400.png)

6. В разделе **Конфигурация Picturepark** щелкните **Настроить Picturepark**, чтобы открыть окно **Настройка единого входа**. Скопируйте **URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.

    ![Настройка единого входа](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_configure.png) 

7. В другом окне веб-браузера войдите на сайт Picturepark своей компании в качестве администратора.

8. Щелкните **Administrative tools** (Администрирование) на панели инструментов в верхней части страницы и выберите **Management Console** (Консоль управления).
   
    ![Консоль управления](./media/active-directory-saas-picturepark-tutorial/ic795062.png "Консоль управления")

9. Щелкните **Authentication** (Аутентификация), а затем выберите **Identity providers** (Поставщики удостоверений).
   
    ![Аутентификация](./media/active-directory-saas-picturepark-tutorial/ic795063.png "Аутентификация")

10. В разделе **Конфигурация поставщика удостоверений** сделайте следующее:
   
    ![Конфигурация поставщика удостоверений](./media/active-directory-saas-picturepark-tutorial/ic795064.png "Конфигурация поставщика удостоверений")
   
    a. Щелкните **Добавить**.
  
    Б. Введите имя конфигурации.
   
    c. Выберите **По умолчанию**.
   
    d. В текстовое поле **Issuer URI** (URI издателя) вставьте значение **SAML Single Sign-On Service URL** (URL-адрес службы единого входа SAML), скопированное на портале Azure.
   
    д. В текстовое поле **Trusted Issuer Thumb Print** (Отпечаток доверенного издателя) вставьте значение **Отпечаток**, скопированное в разделе **Сертификат подписи SAML**. 

11. Щелкните **JoinDefaultUsersGroup**.

12. Чтобы задать атрибут **Emailaddress** в текстовом поле **Claim** (Утверждение), введите `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` и нажмите кнопку **Save** (Сохранить).

      ![Конфигурация](./media/active-directory-saas-picturepark-tutorial/ic795065.png "Конфигурация")

> [!TIP]
> Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.  После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы. Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.

![Создание пользователя Azure AD][100]

**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**

1. На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_01.png) 

2. Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_02.png) 

3. Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_03.png) 

4. На странице диалогового окна **Пользователь** выполните следующие действия.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_04.png) 

    a. В текстовом поле **Имя** введите **BrittaSimon**.

    Б. В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение поля **Пароль**.

    d. Нажмите кнопку **Создать**.
 
### <a name="creating-a-picturepark-test-user"></a>Создание тестового пользователя Picturepark

Чтобы пользователи Azure AD могли выполнять вход в Picturepark, они должны быть подготовлены для Picturepark. В случае с Picturepark подготовка выполняется вручную.

**Чтобы подготовить учетную запись пользователя, сделайте следующее:**

1. Выполните вход в клиент **Picturepark** .

2. Щелкните **Administrative tools** (Администрирование) на панели инструментов в верхней части страницы и выберите **Users** (Пользователи).
   
    ![Пользователи](./media/active-directory-saas-picturepark-tutorial/ic795067.png "Пользователи")

3. На вкладке **Users overview** (Обзор пользователей) щелкните **New** (Создать).
   
    ![Управление пользователями](./media/active-directory-saas-picturepark-tutorial/ic795068.png "Управление пользователями")

4. В диалоговом окне **Create User** (Создание пользователя) введите приведенные ниже данные действительной учетной записи Azure AD, которую необходимо подготовить.
   
    ![Создание пользователя](./media/active-directory-saas-picturepark-tutorial/ic795069.png "Создание пользователя")
   
    a. В текстовое поле **Email Address** (Адрес электронной почты) введите **адрес электронной почты** пользователя, например **BrittaSimon@contoso.com**.  
   
    Б. В текстовые поля **Password** (Пароль) и **Confirm Password** (Подтверждение пароля) введите **пароль** пользователя BrittaSimon. 
   
    c. В текстовое поле **First Name** (Имя) введите **имя пользователя**, **Britta**. 
   
    d. В текстовое поле **Last Name** (Фамилия) введите **фамилию** пользователя, **Simon**.
   
    д. В текстовое поле **Company** (Компания) введите **название компании** пользователя. 
   
    f. В текстовом поле **Country** (Страна) выберите **страну** пользователя.
  
    ж. В текстовое поле **ZIP** (Почтовый индекс) введите **почтовый индекс** города.
   
    h. В текстовое поле **City** (Город) введите **название города** пользователя.

    i. В поле **Язык**укажите язык.
   
    j. Нажмите кнопку **Создать**.

>[!NOTE]
>Вы можете использовать любые другие инструменты создания учетных записей пользователя Picturepark или API, предоставляемые Picturepark для подготовки учетных записей пользователя Azure Active Directory.
> 

### <a name="assigning-the-azure-ad-test-user"></a>Назначение тестового пользователя Azure AD

В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Picturepark.

![Назначение пользователя][200] 

**Чтобы назначить пользователя Britta Simon в Picturepark, выполните следующие действия.**

1. На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.

    ![Назначение пользователя][201] 

2. Из списка приложений выберите **Picturepark**.

    ![Настройка единого входа](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_app.png) 

3. В меню слева выберите **Пользователи и группы**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.

Щелкнув элемент "Picturepark" на панели доступа, вы автоматически войдете в приложение Picturepark. Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по интеграции приложений SaaS с Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_203.png

