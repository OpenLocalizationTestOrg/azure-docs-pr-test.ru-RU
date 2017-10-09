---
title: "Azure Active Directory манифест приложения hello aaaUnderstanding | Документы Microsoft"
description: "Подробную информацию манифеста приложения hello Azure Active Directory, который представляет конфигурацию удостоверения приложения в клиенте Azure AD и используемый toofacilitate авторизации OAuth, взаимодействие согласия и многое другое."
services: active-directory
documentationcenter: 
author: sureshja
manager: mbaldwin
editor: 
ms.assetid: 4804f3d4-0ff1-4280-b663-f8f10d54d184
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: sureshja
ms.custom: aaddev
ms.reviewer: elisol
ms.openlocfilehash: 096c9d5501edbfc08731fea670cee559d4442ad1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-azure-active-directory-application-manifest"></a>Основные сведения о манифесте приложения hello Azure Active Directory
Приложения, которые интегрируются с Azure Active Directory (AD) должен быть зарегистрирован с клиентом Azure AD с помощью конфигурации постоянное удостоверение для приложения hello. Эта конфигурация был запрошен во время выполнения, Включение сценариев, позволяющих приложения toooutsource и Брокер проверки подлинности и авторизации с помощью Azure AD. Дополнительные сведения о модели приложения hello Azure AD см. в разделе hello [Добавление, обновление и удаление приложения] [ ADD-UPD-RMV-APP] статьи.

## <a name="updating-an-applications-identity-configuration"></a>Обновление конфигурации удостоверения для приложения
Фактически несколько параметров доступны обновления свойств hello на конфигурацию удостоверения приложения, которые могут меняться в возможностях и степени сложности, включая следующие hello:

* Hello  **[портал Azure] [ AZURE-PORTAL] веб-интерфейсом** позволяет tooupdate hello наиболее распространенных свойств приложения. Это быстрый hello и как минимум ошибкам способом Ошибка обновления свойств приложения, но не предоставляют свойства tooall полный доступ, как hello следующих двух методов.
* Для более сложных сценариев, в которых требуется tooupdate свойства, которые не представлены в hello классический портал Azure, можно изменить hello **манифест приложения**. Это hello посвящена эта статья и рассматривается более подробно в следующем разделе hello.
* Можно также слишком**написать приложение, использующее hello [Graph API] [ GRAPH-API]**  tooupdate, что требует приложения hello большинство усилий. Возможно, привлекательным вариантом, если вы пишете программное обеспечение для управления, или вам tooupdate свойства приложения на регулярной основе в автоматическом режиме.

## <a name="using-hello-application-manifest-tooupdate-an-applications-identity-configuration"></a>С помощью tooupdate манифеста приложения hello конфигурацию удостоверения приложения
Через hello [портал Azure][AZURE-PORTAL], вы можете управлять конфигурацию удостоверения приложения, обновление манифеста приложения hello, с помощью редактора манифеста встроенного hello. Можно также загрузить и отправить манифест приложения hello в формате JSON. Реальный файл не хранится в каталоге hello. Hello манифест приложения просто операция HTTP GET на сущность приложения hello Azure AD Graph API, который hello передачи операции HTTP PATCH на сущность приложения hello.

В результате в формате hello toounderstand порядка и свойств манифеста приложения hello, нужно будет tooreference hello Graph API [сущность приложения] [ APPLICATION-ENTITY] документации. Вот некоторые примеры изменений, которые можно выполнить с помощью отправки манифеста приложения.

