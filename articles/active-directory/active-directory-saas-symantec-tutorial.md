---
title: "Руководство по интеграции Azure Active Directory с Symantec Web Security Service (WSS) | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и службы безопасности Symantec Web (WSS)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d6e4d893-1f14-4522-ac20-0c73b18c72a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 9f02b3d4ce2073110c55af4b567b0e3b5a88404f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-symantec-web-security-service-wss"></a>Руководство по интеграции Azure Active Directory с Symantec Web Security Service (WSS)

В этом учебнике вы узнаете, как toointegrate вашей компании Symantec Web безопасности Service (WSS) учетной записи с вашей учетной записью Azure Active Directory (Azure AD) WSS для проверки подлинности пользователь подготовлен в hello Azure AD с использованием проверки подлинности SAML и принудительное применение пользователя или правила политик на уровне группы.

Интеграция службы безопасности Symantec Web (WSS) с Azure AD предоставляет hello следующие преимущества:

- Управление hello конечных пользователей и групп, используемых вашей учетной записи WSS с портала Azure AD. 

- Разрешить hello конечным пользователям tooauthenticate сами WSS, используя свои учетные данные Azure AD.

- Включение принудительного применения hello пользователя и группы правил уровень политики, определенных в вашей учетной записи WSS.

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Symantec Web безопасности Service (WSS) необходимо hello следующих элементов:

- подписка Azure AD;
- Учетная запись Symantec Web Security Service (WSS)

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется WSS учетной записью, используются в настоящее время для производственных целей.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Без крайней необходимости не используйте для этого теста учетную запись WSS, которая используется в производственных целях.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В этом учебнике вы настроите к Azure AD tooenable единого входа tooWSS с помощью учетных данных пользователя hello, определенных в вашей учетной записи Azure AD.
Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление приложения hello Symantec Web безопасности Service (WSS) из коллекции hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-symantec-web-security-service-wss-from-hello-gallery"></a>Добавление службы безопасности Symantec Web (WSS) из коллекции hello
tooconfigure hello Интеграция безопасности службы Symantec Web (WSS) в Azure AD, вы должны tooadd Symantec Web безопасности Service (WSS) из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Symantec Web безопасности Service (WSS) из коллекции hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Кнопка Hello Azure Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Hello корпоративных приложений колонку][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Кнопка нового приложения Hello][3]

4. Введите в поле поиска hello **Symantec Web безопасности Service (WSS)**выберите **Symantec Web безопасности Service (WSS)** из панели результатов щелкните **добавить** кнопку tooadd hello приложение.

    ![Symantec Web безопасности Service (WSS) в списке результатов hello](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD

В этом разделе описана настройка и проверка единого входа Azure AD в Symantec Web Security Service (WSS) с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow какие пользователь аналог hello в Symantec Web безопасности Service (WSS) является tooa в Azure AD. Иными словами связи между пользователя Azure AD и связанных пользователей hello в Symantec Web безопасности Service (WSS) необходимо установить toobe.

В компании Symantec Web безопасности Service (WSS), присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и тестирования Azure AD единого входа с Symantec Web безопасности Service (WSS), необходимы следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Symantec Web безопасности Service (WSS)](#create-a-symantec-web-security-service-wss-test-user)**  -toohave аналог Саймон Britta в Symantec Web безопасности Service (WSS), являющийся представлением связанного toohello Azure AD пользователя.
4. **[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении службы безопасности Symantec Web (WSS).

**tooconfigure Azure AD единого входа с Symantec Web безопасности Service (WSS), выполните следующие шаги hello.**

1. В hello в hello портала Azure **Symantec Web безопасности Service (WSS)** странице интеграции приложения щелкните **единого входа**.

    ![Ссылка "Настройка единого входа"][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_samlbase.png)

3. На hello **Symantec Web безопасности службы (WSS) домена и URL-адреса** выполните следующие шаги hello:

    ![Информация о домене и URL-адресах для единого входа в службе Symantec Web Security Service (WSS)](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_url.png)

    а. В hello **идентификатор** текстовом поле введите URL-адрес hello:`https://saml.threatpulse.net:8443/saml/saml_realm`

    b. В hello **URL-адрес ответа** текстовом поле введите URL-адрес hello:`https://saml.threatpulse.net:8443/saml/saml_realm/bcsamlpost`

    > [!NOTE]
    > Обратитесь в службу hello [группа поддержки Symantec Web безопасности Service (WSS) клиента](https://www.symantec.com/contact-us) Если hello значений для hello **идентификатор** и **URL-адрес ответа** не работает ни в какой-либо причине.

4. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-symantec-tutorial/tutorial_general_400.png)
    
6. tooconfigure единого входа на hello стороне Symantec Web безопасности Service (WSS), см. электронную документацию toohello WSS. загружаются Hello **метаданные в формате XML** файла потребуется toobe импортируются в портал WSS hello. Обратитесь в службу hello [поддержки Symantec Web безопасности Service (WSS)](https://www.symantec.com/contact-us) Если вам нужна помощь с конфигурацией hello на портале WSS hello.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD

Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

   ![Создание тестового пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-symantec-tutorial/create_aaduser_01.png)

2. слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-symantec-tutorial/create_aaduser_02.png)

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-symantec-tutorial/create_aaduser_03.png)

4. В hello **пользователя** диалогового окна выполните следующие шаги hello:

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-symantec-tutorial/create_aaduser_04.png)

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.

    c. Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.

    d. Щелкните **Создать**.
 
### <a name="create-a-symantec-web-security-service-wss-test-user"></a>Создание тестового пользователя Symantec Web Security Service (WSS)

В этом разделе описано, как создать пользователя Britta Simon в Symantec Web Security Service (WSS). Hello соответствующего конечного пользователя можно создать вручную на портале WSS hello или можно подождать hello пользователи и группы подготовки на портале WSS toohello toobe синхронизации Azure AD hello через несколько минут (~ 15 минут). Перед использованием единого входа необходимо создать и активировать пользователей. общедоступный IP-адрес Hello машины hello конечного пользователя, который будет использоваться toobrowse веб-сайтов также должны toobe подготовки портала hello Symantec Web безопасности Service (WSS).

> [!NOTE]
> Проверьте [щелкните здесь](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) tooget компьютере открытый IP-адрес.

### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooSymantec службы Web Security (WSS).

![Назначение пользователям ролей hello][200] 

**tooassign tooSymantec Britta Simon Web безопасности Service (WSS) выполните hello следующие шаги.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Symantec Web безопасности Service (WSS)**.

    ![ссылка Symantec Web безопасности Service (WSS) Hello в списке приложений hello](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_app.png)  

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Hello ссылку «Пользователи и группы»][202]

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![область назначения, добавьте Hello][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

В этом разделе вы сможете протестировать hello единого входа функции настройки вашей toouse WSS учетной записи в Azure AD для проверки подлинности SAML.

После настройки веб-браузера tooproxy трафика, tooWSS при открытии веб-браузере и повторите toobrowse tooa сайта, то вы будете перенаправлены toohello входа Azure на странице. Введите учетные данные hello hello тестирования конечного пользователя, предоставленное в hello Azure AD (то есть, BrittaSimon) и связанный пароль. Пройдя проверку подлинности, вы будете иметь доступ toobrowse toohello веб-сайт, выбранный. Следует ли создать правила политики на tooblock стороне hello WSS BrittaSimon с просмотра tooa конкретного сайта, при попытке сайта toothat toobrowse имени пользователя BrittaSimon должен отобразиться страница блок WSS hello.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_203.png

