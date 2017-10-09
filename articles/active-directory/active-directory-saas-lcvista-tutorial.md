---
title: "Руководство. Интеграция Azure Active Directory с LCVista | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и LCVista."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8db80d6e-3275-419f-aa39-6115a7bc9800
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: jeedes
ms.openlocfilehash: 5a4c7eb7d54b8b68c8241a97b9e516a3f6e55c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lcvista"></a>Руководство. Интеграция Azure Active Directory с LCVista

В этом учебнике вы узнаете, как toointegrate LCVista с Azure Active Directory (Azure AD).

Интеграция с Azure AD LCVista предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooLCVista
- Можно включить на пользователей tooautomatically get вошедшего tooLCVista (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с LCVista требуется hello следующих элементов:

- подписка Azure AD;
- подписка LCVista с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление LCVista из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-lcvista-from-hello-gallery"></a>Добавление LCVista из галереи hello
tooconfigure hello интеграции LCVista в Azure AD, вы должны tooadd LCVista из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd LCVista из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **LCVista**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_search.png)

5. В панели результатов hello выберите **LCVista**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в LCVista с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в LCVista является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в LCVista должен установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в LCVista.

tooconfigure и теста Azure AD единого входа с LCVista, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя LCVista](#creating-a-lcvista-test-user)**  -toohave аналог Саймон Britta в LCVista, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении LCVista.

**tooconfigure Azure AD единого входа с LCVista, выполните следующие шаги hello.**

1. В hello в hello портала Azure **LCVista** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_samlbase.png)

3. На hello **URL-адреса и домена LCVista** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.lcvista.com/rainier/login`

    b. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.lcvista.com` 
     
    > [!NOTE] 
    > Эти значения не являются реальными hello. Обновить значения hello фактический идентификатор и URL-адрес входа. Обратитесь к [группа поддержки клиента LCVista](https://lcvista.com/contact) tooget эти значения. 

4. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-lcvista-tutorial/tutorial_general_400.png)
    
6. На hello **конфигурации LCVista** щелкните **Настройка LCVista** tooopen **Настройка входа** окна. Копировать hello **идентификатор сущности SAML** и **SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_configure.png) 

7.  Войдите на tooyour LCVista приложения от имени администратора.

8. В hello **конфигурации SAML** статьи, проверьте hello **входа включить SAML** и введите сведения о hello, как упоминалось в под изображением. 

    ![Настройка единого входа](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_config.png)

    а. Вставить hello **URL-адрес издателя** скопирован из Azure AD в hello **идентификатор сущности** раздела. 

    b. Вставить hello **единого входа URL-адрес службы** скопирован из Azure AD в hello **URL-адрес** раздела.

    c. Из метаданных (XML) которого загруженный с портала Azure скопируйте значение hello **X509Certificate** и вставьте его в hello **x509 сертификатов** раздела.

    d. В hello **атрибут имени** текстовое значение hello вставить `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.

    д. В hello **атрибут фамилии** текстовое значение hello вставить `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.

    f. В hello **атрибут адреса электронной почты** текстовое значение hello вставить `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.

    ж. В hello **атрибута Username** текстовое значение hello вставить `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.

    д. Нажмите кнопку **Сохранить** toosave hello параметры.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lcvista-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lcvista-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lcvista-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-lcvista-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-lcvista-test-user"></a>Создание тестового пользователя LCVista

В этом разделе описано, как создать пользователя Britta Simon в LCVista. Требуется toocontact [группа поддержки клиента LCVista](https://lcvista.com/contact) tooadd пользователей hello в hello LCVista приложения. 

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooLCVista доступа.

![Назначение пользователя][200] 

**tooassign tooLCVista Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **LCVista**.

    ![Настройка единого входа](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello. Щелкните плитку LCVista hello в hello панели доступа, могут быть перенаправлены на страницу входа tooOrganization. После успешного входа будет подписан на tooyour LCVista приложения. Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](https://msdn.microsoft.com/library/dn308586).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_203.png

