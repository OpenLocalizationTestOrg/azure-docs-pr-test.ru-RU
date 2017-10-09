---
title: "Руководство по интеграции Azure Active Directory с ServiceNow | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и ServiceNow и ServiceNow, экспресс-выпуск."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 1d8eb99e-8ce5-4ba4-8b54-5c3d9ae573f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: df6a07dd1aa437198fbdb9d0a04ea14f3a320249
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicenow"></a>Руководство: интеграция Azure Active Directory с ServiceNow
В этом учебнике вы узнаете, как toointegrate ServiceNow и ServiceNow, экспресс-выпуск с Azure Active Directory (Azure AD).

Интеграция с Azure AD ServiceNow и ServiceNow Express предоставляет hello следующие преимущества:

* Можно управлять в Azure AD, имеющего доступ tooServiceNow и ServiceNow, экспресс-выпуск
* Можно разрешить пользователям tooautomatically get вошедшего tooServiceNow и ServiceNow Express (Single Sign-On) с их учетными записями Azure AD
* Можно управлять учетными записями в одном централизованном месте - hello классический портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования
tooconfigure интеграция Azure AD с ServiceNow и ServiceNow Express необходимо hello следующих элементов:

* подписка Azure AD;
* Экземпляр или клиент ServiceNow версии Calgary или выше (для ServiceNow).
* Экземпляр ServiceNow Express версии Helsinki или выше (для ServiceNow Express).
* Hello клиента ServiceNow должен иметь hello [несколько единого входа на подключаемый модуль поставщика](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) включена. Это можно сделать путем [отправки запроса на обслуживание](https://hi.service-now.com). 

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.
> 
> 

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

* Не следует использовать рабочую среду при отсутствии необходимости.
* Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление ServiceNow из галереи hello
2. Настройка и проверка единого входа Azure AD в ServiceNow или ServiceNow Express.

## <a name="adding-servicenow-from-hello-gallery"></a>Добавление ServiceNow из галереи hello
tooconfigure hello интеграции ServiceNow или ServiceNow Express в Azure AD, вы должны tooadd ServiceNow из списка tooyour коллекции hello управляемых приложений SaaS. 

**tooadd ServiceNow из галереи hello, выполните следующие шаги hello.**

1. В hello **классический портал Azure**, на левой панели навигации hello, нажмите кнопку **Active Directory**. 
   
    ![Active Directory][1]
2. Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.
3. Щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.
   
    ![Приложения][2]
4. Нажмите кнопку **добавить** hello нижней части страницы приветствия.
   
    ![Приложения][3]
5. На hello **что вам требуется toodo** диалоговое окно, нажмите кнопку **добавить приложение из коллекции hello**.
   
    ![Приложения][4]
6. Введите в поле поиска hello **ServiceNow**.
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_01.png)
7. В области результатов hello выберите **ServiceNow**и нажмите кнопку **завершить** tooadd приложения hello.
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описано, как настроить и проверить единый вход Azure AD в ServiceNow или ServiceNow Express с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в ServiceNow является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в ServiceNow должен установить toobe.
Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в ServiceNow. tooconfigure и теста Azure AD единого входа с ServiceNow, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On для ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)**  -tooenable вашей toouse пользователи этой функции.
2. **[Настройка Azure AD Single Sign-On для быстрой ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow-express)**  -tooenable вашей toouse пользователи этой функции.
3. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
4. **[Создание тестового пользователя ServiceNow](#creating-a-servicenow-test-user)**  -toohave аналог Саймон Britta в ServiceNow, представление связанных toohello Azure AD ей.
5. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
6. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

> [!NOTE]
> Если вы хотите tooconfigure ServiceNow пропустите шаг 2. Аналогичным образом tooconfigure ServiceNow Express опустить шаг 1.
> 
> 

### <a name="configuring-azure-ad-single-sign-on-for-servicenow"></a>Настройка единого входа Azure AD в ServiceNow
1. Классического портала Azure AD hello на hello **ServiceNow** странице интеграции приложения щелкните **настроить единый вход** tooopen hello **Настройка единого входа** диалоговое окно .
   
    ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Настройка единого входа")

2. На hello **предпочитаемый как toosign пользователей на tooServiceNow** выберите **Microsoft Azure AD Single Sign-On**, а затем нажмите кнопку **Далее**.
   
    ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Настройка единого входа")

3. На hello **Настройка параметров приложения** выполните следующие шаги hello:
   
    ![Настройка URL-адреса приложения](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Настройка URL-адреса приложения")
   
    а. в hello **ServiceNow на URL-адрес входа** текстовое поле, введите URL-адрес, используемую приложением пользователей tooyour toosign на ServiceNow следующий шаблон hello: `https://<instance-name>.service-now.com`.
   
    b. В hello **идентификатор** текстовое поле, введите URL-адрес, используемую приложением пользователей tooyour toosign на ServiceNow следующий шаблон hello: `https://<instance-name>.service-now.com`.
   
    c. Щелкните **Далее**

4. toohave Azure AD, автоматически Настройка ServiceNow для проверки подлинности на основе SAML, введите имя экземпляра, имя пользователя администратора и пароль администратора ServiceNow в hello **автоматически настроить единый вход** форму и нажмите кнопку  *Настройка*. Обратите внимание, что указано имя пользователя администратора hello должен иметь hello **security_admin** роли, назначенные в ServiceNow для этого toowork. В противном случае toomanually настроить ServiceNow toouse Azure AD как поставщика удостоверений SAML, нажмите кнопку **вручную настроить приложение hello для единого входа**, нажмите кнопку **Далее** и завершения hello следующие шаги.
   
    ![Настройка URL-адреса приложения](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Настройка URL-адреса приложения")

5. На hello **Настройка единого входа в ServiceNow** щелкните **загрузки сертификата**, сохраните файл сертификата hello на локальном компьютере.
   
    ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Настройка единого входа")

6. Вход tooyour ServiceNow приложения от имени администратора.

7. Активировать hello *интеграция - несколько поставщика единого входа установщика* Здравствуйте, подключаемый модуль, выполнив следующие шаги:
   
    а. Hello hello левой панели навигации перейдите слишком**определения системы** статьи, а затем нажмите кнопку **подключаемых модулей**.
   
    ![Настройка URL-адреса приложения](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "Активация подключаемого модуля")
   
    b. Найдите *Integration - Multiple Provider Single Sign-On Installer* (Интеграция — установщик единого входа для нескольких поставщиков).
   
    ![Настройка URL-адреса приложения](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "Активация подключаемого модуля")
   
    c. Выберите hello подключаемого модуля. Щелкните правой кнопкой мыши и выберите **Activate/Upgrade** (Активировать или обновить).
   
    d. Нажмите кнопку hello **активировать** кнопки.

8. Hello hello левой панели навигации щелкните **свойства**.  
   
    ![Настройка URL-адреса приложения](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "Настройка URL-адреса приложения")

9. На hello **несколько свойств поставщика единого входа** диалоговое окно, выполните следующие шаги hello:
   
    ![Настройка URL-адреса приложения](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "Настройка URL-адреса приложения")
   
    а. Для параметра **Enable multiple provider SSO** (Включить единый вход для нескольких поставщиков) выберите значение **Yes** (Да).
   
    b. Как **включить ведение журнала отладки получен hello несколько поставщика единого входа интеграции**выберите **Да**.
   
    c. В **поле hello hello пользователем таблица...**  введите **имя_пользователя**.
   
    d. Щелкните **Сохранить**.

10. Hello hello левой панели навигации щелкните **x509 сертификаты**.
    
     ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "Настройка единого входа")

11. На hello **сертификаты X.509** диалоговое окно, нажмите кнопку **New**.
    
     ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "Настройка единого входа")

12. На hello **сертификаты X.509** диалоговое окно, выполните следующие шаги hello:
    
     ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Настройка единого входа")
    
     а. Нажмите кнопку **Создать**.
    
     b. В hello **имя** текстовом поле введите имя для конфигурации (например: **TestSAML2.0**).
    
     c. Установите флажок **Активно**.
    
     d. В поле **Format** (Формат) выберите **PEM**.
    
     д. В поле **Type** (Тип) выберите **Trust Store Cert** (Сертификат хранилища доверия).
    
     f. Откройте сертификат в кодировке Base64 в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **сертификат PEM** текстового поля.
    
     ж. Нажмите кнопку **Обновить**.

13. Hello hello левой панели навигации щелкните **Поставщики удостоверений**.
    
     ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "Настройка единого входа")

