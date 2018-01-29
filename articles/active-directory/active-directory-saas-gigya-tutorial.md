---
title: "Руководство по интеграции Azure Active Directory с Gigya | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Gigya."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 2c7d200b-9242-44a5-ac8a-ab3214a78e41
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 74bc67fb90f0505d2e1f213a4a0cdc26ade22872
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-gigya"></a>Руководство. Интеграция Azure Active Directory с Gigya

В этом руководстве описано, как интегрировать Gigya с Azure Active Directory (Azure AD).

Интеграция Azure AD с приложением Gigya обеспечивает следующие преимущества.

- С помощью Azure AD можно управлять доступом к Gigya.
- Вы можете включить автоматический вход пользователей в Gigya (единый вход) с учетной записью Azure AD.
- Вы можете управлять учетными записями централизованно — через портал Azure.

Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Технические условия

Чтобы настроить интеграцию Azure AD с Gigya, вам потребуется:

- подписка Azure AD;
- подписка Gigya с поддержкой единого входа.

> [!NOTE]
> Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.

При проверке действий в этом учебнике соблюдайте следующие рекомендации:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Сценарий, описанный в этом учебнике, состоит из двух стандартных блоков.

1. Добавление Gigya из коллекции
2. настройка и проверка единого входа в Azure AD.

## <a name="adding-gigya-from-the-gallery"></a>Добавление Gigya из коллекции
Чтобы настроить интеграцию Gigya с Azure AD, необходимо добавить Gigya из коллекции в список управляемых приложений SaaS.

**Чтобы добавить Gigya из коллекции, выполните следующие действия.**

1. На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**. 

    ![Active Directory][1]

2. Перейдите к разделу **Корпоративные приложения**. Затем выберите **Все приложения**.

    ![ПРИЛОЖЕНИЯ][2]
    
3. Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.

    ![ПРИЛОЖЕНИЯ][3]

4. В поле поиска введите **Gigya**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_search.png)

5. На панели результатов выберите **Gigya** и нажмите кнопку **Добавить**, чтобы добавить приложение.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>настройка и проверка единого входа в Azure AD.
В этом разделе описана настройка и проверка единого входа Azure AD в приложение Gigya с использованием тестового пользователя Britta Simon.

Для работы единого входа в Azure AD необходимо знать, какой пользователь в Gigya соответствует пользователю в Azure AD. Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Gigya.

Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Gigya.

