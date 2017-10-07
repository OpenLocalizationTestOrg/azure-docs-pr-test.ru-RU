---
title: "Служба приложений Azure: масштабирование приложений службы приложений"
description: "Узнайте hello тонкости масштабирование приложения в службе приложений."
keywords: "служба приложений, служба приложений azure, масштабировать, масштабируемый, план службы приложений, стоимость службы приложений"
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: f403c971-4450-432b-8cea-3eeb426c0147
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/07/2016
ms.author: byvinyal
ms.openlocfilehash: d8cd12f73915a916a75d46da2f751a40d567b189
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-scaling-app-service-applications"></a>Служба приложений Azure: масштабирование приложений службы приложений
Приложения, размещенные в службе приложений Azure, можно [значительно масштабировать](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).
Однако масштабирование приложения является сложной задачей, у которой нет одного универсального решения. toocorrectly масштабировании приложения существует 3 ключевых областях, которые будут передавать успех tooyour приложений:

1. Понимание архитектуры и слабых сторон приложения.
   * Отслеживается в вашем приложении состояние или нет?
   * Что такое все компоненты приложения hello
     * Где находятся hello узких мест в приложении hello?
   * При нагрузке app примененных tooyour, что нарушит первый?
2. Основные сведения о hello ожидается требований к производительности и нагрузки.
   * Требуется ли приложение hello tooserve тысяч пользователей? или один миллион?
   * Будет ли трафик создаваться в определенном географическом регионе или повсеместно?
   * Будут ли иметь место сезонные колебания? Пики нагрузки?
   * Как быстро следует реагировать приложение hello в течение секунды или миллисекунды?
3. Основные сведения о и правильно используйте hello платформы размещения приложения.
   * Функции следует использовать tooachieve моих целей масштабирования?

В этом разделе помогут понять все факторы hello и справки, разработать стратегию, которая использует преимущества hello необходимые службы приложений функции tooachieve целей масштабируемости.

[!INCLUDE [app-service-blueprint-scaling-app-service-applications](../../includes/app-service-blueprint-scaling-app-service-applications.md)]

