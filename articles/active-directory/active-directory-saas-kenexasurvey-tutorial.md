---
title: "Учебник. Интеграция Azure Active Directory с IBM Kenexa Survey Enterprise | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и корпоративный опроса Kenexa IBM."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c7aac6da-f4bf-419e-9e1a-16b460641a52
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: cf7ed886b4418ac396ca7056827ee10fd7a19ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ibm-kenexa-survey-enterprise"></a>Руководство по интеграции Azure Active Directory с IBM Kenexa Survey Enterprise

В этом учебнике вы узнаете, как toointegrate Enterprise опроса Kenexa IBM с Azure Active Directory (Azure AD).

Интеграция Enterprise опроса Kenexa IBM с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooIBM Kenexa опроса предприятия.
- Tooautomatically пользователей при входе в tooIBM Kenexa опроса Enterprise можно включить с помощью единого входа (SSO) с помощью своих учетных записей Azure AD.
- Можно управлять учетными записями в одном централизованном месте: hello портал Azure.

Если требуется tooknow Дополнительные сведения о программное обеспечение как услуга (SaaS) интеграции приложений с Azure AD, см. раздел [доступ к приложению и единый вход в Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с IBM Kenexa опроса предприятия необходимо hello следующих элементов:

- подписка Azure AD;
- подписка на IBM Kenexa Survey Enterprise с поддержкой единого входа.

> [!NOTE]
> При тестировании hello шаги в этом учебнике, рекомендуется не использовать в производственной среде.

tootest hello шаги в этом учебнике, придерживайтесь следующих рекомендаций:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарии, описанные в учебнике hello состоит из двух основных компонентов:

* Добавление IBM Kenexa опроса Enterprise из коллекции hello
* Настройка и проверка единого входа Azure AD.

## <a name="add-ibm-kenexa-survey-enterprise-from-hello-gallery"></a>Добавление IBM Kenexa опроса Enterprise из коллекции hello
tooconfigure интеграции IBM Kenexa опроса Enterprise hello в Azure AD, добавить IBM Kenexa опроса Enterprise из hello коллекции tooyour список управляемых приложений SaaS.

tooadd Enterprise опроса IBM Kenexa из галереи hello hello следующие:

1. В hello [портал Azure](https://portal.azure.com)в левой области hello, щелкнув hello **Azure Active Directory** кнопки. 

    ![Кнопка Hello Azure Active Directory][1]

2. Перейдите в колонку **Корпоративные приложения** и выберите **Все приложения**.

    ![Hello корпоративных приложений колонку][2]
    
3. tooadd приложение, нажмите кнопку hello **новое приложение** кнопки.

    ![Кнопка нового приложения Hello][3]

4. Введите в поле поиска hello **Enterprise опроса IBM Kenexa**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_search.png)

5. В списке результатов hello выберите **Enterprise опроса IBM Kenexa**и нажмите кнопку hello **добавить** кнопку tooadd приложения hello.

    ![IBM Kenexa опроса Enterprise в списке результатов hello](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в IBM Kenexa Survey Enterprise с использованием тестового пользователя Britta Simon.

Для toowork единого входа Azure AD должен tooidentify hello IBM Kenexa опроса Enterprise пользователя аналога в Azure AD. Иными словами, в Azure AD необходимо установить связь между пользователем Azure AD и соответствующим пользователем в IBM Kenexa Survey Enterprise.

tooestablish hello связи, назначить значение hello hello **имя пользователя** IBM Kenexa опроса предприятия в качестве значения hello hello **Username** в Azure AD.

tooconfigure и тестирования SSO Azure AD с IBM Kenexa опроса Enterprise, полный hello блоки в следующих двух разделах hello.

### <a name="configure-azure-ad-sso"></a>Настройка единого входа Azure AD

В этом разделе Включить единый вход Azure AD в hello портал Azure и настройки единого входа в вашем приложении Enterprise опроса Kenexa IBM, выполнив hello ниже:

1. В hello в hello портала Azure **Enterprise опроса IBM Kenexa** странице интеграции приложения щелкните **единого входа**.

    ![Ссылка для настройки единого входа для IBM Kenexa Survey Enterprise][4]

2. В hello **единого входа** диалогового окна hello **режим** выберите **входа на базе SAML** tooenable единого входа.
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_samlbase.png)

3. В hello **URL-адреса и домена предприятия опроса Kenexa IBM** выполните следующие шаги hello:

    ![Сведения о домене и URL-адресах IBM Kenexa Survey Enterprise](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_url.png)

    а. В hello **идентификатор** введите URL-адрес с hello следующий шаблон:`https://surveys.kenexa.com/<companycode>`

    b. В hello **URL-адрес ответа** введите URL-адрес с hello следующий шаблон:`https://surveys.kenexa.com/<companycode>/tools/sso.asp`

    > [!NOTE] 
    > Hello выше значения не являются реальными. Дополнить фактический идентификатор hello и URL-адрес ответа. фактические значения, обратитесь в службу hello hello tooobtain [группа поддержки Enterprise опроса IBM Kenexa](https://www.ibm.com/support/home/?lnk=fcw).

4. В разделе **сертификат подписи SAML**, нажмите кнопку **сертификата (Base64)**и сохраните файл tooyour hello сертификат компьютера.

    ![ссылку для скачивания сертификата (Base64) Hello](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_certificate.png) 

    Hello IBM Kenexa опроса корпоративное приложение ожидает утверждения безопасности утверждения Markup Language (SAML) tooreceive hello в определенном формате, поэтому требуется вы tooadd настраиваемого атрибута сопоставления toohello Настройка атрибутов токена SAML. Hello значение утверждения идентификатора пользователя hello в ответ hello должно соответствовать hello идентификатор единого входа, настроенную в системе Kenexa hello. toomap hello идентификатор соответствующего пользователя в вашей организации, как протокол датаграмм SSO Интернета (IDP), работа с hello [группа поддержки Enterprise опроса IBM Kenexa](https://www.ibm.com/support/home/?lnk=fcw). 

    По умолчанию Azure AD задает идентификатор пользователя hello как значение имени участника (UPN) пользователя hello. Можно изменить это значение на hello **атрибута** вкладки, как показано на следующий снимок экрана приветствия. Интеграция Hello работает только после завершения сопоставления правильно hello.
    
    ![Атрибуты пользователя Hello-диалоговое окно](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_attribute.png) 

5. Щелкните **Сохранить**.

    ![Настройка Hello единым входом кнопку Сохранить](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_400.png)

6. tooopen hello **Настройка входа** окна в разделе **конфигурация предприятия опроса IBM Kenexa**, нажмите кнопку **настроить корпоративный опроса IBM Kenexa**. 
 
    ![Настройка корпоративного опроса IBM Kenexa ссылку Hello](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_configure.png)

7. Копировать hello **URL-адрес выхода**, **идентификатор сущности SAML**, и **SAML единого входа URL-адрес службы** значения из hello **краткий справочник** раздела.

8. В hello **Настройка входа** окна в разделе **краткий справочник**, hello копирования **URL-адрес выхода**, **идентификатор сущности SAML**, и  **SAML единого входа URL-адрес службы** значения.

9. tooconfigure единого входа на hello **Enterprise опроса IBM Kenexa** стороны, отправьте загружаются hello **сертификата (Base64)**, **URL-адрес выхода**, **идентификатор сущности SAML**, и **SAML единого входа URL-адрес службы** значения toohello [группа поддержки Enterprise опроса IBM Kenexa](https://www.ibm.com/support/home/?lnk=fcw).

> [!TIP]
> Можно ссылаться tooa четкими версии этими инструкциями в hello [портал Azure](https://portal.azure.com) при настройке приложения hello. После добавления приложение hello с hello **Active Directory** > **корпоративных приложений** просто щелкните hello **единого входа** вкладку, а затем получить доступ к Hello внедренных документации с помощью hello **конфигурации** раздел в конце hello. toolearn Дополнительные сведения о функции hello внедренные документации, в разделе [Azure AD внедренных документации](https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
В этом разделе создайте тестового пользователя Саймон Britta в hello портал Azure, выполнив hello ниже:

![Создание тестового пользователя Azure AD][100]

1. В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_01.png) 

2. слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.
    
    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.
 
    ![Кнопка "Добавить" Hello](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_03.png) 

4. В hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.

    c. Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.

    d. Щелкните **Создать**.
 
### <a name="create-an-ibm-kenexa-survey-enterprise-test-user"></a>Создание тестового пользователя IBM Kenexa Survey Enterprise

В этом разделе описано, как создать пользователя Britta Simon в приложении IBM Kenexa Survey Enterprise. 

toocreate пользователей в hello IBM Kenexa опроса корпоративной системы и карты hello идентификатор единого входа для них, можно работать с hello [группа поддержки Enterprise опроса IBM Kenexa](https://www.ibm.com/support/home/?lnk=fcw). Это значение идентификатора единого входа также должен быть сопоставлен toohello значение идентификатора пользователя из Azure AD. Можно изменить этот параметр по умолчанию на hello **атрибута** вкладки.

### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя

В этом разделе включите пользователя toouse Britta Simon единого входа Azure путем предоставления доступа tooIBM Kenexa опроса Enterprise.

![Назначение пользователям ролей hello][200] 

пользователь tooassign Britta Simon tooIBM Kenexa опроса Enterprise, hello следующие:

1. В hello портал Azure, откройте hello **приложений** просмотреть, перейдите toohello **каталога** представление, выберите **корпоративных приложений**и нажмите кнопку **все приложения**.

    ![Здравствуйте, «Корпоративных приложений» и «Всех приложений» ссылки][201] 

2. В hello **приложений** выберите **Enterprise опроса IBM Kenexa**.

    ![ссылка на корпоративный опроса Kenexa IBM Hello в списке приложений hello](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_app.png) 

3. Hello левой панели щелкните **пользователей и групп**.

    ![Hello ссылку «Пользователи и группы»][202] 

4. Нажмите кнопку hello **добавить** кнопки и затем в hello **добавить назначение** выберите **пользователей и групп**.

    ![область назначения, добавьте Hello][203]

5. В hello **пользователей и групп** диалогового окна hello **пользователей** выберите **Britta Simon**.

6. В hello **пользователей и групп** диалоговое окно, нажмите кнопку hello **выберите** кнопки.

7. В hello **добавить назначение** диалоговое окно, нажмите кнопку hello **назначить** кнопки.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

В этом разделе можно проверить конфигурацию единого входа Azure AD с помощью панели доступа hello.

При нажатии кнопки hello **Enterprise опроса Kenexa IBM** плитки в Здравствуйте панели доступа, вы должны автоматически входить в tooyour IBM Kenexa опроса корпоративного приложения.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по toointegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_203.png

 
