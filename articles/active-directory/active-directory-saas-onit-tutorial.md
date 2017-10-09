---
title: "Руководство по интеграции Azure Active Directory с Onit | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Onit."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: bc479a28-8fcd-493f-ac53-681975a5149c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jeedes
ms.openlocfilehash: 9e12449e5bf7f169b3cadfaa12438ac5d52ed8f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-onit"></a>Учебник. Интеграция Azure Active Directory с Onit

В этом учебнике вы узнаете, как toointegrate Onit с Azure Active Directory (Azure AD).

Интеграция Onit с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooOnit.
- Можно включить на пользователей tooautomatically get вошедшего tooOnit (Single Sign-On) с помощью своих учетных записей Azure AD.
- Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Onit требуется hello следующих элементов:

- подписка Azure AD;
- Подписка с поддержкой единого входа Onit.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария

В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Onit из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-onit-from-hello-gallery"></a>Добавление Onit из галереи hello
tooconfigure hello интеграции Onit в Azure AD, вы должны tooadd Onit из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Onit из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Кнопка Hello Azure Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Hello корпоративных приложений колонку][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Кнопка нового приложения Hello][3]

4. Введите в поле поиска hello **Onit**выберите **Onit** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.

    ![Onit в списке результатов hello](./media/active-directory-saas-onit-tutorial/tutorial_onit_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD

В этом разделе описана настройка и проверка единого входа Azure AD в приложение Onit с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Onit является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в Onit должен установить toobe.

В Onit, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с Onit, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя, прошедшего Onit](#create-an-onit-test-user)**  -toohave аналог Саймон Britta в Onit, который представляет связанный toohello Azure AD пользователя.
4. **[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#test-single-sign-on)**  tooverify ли hello works конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложение Onit.

**tooconfigure Azure AD единого входа с Onit, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Onit** странице интеграции приложения щелкните **единого входа**.

    ![Ссылка "Настройка единого входа"][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-onit-tutorial/tutorial_onit_samlbase.png)

3. На hello **URL-адреса и домена Onit** выполните следующие шаги hello:

    ![Сведения о домене и URL-адресах единого входа для приложения Onit](./media/active-directory-saas-onit-tutorial/tutorial_onit_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<sub-domain>.onit.com`

    b. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<sub-domain>.onit.com`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновить значения hello фактический URL-адрес входа и идентификатор. Обратитесь к [группа поддержки клиента Onit](https://www.onit.com/support) tooget эти значения. 
 
4. На hello **сертификат подписи SAML** раздел, hello копирования **ОТПЕЧАТОК** значение сертификата.

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-onit-tutorial/tutorial_onit_certificate.png) 

5. Приложение Onit ожидает утверждения SAML hello в определенном формате. Выполните настройку следующих утверждений для этого приложения hello. Вы можете управлять hello значения этих атрибутов из hello **«Атрибутов»** вкладку приложения hello. пример Hello следующий снимок экрана для этого. 

    ![Настройка единого входа](./media/active-directory-saas-onit-tutorial/tutorial_onit_attribute.png) 

6. В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна, Настройка атрибутов токена SAML, как показано на рисунке hello и выполните следующие шаги hello:
    
    | Имя атрибута | Значение атрибута |
    | ------------------- | -------------------- |
    | email | user.mail |
    
    а. Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.

    ![Настройка единого входа](./media/active-directory-saas-onit-tutorial/tutorial_attribute_04.png)

    ![Настройка единого входа](./media/active-directory-saas-onit-tutorial/tutorial_attribute_05.png)

    b. В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.

    c. Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.

    d. Оставьте hello **имен** пустым.
    
    д. Нажмите кнопку **ОК**.

7. Нажмите кнопку **Сохранить** .

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-onit-tutorial/tutorial_general_400.png)

8. На hello **конфигурации Onit** щелкните **Настройка Onit** tooopen **Настройка входа** окна. Копировать hello **URL-адрес выхода, единого входа службы URL-адрес SAML** из hello **краткий справочник.**

    ![Настройка Onit](./media/active-directory-saas-onit-tutorial/tutorial_onit_configure.png)

9. В другом окне веб-браузера войдите на свой корпоративный сайт Onit в качестве администратора.

10. В меню в верхней части hello hello выберите **администрирования**.
   
   ![Администрирование](./media/active-directory-saas-onit-tutorial/IC791174.png "Администрирование")
11. Щелкните **Изменить корпорацию**.
   
   ![Изменить корпорацию](./media/active-directory-saas-onit-tutorial/IC791175.png "Изменить корпорацию")
   
12. Нажмите кнопку hello **безопасности** вкладки.
    
    ![Изменение информации о компании](./media/active-directory-saas-onit-tutorial/IC791176.png "Изменение информации о компании")

13. На hello **безопасности** выполните следующие шаги hello:

    ![Единый вход](./media/active-directory-saas-onit-tutorial/IC791177.png "Единый вход")

    а. Для параметра **Authentication Strategy** (Стратегия проверки подлинности) выберите значение **Single Sign On and Password** (Единый вход и пароль).
    
    b. В **URL-адрес назначения Idp** текстовое значение hello вставить **SAML единого входа URL-адрес службы**, который вы скопировали из портала Azure.

    c. В **URL-адрес выхода поставщика удостоверений** текстовое значение hello вставить **URL-адрес выхода**, который вы скопировали из портала Azure.

    d. В **отпечаток сертификата поставщика удостоверений (SHA1)** текстовое поле, вставить hello **отпечаток** значение сертификат, который вы скопировали из портала Azure.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD

Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

   ![Создание тестового пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-onit-tutorial/create_aaduser_01.png)

2. слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-onit-tutorial/create_aaduser_02.png)

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-onit-tutorial/create_aaduser_03.png)

