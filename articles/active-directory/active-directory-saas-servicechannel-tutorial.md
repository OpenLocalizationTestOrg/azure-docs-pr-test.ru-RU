---
title: "Руководство по интеграции Azure Active Directory с ServiceChannel | Документы Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и ServiceChannel."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c3546eab-96b5-489b-a309-b895eb428053
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/3/2017
ms.author: jeedes
ms.openlocfilehash: 956371a1e99dcba4137c271ecfe8a62b9ec64a99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicechannel"></a>Руководство: интеграция Azure Active Directory с ServiceChannel

В этом учебнике вы узнаете, как toointegrate ServiceChannel с Azure Active Directory (Azure AD).

Интеграция с Azure AD ServiceChannel предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooServiceChannel
- Можно включить на пользователей tooautomatically get вошедшего tooServiceChannel (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал управления Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с ServiceChannel требуется hello следующих элементов:

- подписка Azure AD;
- подписка ServiceChannel с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не следует использовать рабочую среду при отсутствии необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление ServiceChannel из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-servicechannel-from-hello-gallery"></a>Добавление ServiceChannel из галереи hello
tooconfigure hello интеграции ServiceChannel в Azure AD, вы должны tooadd ServiceChannel из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd ServiceChannel из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портала управления Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. Нажмите кнопку **добавить** кнопку в верхней части hello диалогового окна "hello".

    ![Приложения][3]

4. Введите в поле поиска hello **ServiceChannel**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_000.png)

5. В панели результатов hello выберите **ServiceChannel**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_2.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в ServiceChannel с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в ServiceChannel является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в ServiceChannel должен установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в ServiceChannel.

tooconfigure и теста Azure AD единого входа с ServiceChannel, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя ServiceChannel](#creating-a-servicechannel-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал управления Azure hello и настройки единого входа в приложении ServiceChannel.

**tooconfigure Azure AD единого входа с ServiceChannel, выполните следующие шаги hello.**

1. На портале управления Azure hello на hello **ServiceChannel** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна, как **режим** выберите **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_01.png)

3. На hello **URL-адреса и домена ServiceChannel** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_urls.png)

    а. В hello **идентификатор** текстовое поле, значение типа hello как:`http://adfs.<domain>.com/adfs/service/trust`

    b. В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<customer domain>.servicechannel.com/saml/acs`

    > [!NOTE] 
    > Обратите внимание на то, что они не hello реальные значения. У вас tooupdate эти значения с hello фактический идентификатор и ответ URL-адрес. Здесь мы предлагаем вам toouse hello уникальное значение строки в hello идентификатор. Обратитесь к [ServiceChannel поддержки](https://servicechannel.zendesk.com/hc/en-us) tooget эти значения.

4. Приложение ServiceChannel ожидает утверждения SAML hello в определенном формате, требующий вы tooadd настраиваемого атрибута сопоставления tooyour атрибутов токена конфигурация SAML. пример Hello следующий снимок экрана для этого. **NameIdentifier (идентификатор пользователя)** hello только обязательные утверждение и значение по умолчанию hello — **user.userprincipalname** , но ServiceChannel ожидает этот toobe, сопоставленный с **user.mail**. При планировании подготовки пользователей tooenable только в момент времени, то необходимо добавить hello после утверждения, как показано ниже. **Роль** утверждения должен сопоставить слишком toobe**user.assignedroles** , содержащее роли hello hello.  

    Дополнительные инструкции по работе с утверждениями можно найти в руководстве по ServiceChannel [здесь](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example).
    
    ![Настройка единого входа](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_attribute.png)

    > [!NOTE] 
    > Нажмите кнопку [здесь](http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/) tooknow как tooconfigure **роли** в Azure AD

5. В **атрибуты пользователя** щелкните **представление и редактировать все остальные атрибуты пользователя** и задавать атрибуты hello.

    | Имя атрибута | Значение атрибута |
    | --- | --- |    
    | Роль| user.assignedroles |

    а. Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.

    ![Настройка единого входа](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_04.png)

    ![Настройка единого входа](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_05.png)
    
    b. В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.
    
    c. Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.
    
    d. Нажмите кнопку **ОК**.
    
6. На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_05.png) 

7. Щелкните **Сохранить**.

    ![Настройка единого входа](./media/active-directory-saas-servicechannel-tutorial/tutorial_general_400.png)

8. На hello **конфигурации ServiceChannel** щелкните **Настройка ServiceChannel** tooopen **Настройка входа** окна. Обратите внимание, hello **идентификатор SAML Enitity** из hello **краткий справочник** раздела.

9. tooconfigure единого входа на **ServiceChannel** стороны, необходимо загрузить hello toosend **сертификата (Base64)** и **идентификатор сущности SAML** слишком[ Группа поддержки ServiceChannel](https://servicechannel.zendesk.com/hc/en-us). Они будут устанавливается в порядке toohave hello правильно настроенной на обеих сторонах соединения единого входа SAML.

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя на портале управления Azure hello, вызывается Саймон Britta.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал управления Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_01.png) 

2. Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_02.png) 

3. Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**. 

### <a name="creating-a-servicechannel-test-user"></a>Создание тестового пользователя ServiceChannel

В время подготовки пользователей и после проверки подлинности пользователей в приложении hello автоматически создаются непосредственно поддерживает приложение. Для настройки полной подготовки пользователей обратитесь в [службу поддержки ServiceChannel](https://servicechannel.zendesk.com/hc/en-us).

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления ее tooServiceChannel доступа.

![Назначение пользователя][200] 

**tooassign tooServiceChannel Britta Simon выполните следующие шаги hello.**

1. На портале управления Azure hello, открыть представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **ServiceChannel**.

    ![Настройка единого входа](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_app01.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello ServiceChannel плитки в панели доступа hello, вы должны получить приложение автоматически вошедшего tooyour ServiceChannel.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_203.png