14. На hello **Поставщики удостоверений** диалоговое окно, нажмите кнопку **New**:
    
     ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "Настройка единого входа")

15. На hello **Поставщики удостоверений** диалоговое окно, нажмите кнопку **SAML2 обновление 1?**:
    
     ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "Настройка единого входа")

16. В диалоговом окне Свойства обновление 1 SAML2 hello выполните следующие шаги hello.
    
     ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "Настройка единого входа")

    а. в hello **имя** текстовом поле введите имя для конфигурации (например: **SAML 2.0**).

    b. В hello **поле пользователя** введите **электронной почты** или **имя_пользователя**, в зависимости от того, какое поле используется toouniquely идентификации пользователей в вашем развертывании ServiceNow. 

    > [!NOTE] 
    > Можно либо идентификатора пользователя hello Azure AD (имя участника-пользователя) tooemit настройки Azure AD или hello адрес электронной почты как hello уникальный идентификатор в токене SAML hello с переходом toohello **ServiceNow > атрибуты > Single Sign-On** раздела Здравствуйте классический портал Azure и сопоставление hello требуемого поля toohello **nameidentifier** атрибута. значение Hello, сохраненные для выбранного атрибута hello в Azure AD (например имя участника-пользователя) должно соответствовать hello значение, хранящееся в ServiceNow для hello введенные поля (например имя_пользователя)

    c. В классическом портале Azure AD hello, скопируйте hello **идентификатор поставщика удостоверений** значение, а затем вставьте его в hello **URL-адрес поставщика удостоверений** текстового поля.

    d. В классическом портале Azure AD hello, скопируйте hello **URL-адрес запроса проверки подлинности** значение, а затем вставьте его в hello **AuthnRequest поставщика удостоверений** текстового поля.

    д. В классическом портале Azure AD hello, скопируйте hello **URL-адрес службы единого выхода** значение, а затем вставьте его в hello **SingleLogoutRequest поставщика удостоверений** текстового поля.

    f. В hello **домашней страницы ServiceNow** текстовом поле введите URL-адрес hello вашей домашней страницы экземпляра ServiceNow.

    > [!NOTE] 
    > Домашняя страница экземпляра ServiceNow Hello составляется из вашего **URL-адрес клиента ServieNow** и **/navpage.do** (например:`https://fabrikam.service-now.com/navpage.do`).

    ж. В hello **идентификатор сущности или издателя** текстовом поле введите hello URL-адрес клиента ServiceNow.

    h. В hello **аудитории URL-адрес** в текстовое поле введите hello URL-адрес клиента ServiceNow. 

    i. В hello **привязки протокола для SingleLogoutRequest поставщика Удостоверений hello** введите **urn: oasis: имена: tc: SAML:2.0:bindings:HTTP-перенаправления**.

    j. В hello политики идентификатора имени текстового поля, введите **urn: oasis: имена: tc: SAML:1.1:nameid-формат: Неизвестная**.

    k. Снимите флажок **Create an AuthnContextClass**(Создать класс контекста проверки подлинности).

    l. В hello **метод AuthnContextClassRef**, тип `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`. Это действие требуется только для организаций на основе облака. Если используется локальная аутентификация AD FS или MFA, это значение указывать не нужно. 

    m. В текстовое поле **Clock Skew** (Разница в показаниях часов) введите **60**.

    n. В поле **Single Sign On Script** (Сценарий единого входа) выберите **MultiSSO_SAML2_Update1**.

    o. Как **x509 сертификат**выберите hello сертификат, созданный на предыдущем шаге hello.

    p. Нажмите кнопку **Submit**(Отправить). 