4. В hello **пользователя** диалогового окна выполните следующие шаги hello:

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-onit-tutorial/create_aaduser_04.png)

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.

    c. Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.

    d. Щелкните **Создать**.
 
### <a name="create-an-onit-test-user"></a>Создание тестового пользователя Onit

В порядке tooenable toolog пользователей Azure AD в Onit их необходимо подготовить в Onit.  

В случае hello объекта Onit Подготовка выполняется вручную.

**tooconfigure подготовки пользователей, выполните следующие шаги hello.**

1. Войдите на tooyour **Onit** сайт компании от имени администратора.
2. Нажмите кнопку **Add User**(Добавить пользователя).
   
   ![Администрирование](./media/active-directory-saas-onit-tutorial/IC791180.png "Администрирование")
3. На hello **добавить пользователя** диалогового окна выполните следующие шаги hello:
   
   ![Добавление пользователя](./media/active-directory-saas-onit-tutorial/IC791181.png "Добавление пользователя")
   
  1. Тип hello **имя** и hello **адрес электронной почты** из допустимых Azure текстовые поля, связанные с учетной записью AD, которые должны tooprovision hello.
  2. Щелкните **Создать**.    
   
 > [!NOTE]
 > Владелец учетной записи Azure Active Directory Hello получает сообщение электронной почты и соответствует tooconfirm ссылку свою учетную запись, чтобы она стала активной.

### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooOnit доступа.

![Назначение пользователям ролей hello][200] 

**tooassign tooOnit Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Onit**.

    ![ссылка Onit Hello в списке приложений hello](./media/active-directory-saas-onit-tutorial/tutorial_onit_app.png)  

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Hello ссылку «Пользователи и группы»][202]

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![область назначения, добавьте Hello][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello Onit плитки в панели доступа hello, вы должны получить tooyour автоматически подписан в приложение Onit.
Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-onit-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-onit-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-onit-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-onit-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-onit-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-onit-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-onit-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-onit-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-onit-tutorial/tutorial_general_203.png

