---
title: "Руководство по интеграции Azure Active Directory с TalentLMS | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в TalentLMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c903d20d-18e3-42b0-b997-6349c5412dde
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: f28d6fbfad9dae578a20db7218b7e3b174ed859c
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-talentlms"></a>Руководство по интеграции Azure Active Directory с TalentLMS

В этом руководстве описано, как интегрировать приложение TalentLMS с Azure Active Directory (Azure AD).

Интеграция Azure AD с приложением TalentLMS обеспечивает следующие преимущества:

- С помощью Azure AD вы можете контролировать доступ к TalentLMS.
- Вы можете включить автоматический вход пользователей в TalentLMS (единый вход) с учетной записью Azure AD.
- Вы можете управлять учетными записями централизованно — через портал Azure.

Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

Чтобы настроить интеграцию Azure AD с TalentLMS, вам потребуется:

- подписка Azure AD;
- подписка TalentLMS с поддержкой единого входа.

> [!NOTE]
> Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.

При проверке действий в этом учебнике соблюдайте следующие рекомендации:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Сценарий, описанный в этом учебнике, состоит из двух основных блоков:

1. Добавление TalentLMS из коллекции.
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-talentlms-from-the-gallery"></a>Добавление TalentLMS из коллекции
Чтобы настроить интеграцию TalentLMS с Azure AD, необходимо добавить TalentLMS из коллекции в список управляемых приложений SaaS.

**Чтобы добавить TalentLMS из коллекции, выполните следующие действия.**

1. На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**. 

    ![Active Directory][1]

2. Перейдите к разделу **Корпоративные приложения**. Затем выберите **Все приложения**.

    ![Приложения][2]
    
3. Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.

    ![Приложения][3]

4. В поле поиска введите **TalentLMS**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_search.png)

5. На панели результатов выберите **TalentLMS** и нажмите кнопку **Добавить**, чтобы добавить это приложение.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в TalentLMS с использованием тестового пользователя Britta Simon.

Чтобы единый вход работал, Azure AD необходима информация о том, какой пользователь в TalentLMS соответствует пользователю в Azure AD. Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в TalentLMS.

Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в TalentLMS.

Чтобы настроить и проверить единый вход Azure AD в TalentLMS, вам потребуется выполнить действия в следующих стандартных блоках.

1. **[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.
3. **[Создание тестового пользователя TalentLMS](#creating-a-talentlms-test-user)** требуется для того, чтобы в TalentLMS существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.
4. **[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.
5. **[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении TalentLMS.

**Чтобы настроить единый вход Azure AD в TalentLMS, выполните следующие действия.**

1. На портале Azure на странице интеграции с приложением **TalentLMS** щелкните **Единый вход**.

    ![Настройка единого входа][4]

2. В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_samlbase.png)

3. В разделе **Домены и URL-адреса приложения TalentLMS** сделайте следующее.

    ![Настройка единого входа](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_url.png)

    а. В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<tenant-name>.TalentLMSapp.com`

    b. В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `http://<tenant-name>.talentlms.com`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Замените эти значения фактическим URL-адресом для входа и идентификатором. Чтобы получить эти значения, обратитесь к [группе поддержки TalentLMS](https://www.talentlms.com/contact). 
 
4. В разделе **Сертификат подписи SAML** скопируйте значение **Отпечаток** сертификата.

    ![Настройка единого входа](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-talentlms-tutorial/tutorial_general_400.png)

6. В разделе **Конфигурация TalentLMS** щелкните **Настроить TalentLMS**, чтобы открыть окно **Настройка единого входа**. Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.

    ![Настройка единого входа](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_configure.png)  

7. В другом окне веб-браузера войдите на свой корпоративный веб-сайт TalentLMS в качестве администратора.

8. В разделе **Учетная запись и параметры** выберите вкладку **Пользователи**.
   
    ![Учетная запись и параметры](./media/active-directory-saas-talentlms-tutorial/IC777296.png "Учетная запись и параметры")

9. Щелкните **Единый вход**.

10. В разделе "Единый вход" выполните следующие действия:
   
    ![Единый вход](./media/active-directory-saas-talentlms-tutorial/IC777297.png "Единый вход")   

    а. Из списка **Тип интеграции единого входа** выберите **SAML 2.0**.

    b. В текстовое поле **Identity Provider (IDP)** (Поставщик удостоверений (IdP)) вставьте значение **SAML Entity ID** (Идентификатор сущности SAML), скопированное на портале Azure.
 
    c. Вставьте значение **Отпечаток** с портала Azure в текстовое поле **Certificate Fingerprint** (Отпечаток сертификата).    

    г)  В текстовое поле **Remote sign-in URL** (URL-адрес удаленного входа) вставьте значение **SAML Single Sign-On Service URL** (URL-адрес службы единого входа SAML), скопированное на портале Azure.
 
    д. В текстовое поле **Remote sign-out URL** (URL-адрес удаленного выхода) вставьте значение **URL-адрес выхода**, скопированное на портале Azure.

    f. Укажите следующие сведения. 

    * В текстовое поле **TargetedID** (Целевой идентификатор) введите `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.
     
    * В текстовое поле **First Name** (Имя) введите `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.
    
    * В текстовое поле **Last Name** (Фамилия) введите `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.
    
    * В текстовое поле **Email** (Электронная почта) введите `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.
    
11. Щелкните **Сохранить**.
 
> [!TIP]
> Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.  После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы. Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.

![Создание пользователя Azure AD][100]

**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**

1. На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_01.png) 

2. Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_02.png) 

3. Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_03.png) 

4. На странице диалогового окна **Пользователь** выполните следующие действия.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_04.png) 

    а. В текстовом поле **Имя** введите **BrittaSimon**.

    b. В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение поля **Пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-talentlms-test-user"></a>Создание тестового пользователя TalentLMS

Чтобы пользователи Azure AD могли выполнить вход в TalentLMS, они должны быть подготовлены в TalentLMS. В случае использования TalentLMS подготовка выполняется вручную.

**Чтобы подготовить учетную запись пользователя, сделайте следующее:**

1. Войдите в клиент **TalentLMS** .

2. Щелкните **Пользователи**, а затем — **Добавить пользователя**.

3. На странице диалогового окна **Добавление пользователя** сделайте следующее:
   
    ![Добавление пользователя](./media/active-directory-saas-talentlms-tutorial/IC777299.png "Добавление пользователя")  

    а. В текстовое поле **First name** (Имя) введите имя пользователя, например **Britta**.

    b. В текстовое поле **Last name** (Фамилия) введите фамилию пользователя, например **Simon**.
 
    c. В текстовое поле **Email address** (Адрес электронной почты) введите адрес электронной почты пользователя, например **brittasimon@contoso.com**.

    г) Нажмите кнопку **Add User**(Добавить пользователя).

>[!NOTE]
>Вы можете использовать любые другие средства создания учетной записи пользователя TalentLMS или API-интерфейсы, предоставляемые TalentLMS для подготовки учетных записей пользователя AAD.
 

### <a name="assigning-the-azure-ad-test-user"></a>Назначение тестового пользователя Azure AD

В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к TalentLMS.

![Назначение пользователя][200] 

**Чтобы назначить пользователя Britta Simon в TalentLMS, выполните следующие действия.**

1. На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.

    ![Назначение пользователя][201] 

2. Из списка приложений выберите **TalentLMS**.

    ![Настройка единого входа](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_app.png) 

3. В меню слева выберите **Пользователи и группы**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.

Щелкнув элемент "TalentLMS" на панели доступа, вы автоматически войдете в приложение TalentLMS.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по интеграции приложений SaaS с Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_203.png

