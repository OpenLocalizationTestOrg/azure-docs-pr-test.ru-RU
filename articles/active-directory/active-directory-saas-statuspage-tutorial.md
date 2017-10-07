---
title: "Руководство по интеграции Azure Active Directory и StatusPage | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и StatusPage."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f6ee8bb3-df43-4c0d-bf84-89f18deac4b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 7c6717017984241e9e459273ead4b5e062311120
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-statuspage"></a>Руководство. Интеграция Azure Active Directory и StatusPage

В этом учебнике вы узнаете, как toointegrate StatusPage с Azure Active Directory (Azure AD).

Интеграция с Azure AD StatusPage предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooStatusPage
- Можно включить на пользователей tooautomatically get вошедшего tooStatusPage (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с StatusPage требуется hello следующих элементов:

- подписка Azure AD;
- подписка StatusPage с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление StatusPage из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-statuspage-from-hello-gallery"></a>Добавление StatusPage из галереи hello
tooconfigure hello интеграции StatusPage в Azure AD, вы должны tooadd StatusPage из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd StatusPage из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **StatusPage**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_search.png)

5. В панели результатов hello выберите **StatusPage**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в StatusPage с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в StatusPage является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в StatusPage должен установить toobe.

В StatusPage, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с StatusPage, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя StatusPage](#creating-a-statuspage-test-user)**  -toohave аналог Саймон Britta в StatusPage, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении StatusPage.

**tooconfigure Azure AD единого входа с StatusPage, выполните следующие шаги hello.**

1. В hello в hello портала Azure **StatusPage** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_samlbase.png)

3. На hello **URL-адреса и домена StatusPage** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_url.png)

    а. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:
    | |
    |--|
    | `https://<subdomain>.statuspagestaging.com/` |
    | `https://<subdomain>.statuspage.io/` |

    b. В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello: 
    | |
    |--|
    | `https://<subdomain>.statuspagestaging.com/sso/saml/consume` |
    | `https://<subdomain>.statuspage.io/sso/saml/consume` |

    > [!NOTE]
    > Обратитесь в службу поддержки StatusPage hello в [ SupportTeam@statuspage.io ](mailto:SupportTeam@statuspage.io)toorequest метаданных необходимые tooconfigure единого входа. 
    >
    >а. Из метаданных hello, скопируйте значение издателя hello и вставьте его в hello **идентификатор** текстового поля.
    >
    >b. Из метаданных hello hello URL-адрес ответа скопируйте и вставьте его в hello **URL-адрес ответа** текстового поля.

4. На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-statuspage-tutorial/tutorial_general_400.png)

6. На hello **конфигурации StatusPage** щелкните **Настройка StatusPage** tooopen **Настройка входа** окна. Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_configure.png) 

7. В другом окне браузера Войдите на сайт компании StatusPage tooyour с правами администратора.

8. На главной панели инструментов hello, щелкните **Управление учетной записью**.
   
    ![Настройка единого входа](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_06.png) 

10. Нажмите кнопку hello **Single Sign-on** вкладки. 
   
    ![Настройка единого входа](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_07.png) 

11. На странице настройки единого входа hello выполните следующие шаги hello.
   
    ![Настройка единого входа](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_08.png) 

    ![Настройка единого входа](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_09.png) 
 
    а. В hello **URL-адрес единого входа для целевого** текстовое значение hello вставить **SAML единого входа URL-адрес службы**, который вы скопировали из портала Azure.

    b. Откройте загруженный сертификат в блокноте, hello копирования содержимого, а затем вставьте его в hello **сертификат** текстового поля. 

    c. Щелкните **SAVE CONFIGURATION** (Сохранить конфигурацию).

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-statuspage-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-statuspage-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-statuspage-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-statuspage-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-statuspage-test-user"></a>Создание тестового пользователя в приложении StatusPage

Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в StatusPage.

Приложение StatusPage поддерживает JIT-подготовку. Эта функция уже включена в ходе [настройки единого входа в Azure AD](#configuring-azure-ad-single-sign-on).

**toocreate пользователя с именем Саймон Britta в StatusPage, выполните следующие шаги hello.**

1. Корпоративный сайт StatusPage tooyour входа от имени администратора.

2. В меню в верхней части hello hello выберите **Управление учетной записью**.

    ![Настройка единого входа](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_06.png)

3. Нажмите кнопку hello **члены команды** вкладки. 
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_10.png) 

4. Щелкните **ADD TEAM MEMBER** (Добавить участника команды). 
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_11.png) 

5. Тип hello **адрес электронной почты**, **имя**, и **Sur имя** действительного пользователя требуется tooprovision в hello связанные текстовые поля. 
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_12.png) 

6. Для параметра **Role** (Роль) выберите значение **Client Administrator** (Администратор клиента).

7. Щелкните **CREATE ACCOUNT** (Создать учетную запись).

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooStatusPage доступа.

![Назначение пользователя][200] 

**tooassign tooStatusPage Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **StatusPage**.

    ![Настройка единого входа](./media/active-directory-saas-statuspage-tutorial/tutorial_statuspage_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".

При нажатии кнопки hello StatusPage плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour StatusPage приложения.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-statuspage-tutorial/tutorial_general_203.png

