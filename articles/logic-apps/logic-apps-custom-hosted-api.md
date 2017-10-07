---
title: "Вызовите aaaDeploy и пройти проверку подлинности веб-API и REST API для приложения логики Azure | Документы Microsoft"
description: "Развертывание, проверка подлинности и вызов веб-интерфейсов API и интерфейсов REST API в рабочих процессах для интеграции системы с приложениями логики Azure"
keywords: "веб-интерфейсы API, интерфейсы REST API, соединители, рабочие процессы, интеграция системы, проверка подлинности"
services: logic-apps
author: stepsic-microsoft-com
manager: anneta
editor: 
documentationcenter: 
ms.assetid: f113005d-0ba6-496b-8230-c1eadbd6dbb9
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: LADocs; stepsic
ms.openlocfilehash: ca1e4f28196b21f43b7c9ab94029684121e36f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-call-and-authenticate-custom-apis-as-connectors-for-logic-apps"></a>Развертывание, вызов и проверка подлинности пользовательских API в качестве соединителей для приложений логики

По окончании [создавать пользовательские API](./logic-apps-create-api-app.md) , обеспечивающие toouse действий или триггеров в логике приложения рабочих процессов, необходимо развернуть собственные интерфейсы API, прежде чем их можно вызывать. И хотя API-Интерфейс любых можно вызывать из приложения логики, для получения наилучших результатов hello, добавьте [метаданных Swagger](http://swagger.io/specification/) , описывающий операции и параметры вашего API. Этот файл Swagger позволяет улучшить работу API и упростить его интеграцию с приложениями логики.

Интерфейсы API, как можно развернуть [веб-приложений](../app-service-web/app-service-web-overview.md), но следует рассмотреть возможность развертывания интерфейсы API, как [приложения API](../app-service-api/app-service-api-apps-why-best-platform.md), которой может облегчить вашу работу при построении, размещения и использовать интерфейсы API в облаке hello и на локальном компьютере. Не нужно toochange любого кода в собственные интерфейсы API — просто развертывания приложения API tooan кода. Собственные интерфейсы API можно разместить на [службе приложений Azure](../app-service/app-service-value-prop-what-is.md), платформа как услуги (PaaS), предоставляющий одним из способов наиболее простым и максимально масштабируемые hello для API размещения.

tooauthenticate вызовы от логики приложения tooyour API-интерфейсы, настройкой Azure Active Directory в hello портал Azure, что избавляет tooupdate кода. Вы можете также применить обязательную проверку подлинности с помощью кода API.

## <a name="deploy-your-api-as-a-web-app-or-api-app"></a>Развертывание API в качестве веб-приложения или приложения API

Перед вызовом настраиваемого API из логики приложения, разверните API как веб-приложения или tooAzure приложение API службы приложений. Кроме того, toomake Swagger документ для чтения в hello конструктор логики приложения, задайте свойства определения hello API и включите [ресурсов независимо от источника (CORS) для управления доступом](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) для веб-приложения или приложения API.

1. В hello портал Azure выберите веб-приложения или приложения API.

2. В колонке hello, которое открывается в разделе **API**, выберите **определения API**. Набор hello **расположение определения API** toohello URL-адрес для файла swagger.json.

   Как правило hello URL-адрес отображается в следующем формате:`https://{name}.azurewebsites.net/swagger/docs/v1)`

   ![Файл tooSwagger ссылки для настраиваемого API](media/logic-apps-custom-hosted-api/custom-api-swagger-url.png)

3. В разделе **API** выберите **CORS**. Задать политику CORS hello для **допускается источников** слишком**"*"** (Разрешить все).

   Этот параметр разрешает запросы из конструктора приложений логики.

   ![Разрешать запросы из пользовательского API tooyour конструктор логику приложения](media/logic-apps-custom-hosted-api/custom-api-cors.png)

Дополнительные сведения вы найдете в следующих статьях:

* [Использование метаданных и пользовательского интерфейса API Swagger](../app-service-api/app-service-api-dotnet-get-started.md#use-swagger-api-metadata-and-ui)
* [Развертывание ASP.NET web API-интерфейсы tooAzure службы приложений](../app-service-api/app-service-api-dotnet-get-started.md)

## <a name="call-your-custom-api-from-logic-app-workflows"></a>Вызов настраиваемого API из рабочих процессов приложения логики

После настройки свойств определения hello API и CORS триггеров и действий пользовательского интерфейса API должен быть доступен для tooinclude в рабочем процессе логику приложения. 

*  tooview hello веб-сайты, Swagger URL-адресов, перейдите к веб-сайтам подписки в конструкторе логики приложения hello.

*  Доступные действия tooview и входных данных, указав документ Swagger использовать hello [HTTP + Swagger действие](../connectors/connectors-native-http-swagger.md).

*  toocall любого API, включая интерфейсы API, которые не имеют или предоставления Swagger документа, всегда можно создать запрос с hello [действия HTTP](../connectors/connectors-native-http.md).

## <a name="authenticate-calls-tooyour-custom-api"></a>Проверки подлинности вызовов tooyour настраиваемого API

Можно защитить tooyour вызывает пользовательский API следующими способами:

* [Изменения в коде](#no-code): защита API с [Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) через hello портал Azure, поэтому вы не имеют tooupdate кода или повторно API.

  > [!NOTE]
  > По умолчанию hello проверки подлинности Azure AD, включите hello портал Azure не предоставляет авторизации разного уровня. Например эта проверка подлинности блокирует вашей toojust API конкретных клиентов, tooa определенного пользователя или приложения. 

* [Обновление кода API.](#update-code). Защитите API, применив [проверку подлинности на основе сертификата](#certificate), [обычную проверку подлинности](#basic) или [проверку подлинности Azure AD](#azure-ad-code) с помощью кода.

<a name="no-code"></a>

### <a name="authenticate-calls-tooyour-api-without-changing-code"></a>Проверки подлинности вызовов API tooyour без изменения кода

Вот hello общие действия для этого метода.

1. Создайте два [удостоверения приложений Azure Active Directory (Azure AD)](../app-service-api/app-service-api-dotnet-service-principal-auth.md): одно для приложения логики, а другое — для веб-приложения или приложения API.

2. tooyour tooauthenticate вызовы API, использовать учетные данные hello (идентификатор клиента и секрет) для hello [участника-службы](../app-service-api/app-service-api-dotnet-service-principal-auth.md) , связанную с hello удостоверение приложения Azure AD для логики приложения.

3. Включите идентификаторы приложений hello в определении логики приложения.

#### <a name="part-1-create-an-azure-ad-application-identity-for-your-logic-app"></a>Часть 1. Создание удостоверения приложения Azure AD для приложения логики

Логика приложения использует этот приложения для Azure AD identity tooauthenticate от Azure AD. Имеется только tooset копирование это удостоверение один раз для вашего каталога. Например, вы можете toouse hello удостоверением для вашего приложения логики, несмотря на то, что можно создавать уникальные идентификаторы для каждого приложения логики. Можно настроить эти удостоверения в hello портал Azure [классический портал Azure](#app-identity-logic-classic), или используйте [PowerShell](#powershell).

**Создайте удостоверение приложения hello логику приложения в hello портал Azure**

1. В hello [портал Azure](https://portal.azure.com "https://portal.azure.com"), выберите **Azure Active Directory**. 

2. Убедитесь, что вы являетесь в hello же каталоге, что веб-приложения или приложения API.

   > [!TIP]
   > каталоги tooswitch выберите свой профиль и выберите другой каталог. Или выберите **Обзор** > **Переключение каталога**.

3. В меню "directory" hello под **управление**, выберите **регистрации приложения** > **Регистрация нового приложения**.

   > [!TIP]
   > По умолчанию hello приложения регистраций перечислены все регистрации приложения в каталоге. Выберите только ваши приложения регистрации, поискового Далее toohello tooview **Мои приложения**. 

   ![Создание регистрации приложения](./media/logic-apps-custom-hosted-api/new-app-registration-azure-portal.png)

4. Присвойте имя вашего удостоверения приложения, оставьте **тип приложения** значение слишком**веб-приложения и API**, укажите уникальный строку в формате домен для **URL-адрес входа**и выберите  **Создание**.

   ![Указание имени и URL-адреса входа для удостоверения приложения](./media/logic-apps-custom-hosted-api/logic-app-identity-azure-portal.png)

   удостоверения приложения Hello, созданный для логики приложения, теперь отображается в списке регистрации приложения hello.

   ![Удостоверение приложения логики](./media/logic-apps-custom-hosted-api/logic-app-identity-created.png)

5. В списке регистрации приложения hello выберите нового удостоверения приложения. Скопируйте и сохраните hello **идентификатор приложения** toouse как Здравствуйте, «идентификатор клиента» для логики приложения в часть 3.

   ![Копирование и сохранение идентификатора приложения для приложения логики](./media/logic-apps-custom-hosted-api/logic-app-application-id.png)

6. Если параметры удостоверения приложения не отображаются, щелкните **Параметры** или **Все параметры**.

7. В разделе **Доступ через API** выберите **Ключи**. В поле **Описание** введите имя для ключа. Выберите **срок действия** ключа в соответствующем поле.

   Hello ключ, который вы создаете выступает в качестве удостоверения приложения hello «секретный» или пароль для логики приложения.

   ![Создание ключа для удостоверения приложения логики](./media/logic-apps-custom-hosted-api/create-logic-app-identity-key-secret-password.png)

8. На панели инструментов hello, выберите **Сохранить**. Ключ отобразится в разделе **Значение**. 
**Убедитесь, что toocopy и сохраните ключ** для последующего использования так как ключ hello скрыта Если оставить hello ключа колонки.

   При настройке приложения логики в часть 3, укажите этот ключ как Здравствуйте, «секретный» или пароль.

   ![Копирование и сохранение ключа для дальнейшего использования](./media/logic-apps-custom-hosted-api/logic-app-copy-key-secret-password.png)

<a name="app-identity-logic-classic"></a>

**Создайте удостоверение приложения hello логику приложения в hello классический портал Azure**

1. В hello классический портал Azure, выберите [ **Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).

2. Выберите hello же каталоге, который используется для веб-приложения или приложения API.

3. На hello **приложений** выберите **добавить** hello нижней части страницы приветствия.

4. Присвойте удостоверению приложения имя и щелкните **Далее** (стрелка вправо).

5. В разделе **Свойства приложения** укажите уникальную строку в формате домена для параметров **URL-адрес для входа** и **URI кода приложения** и щелкните **Завершено** (значок флажка).

6. На hello **Настройка** вкладки, скопируйте и сохраните hello **идентификатор клиента** для вашей toouse приложения логики в часть 3.

7. В разделе **ключей**откройте hello **выберите длительность** списка. Выберите срок действия ключа.

   Hello ключ, который вы создаете выступает в качестве удостоверения приложения hello «секретный» или пароль для логики приложения.

8. Hello нижней части страницы приветствия, выберите **Сохранить**. Может потребоваться toowait через несколько секунд.

9. В разделе **ключей**, убедитесь, что toocopy и сохранить ключ hello, теперь отображается. 

   При настройке приложения логики в часть 3, укажите этот ключ как Здравствуйте, «секретный» или пароль.

Дополнительные сведения, узнайте, как слишком [Настройка имени входа Azure Active Directory toouse приложения службы приложений](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).

<a name="powershell"></a>

**Создать удостоверение приложения hello логику приложения в PowerShell**

Эту задачу можно выполнить в Azure Resource Manager с помощью PowerShell. Выполните следующие команды в PowerShell:

1. `Switch-AzureMode AzureResourceManager`

2. `Add-AzureAccount`

3. `New-AzureADApplication -DisplayName "MyLogicAppID" -HomePage "http://mydomain.tld" -IdentifierUris "http://mydomain.tld" -Password "identity-password"`

4. Убедитесь, что hello toocopy **ИД клиента** hello (идентификатор GUID для клиента Azure AD), **идентификатор приложения**и hello пароль, который использовался.

Дополнительные сведения, узнайте, как слишком [создать участника службы с ресурсами tooaccess PowerShell](../azure-resource-manager/resource-group-authenticate-service-principal.md).

#### <a name="part-2-create-an-azure-ad-application-identity-for-your-web-app-or-api-app"></a>Часть 2. Создание удостоверения приложения Azure AD для веб-приложения или приложения API

Если веб-приложения или приложения API уже развернута, можно включить проверку подлинности и создать удостоверение приложения hello в hello портал Azure. В противном случае вы можете [включить проверку подлинности при развертывании с использованием шаблона Azure Resource Manager](#authen-deploy). 

**Создайте удостоверение приложения hello и включите проверку подлинности в hello портал Azure для развернутых приложений**

1. В hello [портал Azure](https://portal.azure.com "https://portal.azure.com"), найдите и выберите веб-приложения или приложения API. 

2. В разделе **Параметры** выберите **Аутентификация или авторизация**. В разделе **Проверка подлинности службы приложений** включите проверку подлинности, нажав кнопку **Вкл.** В разделе **Поставщики проверки подлинности** щелкните **Azure Active Directory**.

   ![Включение проверки подлинности](./media/logic-apps-custom-hosted-api/custom-web-api-app-authentication.png)

3. Теперь создайте удостоверение приложения для веб-приложения или приложения API, как показано ниже. На hello **параметры Azure Active Directory** задать колонке **режим управления** слишком**Express**. Щелкните **Создать новое приложение AD**. Присвойте удостоверению приложения имя и нажмите кнопку **ОК**. 

   ![Создание удостоверения приложения для веб-приложения или приложения API](./media/logic-apps-custom-hosted-api/custom-api-application-identity.png)

4. На hello **проверки подлинности и авторизации колонке**, выберите **Сохранить**.

Теперь необходимо найти идентификатор клиента hello и идентификатор клиента для удостоверения приложения hello, связанный с веб-приложения или приложения API. Используйте эти идентификаторы в части 3. Поэтому выполните следующие действия для hello портал Azure или [классический портал Azure](#find-id-classic).

**Найти идентификатор клиента удостоверения приложения и идентификатор клиента для веб-приложения или приложения API в hello портал Azure**

1. В разделе **Поставщики проверки подлинности** щелкните **Azure Active Directory**. 

   ![Выбор элемента Azure Active Directory](./media/logic-apps-custom-hosted-api/custom-api-app-identity-client-id-tenant-id.png)

2. На hello **параметры Azure Active Directory** задать колонке **режим управления** слишком**Дополнительно**.

3. Копировать hello **идентификатор клиента**и сохраните этот идентификатор GUID для использования в часть 3.

   > [!TIP] 
   > Если **идентификатор клиента** и **URL-адрес издателя** не отображаются, попробуйте обновить hello портал Azure и повторите шаг 1.

4. В разделе **URL-адрес издателя**, скопируйте и сохраните только hello GUID для часть 3. При необходимости вы также можете использовать этот GUID в шаблоне развертывания веб-приложения или приложения API.

   Этот GUID — идентификатор определенного арендатора (ИД арендатора), который должен отображаться в следующем URL-адресе: `https://sts.windows.net/{GUID}`

5. Без сохранения изменений, закройте hello **параметры Azure Active Directory** колонку.

<a name="find-id-classic"></a>

**Найти идентификатор клиента удостоверения приложения и идентификатор клиента для веб-приложения или приложения API в hello классический портал Azure**

1. В hello классический портал Azure, выберите [ **Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).

2.  Выберите каталог hello, используемого для веб-приложения или приложения API.

3. В hello **поиска** , найдите и выберите удостоверение приложения hello для веб-приложения или приложения API.

4. На hello **Настройка** вкладка, hello копирования **идентификатор клиента**и сохраните этот идентификатор GUID для использования в часть 3.

5. После получения идентификатора клиента hello, внизу hello hello **Настройка** выберите **просмотреть конечные точки**.

6. Скопируйте URL-адрес hello **документа метаданных федерации**и найдите toothat URL-адрес.

7. В документе метаданных hello, которое открывается, найти корень hello **идентификатор EntityDescriptor** элемент, который имеет **entityID** атрибут в этой форме:`https://sts.windows.net/{GUID}` 

      Hello GUID в этот атрибут представляет идентификатор GUID конкретных клиентов (Идентификатором клиента).

8. Скопируйте идентификатор клиента hello и при необходимости сохранить этот идентификатор для использования в часть 3, а также toouse в веб-приложения или приложения API развертывания шаблона.

Дополнительные сведения см. в следующих статьях:

* [Проверка подлинности пользователя для приложений API в службе приложений Azure](../app-service-api/app-service-api-dotnet-user-principal-auth.md)
* [Проверка подлинности и авторизация в службе приложений Azure](../app-service/app-service-authentication-overview.md)

<a name="authen-deploy"></a>

**Проверка подлинности и авторизация в службе приложений Azure**

По-прежнему необходимо создать удостоверение приложения Azure AD для веб-приложения или приложения API, который отличается от удостоверения приложения hello логику приложения. удостоверение приложения hello toocreate, выполните hello предыдущих шагов во второй части hello портал Azure. Вы можно также выполните действия hello в части 1, но необходимо убедиться, что toouse вашего веб-приложения или приложения API фактического `https://{URL}` для **URL-адрес входа** и **URI идентификатора приложения**. Данные этих шагов имеется toosave клиенте hello код и код клиента для использования в шаблон развертывания приложения, а также для часть 3.

> [!NOTE]
> При создании удостоверения приложения hello Azure AD для веб-приложения или приложения API, необходимо использовать портал Azure hello или классический портал Azure, а не в PowerShell. командлет PowerShell Hello не Настройка hello необходимых разрешений toosign пользователей в веб-сайт.

После получения идентификатора клиента hello и ИД клиента включить эти идентификаторы subresource вашего веб-приложения или приложения API в шаблон развертывания.

   ```
   "resources": [
       {
           "apiVersion": "2015-08-01",
           "name": "web",
           "type": "config",
           "dependsOn": ["[concat('Microsoft.Web/sites/','parameters('webAppName'))]"],
           "properties": {
               "siteAuthEnabled": true,
               "siteAuthSettings": {
                 "clientId": "{client-ID}",
                 "issuer": "https://sts.windows.net/{tenant-ID}/",
               }
           }
       }
   ]
   ```

Развертывание tooautomatically пустой веб-приложения и приложения логики, а также проверки подлинности Azure Active Directory, [hello полный шаблон представления здесь](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json), или нажмите кнопку **развертывание tooAzure** здесь:

[![Развертывание tooAzure](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)

#### <a name="part-3-populate-hello-authorization-section-in-your-logic-app"></a>Часть 3: Заполнение hello раздела авторизации в приложении логики

Hello предыдущем шаблоне уже есть в этом разделе авторизации, настройки, но при разработке приложения hello логики напрямую, необходимо включить раздел hello полные права.

Откройте определение приложения логики в представлении кода, последовательно выберите toohello **HTTP** раздел действия, найти hello **авторизации** раздела и включить эту строку:

`{"tenant": "{tenant-ID}", "audience": "{client-ID-from-Part-2-web-app-or-API app}", "clientId": "{client-ID-from-Part-1-logic-app}", "secret": "{key-from-Part-1-logic-app}", "type": "ActiveDirectoryOAuth" }`

| Элемент | Описание |
| ------- | ----------- |
| tenant |Hello GUID для клиента hello Azure AD |
| audience |Обязательный элемент. Hello GUID для hello целевого ресурса, которые должны tooaccess - hello идентификатор клиента из удостоверения приложения hello для веб-приложения или приложения API |
| clientid |Hello GUID для клиента hello, запрашивающие доступ - hello идентификатор клиента из удостоверения приложения hello логику приложения |
| secret |Обязательный элемент. Hello ключ или пароль из удостоверения приложения hello для hello клиента, который запрашивает токен доступа hello |
| type |Тип проверки подлинности Hello. Для проверки подлинности activedirectoryoauth используется значение hello — `ActiveDirectoryOAuth`. |

Например:

```
{
   ...
   "actions": {
      "some-action": {
         "conditions": [],
         "inputs": {
            "method": "post",
            "uri": "https://your-api-azurewebsites.net/api/your-method",
            "authentication": {
               "tenant": "tenant-ID",
               "audience": "client-ID-from-azure-ad-app-for-web-app-or-api-app",
               "clientId": "client-ID-from-azure-ad-app-for-logic-app",
               "secret": "key-from-azure-ad-app-for-logic-app",
               "type": "ActiveDirectoryOAuth"
            }
         },
      }
   }
}
```

<a name="update-code"></a>

### <a name="secure-api-calls-through-code"></a>Безопасные вызовы API с помощью кода

<a name="certificate"></a>

#### <a name="certificate-authentication"></a>Проверка подлинности на основе сертификата

toovalidate hello входящие запросы от логики приложения tooyour веб-приложения или приложения API, можно использовать клиентские сертификаты. tooset код, узнайте [как взаимная проверка подлинности TLS tooconfigure](../app-service-web/app-service-web-configure-tls-mutual-auth.md).

В hello **авторизации** статьи, включите эту строку: 

`{"type": "clientcertificate", "password": "password", "pfx": "long-pfx-key"}`

| Элемент | Описание |
| ------- | ----------- |
| type |Обязательный элемент. Тип проверки подлинности Hello. Для SSL-сертификатов клиента, hello значение должно быть `ClientCertificate`. |
| пароль |Обязательный элемент. Hello пароль для доступа к hello клиентский сертификат (PFX-файла) |
| pfx |Обязательный элемент. Содержимое base64-кодированном hello клиентский сертификат (PFX-файла) |

<a name="basic"></a>

#### <a name="basic-authentication"></a>Обычная аутентификация

toovalidate входящие запросы от логики приложения tooyour веб-приложения или приложения API, можно использовать обычную проверку подлинности, такие как имя пользователя и пароль. Обычная проверка подлинности — это общий шаблон и использовании проверки подлинности в любой язык, используемый toobuild веб-приложения или приложения API.

В hello **авторизации** статьи, включите эту строку:

`{"type": "basic", "username": "username", "password": "password"}`.

| Элемент | Описание |
| --- | --- |
| type |Обязательный элемент. Тип проверки подлинности Hello. Для обычной проверки подлинности должно быть значение hello `Basic`. |
| Имя пользователя |Обязательный элемент. Hello имя пользователя для проверки подлинности |
| пароль |Обязательный элемент. Hello пароль для проверки подлинности |

<a name="azure-ad-code"></a>

#### <a name="azure-active-directory-authentication-through-code"></a>Проверка подлинности Azure Active Directory с помощью кода

По умолчанию hello проверки подлинности Azure AD, включите hello портал Azure не предоставляет авторизации разного уровня. Например эта проверка подлинности блокирует вашей toojust API конкретных клиентов, tooa определенного пользователя или приложения. 

приложения логики tooyour toorestrict API-Интерфейс доступа по коду, извлеките hello заголовок, который имеет hello веб-токен JSON (JWT). Проверьте hello удостоверение и отклонять запросы, которые не соответствуют друг другу.

Двигаемся дальше, tooimplement этой проверки подлинности полностью в собственный код и не используйте hello портал Azure, узнайте, как слишком [проверки подлинности в локальной Active Directory в приложении Azure](../app-service-web/web-sites-authentication-authorization.md).

toocreate удостоверение приложения логики приложения и использовать API, toocall удостоверений, необходимо выполнить предыдущие действия hello.

## <a name="next-steps"></a>Дальнейшие действия

* [Проверка производительности и включение ведения журналов и оповещений системы диагностики для рабочих процессов в приложениях логики](logic-apps-monitor-your-logic-apps.md)