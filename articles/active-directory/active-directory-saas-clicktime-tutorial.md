---
title: "Учебник. Интеграция Azure Active Directory с ClickTime | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory с ClickTime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d437b5ab-4d71-4c13-96d0-79018cebbbd4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: jeedes
ms.openlocfilehash: a0259e31164cad6c6c77ed8aac1c50cd9a3e46ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clicktime"></a>Руководство. Интеграция Azure Active Directory с ClickTime

В этом учебнике вы узнаете, как toointegrate ClickTime с Azure Active Directory (Azure AD).

Интеграция ClickTime с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooClickTime
- Можно включить на пользователей tooautomatically get вошедшего tooClickTime (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с ClickTime требуется hello следующих элементов:

- подписка Azure AD;
- подписка ClickTime с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление ClickTime из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-clicktime-from-hello-gallery"></a>Добавление ClickTime из галереи hello
tooconfigure hello интеграции ClickTime в Azure AD, вы должны tooadd ClickTime из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd ClickTime из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Кнопка Hello Azure Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Hello корпоративных приложений колонку][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Кнопка нового приложения Hello][3]

4. Введите в поле поиска hello **ClickTime**выберите **ClickTime** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.

    ![ClickTime в списке результатов hello](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD

В этом разделе описана настройка и проверка единого входа Azure AD в ClickTime с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в ClickTime является tooa в Azure AD. Другими словами связи между пользователя Azure AD и hello связанных пользователей в ClickTime должен установить toobe.

В ClickTime, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с ClickTime, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя ClickTime](#create-a-clicktime-test-user)**  -toohave аналог Саймон Britta в ClickTime, который представляет связанный toohello Azure AD пользователя.
4. **[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении ClickTime.

**Azure AD tooconfigure единого входа с ClickTime, выполните следующие шаги hello.**

1. В hello в hello портала Azure **ClickTime** странице интеграции приложения щелкните **единого входа**.

    ![Ссылка "Настройка единого входа"][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_samlbase.png)

3. На hello **URL-адреса и домена ClickTime** выполните следующие шаги hello:

    ![Сведения о домене и URL-адресах единого входа приложения ClickTime](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_url.png)

    а. В hello **идентификатор** текстовом поле введите URL-адрес как:`https://app.clicktime.com/sp/`
    
    b. В hello **URL-адрес ответа** текстовое поле, введите URL-адрес, используя hello следующие шаблоны: 

    | |
    |--|
    | `https://app.clicktime.com/Login/` |
    | `https://app.clicktime.com/App/Login/Consume.aspx` |

4. На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-clicktime-tutorial/tutorial_general_400.png)

6. На hello **конфигурации ClickTime** щелкните **Настройка ClickTime** tooopen **Настройка входа** окна. Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка ClickTime](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_configure.png) 

7. В другом окне веб-браузера войдите на свой корпоративный веб-сайт ClickTime в качестве администратора.

8. Щелкните hello панели инструментов в верхней части hello **предпочтения**, а затем нажмите кнопку **параметры безопасности**.

9. В hello **предпочтения-** конфигурации выполните следующие шаги hello:
   
    ![Параметры безопасности](./media/active-directory-saas-clicktime-tutorial/tic777280.png "Параметры безопасности")
   
    а.  Выберите "**Allow** sign-in using Single Sign-On (SSO) with **Azure AD**" (Разрешить единый вход (SSO) с помощью Azure AD).
   
    b. В hello **конечная точка поставщика удостоверений** вставьте **SAML единого входа URL-адрес службы** скопирован из портала Azure.
   
    c.  Откройте hello **сертификат в кодировке base-64** загружен с портала Azure в **Блокнот**, скопируйте содержимое hello и вставьте его в hello **сертификат X.509** текстового поля.
   
    d.  Щелкните **Сохранить**.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание тестового пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-clicktime-tutorial/create_aaduser_01.png) 

2. слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.
    
    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-clicktime-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.
 
    ![Кнопка "Добавить" Hello](./media/active-directory-saas-clicktime-tutorial/create_aaduser_03.png) 

4. В hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-clicktime-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="create-a-clicktime-test-user"></a>Создание тестового пользователя ClickTime

В порядке tooenable toolog пользователей Azure AD в ClickTime их необходимо подготовить в ClickTime.  
В случае hello ClickTime Подготовка выполняется вручную.

> [!NOTE]
> Можно использовать любые другие ClickTime пользователя средства создания учетных записей или API, предоставленные ClickTime tooprovision учетных записей пользователей Azure AD.

**tooprovision учетной записи пользователя, выполните следующие шаги hello.**
1. Войдите в tooyour **ClickTime** клиента.
2. Щелкните hello панели инструментов в верхней части hello **компании**, а затем нажмите кнопку **людей**.
   
    ![Люди](./media/active-directory-saas-clicktime-tutorial/tic777282.png "Люди")
3. Нажмите кнопку **Добавить пользователя**.
   
    ![Добавление пользователя](./media/active-directory-saas-clicktime-tutorial/tic777283.png "Добавление пользователя")
4. В hello раздела новый пользователь выполните следующие шаги hello.
   
    ![Люди](./media/active-directory-saas-clicktime-tutorial/tic777284.png "Люди")
   
    а.  В hello **полное имя** введите полное имя пользователя, таких как **Britta Simon**. 
  
    b.  В hello **адрес электронной почты** электронной почты hello тип пользователя в текстовое поле, например  **brittasimon@contoso.com** .
       
    > [!NOTE]
    > Если вы хотите, можно задать дополнительные свойства объекта hello нового пользователя.
   
    c.  Щелкните **Сохранить**.

### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooClickTime доступа.

![Назначение пользователям ролей hello][200] 

**tooassign tooClickTime Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **ClickTime**.

    ![ClickTimne ссылку в списке приложений hello](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Hello ссылку «Пользователи и группы»][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![область назначения, добавьте Hello][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello ClickTime плитки в панели доступа hello, вы должны получить приложение автоматически вошедшего tooyour ClickTime.
Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_203.png

