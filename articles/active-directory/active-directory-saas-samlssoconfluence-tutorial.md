---
title: "Руководство по интеграции Azure Active Directory с SAML SSO for Confluence by resolution GmbH | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и единого входа SAML для является точка пересечения постановлением GmbH."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6b47d483-d3a3-442d-b123-171e3f0f7486
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: fe50636709857ec49023e24bdc8c6cd8c58e3c7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-confluence-by-resolution-gmbh"></a>Руководство по интеграции Azure Active Directory с SAML SSO for Confluence by resolution GmbH

В этом учебнике вы узнаете, как toointegrate единого входа SAML для является точка пересечения постановлением GmbH с Azure Active Directory (Azure AD).

Интеграция единого входа SAML для является точка пересечения постановлением GmbH с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooSAML единого входа для является точка пересечения постановлением GmbH
- Можно включить на пользователей tooautomatically get вошедшего tooSAML единого входа для является точка пересечения, разрешение GmbH (Single Sign-On) с использованием их учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с помощью единого входа SAML для является точка пересечения постановлением GmbH требуется hello следующих элементов:

- подписка Azure AD;
- подписка SAML SSO for Confluence by resolution GmbH с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление единого входа SAML для является точка пересечения с разрешением GmbH из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-saml-sso-for-confluence-by-resolution-gmbh-from-hello-gallery"></a>Добавление единого входа SAML для является точка пересечения с разрешением GmbH из галереи hello

tooconfigure hello интеграции единого входа SAML для является точка пересечения постановлением GmbH в Azure AD, необходима tooadd единого входа SAML является точка пересечения постановлением GmbH из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd единого входа SAML для является точка пересечения постановлением GmbH из галереи hello выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **единого входа SAML для является точка пересечения постановлением GmbH**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_search.png)

5. В панели результатов hello выберите **единого входа SAML для является точка пересечения постановлением GmbH**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD

В этом разделе описана настройка и проверка единого входа Azure AD в SAML SSO for Confluence by resolution GmbH с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow какой аналог hello пользователь в единый вход SAML для является точка пересечения постановлением GmbH является tooa пользователем в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в единый вход SAML для является точка пересечения для разрешения GmbH должен установить toobe.

В единый вход SAML для является точка пересечения постановлением GmbH, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и выполнить проверку Azure AD единого входа с помощью единого входа SAML является точка пересечения методом GmbH разрешения, необходимые hello toocomplete следующие стандартные блоки.

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание единого входа SAML для является точка пересечения теста пользователем разрешение GmbH](#creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user)**  -toohave аналог Саймон Britta в единый вход SAML для является точка пересечения постановлением GmbH, представление связанных toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в вашей SAML SSO является точка пересечения постановлением GmbH приложения.

**tooconfigure Azure AD единого входа с помощью единого входа SAML для является точка пересечения постановлением GmbH, выполните следующие шаги hello.**

1. В hello в hello портала Azure **единого входа SAML для является точка пересечения постановлением GmbH** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_samlbase.png)

3. На hello **единого входа SAML является точка пересечения постановлением GmbH доменов и URL-адреса** статьи, при желании tooconfigure приложения hello в **IDP** инициировал режим:

    ![Настройка единого входа](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_url_1.png)

    а. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<server-base-url>/plugins/servlet/samlsso`

    b. В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<server-base-url>/plugins/servlet/samlsso`

