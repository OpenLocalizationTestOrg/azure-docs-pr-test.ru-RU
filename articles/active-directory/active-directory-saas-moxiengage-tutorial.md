---
title: "Руководство. Интеграция Azure Active Directory с Moxi Engage | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Moxi Engage."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1135a879-8f00-43b0-ac8a-831593d9586d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jeedes
ms.openlocfilehash: 25b5e377d8d0d504860ab9a8c4dac49c9ca5b104
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moxi-engage"></a>Руководство. Интеграция Azure Active Directory с Moxi Engage

В этом руководстве описано, как интегрировать Moxi Engage с Azure Active Directory (Azure AD).

Интеграция приложения Moxi Engage c Azure AD обеспечивает следующие преимущества.

- С помощью Azure AD вы можете контролировать, у кого есть доступ к приложению Moxi Engage.
- Вы можете включить автоматический вход пользователей в Moxi Engage (единый вход) с учетной записью Azure AD.
- Вы можете управлять учетными записями централизованно — через портал Azure.

Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

Чтобы настроить интеграцию Azure AD с Moxi Engage, вам потребуется:

- подписка Azure AD;
- подписка Moxi Engage с поддержкой единого входа.

> [!NOTE]
> Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.

При проверке действий в этом учебнике соблюдайте следующие рекомендации:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Сценарий, описанный в этом учебнике, состоит из двух основных блоков:

1. Добавление Moxi Engage из коллекции.
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-moxi-engage-from-the-gallery"></a>Добавление Moxi Engage из коллекции
Чтобы настроить интеграцию приложения Moxi Engage с Azure AD, вам нужно добавить это приложение из коллекции в свой список управляемых приложений SaaS.

**Добавление приложения Moxi Engage из коллекции**

1. На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**. 

    ![Active Directory][1]

2. Перейдите к разделу **Корпоративные приложения**. Затем выберите **Все приложения**.

    ![Приложения][2]
    
3. Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.

    ![Приложения][3]

4. В поле поиска введите **Moxi Engage**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-moxiengage-tutorial/tutorial_moxiengage_search.png)

5. На панели результатов выберите **Moxi Engage** и нажмите кнопку **Добавить**, чтобы добавить приложение.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-moxiengage-tutorial/tutorial_moxiengage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в приложение Moxi Engage с использованием тестового пользователя Britta Simon.

Для работы единого входа службе Azure AD нужно знать, какой пользователь в Moxi Engage соответствует пользователю в Azure AD. Иными словами, нужно установить связь между пользователем Azure AD и соответствующим пользователем в Moxi Engage.

Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Moxi Engage.

Чтобы настроить и проверить единый вход Azure AD в Moxi Engage, выполните следующие действия:

1. **[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.
3. **[Создание тестового пользователя Moxi Engage](#creating-a-moxi-engage-test-user)** требуется для создания в Moxi Engage пользователя Britta Simon, связанного с представлением этого пользователя в Azure AD.
4. **[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.
5. **[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе мы включим на портале Azure единый вход Azure AD и настроим его в приложении Moxi Engage.

**Настройка единого входа Azure AD в Moxi Engage**

1. На портале Azure на странице интеграции с приложением **Moxi Engage** щелкните **Единый вход**.

    ![Настройка единого входа][4]

2. В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-moxiengage-tutorial/tutorial_moxiengage_samlbase.png)

3. В разделе **Домены и URL-адреса приложения Moxi Engage** выполните следующие действия:

    ![Настройка единого входа](./media/active-directory-saas-moxiengage-tutorial/tutorial_moxiengage_url.png)

    В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://svc.<moxiworks-integration-domain>/service/v1/auth/inbound/saml/aad`

    > [!NOTE] 
    > Это значение приведено для справки. Вместо него необходимо указать фактический URL-адрес для входа. Для получения этого значения обратитесь в [службу поддержки клиентов Moxi Engage](mailto:support@moxiworks.com). 
 
4. В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.

    ![Настройка единого входа](./media/active-directory-saas-moxiengage-tutorial/tutorial_moxiengage_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-moxiengage-tutorial/tutorial_general_400.png)

6. Чтобы настроить единый вход на стороне **Moxi Engage**, отправьте скачанный **XML-файл метаданных** в [службу поддержки Moxi Engage](mailto:support@moxiworks.com). Специалисты службы поддержки правильно настроят подключение единого входа SAML на обеих сторонах подключения.

> [!TIP]
> Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.  После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы. Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.

![Создание пользователя Azure AD][100]

**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**

1. На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-moxiengage-tutorial/create_aaduser_01.png) 

2. Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-moxiengage-tutorial/create_aaduser_02.png) 

3. Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-moxiengage-tutorial/create_aaduser_03.png) 

4. На странице диалогового окна **Пользователь** выполните следующие действия.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-moxiengage-tutorial/create_aaduser_04.png) 

    а. В текстовом поле **Имя** введите **BrittaSimon**.

    b. В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение поля **Пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-moxi-engage-test-user"></a>Создание тестового пользователя Moxi Engage

В этом разделе описано, как создать пользователя Britta Simon в Moxi Engage. Обратитесь в [службу поддержки Moxi Engage](mailto:support@moxiworks.com), чтобы добавить пользователей на платформу Moxi Engage.

### <a name="assigning-the-azure-ad-test-user"></a>Назначение тестового пользователя Azure AD

В этом разделе мы разрешим пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Moxi Engage.

![Назначение пользователя][200] 

**Назначение пользователя Britta Simon приложению Moxi Engage**

1. На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений выберите **Moxi Engage**.

    ![Настройка единого входа](./media/active-directory-saas-moxiengage-tutorial/tutorial_moxiengage_app.png) 

3. В меню слева выберите **Пользователи и группы**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.

Щелкнув плитку Moxi Engage на панели доступа, вы автоматически войдете в приложение Moxi Engage.
Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по интеграции приложений SaaS с Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moxiengage-tutorial/tutorial_general_203.png

