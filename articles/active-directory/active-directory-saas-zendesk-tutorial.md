---
title: "Руководство по интеграции Azure Active Directory с Zendesk | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Zendesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 9d7c91e5-78f5-4016-862f-0f3242b00680
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/16/2017
ms.author: jeedes
ms.openlocfilehash: 095fdd68cafbb1bf7d753dd82821bdc2fd089ef0
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zendesk"></a>Руководство. Интеграция Azure Active Directory с Zendesk

В этом руководстве описано, как интегрировать Zendesk с Azure Active Directory (Azure AD).

Интеграция Azure AD с приложением Zendesk обеспечивает следующие преимущества.

- С помощью Azure AD вы можете управлять доступом к Zendesk.
- Вы можете активировать автоматический вход пользователей в Zendesk (единый вход) с учетной записью Azure AD.
- Вы можете управлять учетными записями централизованно — на портале Azure.

Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Технические условия

Чтобы настроить интеграцию Azure AD с Zendesk, вам потребуется:

- подписка Azure AD;
- подписка Zendesk с поддержкой единого входа.

> [!NOTE]
> Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.

При проверке действий в этом учебнике соблюдайте следующие рекомендации:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Сценарий, описанный в этом учебнике, состоит из двух стандартных блоков.

1. Добавление Zendesk из коллекции.
2. настройка и проверка единого входа в Azure AD.

## <a name="adding-zendesk-from-the-gallery"></a>Добавление Zendesk из коллекции
Чтобы настроить интеграцию Zendesk с Azure AD, необходимо добавить Zendesk из коллекции в список управляемых приложений SaaS.

**Чтобы добавить Zendesk из коллекции, выполните следующие действия.**

1. На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**. 

    ![Кнопка "Azure Active Directory"][1]

2. Перейдите к разделу **Корпоративные приложения**. Затем выберите **Все приложения**.

    ![Колонка "Корпоративные приложения"][2]
    
3. Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.

    ![Кнопка "Новое приложение"][3]

