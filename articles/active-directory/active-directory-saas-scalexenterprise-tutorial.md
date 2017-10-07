---
title: "Руководство по интеграции Azure Active Directory с ScaleX Enterprise | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и ScaleX Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2379a8d-a659-45f1-87db-9ba156d83183
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: e398b98d9e0957b5f92c82359651c345d22c3a54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scalex-enterprise"></a>Руководство по интеграции Azure Active Directory с ScaleX Enterprise

В этом учебнике вы узнаете, как toointegrate ScaleX предприятия в Azure Active Directory (Azure AD).

Интеграция ScaleX предприятия с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooScaleX предприятия
- Можно включить на пользователей tooautomatically get вошедшего tooScaleX предприятия (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если необходимо, чтобы tooknow см. Дополнительные сведения об интеграции приложений SaaS в Azure AD. [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с ScaleX Enterprise требуется hello следующих элементов:

- подписка Azure AD;
- подписка ScaleX Enterprise с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление ScaleX Enterprise из коллекции hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-scalex-enterprise-from-hello-gallery"></a>Добавление ScaleX Enterprise из коллекции hello
tooconfigure hello интеграции ScaleX Enterprise в tooAzure AD, вы должны tooadd ScaleX Enterprise из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd ScaleX Enterprise из галереи hello выполните hello следующие шаги.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. Нажмите кнопку **добавить** кнопку в верхней части hello диалогового окна "hello".

    ![Приложения][3]

4. Введите в поле поиска hello **ScaleX Enterprise**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_search.png)

5. В панели результатов hello, выберите **ScaleX Enterprise**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в ScaleX Enterprise с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello ScaleX предприятии является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello ScaleX предприятия должен установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** ScaleX предприятия.

tooconfigure и теста Azure AD единого входа с ScaleX Enterprise, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя ScaleX Enterprise](#creating-a-scalex-enterprise-test-user)**  -toohave аналог Саймон Britta ScaleX предприятии, которая является представлением связанного toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении ScaleX предприятия.

**tooconfigure Azure AD единого входа с помощью ScaleX Enterprise выполните следующие шаги hello.**

1. В hello в hello портала Azure **ScaleX Enterprise** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна, как **режим** выберите **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_samlbase.png)

3. На hello **ScaleX домена предприятия и URL-адреса** выполните hello, выполните действия, при желании tooconfigure приложения hello в **IDP** инициировал режим:

    ![Настройка единого входа](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url1.png)

    а. В hello **идентификатор** текстовое значение hello типа, используя следующий шаблон hello:`https://platform.rescale.com/saml2/<company id>/`

    b. В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://platform.rescale.com/saml2/<company id>/acs/`

4. Проверьте **Показывать дополнительные параметры URL-адреса**, если нужно, чтобы приложение hello tooconfigure в **SP** инициировал режим:

    ![Настройка единого входа](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_url2.png)

    В hello **URL-адрес входа** текстовое значение hello типа, используя следующий шаблон hello:`https://platform.rescale.com/saml2/<company id>/sso/`
     
    > [!NOTE] 
    > Они не hello реальные значения. Обновите эти значения с hello фактический идентификатор, URL-адрес ответа или URL-адрес входа. Обратитесь к [группа поддержки ScaleX корпоративный клиент](http://info.rescale.com/contact_sales) tooget эти значения. 

5. Приложение ScaleX ожидает утверждения SAML hello в определенном формате, требующий вы toomodify настраиваемого атрибута сопоставления tooyour атрибутов токена конфигурация SAML. Нажмите кнопку **представление и редактировать все остальные атрибуты пользователя** флажок tooopen hello пользовательские атрибуты параметров.

    ![Настройка единого входа](./media/active-directory-saas-scalexenterprise-tutorial/scalex_attributes.png)
    
    а. Щелкните правой кнопкой мыши атрибут hello **имя** и нажмите кнопку Удалить.

    ![Настройка единого входа](./media/active-directory-saas-scalexenterprise-tutorial/delete_attribute_name.png)

    b. Нажмите кнопку **emailaddress** атрибута tooopen hello изменение атрибута окна. Измените его значение с **user.mail** слишком**user.userprincipalname** и нажмите кнопку ОК.

    ![Настройка единого входа](./media/active-directory-saas-scalexenterprise-tutorial/edit_email_attribute.png)   
    
5. На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_certificate.png) 

6. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_400.png)
    
7. На hello **конфигурация предприятия ScaleX** щелкните **настроить корпоративный ScaleX** tooopen **Настройка входа** окна. Копировать hello **идентификатор сущности SAML** и **SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_configure.png) 

8. tooconfigure единого входа на **ScaleX Enterprise** стороны, toohello веб-сайт корпоративного ScaleX компании от имени администратора имени входа.

9. Щелкните меню hello в верхнем hello справа и выберите **администрирования Contoso**.

    > [!NOTE] 
    > Contoso является лишь примером. Используйте фактическое название компании. 

    ![Настройка единого входа](./media/active-directory-saas-scalexenterprise-tutorial/Test_Admin.png) 

10. Выберите **интеграции** из hello верхнем меню и выберите **Single Sign-On**.

    ![Настройка единого входа](./media/active-directory-saas-scalexenterprise-tutorial/admin_sso.png) 

11. Заполните форму hello следующим образом.

    ![Настройка единого входа](./media/active-directory-saas-scalexenterprise-tutorial/scalex_admin_save.png) 
    
    а. Выберите **Create any user who can authenticate with SSO** (Создание любого пользователя, который может выполнить проверку подлинности с помощью единого входа).

    b. **Поставщик услуг saml**: вставьте значение hello ***urn: oasis: имена: tc: SAML:2.0:nameid-формат: постоянное***

    c. **Имя поля электронной почты поставщика удостоверений в ACS ответ**: вставьте значение hello`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`

    d. **Идентификатор сущности EntityDescriptor поставщика удостоверений:** hello вставить **идентификатор сущности SAML** значения, скопированные из hello портал Azure.

    д. **Удостоверение поставщика SingleSignOnService URL-адрес:** hello вставить **SAML единого входа URL-адрес службы** из hello портал Azure.

    f. **Сертификат открытого X509 поставщика удостоверений:** Привет открыть X509 сертификат будет загружен из hello Azure в Блокнот и вставьте содержимое hello в этом поле. Убедитесь, что не разрывы строк в hello средней hello содержимого сертификата.
    
    ж. Проверьте следующие флажки hello: **включено, шифрование NameID и AuthnRequests входа.**

    h. Нажмите кнопку **параметры единого входа обновления** toosave hello параметры.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_01.png) 

2. Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_02.png) 

3. Вверху hello hello диалоговое окно, нажмите кнопку **добавить** tooopen hello **пользователя** диалогового окна.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-scalexenterprise-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-scalex-enterprise-test-user"></a>Создание тестового пользователя ScaleX Enterprise

Пользователи toolog tooenable Azure AD в tooScaleX Enterprise, их необходимо подготовить в tooScaleX предприятия. В случае hello ScaleX Enterprise Подготовка пользователей осуществляется автоматическое и вручную действия, не требуются. На стороне ScaleX hello будет автоматически подготовлен любого пользователя, прошедшего проверку подлинности с использованием учетных данных единого входа.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления Enterprise tooScaleX доступа пользователя.

![Назначение пользователя][200] 

**tooassign Britta Simon tooScaleX Enterprise, выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **ScaleX Enterprise**.

    ![Настройка единого входа](./media/active-directory-saas-scalexenterprise-tutorial/tutorial_scalexenterprise_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.

### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

Щелкните hello ScaleX Enterprise плитку в hello панели доступа, вы получите автоматически вошедшего tooyour ScaleX корпоративного приложения. Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](https://msdn.microsoft.com/library/dn308586).


## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-scalexenterprise-tutorial/tutorial_general_203.png

