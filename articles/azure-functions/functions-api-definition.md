---
title: "метаданные aaaOpenAPI в функциях Azure | Документы Microsoft"
description: "Обзор поддержки OpenAPI в Функциях Azure"
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 03/23/2017
ms.author: alkarche
ms.openlocfilehash: fff8f14110469a002a6c9dca03f641672003a3a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="openapi-20-metadata-support-in-azure-functions-preview"></a>Поддержка метаданных OpenAPI 2.0 в Функциях Azure (предварительная версия)
OpenAPI 2.0 (прежнее название — Swagger) поддержки метаданных в функциях Azure имеет функцию предварительного просмотра, которые можно использовать определения toowrite OpenAPI 2.0 в приложении функции. Затем можно разместить файл с помощью функции приложения hello.

[Метаданные OpenAPI](http://swagger.io/) позволяет функции, на котором размещается toobe REST API, используемые широкий спектр другого программного обеспечения. Это программное обеспечение включает предложения Майкрософт, например PowerApps и hello [функций приложения API службы приложений Azure](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), средств сторонних разработчиков, например [почтальон](https://www.getpostman.com/docs/importing_swagger), и [многие дополнительные пакеты](http://swagger.io/tools/).

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

>[!TIP]
>Рекомендуется начинать с hello [учебник по началу работы](./functions-api-definition-getting-started.md) и последующий возврат документа toolearn toothis Дополнительные сведения о конкретных компонентов.

## <a name="enable"></a>Включение поддержки определения OpenAPI
Можно настроить все параметры OpenAPI на hello **определения API** страницы в приложении функции **возможности платформы**.

значение поколения hello tooenable размещенного определения OpenAPI и определении краткое руководство **источник определения API** слишком**функции (Предварительная версия)**. **Внешний URL-адрес** позволяет вашей toouse функция определение OpenAPI, который размещается в другом месте.

## <a name="generate-definition"></a>Создание схемы Swagger на основе метаданных функции
Шаблон поможет вам приступить к написанию первого определения OpenAPI. Hello определение шаблона функции создает определение разреженных OpenAPI с помощью все метаданные hello в файле function.json hello для каждой из функций триггер HTTP. Вам потребуется toofill более подробные сведения о своем API из hello [OpenAPI спецификации](http://swagger.io/specification/), например шаблоны запросов и ответов.

Пошаговые инструкции см. в разделе hello [учебник по началу работы](./functions-api-definition-getting-started.md).

### <a name="templates"></a>Доступные шаблоны

|Имя| Описание |
|:-----|:-----|
|Созданное определение|Определение OpenAPI с hello максимальный объем данных может быть выведен из метаданных существующей функции hello.|

### <a name="quickstart-details"></a>Включить метаданные в hello созданное определение

Следующая таблица представляет Hello hello Azure Параметры портала и соответствующих данных в function.json как сопоставленные toohello создан каркас Swagger.

|Swagger.json|Пользовательский интерфейс портала|Function.json|
|:----|:-----|:-----|
|[Host](http://swagger.io/specification/#fixed-fields-15)|**Параметры приложения-функции** > **Параметры службы приложений** > **Обзор** > **URL-адрес**|*Отсутствует*
|[Paths](http://swagger.io/specification/#paths-object-29)|**Интегрировать** > **Выбранные методы HTTP**|Bindings: Route
|[Path Item](http://swagger.io/specification/#path-item-object-32)|**Интегрировать** > **Шаблон маршрута**|Bindings: Methods
|[Безопасность](http://swagger.io/specification/#security-scheme-object-112)|**Ключи**|*Отсутствует*|
|operationID*|**Маршрут + допустимые команды**|Маршрут + допустимые команды|

\*Идентификатор операции Hello является обязательным только для интеграции с PowerApps и потока.
> [!NOTE]
> расширение x-ms-summary Hello предоставляет отображаемое имя в приложении логики, PowerApps и потока.
>
> toolearn более, в разделе [настроить определение Swagger для PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/).

## <a name="CICD"></a>Использовать определение элемента конфигурации/CD tooset API-Интерфейс

 Необходимо включить API определения размещение портала hello перед включением toomodify управления источника вашего определения API из системы управления версиями. Выполните следующие действия:

1. Обзор слишком**определения API (Предварительная версия)** в функции настройки параметров приложения.
  1. Задать **источник определения API** слишком**функция**.
  1. Нажмите кнопку **шаблон API для создания определения** и затем **Сохранить** toocreate определение шаблона для изменения позже.
  1. Обратите внимание на URL-адрес и ключ определения API.
1. [Настройте непрерывную интеграцию и развертывание](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment#continuous-deployment-requirements).
2. Измените файл swagger.json в системе управления исходным кодом по адресу \site\wwwroot\.azurefunctions\swagger\swagger.json.

Теперь изменения, размещенные на функции приложения по URL-АДРЕСУ определения hello API tooswagger.json в репозиторий и ключ, записанное в этап 1.c.

## <a name="next-steps"></a>Дальнейшие действия
* [Создание метаданных OpenAPI 2.0 (Swagger) для приложения-функции (предварительная версия)](functions-api-definition-getting-started.md). Попробуйте нашем пошаговом руководстве toosee определение OpenAPI в действии.
* [Репозиторий GitHub для Функций Azure](https://github.com/Azure/Azure-Functions/). Извлечь toogive репозитория функции hello нам отзывы о обзор поддержки определения hello API. Сделайте вопрос GitHub для чего нужно обновить toosee.
* [Руководство для разработчиков по Функциям Azure](functions-reference.md). Сведения о написании кода функций и определении триггеров и привязок.
