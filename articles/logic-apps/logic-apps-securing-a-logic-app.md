---
title: "aaaSecure доступа к приложениям логику tooAzure | Документы Microsoft"
description: "Добавьте безопасности для защиты tootriggers доступ, входов и выходов, параметров действия и службы, используемые с рабочими процессами в логике приложения Azure."
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 9fab1050-cfbc-4a8b-b1b3-5531bee92856
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 11/22/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: abda2179e4cc2d2295cd8332ec017c848a456264
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="secure-access-tooyour-logic-apps"></a>Защита доступа к tooyour логику приложения

Существует много доступных toohelp средств защиты логику приложения.

* Обеспечение безопасности доступа tootrigger логику приложения (триггер запрос HTTP)
* Защита доступа к toomanage, изменение или чтение приложения логики
* Обеспечение безопасности доступа toocontents входов и выходов для запуска
* Обеспечение безопасности параметров или входных данных в рамках действий в рабочем процессе.
* Защита доступа к tooservices, получать запросы из рабочего процесса

## <a name="secure-access-tootrigger"></a>Tootrigger безопасный доступ

При работе с логики приложения, вызывающего событие HTTP-запроса ([запроса](../connectors/connectors-native-reqres.md) или [веб-перехватчика](../connectors/connectors-native-webhook.md)), вы можете ограничить доступ, чтобы только авторизованные клиенты могут запускать приложение hello логику. Все запросы к приложению логики зашифрованы и защищены с помощью SSL.

### <a name="shared-access-signature"></a>Подписанный URL-адрес

Включает каждой конечной точки запроса для приложения логики [подписи общего доступа (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md) как часть URL-адрес hello. Каждый URL-адрес содержит параметр запроса `sp`, `sv` и `sig`. Разрешения задаются `sp`, и соответствующие методы tooHTTP может быть, `sv` — toogenerate версия, используемая hello, и `sig` является tootrigger используется tooauthenticate доступа. Сигнатура Hello создается с помощью алгоритма hello SHA256 с открытым ключом для всех путей hello URL-адрес и свойства. Hello секретный ключ никогда не предоставляется и не опубликован, а хранятся зашифрованные и хранимые как часть логики приложения hello. Логика приложения авторизует только триггеры, содержащие действительной подписи, созданных с помощью hello секретный ключ.

#### <a name="regenerate-access-keys"></a>Повторное создание ключей доступа

Можно повторно создать новый ключ безопасного в любое время через портал hello API-интерфейса REST или Azure. Все текущие URL-адреса, созданные ранее с помощью старого ключа hello являются недействительными и больше не авторизованным toofire hello логику приложения.

1. В hello портал Azure откройте приложение hello логику, нужно tooregenerate ключ
1. Нажмите кнопку hello **клавиши доступа** пункт **параметры**
1. Выберите процесс завершения hello и ключа tooregenerate hello

URL-адреса, получаемых после повторного создания должны быть подписаны hello новый ключ доступа.

#### <a name="creating-callback-urls-with-an-expiration-date"></a>Создание URL-адреса обратного вызова с истекшим сроком действия

Если URL-адрес hello совместно с другими участниками, можно создать URL-адреса с конкретным разделам и даты окончания срока действия при необходимости. Можно затем легко развертывания ключей или обеспечения доступа toofire приложение имеет ограниченные tooa определенных timespan. Можно указать дату окончания срока действия для URL-адреса через hello [логику приложения REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers):

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

В тексте hello включить свойство hello `NotAfter` как строку даты в JSON, который возвращает URL-адрес обратного вызова, действительна только до hello `NotAfter` даты и времени.

#### <a name="creating-urls-with-primary-or-secondary-secret-key"></a>Создание URL-адресов с использованием первичного или вторичного секретного ключа

После создания или список URL-адресов обратного вызова для триггеров на основе запросов, можно также указать какой URL-адрес ключа toouse toosign hello.  Можно создать URL-адрес, подписанный указанным ключом через hello [логику приложения REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers) следующим образом:

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

В тексте hello включить свойство hello `KeyType` либо как `Primary` или `Secondary`.  Возвращает подписанный hello безопасного ключ, указанный URL-адрес.

### <a name="restrict-incoming-ip-addresses"></a>Ограничение входящих IP-адресов

В дополнение к этому toohello подпись общего доступа, вы можете toorestrict вызов приложения логики только из конкретных клиентов.  Например, при управлении конечной точки через API управления Azure, можно ограничить hello логику приложения tooonly принять hello при запросе hello из hello IP-адрес экземпляра управления API.

Этот параметр можно настроить в параметрах приложения hello логику:

1. В hello портал Azure откройте приложение hello логику, нужно tooadd ограничения IP-адресов
1. Нажмите кнопку hello **конфигурации контроля доступа** пункт **параметры**
1. Укажите список hello toobe диапазоны адресов IP, принимаемое hello триггера

Допустимый диапазон IP имеет формат hello `192.168.1.1/255`. Пожара tooonly hello логику приложения как вложенные логики приложения, установите hello **только в другие приложения логики** параметр. Этот параметр записывает ресурс toohello пустой массив, это означает, что только вызовы из hello самой службой fire (родительского логики приложения) успешно.

> [!NOTE]
> Можно запустить приложение логики с триггером запроса через API-Интерфейс REST hello и управления `/triggers/{triggerName}/run` независимо от IP. Данный сценарий требует проверки подлинности hello Azure REST API, и все события будут отображаться в hello журналов аудита Azure. Настройте политики контроля доступа соответствующим образом.

#### <a name="setting-ip-ranges-on-hello-resource-definition"></a>Задание диапазонов IP-адресов для определения ресурса hello

Если вы используете [шаблон развертывания](logic-apps-create-deploy-template.md) tooautomate развертываниям параметры диапазона hello IP-адреса можно настроить на шаблон ресурсов hello.  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "triggers": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}

