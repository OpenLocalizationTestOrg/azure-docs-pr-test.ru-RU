---
title: "Руководство по интеграции Azure Active Directory c Google Apps в Azure | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Google Apps."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 38a6ca75-7fd0-4cdc-9b9f-fae080c5a016
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 2093b5ab605ec0d7bbefe7a78e1eede34d756f53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-google-apps"></a>Руководство по интеграции Azure Active Directory с Google Apps

В этом учебнике вы узнаете, как toointegrate Google Apps с Azure Active Directory (Azure AD).

Интеграция Google Apps с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooGoogle приложений
- Можно включить на пользователей tooautomatically get вошедшего tooGoogle приложения (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если требуется tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. раздел [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Google Apps, требуется hello следующих элементов:

- подписка Azure AD;
- подписка Google Apps с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="video-tutorial"></a>Видеоруководство
Как tooEnable Single Sign-On tooGoogle приложений в течение 2 минут:

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Enable-single-sign-on-to-Google-Apps-in-2-minutes-with-Azure-AD/player]

## <a name="frequently-asked-questions"></a>Часто задаваемые вопросы
1. **Вопрос. Поддерживают ли Chromebooks и другие устройства Chrome единый вход Azure AD?**
   
    Ответ Да, пользователи получают доступ toosign в их Chromebook устройства, используя свои учетные данные Azure AD. Сведения о том, почему учетные данные могут быть запрошены у пользователей дважды, см. в этой [статье о поддержке Google Apps](https://support.google.com/chrome/a/answer/6060880).

2. **Вопрос. Если включить единый вход, будет пользователей быть может toouse их toosign учетные данные Azure AD в любой продукт Google, например аудитории Google GMail, Google диске, YouTube и т. д.**
   
    О: Да, в зависимости от [какие Google apps](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) выберите tooenable или отключить для вашей организации.

3. **Вопрос. Можно ли включить единый вход только для подмножества пользователей Google Apps?**
   
    Ответ нет, Включение единого входа немедленно требуется все к Google Apps пользователей tooauthenticate с свои учетные данные Azure AD. Так как Google Apps не поддерживает наличие нескольких поставщиков удостоверений, hello поставщика удостоверений Google Apps среды может быть Azure AD или Google--, но не оба hello то же время.

4. **Вопрос. Если пользователь выполнил вход в Windows, являются они автоматически проверять подлинность приложений tooGoogle без будет выведено приглашение для ввода пароля?**
   
    Ответ. Существует два варианта включения этого сценария. Во-первых, пользователи могут входить в устройства Windows 10 посредством [присоединения к Azure Active Directory](active-directory-azureadjoin-overview.md). Кроме того, пользователи могут войти в устройства Windows, присоединенных к домену tooan локальной Active Directory, который был включен для единого входа tooAzure AD через [служб федерации Active Directory (AD FS)](active-directory-aadconnect-user-signin.md) развертывания. Оба варианта требуют tooperform hello инструкциям hello, следуя учебника tooenable единый вход между Azure AD и Google Apps.

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Google Apps из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-google-apps-from-hello-gallery"></a>Добавление Google Apps из галереи hello
tooconfigure hello интеграция Google Apps в Azure AD, вы должны tooadd Google Apps от hello коллекции tooyour список управляемых приложений SaaS.

**tooadd Google Apps из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **Google Apps**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_search.png)

5. В панели результатов hello выберите **Google Apps**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Google Apps с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Google Apps является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в Google Apps должен установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Google Apps.

tooconfigure и теста Azure AD единого входа с Google Apps, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Google Apps](#creating-a-google-apps-test-user)**  -toohave аналог Саймон Britta в Google Apps, представление связанных toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе вы включите Azure AD единым входом в портал Azure hello и настроить единый вход в приложение Google Apps.

**tooconfigure Azure AD единого входа с Google Apps, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Google Apps** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_samlbase.png)

3. На hello **URL-адреса и домен Google Apps** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_url.png)

    В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://mail.google.com/a/<yourdomain>`

    > [!NOTE] 
    > Это значение приведено для справки. Обновите значение hello с hello фактический URL-адрес входа. обратитесь в службу hello [службу поддержки Google](https://www.google.com/contact/).
 
4. На hello **сертификат подписи SAML** щелкните **сертификат** и сохраните hello сертификата на компьютере.

    ![Настройка единого входа](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-google-apps-tutorial/tutorial_general_400.png)

6. На hello **Google Apps конфигурации** щелкните **настроить Google Apps** tooopen **Настройка входа** окна. Копировать hello **URL-адрес выхода, единого входа службы URL-адрес SAML и изменение пароля URL-адреса** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_configure.png) 

