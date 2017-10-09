---
title: "Руководство по интеграции Azure Active Directory с O.C. Tanner — AppreciateHub | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и O.C. Tanner — AppreciateHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dee8fbca-0b60-4a21-8917-1fb6919de5a0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: jeedes
ms.openlocfilehash: 45052cf56e35746d7df5910162e40e3bbcad1aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-oc-tanner---appreciatehub"></a>Руководство по интеграции Azure Active Directory с O.C. Tanner — AppreciateHub

В этом учебнике вы узнаете, как toointegrate O.C. Tanner — AppreciateHub с Azure Active Directory (Azure AD).

Интеграция O.C. Петров - AppreciateHub с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooO.C. Tanner — AppreciateHub
- Можно включить на пользователей tooautomatically get вошедшего tooO.C. Tanner — AppreciateHub (единый вход) под учетной записью Azure AD.
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

Интеграция Azure AD с O.C. tooconfigure Петров - AppreciateHub, требуется hello следующих элементов:

- подписка Azure AD;
- подписка с поддержкой единого входа O.C. подписка Tanner — AppreciateHub с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление O.C. Петров - AppreciateHub из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-oc-tanner---appreciatehub-from-hello-gallery"></a>Добавление O.C. Петров - AppreciateHub из галереи hello
Интеграция hello tooconfigure O.C. Петров - AppreciateHub в Azure AD необходимо tooadd O.C. Петров - AppreciateHub из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd O.C. Петров - AppreciateHub из галереи hello выполнения hello следующие шаги:**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **O.C. Tanner — AppreciateHub**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_search.png)

5. В панели результатов hello выберите **O.C. Петров - AppreciateHub**, а затем нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в приложение O.C. Tanner — AppreciateHub с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователя аналог hello в O.C. Петров - AppreciateHub — tooa пользователя в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в O.C. Петров - AppreciateHub должен установить toobe.

В O.C. Значение hello Петров - AppreciateHub, назначьте hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с O.C. Петров - AppreciateHub, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя O.C. Петров - тестового пользователя AppreciateHub](#creating-a-oc-tanner---appreciatehub-test-user)**  -toohave аналог Саймон Britta в O.C. Петров - AppreciateHub, связанные toohello представление пользователя Azure AD.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в вашей O.C. Tanner — AppreciateHub.

**Azure AD tooconfigure единого входа с O.C. Петров - AppreciateHub, выполните следующие шаги hello:**

1. В hello в hello портала Azure **O.C. Tanner — AppreciateHub** щелкните **Единый вход**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_samlbase.png)

3. На hello **O.C. Петров - URL-адреса и домена AppreciateHub** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_url.png)

    а. В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.appreciatehub.com/fed/sp/authnResponse20`

    > [!NOTE] 
    > Это значение приведено для справки. Измените значение этого параметра hello фактический URL-адрес ответа. Обратитесь в [службу поддержки Петров - группа поддержки AppreciateHub](mailto:sso@octanner.com) tooget это значение.

    b. Привет открыть файл метаданных, с помощью hello по ссылке: [https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata).
   
    c. Найдите hello **md:AssertionConsumerService** узла. 
   
    d. Скопируйте значение hello hello **расположение** атрибута. 
   
    ![Настройка параметров приложения][12]
   
    д. В hello **на URL-адрес входа** textbox за значением hello, полученный в предыдущем шаге hello.

4. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_400.png)

6. tooconfigure единого входа на **O.C. Петров - AppreciateHub** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[O.C. службе поддержки О.С. Tanner — AppreciateHub](mailto:sso@octanner.com).

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-oc-tanner---appreciatehub-test-user"></a>Создание тестового пользователя O.C. Tanner — AppreciateHub

Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в O.C. Tanner — AppreciateHub.

**toocreate пользователь вызвал Саймон Britta в O.C. Петров - AppreciateHub, выполните следующие шаги hello:**

Попросите [службу поддержки Петров - группа поддержки AppreciateHub](mailto:sso@octanner.com) toocreate пользователь, имеющий как hello атрибута nameID совпадает со значением в имя пользователя hello Саймон Britta в Azure AD.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooO.C доступа. Tanner — AppreciateHub.

![Назначение пользователя][200] 

**tooassign tooO.C Britta Simon. Петров - AppreciateHub, выполните следующие шаги hello:**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **O.C. Tanner — AppreciateHub**.

    ![Настройка единого входа](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".  
При нажатии кнопки hello O.C. Петров - AppreciateHub плитки в Здравствуйте панели доступа, вы должны получить автоматически подписан на tooyour O.C. Tanner — AppreciateHub.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_04.png

[12]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_08.png

[100]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_203.png

