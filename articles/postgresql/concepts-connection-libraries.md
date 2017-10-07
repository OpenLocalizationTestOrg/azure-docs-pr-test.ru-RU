---
title: "Библиотеки подключений для базы данных Azure для PostgreSQL | Документация Майкрософт"
description: "В этой статье описываются некоторые библиотеки и драйверы, которые разработчики могут использовать при программировании для PostgreSQL tooconnect приложений и запрос базы данных Azure."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/15/2017
ms.openlocfilehash: 1f7234499d8abe37f8de9008e3158765b1fb0bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connection-libraries-for-azure-database-for-postgresql"></a>Библиотеки подключений для базы данных Azure для PostgreSQL
В этом разделе перечислены библиотеки и драйверы для использования разработчиками для программирования для PostgreSQL tooconnect приложений и запрос базы данных Azure.

## <a name="client-interfaces"></a>Интерфейсы клиента
Большинство языка клиента библиотеки tooconnect tooPostgreSQL сервера являются внешние проекты и распространяются независимо друг от друга. Они поддерживаются на платформах Windows, Linux и Mac. Перечислены некоторые популярные клиентские драйверы hello.

| **Язык** | **Интерфейс клиента** | **Дополнительные сведения** | **Загрузить** |
|--------------|----------------------------------------------------------------|-------------------------------------|--------------------------------------------------------------------|
| Python | [psycopg](http://initd.org/psycopg/) | Интерфейс API базы данных, совместимый с версией 2.0 | [Загрузить](http://initd.org/psycopg/download/) |
| PHP | [php-pgsql](https://php.net/manual/en/book.pgsql.php) | Расширение базы данных | [Установка](https://secure.php.net/manual/en/pgsql.installation.php) |
| Node.js | [Пакет pg npm](https://www.npmjs.com/package/pg) | Клиент чистого JavaScript без блокировки | [Установка](https://www.npmjs.com/package/pg) |
| Java | [JDBC](http://jdbc.postgresql.org/) | Драйвер JDBC типа 4 | [Загрузить](https://jdbc.postgresql.org/download.html)  |
| Ruby | [Пакет pg](https://deveiate.org/code/pg/) | Интерфейс Ruby | [Загрузить](https://rubygems.org/downloads/pg-0.20.0.gem) |
| Go | [Пакет pq](https://godoc.org/github.com/lib/pq) | Драйвер postgres для чистого Go | [Установка](https://github.com/lib/pq/blob/master/README.md) |
| C\#/ .NET | [Npgsql](http://www.npgsql.org/) | Поставщик данных ADO.NET | [Загрузить](https://www.microsoft.com/net/) |
| ODBC | [psqlODBC](https://odbc.postgresql.org/) | Драйвер ODBC | [Загрузить](http://www.postgresql.org/ftp/odbc/versions/) |
| C | [libpq](https://www.postgresql.org/docs/9.6/static/libpq.html) | Основной интерфейс для языка C | Включено |
| C++ | [libpqxx](http://pqxx.org/) | Новый стиль интерфейса для языка C++ | [Загрузить](http://pqxx.org/download/software/) |

## <a name="next-steps"></a>Дальнейшие действия
Эти краткие руководства о том, как прочитать tooconnect и запросов Azure этой базы данных PostgreSQL, используя выбранный язык:

[Python](./connect-python.md) | [Node.JS](./connect-nodejs.md) | [.NET (C#)](./connect-csharp.md)
