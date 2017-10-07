---
title: "tooan операции aaaHow tooadd API в службе управления API Azure | Документы Microsoft"
description: "Узнайте, как tooan tooadd операций API в Azure API Management."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 1158a023-1913-4e9c-93de-9164b672f9b3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: d57fa59a2b0ceb392cde23150a0cbb326e52d27d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-operations-tooan-api-in-azure-api-management"></a>Как tooan tooadd операций API в Azure API Management
Прежде чем API может быть использован в API Management, должны быть добавлены операции. Это руководство показывает, как tooadd и настройки различных типов tooan операций API в службе управления API.

## <a name="add-operation"> </a>Добавление операции
Операции являются добавляется и настраивается tooan API hello портала издателя. tooaccess hello издателя, щелкните **портал издателя** в hello портала Azure для службы управления API.

![Портал издателя][api-management-management-console]

> Если вы еще не создали экземпляра службы управления API, см. раздел [создания экземпляра службы управления API] [ Create an API Management service instance] в hello [приступить к работе со службой управления API Azure] [ Get started with Azure API Management] учебника.
> 
> 

Выберите hello необходимое API в портал издателя hello и выберите hello **операции** вкладки. 

![Операции][api-management-operations]

Нажмите кнопку **добавить операцию** tooadd новую операцию. Hello **новую операцию** будут отображены и hello **подписи** вкладка будет выбран по умолчанию.

![Добавить операцию][api-management-add-operation]

Укажите hello **HTTP-команду** , выбрав из раскрывающегося списка hello.

![Метод HTTP][api-management-http-method]

<a name="url-template"></a>

Определение шаблона hello URL-адрес, введя в фрагмент URL-адреса, состоящий из одного или нескольких сегментов пути URL-адреса и ноль или более параметров строки запроса. шаблон URL-адреса Hello, добавленных toohello базовый URL-адрес hello API, определяет одну операцию HTTP. Он может содержать один или несколько частей переменной с именем, которые идентифицируются изогнутыми фигурными скобками. Эти переменные части называются параметрами шаблона и динамически присваиваются значения, извлеченные из URL-адрес запроса hello при обработке запроса hello платформой управления API hello.

> шаблон URL-адреса Hello могут включать шаблоны из подстановочных знаков. Например, при указании `/*` будет пересылать все запросы для этого HTTP метод toohello обратно остановить службы.

![Шаблон URL-адреса][api-management-url-template]

<a name="rewrite-url-template"></a>

При необходимости укажите hello **перепишите URL-адрес шаблона**. Это позволяет вам toouse hello стандартный шаблон URL-адреса для обработки входящих запросов на hello переднего плана, в ходе вызова hello внутренней через преобразованный URL-адрес в соответствии с toohello перепишите шаблона. В шаблоне перезаписи hello следует использовать параметры шаблона на основе шаблона hello URL-адрес. Hello пример типа как содержимого, закодированные как сегмент пути в веб-службу hello из предыдущего примера hello могут быть предоставлены как параметр запроса в hello API опубликованные через hello платформы управления API, с помощью шаблонов hello URL-адрес.

![Перезапись шаблона URL-адреса][api-management-url-template-rewrite]

Операция toohello вызывающим объектам будет использовать формат hello `/customers?customerid=ALFKI` , и это будет сопоставляться слишком`/Customers('ALFKI')` при вызове hello внутренней службы.

**Отображение** имя и **описание** обеспечивает описание операции hello и документации используется tooprovide toohello разработчики, использующие этот API на портале разработчиков hello.

![Описание][api-management-description]

Описание операции Hello в можно указать как обычный текст или HTML hello **описание** текстовое поле.

## <a name="operation-caching"> </a>Кэширование операций
Кэширование ответов снижает задержку для потребителей hello API, снижает потребление пропускной способности и уменьшается hello нагрузку на реализации службы web hello HTTP hello API. 

tooeasily и быстро включить кэширование для hello операции select hello **кэширование** вкладку и проверьте hello **включить** флажок.

![Caching][api-management-caching-tab]

**Длительность** определяет период времени, во время которого hello ответ операции остается в кэше hello hello. значение по умолчанию Hello — 3600 секунд или 1 час.

Кэширование ключей, используемых toodifferentiate между ответами, чтобы ответ hello соответствующий ключ другой кэша tooeach получите свой собственный отдельный кэшированное значение. При необходимости введите параметры строки запроса и/или toobe заголовки HTTP, используемый при вычислении значения ключа кэша в hello **происходит изменение параметров строки запроса** и **Vary заголовками** текстовые поля, соответственно. Когда ни одна не запроса задан, то полный URL-адрес и hello следующие значения заголовка HTTP используются при создании ключа кэша: **Accept** и **Accept-Charset**.

