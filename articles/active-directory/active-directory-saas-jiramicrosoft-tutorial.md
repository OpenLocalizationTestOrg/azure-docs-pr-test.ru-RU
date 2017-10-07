---
title: "Руководство по интеграции Azure Active Directory с JIRA SAML SSO by Microsoft | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и единого входа SAML JIRA корпорацией Майкрософт."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0dc847b9-eec4-4c31-845e-0144ddedc4a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 178c4c040d9939bca271ac185ca5c2feb14f1247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jira-saml-sso-by-microsoft"></a>Руководство по интеграции Azure Active Directory с JIRA SAML SSO by Microsoft

В этом учебнике вы узнаете, как toointegrate единого входа SAML JIRA корпорацией Майкрософт в Azure Active Directory (Azure AD).

Интеграция единого входа SAML JIRA корпорацией Майкрософт с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooJIRA единого входа SAML корпорацией Майкрософт
- Ваш пользователей tooautomatically get вошедшего tooJIRA единого входа SAML корпорацией Майкрософт (Single Sign-On) можно включить с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с помощью единого входа SAML JIRA корпорацией Майкрософт, требуется hello следующих элементов:

- подписка Azure AD;
- JIRA серверного приложения, установленные на сервере Windows 64-разрядная (локально или в облаке hello инфраструктуры IaaS)
- поддержка HTTPS на сервере JIRA;
- Примечание версии hello поддерживается для подключаемого модуля JIRA упоминаются в под разделом.
- JIRA сервер доступен в Интернете особенно tooAzure входа AD для проверки подлинности и необходимо будет tooreceive hello токена из Azure AD
- в JIRA должны быть настроены учетные данные администратора;
- в JIRA должна быть отключена поддержка WebSudo;
- Тестовый пользователь, созданные в hello JIRA серверного приложения

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется использовать рабочей среде JIRA. Сначала протестируйте интеграцию hello в разработки или промежуточной среде приложения hello, а затем используйте hello рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="supported-versions-of-jira"></a>Поддерживаемые версии JIRA 

Сейчас поддерживаются следующие версии JIRA:

- Ядро JIRA и программного обеспечения: 6.0 too7.2.0
- JIRA службы поддержки: 3.0 too3.2

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление единого входа SAML JIRA корпорацией Майкрософт из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-jira-saml-sso-by-microsoft-from-hello-gallery"></a>Добавление единого входа SAML JIRA корпорацией Майкрософт из галереи hello
tooconfigure hello интеграции единого входа SAML JIRA корпорацией Майкрософт в Azure AD, вы должны tooadd единого входа SAML JIRA корпорацией Майкрософт из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd единого входа SAML JIRA корпорацией Майкрософт из галереи hello выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **JIRA единого входа SAML корпорацией Майкрософт**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_search.png)

5. В панели результатов hello выберите **JIRA единого входа SAML корпорацией Майкрософт**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в JIRA SAML SSO by Microsoft с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в единый вход SAML JIRA корпорацией Майкрософт является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в единый вход SAML JIRA корпорацией Майкрософт должен установить toobe.

В единый вход SAML JIRA корпорацией Майкрософт, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и тестирования Azure AD единого входа с помощью единого входа SAML JIRA корпорацией Майкрософт, необходимы следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание единого входа SAML JIRA теста пользователем Microsoft](#creating-a-jira-saml-sso-by-microsoft-test-user)**  -toohave аналог Саймон Britta в единый вход SAML JIRA корпорацией Майкрософт, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе вы включите Azure AD единым входом в портал Azure hello и настроить единый вход в ваш единого входа SAML JIRA приложением Microsoft.

**tooconfigure Azure AD единого входа с помощью единого входа SAML JIRA корпорацией Майкрософт, выполните следующие шаги hello.**

1. В hello в hello портала Azure **JIRA единого входа SAML корпорацией Майкрософт** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_samlbase.png)

