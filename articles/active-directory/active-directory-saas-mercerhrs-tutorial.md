---
title: "Руководство по интеграции Azure Active Directory с Mercer BenefitsCentral (MBC) | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Mercer BenefitsCentral (MBC)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3788b28c-49aa-4208-9acd-630362008e89
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/21/2017
ms.author: jeedes
ms.openlocfilehash: c577a0163af04bec5737a215e788c3fb92c653c5
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mercer-benefitscentral-mbc"></a>Руководство по интеграции Azure Active Directory с Mercer BenefitsCentral (MBC)

В этом руководстве описано, как интегрировать Mercer BenefitsCentral (MBC) с Azure Active Directory (Azure AD).

Интеграция Azure AD с Mercer BenefitsCentral (MBC) обеспечивает следующие преимущества:

- С помощью Azure AD вы можете контролировать доступ к Mercer BenefitsCentral (MBC).
- Вы можете включить автоматический вход пользователей в Mercer BenefitsCentral (MBC) (единый вход) с использованием учетной записи Azure AD.
- Вы можете управлять учетными записями централизованно — на портале Azure.

Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

Чтобы настроить интеграцию Azure AD с Mercer BenefitsCentral (MBC), вам потребуется:

- подписка Azure AD;
- подписка Mercer BenefitsCentral (MBC) с поддержкой единого входа.

> [!NOTE]
> Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.

При проверке действий в этом учебнике соблюдайте следующие рекомендации:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Сценарий, описанный в этом учебнике, состоит из двух основных блоков:

1. Добавление Mercer BenefitsCentral (MBC) из коллекции
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-mercer-benefitscentral-mbc-from-the-gallery"></a>Добавление Mercer BenefitsCentral (MBC) из коллекции
Чтобы настроить интеграцию Mercer BenefitsCentral (MBC) с Azure AD, необходимо добавить Mercer BenefitsCentral (MBC) из коллекции в список управляемых приложений SaaS.

**Чтобы добавить Mercer BenefitsCentral (MBC) из коллекции, выполните следующие действия.**

1. На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**. 

    ![Кнопка "Azure Active Directory"][1]

2. Перейдите к разделу **Корпоративные приложения**. Затем выберите **Все приложения**.

    ![Колонка "Корпоративные приложения"][2]
    
3. Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.

    ![Кнопка "Новое приложение"][3]