```

### <a name="adding-azure-active-directory-oauth-or-other-security"></a>Добавление Azure Active Directory, OAuth или других механизмов безопасности

Дополнительные авторизации протоколов поверх приложения логики, tooadd [управления API Azure](https://azure.microsoft.com/services/api-management/) предлагает широкие возможности мониторинга, безопасности, политики и документации для любой конечной точки с возможностью tooexpose hello приложения логики как интерфейс API. Управления API Azure можно предоставлять конечную точку открытые или закрытые приложение hello логики, которую может использовать Azure Active Directory, сертификат, OAuth или других стандартов безопасности. При получении запроса API управления Azure пересылает hello запроса toohello логику приложения (выполняются все необходимые преобразования или ограничения на лету). Можно использовать hello входящих диапазон IP-адресов параметры на hello логику приложения tooonly разрешить hello логику приложения toobe запускается из API-интерфейса управления.

## <a name="secure-access-toomanage-or-edit-logic-apps"></a>Защита доступа к toomanage или изменить логику приложений

Вы можете ограничить операции доступа к toomanagement для логики приложения таким образом, может tooperform операции с ресурсом hello только определенным пользователям или группам. Логика приложения используют hello Azure [управление доступом на основе ролей (RBAC)](../active-directory/role-based-access-control-configure.md) компонентов и могут настраиваться с помощью hello тех же средств.  Существует несколько встроенных ролей, которые также можно назначать члены tooas вашей подписки:

* **Логика приложения участника** -предоставляет доступ tooview, изменение и обновление приложения логики.  Невозможно удалить ресурс hello или выполнять операции администрирования.
* **Оператор логику приложения** — можно просматривать приложения логики hello и журнал выполнения и включить или отключить.  Не удается изменить или обновить определение hello.

Можно также использовать [блокировка ресурса Azure](../azure-resource-manager/resource-group-lock-resources.md) tooprevent изменением или удалением приложения логики. Эта возможность является ценным tooprevent производственных ресурсов от изменения или удаления.

## <a name="secure-access-toocontents-of-hello-run-history"></a>Toocontents безопасный доступ из hello, журнал выполнения

Вы можете ограничить доступ toocontents входов или выходов из предыдущих запусков toospecific IP-адресов.  

Все данные в рамках выполнения рабочего процесса шифруются при передаче и хранении. При внесении toorun журнал вызовов, hello служба проверяет подлинность запроса hello и предоставляет ссылки toohello запроса ответа входов и выходов. Эта ссылка может указывать на защищенном поэтому только запросы, tooview содержимое из указанного диапазона IP-адресов возврата hello содержимого. Эту возможность можно использовать в качестве дополнительного метода контроля доступа. Можно также указать IP-адрес в виде `0.0.0.0`, тогда никто не сможет получить доступ к входным и выходным данным. Только пользователь с правами администратора удалось удалить это ограничение, предоставляя возможность hello содержимое tooworkflow доступа «just-in-time».

Этот параметр можно настроить в параметров ресурсов hello hello портала Azure:

1. В hello портал Azure откройте приложение hello логику, нужно tooadd ограничения IP-адресов
1. Нажмите кнопку hello **конфигурации контроля доступа** пункт **параметры**
1. Укажите список диапазонов IP-адресов для доступа к toocontent hello

#### <a name="setting-ip-ranges-on-hello-resource-definition"></a>Задание диапазонов IP-адресов для определения ресурса hello

Если вы используете [шаблон развертывания](logic-apps-create-deploy-template.md) tooautomate развертываниям параметры диапазона hello IP-адреса можно настроить на шаблон ресурсов hello.  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "contents": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}
```

