---
title: "Руководство. Интеграция Azure Active Directory с CA PPM | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и центр сертификации в МИНУТУ."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ca9d5e71-e429-4891-8d10-3498e7210e89
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 571130f3be0529c986aa0d8a08e4172015cd0b40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ca-ppm"></a>Учебник. Интеграция Azure Active Directory с CA PPM

В этом учебнике вы узнаете, как toointegrate PPM ЦС с Azure Active Directory (Azure AD).

Интеграция PPM ЦС с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooCA в МИНУТУ
- Можно включить на пользователей tooautomatically get вошедшего tooCA PPM (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с PPM ЦС необходимо hello следующих элементов:

- подписка Azure AD;
- подписка CA PPM с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление центра сертификации в МИНУТУ из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-ca-ppm-from-hello-gallery"></a>Добавление центра сертификации в МИНУТУ из галереи hello
tooconfigure hello интеграции PPM ЦС в Azure AD, вы должны tooadd PPM ЦС из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd PPM ЦС из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **ЦС PPM**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_search.png)

5. В панели результатов hello выберите **ЦС PPM**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в CA PPM с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в PPM ЦС является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в PPM ЦС должен установить toobe.

В ЦС в МИНУТУ, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с ЦС в МИНУТУ, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя PPM ЦС](#creating-a-ca-ppm-test-user)**  -toohave аналог Саймон Britta в ЦС в МИНУТУ, представление связанных toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении PPM ЦС.

**tooconfigure Azure AD единого входа с PPM ЦС, выполните следующие шаги hello.**

1. В hello в hello портала Azure **ЦС PPM** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_samlbase.png)

3. На hello **URL-адреса и домена PPM ЦС** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_url.png)

    а. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://ca.ondemand.saml.20.post.<companyname>`
    
    b. В hello **URL-адрес ответа** текстовое поле, тип, что:`https://fedsso.ondemand.ca.com/affwebservices/public/saml2assertionconsumer`

    > [!NOTE] 
    > Это значение приведено для справки. Измените значение этого параметра hello фактический идентификатор. Обратитесь к [группа поддержки PPM ЦС](mailto:catechnicalsupport@ca.com) tooget это значение.
 
4. На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-cappm-tutorial/tutorial_general_400.png)

6. На hello **конфигурации ЦС PPM** щелкните **настройки ЦС PPM** tooopen **настройки единого входа** окна. Копировать hello **идентификатор сущности SAML** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_configure.png) 

7. tooconfigure единого входа на **ЦС PPM** стороны, необходимо загрузить hello toosend **Certificate(Base64)** и **идентификатор сущности SAML** слишком[группа поддержки PPM ЦС ](mailto:catechnicalsupport@ca.com).

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cappm-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cappm-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cappm-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cappm-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-ca-ppm-test-user"></a>Создание тестового пользователя CA PPM

В этом разделе описано, как создать пользователя Britta Simon в приложении CA PPM. Работать с [группа поддержки PPM ЦС](mailto:catechnicalsupport@ca.com) tooadd hello пользователей на платформе hello PPM ЦС.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooCA в МИНУТУ.

![Назначение пользователя][200] 

**tooassign tooCA Britta Simon PPM, выполните hello следующие шаги.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **ЦС PPM**.

    ![Настройка единого входа](./media/active-directory-saas-cappm-tutorial/tutorial_cappm_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе Проверьте конфигурацию единого входа Azure AD с помощью панели доступа hello.

При выборе плитки PPM ЦС hello в hello панели доступа, вы должны получить приложения автоматически вошедшего tooyour PPM ЦС.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cappm-tutorial/tutorial_general_203.png

