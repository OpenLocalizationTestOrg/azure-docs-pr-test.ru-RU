---
title: "Руководство по интеграции Azure Active Directory с ServiceNow | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и ServiceNow."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: a5a1a264-7497-47e7-b129-a1b5b1ebff5b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/16/2017
ms.author: jeedes
ms.openlocfilehash: 8b21c7b18c31f3111caa13d08efb5aa42ecc0e49
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicenow"></a>Руководство: интеграция Azure Active Directory с ServiceNow

В этом руководстве описано, как интегрировать ServiceNow с Azure Active Directory (Azure AD).

Интеграция Azure AD с приложением ServiceNow обеспечивает следующие преимущества.

- С помощью Azure AD вы можете управлять доступом к ServiceNow.
- Вы можете включить автоматический вход пользователей в ServiceNow (единый вход) с учетной записью Azure AD.
- Вы можете управлять учетными записями централизованно — на портале Azure.

Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Технические условия

Чтобы настроить интеграцию Azure AD с приложением ServiceNow, вам потребуется:

- подписка Azure AD;
- Экземпляр или клиент ServiceNow версии Calgary или выше (для ServiceNow).
- Экземпляр ServiceNow Express версии Helsinki или выше (для ServiceNow Express).
- В клиенте ServiceNow должен быть включен [подключаемый модуль единого входа для нескольких поставщиков](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0). Это можно сделать путем [отправки запроса на обслуживание](https://hi.service-now.com).

> [!NOTE]
> Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.

При проверке действий в этом учебнике соблюдайте следующие рекомендации:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Сценарий, описанный в этом учебнике, состоит из двух стандартных блоков.

1. Добавление ServiceNow из коллекции.
2. настройка и проверка единого входа в Azure AD.

## <a name="adding-servicenow-from-the-gallery"></a>Добавление ServiceNow из коллекции.
Чтобы настроить интеграцию ServiceNow с Azure AD, необходимо добавить ServiceNow из коллекции в список управляемых приложений SaaS.

**Чтобы добавить ServiceNow из коллекции, сделайте следующее:**

1. На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**. 

    ![Кнопка "Azure Active Directory"][1]

2. Перейдите к разделу **Корпоративные приложения**. Затем выберите **Все приложения**.

    ![Колонка "Корпоративные приложения"][2]
    
3. Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.

    ![Кнопка "Новое приложение"][3]

4. В поле поиска введите **ServiceNow**, на панели результатов выберите **ServiceNow** и нажмите кнопку **Добавить**, чтобы добавить это приложение.

    ![ServiceNow в списке результатов](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD

В этом разделе описано, как настроить и проверить единый вход Azure AD в ServiceNow с использованием тестового пользователя Britta Simon.

Чтобы настроить единый вход в Azure AD, необходимо знать, какой пользователь в ServiceNow соответствует пользователю в Azure AD. Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в ServiceNow.

Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в ServiceNow.

Чтобы настроить и проверить единый вход Azure AD в ServiceNow, вам потребуется выполнить действия в следующих стандартных блоках:

1. **[Настройка единого входа Azure AD в ServiceNow](#configure-azure-ad-single-sign-on-for-servicenow)** необходима, чтобы пользователи могли использовать эту функцию.
2. **[Настройка единого входа Azure AD в ServiceNow Express](#configure-azure-ad-single-sign-on-for-servicenow-express)** необходима, чтобы пользователи могли использовать эту функцию.
3. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.
4. **[Создание тестового пользователя ServiceNow](#create-a-servicenow-test-user)** требуется для создания пользователя Britta Simon в ServiceNow, связанного с соответствующим пользователем в Azure AD.
5. **[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.
6. **[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.

### <a name="configure-azure-ad-single-sign-on-for-servicenow"></a>Настройка единого входа в Azure AD для ServiceNow

В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении ServiceNow.

**Чтобы настроить единый вход Azure AD в ServiceNow, выполните следующие действия.**

1. На портале Azure на странице интеграции с приложением **ServiceNow** щелкните **Единый вход**.

    ![Ссылка "Настройка единого входа"][4]

2. В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_samlbase.png)

3. В разделе **Домены и URL-адреса приложения ServiceNow** сделайте следующее.

    ![Сведения о домене и URL-адресах единого входа приложения ServiceNow](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_url.png)

    a. В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<instance-name>.service-now.com/navpage.do`

    Б. В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<instance-name>.service-now.com`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Необходимо будет изменить эти значения, указав фактические URL-адрес для входа и идентификатор. Это описывается далее в этом руководстве.

4. В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-servicenow-tutorial/tutorial_general_400.png)

6. Для создания URL-адреса **метаданных** выполните следующие действия.

    a. Щелкните **Регистрация приложений**.
    
    ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/appregistrations.png)

    Б. Щелкните **Конечные точки**, чтобы открыть диалоговое окно **Конечные точки**.
    
    ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/endpointicon.png)
    
    c. Нажмите кнопку "Копировать", чтобы скопировать URL-адрес **документа метаданных федерации**, а затем вставьте его в блокнот.

    ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/endpoint.png)

    d. Теперь перейдите на страницу свойств **ServiceNow** и скопируйте **идентификатор приложения** с помощью кнопки **Копировать**, а затем вставьте его в Блокнот.

    ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/appid.png)

    д. Создайте **URL-адрес метаданных** по следующему шаблону: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`.  Скопируйте созданное значение в Блокнот, так как этот URL-адрес метаданных будет использоваться далее в этом руководстве.

7. Иначе говоря, для ServiceNow предоставляется служба настройки одним щелчком мыши, чтобы позволить Azure AD автоматически настроить ServiceNow для аутентификации на основе SAML. Чтобы включить эту службу, перейдите в раздел **Конфигурация ServiceNow** и щелкните **Настроить ServiceNow**, чтобы открыть окно "Настройка единого входа".

    ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_configure.png)

8. Введите имя экземпляра ServiceNow, имя администратора и его пароль в форму **Настройка единого входа**, затем щелкните **Настроить сейчас**. Обратите внимание, что для этого указываемому пользователю с правами администратора должна быть назначена роль **security_admin** в ServiceNow. В противном случае, чтобы вручную настроить ServiceNow для использования Azure AD в качестве поставщика удостоверений SAML, щелкните **Настроить единый вход вручную** и скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML** из раздела "Краткий справочник".

    ![Настройка URL-адреса приложения](./media/active-directory-saas-servicenow-tutorial/configure.png "Настройка URL-адреса приложения")

9. Войдите в приложение ServiceNow в качестве администратора.

10. Активируйте подключаемый модуль **Integration - Multiple Provider Single Sign-On Installer** (Интеграция — установщик единого входа для нескольких поставщиков), выполнив следующие действия.

    a. В левой области навигации найдите раздел **System Definition** (Определение системы) с помощью панели поиска и щелкните **Plugins** (Подключаемые модули).

    ![Активация подключаемого модуля](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "Activate plugin")

     Б. Найдите **Integration - Multiple Provider Single Sign-On Installer** (Интеграция — установщик единого входа для нескольких поставщиков).

     ![Активация подключаемого модуля](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "Activate plugin")

    c. Выберите подключаемый модуль. Щелкните правой кнопкой мыши и выберите **Activate/Upgrade** (Активировать или обновить).

    d. Нажмите кнопку **Активировать**.

11. В левой области навигации найдите раздел **Multi-Provider SSO** (Единый вход с помощью нескольких поставщиков) с помощью панели поиска, затем щелкните **Properties** (Свойства).

    ![Настройка URL-адреса приложения](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "Настройка URL-адреса приложения")

12. В диалоговом окне **Multiple Provider SSO Properties** (Свойства единого входа для нескольких поставщиков) выполните следующие действия.

    ![Настройка URL-адреса приложения](./media/active-directory-saas-servicenow-tutorial/ic7694981.png "Настройка URL-адреса приложения")

    a. Для параметра **Enable multiple provider SSO** (Включить единый вход для нескольких поставщиков) выберите значение **Yes** (Да).

    Б. Для параметра **Enable Auto Importing of users from all identity providers into the user table** (Включить автоматический импорт пользователей из всех поставщиков удостоверений в таблицу пользователей) выберите значение **Yes** (Да).

    c. Для параметра **Enable debug logging for the multiple provider SSO integration** (Включить ведение журнала отладки для интеграции нескольких поставщиков единого входа) выберите значение **Yes** (Да).

    d. В текстовом поле **The field on the user table that...** (Поле в пользовательской таблице) введите значение **user_name**.

    д. Выберите команду **Сохранить**.

13. В левой области навигации найдите раздел **Multi-Provider SSO** (Единый вход с помощью нескольких поставщиков) с помощью панели поиска, затем щелкните **x509 Certificates** (Сертификаты x509).

    ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "Настройка единого входа")

14. В диалоговом окне **X.509 Certificates** (Сертификаты X.509) нажмите кнопку **New** (Создать).

    ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/ic7694974.png "Настройка единого входа")

15. В диалоговом окне **X.509 Certificates** (Сертификаты X.509) выполните следующие действия.

    ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/ic7694975.png "Настройка единого входа")

    a. В текстовое поле **Name** (Имя) введите имя конфигурации (например, **TestSAML2.0**).

    Б. Установите флажок **Активно**.

    c. В поле **Format** (Формат) выберите **PEM**.

    d. В поле **Type** (Тип) выберите **Trust Store Cert** (Сертификат хранилища доверия).

    д. Откройте в Блокноте сертификат в кодировке Base-64, скачанный с портала Azure, скопируйте его содержимое в буфер обмена и вставьте в текстовое поле **PEM Certificate** (Сертификат PEM).

     f. Нажмите кнопку **Submit**(Отправить).

16. На панели навигации слева щелкните **Identity Providers**(Поставщики удостоверений).

    ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "Настройка единого входа")

17. В диалоговом окне **Identity Providers** (Поставщики удостоверений) нажмите кнопку **New** (Создать).

    ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/ic7694977.png "Настройка единого входа")

18. В диалоговом окне **Identity Providers** (Поставщики удостоверений) щелкните **SAML2 Update1?**.

    ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/ic7694978.png "Настройка единого входа")

19. В диалоговом окне SAML2 Update1 Properties (Свойства SAML2 Update1) выполните следующие действия.

    ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/idp.png "Настройка единого входа")

    a. В диалоговом окне **Import Identity Provider Metadata** (Импорт метаданных поставщика удостоверений) выберите **URL** (URL-адрес).

    Б. Введите **URL-адрес метаданных**, созданный на портале Azure.

    c. Щелкните **Импорт**.

20. Будет прочитан URL-адрес метаданных поставщика удостоверений, а также будут заполнены все поля сведений.

    ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/ic7694982.png "Настройка единого входа")

    a. В текстовое поле **Name** (Имя) введите имя конфигурации (например, **SAML 2.0**).

    Б. В текстовом поле **User Field** (Поле пользователя) введите значение **email** или **user_name**, в зависимости от того, какое поле используется для уникальной идентификации пользователей в развернутой службе ServiceNow.

    > [!NOTE]
    > Azure AD можно настроить таким образом, чтобы в качестве уникального идентификатора в токене SAML выдавался идентификатор пользователя Azure AD (имя участника-пользователя) или его электронный адрес. Для этого перейдите в раздел **ServiceNow > Атрибуты > Единый вход** на портале Azure и сопоставьте нужное поле с атрибутом **nameidentifier**. Значение, хранящееся для выбранного атрибута в Azure AD (например, имя участника-пользователя), должно соответствовать значению, хранящемуся в ServiceNow для заполненного поля (например, user_name).

    c. Скопируйте значение **ServiceNow Homepage** (Домашняя страница ServiceNow) и вставьте его в текстовое поле **URL-адрес для входа** в разделе **Домены и URL-адреса приложения ServiceNow** на портале Azure.

    > [!NOTE]
    > URL-адрес домашней страницы экземпляра ServiceNow состоит из **URL-адреса клиента ServiceNow** и **/navpage.do** (например, `https://fabrikam.service-now.com/navpage.do`).

    d. Скопируйте значение **Entity ID / Issuer** (Идентификатор сущности или издатель) и вставьте его в текстовое поле **Идентификатор** в разделе **Домены и URL-адреса приложения ServiceNow** на портале Azure.

     д. В поле **x509 Certificate**(Сертификат x509) отображается сертификат, созданный на предыдущем шаге.

### <a name="configure-azure-ad-single-sign-on-for-servicenow-express"></a>Настройка единого входа в Azure AD для ServiceNow Express

1. На портале Azure на странице интеграции с приложением **ServiceNow** щелкните **Единый вход**.

    ![Настройка единого входа][4]

2. В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.

    ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_samlbase.png)

