---
title: "Руководство по интеграции Azure Active Directory с FilesAnywhere | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и FilesAnywhere."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: jeedes
ms.openlocfilehash: 376364a5c75f8d069ea6390c58586acb378cd8b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-filesanywhere"></a>Руководство по интеграции Azure Active Directory с FilesAnywhere

В этом учебнике вы узнаете, как toointegrate FilesAnywhere с Azure Active Directory (Azure AD).

Интеграция с Azure AD FilesAnywhere предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooFilesAnywhere
- Можно включить на пользователей tooautomatically get вошедшего tooFilesAnywhere (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал управления Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с FilesAnywhere требуется hello следующих элементов:

- подписка Azure AD;
- подписка FilesAnywhere с поддержкой единого входа.


> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.


tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не следует использовать рабочую среду при отсутствии необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление FilesAnywhere из галереи hello
2. Настройка и проверка единого входа в Azure AD


## <a name="adding-filesanywhere-from-hello-gallery"></a>Добавление FilesAnywhere из галереи hello
tooconfigure hello интеграции FilesAnywhere в Azure AD, вы должны tooadd FilesAnywhere из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd FilesAnywhere из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портала управления Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. Нажмите кнопку **добавить** кнопку в верхней части hello диалогового окна "hello".

    ![Приложения][3]

4. Введите в поле поиска hello **FilesAnywhere**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_search.png)

5. В панели результатов hello выберите **FilesAnywhere**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в приложение FilesAnywhere с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в FilesAnywhere является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в FilesAnywhere должен установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в FilesAnywhere.

tooconfigure и теста Azure AD единого входа с FilesAnywhere, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя FilesAnywhere](#creating-a-filesanywhere-test-user)**  -toohave аналог Саймон Britta в FilesAnywhere, представление связанных toohello Azure AD ей.
3. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
4. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал управления Azure hello и настройки единого входа в приложении FilesAnywhere.

**tooconfigure Azure AD единого входа с FilesAnywhere, выполните следующие шаги hello.**

1. На портале управления Azure hello на hello **FilesAnywhere** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна, как **режим** выберите **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_samlbase.png)

3. На hello **URL-адреса и домена FilesAnywhere** статьи, при желании tooconfigure приложения hello в **режиме, инициированный IDP**:

    ![Настройка единого входа](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url.png)
    
    а. В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company name>.filesanywhere.com/saml20.aspx?c=215`
> [!NOTE]
> Обратите внимание, это значение hello **215** — **clientid** и указан для примера. Требуется tooreplace его со значением фактических clientid hello.

4. На hello **URL-адреса и домена FilesAnywhere** статьи, при желании tooconfigure приложения hello в **режиме, инициируемая SP**, выполните следующие шаги hello:
    
    ![Настройка единого входа](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url1.png)

    а. Щелкните hello **Показывать дополнительные параметры URL-адреса** параметр

    b. В hello **на URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<sub domain>.filesanywhere.com/`

    > [!NOTE] 
    > Обратите внимание на то, что они не hello реальные значения. У вас tooupdate эти значения с hello фактический на URL-адрес входа и ответ URL-адрес. Обратитесь к [FilesAnywhere поддержки](mailto:support@FilesAnywhere.com) tooget эти значения. 

5. Программное обеспечение FilesAnywhere приложение ожидает утверждения SAML hello в определенном формате. Выполните настройку следующих утверждений для этого приложения hello. Вы можете управлять hello значения этих атрибутов из hello»**атрибуты пользователя**» на странице интеграции приложения. пример Hello следующий снимок экрана для этого.
    
    ![Настройка единого входа](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_attribute.png)
    
    Когда hello регистрирует пользователей с FilesAnywhere, они получают значение hello **clientid** атрибута из [FilesAnywhere команды](mailto:support@FilesAnywhere.com). Атрибут «Идентификатор клиента» hello tooadd с hello уникальное значение, предоставляемые FilesAnywhere. Все указанные выше атрибуты являются обязательными.
    > [!NOTE] 
    > Обратите внимание, это значение hello **2331** из **clientid** лишь пример. Необходимо получить фактическое значение tooprovide hello.


6. В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна, настроить атрибутов токена SAML, как показано в приведенном выше рисунке hello и выполнять hello следующие шаги:
    
    | Имя атрибута | Значение атрибута |
    | ---------------| --------------- |    
    | clientid | *"uniquevalue"* |

    а. Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.

    ![Настройка единого входа](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_04.png)

    ![Настройка единого входа](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_05.png)
    
    b. В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.
    
    c. Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.
    
    d. Нажмите кнопку **ОК**.

7. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_400.png)

8. На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_certificate.png) 

9. На hello **конфигурации FilesAnywhere** щелкните **Настройка FilesAnywhere** tooopen **Настройка входа** окна.

    ![Настройка единого входа](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configure.png) 

    ![Настройка единого входа](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configuresignon.png)

10. tooget единого входа: Завершение настройки приложения в конце FilesAnywhere контакт [FilesAnywhere поддержки](mailto:support@FilesAnywhere.com) и передавать их в маркер SAML загружаются hello подписи сертификата и единого входа (SSO) URL-адрес.

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя на портале управления Azure hello, вызывается Саймон Britta.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал управления Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_01.png) 

2. Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_02.png) 

3. Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**. 



### <a name="creating-a-filesanywhere-test-user"></a>Создание тестового пользователя FilesAnywhere

В время подготовки пользователей и после проверки подлинности пользователей в приложении hello автоматически создаются непосредственно поддерживает приложение. 


### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления ее tooFilesAnywhere доступа.

![Назначение пользователя][200] 

**tooassign tooFilesAnywhere Britta Simon выполните следующие шаги hello.**

1. На портале управления Azure hello, открыть представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **FilesAnywhere**.

    ![Настройка единого входа](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    


### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello FilesAnywhere плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour FilesAnywhere приложения.


## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_203.png
