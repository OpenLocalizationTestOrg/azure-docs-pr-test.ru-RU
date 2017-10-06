---
title: "Руководство по интеграции Azure Active Directory с Asana | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Asana."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 837e38fe-8f55-475c-87f4-6394dc1fee2b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: jeedes
ms.openlocfilehash: 9ac35dedc809b2b3dfb461d92a5afb066ccdedde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asana"></a>Руководство. Интеграция Azure Active Directory с Asana

В этом учебнике вы узнаете, как toointegrate Asana с Azure Active Directory (Azure AD).

Интеграция с Azure AD Asana предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooAsana
- Можно включить на пользователей tooautomatically get вошедшего tooAsana (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Asana требуется hello следующих элементов:

- подписка Azure AD;
- подписка Asana с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Asana из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-asana-from-hello-gallery"></a>Добавление Asana из галереи hello
tooconfigure hello интеграции Asana в Azure AD, вы должны tooadd Asana из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Asana из галереи hello, выполните следующие шаги hello.**

1. В hello ** [портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Кнопка Hello Azure Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Hello корпоративных приложений колонку][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Кнопка нового приложения Hello][3]

4. Введите в поле поиска hello **Asana**выберите **Asana** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-asana-tutorial/tutorial_asana_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD

В этом разделе описана настройка и проверка единого входа Azure AD в Asana с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Asana является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в Asana должен установить toobe.

В Asana, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с Asana, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on) ** -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user) ** -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя, прошедшего Asana](#create-an-asana-test-user) ** -toohave аналог Саймон Britta в Asana, который представляет связанный toohello Azure AD пользователя.
4. **[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#test-single-sign-on) ** -tooverify ли hello works конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Asana.

**tooconfigure Azure AD единого входа с Asana, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Asana** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-asana-tutorial/tutorial_asana_samlbase.png)

3. На hello **URL-адреса и домена Asana** выполните следующие шаги hello:

    ![Сведения о домене и URL-адресах единого входа для приложения Asana](./media/active-directory-saas-asana-tutorial/tutorial_asana_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес:`https://app.asana.com/`

    b. В hello **идентификатор** текстовое поле, значение типа:`https://app.asana.com/`
 
4. На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-asana-tutorial/tutorial_asana_certificate.png)
    
5. Нажмите кнопку **Сохранить** .

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-asana-tutorial/tutorial_general_400.png)

6. На hello **конфигурации Asana** щелкните **Настройка Asana** tooopen **Настройка входа** окна. Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Конфигурация Asana](./media/active-directory-saas-asana-tutorial/tutorial_asana_configure.png) 

7. В другом окне браузера, tooyour входа Asana приложения. tooconfigure единого входа в Asana параметров рабочей области доступа hello, щелкнув имя рабочей области hello в hello правом верхнем углу экрана приветствия. Щелкните элемент **\<your workspace name\> Settings** (Параметры <имя_рабочей_области>). 
   
    ![Параметры единого входа Asana](./media/active-directory-saas-asana-tutorial/tutorial_asana_09.png)

8. На hello **параметры организации** окно, нажмите кнопку **администрирования**. Нажмите кнопку **членов необходимо войти в систему через SAML** Настройка единого входа tooenable hello. Hello выполните следующие шаги hello.
   
    ![Настройка параметров единого входа организации](./media/active-directory-saas-asana-tutorial/tutorial_asana_10.png)  

     а. В hello **входа в URL-адрес страницы** текстовое поле, вставить hello **SAML единого входа URL-адрес службы**.

     b. Щелкните правой кнопкой мыши сертификат hello загружен с портала Azure, а затем откройте файл сертификата hello, с помощью блокнота или предпочтительный текстовый редактор. Копирования содержимого hello между hello begin и hello конец заголовка сертификата и вставьте его в hello **сертификат X.509** текстового поля.

9. Щелкните **Сохранить**. Go слишком[Asana руководство по настройке единого входа](https://asana.com/guide/help/premium/authentication#gl-saml) Если вам нужна дополнительная помощь.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello ** Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD

Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание тестового пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-asana-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-asana-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-asana-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Кнопка "Добавить" Hello](./media/active-directory-saas-asana-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="create-an-asana-test-user"></a>Создание тестового пользователя Asana

В этом разделе описано, как создать пользователя Britta Simon в приложении Asana.

1. На **Asana**, go toohello **команды** раздел на левой панели hello. Нажмите кнопку hello, а также кнопки входа. 
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-asana-tutorial/tutorial_asana_12.png) 

2. Введите по электронной почте hello britta.simon@contoso.com в hello текстовое поле, а затем выберите **пригласить**.

3. Щелкните **Send Invite**(Отправить приглашение). Hello новый пользователь получит сообщение электронной почты в свою учетную запись электронной почты. Она может потребоваться toocreate и проверить подлинность учетной записи hello.

### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooAsana доступа.

![Назначение пользователям ролей hello][200]

**tooassign tooAsana Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Asana**.

    ![ссылка Asana Hello в списке приложений hello](./media/active-directory-saas-asana-tutorial/tutorial_asana_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Hello ссылку «Пользователи и группы»][202]

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![область назначения, добавьте Hello][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

Цель этого раздела Hello является tootest к Azure AD единого входа.

Переход на страницу входа tooAsana. В текстовом поле адрес электронной почты hello вставить адрес электронной почты hello britta.simon@contoso.com. Оставьте текстовое поле пароля hello в пустым и нажмите кнопку **входа в**. Будет перенаправленный tooAzure AD страницы входа. Введите учетные данные Azure AD. Теперь вы должны войти в Asana.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-asana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-asana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-asana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-asana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-asana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-asana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-asana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-asana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-asana-tutorial/tutorial_general_203.png
[10]: ./media/active-directory-saas-asana-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-asana-tutorial/tutorial_general_070.png
