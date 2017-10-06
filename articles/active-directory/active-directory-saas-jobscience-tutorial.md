---
title: "Учебник. Интеграция Azure Active Directory с Jobscience | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Jobscience."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 77282dcc-bbe2-4728-953d-adb4ab6a713b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 4a4c78aad6d324795a15a9569542afc23b4716d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobscience"></a>Руководство. Интеграция Azure Active Directory с Jobscience

В этом учебнике вы узнаете, как toointegrate Jobscience с Azure Active Directory (Azure AD).

Интеграция Jobscience с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooJobscience
- Можно включить на пользователей tooautomatically get вошедшего tooJobscience (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Jobscience требуется hello следующих элементов:

- подписка Azure AD;
- подписка Jobscience с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Jobscience из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-jobscience-from-hello-gallery"></a>Добавление Jobscience из галереи hello
tooconfigure hello интеграции Jobscience в Azure AD, вы должны tooadd Jobscience из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Jobscience из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **Jobscience**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_search.png)

5. В панели результатов hello выберите **Jobscience**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Jobscience с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Jobscience является tooa в Azure AD. Другими словами связи между пользователя Azure AD и hello связанных пользователей в Jobscience должен установить toobe.

В Jobscience, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с Jobscience, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Jobscience](#creating-a-jobscience-test-user)**  -toohave аналог Саймон Britta в Jobscience, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в Jobscience приложения.

**tooconfigure Azure AD единого входа с Jobscience, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Jobscience** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_samlbase.png)

3. На hello **URL-адреса и домена Jobscience** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_url.png)

    В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`http://<company name>.my.salesforce.com`
    
    > [!NOTE] 
    > Это значение приведено для справки. Измените значение этого параметра hello фактический URL-адрес входа. Это значение можно получить [группа поддержки клиента Jobscience](https://www.jobscience.com/support) или из hello профиль единого входа будет создана, который описан далее в учебнике hello. 
 
4. На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-jobscience-tutorial/tutorial_general_400.png)

6. На hello **конфигурации Jobscience** щелкните **Настройка Jobscience** tooopen **Настройка входа** окна. Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_configure.png) 

7. Войдите в систему tooyour сайте Jobscience для компании как администратор.

8. Go слишком**установки**.
   
   ![Настройка](./media/active-directory-saas-jobscience-tutorial/IC784358.png "Настройка")

9. На панели навигации слева hello в hello **Администрирование** щелкните **Управление доменами** tooexpand hello соответствующий раздел и нажмите кнопку **Мой домен** tooopen hello  **Мой домен** страницы. 
   
   ![Мой домен](./media/active-directory-saas-jobscience-tutorial/ic767825.png "Мой домен")

10. tooverify, домен настроен неправильно, убедитесь, что он находится в "**шаг 4 развернут tooUsers**» и просмотрите вашей»**мои параметры домена**».

    ![Домен развернутые tooUser](./media/active-directory-saas-jobscience-tutorial/ic784377.png "tooUser домена развертывания")

11. Щелкните hello сайте Jobscience для компании **управления безопасностью**и нажмите кнопку **параметры единого входа**.
    
    ![Средства управления безопасностью](./media/active-directory-saas-jobscience-tutorial/ic784364.png "Средства управления безопасностью")

12. В hello **параметры единого входа** выполните следующие шаги hello:
    
    ![Параметры единого входа](./media/active-directory-saas-jobscience-tutorial/ic781026.png "Параметры единого входа")
    
    а. Установите флажок **SAML включен**.

    b. Нажмите кнопку **Создать**.

13. На hello **SAML единого входа для изменения настроек** диалоговое окно, выполните следующие шаги hello:
    
    ![Параметры единого входа SAML](./media/active-directory-saas-jobscience-tutorial/ic784365.png "Параметры единого входа SAML")
    
    а. В hello **имя** текстовом поле введите имя для конфигурации.

    b. В **издателя** текстовое значение hello вставить **SAML идентификатор сущности**, который вы скопировали из портала Azure.

    c. В hello **идентификатор сущности** текстовое поле, тип`https://salesforce-jobscience.com`

    d. Нажмите кнопку **Обзор** tooupload сертификат Azure AD.

    д. Как **типа удостоверения SAML**выберите **утверждение, содержащее hello идентификатор федерации из объекта пользователя hello**.

    f. Как **расположения удостоверения SAML**выберите **удостоверение находится в hello элемент NameIdentfier оператора Subject hello**.

    ж. В **URL-адрес входа поставщика удостоверений** текстовое значение hello вставить **SAML единого входа URL-адрес службы**, который вы скопировали из портала Azure.

    h. В **URL-адрес выхода поставщика удостоверений** текстовое значение hello вставить **URL-адрес выхода**, который вы скопировали из портала Azure.

    i. Щелкните **Сохранить**.

