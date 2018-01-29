---
title: "Руководство по интеграции Azure Active Directory с Adobe Sign | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложении Adobe Sign."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: f9385723-8fe7-4340-8afb-1508dac3e92b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: f68701cc345ee1bb04cde265ac4e2d6a402da557
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-sign"></a>Руководство по интеграции Azure Active Directory с Adobe Sign

В этом руководстве описано, как интегрировать Adobe Sign с Azure Active Directory (Azure AD).

Интеграция Azure AD с Adobe Sign обеспечивает следующие преимущества:

- С помощью Azure AD вы можете контролировать доступ к Adobe Sign.
- Вы можете включить автоматический вход пользователей в Adobe Sign (единый вход) с использованием учетной записи Azure AD.
- Вы можете управлять учетными записями централизованно — через портал Azure.

Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Технические условия

Чтобы настроить интеграцию Azure AD с Adobe Sign, вам потребуется:

- подписка Azure AD;
- подписка Adobe Sign с поддержкой единого входа.

> [!NOTE]
> Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.

При проверке действий в этом учебнике соблюдайте следующие рекомендации:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Сценарий, описанный в этом учебнике, состоит из двух стандартных блоков.

1. Добавление Adobe Sign из коллекции
2. настройка и проверка единого входа в Azure AD.

## <a name="adding-adobe-sign-from-the-gallery"></a>Добавление Adobe Sign из коллекции
Чтобы настроить интеграцию Adobe Sign с Azure AD, необходимо добавить Adobe Sign из коллекции в список управляемых приложений SaaS.

**Чтобы добавить Adobe Sign из коллекции, сделайте следующее.**

1. На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**. 

    ![Active Directory][1]

2. Перейдите к разделу **Корпоративные приложения**. Затем выберите **Все приложения**.

    ![ПРИЛОЖЕНИЯ][2]
    
3. Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.

    ![ПРИЛОЖЕНИЯ][3]

4. В поле поиска введите **Adobe Sign**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_search.png)

5. На панели результатов выберите **Adobe Sign** и нажмите кнопку **Добавить**, чтобы добавить это приложение.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>настройка и проверка единого входа в Azure AD.
В этом разделе описана настройка и проверка единого входа Azure AD в Adobe Sign с использованием тестового пользователя Britta Simon.

Для работы единого входа в Azure AD необходимо знать, какой пользователь в Adobe Sign соответствует пользователю в Azure AD. Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Adobe Sign.

Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Adobe Sign.

Чтобы настроить и проверить единый вход Azure AD в Adobe Sign, вам потребуется выполнить действия в следующих стандартных блоках.

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа в Azure AD от имени пользователя Britta Simon.
3. **[Создание тестового пользователя Adobe Sign](#creating-an-adobe-sign-test-user)** нужно для того, чтобы в Adobe Sign также существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.
4. **[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD;
5. **[Проверка единого входа](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Adobe Sign.

**Чтобы настроить единый вход Azure AD в Adobe Sign, сделайте следующее.**

1. На портале Azure на странице интеграции с приложением **Adobe Sign** щелкните **Единый вход**.

    ![Настройка единого входа][4]

2. В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_samlbase.png)

3. В разделе **Домены и URL-адреса приложения Adobe Sign** сделайте следующее.

    ![Настройка единого входа](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_url.png)

    a. В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<companyname>.echosign.com/`

    Б. В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<companyname>.echosign.com`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Замените эти значения фактическим URL-адресом для входа и идентификатором. Чтобы получить эти значения, обратитесь к [группе поддержки Adobe Sign](https://helpx.adobe.com/in/contact/support.html). 
 
4. В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.

    ![Настройка единого входа](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_400.png)

6. В разделе **Конфигурация Adobe Sign** щелкните **Настроить Adobe Sign**, чтобы открыть окно **Настройка единого входа**. Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.

    ![Настройка единого входа](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_configure.png) 


7. В другом окне веб-браузера войдите на свой корпоративный веб-сайт Adobe Sign в качестве администратора.

8. В меню в верхней части экрана выберите **Account** (Учетная запись), а затем в области навигации с левой стороны выберите **SAML Settings** (Параметры SAML) в разделе **Account Settings** (Параметры учетной записи).
   
   ![Учетная запись](./media/active-directory-saas-adobe-echosign-tutorial/ic789520.png "Учетная запись")

9. В разделе «Параметры SAML» выполните следующие действия.
   
   ![Параметры SAML](./media/active-directory-saas-adobe-echosign-tutorial/ic789521.png "Параметры SAML")
   
   a. В разделе **SAML Mode** (Режим SAML) выберите параметр **SAML Mandatory** (SAML обязательно).
   
   Б. Установите флажок **Allow EchoSign Account Administrators to log in using their EchoSign Credentials**(Разрешить администраторам учетных записей EchoSign вход с использованием учетных данных EchoSign).
   
   c. В разделе **User Creation** (Создание пользователей) установите флажок **Automatically add users authenticated through SAML** (Автоматически добавлять пользователей, прошедших проверку подлинности с использованием SAML).

10. После этого выполните следующие действия.

       ![Параметры SAML](./media/active-directory-saas-adobe-echosign-tutorial/ic789522.png "Параметры SAML")

    a. Вставьте значение **SAML Entity ID** (Идентификатор сущности SAML), скопированное на портале Azure, в поле **IdP Entity ID** (Идентификатор сущности IdP).
    
    Б. В текстовое поле **IdP Login URL** (URL-адрес входа IdP) вставьте значение **URL-адрес службы единого входа SAML**, скопированное на портале Azure.
   
    c. В текстовое поле **IdP Logout URL** (URL-адрес выхода IdP) вставьте значение **URL-адрес выхода**, скопированное на портале Azure.

    d. Откройте скачанный файл **сертификата (Base64)** в Блокноте, скопируйте его содержимое в буфер обмена, а затем вставьте его в текстовое поле **IdP Certificate** (Сертификат IdP).

    д. Нажмите кнопку **Сохранить изменения**.

> [!TIP]
> Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.  После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы. Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.

![Создание пользователя Azure AD][100]

**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**

1. На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_01.png) 

2. Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_02.png) 

3. Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_03.png) 