4. В поле поиска введите **Mercer BenefitsCentral (MBC)**, выберите **Mercer BenefitsCentral (MBC)** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.

    ![Mercer BenefitsCentral (MBC) в списке результатов](./media/active-directory-saas-mercerhrs-tutorial/tutorial_mercerhrs_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD

В этом разделе описана настройка и проверка единого входа Azure AD в Mercer BenefitsCentral (MBC) с использованием тестового пользователя Britta Simon.

Чтобы настроить единый вход в Azure AD, необходимо знать, какой пользователь в Mercer BenefitsCentral (MBC) соответствует пользователю в Azure AD. Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Mercer BenefitsCentral (MBC).

Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Mercer BenefitsCentral (MBC).

Чтобы настроить и проверить единый вход Azure AD в Mercer BenefitsCentral (MBC), требуется выполнить действия в следующих стандартных блоках.

1. **[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.
2. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.
3. **[Создание тестового пользователя приложения Mercer BenefitsCentral (MBC)](#create-a-mercer-benefitscentral-mbc-test-user)** требуется для того, чтобы в Mercer BenefitsCentral (MBC) существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.
4. **[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.
5. **[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Mercer BenefitsCentral (MBC).

**Чтобы настроить единый вход Azure AD в Mercer BenefitsCentral (MBC), сделайте следующее.**

1. На портале Azure на странице интеграции с приложением **Mercer BenefitsCentral (MBC)** щелкните **Единый вход**.

    ![Ссылка "Настройка единого входа"][4]

2. В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-mercerhrs-tutorial/tutorial_mercerhrs_samlbase.png)

3. В разделе **Домены и URL-адреса приложения Mercer BenefitsCentral (MBC)** выполните следующие действия.

    ![Сведения о домене и URL-адресах единого входа приложения Mercer BenefitsCentral (MBC)](./media/active-directory-saas-mercerhrs-tutorial/tutorial_mercerhrs_url.png)

    а. В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `stg.mercerhrs.com/saml2.0`

    b. В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://ssous-stg.mercerhrs.com/SP2/Saml2AssertionConsumer.aspx`.

    > [!NOTE] 
    > Значение URL-адреса ответа приведено для примера. Вместо него нужно указать фактический URL-адрес ответа. Обратитесь к [группе поддержки Mercer BenefitsCentral (MBC)](https://www.mercer.com/contact-us.html), чтобы получить это значение.

4. В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-mercerhrs-tutorial/tutorial_mercerhrs_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-mercerhrs-tutorial/tutorial_general_400.png)

6. В разделе **Конфигурация Mercer BenefitsCentral (MBC)** щелкните **Настроить Mercer BenefitsCentral (MBC)**, чтобы открыть окно **Настройка единого входа**. Скопируйте **URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.

    ![Конфигурация Mercer BenefitsCentral (MBC)](./media/active-directory-saas-mercerhrs-tutorial/tutorial_mercerhrs_configure.png) 

7. Чтобы настроить единый вход на стороне **Mercer BenefitsCentral (MBC)**, нужно отправить скачанный **XML-файл метаданных** и **URL-адрес службы единого входа SAML** [группе поддержки Mercer BenefitsCentral (MBC)](https://www.mercer.com/contact-us.html). Специалисты службы поддержки настроят подключение единого входа SAML на обеих сторонах.

> [!TIP]
> Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.  После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы. Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD

Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.

   ![Создание тестового пользователя Azure AD][100]

**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**

1. На портале Azure в области слева нажмите кнопку **Azure Active Directory**.

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-mercerhrs-tutorial/create_aaduser_01.png)

2. Чтобы открыть список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.

    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-mercerhrs-tutorial/create_aaduser_02.png)

3. Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна **Все пользователи** щелкните **Добавить**.

    ![Кнопка "Добавить"](./media/active-directory-saas-mercerhrs-tutorial/create_aaduser_03.png)

4. В диалоговом окне **Пользователь** сделайте следующее.

    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-mercerhrs-tutorial/create_aaduser_04.png)

    а. В поле **Имя** введите **BrittaSimon**.

    b. В поле **Имя пользователя** введите адрес электронной почты для пользователя Britta Simon.

    c. Установите флажок **Показать пароль** и запишите значение, которое отображается в поле **Пароль**.

    г) Щелкните **Создать**.
  
### <a name="create-a-mercer-benefitscentral-mbc-test-user"></a>Создание тестового пользователя Mercer BenefitsCentral (MBC)

В этом разделе описано, как создать пользователя Britta Simon в Mercer HRS. Обратитесь к [группе поддержки Mercer BenefitsCentral (MBC)](https://www.mercer.com/contact-us.html), чтобы добавить пользователей на платформу Mercer HRS. Перед использованием единого входа необходимо создать и активировать пользователей.

### <a name="assign-the-azure-ad-test-user"></a>Назначение тестового пользователя Azure AD

В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Mercer BenefitsCentral (MBC).

![Назначение роли пользователя][200] 

**Чтобы назначить пользователя Britta Simon в Mercer BenefitsCentral (MBC), сделайте следующее.**

1. На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.

    ![Назначение пользователя][201] 

2. Из списка "Приложения" выберите **Mercer BenefitsCentral (MBC)**.

    ![Ссылка на Mercer BenefitsCentral (MBC) в списке "Приложения"](./media/active-directory-saas-mercerhrs-tutorial/tutorial_mercerhrs_app.png)  

3. В меню слева выберите **Пользователи и группы**.

    ![Ссылка "Пользователи и группы"][202]

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Область "Добавление назначения"][203]

5. В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.

Если щелкнуть элемент "Mercer BenefitsCentral (MBC)" на панели доступа, вы автоматически войдете в приложение Mercer BenefitsCentral (MBC).
Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по интеграции приложений SaaS с Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mercerhrs-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mercerhrs-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mercerhrs-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mercerhrs-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mercerhrs-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mercerhrs-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mercerhrs-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mercerhrs-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mercerhrs-tutorial/tutorial_general_203.png

