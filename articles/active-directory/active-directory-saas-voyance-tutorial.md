---
title: "Руководство по интеграции Azure Active Directory с Voyance | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Voyance."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 539dc1f9-64c9-4dce-b259-2b0b49dcf857
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2017
ms.author: jeedes
ms.openlocfilehash: e2cb9eb6b20e8611a9f6e8529b7c85a8d86ec3e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-voyance"></a>Руководство по интеграции Azure Active Directory с Voyance

В этом учебнике вы узнаете, как toointegrate Voyance с Azure Active Directory (Azure AD).

Интеграция с Azure AD Voyance предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooVoyance
- Можно включить на пользователей tooautomatically get вошедшего tooVoyance (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Voyance требуется hello следующих элементов:

- подписка Azure AD;
- подписка Voyance с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Voyance из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-voyance-from-hello-gallery"></a>Добавление Voyance из галереи hello
tooconfigure hello интеграции Voyance в Azure AD, вы должны tooadd Voyance из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Voyance из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Кнопка Hello Azure Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Hello корпоративных приложений колонку][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Кнопка нового приложения Hello][3]

4. Введите в поле поиска hello **Voyance**выберите **Voyance** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.

    ![Voyance в списке результатов hello](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD

В этом разделе описана настройка и проверка единого входа Azure AD в Voyance с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Voyance является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в Voyance должен установить toobe.

В Voyance, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с Voyance, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Voyance](#create-a-voyance-test-user)**  -toohave аналог Саймон Britta в Voyance, который представляет связанный toohello Azure AD пользователя.
4. **[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Voyance.

**tooconfigure Azure AD единого входа с Voyance, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Voyance** странице интеграции приложения щелкните **единого входа**.

    ![Ссылка "Настройка единого входа"][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_samlbase.png)

3. На hello **Voyance доменов и URL-адреса** выполните hello, выполните действия, при желании tooconfigure приложения hello в **IDP** инициировал режим:

    ![Сведения о домене и URL-адресах единого входа Voyance для поставщика удостоверений](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url1.png)

    а. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.nyansa.com`

    b. В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.nyansa.com/saml/create/`

4. Проверьте **Показывать дополнительные параметры URL-адреса** и выполните следующий шаг при желании tooconfigure приложения hello в hello **SP** инициировал режим:

    ![Сведения о домене и URL-адресах единого входа Voyance для поставщика услуг](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url2.png)

    В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.nyansa.com/`
     
    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновить значения hello фактический идентификатор, URL-адрес ответа и URL-адрес входа. Обратитесь к [группа поддержки клиента Voyance](mailto:support@nyansa.com) tooget эти значения. 

5. На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_certificate.png) 

6. Нажмите кнопку **Сохранить** .

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-voyance-tutorial/tutorial_general_400.png)
    
7. На hello **конфигурации Voyance** щелкните **Настройка Voyance** tooopen **Настройка входа** окна. Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка Voyance](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_configure.png) 

8. В другом окне браузера, клиент Voyance tooyour входа от имени администратора.

9. Перейдите toohello правом верхнем углу панели навигации hello и щелкните hello раскрывающийся список с надписью «**университета Acme**».
    
    ![Настройка единого входа на стороне приложения. Acme University](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_001.png) 

10. Щелкните **Admin Settings** (Параметры администрирования).

    ![Настройка единого входа на стороне приложения. Параметры администрирования](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_002.png)

11. Щелкните вкладку **User Access** (Доступ пользователей).

    ![Настройка единого входа на стороне приложения. Доступ пользователей](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_003.png)

12. Щелкните hello»**единого входа отключена**"tooconfigure кнопку Azure AD как поставщика удостоверений с помощью SAML 2.0.

    ![Настройка единого входа на стороне приложения. Кнопка SSO is disabled (Единый вход отключен)](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_004.png)

13. Go слишком**SAML v2** раздел и выполните следующие действия:

    ![Настройка единого входа на стороне приложения. SAML v2](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_005.png)
    
    а. Щелкните **Включено**.
    
    b. Вставить **SAML единого входа URL-адрес службы**, которого вы скопировали из портала Azure hello в hello **URL-адрес входа поставщика удостоверений** текстового поля.

    c. Откройте загруженный сертификат в кодировке Base64 в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **сертификата поставщика удостоверений** текстового поля.
    
    d. Щелкните **Сохранить**.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD

Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание тестового пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-voyance-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-voyance-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Кнопка "Добавить" Hello](./media/active-directory-saas-voyance-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-voyance-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="create-a-voyance-test-user"></a>Создание тестового пользователя Voyance

Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в Voyance. Приложение Voyance поддерживает JIT-подготовку. Эта функция включена по умолчанию. В этом разделе никакие действия с вашей стороны не требуются. Новый пользователь создается во время попытки tooaccess Voyance, если он еще не существует.

>[!NOTE]
>Если требуется toocreate пользователя вручную, необходимо toocontact [Voyance поддержки](maiLto:support@nyansa.com).

### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooVoyance доступа.

![Назначение пользователям ролей hello][200]

**tooassign tooVoyance Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Voyance**.

    ![ссылка Voyance Hello в списке приложений hello](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Hello ссылку «Пользователи и группы»][202]

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![область назначения, добавьте Hello][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello Voyance плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Voyance приложения.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_203.png

