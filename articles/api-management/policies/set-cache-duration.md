---
title: "Пример политики управления Azure API: установка длительности для кэширования ответа | Документация Майкрософт"
description: "В примере политики управления API Azure показано, как задать длительность кэширования ответа при помощи значения maxAge в заголовке Cache-Control, который отправляется с сервера."
services: api-management
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/13/2017
ms.author: apimpm
ms.openlocfilehash: 8471b51999159c8f6233abbbce998b122163efd8
ms.sourcegitcommit: b854df4fc66c73ba1dd141740a2b348de3e1e028
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/04/2017
---
# <a name="set-response-cache-duration"></a>Установка длительности для кэширования ответа

В статье приведен пример политики управления API Azure, в котором показано, как задать длительность кэширования ответа при помощи значения maxAge в заголовке Cache-Control, который отправляется с сервера. См. дополнительные сведения о [создании и изменении кода политики](../set-edit-policies.md). Также для ознакомления доступны другие [примеры политик](../policy-samples.md).

## <a name="policy"></a>Политика

Вставьте код в блок **inbound**.

[!code-xml[Main](../../../api-management-policy-samples/Snippets/Set cache duration using response cache control header.policy.xml)]

## <a name="next-steps"></a>Дальнейшие действия

Подробнее о политиках службы управления API:

+ [Политики преобразования](../api-management-transformation-policies.md)
+ [Примеры политик](../policy-samples.md)

