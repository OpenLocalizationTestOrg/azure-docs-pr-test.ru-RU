---
title: "Руководство по интеграции Azure Active Directory с OpsGenie | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и OpsGenie."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 41b59b22-a61d-4fe6-ab0d-6c3991d1375f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: b0d8fa13c13ad8d4a85cb482bcd7e440006f0437
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-opsgenie"></a>Руководство. Интеграция Azure Active Directory с OpsGenie

В этом руководстве описано, как интегрировать OpsGenie с Azure Active Directory (Azure AD).

Интеграция Azure AD с приложением OpsGenie обеспечивает следующие преимущества.

- С помощью Azure AD вы можете контролировать доступ к OpsGenie.
- Вы можете включить автоматический вход пользователей в OpsGenie (единый вход) под учетной записью Azure AD.
- Вы можете управлять учетными записями централизованно — через портал Azure.

Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Технические условия

Чтобы настроить интеграцию Azure AD с OpsGenie, вам потребуется:

- подписка Azure AD;
- подписка OpsGenie с поддержкой единого входа.

> [!NOTE]
> Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.

При проверке действий в этом учебнике соблюдайте следующие рекомендации:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Сценарий, описанный в этом учебнике, состоит из двух стандартных блоков.

1. Добавление OpsGenie из коллекции
2. настройка и проверка единого входа в Azure AD.

## <a name="adding-opsgenie-from-the-gallery"></a>Добавление OpsGenie из коллекции
Чтобы настроить интеграцию OpsGenie с Azure AD, необходимо добавить OpsGenie из коллекции в список управляемых приложений SaaS.

**Чтобы добавить OpsGenie из коллекции, выполните следующие действия.**

1. На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**. 

    ![Active Directory][1]

2. Перейдите к разделу **Корпоративные приложения**. Затем выберите **Все приложения**.

    ![ПРИЛОЖЕНИЯ][2]
    
3. Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.

    ![ПРИЛОЖЕНИЯ][3]

4. В поле поиска введите **OpsGenie**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_search.png)

5. На панели результатов выберите **OpsGenie** и нажмите кнопку **Добавить**, чтобы добавить это приложение.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>настройка и проверка единого входа в Azure AD.
В этом разделе описаны настройка и проверка единого входа Azure AD в приложение OpsGenie с использованием тестового пользователя Britta Simon.

Чтобы единый вход работал, Azure AD необходимо знать, какой пользователь в OpsGenie соответствует пользователю в Azure AD. Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в OpsGenie.

Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в OpsGenie.

Чтобы настроить и проверить единый вход Azure AD в OpsGenie, вам потребуется выполнить действия в следующих стандартных блоках:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа в Azure AD от имени пользователя Britta Simon.
3. **[Создание тестового пользователя OpsGenie](#creating-a-opsgenie-test-user)** требуется для создания пользователя Britta Simon в OpsGenie, связанного с соответствующим представлением в Azure AD.
4. **[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD;
5. **[Проверка единого входа](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении OpsGenie.

**Чтобы настроить единый вход Azure AD в OpsGenie, выполните следующие действия.**

1. На портале Azure на странице интеграции с приложением **OpsGenie** щелкните **Единый вход**.

    ![Настройка единого входа][4]

2. В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_samlbase.png)

3. В разделе **Домены и URL-адреса приложения OpsGenie** выполните следующие действия:

    ![Настройка единого входа](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_url.png)

    В текстовом поле **URL-адрес для входа** введите URL-адрес: `https://app.opsgenie.com/auth/login`

4. В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.

    ![Настройка единого входа](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-opsgenie-tutorial/tutorial_general_400.png)

6. В разделе **Настройка OpsGenie** щелкните **Настроить OpsGenie**, чтобы открыть окно **Настройка единого входа**. Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.

    ![Настройка единого входа](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_configure.png) 

7. Откройте другое окно браузера и войдите в OpsGenie с правами администратора.

8. Щелкните **Параметры** и откройте вкладку **Единый вход**.
   
    ![Единый вход в OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_06.png)

9. Чтобы включить единый вход, установите флажок **Включено**.
   
    ![Параметры OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_07.png) 

10. В разделе **Поставщик** откройте вкладку **Azure Active Directory**.
   
    ![Параметры OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_08.png) 

11. На странице диалогового окна Azure Active Directory выполните следующие действия:
   
    ![Параметры OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_09.png)
    
    a. Вставьте **URL-адреса службы единого входа**, который вы скопировали с портала Azure, в текстовое поле **SAML 2.0 Endpoint** (Конечная точка SAML 2.0).
    
    Б. Откройте скачанный сертификат в кодировке Base-64 в Блокноте, скопируйте его содержимое в буфер обмена, а затем вставьте его в текстовое поле **Сертификат X.500**.
    
    c. Нажмите кнопку **Сохранить изменения**.

> [!TIP]
> Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.  После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы. Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.

![Создание пользователя Azure AD][100]

**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**

1. На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_01.png) 

2. Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_02.png) 

3. Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_03.png) 

4. На странице диалогового окна **Пользователь** выполните следующие действия.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-opsgenie-tutorial/create_aaduser_04.png) 

    a. В текстовом поле **Имя** введите **BrittaSimon**.

    Б. В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение поля **Пароль**.

    d. Нажмите кнопку **Создать**.
 
### <a name="creating-a-opsgenie-test-user"></a>Создание тестового пользователя OpsGenie

Цель этого раздела — создать пользователя с именем Britta Simon в OpsGenie. 

1. В окне веб-браузера войдите в клиент OpsGenie с правами администратора.

2. Перейдите к списку пользователей, щелкнув **Пользователь** на левой панели.
   
   ![Параметры OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_10.png) 

3. Нажмите кнопку **Add User**(Добавить пользователя).

4. На странице **Добавление пользователя** выполните следующие действия.
   
   ![Параметры OpsGenie](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_11.png)
   
   a. В текстовом поле **Email** (Адрес электронной почты) введите адрес электронной почты пользователя Britta Simon в Azure Active Directory.
   
   Б. В текстовом поле **Full Name** (Полное имя) введите **Britta Simon**.
   
   c. Выберите команду **Сохранить**. 

>[!NOTE]
>Britta получит по электронной почте инструкции по настройке профиля.

### <a name="assigning-the-azure-ad-test-user"></a>Назначение тестового пользователя Azure AD

В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к OpsGenie.

![Назначение пользователя][200] 

**Чтобы назначить пользователя Britta Simon в OpsGenie, выполните следующие действия.**

1. На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.

    ![Назначение пользователя][201] 

2. Из списка приложений выберите **OpsGenie**.

    ![Настройка единого входа](./media/active-directory-saas-opsgenie-tutorial/tutorial_opsgenie_app.png) 

3. В меню слева выберите **Пользователи и группы**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.

Щелкнув элемент OpsGenie на панели доступа, вы автоматически войдете в приложение OpsGenie.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по интеграции приложений SaaS с Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-opsgenie-tutorial/tutorial_general_203.png

