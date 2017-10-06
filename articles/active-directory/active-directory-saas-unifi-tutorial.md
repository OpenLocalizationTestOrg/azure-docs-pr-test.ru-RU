---
title: "Руководство по интеграции Azure Active Directory с UNIFI | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и UNIFI."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e1f49ee4-d2d4-4a82-9baf-0587ca1f20f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: af7cc1167b5c0cff2a1f4cdaa8a2b93f5a718f81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-unifi"></a>Руководство по интеграции Azure Active Directory с UNIFI

В этом учебнике вы узнаете, как toointegrate UNIFI с Azure Active Directory (Azure AD).

Интеграция с Azure AD UNIFI предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooUNIFI
- Можно включить на пользователей tooautomatically get вошедшего tooUNIFI (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с UNIFI требуется hello следующих элементов:

- подписка Azure AD;
- подписка UNIFI с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление UNIFI из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-unifi-from-hello-gallery"></a>Добавление UNIFI из галереи hello
tooconfigure hello интеграции UNIFI в Azure AD, вы должны tooadd UNIFI из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd UNIFI из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **UNIFI**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_search.png)

5. В панели результатов hello выберите **UNIFI**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в приложение UNIFI с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в UNIFI является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в UNIFI должен установить toobe.

В UNIFI, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с UNIFI, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание UNIFI тестовый пользователь](#creating-a-unifi-test-user)**  -toohave аналог Саймон Britta в UNIFI, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении UNIFI.

**tooconfigure Azure AD единого входа с UNIFI, выполните следующие шаги hello.**

1. В hello в hello портала Azure **UNIFI** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_samlbase.png)

3. На hello **UNIFI доменов и URL-адреса** статьи, при желании tooconfigure приложения hello в **IDP** инициировал режим:

    ![Настройка единого входа](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_url1.png)

    В hello **идентификатор** текстовое значение hello типа:`INVIEWlabs` 

4. Проверьте **Показывать дополнительные параметры URL-адреса**, если нужно, чтобы приложение hello tooconfigure в **SP** инициировал режим:

    ![Настройка единого входа](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_url2.png)

    В hello **URL-адрес входа** текстовом поле введите URL-адрес hello:`https://app.discoverunifi.com/login`

5. На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_certificate.png) 

6. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-unifi-tutorial/tutorial_general_400.png)
    
7. На hello **конфигурации UNIFI** щелкните **Настройка UNIFI** tooopen **Настройка входа** окна. Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_configure.png)

8. В другом окне браузера, войдите на tooyour **UNIFI** сайт компании от имени администратора.

9. Щелкните hello **пользователей**.

    ![Настройка единого входа](./media/active-directory-saas-unifi-tutorial/app1.png) 

10. Щелкните hello **Добавление поставщика удостоверений**.

    ![Настройка единого входа](./media/active-directory-saas-unifi-tutorial/app2.png)

11. В hello **Добавление поставщика удостоверений** выполните следующие шаги hello:   

    ![Настройка единого входа](./media/active-directory-saas-unifi-tutorial/app3.png) 

    а. В hello **имя поставщика** текстовое поле, имя типа hello hello поставщика удостоверений...

    b. В hello hello **URL-адрес поставщика** текстовое поле вставьте hello **SAML единого входа URL-адрес службы** значение, которое было скопировано из портала Azure.

    c. Привет открыть сертификат, загруженный из hello портал Azure в блокноте, удалите hello **---BEGIN CERTIFICATE---** и **---конечный СЕРТИФИКАТ---** тега, а затем вставьте hello оставшееся содержимое Hello **сертификат** текстового поля.

    d. Выберите hello **является поставщиком по умолчанию** флажок.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-unifi-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-unifi-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-unifi-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-unifi-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-unifi-test-user"></a>Создание тестового пользователя UNIFI

В этом разделе описано, как создать пользователя Britta Simon. Приложение **UNIFI** поддерживает автоматическую подготовку пользователей, поэтому действия вручную не требуются. Пользователи создаются автоматически после успешной проверки подлинности из hello Azure AD.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooUNIFI доступа.

![Назначение пользователя][200] 

**tooassign tooUNIFI Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **UNIFI**.

    ![Настройка единого входа](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки UNIFI плитки в панели доступа hello hello, вы должны получить автоматически вошедшего tooyour UNIFI приложения.
Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_203.png

