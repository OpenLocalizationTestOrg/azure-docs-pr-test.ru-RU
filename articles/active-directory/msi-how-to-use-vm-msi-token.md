---
title: "Использование управляемого удостоверения службы виртуальной машины Azure для получения маркеров доступа"
description: "Пошаговые инструкции и примеры использования MSI виртуальной машины Azure для получения маркера доступа OAuth."
services: active-directory
documentationcenter: 
author: bryanla
manager: mtillman
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/01/2017
ms.author: bryanla
ms.openlocfilehash: 6a02b52e7103c9b6e60b09617026fbf6010e76c8
ms.sourcegitcommit: 48fce90a4ec357d2fb89183141610789003993d2
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/12/2018
---
# <a name="how-to-use-an-azure-vm-managed-service-identity-msi-for-token-acquisition"></a>Использование управляемого удостоверения службы (MSI) виртуальной машины Azure для получения маркера 

[!INCLUDE[preview-notice](../../includes/active-directory-msi-preview-notice.md)]  
Эта статья содержит различные примеры кода и скриптов для получения маркера, а также инструкции по обработке ситуаций с просроченным маркером и устранению ошибок HTTP.

## <a name="prerequisites"></a>Необходимые компоненты

[!INCLUDE [msi-qs-configure-prereqs](../../includes/active-directory-msi-qs-configure-prereqs.md)]

