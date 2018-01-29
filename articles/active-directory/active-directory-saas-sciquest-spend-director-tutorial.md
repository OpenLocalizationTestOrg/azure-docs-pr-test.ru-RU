---
title: "Руководство по интеграции Azure Active Directory с SciQuest Spend Director | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и SciQuest Spend Director."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 9fab641b-292e-4bef-91d1-8ccc4f3a0c1f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/12/2017
ms.author: jeedes
ms.openlocfilehash: be9b17f31bedca1ae5704b484760c3ad24fbb14d
ms.sourcegitcommit: 922687d91838b77c038c68b415ab87d94729555e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/13/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sciquest-spend-director"></a>Учебник. Интеграция Azure Active Directory с SciQuest Spend Director

В этом учебнике вы узнаете, как интегрировать SciQuest директор расходов в Azure Active Directory (Azure AD).

Интеграция SciQuest Spend Director с Azure AD обеспечивает следующие преимущества.

- Можно управлять в Azure AD, кто имеет доступ к SciQuest директор расходов.
- Вы можете включить их учетные записи Azure AD пользователям автоматически получить вошедшего в директор расходов SciQuest (Single Sign-On).
- Вы можете управлять учетными записями централизованно — на портале Azure.

Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Технические условия

Чтобы настроить интеграцию Azure AD с SciQuest Spend Director, вам потребуется следующее:

- подписка Azure AD;
- Директор расходов SciQuest единый вход включен подписки

> [!NOTE]
> Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.

При проверке действий в этом учебнике соблюдайте следующие рекомендации:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Сценарий, описанный в этом учебнике, состоит из двух стандартных блоков.

1. Добавление SciQuest Spend Director из коллекции
2. настройка и проверка единого входа в Azure AD.

## <a name="adding-sciquest-spend-director-from-the-gallery"></a>Добавление SciQuest Spend Director из коллекции
Чтобы настроить интеграцию SciQuest Spend Director с Azure AD, вам потребуется добавить SciQuest Spend Director из коллекции в список управляемых приложений SaaS.

**Чтобы добавить SciQuest Spend Director из коллекции, выполните следующие действия:**

1. На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**. 

    ![Кнопка "Azure Active Directory"][1]

2. Перейдите к разделу **Корпоративные приложения**. Затем выберите **Все приложения**.

    ![Колонка "Корпоративные приложения"][2]
    
3. Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.

    ![Кнопка "Новое приложение"][3]

