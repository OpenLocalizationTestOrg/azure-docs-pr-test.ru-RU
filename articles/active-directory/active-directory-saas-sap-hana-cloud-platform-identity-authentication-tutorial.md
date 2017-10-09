---
title: "Руководство по интеграции Azure Active Directory с приложением SAP HANA Cloud Platform Identity Authentication | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и SAP HANA облачной платформы удостоверений проверки подлинности."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1c1320d1-7ba4-4b5f-926f-4996b44d9b5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 2142770779ddb745555b47fc85b5457b573f9506
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform-identity-authentication"></a>Руководство по интеграции Azure Active Directory с приложением SAP HANA Cloud Platform Identity Authentication

В этом учебнике вы узнаете, как toointegrate SAP HANA облачной платформы удостоверений проверки подлинности в Azure Active Directory (Azure AD). Проверка подлинности облачной платформы SAP HANA идентификатора используется в качестве прокси-сервера поставщика удостоверений tooaccess приложения SAP с помощью Azure AD как hello основного поставщика удостоверений.

Интеграция проверки подлинности облачной платформы SAP HANA удостоверений с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooSAP приложения
- Можно включить на пользователей tooautomatically get tooSAP вошедшего приложения единого входа (SSO) с их учетными записями Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello классический портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).


## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с помощью проверки подлинности облачной платформы SAP HANA удостоверений необходимо hello следующих элементов:

- подписка Azure AD;
- Подписка на **SAP HANA Cloud Platform Identity Authentication** с поддержкой единого входа.


>[!NOTE] 
>в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.
>

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не следует использовать рабочую среду при отсутствии необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.

Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление проверки подлинности облачной платформы SAP HANA удостоверений из галереи hello
2. Настройка и проверка единого входа Azure AD.

Прежде чем углубляться в технические подробности hello, это жизненно важных toounderstand hello концепции, с которыми вы будете toolook на. Hello федерации проверки подлинности облачной платформы SAP HANA удостоверений и Azure Active Directory позволяет tooimplement единого входа для приложений или служб, защищенных AAD (в качестве поставщика удостоверений) с приложениями SAP и службах, защищенных облачной платформы SAP HANA удостоверение Проверка подлинности.

В настоящее время проверки подлинности облачной платформы SAP HANA удостоверение выступает в качестве поставщика удостоверений прокси tooSAP приложения. В свою очередь, Azure Active Directory выступает в качестве hello начальные поставщика удостоверений в этой программе установки. 

Привет, следующая схема иллюстрирует это:    

![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/architecture-01.png)

При такой конфигурации клиент SAP HANA Cloud Platform Identity Authentication будет настроен как надежное приложение в Azure Active Directory. 

Все приложения SAP и службы будут tooprotect через таким образом впоследствии настраиваются в консоли управления для проверки подлинности облачной платформы SAP HANA удостоверение hello!

Это означает, что авторизации для предоставления доступа tooSAP приложений и служб месте tootake потребности в проверке подлинности облачной платформы SAP HANA удостоверение для установки (как противоположность tooconfiguring авторизации в Azure Active Directory).

Путем настройки проверки подлинности облачной платформы SAP HANA удостоверения как приложение через hello Azure Active Directory Marketplace, нет необходимости tootake заботиться о настройке необходимых утверждений отдельных / утверждений SAML и преобразования необходимости tooproduce действительный токен проверки подлинности для приложений SAP.

>[!NOTE] 
>В настоящее время единый вход для интернет-решений был проверен только обеими сторонами. Потоки, необходимые для связи "приложение — API" и "API — API", работают, но они еще не проверялись. Они будут проверены в ходе последующих действий.
>

## <a name="add-sap-hana-cloud-platform-identity-authentication-from-hello-gallery"></a>Добавление проверки подлинности облачной платформы SAP HANA удостоверений из коллекции hello
tooconfigure hello интеграции проверки подлинности облачной платформы SAP HANA удостоверений в Azure AD, вы должны tooadd проверки подлинности облачной платформы SAP HANA удостоверений из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd аутентификации SAP HANA облачной платформы удостоверений из галереи hello выполните следующие шаги hello.**