14. На панели навигации слева hello в hello **Администрирование** щелкните **Управление доменами** tooexpand hello соответствующий раздел и нажмите кнопку **Мой домен** tooopen hello  **Мой домен** страницы. 
    
    ![Мой домен](./media/active-directory-saas-jobscience-tutorial/ic767825.png "Мой домен")

15. На hello **Мой домен** страницы в hello **фирменная символика страницы входа** щелкните **изменить**.
    
    ![Фирменная символика страницы входа](./media/active-directory-saas-jobscience-tutorial/ic767826.png "Фирменная символика страницы входа")

16. На hello **фирменная символика страницы входа** страницы в hello **службы проверки подлинности** раздела, название hello вашей **настройки единого входа SAML** отображается. Выберите его, а затем нажмите кнопку **Сохранить**.
    
    ![Фирменная символика страницы входа](./media/active-directory-saas-jobscience-tutorial/ic784366.png "Фирменная символика страницы входа")

17. tooget hello SP инициировал единый вход по URL-адрес входа щелкните hello **параметры единого входа** в hello **управления безопасностью** раздела меню.

    ![Средства управления безопасностью](./media/active-directory-saas-jobscience-tutorial/ic784368.png "Средства управления безопасностью")
    
    Выберите профиль единого входа hello, созданном в предыдущем шаге hello. На этой странице отображаются hello единым входом на URL-адрес для вашей компании (например, [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid).    

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-jobscience-test-user"></a>Создание тестового пользователя Jobscience

В порядке tooenable toolog пользователей Azure AD в tooJobscience их необходимо подготовить в Jobscience. В случае hello объекта Jobscience Подготовка осуществляется вручную.

>[!NOTE]
>Можно использовать любые другие Jobscience пользователя средства создания учетных записей или интерфейсы API, предоставляемые Jobscience tooprovision Azure Active Directory учетных записей пользователей.
>  
        
**tooconfigure подготовки пользователей, выполните следующие шаги hello.**

1. Войдите в tooyour **Jobscience** сайт компании от имени администратора.

2. Go tooSetup.
   
   ![Настройка](./media/active-directory-saas-jobscience-tutorial/ic784358.png "Настройка")
3. Go слишком**Управление пользователями \> пользователей**.
   
   ![Пользователи](./media/active-directory-saas-jobscience-tutorial/ic784369.png "Пользователи")
4. Щелкните **Новый пользователь**.
   
   ![Все пользователи](./media/active-directory-saas-jobscience-tutorial/ic784370.png "Все пользователи")
5. На hello **изменение пользователя** диалоговое окно, выполните следующие шаги hello:
   
   ![Изменение пользователя](./media/active-directory-saas-jobscience-tutorial/ic784371.png "Изменение пользователя")
   
   а. В hello **имя** текстовом поле введите имя пользователя hello как Britta.
   
   b. В hello **Фамилия** текстовом поле введите фамилию пользователя hello как Simon.
   
   c. В hello **псевдоним** текстовом поле введите имя псевдонима пользователя hello как brittas.

   d. В hello **электронной почты** в текстовое поле типа hello адрес электронной почты пользователя, например Brittasimon@contoso.com.

   д. В hello **имя пользователя** текстовое поле, введите имя пользователя, например Brittasimon@contoso.com.

   f. В hello **псевдоним** текстовом поле введите имя пользователя, например Simon ник.

   ж. Щелкните **Сохранить**.

    
> [!NOTE]
> Владелец учетной записи Azure Active Directory Hello получает сообщение электронной почты и соответствует tooconfirm ссылку свою учетную запись, чтобы она стала активной.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooJobscience доступа.

![Назначение пользователя][200] 

**tooassign tooJobscience Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Jobscience**.

    ![Настройка единого входа](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello Jobscience плитки в панели доступа hello, вы должны получить tooyour автоматически подписан на Jobscience приложения.
Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_203.png