* **Объявление областей разрешений (oauth2Permissions)**, предоставляемых через веб-API. См. раздел «TooOther предоставление веб-API приложения» hello в [интеграция приложений с Azure Active Directory] [ INTEGRATING-APPLICATIONS-AAD] сведения о реализации олицетворения пользователя с помощью hello oauth2Permissions область делегированных разрешений. Как упоминалось ранее, свойства сущности приложения описаны в Graph API hello [сущности и сложный тип] [ APPLICATION-ENTITY] статье по ссылкам, включая hello oauth2Permissions свойство, являющееся Коллекция типа [OAuth2Permission][APPLICATION-ENTITY-OAUTH2-PERMISSION].
* **Объявление ролей приложения (appRoles), предоставляемых приложением**. Hello объекта приложений appRoles свойство является коллекцией типа [AppRole][APPLICATION-ENTITY-APP-ROLE]. В разделе hello [управления доступом в Azure AD с помощью облачных приложений на основе ролей] [ RBAC-CLOUD-APPS-AZUREAD] статье в качестве примера реализации.
* **Объявите известных клиентских приложений (knownClientApplications)**, что позволит toologically идентичных hello согласия hello указан клиентского приложения toohello ресурсов и веб-API.
* **Запрос утверждения членства в группах Azure AD tooissue** для hello вход пользователя (groupMembershipClaims).  Это также может быть настроенный tooissue утверждения о hello directory ролей членства пользователя. . В разделе hello [авторизации в облачных приложений, с помощью групп AD] [ AAD-GROUPS-FOR-AUTHORIZATION] статье в качестве примера реализации.
* **Разрешить вашего приложения, toosupport OAuth 2.0 неявного предоставления** потоков (oauth2AllowImplicitFlow). Этот тип потоков доступа используется на страницах со встроенным JavaScript или в одностраничных приложениях (SPA). Дополнительные сведения о предоставления неявное авторизации hello. в разделе [поток в Azure Active Directory разрешений hello основные сведения о неявных OAuth2][IMPLICIT-GRANT].
* **Включить использование X509 сертификатов, как секретный ключ hello** (keyCredentials). В разделе hello [создать приложения службы и управляющая программа в Office 365] [ O365-SERVICE-DAEMON-APPS] и [tooauth руководство разработчика с API диспетчера ресурсов Azure] [ DEV-GUIDE-TO-AUTH-WITH-ARM] статьи, примеры реализации.
* **Добавление нового универсального кода ресурса (URI) идентификатора приложения** (identifierURIs[]). URI ИД приложения используются toouniquely идентификации приложения в рамках своего клиента Azure AD (или нескольких клиентов Azure AD, для сценариев с несколькими клиентами при указании через проверенный пользовательский домен). Они используются при запросе разрешения tooa ресурсов приложения, или получение токена доступа для ресурса приложения. При обновлении этого элемента hello того же обновления становится коллекцию [] servicePrincipalNames toohello соответствующего участника службы, которая живет в домашней клиента приложения hello.

Hello манифест приложения также предоставляет tootrack хорошим способом hello состояние регистрации вашего приложения. Так как она доступна в формате JSON, представление файла hello может проверяться в свою систему управления версиями, а также исходный код вашего приложения.

## <a name="step-by-step-example"></a>Пример подробными инструкциями
Теперь позволяет выполнить пошаговую tooupdate необходимые шаги hello конфигурацию удостоверения приложения с помощью манифеста приложения hello. Одно из предыдущих примеров, hello будут рассматриваться отображаются как toodeclare новое разрешение на уровне для ресурса приложения:

1. Войдите в toohello [портал Azure][AZURE-PORTAL].
2. После вы прошли проверку подлинности, выберите клиент Azure AD, выбрав его из hello правом верхнем углу страницы приветствия.
3. Выберите **Azure Active Directory** расширения из hello слева на панели навигации и щелкните **регистрации приложения**.
4. Найдите приложение hello tooupdate в списке hello и щелкните на нем.
5. На странице приложения hello нажмите **манифеста** tooopen hello встроенного редактора манифеста. 
6. Можно непосредственно редактировать манифест hello, с помощью этого редактора. Обратите внимание, этот манифест hello следует схеме hello для hello [сущность приложения] [ APPLICATION-ENTITY] как упоминалось ранее: например, при условии, что мы хотим tooimplement/предоставляют новое разрешение с именем «Employees.Read.All» в нашем ресурсов приложения (API) необходимо просто добавить коллекции oauth2Permissions toohello элемент новый в секунду, ie:
   
        "oauth2Permissions": [
        {
        "adminConsentDescription": "Allow hello application tooaccess MyWebApplication on behalf of hello signed-in user.",
        "adminConsentDisplayName": "Access MyWebApplication",
        "id": "aade5b35-ea3e-481c-b38d-cba4c78682a0",
        "isEnabled": true,
        "type": "User",
        "userConsentDescription": "Allow hello application tooaccess MyWebApplication on your behalf.",
        "userConsentDisplayName": "Access MyWebApplication",
        "value": "user_impersonation"
        },
        {
        "adminConsentDescription": "Allow hello application toohave read-only access tooall Employee data.",
        "adminConsentDisplayName": "Read-only access tooEmployee records",
        "id": "2b351394-d7a7-4a84-841e-08a6a17e4cb8",
        "isEnabled": true,
        "type": "User",
        "userConsentDescription": "Allow hello application toohave read-only access tooyour Employee data.",
        "userConsentDisplayName": "Read-only access tooyour Employee records",
        "value": "Employees.Read.All"
        }
        ],
   
    Hello записи должно быть уникальным и поэтому необходимо создать новый глобально уникальный идентификатор (GUID) для hello `"id"` свойство. Таким образом так как указан `"type": "User"`, это разрешение может быть согласие tooby любой подлинность учетной записи hello клиента Azure AD, в какие hello зарегистрирован и API-интерфейса ресурсов приложения. Это разрешение tooaccess приложения клиента предоставляет hello его от имени учетной записи hello. Hello описание и отображаемое имя строки используются во время согласия, а также для отображения в hello портал Azure.