4. Установите флажок **Показать дополнительные параметры URL-адресов**, При необходимости приложение hello tooconfigure в **SP** инициировал режим:

    ![Настройка единого входа](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_url_2.png)

    В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<server-base-url>/plugins/servlet/samlsso`
     
    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновить значения hello фактический идентификатор, URL-адрес ответа и URL-адрес входа. Обратитесь к [поддержки единого входа SAML для является точка пересечения постановлением GmbH клиента](https://www.resolution.de/go/support) tooget эти значения. 

5. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_certificate.png) 

6. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_400.png)  
    
7. В другом окне браузера, войдите в tooyour **единого входа SAML для является точка пересечения с портала администрирования GmbH разрешение** с правами администратора.

8. Наведите указатель мыши на шестеренки и выберите hello **надстройки**.
    
    ![Настройка единого входа](./media/active-directory-saas-samlssoconfluence-tutorial/addon1.png)

9. Все страницы перенаправленный tooAdministrator доступа. Введите пароль hello и нажмите кнопку **Подтверждение** кнопки.

    ![Настройка единого входа](./media/active-directory-saas-samlssoconfluence-tutorial/addon2.png)

10. В разделе **ATLASSIAN MARKETPLACE** щелкните **Find new add-ons** (Найти новые надстройки). 

    ![Настройка единого входа](./media/active-directory-saas-samlssoconfluence-tutorial/addon.png)

11. Поиск **SAML единого входа (SSO) для является точка пересечения** и нажмите кнопку **установить** tooinstall кнопку hello нового подключаемого модуля SAML.

    ![Настройка единого входа](./media/active-directory-saas-samlssoconfluence-tutorial/addon7.png)

12. Установка подключаемого модуля Hello начнется. Нажмите кнопку **Закрыть**

    ![Настройка единого входа](./media/active-directory-saas-samlssoconfluence-tutorial/addon8.png)

    ![Настройка единого входа](./media/active-directory-saas-samlssoconfluence-tutorial/addon9.png)

13. Нажмите кнопку **Управление**.

    ![Настройка единого входа](./media/active-directory-saas-samlssoconfluence-tutorial/addon10.png)
    
14. Нажмите кнопку **Настройка** tooconfigure hello нового подключаемого модуля.

    ![Настройка единого входа](./media/active-directory-saas-samlssoconfluence-tutorial/addon11.png)

15. Этот новый подключаемый модуль можно также найти на вкладке **USERS & SECURITY** (Пользователи и безопасность).

    ![Настройка единого входа](./media/active-directory-saas-samlssoconfluence-tutorial/addon3.png)
    
16. На **конфигурации подключаемый модуль единого входа SAML** щелкните **Добавление дополнительного поставщика удостоверений** кнопку tooconfigure hello параметры поставщика удостоверений.

    ![Настройка единого входа](./media/active-directory-saas-samlssoconfluence-tutorial/addon4.png)

17. На этой странице сделайте следующее.

    ![Настройка единого входа](./media/active-directory-saas-samlssoconfluence-tutorial/addon5.png)
 
    а. Добавить **имя** из hello поставщика удостоверений (например, Azure AD).
    
    b. Добавить **описание** из hello поставщика удостоверений (например, Azure AD).

    c. Нажмите кнопку **XML** и выберите hello **метаданные** файл, загруженный с портала Azure.

    d. Нажмите кнопку **Load** (Загрузить).

    д. Считывает метаданные поставщика удостоверений hello и заполняет поля hello, как показано на снимке экрана приветствия.   
18. Нажмите кнопку **сохранить параметры** кнопку Параметры toosave hello.

    ![Настройка единого входа](./media/active-directory-saas-samlssoconfluence-tutorial/addon6.png)

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-samlssoconfluence-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-saml-sso-for-confluence-by-resolution-gmbh-test-user"></a>Создание тестового пользователя SAML SSO for Confluence by resolution GmbH

Пользователи toolog tooenable Azure AD в tooSAML единого входа для является точка пересечения постановлением GmbH, их необходимо подготовить в единый вход SAML для является точка пересечения постановлением GmbH.  
Подготовка в SAML SSO for Confluence by resolution GmbH выполняется вручную.

**tooprovision учетной записи пользователя, выполните следующие шаги hello.**

1. Войдите в tooyour единого входа SAML для является точка пересечения с разрешением GmbH корпоративный сайт с правами администратора.

2. Наведите указатель мыши на шестеренки и выберите hello **Управление пользователями**.

    ![Добавление сотрудника](./media/active-directory-saas-samlssoconfluence-tutorial/user1.png) 

3. В разделе "Users" (Пользователи) выберите вкладку **Add users** (Добавление пользователей). На hello **«Добавить пользователя»** диалогового окна выполните следующие шаги hello:

    ![Добавление сотрудника](./media/active-directory-saas-samlssoconfluence-tutorial/user2.png) 

    а. В hello **Username** текстовое поле, адреса электронной почты пользователя, например Саймон Britta для hello типа.

    b. В hello **полное имя** текстового поля, типа hello полное имя пользователя как Саймон Britta.

    c. В hello **электронной почты** в текстовое поле типа hello адрес электронной почты пользователя, например Brittasimon@contoso.com.

    d. В hello **пароль** текстового поля, типа hello пароль для Саймон Britta.

    д. Нажмите кнопку **подтверждение пароля** вводить пароль hello.
    
    f. Нажмите кнопку **Добавить**.    

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooSAML единого входа для является точка пересечения постановлением GmbH.

![Назначение пользователя][200] 

**tooassign tooSAML Britta Simon единого входа для является точка пересечения постановлением GmbH, выполните hello следующие шаги.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **единого входа SAML для является точка пересечения постановлением GmbH**.

    ![Настройка единого входа](./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_samlssoconfluence_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello единого входа SAML для является точка пересечения, разрешение GmbH плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour единого входа SAML для является точка пересечения постановлением GmbH приложения.
Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samlssoconfluence-tutorial/tutorial_general_203.png