3. На hello **JIRA единого входа SAML, URL-адреса и домена Microsoft** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<domain:port>/plugins/servlet/saml/auth`

    b. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<domain:port>/`

    c. В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<domain:port>/plugins/servlet/saml/auth`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновить значения hello фактический идентификатор, URL-адрес ответа и URL-адрес входа. Если это именованный URL-адрес, то порт указывать необязательно. Эти значения будут получены во время настройки hello Jira подключаемого модуля, который описывается далее в учебнике hello.
 
4. toogenerate hello **метаданные** URL-адрес, выполните следующие шаги hello:

    а. Щелкните **Регистрация приложений**.
    
    ![Настройка единого входа](./media/active-directory-saas-jiramicrosoft-tutorial/appregistrations.png)
   
    b. Нажмите кнопку **конечные точки** tooopen **конечные точки** диалоговое окно.  
    
    ![Настройка единого входа](./media/active-directory-saas-jiramicrosoft-tutorial/endpointicon.png)

    c. Нажмите кнопку toocopy hello копирования **документа МЕТАДАННЫХ ФЕДЕРАЦИИ** URL-адрес и вставьте его в Блокнот.
    
    ![Настройка единого входа](./media/active-directory-saas-jiramicrosoft-tutorial/endpoint.png)
     
    d. Теперь перейдите на странице свойств toohello **JIRA единого входа SAML корпорацией Майкрософт** и копирования hello **идентификатор приложения** с помощью **копирования** кнопку и вставьте его в Блокнот.
 
    ![Настройка единого входа](./media/active-directory-saas-jiramicrosoft-tutorial/appid.png)

    д. Создать hello **URL-адрес метаданных** с помощью hello следующий шаблон: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` и скопируйте это значение в блокноте, как используется позднее для конфигурации hello hello подключаемого модуля.

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_400.png)

6. Обратитесь к [Microsoft](mailto:waadpartners@microsoft.com) с hello следующую информацию для подключаемого модуля JIRA hello.
    
    *   Имя клиента:
    *   Основное доменное имя:
    *   Azure AD Premium: Да/Нет (подключаемого модуля будут доступны tooall hello клиента Free, Basic и Premium SKU)
    *   Число пользователей, которые будут использовать данную интеграцию:
    *   версия JIRA;
    *   Комментарии.

7. В другом окне браузера войдите в экземпляр JIRA tooyour в качестве администратора.

8. Наведите указатель мыши на шестеренки и выберите hello **надстройки**.
    
    ![Настройка единого входа](./media/active-directory-saas-jiramicrosoft-tutorial/addon1.png)

9. На вкладке "Надстройки" щелкните **Управление надстройками**.

    ![Настройка единого входа](./media/active-directory-saas-jiramicrosoft-tutorial/addon7.png)

10. Вручную Загрузите подключаемый модуль hello, предоставляемых корпорацией Майкрософт. Если установлен подключаемый модуль hello, оно появляется в **пользователь установил** надстройки раздел **Управление надстройками** раздела.

11. Нажмите кнопку **Настройка** tooconfigure hello нового подключаемого модуля.

