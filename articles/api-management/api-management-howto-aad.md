---
title: "с помощью Azure Active Directory - Azure API управления учетными записями разработчиков aaaAuthorize | Документы Microsoft"
description: "Узнайте, каким образом tooauthorize пользователей с помощью Azure Active Directory в службе управления API."
services: api-management
documentationcenter: API Management
author: steved0x
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
ms.openlocfilehash: ebf5447a509a47df35e4262138bfcf423cb1dd5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-using-azure-active-directory-in-azure-api-management"></a>Как разработчик tooauthorize учетных записей с помощью Azure Active Directory в Azure API Management
## <a name="overview"></a>Обзор
В этом руководстве показано, как tooenable доступ к toohello портал разработчиков для пользователей из Azure Active Directory. В этом руководстве также показано, как группы пользователей Azure Active Directory, добавив внешней группы, содержащие toomanage hello пользователей Azure Active Directory.

> toocomplete hello шаги в этом руководстве сначала нужно Azure Active Directory в какие toocreate приложения.
> 
> 

## <a name="how-tooauthorize-developer-accounts-using-azure-active-directory"></a>Как разработчик tooauthorize учетных записей с помощью Azure Active Directory
tooget работу, нажмите кнопку **портал издателя** в hello портала Azure для вашей службе управления API. Откроется портал издателя управления API toohello.

![Портал издателя][api-management-management-console]

> Если вы еще не создали экземпляра службы управления API, см. раздел [создания экземпляра службы управления API] [ Create an API Management service instance] в hello [приступить к работе со службой управления API Azure] [ Get started with Azure API Management] учебника.
> 
> 

Нажмите кнопку **безопасности** из hello **API управления** меню hello слева и щелкните **внешних удостоверений**.

![External Identities][api-management-security-external-identities]

В меню **Azure Active Directory** (Внешние удостоверения). Запишите hello **URL-адрес перенаправления** и переключении tooyour Azure Active Directory в hello классический портал Azure.

![External Identities][api-management-security-aad-new]

Нажмите кнопку hello **добавить** toocreate новое приложение Azure Active Directory, а кнопку **добавить приложение, разрабатываемое моей организацией**.

![Добавление нового приложения Azure Active Directory][api-management-new-aad-application-menu]

Введите имя для приложения hello, выберите **веб-приложение или веб-API**и нажмите кнопку Далее hello.

![Новое приложение Azure Active Directory][api-management-new-aad-application-1]

Для **URL-адрес входа**, введите hello URL-адрес входа портала разработчиков. В этом примере hello **URL-адрес входа** — `https://aad03.portal.current.int-azure-api.net/signin`. 

Для hello **URL ИД приложения**, введите домен по умолчанию hello или пользовательского домена для hello Azure Active Directory и добавьте tooit уникальная строка. В этом примере hello домен по умолчанию **https://contoso5api.onmicrosoft.com** используется с суффиксом hello **/api** указанного.

![Свойства нового приложения Azure Active Directory][api-management-new-aad-application-2]

Щелкните toosave кнопку флажок hello и создание приложения hello и переключение toohello **Настройка** вкладке tooconfigure hello нового приложения.

![Новое приложение Azure Active Directory создано][api-management-new-aad-app-created]

Если в нескольких каталогах Azure Active Directory будет toobe, используемый для этого приложения, нажмите кнопку **Да** для **приложение является мультитенантным**. по умолчанию Hello — **нет**.

![Приложение является мультитенантным][api-management-aad-app-multi-tenant]

Копировать hello **URL-адрес перенаправления** из hello **Azure Active Directory** раздел hello **внешних удостоверений** вкладку в портале издателю hello и вставьте его в hello **URL-адрес ответа** текстовое поле. 

![URL-адрес ответа][api-management-aad-reply-url]

Вкладка, выберите hello настройки прокрутки внизу toohello hello **разрешения приложения** раскрывающийся список и проверьте **читать данные каталога**.

![Разрешения приложения][api-management-aad-app-permissions]

Выберите hello **Делегирование разрешений** раскрывающийся список и проверьте **разрешить вход и чтение профилей пользователей**.

![Делегированные разрешения][api-management-aad-delegated-permissions]

> Дополнительные сведения о приложении и делегированные разрешения см. в разделе [hello доступ к Graph API][Accessing hello Graph API].
> 
> 

Копировать hello **идентификатор клиента** toohello буфер обмена.

![Идентификатор клиента][api-management-aad-app-client-id]

Перейдите назад toohello портал издателя и вставьте в hello **идентификатор клиента** копируется из конфигурации приложения hello Azure Active Directory.

![Идентификатор клиента][api-management-client-id]

Перейдите назад toohello конфигурацию Azure Active Directory, а щелкните hello **выберите длительность** раскрывающееся меню в hello **ключей** статьи и указать интервал. В данном примере используется интервал **1 год**.

![Ключ][api-management-aad-key-before-save]

Нажмите кнопку **Сохранить** toosave hello конфигурации и отображения hello ключ. Буфер обмена Копировать hello toohello ключа.

> Запишите этот ключ. После закрытия окна конфигурации hello Azure Active Directory hello ключ не будет отображаться в дальнейшем.
> 
> 

![Ключ][api-management-aad-key-after-save]

Коммутатор задней toohello портала и вставить hello ключ издателя в hello **секрет клиента** текстовое поле.

![Секрет клиента][api-management-client-secret]

**Допускается клиентов** указывает, какие каталоги имеют доступ toohello API-интерфейсов экземпляра службы управления API hello. Укажите домены hello hello вы хотите получить доступ toogrant toowhich экземпляров Azure Active Directory. Несколько доменов можно разделять символами начала новой строки, пробелами или запятыми.

