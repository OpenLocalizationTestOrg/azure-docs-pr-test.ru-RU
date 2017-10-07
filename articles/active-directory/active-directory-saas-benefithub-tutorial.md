---
title: "Руководство по интеграции Azure Active Directory с BenefitHub | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и BenefitHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4069fe32-a452-463f-973e-7aa0baa4c2fa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: c07d6e44e8cbc79afd79c900664011b059206b56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefithub"></a>Руководство по интеграции Azure Active Directory с BenefitHub

В этом учебнике вы узнаете, как toointegrate BenefitHub с Azure Active Directory (Azure AD).

Интеграция с Azure AD BenefitHub предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooBenefitHub
- Можно включить на пользователей tooautomatically get вошедшего tooBenefitHub (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с BenefitHub требуется hello следующих элементов:

- подписка Azure AD;
- подписка BenefitHub с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление BenefitHub из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-benefithub-from-hello-gallery"></a>Добавление BenefitHub из галереи hello
tooconfigure hello интеграции BenefitHub в Azure AD, вы должны tooadd BenefitHub из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd BenefitHub из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **BenefitHub**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_search.png)

5. В панели результатов hello выберите **BenefitHub**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в BenefitHub с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в BenefitHub является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в BenefitHub должен установить toobe.

В BenefitHub, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с BenefitHub, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя BenefitHub](#creating-a-benefithub-test-user)**  -toohave аналог Саймон Britta в BenefitHub, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении BenefitHub.

**tooconfigure Azure AD единого входа с BenefitHub, выполните следующие шаги hello.**

1. В hello в hello портала Azure **BenefitHub** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_samlbase.png)

3. На hello **URL-адреса и домена BenefitHub** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_url1.png)
  
    а. В hello **идентификатор** введите:`urn:benefithub:passport`
    
    b. В hello **URL-адрес ответа** введите:`https://passport.benefithub.info/saml/post/ac`

4. Hello BenefitHub приложения ожидает утверждения SAML hello в определенном формате, требующий вы tooadd настраиваемого атрибута сопоставления tooyour атрибутов токена конфигурация SAML. Настройка следующих утверждений для этого приложения hello. Вы можете управлять hello значения этих атрибутов из hello»**атрибуты пользователя**» на странице интеграции приложения. 

    ![Настройка единого входа](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_attribute.png)

5. В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна настройки атрибутов токена SAML, как показано в hello предшествующий образ и выполнить следующие шаги hello:
    
    | Имя атрибута | Значение атрибута |
    | ------------------- | -------------------- |    
    | organizationid | < organizationid > |

    > [!NOTE]
    > Это значение атрибута приведено для примера. Введите вместо этого значения фактическое значение organizationid. Обратитесь к [BenefitHub поддержки](https://www.benefithub.com/Home/ContactUs) tooget hello фактическое organizationid.
    
    а. Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.

    ![Настройка единого входа](./media/active-directory-saas-benefithub-tutorial/tutorial_attribute_04.png)

    ![Настройка единого входа](./media/active-directory-saas-benefithub-tutorial/tutorial_attribute_05.png)

    b. В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.
    
    c. Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.
    
    d. Нажмите кнопку **ОК**.

    > [!NOTE] 
    > Перед настройкой hello утверждения SAML, необходимо toocontact вашей [BenefitHub поддержки](https://www.benefithub.com/Home/ContactUs) и запросить значение hello hello уникальный идентификатор атрибута для вашего клиента. Необходимо, чтобы это значение tooconfigure hello пользовательского утверждения для приложения.

6. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_certificate.png) 

7. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-benefithub-tutorial/tutorial_general_400.png)

8. tooconfigure единого входа на **BenefitHub** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[BenefitHub поддержки](https://www.benefithub.com/Home/ContactUs). Они устанавливаются hello toohave этот параметр задан правильно на обеих сторонах соединения единого входа SAML.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-benefithub-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-benefithub-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-benefithub-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-benefithub-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-benefithub-test-user"></a>Создание тестового пользователя BenefitHub

В этом разделе описано, как создать пользователя Britta Simon в приложении BenefitHub. Работать с [BenefitHub поддержки](https://www.benefithub.com/Home/ContactUs) для добавления пользователей hello в платформе BenefitHub hello. Перед использованием единого входа необходимо создать и активировать пользователей. 

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooBenefitHub доступа.

![Назначение пользователя][200] 

**tooassign tooBenefitHub Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **BenefitHub**.

    ![Настройка единого входа](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello BenefitHub плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour BenefitHub приложения.
Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](https://msdn.microsoft.com/library/dn308586).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_203.png

