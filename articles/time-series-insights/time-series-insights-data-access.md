---
title: "aaaData политики доступа в Azure Insights ряда времени | Документы Microsoft"
description: "В этом учебнике вы узнаете toomanage политикам доступа в серии аналитики времени"
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/01/2017
ms.author: omravi
ms.openlocfilehash: f286d26c8c5c851c523e9384760dc4b10711fa3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="grant-data-access-tooa-time-series-insights-environment-using-azure-portal"></a>Предоставьте среда доступа к данным tooa аналитики ряда времени с помощью портала Azure

Среда Time Series Insights содержит 2 типа независимых политик доступа:

* политики управления доступом;
* политики доступа к данным.

Оба типа политик предоставляют субъектам Azure Active Directory (пользователям или приложениям) различные разрешения для конкретной среды. Hello субъекты (пользователи и приложения) должны принадлежать toohello active directory (или «Клиент Windows Azure»), связанных с hello подписку, содержащую hello среды.

Политики управления доступом предоставить разрешения связанных toohello конфигурация hello среды, такие как
*   Создание и удаление среды hello, источники событий ссылаться на наборы данных и
*   Управление данными hello политики доступа.

Политики доступа данных tooissue запросы данных, разрешения ссылочных данных в среде hello, совместное и сохраненные запросы и перспективам, связанным со средой hello.

Hello два вида политики позволяют четкое разделение между toohello управления доступом hello среды и доступ к данным toohello внутри среды hello. Например это возможно toosetup среду таким образом, что hello владелец создатель hello среды удаляется из hello доступа к данным. А также пользователей и служб, которые допускаются tooread данные из среды hello могут предоставляться без настройки доступа toohello hello среды.

## <a name="grant-data-access"></a>Предоставление доступа к данным
Hello следующие шаги показывают, как доступ к данным toogrant для участника-пользователя:

1.  Войдите в toohello [портал Azure](https://portal.azure.com).
2.  В меню hello hello левой части hello портал Azure, выберите «Все ресурсы».
3.  Выберите среду Time Series Insights.

  ![Управление источником времени серии аналитики hello - среды](media/data-access/getstarted-grant-data-access1.png)

4.  Выберите Data Plane Access (Доступ к плоскости данных) и щелкните "Добавить".

  ![Управление источником времени серии аналитики hello - Добавление](media/data-access/getstarted-grant-data-access2.png)

5.  Щелкните "Выбор пользователя".
6.  Поиск и выбор пользователя по электронной почте hello.
7.  В колонке "Выбор пользователя" нажмите кнопку "Выбрать".

  ![Управление источником времени серии аналитики hello — Выбор пользователя](media/data-access/getstarted-grant-data-access3.png)

8.  Щелкните "Выбор ролей".
9.  Выберите «Участник», tooallow пользователя toochange ссылочных данных и предоставить другим пользователям среды hello сохраненные запросы и перспективы. В противном случае выберите «Чтения» tooallow пользователь запросов данных в среде hello и сохранение личных (не общем) запросов в среде hello.
10. В колонке «Выберите роль» hello, нажмите кнопку «ОК».

  ![Управление источником времени серии аналитики hello — выберите роль](media/data-access/getstarted-grant-data-access4.png)

11. В колонке «Выберите роль пользователя» hello, нажмите кнопку «ОК».
12. Вы должны увидеть следующее:

  ![Управление источником времени серии аналитики hello - результаты](media/data-access/getstarted-grant-data-access5.png)

## <a name="next-steps"></a>Дальнейшие действия

* [Создание источника событий](time-series-insights-add-event-source.md)
* [Отправлять события](time-series-insights-send-events.md) toohello источник события
* Просмотрите свою среду на [портале Time Series Insights](https://insights.timeseries.azure.com).
