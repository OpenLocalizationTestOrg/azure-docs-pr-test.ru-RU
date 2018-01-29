---
title: "Руководство по интеграции Azure Active Directory с GoToMeeting | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и GoToMeeting."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: bcaf19f2-5809-4e1c-acbc-21a8d3498ccf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/02/2018
ms.author: jeedes
ms.openlocfilehash: 4826dee82e62ffac70d7ca3d6dcfe005129de764
ms.sourcegitcommit: 48fce90a4ec357d2fb89183141610789003993d2
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/12/2018
---
# <a name="tutorial-azure-active-directory-integration-with-gotomeeting"></a>Руководство по интеграции Azure Active Directory с GoToMeeting

В этом руководстве описано, как интегрировать GoToMeeting с Azure Active Directory (Azure AD).

Интеграция GoToMeeting с Azure AD обеспечивает перечисленные ниже преимущества.

- С помощью Azure AD вы можете контролировать доступ к GoToMeeting.
- Вы можете включить автоматический вход пользователей в GoToMeeting (единый вход) с учетной записью Azure AD.
- Вы можете управлять учетными записями централизованно — на портале Azure.

Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Необходимые компоненты

Чтобы настроить интеграцию Azure AD с GoToMeeting, вам потребуется:

- подписка Azure AD;
- подписка GoToMeeting с поддержкой единого входа.

> [!NOTE]
> Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.

При проверке действий в этом учебнике соблюдайте следующие рекомендации:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Сценарий, описанный в этом учебнике, состоит из двух стандартных блоков.

1. Добавление GoToMeeting из коллекции.
2. настройка и проверка единого входа в Azure AD.

## <a name="adding-gotomeeting-from-the-gallery"></a>Добавление GoToMeeting из коллекции.
Чтобы настроить интеграцию GoToMeeting с Azure AD, вам нужно добавить GoToMeeting из коллекции в список управляемых приложений SaaS.

**Чтобы добавить GoToMeeting из коллекции, выполните указанные ниже действия.**

1. На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**. 

    ![Кнопка "Azure Active Directory"][1]

2. Перейдите к разделу **Корпоративные приложения**. Затем выберите **Все приложения**.

    ![Колонка "Корпоративные приложения"][2]
    
3. Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.

    ![Кнопка "Новое приложение"][3]