1. В hello [ **портал управления Azure**](https://portal.azure.com)на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. Нажмите кнопку **добавить** кнопку в верхней части hello диалогового окна "hello".

    ![Приложения][3]

4. Введите в поле поиска hello **проверки подлинности облачной платформы SAP HANA удостоверение**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_01.png)

5. В панели результатов hello выберите **проверки подлинности облачной платформы SAP HANA удостоверение**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_02.png)


##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в SAP HANA Cloud Platform Identity Authentication с использованием тестового пользователя Britta Simon.

Для toowork единого входа Azure AD необходима tooknow пользователь аналог какие hello в проверке подлинности облачной платформы SAP HANA удостоверение является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в SAP HANA облачной платформы удостоверений проверки подлинности должен установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в проверке подлинности облачной платформы SAP HANA удостоверение.

tooconfigure и тестирования единого входа Azure AD, с проверкой подлинности облачной платформы SAP HANA удостоверение, необходимы следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD единого входа](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя проверки подлинности облачной платформы SAP HANA удостоверение](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)**  -toohave аналог Саймон Britta в SAP HANA облачной платформы удостоверений проверки подлинности, который является представлением ей связанного toohello Azure AD.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-sso"></a>Настройка единого входа Azure AD

В этом разделе Включить единый вход Azure AD на портале управления Azure hello и настроить единый вход в приложение проверки подлинности облачной платформы SAP HANA удостоверений.

Проверка подлинности облачной платформы SAP HANA удостоверения приложения ожидает утверждения SAML hello в определенном формате. Вы можете управлять hello значения этих атрибутов из hello»**атрибуты пользователя**» на странице интеграции приложения. пример Hello следующий снимок экрана для этого.

![Настройка единого входа](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_03.png)

**tooconfigure SSO Azure AD с SAP HANA облачной платформы удостоверений проверки подлинности, выполните следующие шаги hello.**

1. На портале управления Azure hello на hello **проверки подлинности облачной платформы SAP HANA удостоверение** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна, как **режим** выберите **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа][5]

3. В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалоговое окно, если для приложения SAP требуется атрибут, например «firstName». В диалоговом окне атрибутов токена SAML hello добавьте атрибут «firstName» hello.
 1. Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.
 
    ![Настройка единого входа][6]

    ![Настройка единого входа](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_05.png)
 2. В hello **имя атрибута** в текстовое поле имя атрибута типа hello «firstName».
 3. Из hello **значение атрибута** список, выберите hello значение атрибута «user.givenname».
 4. Нажмите кнопку **ОК**.

4. На hello **URL-адреса и SAP HANA облачной платформы удостоверений проверки подлинности домена** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_06.png)
 1. В hello **на URL-адрес входа** текстовом поле введите знак hello на URL-адрес для приложения hello SAP.
 2. В hello **идентификатор** текстовое поле, значение типа hello следующий шаблон:`<entity-id>.accounts.ondemand.com` 
    * Если вы не знаете это значение, следуйте документации проверки подлинности облачной платформы SAP HANA удостоверение hello в [конфигурации SAML 2.0 клиента](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html).

5. На hello **настройки проверки подлинности для облачной платформы SAP HANA удостоверение** щелкните **Настройка SAP HANA облачной платформы удостоверений проверки подлинности** tooopen **Настройкавхода** диалогового окна. Щелкните на **метаданных XML SAML** и сохраните файл hello на своем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_07.png) 

    ![Настройка единого входа](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_08.png)

