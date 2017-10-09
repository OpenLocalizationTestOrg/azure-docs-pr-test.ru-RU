---
title: "Руководство по интеграции Azure Active Directory с Cezanne HR Software | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Cezanne HR программного обеспечения."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fb8f95bf-c3c1-4e1f-b2b3-3b67526be72d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 3675acd8871d62c2277def8074f7aa39ac46e2a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-cezanne-hr-software"></a>Руководство по интеграции Azure Active Directory с Cezanne HR Software

В этом учебнике вы узнаете, как toointegrate Cezanne HR программного обеспечения в Azure Active Directory (Azure AD).

Интеграция Cezanne HR программного обеспечения в Azure AD предоставляет следующие преимущества hello. Вы можете:

- Управление Azure AD, имеющего доступ tooCezanne HR программного обеспечения.
- Включите tooautomatically пользователей при входе в tooCezanne HR программного обеспечения с помощью единого входа (SSO) с помощью своих учетных записей Azure AD.
- Управление учетными записями в одном централизованном месте: hello портал Azure.

toolearn Дополнительные сведения о программное обеспечение как услуга (SaaS) интеграции приложений с Azure AD, в разделе [доступ к приложению и единый вход в Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Cezanne HR программного обеспечения необходимо hello следующих элементов:

- подписка Azure AD;
- подписка Cezanne HR Software с поддержкой единого входа.

> [!NOTE]
> tootest hello шаги в этом учебнике, рекомендуется не использовать рабочей среде.

tootest hello шаги в этом учебнике, придерживайтесь следующих рекомендаций:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. 

Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

* Добавление программного обеспечения Cezanne HR из галереи hello
* Настройка и проверка единого входа Azure AD.

## <a name="add-cezanne-hr-software-from-hello-gallery"></a>Добавление Cezanne HR программного обеспечения из библиотеки hello
Интеграция hello tooconfigure Cezanne HR программного обеспечения в Azure AD, добавить Cezanne HR программного обеспечения из hello коллекции tooyour список управляемых приложений SaaS.

tooadd Cezanne HR программного обеспечения из галереи hello hello следующие:

1. В hello  **[портал Azure](https://portal.azure.com)**в левой области hello, выберите hello **Azure Active Directory** кнопки. 

    ![Кнопка «Azure Active Directory» Hello][1]

2. Щелкните **Корпоративные приложения** > **Все приложения**.

    ![Здравствуйте, «Все приложения» ссылки][2]
    
3. новое приложение hello верхней части hello tooadd **все приложения** выберите **новое приложение**.

    ![Здравствуйте, «Новое приложение» кнопки][3]

4. Введите в поле поиска hello **программного обеспечения HR Cezanne**.

    ![поле поиска Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_search.png)

5. В списке результатов hello выберите **программного обеспечения HR Cezanne** , а затем выберите hello **добавить** кнопку tooadd приложения hello.

    ![список результатов Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описано, как настроить и проверить единый вход Azure AD в Cezanne HR Software с использованием тестового пользователя Britta Simon.

Для toowork единого входа Azure AD необходима hello tooknow Cezanne HR аналог программного обеспечения toohello пользователя Azure AD. Другими словами необходимо установить связи между пользователя Azure AD и связанных пользователей hello в hello Cezanne HR программного обеспечения.

tooestablish hello связи, hello назначения программного обеспечения Cezanne HR **имя пользователя** значение как hello Azure AD **Username** значение.

tooconfigure и Azure AD SSO с помощью программного обеспечения Cezanne HR, полный hello следующие стандартные блоки тестов.

### <a name="configure-azure-ad-sso"></a>Настройка единого входа Azure AD

В этом разделе можно включить единый вход Azure AD в hello портал Azure и настройки единого входа в приложении Cezanne HR программного обеспечения, выполнив следующие hello:

1. В hello в hello портала Azure **программного обеспечения HR Cezanne** странице интеграции приложений выберите **единого входа**.

    ![Здравствуйте, команда «Единый вход»][4]

2. tooenable единого входа, в hello **единого входа** диалоговое окно, выберите hello **режим** как **входа на базе SAML**.
 
    ![поле «Режим» Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_samlbase.png)

3. В разделе **URL-адреса и домена программного обеспечения HR Cezanne**, hello следующие:

    ![Hello раздел «Cezanne HR программного обеспечения доменов и URL-адреса»](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_url.png)

    а. В hello **URL-адрес входа** введите URL-адрес имеет hello синтаксис:`https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`

    b. В hello **URL-адрес ответа** введите URL-адрес имеет hello синтаксис:`https://w3.cezanneondemand.com:443/<tenantid>`    
     
    > [!NOTE] 
    > Hello выше значения не являются реальными. Обновите их с URL-адрес ответа фактическое hello и hello URL-адрес входа. значения tooobtain hello, обратитесь в службу hello [группа поддержки клиентского программного обеспечения Cezanne HR](mailto:info@cezannehr.com).

4. В разделе **сертификат подписи SAML**выберите **сертификата (Base64)**и затем сохраните файл сертификата hello на вашем компьютере.

    ![раздел «Сертификат подписи SAML» Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_certificate.png) 

5. Щелкните **Сохранить**.

    ![кнопка «Сохранить» Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_400.png)
    
6. В разделе **конфигурации программного обеспечения HR Cezanne**выберите **Настройка программного обеспечения Cezanne HR** tooopen hello **Настройка входа** окна. Копировать hello **идентификатор сущности SAML** и **SAML единого входа службы** URL-адрес из hello **краткий справочник** раздела.

    ![раздел «Конфигурации программного обеспечения Cezanne HR» Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_configure.png) 

7. В другом окне браузера Войдите на tooyour Cezanne HR программного обеспечения клиента с правами администратора.

8. Выберите в левой области hello **настройки системы**. Выберите **Security Settings** > **Single Sign-On Configuration** ("Параметры безопасности" > "Конфигурация единого входа").

    ![связь «Один настройки единого входа» Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_000.png)

9. В hello **разрешить пользователям toolog hello следующие службы единого входа (SSO) с помощью** области, выберите hello **SAML 2.0** флажок и выберите hello **Расширенная настройка** параметр.

    ![Параметры служб единого входа](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_001.png)

10. Нажмите кнопку **Add New** (Добавить).

    ![Hello кнопку «Добавить»](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_002.png)

11. В разделе **Поставщики удостоверений SAML 2.0**, hello следующие:

    ![раздел «Поставщики удостоверений SAML 2.0» Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_003.png)
    
    а. В hello **отображаемое имя** введите название hello поставщика удостоверений.

    b. В hello **идентификатор сущности** вставьте hello **идентификатор сущности SAML** , скопированный из hello портал Azure. 

    c. В hello **привязки SAML** выберите **POST**.

    d. В hello **конечную точку службы маркеров безопасности** вставьте hello **SAML единого входа службы** URL-адрес, скопированный из hello портал Azure. 
    
    д. В hello **имя атрибута идентификатора пользователя** введите `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.
    
    f. tooupload hello загрузить сертификат из Azure AD, выберите hello **отправить** кнопки.
    
    ж. Нажмите кнопку **ОК**. 

12. Щелкните **Сохранить**.

    ![кнопка «Сохранить» Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_004.png)

> [!TIP]
> При настройке приложения hello, могут читать четкими версию перед инструкции в hello hello [портал Azure](https://portal.azure.com). После добавления приложение hello с hello **Active Directory** > **корпоративных приложений** раздел, выберите hello **единого входа** вкладки. Hello доступа внедряются документации из hello **конфигурации** раздела. 

toolearn Дополнительные сведения о функции hello внедренные документации, в разделе [Azure AD внедренных документации]( https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
В этом разделе создайте тестового пользователя Саймон Britta в hello портал Azure.

![Hello тестового пользователя Саймон Britta][100]

Здравствуйте toocreate тестового пользователя в Azure AD, следующие:

1. В hello **портал Azure**в левой области hello, выберите hello **Azure Active Directory** кнопки.

    ![Кнопка «Azure Active Directory» Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_01.png) 

2. список пользователей, выберите toodisplay hello **пользователей и групп** > **всех пользователей**.
    
    ![Здравствуйте, «Все пользователи» ссылки](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_02.png) 
    
    Hello **всех пользователей** откроется диалоговое окно.

3. tooopen hello **пользователя** выберите **добавить**.
 
    ![Кнопка «Добавить» Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_03.png) 

4. В hello **пользователя** диалогового окна поле, hello следующие:
 
    ![диалоговое окно «User» Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** введите пользователя Britta Simon **адрес электронной почты**.

    c. Выберите hello **Показать пароль** флажок, а затем значение hello примечание, созданный в hello **пароль** поле.

    d. Нажмите кнопку **Создать**.
 
### <a name="create-a-cezanne-hr-software-test-user"></a>Создание тестового пользователя Cezanne HR Software

Пользователи toosign tooenable Azure AD в программном обеспечении tooCezanne отдела Кадров, их необходимо подготовить в отделе Кадров Cezanne программное обеспечение. В случае hello программного обеспечения Cezanne HR Подготовка выполняется вручную.

Подготовка учетной записи пользователя, выполнив hello ниже:

1.  Войдите в tooyour Cezanne HR программного обеспечения корпоративный сайт с правами администратора.

2.  Выберите в левой области hello **установки System** > **Управление пользователями** > **добавить пользователя**.

    ![ссылка «Добавить пользователя» Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "нового пользователя")

3.  В разделе **сведения о лице**, hello следующие:

    ![Hello раздела «Подробности лица»](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "нового пользователя")
    
    а. Установите для параметра **Internal User** (Внутренний пользователь) значение **OFF** (Выключено).
    
    b. В hello **имя** поле, тип hello имя пользователя, например, **Britta**.  
 
    c. В hello **Фамилия** поле, тип hello фамилию пользователя, например, **Simon**.
    
    d. В hello **электронной почты** введите hello адрес электронной почты пользователя, например, Brittasimon@contoso.com.

4.  В разделе **сведения об учетной записи**, hello следующие:

    ![раздел «Сведения об учетной записи» Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "нового пользователя")
    
    а. В hello **Username** введите hello адрес электронной почты пользователя, например, Brittasimon@contoso.com.
    
    b. В hello **пароль** введите пароль пользователя hello.
    
    c. В hello **роль безопасности** выберите **HR Professional**.
    
    d. Нажмите кнопку **ОК**.

5. На hello **единого входа** hello на вкладке **идентификаторов SAML 2.0** выберите **добавить новое**.

    ![Hello кнопку «Добавить»](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "пользователя")

6. В hello **поставщика удостоверений** выберите поставщика удостоверений. В hello **идентификатор пользователя** введите hello адрес электронной почты для учетной записи тестового пользователя Britta Simon.

    ![Здравствуйте, «Поставщик удостоверений» и «Идентификатор пользователя» поля](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "пользователя")
    
7. Щелкните **Сохранить**.

    ![кнопка «Сохранить» Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "пользователя")

### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя

В этом разделе включите тестового пользователя toouse Britta Simon Azure единого входа путем предоставления программного доступа tooCezanne HR.

![Проверка доступа пользователей][200] 

1. В hello портал Azure откройте представление приложения hello, а затем перейдите toohello представления каталога. Щелкните **Корпоративные приложения** > **Все приложения**.

    ![Здравствуйте, «Все приложения» ссылки][201] 

2. В списке приложений hello выберите **программного обеспечения HR Cezanne**.

    ![список «Приложения» Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_app.png) 

3. Выберите в меню hello слева hello, **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Выберите **Добавить**. Затем в hello **добавить назначение** выберите **пользователей и групп**.

    ![Ссылка "Пользователи и группы"][203]

5. В hello **пользователей и групп** диалогового окна hello **пользователей** выберите **Britta Simon**.

6. В hello **пользователей и групп** выберите **выберите**.

7. В hello **добавить назначение** выберите **назначить**.
    
### <a name="test-sso"></a>Проверка единого входа

В этом разделе можно проверить конфигурацию единого входа Azure AD с помощью панели доступа hello.

При выборе плитки программного обеспечения Cezanne HR hello в панель доступа hello входа автоматически tooyour Cezanne HR программного приложения.

## <a name="next-steps"></a>Дальнейшие действия

* [Список учебников по toointegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_203.png

