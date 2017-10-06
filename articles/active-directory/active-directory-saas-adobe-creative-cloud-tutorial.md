---
title: "Руководство по интеграции Azure Active Directory с Adobe Creative Cloud | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Adobe Creative Cloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9ba1171e-56b1-4475-b308-58637d35e5a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 5e66255e9785465974a23cd3ef79c24e28c0250f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-creative-cloud"></a>Руководство по интеграции Azure Active Directory с Adobe Creative Cloud

В этом учебнике вы узнаете, как toointegrate Adobe Creative Cloud с Azure Active Directory (Azure AD).

Интеграция с Azure AD Adobe Creative Cloud предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooAdobe Creative Cloud
- Ваш пользователей tooautomatically get вошедшего tooAdobe Creative Cloud (Single Sign-On) можно включить с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал управления Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Adobe Creative Cloud требуется hello следующих элементов:

- подписка Azure AD;
- подписка Adobe Creative Cloud с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не следует использовать рабочую среду при отсутствии необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Adobe Creative Cloud из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-adobe-creative-cloud-from-hello-gallery"></a>Добавление Adobe Creative Cloud из галереи hello
tooconfigure hello интеграции Adobe Creative Cloud в Azure AD, вы должны tooadd Adobe Creative Cloud из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Adobe Creative Cloud из галереи hello, выполните следующие шаги hello.**

1. В hello ** [портала управления Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. Нажмите кнопку **добавить** кнопку в верхней части hello диалогового окна "hello".

    ![Приложения][3]

4. Введите в поле поиска hello **Adobe Creative Cloud**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_000.png)

5. В панели результатов hello выберите **Adobe Creative Cloud**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Adobe Creative Cloud с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Adobe Creative Cloud является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в Adobe Creative Cloud должен установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Adobe Creative Cloud.

tooconfigure и теста Azure AD единого входа с Adobe Creative Cloud, необходимо toocomplete hello следующие компоненты:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user) ** -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя, прошедшего Adobe Creative Cloud](#creating-an-adobe-creative-cloud-test-user) ** -toohave аналог Саймон Britta в Adobe Creative Cloud, представление связанных toohello Azure AD ей.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on) ** -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал управления Azure hello и настройки единого входа в приложении Adobe Creative Cloud.

**tooconfigure Azure AD единого входа с Adobe Creative Cloud, выполните следующие шаги hello.**

1. На портале управления Azure hello на hello **Adobe Creative Cloud** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна, как **режим** выберите **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_01.png)

3. На hello **Adobe Creative облака домена и URL-адреса** выполните hello, выполните действия, при желании tooconfigure приложения hello в **IDP** инициировал режим:

    ![Настройка единого входа](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url1.png)

    а. В hello **идентификатор** текстовое поле, значение типа hello как:`https://www.okta.com/saml2/service-provider/<token>`

    b. В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company name>.okta.com/auth/saml20/accauthlinktest`

    > [!NOTE] 
    > Обратите внимание на то, что они не hello реальные значения. У вас tooupdate эти значения с hello фактический идентификатор и ответ URL-адрес. Здесь мы предлагаем вам toouse hello уникальное значение строки в hello идентификатор. Если вам требуется toocreate пользователя вручную, необходимо группа поддержки Adobe Creative Cloud toocontact hello.

4. На hello **URL-адреса и Adobe Creative облака домена** выполните hello, выполните действия, при желании tooconfigure приложения hello в **SP** инициировал режим:

    ![Настройка единого входа](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url2.png)

    а. Щелкните hello **Показывать дополнительные параметры URL-адреса** параметр

    b. В hello **URL-адрес входа** текстовое поле, значение типа hello как:`https://adobe.com`

5. На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_05.png) 

6. На hello **Adobe Creative конфигурации облака** щелкните **настроить Adobe Creative Cloud** tooopen **Настройка входа** окна. Скопируйте hello **идентификатор сущности SAML** и **URL-адрес службы единого входа SAML** из раздела краткий справочник.

    ![Настройка единого входа](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_06.png) 

7. В другом окне браузера, клиент Adobe Creative Cloud tooyour входа от имени администратора.

8.  Go слишком**удостоверение** hello левой панели навигации и щелкните свой домен. Выполните hello, выполните действия **единого входа на конфигурации требуется** раздела.

    ![Параметры](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "Параметры")

9. Нажмите кнопку **Обзор** tooupload hello загрузить сертификат из Azure AD слишком**сертификат поставщика Удостоверений**.

10. В hello **издатель IDP** текстовое поле, помещение значения hello **идентификатор сущности SAML** скопирован из **Настройка входа** раздела на портале Azure.

11. В hello **URL-адрес входа поставщика Удостоверений** текстовое поле, помещение значения hello **URL-адрес службы единого входа SAML** скопирован из **Настройка входа** раздела на портале Azure.

12. Для параметра **HTTP — Redirect** (Перенаправление HTTP) выберите вариант **IDP Binding** (Привязка к поставщику удостоверений).

13. Для параметра **Email Address** (Адрес электронной почты) выберите вариант **User Login Setting** (Настройки входа пользователя).
 
14. Нажмите кнопку **Сохранить** .

15. панель мониторинга Hello теперь будет представлять hello XML **«Скачать метаданные»** файла. Он содержит URL-адреса компании Adobe для описания сущности (EntityDescriptor) и URL-адреса службы утверждений (AssertionConsumerService). Откройте файл hello и настроить их в hello приложения Azure AD.

    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_002.png)

    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_003.png)

    а. Используйте hello EntityDescriptor значение Adobe следующие материалы для **идентификатор** на hello **Настройка параметров приложения** диалогового окна.

    b. Используйте hello AssertionConsumerService значение Adobe следующие материалы для **URL-адрес ответа** на hello **Настройка параметров приложения** диалогового окна.
 
### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя на портале управления Azure hello, вызывается Саймон Britta.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал управления Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_01.png) 

2. Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_02.png) 

3. Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**. 

### <a name="creating-an-adobe-creative-cloud-test-user"></a>Создание тестового пользователя Adobe Creative Cloud

В порядке tooenable toolog пользователей Azure AD в Adobe Creative Cloud их необходимо подготовить в Adobe Creative Cloud.  
В случае hello Adobe Creative Cloud Подготовка выполняется вручную.

**tooprovision учетных записей пользователей, выполните следующие действия hello:**

1. Войдите в tooyour корпоративный сайт Adobe Creative Cloud с правами администратора.

2. Выберите параметр **Пользователи**.

    ![Люди](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "Люди")

3. Нажмите кнопку **Пригласить пользователя**.

    ![Приглашение пользователей](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "приглашение пользователей")

4. На hello **пригласить пользователя** диалогового окна выполните следующие шаги hello:

    ![Приглашение участников](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "приглашение участников")

    а. В hello **электронной почты** текстовом поле введите адрес электронной почты hello Саймон Britta учетной записи.
    
    b. Нажмите кнопку **Пригласить**.

    > [!NOTE]
    > Hello владельцем учетной записи Azure Active Directory получит сообщение электронной почты и выполните их учетных записей tooconfirm ссылку, чтобы она стала активной.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа, предоставляя свой доступ tooAdobe Creative Cloud.

![Назначение пользователя][200] 

**tooassign tooAdobe Britta Simon Creative Cloud выполните hello следующие шаги.**

1. На портале управления Azure hello, открыть представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Adobe Creative Cloud**.

    ![Настройка единого входа](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_50.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При выборе плитки Adobe Creative Cloud hello в hello панели доступа, следует получать автоматически вошедшего tooyour Adobe Creative облачного приложения.


## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_203.png