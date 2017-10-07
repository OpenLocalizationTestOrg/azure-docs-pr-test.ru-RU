---
title: "Руководство по интеграции Azure Active Directory с LinkedIn Lookup | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и LinkedIn уточняющего запроса."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a2757a39-1ead-4a3e-91e4-270be3055683
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: d79c34baa676391699e4b49806f16422fcfe73e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-lookup"></a>Руководство по интеграции Azure Active Directory с LinkedIn Lookup

В этом учебнике вы узнаете, как toointegrate уточняющего запроса LinkedIn с Azure Active Directory (Azure AD).

Интеграция LinkedIn подстановки с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooLinkedIn уточняющего запроса
- Можно включить вашей пользователей tooautomatically get вошедшего tooLinkedIn уточняющего запроса (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с LinkedIn подстановки необходимо hello следующих элементов:

- подписка Azure AD;
- подписка LinkedIn Lookup с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление LinkedIn поиска из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-linkedin-lookup-from-hello-gallery"></a>Добавление LinkedIn поиска из галереи hello
tooconfigure hello интеграции LinkedIn уточняющего запроса в Azure AD, вы должны tooadd LinkedIn поиска из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd LinkedIn поиска из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. Нажмите кнопку **новое приложение** кнопку сверху "hello" hello диалоговое окно tooadd новое приложение.

    ![Приложения][3]

4. Введите в поле поиска hello **уточняющего запроса LinkedIn**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_search.png)

5. В панели результатов hello, выберите **уточняющего запроса LinkedIn**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в приложении LinkedIn Lookup с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в уточняющем запросе LinkedIn является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в уточняющем запросе LinkedIn должен установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в уточняющем запросе LinkedIn.

tooconfigure и теста Azure AD единого входа с LinkedIn уточняющего запроса, необходимые hello toocomplete следующие стандартные блоки.

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя, прошедшего подстановки LinkedIn](#creating-an-linkedin-lookup-test-user)**  -toohave аналог Саймон Britta в уточняющем запросе LinkedIn, представление связанных toohello Azure AD.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении LinkedIn уточняющего запроса.

**tooconfigure Azure AD единого входа при поиске LinkedIn выполните следующие шаги hello.**

1. В hello в hello портала Azure **уточняющего запроса LinkedIn** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалоговое окно, в **режим** выберите **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_samlbase.png)

3. В другом окне браузера, tooyour входа **уточняющего запроса LinkedIn** веб-сайта от имени администратора.

4. В **Account Center** (Центр учетных записей) в разделе **Settings** (Параметры) щелкните **Global Settings** (Глобальные параметры). Кроме того, установите **уточняющего запроса** hello в раскрывающемся списке.

    ![Настройка единого входа](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_011.png)

5. Нажмите кнопку **или щелкните здесь tooload и скопируйте отдельные поля из формы hello** и скопируйте **идентификатор сущности** и **URL-адрес утверждение потребителя доступа (ACS)**

    ![Настройка единого входа](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_LinkedIn_admin_032.png)

6. На портале Azure в разделе **LinkedIn просмотр доменов и URL-адреса** выполните hello, выполните действия, при желании tooconfigure приложения hello в **IDP** инициировал режим:

    ![Настройка единого входа](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url.png)

    а. В hello **идентификатор** текстовом поле введите hello **идентификатор сущности** копируются LinkedIn портала 

    b. В hello **URL-адрес ответа** текстовом поле введите hello **утверждение потребителя доступа (ACS) URL-адрес** копируются LinkedIn портала

