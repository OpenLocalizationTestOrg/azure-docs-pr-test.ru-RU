---
title: "Руководство по интеграции Azure Active Directory с PurelyHR | Документы Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в PurelyHR."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 86a9c454-596d-4902-829a-fe126708f739
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: a9075b1759ebd39f164bfe288fb0a365acdcc44c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-purelyhr"></a>Руководство. Интеграция Azure Active Directory с PurelyHR

В этом руководстве описано, как интегрировать PurelyHR с Azure Active Directory (Azure AD).

Интеграция Azure AD с приложением PurelyHR обеспечивает следующие преимущества:

- С помощью Azure AD вы можете контролировать доступ к PurelyHR.
- Вы можете включить автоматический вход пользователей в PurelyHR (единый вход) с применением учетной записи Azure AD.
- Вы можете управлять учетными записями централизованно — через портал Azure.

Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

Чтобы настроить интеграцию Azure AD с PurelyHR, вам потребуется:

- подписка Azure AD;
- подписка PurelyHR с поддержкой единого входа.

> [!NOTE]
> Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.

При проверке действий в этом учебнике соблюдайте следующие рекомендации:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Сценарий, описанный в этом учебнике, состоит из двух основных блоков:

1. Добавление PurelyHR из коллекции
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-purelyhr-from-the-gallery"></a>Добавление PurelyHR из коллекции
Чтобы настроить интеграцию PurelyHR с Azure AD, нужно добавить PurelyHR из коллекции в список управляемых приложений SaaS.

**Чтобы добавить PurelyHR из коллекции, выполните следующие действия:**

1. На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**. 

    ![Active Directory][1]

2. Перейдите к разделу **Корпоративные приложения**. Затем выберите **Все приложения**.

    ![Приложения][2]
    
3. Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.

    ![Приложения][3]

4. В поле поиска введите **PurelyHR**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_search.png)

5. На панели результатов выберите **PurelyHR** и нажмите кнопку **Добавить**, чтобы добавить это приложение.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в PurelyHR с использованием тестового пользователя Britta Simon.

Для работы единого входа в Azure AD нужно знать, какой пользователь в PurelyHR соответствует пользователю в Azure AD. Иными словами, нужно установить связь между пользователем в Azure AD и соответствующим пользователем в PurelyHR.

Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в PurelyHR.

Чтобы настроить и проверить единый вход Azure AD в PurelyHR, вам потребуется выполнить действия в следующих стандартных блоках:

1. **[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.
3. **[Создание тестового пользователя PurelyHR](#creating-a-purelyhr-test-user)** требуется для создания пользователя Britta Simon в PurelyHR, связанного с соответствующим пользователем в Azure AD.
4. **[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.
5. **[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении PurelyHR.

**Чтобы настроить единый вход Azure AD в PurelyHR, выполните следующие действия:**

1. На портале Azure на странице интеграции с приложением **PurelyHR** щелкните **Единый вход**.

    ![Настройка единого входа][4]

2. В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_samlbase.png)

3. Если вы хотите настроить приложение в режиме, инициированном **поставщиком удостоверений**, то в разделе **Домены и URL-адреса приложения PurelyHR** выполните следующие действия:

    ![Настройка единого входа](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_url.png)
   
    В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<companyID>.purelyhr.com/sso-consume`.

4. Установите флажок **Показать дополнительные параметры URL-адресов**, если вы хотите настроить приложение для работы в режиме, инициируемом **поставщиком услуг**.

    ![Настройка единого входа](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_url1.png)
    
    В текстовом поле **URL-адрес для входа** введите значение в следующем формате: `https://<companyID>.purelyhr.com/sso-initiate`.
     
    > [!NOTE]
    > Эти значения приведены в качестве примера. Измените их на фактические значения URL-адреса ответа и URL-адреса входа. Чтобы получить эти значения, обратитесь в [службу поддержки клиентов PurelyHR](http://support.purelyhr.com/). 

5. В разделе **Сертификат для подписи токена SAML** щелкните **Certificate (Base64)** (Сертификат (Base64)), а затем сохраните файл сертификата на компьютере.

    ![Настройка единого входа](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_certificate.png) 

6. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-purelyhr-tutorial/tutorial_general_400.png)
    
7. В разделе **Конфигурация PurelyHR** щелкните **Настроить PurelyHR**, чтобы открыть окно **Настройка единого входа**. Скопируйте **идентификатор сущности SAML и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.

    ![Настройка единого входа](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_configure.png) 

8. Чтобы настроить единый вход на стороне **PurelyHR**, войдите на соответствующий сайт в качестве администратора.

9. Откройте **Панель мониторинга** в параметрах на панели инструментов и щелкните **SSO Settings** (Параметры единого входа).

10. Вставьте в поля нужные значения, как описано ниже.

    ![Настройка единого входа](./media/active-directory-saas-purelyhr-tutorial/purelyhr-dashboard-sso-settings.png)    

    а. Откройте **Сертификат (Base64)**, скачанный на портале Azure, в Блокноте и скопируйте значение сертификата. Вставьте это значение в поле **Сертификат X.509**.

    b. В поле **Idp Issuer URL** (URL-адрес издателя поставщика удостоверений) вставьте **идентификатор сущности SAML**, скопированный на портале Azure.

    c. В поле **Idp Endpoint URL** (URL-адрес конечной точки поставщика удостоверений) вставьте **URL-адрес службы единого входа SAML**, скопированный на портале Azure. 

    d. Установите флажок **Auto-Create Users** (Автоматическое создание пользователей), чтобы включить автоматическую подготовку пользователей в PurelyHR.

    д. Нажмите кнопку **Сохранить изменения**, чтобы сохранить параметры.

> [!TIP]
> Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.  После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы. Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.

![Создание пользователя Azure AD][100]

**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**

1. На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_01.png) 

2. Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_02.png) 

3. Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_03.png) 

4. На странице диалогового окна **Пользователь** выполните следующие действия.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_04.png) 

    а. В текстовом поле **Имя** введите **BrittaSimon**.

    b. В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение поля **Пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-purelyhr-test-user"></a>Создание тестового пользователя PurelyHR

Чтобы пользователи Azure AD могли выполнять вход в PurelyHR, они должны быть подготовлены для PurelyHR. В PurelyHR подготовка пользователей осуществляется автоматически, при этом никакие ручные действия не требуются.

### <a name="assigning-the-azure-ad-test-user"></a>Назначение тестового пользователя Azure AD

В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к PurelyHR.

![Назначение пользователя][200] 

**Чтобы назначить пользователя Britta Simon в PurelyHR, выполните следующие действия:**

1. На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений выберите **PurelyHR**.

    ![Настройка единого входа](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_app.png) 

3. В меню слева выберите **Пользователи и группы**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.

Щелкнув элемент Absorb LMS на панели доступа, вы автоматически входите в приложение Absorb LMS.

Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](https://msdn.microsoft.com/library/dn308586).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по интеграции приложений SaaS с Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_203.png