![Allowed Tenants][api-management-client-allowed-tenants]


Когда hello требуемого указана конфигурация, щелкните **Сохранить**.

![Сохранить][api-management-client-allowed-tenants-save]

После сохранения изменений hello пользователей hello в hello указан Azure Active Directory можно войти в портал разработчиков toohello, следуя указаниям hello [вход с использованием учетной записи Azure Active Directory портал разработчиков toohello] [Log in toohello Developer portal using an Azure Active Directory account].

Можно указать несколько доменов в hello **клиентам разрешено** раздела. Перед любой пользователь может входить в систему с разных доменах hello исходного домена, где зарегистрирован приложения hello, является глобальным администратором другого домена hello должен давать разрешение tooaccess приложения hello данных каталога. разрешение toogrant hello глобальный администратор должен составлять слишком`https://<URL of your developer portal>/aadadminconsent` (например, https://contoso.portal.azure-api.net/aadadminconsent), тип в доменном имени hello hello им нужен доступ tooand toogive клиента Active Directory, нажмите кнопку Отправить. В следующих hello пример, глобальный администратор `miaoaad.onmicrosoft.com` пытается toogive разрешение toothis определенного портал. 

![Разрешения][api-management-aad-consent]

В следующем экране hello hello глобального администратора будет запрашиваемые tooconfirm, предоставление разрешения hello. 

![Разрешения][api-management-permissions-form]

> Если веб-глобального администратора toolog в до разрешения предоставляются глобальным администратором, неудачной попытки входа hello и отображается экран ошибки.
> 
> 

## <a name="how-tooadd-an-external-azure-active-directory-group"></a>Как tooadd внешних Azure Active Directory группы
После включения доступа для пользователей в Azure Active Directory, можно добавить группы Azure Active Directory в API управления toomore легко управлять ассоциации hello разработчиков hello в группе hello с продуктами требуемого hello.

> Вначале нужно настроить tooconfigure внешней группы Azure Active Directory, hello Azure Active Directory на вкладке hello удостоверения с помощью процедуры hello в предыдущем разделе hello. 
> 
> 

Внешние группы Azure Active Directory добавляются из hello **видимость** вкладку hello продукта, для которого вы хотите группу toohello toogrant доступа. Нажмите кнопку **продуктов**и щелкните имя нужного продукта hello hello.

![Настройка продукта][api-management-configure-product]

Переключение toohello **видимость** и нажмите кнопку **Добавление групп из Azure Active Directory**.

![Добавление групп][api-management-add-groups]

Выберите hello **клиента Azure Active Directory** из hello раскрывающегося списка, а затем имя нужной группы hello в hello типа hello **группы** toobe добавлено текстовое поле.

![Выбор группы][api-management-select-group]

Имя этой группы могут находиться в hello **группы** список для Azure Active Directory, как показано в следующий пример hello.

![Список групп Azure Active Directory][api-management-aad-groups-list]

Нажмите кнопку **добавить** toovalidate hello имя группы и добавить группу hello. В этом примере hello **разработчики 5 Contoso** внешней группы будет добавлен. 

![Группа добавлена][api-management-aad-group-added]

Нажмите кнопку **Сохранить** toosave hello новое выделение группы.

После настройки группы Azure Active Directory из одного продукта является доступной toobe проверяется для hello **видимость** вкладке hello других продуктов в hello экземпляра службы управления API.

tooreview и настроить свойства hello для внешних групп, как только они были добавлены, щелкните имя hello hello группы из hello **группы** вкладки.

![Управление группами][api-management-groups]

Здесь можно изменить hello **имя** и hello **описание** hello группы.

![Изменение группы][api-management-edit-group]

Пользователям hello настроенных Azure Active Directory можно войти в портал разработчиков toohello и представление и подписаться tooany группы, для которых они имеют видимость по инструкциям hello в следующем разделе hello.

## <a name="how-toolog-in-toohello-developer-portal-using-an-azure-active-directory-account"></a>Как toolog на портале разработчиков toohello, используя учетную запись Azure Active Directory
toolog в портал разработчиков hello, используя учетную запись Azure Active Directory настроен в предыдущих разделах hello, откройте новое окно браузера, используя hello **URL-адрес входа** из конфигурации приложения hello Active Directory и нажмите кнопку **Azure Active Directory**.

![Портал разработчика][api-management-dev-portal-signin]

Введите учетные данные hello одного из пользователей hello в Azure Active Directory и нажмите кнопку **входа**.

![входа][api-management-aad-signin]

Может появиться запрос с регистрационной формой, если требуются какие-либо дополнительные сведения. Заполните форму регистрации hello и нажмите кнопку **зарегистрироваться**.

![Регистрация][api-management-complete-registration]

Теперь ваш пользователь вошел в портале для разработчиков hello для вашего экземпляра службы управления API.

![Регистрация завершена][api-management-registration-complete]

[api-management-management-console]: ./media/api-management-howto-aad/api-management-management-console.png
[api-management-security-external-identities]: ./media/api-management-howto-aad/api-management-security-external-identities.png
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
[api-management-complete-registration]: ./media/api-management-howto-aad/api-management-complete-registration.png
[api-management-registration-complete]: ./media/api-management-howto-aad/api-management-registration-complete.png
[api-management-aad-app-multi-tenant]: ./media/api-management-howto-aad/api-management-aad-app-multi-tenant.png
[api-management-aad-reply-url]: ./media/api-management-howto-aad/api-management-aad-reply-url.png
[api-management-aad-consent]: ./media/api-management-howto-aad/api-management-aad-consent.png
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

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

[Log in toohello Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account

