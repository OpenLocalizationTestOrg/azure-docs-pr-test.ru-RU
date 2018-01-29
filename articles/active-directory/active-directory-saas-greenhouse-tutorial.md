---
title: "Учебник. Интеграция Azure Active Directory с Greenhouse | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Greenhouse."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 78ec1766-4f79-4f16-9a66-d5584c4b6151
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 37f892439d514b642c1b0cf1a14a3da6084d9ab4
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-greenhouse"></a>Руководство. Интеграция Azure Active Directory с Greenhouse

В этом руководстве описано, как интегрировать Greenhouse с Azure Active Directory (Azure AD).

Интеграция Azure AD с приложением Greenhouse обеспечивает следующие преимущества:

- С помощью Azure AD вы можете контролировать доступ к Greenhouse.
- Вы можете включить автоматический вход пользователей в Greenhouse (единый вход) с учетной записью Azure AD.
- Вы можете управлять учетными записями централизованно — на портале Azure.

Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Технические условия

Чтобы настроить интеграцию Azure AD с приложением Greenhouse, вам потребуется:

- подписка Azure AD;
- подписка с поддержкой единого входа Greenhouse.

> [!NOTE]
> Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.

При проверке действий в этом учебнике соблюдайте следующие рекомендации:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Сценарий, описанный в этом учебнике, состоит из двух стандартных блоков.

1. Добавление Greenhouse из коллекции
2. настройка и проверка единого входа в Azure AD.

## <a name="adding-greenhouse-from-the-gallery"></a>Добавление Greenhouse из коллекции
Чтобы настроить интеграцию Greenhouse с Azure AD, необходимо добавить Greenhouse из коллекции в список управляемых приложений SaaS.

**Чтобы добавить Greenhouse из коллекции, выполните следующие действия.**

1. На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**. 

    ![Кнопка "Azure Active Directory"][1]

2. Перейдите к разделу **Корпоративные приложения**. Затем выберите **Все приложения**.

    ![Колонка "Корпоративные приложения"][2]
    
3. Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.

    ![Кнопка "Новое приложение"][3]

4. В поле поиска введите **Greenhouse**, выберите **Greenhouse** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.

    ![Greenhouse в списке результатов](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD

В этом разделе описана настройка и проверка единого входа Azure AD в приложение Greenhouse с использованием тестового пользователя Britta Simon.

Для работы единого входа в Azure AD необходимо знать, какой пользователь в Greenhouse соответствует пользователю в Azure AD. Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Greenhouse.

Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Greenhouse.

Чтобы настроить и проверить единый вход Azure AD в Greenhouse, вам потребуется выполнить действия в следующих стандартных блоках.

1. **[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.
2. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.
3. **[Создание тестового пользователя приложения Greenhouse](#create-a-greenhouse-test-user)** требуется для создания в Greenhouse пользователя Britta Simon, связанного с представлением пользователя в Azure AD.
4. **[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.
5. **[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Greenhouse.

**Чтобы настроить единый вход Azure AD в Greenhouse, выполните следующие действия.**

1. На портале Azure на странице интеграции с приложением **Greenhouse** щелкните **Единый вход**.

    ![Ссылка "Настройка единого входа"][4]

2. В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_samlbase.png)

3. В разделе **Домены и URL-адреса приложения Greenhouse** выполните следующие действия:

    ![Сведения о домене и URL-адресах единого входа приложения Greenhouse](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_url.png)

    a. В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<companyname>.greenhouse.io`

    Б. В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<companyname>.greenhouse.io`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Замените эти значения фактическим URL-адресом для входа и идентификатором. Чтобы получить эти значения, обратитесь к [группе поддержки Greenhouse](https://www.greenhouse.io/contact). 
 


4. В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-greenhouse-tutorial/tutorial_general_400.png)

6. Чтобы настроить единый вход на стороне **Greenhouse**, отправьте скачанный **XML-файл метаданных** в [службу поддержки Greenhouse](http://www.greenhouse.io/contact).

> [!TIP]
> Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.  После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы. Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD

Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.

   ![Создание тестового пользователя Azure AD][100]

**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**

1. На портале Azure в области слева нажмите кнопку **Azure Active Directory**.

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_01.png)

2. Чтобы открыть список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.

    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_02.png)

3. Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна **Все пользователи** щелкните **Добавить**.

    ![Кнопка "Добавить"](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_03.png)

4. В диалоговом окне **Пользователь** сделайте следующее.

    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_04.png)

    a. В поле **Имя** введите **BrittaSimon**.

    Б. В поле **Имя пользователя** введите адрес электронной почты для пользователя Britta Simon.

    c. Установите флажок **Показать пароль** и запишите значение, которое отображается в поле **Пароль**.

    d. Нажмите кнопку **Создать**.
 
### <a name="create-a-greenhouse-test-user"></a>Создание тестового пользователя Greenhouse

Чтобы пользователи Azure AD могли выполнять вход в Greenhouse, они должны быть подготовлены для Greenhouse. В случае с Greenhouse подготовка выполняется вручную.

>[!NOTE]
>Вы можете использовать любые другие средства создания учетной записи пользователя Greenhouse или API, предоставляемые Greenhouse для подготовки учетных записей пользователя AAD. 

**Чтобы подготовить учетные записи пользователей, выполните следующие действия.**

1. Выполните вход на веб-сайт компании **Greenhouse** в качестве администратора.

2. В меню вверху щелкните **Configure** (Настройка) и выберите **Users** (Пользователи).
   
   ![Пользователи](./media/active-directory-saas-greenhouse-tutorial/ic790791.png "Пользователи")

3. Нажмите кнопку **Новые пользователи**.
   
   ![Новый пользователь](./media/active-directory-saas-greenhouse-tutorial/ic790792.png "Новый пользователь")

4. В разделе **Добавить нового пользователя** выполните следующие действия.
   
   ![Добавление нового пользователя](./media/active-directory-saas-greenhouse-tutorial/ic790793.png "Добавление нового пользователя")

   a. В текстовом поле **Введите адреса электронной почты пользователей** укажите адрес электронной почты действующей учетной записи Azure Active Directory, которую вы хотите подготовить.

   Б. Выберите команду **Сохранить**.    
   
      >[!NOTE]
      >Владельцы учетных записей Azure Active Directory получат электронное сообщение со ссылкой для подтверждения учетной записи перед ее активацией.

### <a name="assign-the-azure-ad-test-user"></a>Назначение тестового пользователя Azure AD

В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к Greenhouse.

![Назначение роли пользователя][200] 

**Чтобы назначить пользователя Britta Simon в Greenhouse, выполните следующие действия.**

1. На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений выберите **Greenhouse**.

    ![Ссылка на Greenhouse в списке "Приложения"](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_app.png)  

3. В меню слева выберите **Пользователи и группы**.

    ![Ссылка "Пользователи и группы"][202]

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Область "Добавление назначения"][203]

5. В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.

Щелкнув элемент Greenhouse на панели доступа, вы автоматически войдете в приложение Greenhouse.
Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по интеграции приложений SaaS с Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_203.png

