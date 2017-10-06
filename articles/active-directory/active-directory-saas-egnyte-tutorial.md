---
title: "Учебник. Интеграция Azure Active Directory с Egnyte | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Egnyte."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8c2101d4-1779-4b36-8464-5c1ff780da18
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: d86fa28a1e7b23474cb76c08aef8539acadaf24d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-egnyte"></a>Руководство. Интеграция Azure Active Directory с Egnyte

В этом учебнике вы узнаете, как toointegrate Egnyte с Azure Active Directory (Azure AD).

Интеграция Egnyte с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooEgnyte
- Можно включить на пользователей tooautomatically get вошедшего tooEgnyte (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Egnyte, требуется hello следующих элементов:

- подписка Azure AD;
- Подписка с поддержкой единого входа Egnyte

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Egnyte из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-egnyte-from-hello-gallery"></a>Добавление Egnyte из галереи hello
tooconfigure hello интеграции Egnyte в Azure AD, вы должны tooadd Egnyte из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Egnyte из галереи hello, выполните следующие шаги hello.**

1. В hello ** [портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **Egnyte**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_search.png)

5. В панели результатов hello выберите **Egnyte**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в приложение Egnyte для тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Egnyte является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в Egnyte должен установить toobe.

В Egnyte, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с Egnyte, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user) ** -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя, прошедшего Egnyte](#creating-an-egnyte-test-user) ** -toohave аналог Саймон Britta в Egnyte, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on) ** -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Egnyte.

**Azure AD tooconfigure единого входа с Egnyte, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Egnyte** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_samlbase.png)

3. На hello **URL-адреса и домена Egnyte** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_url.png)

    В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.egnyte.com`

    > [!NOTE] 
    > Это значение приведено для справки. Измените значение этого параметра hello фактический URL-адрес входа. Обратитесь к [группа поддержки клиента Egnyte](https://www.egnyte.com/corp/contact_egnyte.html) tooget это значение. 
 
4. На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-egnyte-tutorial/tutorial_general_400.png)

6. На hello **конфигурации Egnyte** щелкните **Настройка Egnyte** tooopen **Настройка входа** окна. Копировать hello **идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_configure.png) 

7. В другом окне браузера войти в корпоративный сайт Egnyte tooyour с правами администратора.

8. Щелкните **Параметры**.
   
   ![Параметры](./media/active-directory-saas-egnyte-tutorial/ic787819.png "Параметры")

9. В меню "hello" щелкните **параметры**.

   ![Параметры](./media/active-directory-saas-egnyte-tutorial/ic787820.png "Параметры")

10. Нажмите кнопку hello **конфигурации** , а затем щелкните **безопасности**.

    ![Безопасность](./media/active-directory-saas-egnyte-tutorial/ic787821.png "Безопасность")

11. В hello **единого входа для проверки подлинности** выполните следующие шаги hello:

    ![Аутентификация единого входа](./media/active-directory-saas-egnyte-tutorial/ic787822.png "Аутентификация единого входа")   
    
    а. Выберите для параметра **Single sign-on authentication** (Аутентификация единого входа) значение **SAML 2.0**.
   
    b. Выберите для параметра **Identity provider** (Поставщик удостоверений) значение **AzureAD**.
   
    c. Вставить **SAML единого входа URL-адрес службы** скопирован из портала Azure в hello **URL-адрес входа поставщика удостоверений** текстового поля.
   
    d. Вставить **идентификатор сущности SAML** скопирован из портала Azure в hello **идентификатор сущности поставщика удостоверений** текстового поля.
      
    д. Откройте сертификат в кодировке base-64 в блокноте, загруженные из портала Azure hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **сертификат поставщика удостоверений** текстового поля.
   
    f. Выберите для параметра **Default user mapping** (Сопоставление пользователя по умолчанию) значение **Email address** (Адрес электронной почты).
   
    ж. Выберите для параметра **Use domain-specific issuer value** (Использовать значение издателя домена) значение **disabled** (отключено).
   
    h. Щелкните **Сохранить**.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello ** Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-an-egnyte-test-user"></a>Создание тестового пользователя Egnyte

Пользователи toolog tooenable Azure AD в tooEgnyte, их необходимо подготовить в Egnyte. В случае hello объекта Egnyte Подготовка выполняется вручную.

**tooprovision учетных записей пользователей, выполните следующие действия hello:**

1. Войдите в tooyour **Egnyte** сайт компании от имени администратора.

2. Go слишком**параметры \> пользователи и группы**.

3. Нажмите кнопку **добавить пользователя**, а затем выберите тип hello пользователя требуется tooadd.
   
   ![Пользователи](./media/active-directory-saas-egnyte-tutorial/ic787824.png "Пользователи")

4. В hello **новый обычный пользователь** выполните следующие шаги hello:
   
   ![Новый обычный пользователь](./media/active-directory-saas-egnyte-tutorial/ic787825.png "Новый обычный пользователь")   

   а. Тип hello **электронной почты**, **Username**и другие сведения о действительной учетной записи Azure Active Directory требуется tooprovision.
   
   b. Щелкните **Сохранить**.
    
    >[!NOTE]
    >Владелец учетной записи Azure Active Directory Hello получит уведомление по электронной почте.
    >

>[!NOTE]
>Можно использовать любые другие Egnyte пользователя средства создания учетных записей или интерфейсы API, предоставляемые Egnyte tooprovision учетных записей пользователей AAD.
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooEgnyte доступа.

![Назначение пользователя][200] 

**tooassign tooEgnyte Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Egnyte**.

    ![Настройка единого входа](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello Egnyte плитки в панели доступа hello, вы должны получить tooyour автоматически подписан на Egnyte приложения.
Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_203.png

