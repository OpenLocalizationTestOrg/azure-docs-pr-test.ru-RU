---
title: "Общие сведения о службах мультимедиа aaaAzure | Документы Microsoft"
description: "В этом разделе приводится краткий обзор служб мультимедиа Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7a5e9723-c379-446b-b4d6-d0e41bd7d31f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/04/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 81f9f4d9ff75effea30c10fd09449e9d2025f377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-overview"></a>Общие сведения о службах мультимедиа Azure 

Службы мультимедиа Microsoft Azure — это расширяемая платформа облачных, который позволяет разработчикам toobuild масштабируемая мультимедийная управления и доставки приложения. Media Services основана на API REST, которые позволяют toosecurely передачи, хранения, кодирования и упаковки аудио-и по запросу и динамической потоковой передачи доставки toovarious клиентов (например, ТВ, ПК и мобильных устройств).

Можно создавать сквозные рабочие процессы, полностью использующие службы мультимедиа. Можно также toouse компоненты сторонних разработчиков для некоторых частей рабочего процесса. Например, можно выполнять кодирование с помощью стороннего кодировщика. А затем отправить, защитить, упаковать и доставить содержимое с использованием служб мультимедиа.

Можно выбрать toostream динамического содержимого или доставки содержимого по запросу. Hello разделе также приведены ссылки tooother соответствующие разделы.

## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
Схемы обучения AMS можно просмотреть здесь:

* [Рабочий процесс для потоковой передачи в реальном времени в службах AMS](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-live/)
* [Рабочий процесс для потоковой передачи по запросу в службах AMS](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-on-demand/)

## <a name="prerequisites"></a>Предварительные требования

toostart с помощью служб мультимедиа Azure, должен иметь hello ниже:

* Учетная запись Azure. Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут. Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com).
* Учетная запись служб мультимедиа Azure. Дополнительные сведения см. в статье [Создание учетной записи служб мультимедиа Azure с помощью портала Azure](media-services-portal-create-account.md).
* Настройка среды разработки (необязательно) Выберите .NET или REST API для среды разработки. Дополнительные сведения см. в [разделе о настройке среды](media-services-dotnet-how-to-use.md).

    Кроме того, узнайте, каким образом слишком[программно подключаться tooAMS API](media-services-use-aad-auth-to-access-ams-api.md).
* Конечная точка потоковой передачи уровня "Стандартный" или "Премиум" в состоянии "Запущено".  Дополнительные сведения см. в статье [Управление конечными точками потоковой передачи](media-services-portal-manage-streaming-endpoints.md).

## <a name="sdks-and-tools"></a>Пакеты SDK и средства

toobuild решений служб мультимедиа, можно использовать:

* [REST API для службы мультимедиа.](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference)
* Одно из доступных клиентских hello SDK:
    * [Пакет SDK служб мультимедиа Azure для .NET](https://github.com/Azure/azure-sdk-for-media-services).
    * [Пакет Azure SDK для Java](https://github.com/Azure/azure-sdk-for-java).
    * [Пакет Azure SDK для PHP](https://github.com/Azure/azure-sdk-for-php).
    * [Службы мультимедиа Azure для Node.js](https://github.com/michelle-becker/node-ams-sdk/blob/master/lib/request.js) (это версия пакета SDK для Node.js сторонних производителей. Он поддерживается сообществом и в настоящее время не поддерживает полностью защитить hello API-интерфейсы AMS).
* Существующие средства:
    * [портал Azure](https://portal.azure.com/)
    * [Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (обозреватель служб мультимедиа Azure (AMSE) является приложением Winforms/С# для Windows)

## <a name="concepts-and-overview"></a>Основные сведения и понятия
Основные понятия служб мультимедиа Azure см. в статье [Основные понятия служб мультимедиа Azure](media-services-concepts.md).

Как tooseries, демонстрирующих tooall hello основные компоненты служб мультимедиа Azure, в разделе [учебники Azure Media Services пошаговое](https://docs.com/fukushima-shigeyuki/3439/english-azure-media-services-step-by-step-series). Эта серия имеет отличный обзор понятий и использует средство toodemonstrate AMS hello AMSE задачи. Средство AMSE разработано для Windows. Это средство поддерживает большинство задач hello, можно получить программным образом с [AMS пакет SDK для .NET](https://github.com/Azure/azure-sdk-for-media-services), [пакет Azure SDK для Java](https://github.com/Azure/azure-sdk-for-java), или [Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php).

## <a name="supported-scenarios-and-availability-of-media-services-across-data-centers"></a>Поддерживаемые сценарии и доступность служб мультимедиа в центрах обработки данных

Дополнительные сведения см. в статье [Scenarios and availability of features and services across data centers](scenarios-and-availability.md) (Сценарии и доступность функций служб мультимедиа в центрах обработки данных).

## <a name="service-level-agreement-sla"></a>Соглашение об уровне обслуживания (SLA):

* для кодирования с помощью служб мультимедиа мы гарантируем доступность транзакций через интерфейс REST API на уровне 99,9 %;
* Для потоковой передачи мы будем успешно обслуживать запросы с гарантией доступности на уровне 99,9 % для существующего мультимедийного содержимого, если приобретена одна конечная точка потоковой передачи уровня "Стандартный" или "Премиум".
* Для каналов Live мы гарантирует выполнение каналы внешнего подключения менее 99,9% времени hello.
* При защите содержимого мы гарантируем, что мы будет успешно выполнения ключа запросов менее 99,9% времени hello.
* Для индексатора, мы будет успешно обслуживать запросы индексатора задач, обрабатываться с кодировкой зарезервированный устройство 99,9% времени hello.

Дополнительные сведения можно найти в разделе [Соглашение об уровне обслуживания Microsoft Azure](https://azure.microsoft.com/support/legal/sla/).

Сведения о доступности в центрах обработки данных см. в разделе hello [Avaiability](scenarios-and-availability.md#availability) раздела.

## <a name="support"></a>Поддержка

[Служба поддержки Azure](https://azure.microsoft.com/support/options/) обеспечивает различные варианты поддержки для Azure, включая службы мультимедиа.

## <a name="provide-feedback"></a>Отзывы

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
