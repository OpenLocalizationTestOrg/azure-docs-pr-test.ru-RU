---
title: "aaaHow tooConfigure параметры сервера в базе данных Azure для MySQL | Документы Microsoft"
description: "В этой статье описывается, как параметры tooconfigure доступный сервер в базе данных Azure для использования MySQL hello портал Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/19/2017
ms.openlocfilehash: 8292c8eda605854a06b6a9c82185c857bd353cfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-server-parameters-in-azure-database-for-mysql-using-hello-azure-portal"></a>Как tooconfigure параметры сервера в базе данных Azure с помощью MySQL hello портал Azure

База данных Azure для MySQL поддерживает настройку некоторых параметров сервера. В этой статье описывается, как tooconfigure эти параметры, с помощью hello портал Azure и списки hello поддерживается параметры, значения по умолчанию hello и hello диапазон допустимых значений. Не все параметры сервера можно настроить. Поддерживаются только hello перечисленных здесь.

## <a name="navigate-tooserver-parameters-blade-on-azure-portal"></a>Перейдите в колонку параметров tooServer на портале Azure

Войдите в портал Azure toohello, а затем выберите базу данных Azure для имени сервера MySQL. В разделе hello **параметры** щелкните **параметры сервера** колонки tooopen hello Server параметров для hello базы данных Azure для MySQL.

![Колонка "Параметры сервера" на портале Azure](./media/howto-server-parameters/auzre-portal-server-parameters.png)

## <a name="list-of-configurable-server-parameters"></a>Список доступных для настройки параметров сервера

Hello в следующей таблице перечислены параметры сервера в настоящее время поддерживается hello. Hello параметры можно настроить в соответствии с tooyour требованиям приложения.

> [!div class="mx-tableFixed"]
|Имя параметра|По умолчанию|Диапазонный индекс|Описание|
|---|---|---|---|
|binlog_group_commit_sync_delay|1000|0, 11–1 000 000|Элементы управления сколько микросекундах hello ожидает фиксации журнала в двоичном формате перед синхронизацией toodisk файл журнала в двоичном формате hello.|
|binlog_group_commit_sync_no_delay_count|0|0–1 000 000|Максимальное количество транзакций toowait для перед прекращением hello текущего задержки в соответствии с binlog группы фиксации sync задержки Hello.|
|character_set_server|LATIN1|BIG5, UTF8MB4 и т. д.|Используйте charset_name в качестве кодировки сервера по умолчанию hello.|
|div_precision_increment|4|0–30|Число знаков, с которых масштаб hello tooincrease hello результата операции деления.|
|group_concat_max_len|1024|4–16 777 216|Максимально допустимая длина результата в байтах для hello GROUP_CONCAT().|
|innodb_adaptive_hash_index|ВКЛ|ON, OFF|Указывает, включены ли адаптивные хэш-индексы InnoDB.|
|innodb_lock_wait_timeout|50|1–3600|Hello продолжительность времени в секундах транзакция InnoDB ожидает блокировка строки перед передачей.|
|interactive_timeout|1800|10–1800|Число секунд hello сервер ожидает действия с помощью интерактивного подключения перед его закрытием.|
|log_bin_trust_function_creators|ВЫКЛ.|ON, OFF|Эта переменная применяется, когда включено ведение журнала в двоичном формате. Это ограничение контролирует ли хранимой функции могут быть создатели доверенные не toocreate хранимой функции, вызывающие toobe небезопасный события записываются в журнал событий toohello двоичных файлов.|
|log_queries_not_using_indexes|ВЫКЛ.|ON, OFF|Журналы запросов, которые являются ожидается tooretrieve все tooslow строк для журнала запросов.|
|log_slow_admin_statements|ВЫКЛ.|ON, OFF|Включите инструкции медленно администратора в hello инструкций, созданных toohello журнал медленных запросов.|
|log_throttle_queries_not_using_indexes|0|0–4 294 967 295|Ограничения hello число таких запросов в минуту, который можно записать в журнал toohello медленных запросов.|
|long_query_time|10|1–10^100|Если запрос занимает больше времени, чем это (в секундах), hello server увеличивает значение переменной состояния Slow_queries hello.|
|max_allowed_packet|536 870 912|1024–1 073 741 824|Максимальный размер Hello один пакет или любая строка создается промежуточного или любого параметра, отправленных hello mysql_stmt_send_long_data() C API-функции.|
|min_examined_row_limit|0|0-18 446 744 073 709 551 615|Заносит в журнал запросов, которые содержат больше hello настроить количество строк в журнал медленных запросов hello. |
|server_id|3 293 747 068|1000–4 294 967 295|Hello server идентификатор, используемый в репликации toogive каждого главного и подчиненного уникальный идентификатор.|
|slave_net_timeout|60|30–3600|Hello количество секунд toowait дополнительные данные из образца hello ведомый hello считает подключения hello нечитаемым, прерывает чтение hello и пытается tooreconnect.|
|slow_query_log|ВЫКЛ.|ON, OFF|Включить или отключить журнал медленных запросов hello.|
|sql_mode|Выбрано значение 0.|ALLOW_INVALID_DATES, IGNORE_SPACE и т. д.|Hello текущий режим SQL server.|
|time_zone|SYSTEM|Примеры: -8:00, +05:30.|часовой пояс сервера Hello.|
|wait_timeout|120|60–240|Hello номер сервера hello секунд ожидает действие для неинтерактивных подключения перед его закрытием.|

## <a name="next-steps"></a>Дальнейшие действия
- [Библиотеки подключений для базы данных Azure для MySQL](concepts-connection-libraries.md)