6. tooget единого входа, настроенному для вашего приложения перейдите tooSAP HANA облачной платформы удостоверений проверки подлинности консоли администрирования. URL-адрес Hello имеет hello следующий шаблон:`https://<tenant-id>.accounts.ondemand.com/admin`
 * Следуйте hello документации для проверки подлинности облачной платформы SAP HANA удостоверение слишком[Настройка Microsoft Azure AD в качестве организации поставщика удостоверений в SAP HANA облачной платформы удостоверений проверки подлинности](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html). 

7. На портале управления Azure hello щелкните **Сохранить** кнопки.
8. По-прежнему hello, выполнив действия, только в том случае, если нужно tooadd и Включение единого входа для другого приложения SAP. Повторите шаги в разделе hello раздел «Добавление SAP HANA облачной платформы удостоверений проверки подлинности из галереи hello» tooadd другой экземпляр SAP HANA облачной платформы удостоверений проверки подлинности.
9. На портале управления Azure hello на hello **проверки подлинности облачной платформы SAP HANA удостоверение** странице интеграции приложения щелкните **входа на связанный**.

    ![Настройка связанного единого входа](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/linked_sign_on.png)
10. Сохраните конфигурацию hello.

>[!NOTE] 
>новое приложение Hello будет использовать hello настройку единого входа для предыдущего SAP приложения hello. Убедитесь, что вы используйте hello же корпоративной поставщиков удостоверений в hello проверки подлинности консоли администрирования облачной платформы SAP HANA удостоверений.
>

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Hello цель этого раздела — toocreate тестового пользователя на новом портале hello вызывается Саймон Britta.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал управления Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_01.png) 

2. Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_02.png) 

3. Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_04.png) 
  1. В hello **имя** введите **BrittaSimon**.
  2. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.
  3. Выберите **Показать пароль** и запишите значение hello hello **пароль**.
  4. Щелкните **Создать**. 

### <a name="create-a-sap-hana-cloud-platform-identity-authentication-test-user"></a>Создание тестового пользователя SAP HANA Cloud Platform Identity Authentication

Toocreate проверки подлинности облачной платформы SAP HANA удостоверение пользователя не требуется. Пользователи находятся в хранилище пользователя hello Azure AD могут использовать функциональные возможности Единого hello.

Проверка подлинности облачной платформы SAP HANA идентификатора поддерживает параметр hello федерации удостоверений. Этот параметр позволяет toocheck приложения hello, если проверку подлинности поставщиком hello корпоративными удостоверениями пользователей hello существует в hello хранилища из SAP HANA облачной платформы удостоверений проверки подлинности пользователя. 

При параметрах по умолчанию hello hello федерации удостоверений параметр отключен. При включении федерации удостоверений hello только тех пользователей, импортируемые в SAP HANA облачной платформы удостоверений проверки подлинности, приложение может tooaccess hello. 

Дополнительные сведения о том, как tooenable или отключите федерации удостоверений с SAP HANA облачной платформы удостоверений проверки подлинности, отображается включить федерацию удостоверений с аутентификацией SAP HANA облачной платформы удостоверений в [Настройка федерации удостоверений с hello хранилища из SAP HANA облачной платформы удостоверений проверки подлинности пользователя. ](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html).

### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа, предоставляя свой доступ tooSAP HANA облачной платформы удостоверений проверки подлинности.

![Назначение пользователя][200] 

**tooassign tooSAP Britta Simon HANA облачной платформы удостоверений проверки подлинности, выполните следующие шаги hello.**

1. На портале управления Azure hello, открыть представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **проверки подлинности облачной платформы SAP HANA удостоверение**.

    ![Настройка единого входа](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_09.png)

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    

### <a name="test-single-sign-on"></a>Проверка единого входа

В этом разделе Проверьте конфигурацию единого входа Azure AD с помощью панели доступа hello.

Если щелкнуть плитку проверки подлинности облачной платформы SAP HANA удостоверение hello в hello панели доступа, следует получать автоматически вошедшего tooyour проверки подлинности облачной платформы SAP HANA удостоверение приложения.


## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_06.png

[100]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_203.png