Если вы планируете использовать примеры Azure PowerShell в этой статье, убедитесь, что установлена последняя версия [Azure PowerShell](https://www.powershellgallery.com/packages/AzureRM).


> [!IMPORTANT]
> - Во всех примерах кода или скриптов в этой статье предполагается, что клиент выполняется на виртуальной машине с поддержкой MSI. Используйте функцию подключения виртуальной машины на портале Azure для удаленного подключения к своей виртуальной машине. Дополнительные сведения о включении MSI на виртуальной машине см. в статье [Настройка управляемого удостоверения службы (MSI) на виртуальной машине Azure с помощью портала Azure](msi-qs-configure-portal-windows-vm.md) или в одном из вариантов статей (с использованием PowerShell, CLI, шаблона или пакета SDK для Azure). 

## <a name="overview"></a>Обзор

Клиентское приложение может запрашивать [маркер доступа к приложению](develop/active-directory-dev-glossary.md#access-token) MSI для доступа к данному ресурсу. Маркер создан на основе [субъекта-службы MSI](msi-overview.md#how-does-it-work). Таким образом клиенту не нужно регистрироваться для получения маркера доступа для собственного субъекта-службы. Маркер подходит для использования в качестве маркера носителя при [выполнении вызовов между службами, требующих учетных данных клиента](active-directory-protocols-oauth-service-to-service.md).

|  |  |
| -------------- | -------------------- |
| [Получение маркера с использованием HTTP](#get-a-token-using-http) | Сведения о протоколе для конечной точки маркера MSI |
| [Получение маркера с использованием C#](#get-a-token-using-c) | Пример использования конечной точки MSI REST от клиента C# |
| [Получение маркера с использованием Go](#get-a-token-using-go) | Пример использования конечной точки MSI REST от клиента Go |
| [Получение маркера с использованием Azure PowerShell](#get-a-token-using-azure-powershell) | Пример использования конечной точки MSI REST от клиента Azure PowerShell |
| [Получение маркера с использованием CURL](#get-a-token-using-curl) | Пример использования конечной точки MSI REST от клиента Bash/CURL |
| [Обработка срока действия маркера](#handling-token-expiration) | Рекомендации по обработке срока действия маркера доступа |
| [Обработка ошибок](#error-handling) | Рекомендации по обработке ошибок HTTP, возвращаемых из конечной точки маркера MSI |
| [Идентификаторы ресурсов для служб Azure](#resource-ids-for-azure-services) | Сведения о том, где можно получить идентификаторы ресурсов для поддерживаемых служб Azure |

## <a name="get-a-token-using-http"></a>Получение маркера с использованием HTTP 

Основной интерфейс для получения маркера доступа создан на основе REST, что делает его доступным для любого клиентского приложения, выполняющегося на виртуальной машине,которая может выполнять вызовы HTTP REST. Это похоже на модель программирования Azure AD, за исключением того, что клиент использует конечную точку localhost на виртуальной машине (а не конечную точку Azure AD).

Пример запроса:

```
GET http://localhost:50342/oauth2/token?resource=https%3A%2F%2Fmanagement.azure.com%2F HTTP/1.1
Metadata: true
```

| Элемент | ОПИСАНИЕ |
| ------- | ----------- |
| `GET` | HTTP-команда, указывающая, что необходимо извлечь данные из конечной точки. В этом случае используется маркер доступа OAuth. | 
| `http://localhost:50342/oauth2/token` | Конечная точка MSI, в которой порт 50342 является портом по умолчанию, который можно настроить. |
| `resource` | Параметр строки запроса, указывающий URI идентификатора приложения целевого ресурса. Он также отображается в утверждении (аудитории) `aud` выданного маркера. В этом примере запрашивается маркер для доступа к Azure Resource Manager, который имеет универсальный код ресурса (URI) идентификатора приложения https://management.azure.com/. |
| `Metadata` | Поле заголовка HTTP-запроса, требуемое MSI с целью устранения рисков от атак с подделкой запроса со стороны сервера (SSRF). Должно быть присвоено значение true (все в нижнем регистре).

Пример ответа:

```
HTTP/1.1 200 OK
Content-Type: application/json
{
  "access_token": "eyJ0eXAi...",
  "refresh_token": "",
  "expires_in": "3599",
  "expires_on": "1506484173",
  "not_before": "1506480273",
  "resource": "https://management.azure.com/",
  "token_type": "Bearer"
}
```

| Элемент | ОПИСАНИЕ |
| ------- | ----------- |
| `access_token` | Запрашиваемый маркер доступа. При вызове защищенного REST API маркер внедряется в поле `Authorization` заголовка запроса в качестве маркера носителя, позволяя API выполнить проверку подлинности вызывающего объекта. | 
| `refresh_token` | Не используется MSI. |
| `expires_in` | Количество секунд, в течение которых маркер доступа является действительным, прежде чем его срок действия истечет (с момента выдачи). Время выдачи можно найти в утверждении `iat` маркера. |
| `expires_on` | Период времени после истечения срока действия маркера доступа. Дата представляется как количество секунд с 1970-01-01T0:0:0Z в формате UTC (соответствует утверждению `exp` маркера). |
| `not_before` | Период времени, когда маркер доступа вступает в силу и может быть принят. Дата представляется как количество секунд с 1970-01-01T0:0:0Z в формате UTC (соответствует утверждению `nbf` маркера). |
| `resource` | Ресурс, для которого был запрошен маркер доступа, соответствует параметру строки запроса `resource`. |
| `token_type` | Тип маркера, который является маркером доступа носителя, что значит, что ресурс может предоставлять доступ носителю этого маркера. |

## <a name="get-a-token-using-c"></a>Получение маркера с использованием C#

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Net;
using System.Web.Script.Serialization; 

// Build request to acquire MSI token
HttpWebRequest request = (HttpWebRequest)WebRequest.Create("http://localhost:50342/oauth2/token?resource=https://management.azure.com/");
request.Headers["Metadata"] = "true";
request.Method = "GET";

try
{
    // Call /token endpoint
    HttpWebResponse response = (HttpWebResponse)request.GetResponse();

    // Pipe response Stream to a StreamReader, and extract access token
    StreamReader streamResponse = new StreamReader(response.GetResponseStream()); 
    string stringResponse = streamResponse.ReadToEnd();
    JavaScriptSerializer j = new JavaScriptSerializer();
    Dictionary<string, string> list = (Dictionary<string, string>) j.Deserialize(stringResponse, typeof(Dictionary<string, string>));
    string accessToken = list["access_token"];
}
catch (Exception e)
{
    string errorText = String.Format("{0} \n\n{1}", e.Message, e.InnerException != null ? e.InnerException.Message : "Acquire token failed");
}

```

## <a name="get-a-token-using-go"></a>Получение маркера с использованием Go

```
package main

import (
  "fmt"
  "io/ioutil"
  "net/http"
  "net/url"
  "encoding/json"
)

type responseJson struct {
  AccessToken string `json:"access_token"`
  RefreshToken string `json:"refresh_token"`
  ExpiresIn string `json:"expires_in"`
  ExpiresOn string `json:"expires_on"`
  NotBefore string `json:"not_before"`
  Resource string `json:"resource"`
  TokenType string `json:"token_type"`
}

func main() {
    
    // Create HTTP request for MSI token to access Azure Resource Manager
    var msi_endpoint *url.URL
    msi_endpoint, err := url.Parse("http://localhost:50342/oauth2/token")
    if err != nil {
      fmt.Println("Error creating URL: ", err)
      return 
    }
    msi_parameters := url.Values{}
    msi_parameters.Add("resource", "https://management.azure.com/")
    msi_endpoint.RawQuery = msi_parameters.Encode()
    req, err := http.NewRequest("GET", msi_endpoint.String(), nil)
    if err != nil {
      fmt.Println("Error creating HTTP request: ", err)
      return 
    }
    req.Header.Add("Metadata", "true")

    // Call MSI /token endpoint
    client := &http.Client{}
    resp, err := client.Do(req) 
    if err != nil{
      fmt.Println("Error calling token endpoint: ", err)
      return
    }

    // Pull out response body
    responseBytes,err := ioutil.ReadAll(resp.Body)
    defer resp.Body.Close()
    if err != nil {
      fmt.Println("Error reading response body : ", err)
      return
    }

    // Unmarshall response body into struct
    var r responseJson
    err = json.Unmarshal(responseBytes, &r)
    if err != nil {
      fmt.Println("Error unmarshalling the response:", err)
      return
    }

    // Print HTTP response and marshalled response body elements to console
    fmt.Println("Response status:", resp.Status)
    fmt.Println("access_token: ", r.AccessToken)
    fmt.Println("refresh_token: ", r.RefreshToken)
    fmt.Println("expires_in: ", r.ExpiresIn)
    fmt.Println("expires_on: ", r.ExpiresOn)
    fmt.Println("not_before: ", r.NotBefore)
    fmt.Println("resource: ", r.Resource)
    fmt.Println("token_type: ", r.TokenType)
}
```

## <a name="get-a-token-using-azure-powershell"></a>Получение маркера с использованием Azure PowerShell

В следующем примере демонстрируется использование конечной точки MSI REST от клиента PowerShell для выполнения таких задач:

1. Получение маркера доступа.
2. Использование маркера доступа для вызова REST API Azure Resource Manager и получения информации о виртуальной машине. Не забудьте указать свой идентификатор подписки, имя группы ресурсов и имя виртуальной машины для `<SUBSCRIPTION-ID>`, `<RESOURCE-GROUP>` и `<VM-NAME>` соответственно.

```azurepowershell
# Get an access token for the MSI
$response = Invoke-WebRequest -Uri http://localhost:50342/oauth2/token `
                              -Method GET -Body @{resource="https://management.azure.com/"} -Headers @{Metadata="true"}
$content =$response.Content | ConvertFrom-Json
$access_token = $content.access_token
echo "The MSI access token is $access_token"

# Use the access token to get resource information for the VM
$vmInfoRest = (Invoke-WebRequest -Uri https://management.azure.com/subscriptions/<SUBSCRIPTION-ID>/resourceGroups/<RESOURCE-GROUP>/providers/Microsoft.Compute/virtualMachines/<VM-NAME>?api-version=2017-12-01 -Method GET -ContentType "application/json" -Headers @{ Authorization ="Bearer $access_token"}).content
echo "JSON returned from call to get VM info:"
echo $vmInfoRest

```

## <a name="get-a-token-using-curl"></a>Получение маркера с использованием CURL

```bash
response=$(curl http://localhost:50342/oauth2/token --data "resource=https://management.azure.com/" -H Metadata:true -s)
access_token=$(echo $response | python -c 'import sys, json; print (json.load(sys.stdin)["access_token"])')
echo The MSI access token is $access_token
```

## <a name="handling-token-expiration"></a>Обработка срока действия маркера

Локальная подсистема MSI кэширует маркеры. Таким образом их можно вызывать столько, сколько нужно, а сетевой вызов Azure AD выполняется, только если:
- произошел промах кэша из-за отсутствия маркера в кэше;
- истек срок действия маркера.

Если маркер кэшируется в коде, необходимо подготовиться к обработке сценариев, в которых ресурс указывает, что срок действия маркера истек.

## <a name="error-handling"></a>Обработка ошибок 

Конечная точка MSI сообщает об ошибках в поле кода состояния заголовка ответного сообщения HTTP в виде ошибок 4xx или 5xx:

| Код состояния | Причина ошибки | Способ устранения |
| ----------- | ------------ | ------------- |
| Ошибка 4xx в запросе. | Один или несколько параметров запроса неверные. | Не выполняйте повторную попытку.  Для получения дополнительной информации просмотрите сведения об ошибке.  Ошибки 4xx — это ошибки времени разработки.|
| Временная ошибка 5xx службы. | Подсистема MSI или Azure Active Directory вернули временную ошибку. | По прошествии 1 секунды можно безопасно повторить попытку.  Если повторные попытки будут выполняться слишком быстро или слишком часто, Azure AD может возвратить ошибку ограничения частоты (429).|

Если возникает ошибка, в соответствующем тексте ответа HTTP содержится код JSON с подробностями об ошибке:

| Элемент | ОПИСАНИЕ |
| ------- | ----------- |
| error   | Идентификатор ошибки. |
| error_description | Подробное описание ошибки. **Описания ошибки могут в любое время измениться. Не записывайте код, который создает ветвь на основе значений в описании ошибки.**|

### <a name="http-response-reference"></a>Ссылка ответа HTTP

В этом разделе описываются возможные сообщения об ошибках. Состояние "200 ОК" — это успешный ответ, а маркер доступа содержится в коде JSON текста ответа в элементе access_token.

| Код состояния | Ошибка | Описание ошибки | Решение |
| ----------- | ----- | ----------------- | -------- |
| 400 — недопустимый запрос | invalid_resource | AADSTS50001: приложение с именем *\<URI\>* не найдено в клиенте с именем *\<TENANT-ID\>*. Это может произойти, если приложение установил не администратор клиента или если пользователь в клиенте не предоставил к нему разрешение. Возможно, вы отправили запрос на проверку подлинности не тому клиенту. | (только для Linux) |
| 400 — недопустимый запрос | bad_request_102 | Необходимый заголовок метаданных не указан | Поле заголовка запроса `Metadata` отсутствует или имеет неправильный формат. Должно быть указано значение `true` в нижнем регистре. В качестве примера см. "Пример запроса" в [предыдущем разделе для REST](#rest).|
| 401 — недостаточно прав | unknown_source | Неизвестный *\<URI\>* источника | Убедитесь, что универсальный код ресурса (URI) запроса HTTP GET имеет правильный формат. Часть `scheme:host/resource-path` должна быть указана как `http://localhost:50342/oauth2/token`. В качестве примера см. "Пример запроса" в [предыдущем разделе для REST](#rest).|
|           | invalid_request | В запросе отсутствует требуемый параметр, он включает недопустимое значение параметра, параметр указан несколько раз или как-то искажен. |  |
|           | unauthorized_client | Клиент не авторизован для запроса маркера доступа с помощью этого метода. | Ошибка возникла из-за запроса, который не использовал локальное замыкание на себя для вызова расширения, или из-за того, что на виртуальной машине неправильно настроен MSI. Если вам нужна помощь при конфигурации виртуальной машины, см. статью [Настройка управляемого удостоверения службы (MSI) на виртуальной машине Azure с помощью портала Azure](msi-qs-configure-portal-windows-vm.md). |
|           | access_denied | Владелец ресурса или сервер авторизации отклонил запрос. |  |
|           | unsupported_response_type | Сервер авторизации не поддерживает получение маркера доступа с помощью этого метода. |  |
|           | invalid_scope | Запрошенная область недопустима, неизвестна или неверна. |  |
| 500 — внутренняя ошибка сервера | неизвестно | Не удалось извлечь маркер из Active Directory. Дополнительные сведения см. в журналах в *\<путь к файлу\>*. | Убедитесь, что MSI включен на виртуальной машине. Если вам нужна помощь при конфигурации виртуальной машины, см. статью [Настройка управляемого удостоверения службы (MSI) на виртуальной машине Azure с помощью портала Azure](msi-qs-configure-portal-windows-vm.md).<br><br>Кроме того, убедитесь, что универсальный код ресурса (URI) запроса HTTP GET отформатирован правильно, в частности универсальный код ресурса (URI), указанный в строке запроса. В качестве примера см. "Пример запроса" в [предыдущем разделе для REST](#rest) или раздел [Службы Azure, поддерживающие аутентификацию Azure AD](msi-overview.md#azure-services-that-support-azure-ad-authentication) для получения списка служб и соответствующих идентификаторов ресурсов.

## <a name="resource-ids-for-azure-services"></a>Идентификаторы ресурсов для служб Azure

Список ресурсов, которые поддерживают Azure AD и были протестированы с MSI и соответствующими идентификаторами ресурсов, см. в разделе [Службы Azure, поддерживающие аутентификацию Azure AD](msi-overview.md#azure-services-that-support-azure-ad-authentication).


## <a name="related-content"></a>Связанная информация

- О том, как включить MSI для виртуальной машины Azure, можно узнать в статье [Настройка управляемого удостоверения службы (MSI) на виртуальной машине Azure с помощью портала Azure](msi-qs-configure-portal-windows-vm.md).

Оставляйте свои замечания и пожелания в разделе ниже. Они помогают нам улучшать содержимое веб-сайта.








