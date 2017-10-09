---
title: "Учебник. Интеграция Azure Active Directory с Huddle | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Huddle."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8389ba4c-f5f8-4ede-b2f4-32eae844ceb0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 0b2f6c4d839943cdd07699a1ff95dc8f90505699
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-huddle"></a>Руководство. Интеграция Azure Active Directory с Huddle

В этом учебнике вы узнаете, как toointegrate Huddle с Azure Active Directory (Azure AD).

Интеграция Huddle с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooHuddle
- Можно включить на пользователей tooautomatically get вошедшего tooHuddle (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

Интеграция Azure AD tooconfigure с Huddle, требуется hello следующих элементов:

- подписка Azure AD;
- Подписка с поддержкой единого входа Huddle

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария

В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Huddle из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-huddle-from-hello-gallery"></a>Добавление Huddle из галереи hello
интеграции hello tooconfigure Huddle в Azure AD, вы должны tooadd Huddle из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Huddle из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **Huddle**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_search.png)

5. В панели результатов hello выберите **Huddle**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD

В этом разделе описана настройка и проверка единого входа Azure AD с Huddle с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Huddle является tooa в Azure AD. Другими словами связи между пользователя Azure AD и hello, связанные с пользователем в Huddle потребности toobe установлено.

В Huddle, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с Huddle, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.

2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.

3. **[Создание тестового пользователя Huddle](#creating-a-huddle-test-user)**  -toohave аналог Саймон Britta в Huddle, который представляет связанный toohello Azure AD пользователя.

4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.

5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Huddle.

**tooconfigure Azure AD единого входа с Huddle, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Huddle** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_samlbase.png)

3. На hello **Huddle доменов и URL-адреса** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_url.png)

    В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`http://<company name>.huddle.com`

    > [!NOTE] 
    > Это значение приведено для справки. Измените значение этого параметра hello фактический URL-адрес входа. Обратитесь к [группа поддержки Huddle клиента](https://huddle.zendesk.com) tooget это значение. 

4. На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-huddle-tutorial/tutorial_general_400.png)

6. На hello **Huddle конфигурации** щелкните **Настройка Huddle** tooopen **Настройка входа** окна. Копировать hello **идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.** 

    ![Настройка единого входа](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_configure.png) 
    
7. tooconfigure единого входа на стороне Huddle, необходимо загрузить hello toosend **сертификат**, **SAML единого входа URL-адрес службы**, и **идентификатор сущности SAML** слишком[Группа поддержки huddle клиента](https://huddle.zendesk.com). Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.  
   
    >[!NOTE]
    > Единый вход должен toobe включен группой поддержки Huddle hello. Можно получать уведомления, когда после завершения настройки hello. 
    > 

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 
   
### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD

Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-huddle-test-user"></a>Создание тестового пользователя Huddle

Пользователи toolog tooenable Azure AD в tooHuddle, их необходимо подготовить в Huddle. В случае hello объекта Huddle Подготовка выполняется вручную.

**tooconfigure подготовки пользователей, выполните следующие шаги hello.**

1. Войдите в tooyour **Huddle** сайт компании от имени администратора.
2. Нажмите **Рабочая область**.
3. Щелкните **People \> Invite People** (Пользователи > Пригласить пользователей).
   
   ![Люди](./media/active-directory-saas-huddle-tutorial/IC787838.png "Люди")

4. В hello **создать новое приглашение** выполните следующие шаги hello:
   
   ![Создание приглашения](./media/active-directory-saas-huddle-tutorial/IC787839.png "Создание приглашения")
   
   а. В hello **Выбор людей toojoin команды tooinvite** выберите **команды**.

   b. Тип hello **адрес электронной почты** допустимым Azure AD учетной записи требуется tooprovision в слишком**введите адрес электронной почты людям хотелось бы tooinvite** текстового поля.

   c. Нажмите кнопку **Пригласить**.   
   
    >[!NOTE]
    > Здравствуйте, что владелец получит сообщение электронной почты, включая учетную запись hello tooconfirm ссылку, чтобы она стала активной учетной записи Azure AD. 
    > 

>[!NOTE]
>Можно использовать любые другие Huddle пользователя средства создания учетных записей или интерфейсы API, предоставляемые Huddle tooprovision учетных записей пользователей Azure AD. 
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooHuddle доступа.

![Назначение пользователя][200] 

**tooassign tooHuddle Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Huddle**.

    ![Настройка единого входа](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

Если щелкнуть плитку Huddle hello в hello панели доступа, следует получать автоматически страницы входа Huddle приложения.
Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_04.png
[100]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_203.png