4. В поле поиска введите **GoToMeeting**, выберите **GoToMeeting** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.

    ![GoToMeeting в списке результатов](./media/active-directory-saas-gotomeeting-tutorial/tutorial_gotomeeting_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD

В этом разделе описана настройка и проверка единого входа Azure AD в GoToMeeting с использованием тестового пользователя Britta Simon.

Чтобы единый вход работал, Azure AD необходимо знать, какой пользователь в GoToMeeting соответствует пользователю в Azure AD. Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем GoToMeeting.

Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в GoToMeeting.

Чтобы настроить и проверить единый вход Azure AD в GoToMeeting, вам нужно выполнить действия в перечисленных ниже стандартных блоках.

1. **[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.
2. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.
3. **[Создание тестового пользователя приложения GoToMeeting](#create-a-gotomeeting-test-user)** требуется для того, чтобы в GoToMeeting существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.
4. **[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.
5. **[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении GoToMeeting.

**Чтобы настроить единый вход Azure AD в GoToMeeting, выполните указанные ниже действия.**

1. На портале Azure на странице интеграции с приложением **GoToMeeting** щелкните **Единый вход**.

    ![Ссылка "Настройка единого входа"][4]

2. В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-gotomeeting-tutorial/tutorial_gotomeeting_samlbase.png)

3. В разделе **Домены и URL-адреса приложения GoToMeeting** сделайте следующее:

    ![Сведения о домене и URL-адресах единого входа для приложения GoToMeeting](./media/active-directory-saas-gotomeeting-tutorial/tutorial_gotomeeting_url.png)

    В текстовом поле **Идентификатор** введите URL-адрес `https://login.citrixonline.com/saml/sp`.

4. В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-gotomeeting-tutorial/tutorial_gotomeeting_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-gotomeeting-tutorial/tutorial_general_400.png)

6. Для создания URL-адреса **метаданных** выполните следующие действия.

    a. Щелкните **Регистрация приложений**.
    
    ![Настройка единого входа](./media/active-directory-saas-gotomeeting-tutorial/tutorial_gotomeeting_appregistrations.png)
   
    Б. Щелкните **Конечные точки**, чтобы открыть диалоговое окно **Конечные точки**.  
    
    ![Настройка единого входа](./media/active-directory-saas-gotomeeting-tutorial/tutorial_gotomeeting_endpointicon.png)

    c. Нажмите кнопку "Копировать", чтобы скопировать URL-адрес **документа метаданных федерации**, а затем вставьте его в блокнот.
    
    ![Настройка единого входа](./media/active-directory-saas-gotomeeting-tutorial/tutorial_gotomeeting_endpoint.png)
     
    d. Теперь перейдите на страницу свойств **GoToMeeting** и скопируйте **идентификатор приложения** с помощью кнопки **Копировать**, а затем вставьте его в Блокнот.
 
    ![Настройка единого входа](./media/active-directory-saas-gotomeeting-tutorial/tutorial_gotomeeting_appid.png)

    д. Создайте **URL-адрес метаданных** по следующему шаблону: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`.   

7. В разделе **Настройка GoToMeeting** щелкните **Настроить GoToMeeting**, чтобы открыть окно **Настройка единого входа**. Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.

    ![Настройка GoToMeeting](./media/active-directory-saas-gotomeeting-tutorial/tutorial_gotomeeting_configure.png) 

8. В другом окне браузера войдите в [центр организации GoToMeeting](https://organization.logmeininc.com/).

9. На вкладке **Identity provider** (Поставщик удостоверений) вы можете настроить параметры Azure, предоставив сгенерированный **URL-адрес метаданных**, загруженный **файл метаданных** или выбрав режим **Manual** (Вручную).

10. Для создания **URL-адреса метаданных** выполните следующие действия.

    ![Настройка GoToMeeting](./media/active-directory-saas-gotomeeting-tutorial/config1.png)

    a. В поле **How would you like to configure your SAML IDP?** (Как вы хотите настроить поставщик удостоверений SAML?) из раскрывающегося списка выберите **Automatic** (Автоматически).

    Б. Вставьте **URL-адрес метаданных**, который вы сгенерировали на предыдущих шагах, в текстовое поле **Metadata URL** (URL-адрес метаданных).

    c. Выберите команду **Сохранить**.

11. Для создания **файла метаданных** выполните следующие действия.

    ![Настройка GoToMeeting](./media/active-directory-saas-gotomeeting-tutorial/config2.png)

    a. В поле **How would you like to configure your SAML IDP?** (Как вы хотите настроить поставщик удостоверений SAML?) из раскрывающегося списка выберите **Upload SAML metadata file** (Передать файл метаданных SAML).

    Б. Чтобы отправить загруженный файл метаданных, нажмите кнопку **Upload metadata file** (Отправить файл метаданных).

    c. Выберите команду **Сохранить**.

12. Если вы хотите использовать режим **Manual** (Вручную), выполните следующие действия.

    ![Настройка GoToMeeting](./media/active-directory-saas-gotomeeting-tutorial/config3.png)

    a.  В текстовое поле **Sign-in page URL** (URL-адрес страницы входа) вставьте значение **SAML Single Sign-On Service URL** (URL-адрес службы единого входа SAML), скопированное на портале Azure.

    Б.  В текстовое поле **Sign-out page URL** (URL-адрес страницы выхода) вставьте значение **URL-адрес выхода**, скопированное на портале Azure.

    c.  В текстовое поле **Identity Provider Entity ID** (Идентификатор сущности поставщика удостоверений) вставьте значение **SAML Entity ID** (Идентификатор сущности SAML), скопированное на портале Azure.

    d. Извлеките X509Certificate из загруженного файла метаданных и передайте этот сертификат, нажав кнопку **Upload certificate** (Отправить сертификат).

    д. Выберите команду **Сохранить**.

> [!TIP]
> Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.  После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы. Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD

Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.

   ![Создание тестового пользователя Azure AD][100]

**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**

1. На портале Azure в области слева нажмите кнопку **Azure Active Directory**.

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-gotomeeting-tutorial/create_aaduser_01.png)

2. Чтобы открыть список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.

    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-gotomeeting-tutorial/create_aaduser_02.png)

3. Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна **Все пользователи** щелкните **Добавить**.

    ![Кнопка "Добавить"](./media/active-directory-saas-gotomeeting-tutorial/create_aaduser_03.png)

4. В диалоговом окне **Пользователь** сделайте следующее.

    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-gotomeeting-tutorial/create_aaduser_04.png)

    a. В поле **Имя** введите **BrittaSimon**.

    Б. В поле **Имя пользователя** введите адрес электронной почты для пользователя Britta Simon.

    c. Установите флажок **Показать пароль** и запишите значение, которое отображается в поле **Пароль**.

    d. Нажмите кнопку **Создать**.
 
### <a name="create-a-gotomeeting-test-user"></a>Создание тестового пользователя GoToMeeting

В этом разделе вы создадите в GoToMeeting пользователя с именем Britta Simon. Приложение GoToMeeting поддерживает JIT-подготовку. Эта функция включена по умолчанию.

В этом разделе никакие действия с вашей стороны не требуются. Если пользователь в GoToMeeting еще не существует, он будет создан при попытке доступа к приложению GoToMeeting.

> [!NOTE]
> Чтобы создать пользователя вручную, обратитесь в [службу поддержки GoToMeeting](https://support.logmeininc.com/gotomeeting).

### <a name="assign-the-azure-ad-test-user"></a>Назначение тестового пользователя Azure AD

В этом разделе описано, как предоставить пользователю Britta Simon доступ к GoToMeeting, чтобы он мог использовать единый вход Azure.

![Назначение роли пользователя][200] 

**Чтобы назначить пользователя Britta Simon в GoToMeeting, выполните указанные ниже действия.**

1. На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений выберите **GoToMeeting**.

    ![Ссылка на GoToMeeting в списке "Приложения"](./media/active-directory-saas-gotomeeting-tutorial/tutorial_gotomeeting_app.png)  

3. В меню слева выберите **Пользователи и группы**.

    ![Ссылка "Пользователи и группы"][202]

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Область "Добавление назначения"][203]

5. В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.

Щелкнув плитку GoToMeeting на панели доступа, вы автоматически войдете в приложение GoToMeeting.
Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по интеграции приложений SaaS с Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Руководство по настройке Google Apps для автоматической подготовки пользователей](https://docs.microsoft.com/azure/active-directory/active-directory-saas-citrixgotomeeting-provisioning-tutorial)


<!--Image references-->

[1]: ./media/active-directory-saas-gotomeeting-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-gotomeeting-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-gotomeeting-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-gotomeeting-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-gotomeeting-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-gotomeeting-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-gotomeeting-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-gotomeeting-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-gotomeeting-tutorial/tutorial_general_203.png

