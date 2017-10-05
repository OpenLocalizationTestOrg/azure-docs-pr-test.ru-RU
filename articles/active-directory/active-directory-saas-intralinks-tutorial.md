---
title: "Учебник. Интеграция Azure Active Directory с Intralinks | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Intralinks."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 147f2bf9-166b-402e-adc4-4b19dd336883
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: ee7fd5b88ac806104002ffb41af11bab4fd1b2dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intralinks"></a>Руководство. Интеграция Azure Active Directory с Intralinks

В этом руководстве описано, как интегрировать Intralinks с Azure Active Directory (Azure AD).

Интеграция Azure AD с приложением Intralinks обеспечивает следующие преимущества:

- С помощью Azure AD вы можете контролировать доступ к Intralinks.
- Вы можете включить автоматический вход пользователей в Intralinks (единый вход) с использованием учетной записи Azure AD.
- Вы можете управлять учетными записями централизованно — через портал Azure.

Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

Чтобы настроить интеграцию Azure AD с Intralinks, вам потребуется:

- подписка Azure AD;
- подписка Intralinks с поддержкой единого входа.

> [!NOTE]
> Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.

При проверке действий в этом учебнике соблюдайте следующие рекомендации:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Сценарий, описанный в этом руководстве, состоит из двух стандартных блоков.

1. Добавление Intralinks из коллекции.
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-intralinks-from-the-gallery"></a>Добавление Intralinks из коллекции.
Чтобы настроить интеграцию Intralinks с Azure AD, необходимо добавить Intralinks из коллекции в список управляемых приложений SaaS.

**Чтобы добавить Intralinks из коллекции, выполните следующие действия.**

1. На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**. 

    ![Active Directory][1]

2. Перейдите к разделу **Корпоративные приложения**. Затем выберите **Все приложения**.

    ![Приложения][2]
    
3. Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.

    ![Приложения][3]

4. В поле поиска введите **Intralinks**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. На панели результатов выберите **Intralinks** и нажмите кнопку **Добавить**, чтобы добавить это приложение.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Intralinks с использованием тестового пользователя Britta Simon.

Для работы единого входа в Azure AD необходимо знать, какой пользователь в Intralinks соответствует пользователю в Azure AD. Иными словами, необходимо установить связь между пользователям Azure AD и соответствующим пользователем в Intralinks.

Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Intralinks.

Чтобы настроить и проверить единый вход Azure AD в Intralinks, вам потребуется выполнить действия в следующих стандартных блоках:

1. **[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.
3. **[Создание тестового пользователя Intralinks](#creating-an-intralinks-test-user)** требуется для того, чтобы в Intralinks существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.
4. **[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.
5. **[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Intralinks.

**Чтобы настроить единый вход Azure AD в Intralinks, выполните следующие действия.**

1. На портале Azure на странице интеграции с приложением **Intralinks** щелкните **Единый вход**.

    ![Настройка единого входа][4]

2. В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_samlbase.png)

3. В разделе **Домены и URL-адреса приложения Intralinks** выполните следующие действия.

    ![Настройка единого входа](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_url.png)

    В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`.

    > [!NOTE] 
    > Это значение приведено для справки. Вместо него необходимо указать фактический URL-адрес входа. Для получения данного значения обратитесь к [группе поддержки Intralinks](https://www.intralinks.com/contact-1). 
 
4. В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.

    ![Настройка единого входа](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

6. Чтобы настроить единый вход на стороне **Intralinks**, отправьте [группе поддержки Intralinks](https://www.intralinks.com/contact-1) скачанный **XML-файл метаданных**. Специалисты службы поддержки настроят подключение единого входа SAML на обеих сторонах.

> [!TIP]
> Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.  После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы. Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.

![Создание пользователя Azure AD][100]

**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**

1. На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_01.png) 

2. Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_02.png) 

3. Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_03.png) 

4. На странице диалогового окна **Пользователь** выполните следующие действия.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_04.png) 

    а. В текстовом поле **Имя** введите **BrittaSimon**.

    b. В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение поля **Пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-an-intralinks-test-user"></a>Создание тестового пользователя Intralinks

В этом разделе описано, как создать пользователя Britta Simon в приложении Intralinks. Обратитесь к [группе поддержки Intralinks](https://www.intralinks.com/contact-1), чтобы добавить пользователей на платформу Intralinks.

### <a name="assigning-the-azure-ad-test-user"></a>Назначение тестового пользователя Azure AD

В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Intralinks.

![Назначение пользователя][200] 

**Чтобы назначить пользователя Britta Simon в Intralinks, выполните следующие действия.**

1. На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений выберите **Intralinks**.

    ![Настройка единого входа](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_app.png) 

3. В меню слева выберите **Пользователи и группы**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.

### <a name="add-intralinks-via-or-elite-application"></a>Добавление приложения Intralinks VIA или Elite

Для всех приложений Intralinks используется одна платформа удостоверений единого входа, за исключением приложения Deal Nexus. Поэтому, если вы планируете использовать любое другое приложение Intralinks, сначала необходимо настроить единый вход для одного основного приложения Intralinks с помощью процедуры, описанной выше.

После этого вы можете выполнить описанные ниже действия, чтобы добавить другое приложение Intralinks в клиент, который может использовать это основное приложение для единого входа. 

>[!NOTE]
>Эта функция доступна только для клиентов SKU Azure AD уровня "Премиум" и недоступна для клиентов SKU уровня "Бесплатный" или "Базовый".

1. На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**. 

    ![Active Directory][1]


2. Перейдите к разделу **Корпоративные приложения**. Затем выберите **Все приложения**.

    ![Приложения][2]
    
3. Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.

    ![Приложения][3]

4. В поле поиска введите **Intralinks**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. На странице **Intralinks Add app** (Добавление приложения Intralinks) выполните следующие действия.

    ![Добавление приложения Intralinks VIA или Elite](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addapp.png)

    а. В текстовое поле **Имя** введите соответствующее имя приложения, например **Intralinks Elite**.

    b. Нажмите кнопку **Добавить**.

6.  На портале Azure на странице интеграции с приложением **Intralinks** щелкните **Единый вход**.

    ![Настройка единого входа][4]

7. В диалоговом окне **Единый вход** для параметра **Режим** выберите значение **Вход по ссылке**.
 
    ![Настройка единого входа](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_linkedsignon.png)

8. Получите от [команды Intralinks](https://www.intralinks.com/contact-1) URL-адрес единого входа, инициируемого поставщиком услуг, для другого приложения Intralinks. Затем введите этот URL-адрес в разделе **Настройка URL-адреса для единого входа**, как показано ниже. 
    
     ![Настройка единого входа](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_customappurl.png)
    
     В текстовом поле "URL-адрес входа" введите URL-адрес, с помощью которого пользователи входят в приложение Intralinks, в следующем формате:
   
    `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`

9. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

10. Назначьте приложения пользователям или группам, как показано в разделе **[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)**.

### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.

Щелкнув плитку Intralinks на панели доступа, вы автоматически войдете в приложение Intralinks.
Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по интеграции приложений SaaS с Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_203.png

