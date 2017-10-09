---
title: "aaaAuthorize учетными записями разработчиков с помощью Azure Active Directory B2C - службе управления API Azure | Документы Microsoft"
description: "Узнайте, каким образом tooauthorize пользователей с помощью Azure Active Directory B2C в службе управления API."
services: api-management
documentationcenter: API Management
author: miaojiang
manager: erikre
editor: 
ms.assetid: 33a69a83-94f2-4e4e-9cef-f2a5af3c9732
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 28f7cae53138938dbbc848b4afcbf08b72690e37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-by-using-azure-active-directory-b2c-in-azure-api-management"></a>Как разработчик tooauthorize учетных записей с помощью Azure Active Directory B2C в службе управления API Azure
## <a name="overview"></a>Обзор
Azure Active Directory B2C — это облачное решение, позволяющее управлять удостоверениями в веб-приложениях и мобильных приложениях, с которыми взаимодействуют клиенты. Он используется портал разработчиков tooyour toomanage доступа. В этом руководстве представлены hello конфигурации, необходимые в вашей toointegrate службы управления API с Azure Active Directory B2C. Сведения о включении портал разработчиков toohello доступ с помощью классической Azure Active Directory см. в разделе [как разработчик tooauthorize учетных записей с помощью Azure Active Directory].

> [!NOTE]
> toocomplete hello шаги данного руководства, сначала нужно toocreate клиента Azure Active Directory B2C приложение. Кроме того требуются ли toohave регистрации и входа политики готова. Дополнительные сведения см. в статье [Azure Active Directory B2C: регистрация и вход пользователей в приложения].

## <a name="authorize-developer-accounts-by-using-azure-active-directory-b2c"></a>Авторизация учетных записей разработчиков с помощью Azure Active Directory B2C

1. tooget работу, нажмите кнопку **портал издателя** в hello портала Azure для вашей службе управления API. Откроется портал издателя управления API toohello.

   ![Портал издателя][api-management-management-console]

   > [!NOTE]
   > Если вы еще не создали экземпляра службы управления API, см. раздел [создания экземпляра службы управления API] [ Create an API Management service instance] в hello [Приступая к работе с API управления Azure учебника][Get started with Azure API Management].

2. На hello **API управления** меню, нажмите кнопку **безопасности**. На hello **удостоверения** выберите **Azure Active Directory B2C**.

  ![Внешние удостоверения 1][api-management-howto-aad-b2c-security-tab]

3. Запишите hello **URL-адрес перенаправления** и переключении tooAzure Active Directory B2C в hello портал Azure.

  ![Внешние удостоверения 2][api-management-howto-aad-b2c-security-tab-reply-url]

4. Нажмите кнопку hello **приложений** кнопки.

  ![Регистрация нового приложения 1][api-management-howto-aad-b2c-portal-menu]

5. Нажмите кнопку hello **добавить** кнопку приложения toocreate новый Azure Active Directory B2C.

  ![Регистрация нового приложения 2][api-management-howto-aad-b2c-add-button]

6. В hello **новое приложение** колонки, введите имя для приложения hello. Выберите **Да** под параметром **Веб-приложения и веб-API** и **Да** под параметром **Разрешить неявный поток**. А затем копировать hello **URL-адрес перенаправления** из hello **Azure Active Directory B2C** раздел hello **удостоверения** вкладку в портале издателю hello и вставьте его в hello **URL-адрес ответа** текстовое поле.

  ![Регистрация нового приложения 3][api-management-howto-aad-b2c-app-details]

7. Нажмите кнопку hello **создать** кнопки. При создании приложения hello, оно появляется в hello **приложений** колонку. Щелкните toosee имя приложения hello сведения о нем.

  ![Регистрация нового приложения 4][api-management-howto-aad-b2c-app-created]

8. Из hello **свойства** колонки, hello копирования **идентификатор приложения** toohello буфер обмена.

  ![Идентификатор приложения 1][api-management-howto-aad-b2c-app-id]

9. Перейдите назад toohello портал издателя и вставьте идентификатор hello в hello **идентификатор клиента** текстовое поле.

  ![Идентификатор приложения 2][api-management-howto-aad-b2c-client-id]

10. Перейдите назад toohello портал Azure, щелкните hello **ключей** , а затем нажмите **создать ключ**. Нажмите кнопку **Сохранить** toosave hello конфигурации и отображения hello **ключ приложения**. Буфер обмена Копировать hello toohello ключа.

  ![Ключ приложения 1][api-management-howto-aad-b2c-app-key]