12. Выполните следующие действия на странице настройки:

    ![Настройка единого входа](./media/active-directory-saas-jiramicrosoft-tutorial/addon5.png)
 
    а. В **URL-адрес метаданных** вставьте hello **URL-адрес метаданных** создаются из Azure AD и щелкните hello **Разрешить** кнопки. Считывает URL-адрес метаданных поставщика удостоверений hello и заполняет все сведения о полях hello.

    > [!Note]
    > По умолчанию идентификатор пользователя SAML указан в идентификаторе имени. Можно изменить этот параметр tooan атрибута и введите имя соответствующего атрибута hello.

    > [!TIP]
    > Убедитесь, что имеется только один сертификат, сопоставленных с приложение hello, таким образом, не содержит ошибок в разрешении метаданных hello. Если имеется несколько сертификатов, при разрешении метаданных hello admin возвращает ошибку.
    
    b. Копировать hello **идентификатор, URL-адрес ответа и URL-адрес входа** значения и вставьте их в **идентификатор, URL-адрес ответа и URL-адрес входа** соответственно, в текстовых полях **единого входа SAML JIRA доменом Microsoft и URL-адреса** раздела на портале Azure.

    c. В **имя кнопки входа** имя типа hello кнопки организация хочет hello toosee пользователей на экране входа.

    d. В **размещение идентификатора пользователя SAML** выберите либо **идентификатор пользователя находится в элементе NameIdentifier hello hello оператора Subject** или **идентификатор пользователя — это элемент атрибута**.  Этот идентификатор имеет идентификатор пользователя JIRA toobe hello. Если идентификатор пользователя hello нет соответствия, система не позволит пользователям toolog в. 
    
    д. При выборе **идентификатор пользователя — это элемент атрибута** параметр, а затем в **имя атрибута** текстовое поле типа hello имя атрибута hello, где ожидается идентификатор пользователя. 

    f. При использовании hello федеративного домена (например, служб федерации Active Directory и т.д.) в Azure AD выберите команду hello **включения обнаружения домашней области** и настройте hello **доменное имя**.
    
    ж. В **доменное имя** типа hello доменное имя здесь в случае входа на основе ADFS hello.

    h. Проверьте **Включить единый Выход** при необходимости toolog out из Azure AD, когда пользователь выполняет выход из JIRA. 

    i. Нажмите кнопку **Сохранить** кнопку Параметры toosave hello.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-jira-saml-sso-by-microsoft-test-user"></a>Создание тестового пользователя JIRA SAML SSO by Microsoft

Пользователи toolog tooenable Azure AD в tooJIRA на локальном сервере, их необходимо подготовить в единый вход SAML JIRA корпорацией Майкрософт. Для JIRA SAML SSO by Microsoft подготовка выполняется вручную.

**tooprovision учетной записи пользователя, выполните следующие шаги hello.**

1. Войдите в tooyour JIRA локального сервера с правами администратора.

2. Наведите указатель мыши на шестеренки и выберите hello **Управление пользователями**.

    ![Добавление сотрудника](./media/active-directory-saas-jiramicrosoft-tutorial/user1.png) 

3. Являются tooenter страницы доступ перенаправленной tooAdministrator **пароль** и нажмите кнопку **Подтверждение** кнопки.

    ![Добавление сотрудника](./media/active-directory-saas-jiramicrosoft-tutorial/user2.png) 

4. В разделе **User management** (Управление пользователями) щелкните **Create user** (Создать пользователя).

    ![Добавление сотрудника](./media/active-directory-saas-jiramicrosoft-tutorial/user3.png) 

5. На hello **«Создать пользователя»** диалогового окна выполните следующие шаги hello:

    ![Добавление сотрудника](./media/active-directory-saas-jiramicrosoft-tutorial/user4.png) 

    а. В hello **адрес электронной почты** в текстовое поле типа hello адрес электронной почты пользователя, например Brittasimon@contoso.com.

    b. В hello **полное имя** текстовое поле, полное имя типа пользователя hello как Саймон Britta.

    c. В hello **Username** электронной почты hello тип пользователя в текстовое поле, например Brittasimon@contoso.com.

    d. В hello **пароль** текстового поля, типа hello пароль пользователя.

    д. Щелкните **Create user** (Создать пользователя).   

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooJIRA единого входа SAML корпорацией Майкрософт.

![Назначение пользователя][200] 

**tooassign tooJIRA Britta Simon единого входа SAML корпорацией Майкрософт, выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **JIRA единого входа SAML корпорацией Майкрософт**.

    ![Настройка единого входа](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello единого входа SAML JIRA по Microsoft плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour единого входа SAML JIRA приложением Microsoft.
Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_203.png