6. По завершении обновление манифеста hello, нажмите кнопку **Сохранить** toosave hello манифест.  
   
Теперь, когда hello манифест сохраняется, вы предоставляете зарегистрированного клиентского приложения access toohello новое разрешение, мы добавили выше. Это время можно использовать hello веб-Интерфейс портала Azure вместо редактирования манифеста приложения hello клиента:  

1. Сперва сверьтесь toohello **параметры** колонке hello toowhich приложения клиента нужно tooadd toohello новый API-Интерфейс, щелкните **требуемые разрешения** и выберите **выберите API** .
2. Затем откроется список зарегистрированных ресурсов приложения (API) в клиенте hello hello. Щелкните tooselect приложения hello ресурсов или имя типа hello поле поиска hello приложения hello. Если вы нашли приложения hello, нажмите кнопку **выберите**.  
3. Это может занять toohello **выберите разрешения** страницу, которая будет отображаться список hello разрешения для приложений и делегированные разрешения для ресурсов приложения hello. Здравствуйте, выберите новое разрешение в порядке tooadd его toohello клиенту список разрешений. Это новое разрешение будет храниться в конфигурацию удостоверения hello клиентское приложение, в свойство коллекции «requiredResourceAccess» hello.


Вот и все. Теперь ваши приложения будут запускаться с новой конфигурацией удостоверений.

## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные сведения о hello связь между объекты приложения и субъекта-службы приложения в разделе [объекты участника службы в Azure AD, приложения и][AAD-APP-OBJECTS].
* В разделе hello [глоссарий разработчика Azure AD] [ AAD-DEVELOPER-GLOSSARY] определения некоторые основные понятия для разработчиков hello основных компонентов Azure Active Directory (AD).

Используйте раздел hello комментарии ниже tooprovide отзывы и помогают уточнить и отформатировать содержимое веб-узла.

<!--article references -->
[AAD-APP-OBJECTS]: active-directory-application-objects.md
[AAD-DEVELOPER-GLOSSARY]: active-directory-dev-glossary.md
[AAD-GROUPS-FOR-AUTHORIZATION]: http://www.dushyantgill.com/blog/2014/12/10/authorization-cloud-applications-using-ad-groups/
[ADD-UPD-RMV-APP]: active-directory-integrating-applications.md
[APPLICATION-ENTITY]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[APPLICATION-ENTITY-APP-ROLE]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#approle-type
[APPLICATION-ENTITY-OAUTH2-PERMISSION]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permission-type
[AZURE-PORTAL]: https://portal.azure.com
[DEV-GUIDE-TO-AUTH-WITH-ARM]: http://www.dushyantgill.com/blog/2015/05/23/developers-guide-to-auth-with-azure-resource-manager-api/
[GRAPH-API]: active-directory-graph-api.md
[IMPLICIT-GRANT]: active-directory-dev-understanding-oauth2-implicit-grant.md
[INTEGRATING-APPLICATIONS-AAD]: https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/
[O365-PERM-DETAILS]: https://msdn.microsoft.com/office/office365/HowTo/application-manifest
[O365-SERVICE-DAEMON-APPS]: https://msdn.microsoft.com/office/office365/howto/building-service-apps-in-office-365
[RBAC-CLOUD-APPS-AZUREAD]: http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/

