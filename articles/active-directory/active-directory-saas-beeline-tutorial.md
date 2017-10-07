---
title: "Руководство по интеграции Azure Active Directory с BeeLine | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и BeeLine."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0726859d-1dac-44a0-810b-da56d89039ee
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 92f228d33980c21ad934185ab89d73795f7f69bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-beeline"></a>Руководство по интеграции Azure Active Directory с Beeline

В этом учебнике вы узнаете, как toointegrate BeeLine с Azure Active Directory (Azure AD).

Интеграция с Azure AD BeeLine предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooBeeLine
- Можно включить на пользователей tooautomatically get вошедшего tooBeeLine (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с BeeLine требуется hello следующих элементов:

- подписка Azure AD;
- подписка BeeLine с активированной функцией единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление BeeLine из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-beeline-from-hello-gallery"></a>Добавление BeeLine из галереи hello
tooconfigure hello интеграции BeeLine в Azure AD, вы должны tooadd BeeLine из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd BeeLine из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **BeeLine**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_search.png)

5. В панели результатов hello выберите **BeeLine**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в BeeLine с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в BeeLine является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в BeeLine должен установить toobe.

В BeeLine, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с BeeLine, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя BeeLine](#creating-a-beeline-test-user)**  -toohave аналог Саймон Britta в BeeLine, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении BeeLine.

**tooconfigure Azure AD единого входа с BeeLine, выполните следующие шаги hello.**

1. В hello в hello портала Azure **BeeLine** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_samlbase.png)

3. На hello **URL-адреса и домена BeeLine** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_url.png)

    а. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://projects.beeline.net/<instancename>`

    b. В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:
    | |
    |--|
    | `https://projects.beeline.net/<instancename>/SSO_External.ashx`|
    | `https://projects.beeline.net/<companyname>/SSO_External.ashx` |

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновите эти значения с hello фактический идентификатор и ответ URL-адрес. Обратитесь к [BeeLine поддержки](https://www.beeline.com/contact-us/) tooget эти значения.
 
4. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_certificate.png) 

5. Приложение Beeline ожидает утверждения SAML hello в определенном формате. Можно работать с [BeeLine поддержки](https://www.beeline.com/contact-us/) первый tooidentify hello идентификатор пользователя, который будет сопоставлена с приложение hello. Также выполните рекомендации hello из [BeeLine поддержки](https://www.beeline.com/contact-us/) о hello атрибут, который хочет toouse для данного сопоставления. Вы можете управлять hello значение этого атрибута из hello **атрибуты пользователя** вкладку приложения hello. пример Hello следующий снимок экрана для этого. Здесь мы сопоставленной hello **идентификатор пользователя** утверждение со hello **userprincipalname** атрибут, который предоставляет уникальный идентификатор, который будет отправлен toohello Beeline приложения в hello каждой успешной SAML Ответ.

    ![Настройка единого входа](./media/active-directory-saas-beeline-tutorial/tutorial_attribute.png)  

6. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-beeline-tutorial/tutorial_general_400.png)

7. На hello **конфигурации BeeLine** щелкните **Настройка BeeLine** tooopen **Настройка входа** окна. Копировать hello **URL-адрес выхода** и **идентификатор сущности SAML** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_configure.png) 

8. tooconfigure единого входа на **BeeLine** стороны, необходимо загрузить hello toosend **метаданные в формате XML** и **идентификатор сущности SAML**, **URL-адрес выхода**слишком[BeeLine поддержки](https://www.beeline.com/contact-us/).

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-beeline-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-beeline-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-beeline-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-beeline-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-beeline-test-user"></a>Создание тестового пользователя BeeLine

В этом разделе описано, как создать пользователя Britta Simon в приложении Beeline. Beeline приложению все пользователи toobe hello, подготовить в приложении hello перед выполнением единого входа. Таким образом работают с hello [BeeLine поддержки](https://www.beeline.com/contact-us/) tooprovision этих пользователей в приложение hello. 

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooBeeLine доступа.

![Назначение пользователя][200] 

**tooassign tooBeeLine Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **BeeLine**.

    ![Настройка единого входа](./media/active-directory-saas-beeline-tutorial/tutorial_beeline_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello. При нажатии кнопки hello Beeline плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Beeline приложения.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-beeline-tutorial/tutorial_general_203.png

