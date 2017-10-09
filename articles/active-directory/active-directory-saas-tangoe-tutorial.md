---
title: "Руководство по интеграции Azure Active Directory с Tangoe Command Premium Mobile | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Tangoe команда Premium Mobile."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2b0b544c-9c2c-49cd-862b-ec2ee9330126
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 7bd1cd6afade58a4a47a173b249f92eb84e42112
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tangoe-command-premium-mobile"></a>Учебник. Интеграция Azure Active Directory с Tangoe Command Premium Mobile

В этом учебнике вы узнаете, как toointegrate Tangoe команда Premium мобильные приложения с помощью Azure Active Directory (Azure AD).

Интеграция с Azure AD Premium Mobile Tangoe команда предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooTangoe Mobile Premium команды
- Ваш пользователей tooautomatically get вошедшего tooTangoe Mobile Premium команды (Single Sign-On) можно включить с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Mobile Premium команда Tangoe требуется hello следующих элементов:

- подписка Azure AD;
- подписка Tangoe Command Premium Mobile с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление мобильных Premium Tangoe команды из коллекции hello
2. Настройка и проверка единого входа в Azure AD

## <a name="add-tangoe-command-premium-mobile-from-hello-gallery"></a>Добавление мобильных Premium Tangoe команды из коллекции hello
tooconfigure hello интеграции Mobile Premium Tangoe команды в Azure AD, вы должны tooadd Mobile Premium Tangoe команды из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Tangoe Mobile Premium команды из галереи hello выполните hello следующие шаги.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **Tangoe команда Premium Mobile**выберите **Mobile Premium команда Tangoe** из панели «результат» нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Добавление Tangoe Command Premium Mobile из коллекции ](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Tangoe Command Premium Mobile с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Tangoe команда Premium Mobile является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в Tangoe команда Premium Mobile должен установить toobe.

В мобильных Premium Tangoe команды, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и тестирования Azure AD единого входа с Mobile Premium Tangoe команды, необходимые hello toocomplete следующие стандартные блоки.

1. **[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Mobile Premium команда Tangoe](#create-a-tangoe-command-premium-mobile-test-user)**  -toohave аналог Саймон Britta в Tangoe команда Premium Mobile, представление связанных toohello Azure AD пользователя.
4. **[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Tangoe команда Premium Mobile.

**tooconfigure Azure AD единого входа с мобильных устройств Tangoe команда Premium, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Mobile Premium команда Tangoe** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Параметр "Вход на основе SAML"](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_samlbase.png)

3. На hello **Tangoe команда Premium Mobile домена и URL-адреса** выполните следующие шаги hello:

    ![Домены и URL-адреса приложения Tangoe Command Premium Mobile](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=<tenant issuer>&TARGET=<target page url>`

    b. В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://sso.tangoe.com/sp/ACS.saml2`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновите эти значения с hello фактический URL-адрес ответа и URL-адрес входа. Обратитесь к [Tangoe команда Premium мобильного клиента поддержки](https://www.tangoe.com/contact-2/) tooget эти значения. 

4. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.

    ![Раздел "Сертификат подписи SAML"](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Кнопка "Сохранить"](./media/active-directory-saas-tangoe-tutorial/tutorial_general_400.png)
    
6. На hello **конфигурация мобильных Premium команда Tangoe** щелкните **Настройка Mobile Premium Tangoe команда** tooopen **Настройка входа** окна. Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Раздел настройки Tangoe Command Premium Mobile](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_configure.png) 

7. tooget SSO настроен для вашего приложения, обратитесь в службу вашей [группа поддержки Tangoe команда Premium мобильного клиента](https://www.tangoe.com/contact-2/) и предоставляют hello следующее:

   - Hello скачанный файл метаданных
   - Hello **SAML идентификатор сущности**
   - Hello **SAML единого входа URL-адрес службы**
   - Hello **URL-адрес выхода**

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tangoe-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Выберите "Пользователи и группы" > "Все пользователи".](./media/active-directory-saas-tangoe-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Добавить пользователя](./media/active-directory-saas-tangoe-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-tangoe-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="create-a-tangoe-command-premium-mobile-test-user"></a>Создание тестового пользователя Tangoe Command Premium Mobile

В этом разделе мы создадим пользователя Britta Simon в приложении Tangoe Command Premium Mobile. 

Mobile Premium команда Tangoe приложению все пользователи toobe hello, подготовить в приложении hello перед выполнением единого входа. Так что произведите работы с hello [Tangoe команда Premium мобильного клиента поддержки](https://www.tangoe.com/contact-2/) tooprovision этих пользователей в приложение hello. 

### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooTangoe Mobile Premium команды.

![Назначение пользователя][200] 

**tooassign tooTangoe Britta Simon команда мобильных Premium, выполните hello следующие шаги.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Mobile Premium команды Tangoe**.

    ![Tangoe Command Premium Mobile в списке приложений](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

В этом разделе Проверьте конфигурацию единого входа Azure AD с помощью панели доступа hello.

Если щелкнуть плитку Tangoe команда Premium Mobile hello в hello панели доступа, следует получать автоматически вошедшего tooyour Tangoe команда Premium мобильного приложения. Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_203.png