7. Откройте новую вкладку в браузере и войдите с hello [консоли администрирования приложения Google](http://admin.google.com/) с помощью учетной записи администратора.

8. Выберите пункт **Безопасность**. Если вы не видите ссылку hello, они могут быть скрыты в hello **другие элементы** меню hello нижней части экрана приветствия.
   
    ![Выбор элемента "Безопасность"][10]

9. На hello **безопасности** щелкните **настройки единого входа (SSO).**
   
    ![Выбор элемента "Единый вход"][11]

10. Выполните следующие изменения конфигурации hello.
   
    ![Настройка единого входа][12]
   
    а. Выберите **Setup SSO with third party identity provider**(Настройка единого входа с помощью стороннего поставщика удостоверений).

    b. В **входа в URL-адрес страницы** поля в Google Apps, вставьте значение hello **единого входа URL-адрес службы**, который вы скопировали из портала Azure.

    c. В hello **URL-адрес страницы выхода** поля в Google Apps, вставьте значение hello **URL-адрес выхода**, который вы скопировали из портала Azure. 

    d. В hello **изменение пароля URL-адреса** поля в Google Apps, вставьте значение hello **изменение пароля URL-адреса**, который вы скопировали из портала Azure. 

    д. В Google Apps для hello **сертификат проверки**, отправить hello сертификат, загруженный с портала Azure.

    f. Нажмите кнопку **Сохранить изменения**.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
 
### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-google-apps-test-user"></a>Создание тестового пользователя Google Apps

Цель этого раздела Hello — toocreate пользователя с именем Britta Simon в программном обеспечении Google Apps. Google Apps поддерживает JIT-подготовку. Эта функция включена по умолчанию. В этом разделе никакие действия с вашей стороны не требуются. Если пользователь еще не существует в программном обеспечении Google Apps, новый создается при попытке tooaccess программного обеспечения Google Apps.

>[!NOTE] 
>Если вам требуется toocreate пользователя вручную, обратитесь в службу hello [службу поддержки Google](https://www.google.com/contact/).

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooGoogle приложений.

![Назначение пользователя][200] 

**tooassign Britta Simon tooGoogle приложений, выполните hello следующие шаги.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Google Apps**.

    ![Настройка единого входа](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе Здравствуйте, единого входа параметры, откройте панель доступа по адресу tootest [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md), затем войдите в hello тестовую учетную запись и нажмите кнопку **Google Apps** плитки в панели доступа hello.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Руководство по настройке Google Apps для автоматической подготовки пользователей](active-directory-saas-google-apps-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_203.png

[0]: ./media/active-directory-saas-google-apps-tutorial/azure-active-directory.png

[5]: ./media/active-directory-saas-google-apps-tutorial/gapps-added.png
[6]: ./media/active-directory-saas-google-apps-tutorial/config-sso.png
[7]: ./media/active-directory-saas-google-apps-tutorial/sso-gapps.png
[8]: ./media/active-directory-saas-google-apps-tutorial/sso-url.png
[9]: ./media/active-directory-saas-google-apps-tutorial/download-cert.png
[10]: ./media/active-directory-saas-google-apps-tutorial/gapps-security.png
[11]: ./media/active-directory-saas-google-apps-tutorial/security-gapps.png
[12]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-config.png
[13]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-confirm.png
[14]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-email.png
[15]: ./media/active-directory-saas-google-apps-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-tutorial/gapps-api-enabled.png
[17]: ./media/active-directory-saas-google-apps-tutorial/add-custom-domain.png
[18]: ./media/active-directory-saas-google-apps-tutorial/specify-domain.png
[19]: ./media/active-directory-saas-google-apps-tutorial/verify-domain.png
[20]: ./media/active-directory-saas-google-apps-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-another.png
[23]: ./media/active-directory-saas-google-apps-tutorial/apps-gapps.png
[24]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-tutorial/gapps-auth.png
[29]: ./media/active-directory-saas-google-apps-tutorial/assign-users.png
[30]: ./media/active-directory-saas-google-apps-tutorial/assign-confirm.png