Чтобы настроить и проверить единый вход Azure AD в Gigya, вам потребуется выполнить действия в следующих стандартных блоках.

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа в Azure AD от имени пользователя Britta Simon.
3. **[Создание тестового пользователя Gigya](#creating-a-gigya-test-user)** требуется для создания в Gigya пользователя Britta Simon, связанного с представлением этого же пользователя в Azure AD.
4. **[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD;
5. **[Проверка единого входа](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе описано, как включить единый вход Azure AD на новом портале Azure и настроить его в приложении Gigya.

**Чтобы настроить единый вход Azure AD в Gigya, выполните следующие действия.**

1. На портале Azure на странице интеграции с приложением **Gigya** щелкните **Единый вход**.

    ![Настройка единого входа][4]

2. В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_samlbase.png)

3. В разделе **Домен и URL-адреса приложения Gigya** выполните следующие действия.

    ![Настройка единого входа](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_url.png)

    a. В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `http://<companyname>.gigya.com`

    Б. В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://fidm.gigya.com/saml/v2.0/<companyname>`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Замените эти значения фактическим URL-адресом для входа и идентификатором. Чтобы получить их, обратитесь в [службу поддержки клиентов Gigya](https://www.gigya.com/support-policy/). 
 
4. В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.

    ![Настройка единого входа](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-gigya-tutorial/tutorial_general_400.png)

6. В разделе **Настройка Gigya** щелкните **Настроить Gigya**, чтобы открыть окно **Настройка единого входа**. Скопируйте **идентификатор сущности SAML и URL-адрес службы единого входа SAML** из раздела **Quick Reference** (Краткий справочник).

    ![Настройка единого входа](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_configure.png) 

7. В другом окне веб-браузера войдите на свой корпоративный веб-сайт Gigya в качестве администратора.

8. Последовательно выберите **Settings \> SAML Login** (Параметры > Вход SAML) и нажмите кнопку **Add** (Добавить).
   
    ![Вход SAML](./media/active-directory-saas-gigya-tutorial/ic789532.png "Вход SAML")

9. В разделе **Вход SAML** выполните следующие действия.
   
    ![Настройка SAML](./media/active-directory-saas-gigya-tutorial/ic789533.png "Настройка SAML")
   
    a. В текстовом поле **Имя** введите имя конфигурации.
   
    Б. В текстовое поле **Издатель** вставьте значение **идентификатора сущности SAML**, скопированное на портале Azure. 
   
    c. В текстовое поле **URL-адрес службы единого входа** вставьте значение **URL-адреса службы единого входа**, скопированное на портале Azure.
   
    d. В текстовое поле **Формат идентификатора имени** вставьте значение **формата идентификатора имени**, скопированное на портале Azure.
   
    д. Откройте в блокноте сертификат в кодировке Base-64, скачанный с портала Azure, скопируйте его в буфер обмена и вставьте в текстовое поле **Сертификат X.509**.
   
    f. Нажмите кнопку **Сохранить параметры**.

> [!TIP]
> Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.  После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы. Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD

Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.

![Создание пользователя Azure AD][100]

**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**

1. На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-gigya-tutorial/create_aaduser_01.png) 

2. Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-gigya-tutorial/create_aaduser_02.png) 

3. Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-gigya-tutorial/create_aaduser_03.png) 

4. На странице диалогового окна **Пользователь** выполните следующие действия.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-gigya-tutorial/create_aaduser_04.png) 

    a. В текстовом поле **Имя** введите **BrittaSimon**.

    Б. В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение поля **Пароль**.

    d. Нажмите кнопку **Создать**.
 
### <a name="creating-a-gigya-test-user"></a>Создание тестового пользователя Gigya

Чтобы пользователи Azure AD могли выполнять вход в Gigya, они должны быть подготовлены для Gigya.  
В случае с Gigya подготовка выполняется вручную.

### <a name="to-provision-a-user-accounts-perform-the-following-steps"></a>Чтобы подготовить учетные записи пользователей, выполните следующие действия.

1. Выполните вход на корпоративный веб-сайт **Gigya** в качестве администратора.

2. Последовательно выберите **Admin \> Manage Users** (Администратор > Управление пользователями) и нажмите кнопку **Invite Users** (Пригласить пользователей).
   
    ![Управление пользователями](./media/active-directory-saas-gigya-tutorial/ic789535.png "Управление пользователями")

3. В диалоговом окне "Пригласить пользователей" выполните следующие действия.
   
    ![Приглашение пользователей](./media/active-directory-saas-gigya-tutorial/ic789536.png "приглашение пользователей")
   
    a. В текстовое поле **Электронная почта** введите адрес электронной почты действующей учетной записи Azure Active Directory, которую вы хотите подготовить.
    
    Б. Нажмите кнопку **Пригласить пользователя**.
      
    > [!NOTE]
    > Владелец учетной записи Azure Active Directory получит по электронной почте сообщение со ссылкой для активации учетной записи.
    > 
    

### <a name="assigning-the-azure-ad-test-user"></a>Назначение тестового пользователя Azure AD

В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к Gigya.

![Назначение пользователя][200] 

**Чтобы назначить пользователя Britta Simon в Gigya, выполните следующие действия.**

1. На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений выберите **Gigya**.

    ![Настройка единого входа](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_app.png) 

3. В меню слева выберите **Пользователи и группы**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.

Щелкнув плитку Gigya на панели доступа, вы автоматически войдете в приложение Gigya.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по интеграции приложений SaaS с Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_203.png

