---
title: "Руководство по интеграции Azure Active Directory с SumoLogic | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в SumoLogic."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fbb76765-92d7-4801-9833-573b11b4d910
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: e739106472ccf930b2942eb810dd844f2b1ade7c
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sumologic"></a>Руководство. Интеграция Azure Active Directory с SumoLogic

В этом руководстве описано, как интегрировать SumoLogic с Azure Active Directory (Azure AD).

Интеграция Azure AD с приложением SumoLogic обеспечивает следующие преимущества.

- С помощью Azure AD вы можете контролировать доступ к SumoLogic.
- Вы можете включить автоматический вход пользователей в SumoLogic (единый вход) с учетной записью Azure AD.
- Вы можете управлять учетными записями централизованно — через портал Azure.

Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

Чтобы настроить интеграцию Azure AD с приложением SumoLogic, вам потребуется:

- подписка Azure AD;
- подписка с поддержкой единого входа SumoLogic.

> [!NOTE]
> Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.

При проверке действий в этом учебнике соблюдайте следующие рекомендации:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Сценарий, описанный в этом учебнике, состоит из двух основных блоков:

1. Добавление SumoLogic из коллекции
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-sumologic-from-the-gallery"></a>Добавление SumoLogic из коллекции
Чтобы настроить интеграцию SumoLogic с Azure AD, необходимо добавить SumoLogic из коллекции в список управляемых приложений SaaS.

**Чтобы добавить SumoLogic из коллекции, сделайте следующее:**

1. На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**. 

    ![Active Directory][1]

2. Перейдите к разделу **Корпоративные приложения**. Затем выберите **Все приложения**.

    ![Приложения][2]
    
3. Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.

    ![Приложения][3]

4. В поле поиска введите **SumoLogic**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_search.png)

5. На панели результатов выберите **SumoLogic** и нажмите кнопку **Добавить**, чтобы добавить приложение.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в SumoLogic с использованием тестового пользователя Britta Simon.

Для работы единого входа в Azure AD необходимо знать, какой пользователь в SumoLogic соответствует пользователю в Azure AD. Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в SumoLogic.

Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в SumoLogic.

Чтобы настроить и проверить единый вход Azure AD в SumoLogic, выполните действия в следующих стандартных блоках:

