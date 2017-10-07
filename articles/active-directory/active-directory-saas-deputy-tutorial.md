---
title: "Учебник. Интеграция Azure Active Directory с Deputy | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и заместителем."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5665c3ac-5689-4201-80fe-fcc677d4430d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 42f65b758682ce2513b6bb38ef40a19f955c88c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-deputy"></a>Руководство. Интеграция Azure Active Directory с Deputy

В этом учебнике вы узнаете, как toointegrate заместителем с Azure Active Directory (Azure AD).

Интеграция с Azure AD заместителем предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooDeputy
- Можно включить на пользователей tooautomatically get вошедшего tooDeputy (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с заместителем требуется hello следующих элементов:

- подписка Azure AD;
- подписка Deputy с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление заместителем из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-deputy-from-hello-gallery"></a>Добавление заместителем из галереи hello
tooconfigure hello интеграции заместителем в Azure AD, вы должны tooadd заместителем из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd заместителем из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **заместителем**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_search.png)

5. В панели результатов hello выберите **заместителем**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в приложение Deputy с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в заместителем является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в заместителем должен установить toobe.

В заместителем, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с заместителем, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя заместителем](#creating-a-deputy-test-user)**  -toohave аналог Саймон Britta в заместителем, представление связанных toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении заместителем.

**tooconfigure Azure AD единого входа с заместителем, выполните следующие шаги hello.**

1. В hello в hello портала Azure **заместителем** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_samlbase.png)

3. На hello **заместителем доменов и URL-адреса** статьи, при желании tooconfigure приложения hello в **IDP** инициировал режим:

    ![Настройка единого входа](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url1.png)

    а. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:
    |  |
    | ----|
    | `https://<subdomain>.<region>.au.deputy.com` |
    | `https://<subdomain>.<region>.ent-au.deputy.com` |
    | `https://<subdomain>.<region>.na.deputy.com`|
    | `https://<subdomain>.<region>.ent-na.deputy.com`|
    | `https://<subdomain>.<region>.eu.deputy.com` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com` |
    | `https://<subdomain>.<region>.as.deputy.com` |
    | `https://<subdomain>.<region>.ent-as.deputy.com` |
    | `https://<subdomain>.<region>.la.deputy.com` |
    | `https://<subdomain>.<region>.ent-la.deputy.com` |
    | `https://<subdomain>.<region>.af.deputy.com` |
    | `https://<subdomain>.<region>.ent-af.deputy.com` |
    | `https://<subdomain>.<region>.an.deputy.com` |
    | `https://<subdomain>.<region>.ent-an.deputy.com` |
    | `https://<subdomain>.<region>.deputy.com` |

    b. В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:
    | |
    |----|
    | `https://<subdomain>.<region>.au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.deputy.com/exec/devapp/samlacs.` |

4. Установите флажок **Показать дополнительные параметры URL-адресов**, При необходимости приложение hello tooconfigure в **SP** инициировал режим:

    ![Настройка единого входа](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url2.png)

    В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<your-subdomain>.<region>.deputy.com`
    
    >[!NOTE]
    > Суффикс региона Deputy необязательный, или следует использовать один из следующих: au | na | eu |as |la |af |an |ent-au |ent-na |ent-eu |ent-as | ent-la | ent-af | ent-an.

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновить значения hello фактический идентификатор, URL-адрес ответа и URL-адрес входа. Обратитесь к [группа поддержки заместителем](https://www.deputy.com/call-centers-customer-support-scheduling-software) tooget эти значения. 

5. На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_certificate.png) 

6. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-deputy-tutorial/tutorial_general_400.png)
    
7. На hello **конфигурации заместителем** щелкните **Настройка заместителем** tooopen **Настройка входа** окна. Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_configure.png) 

8. Перейдите на URL-адреса toohello:[https://(your-subdomain).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config). Go слишком**параметры безопасности** и нажмите кнопку **изменить**.
   
    ![Настройка единого входа](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_004.png)

9. На странице **Параметры безопасности** сделайте следующее:

    ![Настройка единого входа](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_005.png)
    
    а. разрешите **вход с помощью учетных записей социальных сетей**;
   
    b. Откройте сертификат в кодировке Base64 загружен с портала Azure в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **OpenSSL сертификат** текстового поля.
   
    c. Введите в текстовое поле URL-адрес единого входа SAML hello`https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`
    
    d. В текстовом поле URL-адрес единого входа SAML hello, замените `<your subdomain>` с дочернего домена.
   
    д. В текстовом поле URL-адрес единого входа SAML hello, замените `<saml sso url>` с hello **SAML единого входа URL-адрес службы** было скопировано из hello портал Azure.
   
    f. Нажмите кнопку **Сохранить параметры**.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-deputy-test-user"></a>Создание тестового пользователя приложения Deputy

Пользователи toolog tooenable Azure AD в tooDeputy, их необходимо подготовить в заместителем. В случае с Deputy подготовка выполняется вручную.

#### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a>tooprovision учетной записи пользователя, выполните следующие шаги hello.
1. Войдите на сайте компании заместителем tooyour в качестве администратора.

2. На верхней панели навигации панели hello выберите **людей**.
   
   ![Люди](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "Люди")

3. Щелкните hello **добавьте людей** и нажмите кнопку **добавить один человек**.
   
   ![Добавить участников](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "добавить участников")

4. Выполните следующие шаги hello и нажмите **сохранить и приглашать**.
   
   ![Новый пользователь](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "Новый пользователь")

   а. В hello **имя** в текстовое поле имя типа hello пользователя как **BrittaSimon**.
   
   b. В hello **электронной почты** текстовом поле введите адрес электронной почты hello требуется tooprovision учетной записи Azure AD.
   
   c. В hello **работать на** в текстовое поле имя бизнеса типа hello.
   
   d. Нажмите кнопку **Save & Invite** (Сохранить и пригласить).

5. Hello владельцем учетной записи AAD получит сообщение электронной почты и соответствует tooconfirm ссылку свою учетную запись, чтобы она стала активной. Можно использовать любые другие заместителем пользователя средства создания учетных записей или интерфейсы API, предоставляемые заместителем tooprovision AAD учетных записей пользователей.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooDeputy доступа.

![Назначение пользователя][200] 

**tooassign tooDeputy Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **заместителем**.

    ![Настройка единого входа](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

Цель этого раздела Hello является tootest конфигурации единого входа Azure AD с помощью панели доступа "hello".

При нажатии кнопки hello заместителем плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour заместителем приложения.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_203.png

