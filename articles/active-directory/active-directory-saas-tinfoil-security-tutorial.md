---
title: "Руководство по интеграции Azure Active Directory с TINFOIL SECURITY | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и TINFOIL SECURITY."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: da02da92-e3b0-4c09-ad6c-180882b0f9f8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 1a3fa9880d9e026c2d6d6548188df2269ff69139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tinfoil-security"></a>Руководство по интеграции Azure Active Directory с TINFOIL SECURITY

В этом учебнике вы узнаете, как toointegrate TINFOIL SECURITY с Azure Active Directory (Azure AD).

Интеграция TINFOIL SECURITY с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooTINFOIL безопасности
- Можно включить на пользователей tooautomatically get вошедшего tooTINFOIL безопасности (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с TINFOIL SECURITY требуется hello следующих элементов:

- подписка Azure AD;
- подписка TINFOIL SECURITY с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление TINFOIL SECURITY из коллекции hello
2. Настройка и проверка единого входа в Azure AD

## <a name="add-tinfoil-security-from-hello-gallery"></a>Добавление TINFOIL SECURITY из коллекции hello
tooconfigure hello интеграции TINFOIL SECURITY в Azure AD, вы должны tooadd TINFOIL SECURITY из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd TINFOIL SECURITY из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **TINFOIL SECURITY**выберите **TINFOIL SECURITY** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.

    ![Добавление TINFOIL SECURITY из коллекции](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в TINFOIL SECURITY с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователя аналог hello в TINFOIL SECURITY — tooa пользователя в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в TINFOIL SECURITY должен установить toobe.

В TINFOIL SECURITY, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с TINFOIL SECURITY, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя TINFOIL SECURITY](#create-a-tinfoil-security-test-user)**  -toohave аналог Саймон Britta в TINFOIL SECURITY, представление связанных toohello Azure AD пользователя.
4. **[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении TINFOIL SECURITY.

**tooconfigure Azure AD единого входа с TINFOIL SECURITY, выполните следующие шаги hello.**

1. В hello в hello портала Azure **TINFOIL SECURITY** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Вход на основе SAML](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_samlbase.png)

3. На hello **TINFOIL безопасности домена и URL-адреса** статьи, hello пользователь не имеет tooperform все меры как приложение hello уже заранее интегрировано с Azure.

    ![Настройка единого входа](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_url.png)


4. На hello **сертификат подписи SAML** раздел, hello копирования **ОТПЕЧАТОК** значение.

    ![Раздел "Сертификат подписи SAML"](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_certificate.png) 

5. сопоставления атрибутов hello необходимые tooadd, выполните hello следующие шаги.
    
    ![Атрибуты](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute1.png "Атрибуты")
    
    | Имя атрибута    |   Значение атрибута |
    | ------------------- | -------------------- |
    | accountid | UXXXXXXXXXXXXX |
    
    а. Щелкните **добавить атрибут пользователя**.
    
    ![Добавление атрибута](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_attribute.png "Атрибуты")
    
    ![Добавление атрибута](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_addatt.png "Атрибуты")
    
    b. В hello **имя атрибута** введите **accountid**.
    
    c. В hello **значение атрибута** текстовое значение идентификатора учетной записи hello вставить которого вы получите позднее hello учебника.
    
    d. Нажмите кнопку **ОК**.    

6. Нажмите кнопку **Сохранить** .

    ![Кнопка "Сохранить"](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_400.png)

7. На hello **конфигурация безопасности TINFOIL** щелкните **Настройка TINFOIL SECURITY** tooopen **Настройка входа** окна. Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Конфигурация TINFOIL SECURITY](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_configure.png) 

8. В другом окне веб-браузера войдите на свой корпоративный веб-сайт TINFOIL SECURITY в качестве администратора.

9. Щелкните hello панели инструментов в верхней части hello **Моя учетная запись**.
   
    ![Панель мониторинга](./media/active-directory-saas-tinfoil-security-tutorial/ic798971.png "Панель мониторинга")

10. Выберите пункт **Безопасность**.
   
    ![Безопасность](./media/active-directory-saas-tinfoil-security-tutorial/ic798972.png "Безопасность")

11. На hello **Single Sign-On** конфигурации выполните следующие шаги hello:
   
    ![Единый вход](./media/active-directory-saas-tinfoil-security-tutorial/ic798973.png "Единый вход")
   
    а. Выберите **Включить SAML**.
   
    b. Щелкните **Настроить вручную**.
   
    c. В **URL-адрес Post для SAML** текстовое значение hello вставить **SAML единого входа URL-адрес службы** скопирован из портала Azure
   
    d. В **отпечаток сертификата SAML** текстовое значение hello вставить **отпечаток** скопирован из **сертификат подписи SAML** раздела.
  
    д. Копировать **свой идентификатор учетной записи** значение и вставьте значение hello в **значение атрибута** текстовое поле под **Добавление атрибута** раздела на портале Azure.
   
    f. Щелкните **Сохранить**.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Выберите "Пользователи и группы" > "Все пользователи". ](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Пользователь](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tinfoil-security-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="create-a-tinfoil-security-test-user"></a>Создание тестового пользователя TINFOIL SECURITY

В порядке tooenable toolog пользователей Azure AD в TINFOIL SECURITY их необходимо подготовить в TINFOIL SECURITY. В случае TINFOIL SECURITY hello Подготовка выполняется вручную.

**tooget пользователь подготовлен, выполните следующие шаги hello.**

1. Hello пользователь входит в учетной записи предприятия, требуется слишком[обратитесь в службу поддержки TINFOIL SECURITY hello](https://www.tinfoilsecurity.com/contact) tooget hello Создание учетной записи пользователя.

2. Если пользователь hello обычный пользователь TINFOIL SECURITY SaaS, hello пользователя можно добавить участника совместной работы tooany сайтов hello пользователя. Этот триггеры toosend процесс, указанный toohello приглашение по электронной почте toocreate новой учетной записи безопасности TINFOIL SECURITY.

> [!NOTE]
> Можно использовать любые другие TINFOIL SECURITY пользователя средства создания учетных записей или API, предоставленные TINFOIL SECURITY tooprovision учетных записей пользователей Azure AD.
> 
> 

### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooTINFOIL безопасности.

![Назначение пользователя][200] 

**tooassign tooTINFOIL Britta Simon безопасности, выполните hello следующие шаги.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **TINFOIL SECURITY**.

    ![Выбор TINFOIL SECURITY](./media/active-directory-saas-tinfoil-security-tutorial/tutorial_tinfoil-security_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При выборе плитки TINFOIL SECURITY hello в hello панели доступа, вы должны получить приложение автоматически вошедшего tooyour TINFOIL SECURITY. Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tinfoil-security-tutorial/tutorial_general_203.png