4. В поле поиска введите **директор расходов SciQuest**выберите **директор расходов SciQuest** из панели результатов щелкните **добавить** кнопку, чтобы добавить приложение.

    ![Директор расходов SciQuest в списке результатов](./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquestspenddirector_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD

В этом разделе настройки и тестирования в Azure AD единого входа с директор расходов SciQuest основании тестового пользователя с именем «Britta Simon».

Azure AD для единого входа для работы, необходимо знать пользователя аналога в директор расходов SciQuest для пользователя в Azure AD. Иными словами, необходимо установить связь между пользователям Azure AD и соответствующим пользователем в SciQuest Spend Director.

В SciQuest директор расходов, присвойте значение **имя пользователя** в Azure AD в качестве значения **Username** для установления связи.

Чтобы настроить и проверить единый вход в Azure AD в SciQuest Spend Director, вам потребуется выполнить действия в следующих блоках:

1. **[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.
2. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.
3. **[Создание тестового пользователя директор расходов SciQuest](#create-a-sciquest-spend-director-test-user)**  — на аналог Саймон Britta в SciQuest тратить директора, связанного с представлением Azure AD пользователя.
4. **[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.
5. **[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе включения Azure AD единого входа на портале Azure и настройки единого входа в приложении SciQuest директор расходов.

**Чтобы настроить единый вход в Azure AD с помощью SciQuest Spend Director, выполните следующие действия:**

1. На портале Azure на **директор расходов SciQuest** странице интеграции приложения щелкните **единого входа**.

    ![Ссылка "Настройка единого входа"][4]

2. В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquestspenddirector_samlbase.png)

3. На **URL-адреса и домена директор расходов SciQuest** выполните следующие действия:

    ![URL-адреса и домена директор расходов SciQuest единого входа сведения](./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquestspenddirector_url.png)

    a. В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<companyname>.sciquest.com/apps/Router/SAMLAuth/<instancename>`

    Б. В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<companyname>.sciquest.com`

    c. В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<companyname>.sciquest.com/apps/Router/ExternalAuth/Login/<instancename>`.

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Укажите вместо них фактические значения URL-адреса для входа, идентификатора и URL-адреса ответа. Обратитесь к [группа поддержки клиента директор расходов SciQuest](https://www.jaggaer.com/contact-us/) для получения этих значений. 

4. В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquestspenddirector_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_400.png)

6. Для настройки единого входа на **директор расходов SciQuest** стороны, необходимо отправить загруженного **метаданные в формате XML** для [группа поддержки директор расходов SciQuest](https://www.jaggaer.com/contact-us/).

> [!TIP]
> Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.  После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы. Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD

Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.

   ![Создание тестового пользователя Azure AD][100]

**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**

1. На портале Azure в области слева нажмите кнопку **Azure Active Directory**.

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-sciquest-spend-director-tutorial/create_aaduser_01.png)

2. Чтобы открыть список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.

    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-sciquest-spend-director-tutorial/create_aaduser_02.png)

3. Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна **Все пользователи** щелкните **Добавить**.

    ![Кнопка "Добавить"](./media/active-directory-saas-sciquest-spend-director-tutorial/create_aaduser_03.png)

4. В диалоговом окне **Пользователь** сделайте следующее.

    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-sciquest-spend-director-tutorial/create_aaduser_04.png)

    a. В поле **Имя** введите **BrittaSimon**.

    Б. В поле **Имя пользователя** введите адрес электронной почты для пользователя Britta Simon.

    c. Установите флажок **Показать пароль** и запишите значение, которое отображается в поле **Пароль**.

    d. Нажмите кнопку **Создать**.
 
### <a name="create-a-sciquest-spend-director-test-user"></a>Создание тестового пользователя SciQuest директор расходов

Цель этого раздела — создать пользователя с именем Britta Simon в SciQuest Spend Director.

Необходимо обратиться к [группа поддержки директор расходов SciQuest](https://www.jaggaer.com/contact-us/) и предоставить им сведения о вашей учетной записи теста, чтобы она создана.

Вы также можете использовать JIT-подготовку — функцию единого входа, поддерживаемую SciQuest Spend Director.  
Если функция JIT-подготовки включена, SciQuest Spend Director автоматически создает пользователей при попытке единого входа, если они еще не созданы. Эта функция устраняет необходимость вручную создавать дублирующих пользователей для единого входа.

Для получения включении подготовки just-in-time, необходимо обратиться к [группа поддержки директор расходов SciQuest](https://www.jaggaer.com/contact-us/).

### <a name="assign-the-azure-ad-test-user"></a>Назначение тестового пользователя Azure AD

В этом разделе включите Саймон Britta для использования Azure единого входа, предоставление доступа к SciQuest директор расходов.

![Назначение роли пользователя][200] 

**Чтобы назначить Britta Simon в SciQuest Spend Director, выполните следующие действия:**

1. На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений выберите **SciQuest Spend Director**.

    ![Директор расходов SciQuest ссылку в список приложений](./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquestspenddirector_app.png)  

3. В меню слева выберите **Пользователи и группы**.

    ![Ссылка "Пользователи и группы"][202]

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Область "Добавление назначения"][203]

5. В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.

Нажав элемент SciQuest Spend Director на панели доступа, вы автоматически войдете в приложение SciQuest Spend Director.
Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по интеграции приложений SaaS с Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_203.png