1. **[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.
3. **[Создание тестового пользователя SumoLogic](#creating-a-sumologic-test-user)** требуется для того, чтобы в SumoLogic существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.
4. **[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.
5. **[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе мы включим на портале Azure единый вход Azure AD и настроим его в приложении SumoLogic.

**Чтобы настроить единый вход Azure AD в SumoLogic, сделайте следующее:**

1. На портале Azure на странице интеграции с приложением **SumoLogic** щелкните **Единый вход**.

    ![Настройка единого входа][4]

2. В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_samlbase.png)

3. В разделе **Домены и URL-адреса приложения SumoLogic** сделайте следующее:

    ![Настройка единого входа](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_url.png)

    а. В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<tenantname>.SumoLogic.com`

    b. В текстовом поле **Идентификатор** введите URL-адрес в следующем формате:
    | |
    |--|
    | `https://<tenantname>.us2.sumologic.com` |
    | `https://<tenantname>.sumologic.com` |
    | `https://<tenantname>.us4.sumologic.com` |
    | `https://<tenantname>.eu.sumologic.com` |
    | `https://<tenantname>.au.sumologic.com` |

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Замените эти значения фактическим URL-адресом для входа и идентификатором. Чтобы получить эти значения, обратитесь в [службу поддержки клиентов SumoLogic](https://www.sumologic.com/contact-us/). 
 
4. В разделе **Сертификат для подписи токена SAML** щелкните **Certificate (Base64)** (Сертификат (Base64)), а затем сохраните файл сертификата на компьютере.

    ![Настройка единого входа](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-sumologic-tutorial/tutorial_general_400.png)

6. В разделе **Конфигурация SumoLogic** щелкните **Настроить SumoLogic**, чтобы открыть окно **Настройка единого входа**. Скопируйте **идентификатор сущности SAML и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.

    ![Настройка единого входа](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_configure.png) 

7. В другом окне веб-браузера войдите на корпоративный веб-сайт SumoLogic в качестве администратора.

8. Выберите **Manage (Управление) \> Security (Безопасность)**.
   
    ![Управление](./media/active-directory-saas-sumologic-tutorial/ic778556.png "Управление")

9. Нажмите кнопку **SAML**.
   
    ![Глобальные параметры безопасности](./media/active-directory-saas-sumologic-tutorial/ic778557.png "Глобальные параметры безопасности")

10. В списке **Select a configuration or create a new one** (Выберите настройку или создайте новую) выберите **Azure AD**, а затем щелкните **Configure** (Настройка).
   
    ![Настройка SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778558.png "Настройка SAML 2.0")

11. В диалоговом окне **Настройка SAML 2.0** сделайте следующее:
   
    ![Настройка SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778559.png "Настройка SAML 2.0")
   
    а. В текстовом поле **Configuration Name** (Имя конфигурации) введите **Azure AD**. 

    b. Выберите **Режим отладки**.

    c. В текстовое поле **Issuer** (Издатель) вставьте значение **идентификатора сущности SAML**, скопированное на портале Azure. 

    d. В текстовое поле **Authn Request URL** (URL-адрес запроса аутентификации) вставьте значение **URL-адрес службы единого входа SAML**, скопированное на портале Azure.

    д. Откройте сертификат в кодировке Base-64 в Блокноте, скопируйте его содержимое в буфер обмена и вставьте весь сертификат в текстовое поле **Сертификат X.509** .

    f. В поле **Email Attribute** (Атрибут электронной почты) задайте значение **Use SAML subject** (Использовать субъект SAML).  

    g. Выберите пункт **Конфигурация входа, инициируемая поставщиком услуг**.

    h. В текстовом поле **Login Path** (Путь входа) введите **Azure** и нажмите кнопку **Save** (Сохранить).

> [!TIP]
> Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.  После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы. Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.

![Создание пользователя Azure AD][100]

**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**

1. На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_01.png) 

2. Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_02.png) 

3. Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_03.png) 

4. На странице диалогового окна **Пользователь** выполните следующие действия.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_04.png) 

    а. В текстовом поле **Имя** введите **BrittaSimon**.

    b. В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение поля **Пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-sumologic-test-user"></a>Создание тестового пользователя SumoLogic

Чтобы пользователи Azure AD могли входить в SumoLogic, их необходимо подготовить для SumoLogic.  

* В случае SumoLogic подготовка пользователей осуществляется вручную.

**Чтобы подготовить учетную запись пользователя, сделайте следующее:**

1. Войдите в клиент **SumoLogic** .

2. Выберите **Manage \> Users** (Управление > Пользователи).
   
    ![Пользователи](./media/active-directory-saas-sumologic-tutorial/ic778561.png "Пользователи")

3. Щелкните **Добавить**.
   
    ![Пользователи](./media/active-directory-saas-sumologic-tutorial/ic778562.png "Пользователи")

4. В диалоговом окне **Новый пользователь** сделайте следующее:
   
    ![Новый пользователь](./media/active-directory-saas-sumologic-tutorial/ic778563.png "Новый пользователь") 
 
    а. Введите сведения об учетной записи Azure AD, которую необходимо подготовить, в текстовые поля **First Name** (Имя), **Last Name** (Фамилия) и **Email** (Адрес электронной почты).
  
    b. Выберите роль.
  
    c. Для параметра **Status** (Состояние) выберите значение **Active** (Активно).
  
    d. Щелкните **Сохранить**.

>[!NOTE]
>Вы можете использовать любые другие средства создания учетной записи пользователя SumoLogic или API-интерфейсы, предоставляемые SumoLogic для подготовки учетных записей пользователя AAD. 
> 

### <a name="assigning-the-azure-ad-test-user"></a>Назначение тестового пользователя Azure AD

В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив доступ к SumoLogic.

![Назначение пользователя][200] 

**Чтобы назначить пользователя Britta Simon приложению SumoLogic, сделайте следующее:**

1. На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений выберите **SumoLogic**.

    ![Настройка единого входа](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_app.png) 

3. В меню слева выберите **Пользователи и группы**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.

Щелкнув плитку SumoLogic на панели доступа, вы автоматически войдете в приложение SumoLogic.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по интеграции приложений SaaS с Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_203.png

