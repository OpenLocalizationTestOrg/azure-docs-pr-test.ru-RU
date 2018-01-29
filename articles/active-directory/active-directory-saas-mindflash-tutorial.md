---
title: "Учебник. Интеграция Azure Active Directory с Mindflash | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложении Mindflash."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: bdf91993-aaaa-4598-89b7-77ef8ca065d5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: e7502e46f8aaa849155d5c330d6ff6089b2a7276
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mindflash"></a>Руководство. Интеграция Azure Active Directory с Mindflash

В этом руководстве описано, как интегрировать Mindflash с Azure Active Directory (Azure AD).

Интеграция Azure AD с приложением Mindflash обеспечивает следующие преимущества.

- С помощью Azure AD вы можете контролировать доступ к Mindflash.
- Вы можете включить автоматический вход пользователей в Mindflash (единый вход) с использованием учетной записи Azure AD.
- Вы можете управлять учетными записями централизованно — через портал Azure.

Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Технические условия

Чтобы настроить интеграцию Azure AD с Mindflash, вам потребуется:

- подписка Azure AD;
- Подписка на Mindflash с поддержкой единого входа

> [!NOTE]
> Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.

При проверке действий в этом учебнике соблюдайте следующие рекомендации:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Сценарий, описанный в этом учебнике, состоит из двух стандартных блоков.

1. Добавление Mindflash из коллекции.
2. настройка и проверка единого входа в Azure AD.

## <a name="adding-mindflash-from-the-gallery"></a>Добавление Mindflash из коллекции
Чтобы настроить интеграцию Mindflash с Azure AD, необходимо добавить Mindflash из коллекции в список управляемых приложений SaaS.

**Чтобы добавить Mindflash из коллекции, выполните следующие действия.**

1. На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**. 

    ![Active Directory][1]

2. Перейдите к разделу **Корпоративные приложения**. Затем выберите **Все приложения**.

    ![ПРИЛОЖЕНИЯ][2]
    
3. Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.

    ![ПРИЛОЖЕНИЯ][3]

4. В поле поиска введите **Mindflash**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_search.png)

5. На панели результатов выберите **Mindflash** и нажмите кнопку **Добавить**, чтобы добавить приложение.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>настройка и проверка единого входа в Azure AD.
В этом разделе описаны настройка и проверка единого входа Azure AD в Mindflash с использованием тестового пользователя Britta Simon.

Для работы единого входа Azure AD необходимо знать, какому пользователю в Azure AD соответствует пользователь в Mindflash. Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Mindflash.

Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Mindflash.

Чтобы настроить и проверить единый вход Azure AD в Mindflash, вам потребуется выполнить действия в следующих стандартных блоках.

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа в Azure AD от имени пользователя Britta Simon.
3. **[Создание тестового пользователя Mindflash](#creating-a-mindflash-test-user)** требуется для создания в Mindflash пользователя Britta Simon, связанного с представлением этого пользователя в Azure AD.
4. **[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD;
5. **[Проверка единого входа](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Mindflash.

**Чтобы настроить единый вход Azure AD в Mindflash, выполните следующие действия.**

1. На портале Azure на странице интеграции с приложением **Mindflash** щелкните **Единый вход**.

    ![Настройка единого входа][4]

2. В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_samlbase.png)

3. В разделе **Домены и URL-адреса приложения Mindflash** выполните следующие действия:

    ![Настройка единого входа](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_url.png)

    a. В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<companyname>.mindflash.com`

    Б. В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<companyname>.mindflash.com`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Замените эти значения фактическим URL-адресом для входа и идентификатором. Чтобы получить их, обратитесь в [службу поддержки клиентов Mindflash](https://www.mindflash.com/contact/). 
 


4. В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.

    ![Настройка единого входа](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-mindflash-tutorial/tutorial_general_400.png)

6. Чтобы настроить единый вход на стороне **Mindflash**, отправьте скачанный **XML-файл метаданных** в [службу поддержки Mindflash](https://www.mindflash.com/contact/).

> [!TIP]
> Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.  После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы. Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.

![Создание пользователя Azure AD][100]

**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**

1. На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mindflash-tutorial/create_aaduser_01.png) 

2. Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mindflash-tutorial/create_aaduser_02.png) 

3. Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mindflash-tutorial/create_aaduser_03.png) 

4. На странице диалогового окна **Пользователь** выполните следующие действия.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mindflash-tutorial/create_aaduser_04.png) 

    a. В текстовом поле **Имя** введите **BrittaSimon**.

    Б. В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение поля **Пароль**.

    d. Нажмите кнопку **Создать**.
 
### <a name="creating-a-mindflash-test-user"></a>Создание тестового пользователя Mindflash

Чтобы разрешить пользователям Azure AD вход в Mindflash, они должны быть подготовлены для Mindflash. В случае с Mindflash подготовка выполняется вручную.

### <a name="to-provision-a-user-accounts-perform-the-following-steps"></a>Чтобы подготовить учетные записи пользователей, выполните следующие действия.

1. Выполните вход в **Mindflash** на веб-сайте компании в качестве администратора.

2. Перейдите в раздел **Управление пользователями**.
   
    ![Управление пользователями](./media/active-directory-saas-mindflash-tutorial/ic787140.png "Управление пользователями")

3. Нажмите кнопку **Add Users** (Добавить пользователей), а затем выберите **New** (Создать).

4. В разделе **Add New Users** (Добавление новых пользователей) введите соответствующие данные действующей учетной записи Azure AD, которую необходимо подготовить.
   
    ![Add New Users](./media/active-directory-saas-mindflash-tutorial/ic787141.png "Add New Users") (Добавление новых пользователей)
   
    a. В текстовое поле **First Name** (Имя) введите **имя пользователя**, например **Britta**.

    Б. В текстовое поле **Last Name** (Фамилия) введите **фамилию**, например **Simon**.
    
    c. В текстовое поле **Email** (Адрес электронной почты) введите **адрес электронной почты** пользователя, например **BrittaSimon@contoso.com**.

    Б. Щелкните **Добавить**.

>[!NOTE]
>Для подготовки учетных записей пользователей AAD можно использовать любые другие средства создания учетных записей Mindflash или API, предоставляемое Mindflash. 
> 

### <a name="assigning-the-azure-ad-test-user"></a>Назначение тестового пользователя Azure AD

В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к Mindflash.

![Назначение пользователя][200] 

**Чтобы назначить пользователя Britta Simon в Mindflash, сделайте следующее:**

1. На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений выберите **Mindflash**.

    ![Настройка единого входа](./media/active-directory-saas-mindflash-tutorial/tutorial_mindflash_app.png) 

3. В меню слева выберите **Пользователи и группы**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.

Когда вы щелкните элемент Mindflash на панели доступа, должна появиться страница входа в приложение Mindflash.
Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по интеграции приложений SaaS с Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mindflash-tutorial/tutorial_general_203.png