> Дополнительные сведения о кэшировании и политики кэширования см. в разделе [отображением результатов операции toocache в Azure API Management][How toocache operation results in Azure API Management].
> 
> 

## <a name="request-parameters"> </a>Параметры запроса
Параметры операции осуществляется на вкладке Параметры hello. Параметры, заданные в hello **URL-адрес шаблона** на hello **подписи** вкладка добавляются автоматически и можно изменить только путем изменения шаблона hello URL-адрес. Дополнительные параметры можно вводить вручную.

tooadd новый параметр запроса, нажмите кнопку **добавить параметр запроса** и введите hello следующую информацию:

* **Имя** - имя параметра.
* **Описание** -краткое описание параметра hello (необязательно).
* **Тип** -типа параметра, выбранного в раскрывающемся hello.
* **Значения** -значения, которые могут быть назначены toothis параметра. Одно из значений hello может быть помечен как по умолчанию (необязательно).
* **Требуется** -сделать обязательным параметром hello, установив флажок hello. 

![Параметры запроса][api-management-request-parameters]

## <a name="request-body"> </a>Текст запроса
Если операция hello позволяет (например, PUT, POST) и требует тело может предоставлять его во всех hello примером поддерживаемые форматы представления (например json, XML). 

> текст запроса Hello используется только для документирования и не проверяется.
> 
> 

текст запроса, tooenter переключения toohello **текст** вкладки.

Нажмите кнопку **добавить представление**начать ввод имени требуемого типа содержимого (например приложение/json), выберите его в раскрывающемся hello и вставить hello требуемого пример текста запроса в выбранном формате hello в текстовое поле hello. 

![Тело запроса][api-management-request-body]

В дополнительных toorepresentations также можно указать необязательное текстовое описание в hello **описание** текстовое поле.

## <a name="responses"> </a>Ответы
Это примеры tooprovide хорошей практикой ответов для всех коды состояния, которые может привести к операции hello. Каждый код состояния может иметь более одного пример текста ответа, один для каждого из hello поддерживаемые типы содержимого. 

Щелкните tooadd ответ, **добавить** и начните вводить код hello требуемого состояния. В этом пример hello состояние код- **200 ОК**. Если hello код отображается в раскрывающемся списке hello, выберите его и hello код ответа — операция создана и добавлена tooyour.

![Код ответа][api-management-response-code]

Нажмите кнопку **добавить представление**, начните вводить имя требуемого типа содержимого hello (например приложение/json) и выберите его в hello раскрывающийся список.

![Тип контента тела][api-management-response-body-content-type]

Вставьте hello пример текста ответа в выбранном формате hello в текстовое поле hello. 

![Тело ответа][api-management-response-body]

При желании добавьте описание (необязательно) в hello **описание** текстовое поле.

Настроив hello операцию, нажмите кнопку **Сохранить**.

## <a name="next-steps"> </a>Дальнейшие действия
После добавления hello операций tooan API hello следующий шаг hello tooassociate API с продуктом и опубликовать разработчики могут вызывать его операций.

* [Как toocreate и публикация продукта][How toocreate and publish a product]

[api-management-management-console]: ./media/api-management-howto-add-operations/api-management-management-console.png
[api-management-operations]: ./media/api-management-howto-add-operations/api-management-operations.png
[api-management-add-operation]: ./media/api-management-howto-add-operations/api-management-add-operation.png
[api-management-http-method]: ./media/api-management-howto-add-operations/api-management-http-method.png
[api-management-url-template]: ./media/api-management-howto-add-operations/api-management-url-template.png
[api-management-url-template-rewrite]: ./media/api-management-howto-add-operations/api-management-url-template-rewrite.png
[api-management-description]: ./media/api-management-howto-add-operations/api-management-description.png
[api-management-caching-tab]: ./media/api-management-howto-add-operations/api-management-caching-tab.png
[api-management-request-parameters]: ./media/api-management-howto-add-operations/api-management-request-parameters.png
[api-management-request-body]: ./media/api-management-howto-add-operations/api-management-request-body.png
[api-management-response-code]: ./media/api-management-howto-add-operations/api-management-response-code.png
[api-management-response-body-content-type]: ./media/api-management-howto-add-operations/api-management-response-body-content-type.png
[api-management-response-body]: ./media/api-management-howto-add-operations/api-management-response-body.png


[api-management-contoso-api]: ./media/api-management-howto-add-operations/api-management-contoso-api.png

[api-management-add-new-api]: ./media/api-management-howto-add-operations/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-add-operations/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-add-operations/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-add-operations/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-add-operations/api-management-echo-operations.png

[Add an operation]: #add-operation
[Operation caching]: #operation-caching
[Request parameters]: #request-parameters
[Request body]: #request-body
[Responses]: #responses
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocache operation results in Azure API Management]: api-management-howto-cache.md
