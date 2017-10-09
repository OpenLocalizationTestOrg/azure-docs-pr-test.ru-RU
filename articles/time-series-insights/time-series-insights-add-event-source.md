---
title: "aaaAdd tooyour Azure Insights ряда времени событий исходной среды | Документы Microsoft"
description: "В этом учебнике подключения tooyour аналитики ряда времени событий исходной среды"
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: santoshb
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: omravi
ms.openlocfilehash: 817df5e81cb4dc3d7376914a4651aabebadbcc32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-source-for-your-time-series-insights-environment-using-hello-ibiza-portal"></a>Создать источник событий для среды времени серии аналитики портале Ibiza hello

Источник событий Time Series Insights является производным от брокеров событий, таких как концентраторы событий Azure. Аналитики ряда времени непосредственно подключается tooEvent источников, передаче потока данных hello без необходимости toowrite пользователей одной строки кода. Сейчас Time Series Insights поддерживает концентраторы событий Azure и Центр Интернета вещей. Дополнительные источники событий будет добавлена в будущем hello.

## <a name="steps-tooadd-an-event-source-tooyour-environment"></a>Действия tooadd среды tooyour источника событий

1.  Войдите в toohello [портал Ibiza](https://portal.azure.com).
2.  Выберите «Все ресурсы» в меню hello hello левой части портала Ibiza hello.
3.  Выберите среду Time Series Insights.

  ![Создать источник событий аналитики ряда времени hello](media/add-event-source/getstarted-create-event-source-1.png)

4.  Выберите "Источники событий" и щелкните "+ Добавить".

  ![Создать источник событий аналитики ряда времени hello - подробные сведения](media/add-event-source/getstarted-create-event-source-2.png)

5.  Укажите имя источника события hello hello. Это имя связано со всеми событиями из источника событий. Оно доступно во время выполнения запроса.
6.  Выберите концентратор событий из списка hello ресурсов концентратора событий в текущей подписке hello. В противном случае выберите параметр импорта «параметры укажите концентратора событий вручную» toospecify концентратор событий в другую подписку. События должны быть опубликованы в формате JSON.
7.  Выберите политику, которая разрешение чтения в концентратор событий hello.
8.  Укажите концентратор событий или группу потребителей.

  > [!IMPORTANT]
  > Убедитесь, что эта группа потребителей не используется другой службой (например, заданием Stream Analytics или другой средой Time Series Insights). Если группа потребителей используется другими службами, считать операции отрицательно влияет для этой среды и hello других служб. При использовании как hello группа потребителей «$Default» может привести toopotential повторного использования другими пользователями.

9.  Щелкните "Создать".

После создания источника событий hello аналитики ряда времени с автоматическим запуском потоковой передачи данных в вашей среде.

## <a name="next-steps"></a>Дальнейшие действия

* [Отправлять события](time-series-insights-send-events.md) toohello источник события
* Просмотрите свою среду на [портале Time Series Insights](https://insights.timeseries.azure.com).
