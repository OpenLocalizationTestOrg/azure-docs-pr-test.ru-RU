---
title: "aaaServer журналы в базе данных Azure для PostgreSQL | Документы Microsoft"
description: "Создание журналов запросов и ошибок в базе данных Azure для PostgreSQL."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 22575f3882ce67fe640952f0a8dbfd8dcb4b16fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="server-logs-in-azure-database-for-postgresql"></a>Журналы сервера в базе данных Azure для PostgreSQL 
База данных Azure для PostgreSQL создает журналы запросов и ошибок. Тем не менее журналы tootransaction доступа не поддерживается. Эти журналы могут быть используется tooidentify, устранение неполадок и исправить ошибки конфигурации и проблемы с производительностью. Дополнительные сведения см. на странице [Error Reporting and Logging](https://www.postgresql.org/docs/9.6/static/runtime-config-logging.html) (Отчеты об ошибках и ведение журнала).

## <a name="access-server-logs"></a>Доступ к журналам сервера
Можно перечислить и загрузить с помощью портала Azure hello журналы ошибок сервера Azure PostgreSQL [Azure CLI](howto-configure-server-logs-using-cli.md) и API REST Azure.

## <a name="log-retention"></a>Хранение журналов
Можно задать срок хранения hello журналы системы с помощью **журнала\_хранения\_период** параметр, связанный с сервером. Единица измерения Hello для этого параметра — дней (требуются tooconfirm). значение по умолчанию Hello — три дня. Hello максимальное значение составляет 7 дней. Обратите внимание, что ваш сервер должен иметь достаточно hello toocontain хранилище, выделенное сохраняются файлы журналов.
файлы журналов Hello будет вращаться каждый час или размером 100 МБ, наступит раньше.

## <a name="configure-logging-for-azure-postgresql-server"></a>Настройка ведения журнала для сервера Azure PostgreSQL
Вы можете включить для своего сервера ведение журнала запросов и журнала ошибок. Журналы ошибок могут содержать сведения об автоматической очистке, подключениях и контрольных точках.

Чтобы включить ведение журнала запросов для экземпляра базы данных PostgreSQL, необходимо настроить два параметра сервера: log\_statement и log\_min\_duration\_statement.

Hello **журнала\_инструкции** параметр определяет, какие инструкции SQL регистрируются. Рекомендуется установить этот параметр слишком***все*** toolog все операторы; значение по умолчанию hello none (необходим tooconfirm).

Hello **журнала\_min\_длительность\_инструкции** параметр задает hello предел в миллисекундах toobe инструкции, в журнал. Регистрируются все инструкции SQL, выполняемых больше значения параметра hello. Этот параметр является toominus отключено и 1 (-1) по умолчанию (необходимость tooconfirm). Включение этого параметра может быть полезным, когда требуется отследить в приложениях неоптимизированные запросы.

Hello **журнала\_min\_сообщений** позволяет toocontrol, какие уровни сообщений записываются в журнал toohello сервера. по умолчанию Hello — предупреждение. (требуется tooconfirm)

Дополнительные сведения об этих настройках см. в документации на странице [Error Reporting and Logging](https://www.postgresql.org/docs/9.6/static/runtime-config-logging.html) (Отчеты об ошибках и ведение журнала). Чтобы настроить конкретно параметры сервера базы данных Azure для PostgreSQL, см. статью [Журналы сервера в базе данных Azure для PostgreSQL](concepts-server-logs.md).

## <a name="next-steps"></a>Дальнейшие действия
- см. журналы tooaccess, с помощью интерфейса командной строки Azure CLI [настроить и доступ журналы сервера, с помощью Azure CLI](howto-configure-server-logs-using-cli.md)
- Дополнительные сведения о параметрах сервера см. в статье [Настройка параметров службы в базе данных Azure для PostgreSQL](howto-configure-server-parameters-using-cli.md).