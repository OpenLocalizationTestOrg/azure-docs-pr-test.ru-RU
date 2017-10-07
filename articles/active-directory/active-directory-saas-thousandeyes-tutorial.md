---
title: "Руководство по интеграции Azure Active Directory с ThousandEyes | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и ThousandEyes."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 790e3f1e-1591-4dd6-87df-590b7bf8b4ba
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: jeedes
ms.openlocfilehash: fbfbfb71809355b1b138762757a851907737730b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thousandeyes"></a>Учебник. Интеграция Azure Active Directory с ThousandEyes

В этом учебнике вы узнаете, как toointegrate ThousandEyes с Azure Active Directory (Azure AD).

Интеграция ThousandEyes с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooThousandEyes
- Можно включить на пользователей tooautomatically get вошедшего tooThousandEyes (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с ThousandEyes требуется hello следующих элементов:

- подписка Azure AD;
- подписка ThousandEyes с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление ThousandEyes из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-thousandeyes-from-hello-gallery"></a>Добавление ThousandEyes из галереи hello
tooconfigure hello интеграции ThousandEyes в Azure AD, вы должны tooadd ThousandEyes из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd ThousandEyes из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **ThousandEyes**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_search.png)

5. В панели результатов hello выберите **ThousandEyes**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в ThousandEyes с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в ThousandEyes является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в ThousandEyes должен установить toobe.

В ThousandEyes, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с ThousandEyes, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя ThousandEyes](#creating-a-thousandeyes-test-user)**  -toohave аналог Саймон Britta в ThousandEyes, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложение ThousandEyes.

**Azure AD tooconfigure единого входа с ThousandEyes, выполните следующие шаги hello.**

1. В hello в hello портала Azure **ThousandEyes** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_samlbase.png)

3. На hello **URL-адреса и домена ThousandEyes** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_url.png)

    В hello **URL-адрес входа** текстовом поле введите URL-адрес как:`https://app.thousandeyes.com/login/sso`

4. На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_400.png)

6. На hello **конфигурации ThousandEyes** щелкните **Настройка ThousandEyes** tooopen **Настройка входа** окна. Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_configure.png) 

7. В другом окне браузера, войдите на tooyour **ThousandEyes** сайт компании от имени администратора.

8. В меню в верхней части hello hello выберите **параметры**.
   
    ![Параметры](./media/active-directory-saas-thousandeyes-tutorial/ic790066.png "Параметры")

9. В нижней части страницы нажмите кнопку **Учетная запись**
   
    ![Учетная запись](./media/active-directory-saas-thousandeyes-tutorial/ic790067.png "Учетная запись")

10. Нажмите кнопку hello **безопасность и аутентификация** вкладки.
   
    ![Безопасность и проверка подлинности](./media/active-directory-saas-thousandeyes-tutorial/ic790068.png "Безопасность и проверка подлинности")

11. В hello **настройки единого входа** выполните следующие шаги hello:
   
    ![Настройка единого входа](./media/active-directory-saas-thousandeyes-tutorial/ic790069.png "Настройка единого входа")
  
    а. Выберите пункт **Включить единый вход**.
  
    b. В текстовое поле **Login Page URL** (URL-адрес страницы входа) вставьте значение **SAML Single Sign-On Service URL** (URL-адрес службы единого входа SAML), скопированное на портале Azure.
  
    c. В текстовое поле **Logout Page URL** (URL-адрес выхода) вставьте значение **URL-адрес выхода**, скопированное на портале Azure.
  
    г) В текстовое поле **Identity Provider Issuer** (Издатель поставщика удостоверений) вставьте значение **SAML Entity ID** (Идентификатор сущности SAML), скопированное на портале Azure.
  
    д. В **сертификат проверки**, нажмите кнопку **выбрать файл**, а затем отправьте hello сертификат, загруженный с портала Azure.
  
    f. Щелкните **Сохранить**.
 
> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-thousandeyes-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-thousandeyes-test-user"></a>Создание тестового пользователя ThousandEyes

В порядке tooenable toolog пользователей Azure AD в ThousandEyes их необходимо подготовить в ThousandEyes.  
В случае hello объекта ThousandEyes Подготовка выполняется вручную.

>[!NOTE]
>Можно использовать любые другие ThousandEyes пользователя средства создания учетных записей или интерфейсы API, предоставляемые ThousandEyes tooprovision Azure Active Directory учетных записей пользователей.

**tooprovision tooThousandEyes учетной записи пользователя, выполните следующие шаги hello.**

1. Войдите на свой корпоративный веб-сайт ThousandEyes в качестве администратора.

2. Щелкните **Параметры**.
   
    ![Параметры](./media/active-directory-saas-thousandeyes-tutorial/IC790066.png "Параметры")

3. Выберите раздел **Учетная запись**.
   
    ![Учетная запись](./media/active-directory-saas-thousandeyes-tutorial/IC790067.png "Учетная запись")

4. Нажмите кнопку hello **учетные записи и пользователи** вкладки.
   
    ![Учетные записи и пользователи](./media/active-directory-saas-thousandeyes-tutorial/IC790073.png "Учетные записи и пользователи")

5. В hello **Добавление пользователей и учетных записей** выполните следующие шаги hello:
   
    ![Добавление учетных записей пользователей](./media/active-directory-saas-thousandeyes-tutorial/IC790074.png "Добавление учетных записей пользователей")   
  
    а. В **имя** в текстовое поле имя пользователя как типа hello **Britta Simon**.

    b. В **электронной почты** электронной почты hello тип пользователя в текстовое поле, например  **brittasimon@contoso.com** .
   
    b. Нажмите кнопку **tooAccount добавить пользователя**.
      
     >[!NOTE]
     >Владелец учетной записи Azure Active Directory Hello будет отправлено электронное tooconfirm ссылку и активации учетной записи hello.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooThousandEyes доступа.

![Назначение пользователя][200] 

**tooassign tooThousandEyes Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **ThousandEyes**.

    ![Настройка единого входа](./media/active-directory-saas-thousandeyes-tutorial/tutorial_thousandeyes_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки ThousandEyes плитки в панели доступа hello приветствия, вы должны получить tooyour автоматически подписан в приложение ThousandEyes.

Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thousandeyes-tutorial/tutorial_general_203.png