11. Коммутатор задней toohello портала и вставить hello ключ издателя в hello **секрет клиента** текстовое поле.

  ![Ключ приложения 2][api-management-howto-aad-b2c-client-secret]

12. Укажите доменное имя клиента Azure Active Directory B2C hello в hello **допускается клиента**.

  ![Разрешенный клиент][api-management-howto-aad-b2c-allowed-tenant]

13. Укажите hello **политики регистрации** и **Signin политики**. При необходимости можно также предоставить hello **редактирование политики профиля** и **политика сброса пароля**.

  ![Политики][api-management-howto-aad-b2c-policies]

  > [!NOTE]
  > Дополнительные сведения о политиках см. в статье [Azure Active Directory B2C: расширяемая инфраструктура политик].

14. После выбора hello требуемую конфигурацию, нажмите кнопку **Сохранить**.

  После сохранения изменений hello разработчикам будет может toocreate новые учетные записи и войдите в портал разработчиков toohello с использованием Azure Active Directory B2C.

## <a name="sign-up-for-a-developer-account-by-using-azure-active-directory-b2c"></a>Регистрация учетных записей разработчиков с помощью Azure Active Directory B2C

1. toosign для использования учетной записи разработчика с помощью Azure Active Directory B2C откройте новое окно браузера и перейдите на портал разработчиков toohello. Нажмите кнопку hello **зарегистрироваться** кнопки.

   ![Портал разработчика 1][api-management-howto-aad-b2c-dev-portal]

2. Выберите toosign с **Azure Active Directory B2C**.

   ![Портал разработчика 2][api-management-howto-aad-b2c-dev-portal-b2c-button]

3. Вы перенаправленный toohello политики регистрации, настроенную в предыдущем разделе hello. Нажмите кнопку toosign, используя свой адрес электронной почты или один из существующих учетных записей социальных сетей.

   > [!NOTE]
   > Если Azure Active Directory B2C hello единственный параметр, который включен в hello **удостоверения** вкладку портала издателя hello, вы будете политики регистрации перенаправленных toohello напрямую.

   ![Портал разработчика][api-management-howto-aad-b2c-dev-portal-b2c-options]

   После завершения регистрации hello вы портал разработчиков перенаправленный toohello назад. Теперь, выполнив вход в портал разработчиков toohello для вашего экземпляра службы управления API.

    ![Регистрация завершена][api-management-registration-complete]

## <a name="next-steps"></a>Дальнейшие действия

*  [Azure Active Directory B2C: регистрация и вход пользователей в приложения]
*  [Azure Active Directory B2C: расширяемая инфраструктура политик]
*  [Azure Active Directory (AD) B2C: организация регистрации и входа для потребителей с учетными записями Microsoft]
*  [Azure Active Directory B2C: организация регистрации и входа для потребителей с учетными записями Google+]
*  [Azure Active Directory B2C: регистрация и вход пользователей с помощью учетных записей LinkedIn]
*  [Azure Active Directory B2C: регистрация и вход пользователей с учетными записями Facebook]




[api-management-howto-aad-b2c-security-tab]: ./media/api-management-howto-aad-b2c/api-management-b2c-security-tab.PNG
[api-management-howto-aad-b2c-security-tab-reply-url]: ./media/api-management-howto-aad-b2c/api-management-b2c-security-tab-reply-url.PNG
[api-management-howto-aad-b2c-portal-menu]: ./media/api-management-howto-aad-b2c/api-management-b2c-portal-menu.PNG
[api-management-howto-aad-b2c-add-button]: ./media/api-management-howto-aad-b2c/api-management-b2c-add-button.PNG
[api-management-howto-aad-b2c-app-details]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-details.PNG
[api-management-howto-aad-b2c-app-created]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-created.PNG
[api-management-howto-aad-b2c-app-id]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-id.PNG
[api-management-howto-aad-b2c-client-id]: ./media/api-management-howto-aad-b2c/api-management-b2c-client-id.PNG
[api-management-howto-aad-b2c-app-key]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-key.PNG
[api-management-howto-aad-b2c-app-key-saved]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-key-saved.PNG
[api-management-howto-aad-b2c-client-secret]: ./media/api-management-howto-aad-b2c/api-management-b2c-client-secret.PNG
[api-management-howto-aad-b2c-allowed-tenant]: ./media/api-management-howto-aad-b2c/api-management-b2c-allowed-tenant.PNG
[api-management-howto-aad-b2c-policies]: ./media/api-management-howto-aad-b2c/api-management-b2c-policies.PNG
[api-management-howto-aad-b2c-dev-portal]: ./media/api-management-howto-aad-b2c/api-management-b2c-dev-portal.PNG
[api-management-howto-aad-b2c-dev-portal-b2c-button]: ./media/api-management-howto-aad-b2c/api-management-b2c-dev-portal-b2c-button.PNG
[api-management-howto-aad-b2c-dev-portal-b2c-options]: ./media/api-management-howto-aad-b2c/api-management-b2c-dev-portal-b2c-options.PNG
[api-management-complete-registration]: ./media/api-management-howto-aad/api-management-complete-registration.PNG
[api-management-registration-complete]: ./media/api-management-howto-aad/api-management-registration-complete.png

