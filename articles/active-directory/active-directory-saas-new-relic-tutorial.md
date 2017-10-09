---
title: "Руководство по интеграции Azure Active Directory с New Relic | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и New Relic."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3186b9a8-f4d8-45e2-ad82-6275f95e7aa6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: dc8f0df3b18a32bde155e8911a581fc5f91af217
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-new-relic"></a>Учебник. Интеграция Azure Active Directory с New Relic

В этом учебнике вы узнаете, как toointegrate New Relic с Azure Active Directory (Azure AD).

Интеграция New Relic с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooNew Relic
- Можно включить на пользователей tooautomatically get вошедшего tooNew Relic (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с New Relic, требуется hello следующих элементов:

- подписка Azure AD;
- Подписка с поддержкой единого входа New Relic.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление New Relic из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-new-relic-from-hello-gallery"></a>Добавление New Relic из галереи hello
tooconfigure hello интеграции New Relic в Azure AD, вы должны tooadd New Relic из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd New Relic из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **New Relic**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_search.png)

5. В панели результатов hello выберите **New Relic**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описаны настройка и проверка единого входа Azure AD в приложение New Relic с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в New Relic является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в New Relic должен установить toobe.

В New Relic, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с New Relic, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя New Relic](#creating-a-new-relic-test-user)**  -toohave аналог Саймон Britta в New Relic, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложение New Relic.

**tooconfigure Azure AD единого входа с New Relic, выполните следующие шаги hello.**

1. В hello в hello портала Azure **New Relic** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_samlbase.png)

3. На hello **URL-адреса и нового домена Relic** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_url.png)

    В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.newrelic.com`

    > [!NOTE] 
    > значение Hello не является вещественным числом. Значение hello обновления с hello фактический URL-адрес входа. Обратитесь к [группа поддержки нового клиента Relic](https://support.newrelic.com/) tooget значение hello. 
 
4. На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-new-relic-tutorial/tutorial_general_400.png)

6. На hello **новую конфигурацию Relic** щелкните **Настройка New Relic** tooopen **Настройка входа** окна. Копировать hello **URL-адрес выхода и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_configure.png) 

7. В другом окне браузера, войдите на tooyour **New Relic** сайт компании от имени администратора.

8. В меню в верхней части hello hello выберите **параметры учетной записи**.
   
    ![Параметры учетной записи](./media/active-directory-saas-new-relic-tutorial/ic797036.png "параметры учетной записи")

9. Нажмите кнопку hello **безопасности и проверки подлинности** , а затем щелкните hello **единого входа** вкладки.
   
    ![Единый вход](./media/active-directory-saas-new-relic-tutorial/ic797037.png "Единый вход")

10. На странице диалогового окна SAML hello выполните следующие шаги hello.
   
    ![SAML](./media/active-directory-saas-new-relic-tutorial/ic797038.png "SAML")
   
   а. Нажмите кнопку **выбрать файл** tooupload Скачанный сертификат Azure Active Directory.

   b. В hello **URL-адрес удаленного входа** текстовое значение hello вставить **SAML единого входа URL-адрес службы**, который вы скопировали из портала Azure.
   
   c. В hello **целевой URL-адрес выхода** текстовое значение hello вставить **URL-адрес выхода**, который вы скопировали из портала Azure.

   d. Щелкните **Сохранить изменения**.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-new-relic-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-new-relic-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-new-relic-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-new-relic-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-new-relic-test-user"></a>Создание тестового пользователя New Relic

В порядке tooenable toolog пользователей Azure Active Directory в tooNew Relic их необходимо подготовить в New Relic. В случае hello объекта New Relic Подготовка выполняется вручную.

**tooprovision tooNew учетной записи пользователя Relic, выполните следующие шаги hello.**

1. Войдите в tooyour **New Relic** сайт компании от имени администратора.

2. В меню в верхней части hello hello выберите **параметры учетной записи**.
   
    ![Параметры учетной записи](./media/active-directory-saas-new-relic-tutorial/ic797040.png "параметры учетной записи")

3. В hello **учетной записи** на hello панели слева, нажмите кнопку **Сводка**, а затем нажмите кнопку **добавить пользователя**.
   
    ![Параметры учетной записи](./media/active-directory-saas-new-relic-tutorial/ic797041.png "параметры учетной записи")

4. На hello **активных пользователей** диалоговое окно, выполните следующие шаги hello:
   
    ![Активные пользователи](./media/active-directory-saas-new-relic-tutorial/ic797042.png "Активные пользователи")
   
    а. В hello **электронной почты** текстового поля, типа hello адрес электронной почты действительного пользователя Azure Active Directory требуется tooprovision.

    b. Для параметра **Role** (Роль) выберите значение **User** (Пользователь).

    c. Щелкните **Добавить этого пользователя**.

>[!NOTE]
>Можно использовать любые другие New Relic пользователя средства создания учетных записей или интерфейсы API, предоставляемые New Relic tooprovision учетных записей пользователей AAD.
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooNew Relic.

![Назначение пользователя][200] 

**tooassign Britta Simon tooNew Relic, выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **New Relic**.

    ![Настройка единого входа](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".

При нажатии кнопки hello New Relic плитки в панели доступа hello, вы должны получить приложение автоматически вошедшего tooyour New Relic.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_203.png

