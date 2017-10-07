---
title: "Обработка с использованием носителя aaaScale hello портал Azure | Документы Microsoft"
description: "Этот учебник поможет выполнить действия hello масштабирования носителя, обработка с использованием портала Azure hello."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: e500f733-68aa-450c-b212-cf717c0d15da
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: juliako
ms.openlocfilehash: 89240c6f7579b8795e7b47f2b1c398b1d5477e20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-reserved-unit-type"></a>Изменение hello защищены тип единицы измерения
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-encoding-units.md)
> * [Портал](media-services-portal-scale-media-processing.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a>Обзор

Учетная запись служб мультимедиа связан с зарезервированным тип базового определяет hello скорость обработки задач обработки мультимедиа. Можно выбрать между hello следующие зарезервированные типы единиц измерения: **S1**, **S2**, или **S3**. Например, hello же кодированию выполняется быстрее при использовании hello **S2** тип зарезервированных единиц сравнить toohello **S1** типа.

Кроме toospecifying hello зарезервировано тип единицы измерения, можно указать tooprovision свою учетную запись с **зарезервированных единиц** (RUs). Hello число подготовленных RUs определяет hello количество мультимедийных задач, которые можно одновременно обрабатывать в данной учетной записи.

>[!NOTE]
>Зарезервированные единицы позволяют распараллелить всю обработку мультимедиа, включая задания индексирования с использованием индексатора мультимедийных данных Azure. Однако в отличие от кодировки, задания индексирования не будут обрабатываться быстрее при использовании более производительных зарезервированных единиц.

> [!IMPORTANT]
> Убедитесь, что hello tooreview [Обзор](media-services-scale-media-processing-overview.md) tooget разделе Дополнительные сведения о масштабировании раздела с мультимедиа.
> 
> 

## <a name="scale-media-processing"></a>Масштабирование обработки мультимедиа
toochange hello зарезервированные единицы типа и hello число зарезервированных единиц hello следующие:

1. В hello [портал Azure](https://portal.azure.com/), выберите учетную запись служб мультимедиа Azure.
2. В hello **параметры** выберите **зарезервированные единицы мультимедиа**.
   
    Число зарезервированных единиц для hello hello toochange выбранный тип зарезервированных единиц, используйте hello **единицы обслуживаться носителя** ползунок.
   
    toochange hello **тип ЗАРЕЗЕРВИРОВАННЫХ ЕДИНИЦ**, нажмите клавишу S1, S2 и S3.
   
    ![Страница "Процессоры"](./media/media-services-portal-scale-media-processing/media-services-scale-media-processing.png)
3. Нажмите клавишу hello СОХРАНИТЕ toosave кнопки изменения.
   
    новые зарезервированные элементы Hello выделяются при нажатии клавиши СОХРАНЕНИЯ.

## <a name="next-steps"></a>Дальнейшие действия
Просмотрите схемы обучения работе со службами мультимедиа.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

