---
title: "Руководство по интеграции Azure Active Directory с Tableau Online | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Tableau Online."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d4b1149-ba3b-4f4e-8bce-9791316b730d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: 590b2674270c340b4750c7b6feeaf4f0df4bf853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-online"></a>Руководство. Интеграция Azure Active Directory с Tableau Online

В этом учебнике вы узнаете, как toointegrate Tableau Online с Azure Active Directory (Azure AD).

Интеграция Tableau Online с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего tooTableau доступ через Интернет
- Можно включить на пользователей tooautomatically get вошедшего tooTableau сети (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Tableau Online требуется hello следующих элементов:

- подписка Azure AD;
- подписка на Tableau Online с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Tableau Online из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-tableau-online-from-hello-gallery"></a>Добавление Tableau Online из галереи hello
tooconfigure hello интеграции Tableau сети в Azure AD, вы должны tooadd Tableau сети из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Tableau сети из галереи hello выполните hello следующие шаги.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **Tableau Online**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_search.png)

5. В панели результатов hello выберите **Tableau Online**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Tableau Online с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в документации по Tableau является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в документации по Tableau должен установить toobe.

В документации по Tableau, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и тестирования Azure AD единого входа с Tableau Online, необходимые hello toocomplete следующие стандартные блоки.

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Tableau Online](#creating-a-tableau-online-test-user)**  -toohave аналог Саймон Britta документации Tableau, представление связанных toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Tableau Online.

**tooconfigure Azure AD единого входа с Tableau Online выполните следующие шаги hello.**

1. В hello в hello портала Azure **Tableau Online** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_samlbase.png)

3. На hello **URL-адреса и домена Tableau** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_url.png)
    
    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес hello:`https://sso.online.tableau.com`

    b. В hello **идентификатор** текстовом поле введите URL-адрес hello:`https://sso.online.tableau.com/public/sp/<instancename>`

4. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-tableauonline-tutorial/tutorial_general_400.png)

6. В другом окне браузера, tooyour входа Tableau интерактивных приложений. Go слишком**параметры** и затем **проверки подлинности**.
   
    ![Настройка единого входа](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_09.png)
    
7. tooenable SAML в разделе **типы проверки подлинности** раздела. Проверьте hello **единого входа с помощью SAML** флажок.
   
    ![Настройка единого входа](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_12.png)

8. Прокрутите вниз до раздела **Import metadata file into Tableau Online** (Импорт файла метаданных в Tableau Online).  Нажмите кнопку Обзор и импортируйте файл метаданных hello, загруженный из Azure AD. Нажмите кнопку **Применить**.
   
   ![Настройка единого входа](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_13.png)

9. В hello **соответствует утверждения** статьи, вставьте соответствующее имя утверждения поставщика удостоверений hello для **адрес электронной почты**, **имя**, и **Фамилия** . tooget эту информацию из Azure AD: 
  
    а. В hello портал Azure, перейдите на hello **Tableau Online** странице интеграции приложений.
    
    b. В разделе "атрибуты" hello, выберите hello **«просмотреть и изменить все остальные атрибуты пользователя»** флажок. 
    
   ![Настройка единого входа](./media/active-directory-saas-tableauonline-tutorial/attributesection.png)
      
    c. Скопируйте значения этих атрибутов пространства имен hello: givenname, электронной почты и фамилия, используя hello следующие действия:

   ![Единый вход в Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_10.png)
    
    г) Щелкните значение **user.givenname**. 
    
    д. Скопируйте значение hello из hello **имен** текстового поля.

   ![Настройка единого входа](./media/active-directory-saas-tableauonline-tutorial/attributesection2.png)

    f. toocopy параметры имен hello hello электронной почты и фамилии выполните hello в предыдущих шагах.

    ж. Переключение toohello Tableau интерактивного приложения, а затем задайте hello **Tableau интерактивные атрибуты** следующим образом:
     * электронный адрес: **mail** или **userprincipalname**;
     * имя: **givenname**
     * фамилия: **surname**
   
   ![Настройка единого входа](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_14.png)

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-tableau-online-test-user"></a>Создание тестового пользователя Tableau Online

В этом разделе описано, как создать пользователя Britta Simon в приложении Tableau Online.

1. В приложении **Tableau Online** щелкните **Settings** (Параметры), а затем выберите раздел **Authentication** (Проверка подлинности). Прокрутите список вниз слишком**Выбор: пользователи** раздела. Щелкните **Add Users** (Добавить пользователей), а затем — **Enter Email Addresses** (Введите адреса электронной почты).
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_15.png)
2. Установите переключатель **Add users for single sign-on (SSO) authentication**(Добавить пользователей для проверки подлинности единого входа). В hello **введите адреса электронной почты** добавить текстовое полеbritta.simon@contoso.com
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_11.png)
3. Щелкните **Создать**.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooTableau доступа через Интернет.

![Назначение пользователя][200] 

**tooassign Britta Simon tooTableau через Интернет, выполнять hello следующие шаги:**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Tableau Online**.

    ![Настройка единого входа](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

Цель этого раздела Hello является tootest конфигурации единого входа Azure AD с помощью панели доступа "hello".

При нажатии кнопки hello Tableau Online плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Tableau интерактивных приложений.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_203.png