1. На классический портал hello Azure AD, выберите Подтверждение настройки единого входа hello и нажмите кнопку **Далее**. 
   
    ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Настройка единого входа")

2. На hello **единого входа для подтверждения** щелкните **завершить**.
   
    ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Настройка единого входа")

### <a name="configuring-azure-ad-single-sign-on-for-servicenow-express"></a>Настройка единого входа в Azure AD для ServiceNow Express
1. Классического портала Azure AD hello на hello **ServiceNow** странице интеграции приложения щелкните **настроить единый вход** tooopen hello **Настройка единого входа** диалоговое окно .
   
    ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Настройка единого входа")

2. На hello **предпочитаемый как toosign пользователей на tooServiceNow** выберите **Microsoft Azure AD Single Sign-On**, а затем нажмите кнопку **Далее**.
   
    ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Настройка единого входа")

3. На hello **Настройка параметров приложения** выполните следующие шаги hello:
   
    ![Настройка URL-адреса приложения](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Настройка URL-адреса приложения")
   
    а. в hello **ServiceNow на URL-адрес входа** текстовое поле, введите URL-адрес, используемую приложением пользователей tooyour toosign на ServiceNow следующий шаблон hello: `https://<instance-name>.service-now.com`.
   
    b. В hello **URL-адрес издателя** текстовое поле, введите URL-адрес, используемую приложением пользователей tooyour toosign на ServiceNow следующий шаблон hello `https://<instance-name>.service-now.com`.
   
    c. Щелкните **Далее**

4. Нажмите кнопку **вручную настроить приложение hello для единого входа**, нажмите кнопку **Далее** и завершения hello следующие шаги.
   
    ![Настройка URL-адреса приложения](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Настройка URL-адреса приложения")

5. На hello **Настройка единого входа в ServiceNow** щелкните **загрузки сертификата**, сохраните файл сертификата hello на локальном компьютере и нажмите кнопку **Далее**.
   
    ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Настройка единого входа")

6. Вход tooyour ServiceNow Express приложения от имени администратора.

7. Hello hello левой панели навигации щелкните **Single Sign-On**.  
   
    ![Настройка URL-адреса приложения](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "Настройка URL-адреса приложения")

8. На hello **Single Sign-On** диалоговое окно, щелкните значок конфигурации hello в верхнем hello вправо и задайте hello следующие свойства:
   
    ![Настройка URL-адреса приложения](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "Настройка URL-адреса приложения")
   
    а. Переключить **Включение нескольких поставщика единого входа** toohello справа.
   
    b. Переключить **Включение ведения журнала для hello поставщик нескольких интеграции единого входа для отладки** toohello справа.
   
    c. В **поле hello hello пользователем таблица...**  введите **имя_пользователя**.
9. На hello **Single Sign-On** диалоговое окно, нажмите кнопку **Добавление нового сертификата**.
   
    ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "Настройка единого входа")
10. На hello **сертификаты X.509** диалоговое окно, выполните следующие шаги hello:
    
    ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Настройка единого входа")
    
    а. В hello **имя** текстовом поле введите имя для конфигурации (например: **TestSAML2.0**).
    
    b. Установите флажок **Активно**.
    
    c. В поле **Format** (Формат) выберите **PEM**.
    
    d. В поле **Type** (Тип) выберите **Trust Store Cert** (Сертификат хранилища доверия).
    
    д. Создайте файл в кодировке Base 64 из скачанного сертификата.
    
    > [!NOTE]
    > Дополнительные сведения см. в разделе [как tooconvert двоичные данные сертификата в текстовый файл](http://youtu.be/PlgrzUZ-Y1o).
    > 
    > 
    
    f. Откройте сертификат в кодировке Base64 в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **сертификат PEM** текстового поля.
    
    ж. Нажмите кнопку **Обновить**.
11. На hello **Single Sign-On** диалоговое окно, нажмите кнопку **добавить нового поставщика удостоверений**.
    
    ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "Настройка единого входа")
12. На hello **Добавление поставщика удостоверений** диалогового окна в разделе **Настройка поставщика удостоверений**, выполните следующие шаги hello:
    
    ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "Настройка единого входа")

    а. в hello **имя** текстовом поле введите имя для конфигурации (например: **SAML 2.0**).

    b. В классическом портале Azure AD hello, скопируйте hello **идентификатор поставщика удостоверений** значение, а затем вставьте его в hello **URL-адрес поставщика удостоверений** текстового поля.

    c. В классическом портале Azure AD hello, скопируйте hello **URL-адрес запроса проверки подлинности** значение, а затем вставьте его в hello **AuthnRequest поставщика удостоверений** текстового поля.

    d. В классическом портале Azure AD hello, скопируйте hello **URL-адрес службы единого выхода** значение, а затем вставьте его в hello **SingleLogoutRequest поставщика удостоверений** текстового поля.

    д. Как **сертификат поставщика удостоверений**выберите hello сертификат, созданный на предыдущем шаге hello.


