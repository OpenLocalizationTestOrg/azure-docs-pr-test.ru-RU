---
title: "aaaAuthenticate с API REST для Mobile Engagement"
description: "Описывает способ tooauthenticate с API REST Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: da82cb36-957a-4e19-a805-b44733cf6597
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 10/05/2016
ms.author: wesmc;ricksal
ms.openlocfilehash: 9b54aa5ec3da4bcf55ffe5b7e8d1759095d0c486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis"></a>Аутентификация с помощью интерфейсов REST API Служб мобильного взаимодействия
## <a name="overview"></a>Обзор
В этом документе описывается, как tooget допустимым Oauth AAD токен tooauthenticate с hello API-интерфейс REST Mobile Engagement. 

Предполагается, что у вас есть действующая подписка Azure и вы создали приложение Служб мобильного взаимодействия, используя одно из наших [руководств для разработчиков](mobile-engagement-windows-store-dotnet-get-started.md).

## <a name="authentication"></a>Аутентификация
Для проверки подлинности необходимо использовать маркер OAuth на основе Microsoft Azure Active Directory. 

Запрос заказа tooauthentication API заголовок авторизации должны быть добавлены tooevery запрос, который имеет hello следующие формы:

    Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGmJlNmV2ZWJPamg2TTNXR1E...

> [!NOTE]
> Срок действия токенов Azure Active Directory — 1 час.
> 
> 

Существует несколько способов tooget маркер. С момента hello API-интерфейсы обычно вызываются из облачной службы требуется toouse ключ API. Ключ API в Azure — это пароль субъекта-службы. Hello следующая процедура описывает один из способов toosetting его настройка вручную.

### <a name="one-time-setup-using-script"></a>Однократная настройка (с использованием сценария)
Необходимо следовать hello набор инструкций ниже tooperform hello установки с помощью сценария PowerShell, который принимает hello минимальное время для программы установки, но использует hello наиболее допустимые значения по умолчанию. При необходимости можно также выполнить hello инструкциям hello [ручная установка](mobile-engagement-api-authentication-manual.md) для этого hello непосредственно портал Azure и настройку точно. 