4. На странице диалогового окна **Пользователь** выполните следующие действия.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_04.png) 

    a. В текстовом поле **Имя** введите **BrittaSimon**.

    Б. В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение поля **Пароль**.

    d. Нажмите кнопку **Создать**.
 
### <a name="creating-an-adobe-sign-test-user"></a>Создание тестового пользователя Adobe Sign

Чтобы пользователи Azure AD могли выполнять вход в Adobe Sign, они должны быть подготовлены в Adobe Sign. В случае Adobe Sign подготовка выполняется вручную.

>[!NOTE]
>Вы можете использовать любые другие инструменты создания учетной записи пользователя Adobe Sign или API, предоставляемые Adobe Sign для подготовки учетных записей пользователя AAD. 

**Чтобы подготовить учетную запись пользователя, сделайте следующее:**

1. Выполните вход на свой корпоративный веб-сайт **Adobe Sign** в качестве администратора.

2. В меню в верхней части экрана щелкните **Account** (Учетная запись), а затем в области навигации слева выберите **Users & Groups** (Пользователи и группы), а затем — **Create a new user** (Создать пользователя).
   
   ![Учетная запись](./media/active-directory-saas-adobe-echosign-tutorial/ic789524.png "Учетная запись")
   
3. В разделе **Создание нового пользователя** выполните следующие действия.
   
   ![Создание пользователя](./media/active-directory-saas-adobe-echosign-tutorial/ic789525.png "Создание пользователя")
   
   a. Введите в текстовые поля **Email Address** (Адрес электронной почты), **First Name** (Имя) и **Last Name** (Фамилия) соответствующие данные действующей учетной записи AAD, которую нужно подготовить.
   
   Б. Нажмите кнопку **Создать пользователя**.

>[!NOTE]
>Владелец учетной записи Azure Active Directory получит электронное сообщение со ссылкой для подтверждения учетной записи перед ее активацией. 

### <a name="assigning-the-azure-ad-test-user"></a>Назначение тестового пользователя Azure AD

В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Adobe Sign.

![Назначение пользователя][200] 

**Чтобы назначить пользователя Britta Simon в Adobe Sign, выполните указанные ниже действия.**

1. На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.

    ![Назначение пользователя][201] 

2. Из списка приложений выберите **Adobe Sign**.

    ![Настройка единого входа](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_app.png) 

3. В меню слева выберите **Пользователи и группы**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

Щелкнув элемент "Adobe Sign" на панели доступа, вы автоматически войдете в приложение Adobe Sign.
Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по интеграции приложений SaaS с Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_203.png

