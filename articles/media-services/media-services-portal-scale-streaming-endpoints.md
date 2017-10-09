---
title: "конечные точки с портала Azure hello потоковой передачи aaaScale | Документы Microsoft"
description: "Этот учебник поможет выполнить шаги hello масштабирования конечных точек потоковой передачи с hello портал Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 1008b3a3-2fa1-4146-85bd-2cf43cd1e00e
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: juliako
ms.openlocfilehash: e466edf9232558b9e270f54ee2849cd9b22ad121
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="scale-streaming-endpoints-with-hello-azure-portal"></a>Масштабирование конечных точек потоковой передачи с hello портал Azure
## <a name="overview"></a>Обзор

> [!NOTE]
> toocomplete этого учебника необходима учетная запись Azure. Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

Конечные точки уровня **Премиум** подходят для выполнения более сложных задач благодаря выделенной пропускной способности и возможности масштабирования. Клиенты, имеющие конечную точку потоковой передачи уровня **Премиум**, по умолчанию получают одну единицу потоковой передачи. Hello конечной точки потоковой передачи можно масштабировать, добавляя SUs. Каждый SU приводится дополнительная пропускная способность емкость toohello приложения. Дополнительные сведения о потоковой передаче типы конечных точек и настройке CDN см. в разделе hello [Общие сведения о конечной точке потоковой передачи](media-services-portal-manage-streaming-endpoints.md) раздела.
 
В этом разделе показано, как tooscale конечной точки потоковой передачи.

Дополнительные сведения о ценах на службы мультимедиа см. [здесь](http://go.microsoft.com/fwlink/?LinkId=275107).

## <a name="scale-streaming-endpoints"></a>Масштабирование конечных точек потоковой передачи

число единиц потоковой передачи hello toochange hello следующие:

1. В hello [портал Azure](https://portal.azure.com/), выберите учетную запись служб мультимедиа Azure.
2. В hello **параметры** выберите **конечные точки потоковой передачи**.
3. Щелкните конечную точку потоковой передачи hello, которые должны tooscale. 

    [!NOTE] Масштабировать можно только конечные точки потоковой передачи уровня **Премиум**.

4. Переместите hello ползунок toospecify hello число единиц потоковой передачи.

    ![конечной точки потоковой передачи](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints3.png)

## <a name="next-steps"></a>Дальнейшие действия
Просмотрите схемы обучения работе со службами мультимедиа.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

