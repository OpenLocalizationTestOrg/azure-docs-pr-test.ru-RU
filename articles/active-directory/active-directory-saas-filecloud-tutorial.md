---
title: "Учебник. Интеграция Azure Active Directory с FileCloud | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и FileCloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: f39f0ddd-b504-4562-971f-77b88d1e75fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: ad03516f684acc59912ffc57f6e0712828bd03f2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-filecloud"></a>Учебник. Интеграция Azure Active Directory с FileCloud

В этом руководстве описано, как интегрировать FileCloud с Azure Active Directory (Azure AD).

Интеграция FileCloud с Azure AD обеспечивает следующие преимущества.

- С помощью Azure AD вы можете контролировать доступ к FileCloud.
- Вы можете включить автоматический вход пользователей в FileCloud (единый вход) с использованием учетной записи Azure AD.
- Вы можете управлять учетными записями централизованно — на портале Azure.

Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

Чтобы настроить интеграцию Azure AD с FileCloud, вам потребуется:

- подписка Azure AD;
- подписка FileCloud с поддержкой единого входа.

> [!NOTE]
> Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.

При проверке действий в этом учебнике соблюдайте следующие рекомендации:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Сценарий, описанный в этом учебнике, состоит из двух основных блоков:

1. Добавление FileCloud из коллекции
2. Настройка и проверка единого входа в Azure AD.

## <a name="adding-filecloud-from-the-gallery"></a>Добавление FileCloud из коллекции
Чтобы настроить интеграцию FileCloud с Azure AD, необходимо добавить FileCloud из коллекции в список управляемых приложений SaaS.

**Чтобы добавить FileCloud из коллекции, выполните следующие действия.**

1. На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**. 

    ![Кнопка "Azure Active Directory"][1]

2. Перейдите к разделу **Корпоративные приложения**. Затем выберите **Все приложения**.

    ![Колонка "Корпоративные приложения"][2]
    
3. Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.

    ![Кнопка "Новое приложение"][3]

4. В поле поиска введите **FileCloud**, выберите **FileCloud** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.

    ![FileCloud в списке результатов](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD

В этом разделе описана настройка и проверка единого входа Azure AD в приложение FileCloud с помощью тестового пользователя Britta Simon.

Для работы единого входа в Azure AD необходимо знать, какой пользователь в FileCloud соответствует пользователю в Azure AD. Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в FileCloud.

Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в FileCloud.

Чтобы настроить и проверить единый вход Azure AD в FileCloud, выполните следующие стандартные действия.

1. **[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.
2. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.
3. **[Создание тестового пользователя FileCloud](#create-a-filecloud-test-user)** нужно для того, чтобы в FileCloud также существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.
4. **[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.
5. **[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении FileCloud.

**Чтобы настроить единый вход Azure AD в FileCloud, выполните следующие действия.**

1. На портале Azure на странице интеграции с приложением **FileCloud** щелкните **Единый вход**.

    ![Ссылка "Настройка единого входа"][4]

2. В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_samlbase.png)

3. В разделе **Домены и URL-адреса приложения FileCloud** выполните указанные ниже действия.

    ![Сведения о домене и URL-адресах единого входа приложения FileCloud](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_url.png)

    а. В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<subdomain>.filecloudhosted.com`

    b. В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<subdomain>.filecloudhosted.com/simplesaml/module.php/saml/sp/metadata.php/default-sp`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Замените эти значения фактическим URL-адресом для входа и идентификатором. Чтобы получить эти значения, обратитесь в [службу поддержки клиентов FileCloud](mailto:support@codelathe.com).

4. В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-filecloud-tutorial/tutorial_general_400.png)

6. В разделе **Настройка FileCloud** щелкните **Настроить FileCloud**, чтобы открыть окно **Настройка единого входа**. Скопируйте значение **SAML Entity ID** (Идентификатор сущности SAML) из раздела **Краткий справочник**.

    ![Настройка FileCloud](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_configure.png) 

7. В другом окне веб-браузера войдите в свой клиент FileCloud с правами администратора.

8. В левой панели навигации щелкните **Settings**(Параметры). 
   
    ![Раздел "Settings" (Параметры) на стороне приложения](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_000.png)

9. Щелкните вкладку **SSO** (Единый вход) в разделе "Settings" (Параметры). 
   
    ![Вкладка "Single Sign-On" (Единый вход) на стороне приложения](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_001.png)

10. На панели **Single Sign On (SSO) Settings** (Параметры единого входа) для параметра **Default SSO Type** (Тип единого входа по умолчанию) выберите значение **SAML**.
   
    ![Панель "Single Sign-On Settings" (Параметры единого входа) на стороне приложения](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_002.png)

11. Вставьте значение **Идентификатор сущности SAML**, скопированное на портале Azure, в поле **IdP End Point URL** (URL-адрес конечной точки IdP).

    ![Текстовое поле "IDP End Point URL" (URL-адрес конечной точки IDP)](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_003.png)

12. Откройте скачанный файл метаданных в Блокноте, скопируйте его содержимое в буфер обмена, а затем вставьте в текстовое поле **IdP Meta Data** (Метаданные IdP) на панели **SAML Settings** (Параметры SAML).

    ![Раздел "IDP Meta Data" (Метаданные IDP) на стороне приложения](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_004.png)

13. Нажмите кнопку **Сохранить** .

> [!TIP]
> Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.  После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы. Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD

Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.

   ![Создание тестового пользователя Azure AD][100]

**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**

1. На портале Azure в области слева нажмите кнопку **Azure Active Directory**.

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-filecloud-tutorial/create_aaduser_01.png)

2. Чтобы открыть список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.

    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-filecloud-tutorial/create_aaduser_02.png)

3. Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна **Все пользователи** щелкните **Добавить**.

    ![Кнопка "Добавить"](./media/active-directory-saas-filecloud-tutorial/create_aaduser_03.png)

4. В диалоговом окне **Пользователь** сделайте следующее.

    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-filecloud-tutorial/create_aaduser_04.png)

    а. В поле **Имя** введите **BrittaSimon**.

    b. В поле **Имя пользователя** введите адрес электронной почты для пользователя Britta Simon.

    c. Установите флажок **Показать пароль** и запишите значение, которое отображается в поле **Пароль**.

    г) Щелкните **Создать**.
 
### <a name="create-a-filecloud-test-user"></a>Создание тестового пользователя FileCloud

Цель этого раздела — создать пользователя с именем Britta Simon в FileCloud. FileCloud поддерживает JIT-подготовку. Эта функция включена по умолчанию. В этом разделе никакие действия с вашей стороны не требуются. Пользователь создается при попытке получить доступ к приложению FileCloud (если он еще не существует).

>[!NOTE]
>Если вам нужно вручную создать пользователя, обратитесь в [службу поддержки клиентов FileCloud](mailto:support@codelathe.com). 

### <a name="assign-the-azure-ad-test-user"></a>Назначение тестового пользователя Azure AD

В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к FileCloud.

![Назначение роли пользователя][200] 

**Чтобы назначить пользователя Britta Simon в FileCloud, выполните следующие действия.**

1. На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.

    ![Назначение пользователя][201] 

2. Из списка приложений выберите **FileCloud**.

    ![Ссылка на FileCloud в списке "Приложения"](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_app.png)  

3. В меню слева выберите **Пользователи и группы**.

    ![Ссылка "Пользователи и группы"][202]

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Область "Добавление назначения"][203]

5. В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.

Щелкнув элемент "FileCloud" на панели доступа, вы автоматически войдете в приложение FileCloud.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по интеграции приложений SaaS с Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_203.png

