---
title: "обработки путем добавления единицы кодирования — Azure media aaaScale |  Документы Microsoft"
description: "Узнайте, как единицы кодирования tooadd toohow в .NET Framework"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 33f7625a-966a-4f06-bc09-bccd6e2a42b5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;milangada;
ms.openlocfilehash: b9f71a6487c5d136319a38a1598d60edfaa81b9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-encoding-with-net-sdk"></a>Как tooscale кодирование с помощью пакета SDK для .NET
> [!div class="op_single_selector"]
> * [Портал](media-services-portal-scale-media-processing.md)
> * [.NET](media-services-dotnet-encoding-units.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a>Обзор
> [!IMPORTANT]
> Убедитесь, что hello tooreview [Обзор](media-services-scale-media-processing-overview.md) tooget разделе Дополнительные сведения о масштабировании раздела с мультимедиа.
> 
> 

toochange hello зарезервированные единицы типа и hello количество зарезервированные единицы кодирования с помощью пакета SDK .NET, hello следующие:

    IEncodingReservedUnit encodingS1ReservedUnit = _context.EncodingReservedUnits.FirstOrDefault();
    encodingS1ReservedUnit.ReservedUnitType = ReservedUnitType.Basic; // Corresponds tooS1
    encodingS1ReservedUnit.Update();
    Console.WriteLine("Reserved Unit Type: {0}", encodingS1ReservedUnit.ReservedUnitType);

    encodingS1ReservedUnit.CurrentReservedUnits = 2;
    encodingS1ReservedUnit.Update();

    Console.WriteLine("Number of reserved units: {0}", encodingS1ReservedUnit.CurrentReservedUnits);

## <a name="opening-a-support-ticket"></a>Открытие запроса в службу поддержки
По умолчанию каждая учетная запись служб мультимедиа можно масштабировать tooup too25 кодирования и 5 по требованию зарезервированные элементы потоковой передачи. Вы можете запросить более высокий предел, открыв запрос в службу поддержки.

### <a name="open-a-support-ticket"></a>Открытие запроса в службу поддержки
обращение в службу поддержки tooopen hello следующие:

1. Щелкните [Получить поддержку](https://manage.windowsazure.com/?getsupport=true). Если вы не вошли в, будет иметь tooenter запрашиваемые учетные данные.
2. Выберите свою подписку.
3. В группе типа поддержки выберите "Техническая".
4. Щелкните "Создать запрос в службу поддержки".
5. Выберите «Службы мультимедиа Azure» в список продуктов hello приведены на следующей странице приветствия.
6. Выберите соответствующее значение в поле "Тип проблемы".
7. Нажмите кнопку "Продолжить".
8. Следуйте указаниям на следующей странице, а затем введите сведения о проблеме.
9. Нажмите кнопку Отправить запрос tooopen hello.

## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

