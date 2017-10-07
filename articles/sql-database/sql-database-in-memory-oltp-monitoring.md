---
title: "хранилище в памяти XTP aaaMonitor | Документы Microsoft"
description: "Сведения об оценке и мониторинге использования и емкости хранилища XTP в памяти и об устранении нехватки памяти 41823."
services: sql-database
documentationcenter: 
author: jodebrui
manager: jhubbard
editor: 
ms.assetid: b617308e-692c-4938-8fa2-070034a3ecef
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: jodebrui
ms.openlocfilehash: fcb17bd8e9ebef4862d4b55bf5a79b45b9419fca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-in-memory-oltp-storage"></a>Мониторинг хранилища OLTP в памяти
При использовании [выполняющейся в памяти OLTP](sql-database-in-memory.md) данные в оптимизированных для памяти таблицах и переменные таблиц находятся в выполняющемся в памяти хранилище OLTP. Каждая служба Premium имеет максимальный размер хранилища In-Memory OLTP, который описан в hello [статье уровни служб базы данных SQL](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels). При превышении этого ограничения операции вставки и обновления могут завершаться сбоем (ошибка 41823). На этом этапе будет требуется tooeither удаления данных tooreclaim памяти или обновите hello уровня производительности базы данных.

## <a name="determine-whether-data-will-fit-within-hello-in-memory-storage-cap"></a>Определить, будут ли данные не умещаются в cap hello хранилище в памяти
Определить ограничение хранилища hello: обратитесь к hello [статье уровни служб базы данных SQL](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) для hello хранилища caps hello разных уровней служб Premium.

Оценка памяти, что требования для оптимизированной для памяти таблицы работает hello таким же образом для SQL Server, как он выполняет в базе данных SQL Azure. Отключите эту статью tooreview несколько минут на [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).

Обратите внимание, что таблица hello и переменных строк таблицы, а также индексов, учитываются при определении размера данных hello max пользователя. Кроме того инструкции ALTER TABLE необходимо достаточное количество места toocreate новую версию hello всей таблицы и ее индексов.

## <a name="monitoring-and-alerting"></a>Мониторинг и оповещения
Вы можете отслеживать использование хранилища в памяти в процентах от hello [крепления хранилища для уровня производительности](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) в hello Azure [портала](https://portal.azure.com/): 

* В колонке базы данных hello найдите поле использования ресурсов hello и щелкните изменить.
* Выберите метрику hello `In-Memory OLTP Storage percentage`.
* tooadd оповещение, щелкните hello использование ресурсов поле tooopen hello колонка метрики, затем выберите команду добавить оповещение.

Или используйте hello следующий запрос использование хранилища в памяти tooshow hello:

    SELECT xtp_storage_percent FROM sys.dm_db_resource_stats


## <a name="correct-out-of-memory-situations---error-41823"></a>Исправление ситуаций с нехваткой памяти (ошибка 41823)
Нехватка памяти приводит к тому, что операции вставки, обновления и создания завершаются сбоем с сообщением об ошибке 41823.

Сообщение об ошибке 41823 означает, что hello оптимизированных для памяти таблицы и табличные переменные превысили максимальный размер hello.

tooresolve эту ошибку, либо:

* Удалить данные из оптимизированных для памяти таблиц hello, потенциально разгрузки tootraditional данных hello, дисковых таблиц; или,
* Обновление tooone уровня службы hello недостаточно места в памяти для данных hello необходимо tookeep в таблицах, оптимизированных для памяти.

## <a name="next-steps"></a>Дальнейшие действия
Инструкции по мониторингу см. в разделе [Мониторинг базы данных SQL Azure с помощью динамических представлений управления](sql-database-monitoring-with-dmvs.md).