3. В разделе **Домены и URL-адреса приложения ServiceNow** сделайте следующее.

    ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_url.png)

    a. В текстовом поле **URL-адрес для входа** введите значение в следующем формате: `https://<instance-name>.service-now.com/navpage.do`.

    Б. В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<instance-name>.service-now.com`

    > [!NOTE]
    > Эти значения приведены в качестве примера. Замените эти значения фактическим URL-адресом для входа и идентификатором. Чтобы получить эти значения, обратитесь к [группе поддержки клиентов ServiceNow](https://www.servicenow.com/support/contact-support.html).

4. В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.

    ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_certificate.png)

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/tutorial_general_400.png)

6. Иначе говоря, для ServiceNow предоставляется служба настройки одним щелчком мыши, чтобы позволить Azure AD автоматически настроить ServiceNow для аутентификации на основе SAML. Чтобы включить эту службу, перейдите в раздел **Конфигурация ServiceNow** и щелкните **Настроить ServiceNow**, чтобы открыть окно "Настройка единого входа".

    ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_configure.png)

7. Введите имя экземпляра ServiceNow, имя администратора и его пароль в форму **Настройка единого входа**, затем щелкните **Настроить сейчас**. Обратите внимание, что для этого указываемому пользователю с правами администратора должна быть назначена роль **security_admin** в ServiceNow. В противном случае, чтобы вручную настроить ServiceNow для использования Azure AD в качестве поставщика удостоверений SAML, щелкните **Настроить единый вход вручную** и скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML** из раздела "Краткий справочник".

    ![Настройка URL-адреса приложения](./media/active-directory-saas-servicenow-tutorial/configure.png "Настройка URL-адреса приложения")

8. Войдите в приложение ServiceNow Express в качестве администратора.

9. В расположенной слева области навигации щелкните **Единый вход**.

    ![Настройка URL-адреса приложения](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "Настройка URL-адреса приложения")

10. В диалоговом окне **Единый вход** щелкните значок конфигурации в правом верхнем углу и настройте следующие свойства.

    ![Настройка URL-адреса приложения](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "Настройка URL-адреса приложения")

    a. Передвиньте переключатель **Enable multiple provider SSO** (Включить единый вход для нескольких поставщиков) вправо.
    
    Б. Передвиньте переключатель **Enable debug logging for the multiple provider SSO integration** (Включить ведение журнала отладки для интеграции нескольких поставщиков единого входа) вправо.
    
    c. В текстовом поле **The field on the user table that...** (Поле в пользовательской таблице) введите значение **user_name**.

11. В диалоговом окне **Единый вход** щелкните **Добавить новый сертификат**.

    ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "Настройка единого входа")

12. В диалоговом окне **X.509 Certificates** (Сертификаты X.509) выполните следующие действия.

    ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/ic7694975.png "Настройка единого входа")

    a. В текстовое поле **Name** (Имя) введите имя конфигурации (например, **TestSAML2.0**).

    Б. Установите флажок **Активно**.

    c. В поле **Format** (Формат) выберите **PEM**.

    d. В поле **Type** (Тип) выберите **Trust Store Cert** (Сертификат хранилища доверия).

    д. Откройте в Блокноте сертификат в кодировке Base64, скачанный с портала Azure, скопируйте его содержимое в буфер обмена и вставьте в текстовое поле **PEM Certificate** (Сертификат PEM).

    f. Нажмите кнопку **Update** (Обновить).

13. В диалоговом окне **Единый вход** щелкните **Add New IdP** (Добавить нового поставщика удостоверений).

    ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "Настройка единого входа")

14. В диалоговом окне **Add New Identity Provider** (Добавление нового поставщика удостоверений) в разделе **Configure Identity Provider** (Настройка поставщика удостоверений) выполните следующие действия.

    ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "Настройка единого входа")

    a. В текстовое поле **Name** (Имя) введите имя конфигурации (например, **SAML 2.0**).

    Б. В поле **Identity Provider URL** (URL-адрес поставщика удостоверений) вставьте значение поля **Идентификатор поставщика удостоверений**, скопированное на портале Azure.
    
    c. В поле **Identity Provider's AuthnRequest** (Запрос на аутентификацию поставщика удостоверений) вставьте значение поля **URL-адрес запроса проверки подлинности**, скопированное на портале Azure.

    d. В поле **Identity Provider's SingleLogoutRequest** (Запрос на единый выход поставщика удостоверений) вставьте значение поля **URL-адрес службы единого выхода**, скопированное на портале Azure.

    д. В поле **Identity Provider Certificate** (Сертификат поставщика удостоверений) выберите сертификат, созданный на предыдущем шаге.

15. Щелкните **Дополнительные параметры** и в разделе **Additional Identity Provider Properties** (Дополнительные свойства поставщика удостоверений) выполните следующие действия.

    ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "Настройка единого входа")

    a. В текстовом поле **Protocol Binding for the IDP's SingleLogoutRequest** (Привязка протокола для запроса на единый выход поставщика удостоверений) введите **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.

    Б. В текстовое поле **NameID Policy** (Политика идентификатора имени) введите **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.

    c. В поле **AuthnContextClassRef Method** (Метод AuthnContextClassRef) введите `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`.

    d. Снимите флажок **Create an AuthnContextClass**(Создать класс контекста проверки подлинности).

16. В разделе **Additional Service Provider Properties** (Дополнительные свойства поставщика услуг) выполните следующие действия.

    ![Настройка единого входа](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "Настройка единого входа")

    a. В текстовое поле **ServiceNow Homepage** (Домашняя страница ServiceNow) введите URL-адрес домашней страницы экземпляра ServiceNow.

    > [!NOTE]
    > URL-адрес домашней страницы экземпляра ServiceNow состоит из **URL-адреса клиента ServiceNow** и **/navpage.do** (например, `https://fabrikam.service-now.com/navpage.do`).

    Б. В текстовое поле **Entity ID / Issuer** (Идентификатор сущности или издатель) введите URL-адрес клиента ServiceNow.

    c. В текстовое поле **Audience URI** (URI аудитории) введите URL-адрес клиента ServiceNow.

    d. В текстовое поле **Clock Skew** (Разница в показаниях часов) введите **60**.

    д. В текстовом поле **User Field** (Поле пользователя) введите значение **email** или **user_name**, в зависимости от того, какое поле используется для уникальной идентификации пользователей в развернутой службе ServiceNow.

    > [!NOTE]
    > Azure AD можно настроить таким образом, чтобы в качестве уникального идентификатора в токене SAML выдавался идентификатор пользователя Azure AD (имя участника-пользователя) или его электронный адрес. Для этого перейдите в раздел **ServiceNow > Атрибуты > Единый вход** на портале Azure и сопоставьте нужное поле с атрибутом **nameidentifier**. Значение, хранящееся для выбранного атрибута в Azure AD (например, имя участника-пользователя), должно соответствовать значению, хранящемуся в ServiceNow для заполненного поля (например, user_name).

    f. Выберите команду **Сохранить**.

