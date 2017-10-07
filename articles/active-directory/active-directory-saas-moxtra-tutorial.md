---
title: "Руководство по интеграции Azure Active Directory с Moxtra | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Moxtra."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2aed2d4b-1dcd-4839-8fed-9419d107c61c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 82e2fcc390ba508e86a3992ec1c81d0a0ffed96b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moxtra"></a>Учебник. Интеграция Azure Active Directory с Moxtra

В этом учебнике вы узнаете, как toointegrate Moxtra с Azure Active Directory (Azure AD).

Интеграция с Azure AD Moxtra предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooMoxtra
- Можно включить на пользователей tooautomatically get вошедшего tooMoxtra (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Moxtra требуется hello следующих элементов:

- подписка Azure AD;
- подписка Moxtra с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Moxtra из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-moxtra-from-hello-gallery"></a>Добавление Moxtra из галереи hello
tooconfigure hello интеграции Moxtra в Azure AD, вы должны tooadd Moxtra из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Moxtra из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **Moxtra**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_search.png)

5. В панели результатов hello выберите **Moxtra**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описаны настройка и проверка единого входа Azure AD в приложение Moxtra с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Moxtra является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в Moxtra должен установить toobe.

В Moxtra, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с Moxtra, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Moxtra](#creating-a-moxtra-test-user)**  -toohave аналог Саймон Britta в Moxtra, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Moxtra.

**Azure AD tooconfigure единого входа с Moxtra, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Moxtra** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_samlbase.png)

3. На hello **URL-адреса и домена Moxtra** выполните следующий шаг hello:

    ![Настройка единого входа](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_url.png)

    В hello **URL-адрес входа** текстовом поле введите URL-адрес как:`https://www.moxtra.com/service/#login`

4. Moxtra приложение ожидает утверждения SAML hello в определенном формате. Настройка следующих утверждений для этого приложения hello. Вы можете управлять hello значения этих атрибутов из hello»**атрибуты пользователя**» на странице интеграции приложения. Следующий снимок экрана приветствия показан пример для этой конфигурации. 

    ![Настройка единого входа](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_attributes.png)
    
5. В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна, Настройка атрибутов токена SAML, как показано на рисунке hello и выполните следующие шаги hello:
    
    | Имя атрибута | Значение атрибута |
    | ------------------- | -------------------- |    
    | firstname | user.givenname |
    | lastname | user.surname |
    | idpid    | < идентификатор сущности SAML > 

    > [!Note]
    > Здравствуйте, значение **idpid** атрибут не является реальным. Можно получить фактическое значение hello из **краткий справочник** раздела **Moxtra конфигурации**.
    
    а. Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.

    ![Настройка единого входа](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_04.png)

    b. В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.

    ![Настройка единого входа](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_05.png)

    c. Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.

    d. Нажмите кнопку **ОК**.
    
5. На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_certificate.png) 

6. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-moxtra-tutorial/tutorial_general_400.png)

7. На hello **конфигурации Moxtra** щелкните **Настройка Moxtra** tooopen **Настройка входа** окна. Копировать hello **идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_configure.png) 

8. В другом окне браузера Войдите на сайт компании Moxtra tooyour с правами администратора.

9. Щелкните hello панели инструментов слева hello **консоли администрирования > SAML Single Sign-on**и нажмите кнопку **New**.
   
    ![Настройка единого входа](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_06.png) 

10. На hello **SAML** выполните следующие шаги hello:
   
    ![Настройка единого входа](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_08.png)   
 
    а. В hello **имя** текстовом поле введите имя для конфигурации (например: *SAML*). 
  
    b. В hello **идентификатор сущности поставщика удостоверений** текстовое значение hello вставить **идентификатор сущности SAML** скопирован из портала Azure. 
 
    c. В **URL-адрес входа** текстовое значение hello вставить **SAML единого входа URL-адрес службы** скопирован из портала Azure. 
 
    d. В hello **AuthnContextClassRef** введите **urn: oasis: имена: tc: SAML:2.0:ac:classes:Password**. 
 
    д. В hello **формата идентификатора имени** введите **urn: oasis: имена: tc: SAML:1.1:nameid-format: emailAddress**. 
 
    f. Откройте сертификат, который вы скачали из портала Azure в блокноте, скопируйте содержимое hello и вставьте его в hello **сертификат** текстового поля.    
 
    ж. Hello SAML электронной почты домена введите в текстовое поле почтового домена SAML.    
  
    >[!NOTE]
    >toosee hello действия tooverify hello домена щелкните hello»**я**» ниже.

    h. Нажмите кнопку **Обновить**.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-moxtra-test-user"></a>Создание тестового пользователя Moxtra

Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в Moxtra.

**toocreate пользователя с именем Саймон Britta в Moxtra, выполните следующие шаги hello.**

1. Войдите на tooyour Moxtra корпоративный сайт с правами администратора.

2. Щелкните hello панели инструментов слева hello **консоли администрирования > Управление пользователями**, а затем **добавить пользователя**.
   
    ![Настройка единого входа](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_10.png) 

3. На hello **добавить пользователя** диалоговое окно, выполните следующие шаги hello:
  
    а. В hello **имя** введите **Britta**.
  
    b. В hello **Фамилия** введите **Simon**.
  
    c. В hello **электронной почты** введите совпадает с адресом электронной почты Britta в портале Azure.
  
    d. В hello **деления** введите **разработки**.
  
    д. В hello **отдел** введите **ИТ**.
  
    f. Выберите **Администратор**.
  
    ж. Щелкните **Добавить**.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooMoxtra доступа.

![Назначение пользователя][200] 

**tooassign tooMoxtra Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Moxtra**.

    ![Настройка единого входа](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello Moxtra плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Moxtra приложения.
Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_203.png