1. Получить последнюю версию Azure PowerShell из hello [здесь](http://aka.ms/webpi-azps). Дополнительные сведения о инструкции по загрузке hello вы увидите это [ссылку](/powershell/azure/overview).  
2. После установки Azure PowerShell, используйте hello следующими командами наличие hello tooensure **модуль Azure** установлены:
   
    а. Убедитесь, что hello модуля Azure PowerShell доступна в список доступных модулей hello. 
   
        Get-Module –ListAvailable 
   
    ![Доступные модули Azure][1]
   
    b. Если не удается найти модуль Azure PowerShell hello в hello над списком необходимо toorun hello следующее:
   
        Import-Module Azure 
3. Здравствуйте, toohello входа диспетчера ресурсов Azure из PowerShell, выполнив следующую команду и имя пользователя и пароль для учетной записи Azure: 
   
        Login-AzureRmAccount
4. Если у вас несколько подписок необходимо запускать следующую hello.
   
    а. Получение списка всех подписок и копирования hello SubscriptionId hello подписки, которые нужно toouse. Убедитесь, что эта подписка hello того же, имеющая hello Mobile Engagement приложения, которое будет toointeract с помощью hello API-интерфейсы. 
   
        Get-AzureRmSubscription
   
    b. Выполнения hello следующая команда обеспечивает hello SubscriptionId tooconfigure hello подписки toobe используется.
   
        Select-AzureRmSubscription –SubscriptionId <subscriptionId>
5. Скопируйте текст hello для hello [New AzureRmServicePrincipalOwner.ps1](https://raw.githubusercontent.com/matt-gibbs/azbits/master/src/New-AzureRmServicePrincipalOwner.ps1) сценариев tooyour локального компьютера и сохранить его как командлет PowerShell (например `APIAuth.ps1`) и выполните его `.\APIAuth.ps1`. 
6. Hello скрипт запросит tooprovide во входных данных для **principalName**. Укажите подходящее имя должно toouse toocreate приложение Active Directory (например APIAuth). 
7. После завершения скрипта hello, будут показаны следующие четыре значения, которые потребуются hello tooauthenticate программными средствами с помощью AD, поэтому следует убедиться, что toocopy их. 
   
    **TenantId**, **SubscriptionId**, **ApplicationId** и **Secret**.
   
    Вы будете использовать TenantId в качестве `{TENANT_ID}`, ApplicationId — в качестве `{CLIENT_ID}`, а секрет — в качестве `{CLIENT_SECRET}`.
   
   > [!NOTE]
   > Политика безопасности по умолчанию может блокировать выполнение сценариев PowerShell. В этом случае временно настройте выполнение сценария выполнения политики tooallow с помощью hello следующую команду:
   > 
   > Set-ExecutionPolicy RemoteSigned
   > 
   > 
8. Ниже показано, как hello набор командлетов PS выглядит следующим образом. 
   
    ![][3]
9. Проверьте на портале управления Azure hello новое приложение AD создания с именем hello при условии вызов сценария toohello **principalName** под **Показать приложений, которыми владеет Моя компания**.
   
    ![][4]

#### <a name="steps-tooget-a-valid-token"></a>Действия tooget допустимый токен
1. Вызвать hello API с hello следующие параметры и убедитесь, что tooreplace hello КЛИЕНТА\_идентификатор, клиент\_идентификатор и клиент\_СЕКРЕТ:
   
   * **URL-адрес запроса** — в формате *https://login.microsoftonline.com/{TENANT\_ID}/oauth2/token*
   * **Заголовок Content-Type HTTP** как *application/x-www-form-urlencoded*
   * **Текст запроса HTTP** — в формате *grant\_type=client\_credentials&client_id={CLIENT\_ID}&client_secret={CLIENT\_SECRET}&resource=https%3A%2F%2Fmanagement.core.windows.net%2F*
     
     Hello ниже приведен пример запроса:
     
       POST /{TENANT_ID}/oauth2/token HTTP/1.1   Host: login.microsoftonline.com   Content-Type: application/x-www-form-urlencoded   grant_type=client_credentials&client_id={CLIENT_ID}&client_secret={CLIENT_SECRET}&reso   urce=https%3A%2F%2Fmanagement.core.windows.net%2F
     
     Вот пример ответа на запрос:
     
       HTTP/1.1 200 OK   Content-Type: application/json; charset=utf-8   Content-Length: 1234
     
       {"token_type":"Bearer","expires_in":"3599","expires_on":"1445395811","not_before":"144   5391911","resource":"https://management.core.windows.net/","access_token":{ACCESS_TOKEN}}
     
     В этом примере включены, параметры отправки hello, кодирование URL-адресов `resource` значение имеет `https://management.core.windows.net/`. Будьте внимательны, кодирование URL-адрес tooalso `{CLIENT_SECRET}` как она может содержать специальные символы.
     
     > [!NOTE]
     > Для тестирования можно использовать средство клиента HTTP, такое как [Fiddler](http://www.telerik.com/fiddler) или [расширение Chrome Postman](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop). 
     > 
     > 
2. Теперь в все вызовы API, включите заголовок запроса авторизации hello.
   
        Authorization: Bearer {ACCESS_TOKEN}
   
    Если получить код состояния 401 возвращается, текст ответа для проверки hello, его может подсказать, истек токен hello. В этом случае следует получить новый маркер.

## <a name="using-hello-apis"></a>С помощью API-интерфейсы hello
Теперь, у вас есть действительный токен, все вызовы hello API toomake готовности.

1. В каждом запросе API необходимо toopass допустимый, неистекшим сроком действия маркера, который вы получили в предыдущем разделе hello.
2. Вам потребуется tooplug некоторыми параметрами в hello запрос URI, который идентифицирует приложение. Hello URI запроса выглядит как следующий hello
   
        https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/
        providers/Microsoft.MobileEngagement/appcollections/{app-collection}/apps/{app-resource-name}/
   
    Параметры tooget hello, щелкните имя приложения и выберите команду панели мониторинга и как следующие hello со всеми тремя параметрами Здравствуйте, откроется страница.
   
   * **1** `{subscription-id}`
   * **2** `{app-collection}`
   * **3** `{app-resource-name}`
   * **4** имя вашей группы ресурсов будет toobe **MobileEngagement** Если не был создан новый. 
     
     ![Параметры URI API Служб мобильного взаимодействия][2]

> [!NOTE]
> <br/>
> 
> 1. Не обращайте внимания hello корневой адрес API, как это было для hello предыдущих API-интерфейсы.<br/>
> 2. Если вы создали приложение hello, с помощью портала Azure Classic требуется toouse hello ресурса приложения имя, отличных от само имя приложения hello. Если вы создали приложение hello в hello портал Azure следует использовать hello само (нет никакой разницы между имени ресурсов приложения и приложения для приложений, созданных на новом портале hello) имя приложения.  
> 
> 

<!-- Images -->
[1]: ./media/mobile-engagement-api-authentication/azure-module.png
[2]: ./media/mobile-engagement-api-authentication/mobile-engagement-api-uri-params.png
[3]: ./media/mobile-engagement-api-authentication/ps-cmdlets.png
[4]: ./media/mobile-engagement-api-authentication/ad-app-creation.png