> [!TIP]
> Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.  После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы. Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD

Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.

   ![Создание тестового пользователя Azure AD][100]

**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**

1. На портале Azure в области слева нажмите кнопку **Azure Active Directory**.

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-servicenow-tutorial/create_aaduser_01.png)

2. Чтобы открыть список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.

    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-servicenow-tutorial/create_aaduser_02.png)

3. Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна **Все пользователи** щелкните **Добавить**.

    ![Кнопка "Добавить"](./media/active-directory-saas-servicenow-tutorial/create_aaduser_03.png)

4. В диалоговом окне **Пользователь** сделайте следующее.

    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-servicenow-tutorial/create_aaduser_04.png)

    a. В поле **Имя** введите **BrittaSimon**.

    Б. В поле **Имя пользователя** введите адрес электронной почты для пользователя Britta Simon.

    c. Установите флажок **Показать пароль** и запишите значение, которое отображается в поле **Пароль**.

    d. Нажмите кнопку **Создать**.
 
### <a name="create-a-servicenow-test-user"></a>Создание тестового пользователя ServiceNow

В этом разделе описано, как создать пользователя Britta Simon в ServiceNow. Если вы не знаете, как добавить пользователя в свою учетную запись ServiceNow или ServiceNow Express, обратитесь к [группе поддержки клиентов ServiceNow](https://www.servicenow.com/support/contact-support.html).

### <a name="assign-the-azure-ad-test-user"></a>Назначение тестового пользователя Azure AD

В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив доступ к ServiceNow.

![Назначение роли пользователя][200] 

**Чтобы назначить пользователя Britta Simon в ServiceNow, сделайте следующее:**

1. На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений выберите **ServiceNow**.

    ![Ссылка на ServiceNow в списке приложений](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_app.png)  

3. В меню слева выберите **Пользователи и группы**.

    ![Ссылка "Пользователи и группы"][202]

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Область "Добавление назначения"][203]

5. В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.

Щелкнув плитку ServiceNow на панели доступа, вы автоматически войдете в приложение ServiceNow.
Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по интеграции приложений SaaS с Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_203.png