4. В поле поиска введите **Zendesk**, выберите **Zendesk** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.

    ![Zendesk в списке результатов](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD

В этом разделе описана настройка и проверка единого входа Azure AD в приложение Zendesk с использованием тестового пользователя Britta Simon.

Чтобы единый вход работал, Azure AD необходимо знать, какой пользователь в Zendesk соответствует пользователю в Azure AD. Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Zendesk.

Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Zendesk.

Чтобы настроить и проверить единый вход Azure AD в Zendesk, вам потребуется выполнить действия в следующих стандартных блоках:

1. **[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.
2. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.
3. **[Создание тестового пользователя Zendesk](#create-a-zendesk-test-user)** требуется для создания в Zendesk пользователя Britta Simon, связанного с представлением этого же пользователя в Azure AD.
4. **[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.
5. **[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Zendesk.

**Чтобы настроить единый вход Azure AD в Zendesk, сделайте следующее:**

1. На портале Azure на странице интеграции с приложением **Zendesk** щелкните **Единый вход**.

    ![Ссылка "Настройка единого входа"][4]

2. В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_samlbase.png)

3. В разделе **Домены и URL-адреса приложения Zendesk** выполните следующие действия:

    ![Сведения о домене и URL-адресах единого входа для приложения Zendesk](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_url.png)

    a. В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<subdomain>.zendesk.com`

    Б. В текстовом поле **Идентификатор** введите значение в следующем формате: `<subdomain>.zendesk.com`.

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Замените эти значения фактическим URL-адресом для входа и идентификатором. Чтобы получить эти значения, обратитесь в [службу поддержки клиентов Zendesk](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise). 
 
4. В разделе **Сертификат подписи SAML** скопируйте значение **Отпечаток**.

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_certificate.png)

5. Приложение Zendesk ожидает утверждения SAML в определенном формате. Обязательные атрибуты SAML отсутствуют, но при необходимости можно добавить атрибут из раздела **Атрибуты пользователя**, выполнив следующие шаги: 

     ![Настройка единого входа](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes1.png)

    a. Щелкните **Добавить атрибут**, чтобы открыть диалоговое окно **Добавление атрибута**.

    ![Добавление атрибута для настройки единого входа](./media/active-directory-saas-zendesk-tutorial/tutorial_attribute_04.png)

    ![Окно добавления атрибута для настройки единого входа](./media/active-directory-saas-zendesk-tutorial/tutorial_attribute_05.png)

    Б. В текстовом поле **Имя** введите имя атрибута, отображаемое для этой строки.

    c. В списке **Значение** выберите значение атрибута, отображаемое для этой строки.
    
    d. Нажмите кнопку **ОК**.
 
    > [!NOTE] 
    > Используйте атрибуты расширения для добавления атрибутов, которые отсутствуют в Azure AD по умолчанию. Щелкните [User attributes that can be set in SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) (Атрибуты пользователя, которые можно настроить в SAML), чтобы получить полный список атрибутов SAML, которые принимает **Zendesk**.  

6. Нажмите кнопку **Сохранить** .

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-zendesk-tutorial/tutorial_general_400.png)

7. В разделе **Настройка Zendesk** щелкните **Настроить Zendesk**, чтобы открыть окно **Настройка единого входа**. Скопируйте **URL-адрес выхода и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.

    ![Конфигурация Zendesk](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_configure.png) 

8. В другом окне браузера войдите на свой корпоративный сайт Zendesk в качестве администратора.

9. Щелкните **Администратор**.

10. В области навигации слева щелкните **Settings** (Параметры), а затем щелкните **Security** (Безопасность).

11. На странице **Безопасность** сделайте следующее: 
   
     ![Безопасность](./media/active-directory-saas-zendesk-tutorial/ic773089.png "Безопасность")

    ![Единый вход](./media/active-directory-saas-zendesk-tutorial/ic773090.png "Единый вход")

     a. Щелкните вкладку **Admin & Agents** (Администраторы и агенты).

     Б. Выберите **Single sign-on (SSO) and SAML** (Единый вход и SAML), а затем щелкните **SAML**.

     c. В текстовое поле **URL-адрес единого входа SAML** вставьте значение **URL-адреса службы единого входа SAML**, скопированное на портале Azure. 

     d. В текстовое поле **URL-адрес удаленного выхода** вставьте значение **URL-адреса выхода**, скопированное на портале Azure.
        
     д. В текстовое поле **Certificate Fingerprint** (Отпечаток сертификата) вставьте значение **Отпечаток**, которое вы скопировали на портале Azure.
     
     f. Выберите команду **Сохранить**.

> [!TIP]
> Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.  После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы. Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD

Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.

   ![Создание тестового пользователя Azure AD][100]

**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**

1. На портале Azure в области слева нажмите кнопку **Azure Active Directory**.

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-zendesk-tutorial/create_aaduser_01.png)

2. Чтобы открыть список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.

    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-zendesk-tutorial/create_aaduser_02.png)

3. Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна **Все пользователи** щелкните **Добавить**.

    ![Кнопка "Добавить"](./media/active-directory-saas-zendesk-tutorial/create_aaduser_03.png)

4. В диалоговом окне **Пользователь** сделайте следующее.

    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-zendesk-tutorial/create_aaduser_04.png)

    a. В поле **Имя** введите **BrittaSimon**.

    Б. В поле **Имя пользователя** введите адрес электронной почты для пользователя Britta Simon.

    c. Установите флажок **Показать пароль** и запишите значение, которое отображается в поле **Пароль**.

    d. Нажмите кнопку **Создать**.
 
### <a name="create-a-zendesk-test-user"></a>Создание тестового пользователя Zendesk

Чтобы пользователи Azure AD могли выполнять вход в **Zendesk**, они должны быть подготовлены для **Zendesk**.  
В зависимости от роли, назначенной в приложениях, ожидаемое поведение будет следующим:

 1. Учетные записи с ролью **Конечный пользователь** подготавливаются автоматически при входе.
 2. Учетные записи с ролями **Агент** и **Администратор** необходимо вручную подготовить в **Zendesk** перед выполнением входа.
 
**Чтобы подготовить учетную запись пользователя, сделайте следующее:**

1. Войдите в клиент **Zendesk** .

2. Откройте вкладку **Список клиентов** .

3. Выберите вкладку **User** (Пользователь) и нажмите кнопку **Add** (Добавить).
   
    ![Добавление пользователя](./media/active-directory-saas-zendesk-tutorial/ic773632.png "Добавление пользователя")
4. Введите **имя** и **электронный адрес** существующей учетной записи Azure AD, которую нужно подготовить, а затем нажмите кнопку **Сохранить**.
   
    ![Новый пользователь](./media/active-directory-saas-zendesk-tutorial/ic773633.png "Новый пользователь")

> [!NOTE]
> Вы можете использовать любые другие средства создания учетной записи пользователя Zendesk или API, предоставляемые Zendesk, для подготовки учетных записей пользователей AAD.

### <a name="assign-the-azure-ad-test-user"></a>Назначение тестового пользователя Azure AD

В этом разделе описано, как предоставить пользователю Britta Simon доступ к Zendesk, чтобы он мог использовать единый вход Azure.

![Назначение роли пользователя][200] 

**Чтобы назначить пользователя Britta Simon в Zendesk, сделайте следующее:**

1. На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений выберите **Zendesk**.

    ![Ссылка на Zendesk в списке приложений](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_app.png)  

3. В меню слева выберите **Пользователи и группы**.

    ![Ссылка "Пользователи и группы"][202]

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Область "Добавление назначения"][203]

5. В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.

Щелкнув элемент Zendesk на панели доступа, вы автоматически войдете в приложение Zendesk.
Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по интеграции приложений SaaS с Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_203.png