1. Нажмите кнопку **Дополнительные параметры**, а затем в разделе **дополнительные свойства поставщика удостоверений**, выполните следующие шаги hello:
   
    ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "Настройка единого входа")
   
    а. В hello **привязки протокола для SingleLogoutRequest поставщика Удостоверений hello** введите **urn: oasis: имена: tc: SAML:2.0:bindings:HTTP-перенаправления**.
   
    b. В hello **политики идентификатора имени** введите **urn: oasis: имена: tc: SAML:1.1:nameid-формат: Неизвестная**.    
   
    c. В hello **метод AuthnContextClassRef**, тип **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.
   
    d. Снимите флажок **Create an AuthnContextClass**(Создать класс контекста проверки подлинности).

2. В разделе **дополнительные свойства поставщика службы**, выполните следующие шаги hello:
   
    ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "Настройка единого входа")
   
    а. В hello **домашней страницы ServiceNow** текстовом поле введите URL-адрес hello вашей домашней страницы экземпляра ServiceNow.
   
    > [!NOTE]
    > Домашняя страница экземпляра ServiceNow Hello составляется из вашего **URL-адрес клиента ServieNow** и **/navpage.do** (например: `https://fabrikam.service-now.com/navpage.do`).
    > 
    > 
   
    b. В hello **идентификатор сущности или издателя** текстовом поле введите hello URL-адрес клиента ServiceNow.
   
    c. В hello **URI аудитории** текстовом поле введите hello URL-адрес клиента ServiceNow. 
   
    d. В текстовое поле **Clock Skew** (Разница в показаниях часов) введите **60**.
   
    д. В hello **поле пользователя** введите **электронной почты** или **имя_пользователя**, в зависимости от того, какое поле используется toouniquely идентификации пользователей в вашем развертывании ServiceNow.
   
    > [!NOTE]
    > Можно либо идентификатора пользователя hello Azure AD (имя участника-пользователя) tooemit настройки Azure AD или hello адрес электронной почты как hello уникальный идентификатор в токене SAML hello с переходом toohello **ServiceNow > атрибуты > Single Sign-On** раздела Здравствуйте классический портал Azure и сопоставление hello требуемого поля toohello **nameidentifier** атрибута. значение Hello, сохраненные для выбранного атрибута hello в Azure AD (например имя участника-пользователя) должно соответствовать hello значение, хранящееся в ServiceNow для hello введенные поля (например имя_пользователя)
    > 
    > 
   
    f. Щелкните **Сохранить**. 

