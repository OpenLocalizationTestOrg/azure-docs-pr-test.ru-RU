---
title: "Учебник. Интеграция Azure Active Directory с Evidence.com | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложении Evidence.com."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: f9a7cb7c-ff67-40dc-872c-1fa35f9dd03b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: a9c474cfc648fc8a306d736c89a4813d82c133ea
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-evidencecom"></a>Руководство. Интеграция Azure Active Directory с Evidence.com

В этом руководстве описано, как интегрировать Evidence.com с Azure Active Directory (Azure AD).

Интеграция Azure AD с приложением Evidence.com обеспечивает следующие преимущества:

- С помощью Azure AD вы можете контролировать доступ к Evidence.com.
- Вы можете включить автоматический вход пользователей в Evidence.com (единый вход) с применением учетной записи Azure AD.
- Вы можете управлять учетными записями централизованно — на портале Azure.

Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

Чтобы настроить интеграцию Azure AD с Evidence.com, вам потребуется:

- подписка Azure AD;
- Подписка Evidence.com с поддержкой единого входа.

> [!NOTE]
> Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.

При проверке действий в этом учебнике соблюдайте следующие рекомендации:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Сценарий, описанный в этом учебнике, состоит из двух основных блоков:

1. Добавление Evidence.com из коллекции.
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-evidencecom-from-the-gallery"></a>Добавление Evidence.com из коллекции
Чтобы настроить интеграцию Evidence.com с Azure AD, необходимо добавить Evidence.com из коллекции в список управляемых приложений SaaS.

**Чтобы добавить Evidence.com из коллекции, сделайте следующее:**

1. На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**. 

    ![Кнопка "Azure Active Directory"][1]

2. Перейдите к разделу **Корпоративные приложения**. Затем выберите **Все приложения**.

    ![Колонка "Корпоративные приложения"][2]
    
3. Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.

    ![Кнопка "Новое приложение"][3]

4. В поле поиска введите **Evidence.com**, на панели результатов выберите **Evidence.com** и нажмите кнопку **Добавить**, чтобы добавить это приложение.

    ![Evidence.com в списке результатов](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD

В этом разделе описана настройка и проверка единого входа Azure AD в Evidence.com с использованием тестового пользователя Britta Simon.

Для работы единого входа в Azure AD необходимо знать, какой пользователь в Evidence.com соответствует пользователю в Azure AD. Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Evidence.com.

Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Evidence.com.

Чтобы настроить и проверить единый вход Azure AD в Evidence.com, необходимо выполнить действия в следующих стандартных блоках.

1. **[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.
2. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.
3. **[Создание тестового пользователя Evidence.com](#create-a-evidencecom-test-user)** требуется для того, чтобы в Evidence.com существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.
4. **[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.
5. **[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Evidence.com.

**Чтобы настроить единый вход Azure AD в Evidence.com, сделайте следующее:**

1. На портале Azure на странице интеграции с приложением **Evidence.com** щелкните **Единый вход**.

    ![Ссылка "Настройка единого входа"][4]

2. В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_samlbase.png)

3. В разделе **Домены и URL-адреса приложения Evidence.com** сделайте следующее:

    ![Сведения о домене и URL-адресах единого входа для приложения Evidence.com](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_url.png)

    а. В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<yourtenant>.evidence.com`

    b. В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<yourtenant>.evidence.com`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Замените эти значения фактическим URL-адресом для входа и идентификатором. Чтобы получить их, обратитесь в [службу поддержки клиентов Evidence.com](https://communities.taser.com/support/SupportContactUs?typ=LE). 

4. В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-evidence-tutorial/tutorial_general_400.png)

6. В разделе **конфигурации Evidence.com** щелкните **Настроить Evidence.com**, чтобы открыть окно **Настройка единого входа**. Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.

    ![Конфигурация Evidence.com](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_configure.png) 

7. В отдельном окне браузера войдите в клиент Evidence.com с правами администратора и перейдите к вкладке **Admin** (Администрирование).

8. Щелкните **Agency Single Sign On**

9. Выберите параметр **SAML Based Single Sign On**

10. Скопируйте **идентификатор сущности SAML**, **URL-адрес службы единого входа SAML** и **URL-адрес выхода**, отображаемые на портале Azure, и добавьте их в соответствующие поля в приложении Evidence.com.

11. Откройте скачанный файл сертификата в кодировке Base64 в Блокноте, скопируйте его содержимое в буфер обмена, а затем вставьте его в поле **Security Certificate** (Сертификат безопасности). 

12. Сохраните конфигурацию в Evidence.com.

> [!TIP]
> Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.  После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы. Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD

Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.

   ![Создание тестового пользователя Azure AD][100]

**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**

1. На портале Azure в области слева нажмите кнопку **Azure Active Directory**.

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-evidence-tutorial/create_aaduser_01.png)

2. Чтобы открыть список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.

    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-evidence-tutorial/create_aaduser_02.png)

3. Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна **Все пользователи** щелкните **Добавить**.

    ![Кнопка "Добавить"](./media/active-directory-saas-evidence-tutorial/create_aaduser_03.png)

4. В диалоговом окне **Пользователь** сделайте следующее.

    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-evidence-tutorial/create_aaduser_04.png)

    а. В поле **Имя** введите **BrittaSimon**.

    b. В поле **Имя пользователя** введите адрес электронной почты для пользователя Britta Simon.

    c. Установите флажок **Показать пароль** и запишите значение, которое отображается в поле **Пароль**.

    г) Щелкните **Создать**.
 
### <a name="create-a-evidencecom-test-user"></a>Создание тестового пользователя Evidence.com

Чтобы пользователи Azure AD могли выполнять вход, нужно подготовить их для доступа в приложении Evidence.com. В этом разделе описано, как создавать учетные записи пользователей Azure AD в Evidence.com.

**Чтобы подготовить учетную запись пользователя в Evidence.com, выполните следующие действия.**

1. В окне веб-браузера войдите на корпоративный веб-сайт Evidence.com в качестве администратора.

2. Перейдите к вкладке **Admin** (Администрирование).

3. Щелкните **Add User**(Добавить пользователя).

4. Нажмите кнопку **Add** (Добавить).

5. Параметр **Email Address** (Адрес электронной почты) для нового пользователя должен совпадать с именем пользователя в Azure AD, которому вы хотите предоставить доступ. Возможно, в вашей организации в качестве имени пользователя не используется адрес электронной почты. Тогда зайдите на портале Azure в раздел **Evidence.com > Атрибуты > Единый вход** и измените параметр nameidentifier (идентификатор имени, отправляемый приложению Evidence.com) так, чтобы передавался именно адрес электронной почты.

### <a name="assign-the-azure-ad-test-user"></a>Назначение тестового пользователя Azure AD

В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Evidence.com.

![Назначение роли пользователя][200] 

**Чтобы назначить пользователя Britta Simon приложению Evidence.com, сделайте следующее:**

1. На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений выберите **Evidence.com**.

    ![Ссылка Evidence.com в списке приложений](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_app.png)  

3. В меню слева выберите **Пользователи и группы**.

    ![Ссылка "Пользователи и группы"][202]

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Область "Добавление назначения"][203]

5. В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.

Щелкнув элемент Evidence.com на панели доступа, вы автоматически войдете в приложение Evidence.com.
Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по интеграции приложений SaaS с Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_203.png