[api-management-management-console]: ./media/api-management-howto-aad/api-management-management-console.png
[api-management-security-external-identities]: ./media/api-management-howto-aad/api-management-b2c-security-tab.png
[api-management-security-aad-new]: ./media/api-management-howto-aad/api-management-security-aad-new.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-aad/api-management-new-aad-application-menu.png
[api-management-new-aad-application-1]: ./media/api-management-howto-aad/api-management-new-aad-application-1.png
[api-management-new-aad-application-2]: ./media/api-management-howto-aad/api-management-new-aad-application-2.png
[api-management-new-aad-app-created]: ./media/api-management-howto-aad/api-management-new-aad-app-created.png
[api-management-aad-app-permissions]: ./media/api-management-howto-aad/api-management-aad-app-permissions.png
[api-management-aad-app-client-id]: ./media/api-management-howto-aad/api-management-aad-app-client-id.png
[api-management-client-id]: ./media/api-management-howto-aad/api-management-client-id.png
[api-management-aad-key-before-save]: ./media/api-management-howto-aad/api-management-aad-key-before-save.png
[api-management-aad-key-after-save]: ./media/api-management-howto-aad/api-management-aad-key-after-save.png
[api-management-client-secret]: ./media/api-management-howto-aad/api-management-client-secret.png
[api-management-client-allowed-tenants]: ./media/api-management-howto-aad/api-management-client-allowed-tenants.png
[api-management-client-allowed-tenants-save]: ./media/api-management-howto-aad/api-management-client-allowed-tenants-save.png
[api-management-aad-delegated-permissions]: ./media/api-management-howto-aad/api-management-aad-delegated-permissions.png
[api-management-dev-portal-signin]: ./media/api-management-howto-aad/api-management-dev-portal-signin.png
[api-management-aad-signin]: ./media/api-management-howto-aad/api-management-aad-signin.png
[api-management-aad-app-multi-tenant]: ./media/api-management-howto-aad/api-management-aad-app-multi-tenant.png
[api-management-aad-reply-url]: ./media/api-management-howto-aad/api-management-aad-reply-url.png
[api-management-permissions-form]: ./media/api-management-howto-aad/api-management-permissions-form.png
[api-management-configure-product]: ./media/api-management-howto-aad/api-management-configure-product.png
[api-management-add-groups]: ./media/api-management-howto-aad/api-management-add-groups.png
[api-management-select-group]: ./media/api-management-howto-aad/api-management-select-group.png
[api-management-aad-groups-list]: ./media/api-management-howto-aad/api-management-aad-groups-list.png
[api-management-aad-group-added]: ./media/api-management-howto-aad/api-management-aad-group-added.png
[api-management-groups]: ./media/api-management-howto-aad/api-management-groups.png
[api-management-edit-group]: ./media/api-management-howto-aad/api-management-edit-group.png

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[Accessing hello Graph API]: http://msdn.microsoft.com/library/azure/dn132599.aspx#BKMK_Graph
[Azure Active Directory B2C: регистрация и вход пользователей в приложения]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview
[как разработчик tooauthorize учетных записей с помощью Azure Active Directory]: https://docs.microsoft.com/azure/api-management/api-management-howto-aad
[Azure Active Directory B2C: расширяемая инфраструктура политик]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-policies
[Azure Active Directory (AD) B2C: организация регистрации и входа для потребителей с учетными записями Microsoft]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-msa-app
[Azure Active Directory B2C: организация регистрации и входа для потребителей с учетными записями Google+]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-goog-app
[Azure Active Directory B2C: регистрация и вход пользователей с учетными записями Facebook]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-fb-app
[Azure Active Directory B2C: регистрация и вход пользователей с помощью учетных записей LinkedIn]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-li-app

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

[Log in toohello Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account