3. На классический портал hello Azure AD, выберите Подтверждение настройки единого входа hello и нажмите кнопку **Далее**. 
   
    ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Настройка единого входа")

4. На hello **единого входа для подтверждения** щелкните **завершить**.
   
    ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Настройка единого входа")

## <a name="configuring-user-provisioning"></a>Настройка подготовки учетных записей пользователей
Цель этого раздела Hello является toooutline как tooenable пользователя Подготовка пользователя Active Directory учетных записей tooServiceNow.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure подготовки пользователей, выполните следующие шаги hello.
1. Hello Azure Management классического портала на hello **ServiceNow** странице интеграции приложения щелкните **Настройка подготовки пользователя**. 
   
    ![Подготовка учетных записей пользователей](./media/active-directory-saas-servicenow-tutorial/IC769498.png "Подготовка учетных записей пользователей")

2. На hello **введите ваш ServiceNow учетные данные tooenable автоматическую подготовку пользователей** укажите следующие параметры конфигурации hello:
   
     а. В hello **имя экземпляра ServiceNow** текстовое поле, имя экземпляра ServiceNow типа hello.
   
     b. В hello **имя пользователя администратора ServiceNow** в текстовое поле имя типа hello hello учетной записи администратора ServiceNow.
   
     c. В hello **пароль администратора ServiceNow** текстового поля, типа hello пароль для этой учетной записи.
   
     d. Нажмите кнопку **проверки** tooverify конфигурации.
   
     д. Нажмите кнопку hello **Далее** hello tooopen кнопку **дальнейшие действия** страницы.
   
     f. Tooprovision приложения toothis всех пользователей, выберите «**автоматически подготовить все учетные записи пользователей в приложении toothis directory hello**». 
   
    ![Дальнейшие действия](./media/active-directory-saas-servicenow-tutorial/IC698804.png "Дальнейшие действия")
   
     ж. На hello **дальнейшие действия** щелкните **завершить** toosave конфигурации.

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
В этом разделе создайте тестового пользователя вызывается Саймон Britta классическом портале hello.