## <a name="secure-parameters-and-inputs-within-a-workflow"></a>Параметры безопасности и входные данные в рабочем процессе

Может потребоваться tooparameterize некоторые аспекты определение рабочего процесса для развертывания в средах. Кроме того, некоторые параметры могут быть безопасные параметры, необходимо исключить tooappear при изменении рабочего процесса, такие как идентификатор клиента и секрет клиента для [проверки подлинности Azure Active Directory](../connectors/connectors-native-http.md#authentication) действия HTTP.

### <a name="using-parameters-and-secure-parameters"></a>Использование параметров и параметров безопасности

tooaccess hello значение параметра ресурсов во время выполнения, hello [язык определения рабочих процессов](http://aka.ms/logicappsdocs) предоставляет `@parameters()` операции. Кроме того, вы можете [укажите параметры в шаблон развертывания ресурсов hello](../azure-resource-manager/resource-group-authoring-templates.md#parameters). Однако если указан тип параметра hello `securestring`, параметр hello не будет возвращен с rest hello hello определения ресурса и не будет доступен, просмотрев hello ресурса после развертывания.

> [!NOTE]
> Если параметра используется в заголовках hello или основной текст запроса, hello параметра может быть видимой осуществлять доступ к истории выполнения hello и исходящих HTTP-запроса. Убедитесь, что tooset политик доступа к содержимому соответствующим образом.
> Заголовки авторизации никогда не отображаются во входных и выходных данных. Поэтому если существует используется секрет hello, секрет hello не удается найти.

#### <a name="resource-deployment-template-with-secrets"></a>Шаблон развертывания ресурсов с использованием секретов

Hello пример развертывания, который ссылается на безопасный параметр `secret` во время выполнения. В файле отдельные параметры, можно указать значение hello среды для hello `secret`, или используйте [KeyVault диспетчера ресурсов Azure](../azure-resource-manager/resource-manager-keyvault-parameter.md) секреты tooretrieve во время развертывания.

``` json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "secretDeploymentParam": {
      "type": "securestring"
    }
  },
  "variables": {},
  "resources": [
    {
      "name": "secret-deploy",
      "type": "Microsoft.Logic/workflows",
      "location": "westus",
      "tags": {
        "displayName": "LogicApp"
      },
      "apiVersion": "2016-06-01",
      "properties": {
        "definition": {
          "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "actions": {
            "Call_External_API": {
              "type": "http",
              "inputs": {
                "headers": {
                  "Authorization": "@parameters('secret')"
                },
                "body": "This is hello request"
              },
              "runAfter": {}
            }
          },
          "parameters": {
            "secret": {
              "type": "SecureString"
            }
          },
          "triggers": {
            "manual": {
              "type": "Request",
              "kind": "Http",
              "inputs": {
                "schema": {}
              }
            }
          },
          "contentVersion": "1.0.0.0",
          "outputs": {}
        },
        "parameters": {
          "secret": {
            "value": "[parameters('secretDeploymentParam')]"
          }
        }
      }
    }
  ],
  "outputs": {}
}
```

## <a name="secure-access-tooservices-receiving-requests-from-a-workflow"></a>Защита доступа к tooservices получения запросов из рабочего процесса

Много способов toohelp являются безопасными по любой конечной точки hello логику приложению tooaccess.

### <a name="using-authentication-on-outbound-requests"></a>Использование проверки подлинности при исходящих запросах

При работе с HTTP, HTTP + Swagger (открытых API) или веб-перехватчика действие, можно добавить отправляемого запроса toohello проверки подлинности. Это может быть обычная аутентификация, аутентификация на основе сертификата или аутентификация Azure Active Directory. Сведения о том, как tooconfigure этой проверки подлинности можно найти [в этой статье](../connectors/connectors-native-http.md#authentication).

### <a name="restricting-access-toologic-app-ip-addresses"></a>Ограничения IP-адресов доступа toologic приложения

Все вызовы из приложений логики поступают из определенного набора IP-адресов для каждого региона. Можно добавить дополнительную фильтрацию tooonly прием запросов по сравнению с указанных IP-адресов. Список этих IP-адресов можно найти в статье [Ограничения и настройка приложений логики](logic-apps-limits-and-config.md#configuration).

### <a name="on-premises-connectivity"></a>Локальные возможности подключения

Приложения логики обеспечивают интеграцию с несколькими tooprovide служб, безопасную и надежную локальной связи.

#### <a name="on-premises-data-gateway"></a>Локальный шлюз данных

Многие управляемых соединители для логики приложений обеспечивают безопасное подключение между tooon локальной системы, включая файловой системы, SQL, SharePoint, DB2 и многое другое. шлюз Hello передает данные из локальных источников шифрованные каналы через hello Azure Service Bus. Весь трафик поступает как безопасный исходящий трафик от агента hello шлюза. Дополнительные сведения о [как работает шлюз данных hello](logic-apps-gateway-install.md#gateway-cloud-service).

#### <a name="azure-api-management"></a>Cлужба управления Azure API 

[Управления API Azure](https://azure.microsoft.com/services/api-management/) имеет возможности подключения в локальной среде, включая интеграцию сеть сеть VPN и ExpressRoute для защищенных систем tooon локальный прокси-сервера и обмена данными. В hello конструктор логики приложения можно быстро выбрать интерфейс API, предоставляемых API управления Azure в рамках рабочего процесса, предоставляют быстрый доступ tooon локальные системы.

#### <a name="hybrid-connections-from-azure-app-service"></a>Гибридные подключения из службы приложений Azure

Hello локальной гибридного подключения можно использовать для Azure API и веб-приложений toocommunicate локальной.  Сведения о гибридных подключений и обнаружение tooconfigure [в этой статье](../app-service-web/web-sites-hybrid-connection-get-started.md).

## <a name="next-steps"></a>Дальнейшие действия
[Создание шаблона развертывания приложения логики](logic-apps-create-deploy-template.md)  
[Обработка исключений](logic-apps-exception-handling.md)  
[См. статью Мониторинг приложений логики.](logic-apps-monitor-your-logic-apps.md)  
[Диагностика сбоев приложений логики](logic-apps-diagnosing-failures.md)  