7. Проверьте **Показывать дополнительные параметры URL-адреса**, если нужно, чтобы приложение hello tooconfigure в **SP** инициировал режим:

    ![Настройка единого входа](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_url1.png)

    В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://www.linkedIn.com/checkpoint/enterprise/login/<AccountId>?application=lookup`
     
    > [!NOTE] 
    > Не является действительным значением. Hello пользователем tooupdate эти значения с hello фактический URL-адрес входа. Обратитесь к [уточняющего запроса клиент LinkedIn поддержки](https://business.LinkedIn.com/lookup) tooget это значение.

8. Ваш **уточняющего запроса LinkedIn** приложение ожидает утверждения SAML hello в определенном формате. Hello пользователем конфигурация атрибутов токена SAML toohello сопоставления tooadd настраиваемого атрибута. Следующий снимок экрана приветствия показан пример. значение по умолчанию Hello **идентификатор пользователя** — **user.userprincipalname** , но это toobe, сопоставленный с адресом электронной почты пользователя hello ожидает LinkedIn уточняющего запроса. Можно использовать **user.mail** атрибут из списка hello, или используйте hello соответствующее значение атрибута на основе конфигурации в организации. 

    ![Настройка единого входа](./media/active-directory-saas-LinkedInlookup-tutorial/updateusermail.png)
    
9. В **атрибуты пользователя** щелкните **представление и редактировать все остальные атрибуты пользователя** и задавать атрибуты hello. Hello пользователь должен tooadd четыре утверждения с именем **электронной почты**, **отдел**, **firstname**, и **lastname** и hello значение — toobe сопоставлено с **user.mail**, **user.department**, **user.givenname**, и **user.surname** соответственно

    | Имя атрибута | Значение атрибута |
    | --- | --- |
    | email| user.mail |    
    | department| user.department |
    | firstname| user.givenname |
    | lastname| user.surname |

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/userattribute.png)

    а. Нажмите кнопку **Добавление атрибута** tooopen hello **Добавление атрибута** диалогового окна.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/4.png)
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/5.png)
   
    b. В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.
    
    c. Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.
    
    d. Нажмите кнопку **ОК**.

10. Выполните следующие действия на hello hello **имя** атрибута -

    а. Щелкните hello атрибут tooopen hello **изменение атрибута** окна.

    ![Настройка единого входа](./media/active-directory-saas-LinkedInlookup-tutorial/url_update.png)

    b. Удалить значение URL-адрес hello из hello **пространства имен**.
    
    c. Нажмите кнопку **ОК** toosave приветствия.

10. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и сохраните hello XML-файл на компьютере.

    ![Настройка единого входа](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_certificate.png) 

11. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_400.png)

12. Go слишком**параметры администрирования LinkedIn** раздела. Отправка hello XML-файл, загруженный с портала Azure hello, щелкнув hello **отправить XML-файл** параметр.

    ![Настройка единого входа](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_metadata_03.png)

13. Нажмите кнопку **на** tooenable единого входа. Изменение состояния единого входа с **не подключены** слишком**подключено**

    ![Настройка единого входа](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedIn_admin_05.png)

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_01.png) 

2. Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_02.png) 

3. Нажмите кнопку **добавить** tooopen hello **пользователя** диалогового окна.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **Britta Simon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из Саймон Britta.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-an-linkedin-lookup-test-user"></a>Создание тестового пользователя LinkedIn Lookup

Связанное приложение поиска поддерживает только в подготовки пользователей Time (JIT) и после проверки подлинности пользователей автоматически создаются в приложении hello. Активировать **автоматически назначать лицензии** tooassign toohello лицензии пользователя.
   
   ![Создание тестового пользователя Azure AD](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedin_admin_license.png)

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooLinkedIn уточняющего запроса.

![Назначение пользователя][200] 

**tooassign tooLinkedIn Britta Simon уточняющего запроса, выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **уточняющего запроса LinkedIn**.

    ![Настройка единого входа](./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_linkedInlookup_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.

    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello, LinkedIn подстановки плитки в панели доступа hello, должна быть страницей перенаправленный tooOrganizational, при наличии tooprovide личные сведения учетной записи LinkedIn. В результате ваша личная учетная запись связывается с вашей рабочей учетной записью LinkedIn. 

Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-LinkedInlookup-tutorial/tutorial_general_203.png