![Создание пользователя Azure AD][20]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **классический портал Azure**, на левой панели навигации hello, нажмите кнопку **Active Directory**.
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_09.png) 

2. Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.

3. Щелкните toodisplay hello список пользователей, выберите в меню в верхней части экрана приветствия hello **пользователей**.
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_03.png) 

4. tooopen hello **добавить пользователя** щелкните диалоговое окно в нижней hello инструментов hello **добавить пользователя**.
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_04.png) 

5. На hello **сообщите нам об этом пользователе** диалогового окна выполните следующие шаги hello:
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_05.png) 
   
    а. В поле «Тип пользователя» выберите значение «Новый пользователь в вашей организации».
   
    b. В имени пользователя hello **textbox**, тип **BrittaSimon**.
   
    c. Щелкните **Далее**.

6. На hello **профиля пользователя** диалогового окна выполните следующие шаги hello:
   
   ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_06.png) 
   
   а. В hello **имя** введите **Britta**.  
   
   b. В hello **Фамилия** текстовое поле, тип, **Simon**.
   
   c. В hello **отображаемое имя** введите **Britta Simon**.
   
   d. В hello **роли** выберите **пользователя**.
   
   д. Щелкните **Далее**.

7. На hello **получение временного пароля** странице диалогового окна щелкните **создания**.
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_07.png) 

8. На hello **получение временного пароля** диалогового окна выполните следующие шаги hello:
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_08.png) 
   
    а. Запишите значение hello hello **новый пароль**.
   
    b. Нажмите **Завершено**.   

### <a name="creating-a-servicenow-test-user"></a>Создание тестового пользователя ServiceNow
В этом разделе описано, как создать пользователя Britta Simon в ServiceNow. В этом разделе описано, как создать пользователя Britta Simon в ServiceNow. Если вы не знаете, как tooadd в ServiceNow или ServiceNow Express учетная запись пользователя, обратитесь в службу технической поддержки ServiceNow.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя
В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления ее tooServiceNow доступа.

![Назначение пользователя][200] 

**tooassign tooServiceNow Britta Simon выполните следующие шаги hello.**

1. Hello классического портала щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.
   
    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **ServiceNow**.
   
    ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_10.png) 

3. В меню в верхней части hello hello выберите **пользователей**.
   
    ![Назначение пользователя][203] 

4. В списке Привет всем пользователям, выберите **Britta Simon**.

5. В нижней hello hello инструментов, нажмите кнопку **назначить**.
   
    ![Назначение пользователя][205]

### <a name="testing-single-sign-on"></a>Проверка единого входа
Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".

При нажатии кнопки hello ServiceNow плитки в панели доступа hello, вы должны получить приложение автоматически вошедшего tooyour ServiceNow.

## <a name="additional-resources"></a>Дополнительные ресурсы
* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_04.png


[5]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_06.png
[7]:  ./media/active-directory-saas-servicenow-tutorial/tutorial_general_050.png
[10]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_070.png
[20]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_205.png
