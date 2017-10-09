---
title: "Правила брандмауэра сервера базы данных Azure для PostgreSQL | Документация Майкрософт"
description: "Описываются правила брандмауэра сервера базы данных Azure для PostgreSQL."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 1d46a4434c483c3612a9a7b4cdef718d6dc3e765
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-server-firewall-rules"></a>Правила брандмауэра сервера базы данных Azure для PostgreSQL
Брандмауэр не все сервера базы данных access tooyour, пока вы не укажете компьютеры, на которых есть разрешение. Hello брандмауэр предоставляет серверу toohello доступ на основании hello, рассчитанные на IP-адреса каждого запроса.
tooconfigure брандмауэра, создать правила брандмауэра, которые указывают диапазон допустимых IP-адресов. Можно создавать правила брандмауэра на уровне сервера hello.

**Правила брандмауэра:** эти правила позволяют клиентам tooaccess всей базы данных Azure для сервера PostgreSQL, то есть все базы данных hello в hello на одном логическом сервере. Правила брандмауэра уровня сервера можно настроить с помощью hello портал Azure или Azure CLI команд. правила брандмауэра уровня сервера toocreate, необходимо быть владельцем подписки hello или участником подписки.

## <a name="firewall-overview"></a>Общие сведения о брандмауэре
Доступ tooyour все базы данных базы данных Azure для сервера PostgreSQL заблокирован брандмауэром hello по умолчанию. toobegin с помощью сервера с другого компьютера необходимо toospecify один или более серверного уровня брандмауэра правила tooenable доступа tooyour сервера. Используйте toospecify правила брандмауэра hello, какой IP-адрес в диапазоне от tooallow Интернет hello. Toohello доступа Azure веб-сайта портала сам он не подвержен влиянию hello правила брандмауэра.
Здравствуйте, попытки соединения из Интернета и Azure должны сначала пройти через брандмауэр hello до попадания базы данных PostgreSQL, как показано в hello, следующая схема:

![Поток пример того, как работает брандмауэр hello](media/concepts-firewall-rules/1-firewall-concept.png)

## <a name="connecting-from-hello-internet"></a>Подключение из Интернета hello
Правила брандмауэра уровня сервера в hello базы данных Azure для сервера PostgreSQL применяются tooall баз данных. Если в одном из диапазонов hello, указанных в правилах брандмауэра уровня сервера hello hello IP-адреса запроса hello, предоставляется возможность подключения hello.
Если IP-адреса hello hello запроса находится за пределами hello диапазонов, указанных в hello уровня базы данных или правила брандмауэра уровня сервера, происходит сбой запроса подключения hello.
Например если приложение соединяется с драйвером JDBC для PostgreSQL, могут возникнуть ошибки попытка tooconnect при hello брандмауэр блокирует подключение hello.
> java.util.concurrent.ExecutionException: java.lang.RuntimeException: org.postgresql.util.PSQLException: FATAL: no pg\_hba.conf entry for host "123.45.67.890", user "adminuser", database "postgresql", SSL

## <a name="programmatically-managing-firewall-rules"></a>Программное управление правилами брандмауэра
В дополнение к этому toohello портал Azure, могут быть правила брандмауэра управлять программным путем с помощью Azure CLI.
Ознакомьтесь также со статьей [Создание правил брандмауэра базы данных Azure для PostgreSQL и управление ими с помощью Azure CLI](howto-manage-firewall-using-cli.md).

## <a name="troubleshooting-hello-database-firewall"></a>Устранение неполадок брандмауэра hello базы данных
Примите во внимание при toohello доступа к базе данных Microsoft Azure для службы сервера PostgreSQL работать не так, как предполагается, что следующие точки hello.

* **Список разрешенных toohello изменения не вступили в силу еще:** может быть как больше пяти минут задержки для изменения toohello базы данных Azure для эффекта tootake конфигурации брандмауэра сервера PostgreSQL.

* **Hello входа не имеет прав или неправильный пароль был использован:** hello toohello подключения базы данных Azure для сервера PostgreSQL — Если имени входа нет разрешений на hello базы данных Azure для PostgreSQL сервера или hello используется неверный пароль, запрещено. Только создания параметра брандмауэра предоставляет клиентам возможность tooattempt подключении tooyour серверу; Каждый клиент должен предоставить необходимые учетные записи hello.

Например с помощью клиента JDBC, может появиться следующая ошибка hello.
> java.util.concurrent.ExecutionException: java.lang.RuntimeException: org.postgresql.util.PSQLException: FATAL: password authentication failed for user "yourusername"

* **Динамический IP-адрес:** при наличии подключения к Интернету с динамическим IP-адресов и испытываете проблемы с прохождением через брандмауэр hello, может воспользоваться hello следующие решения:

* Попросите поставщика услуг Интернета (ISP) для диапазона IP-адресов hello hello, доступа к базе данных Azure tooyour клиентских компьютеров, назначенных для сервера PostgreSQL, а затем добавьте hello диапазон IP-адресов в качестве правила брандмауэра.

* Получить статический IP-адреса для клиентских компьютеров, а затем задать hello IP-адреса в правила брандмауэра.

## <a name="next-steps"></a>Дальнейшие действия
Ниже перечислены статьи о создании правил брандмауэра уровня сервера и уровня базы данных.
* [Создание и управление для правила брандмауэра PostgreSQL, с помощью портала Azure hello базы данных Azure](howto-manage-firewall-using-portal.md)
* [Создание правил брандмауэра базы данных Azure для PostgreSQL и управление ими с помощью Azure CLI](howto-manage-firewall-using-cli.md)