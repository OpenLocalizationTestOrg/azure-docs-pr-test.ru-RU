---
title: "Основные понятия aaaServer в базе данных Azure для PostgreSQL | Документы Microsoft"
description: "В этой статье приведены рекомендации и указания по работе с серверами базы данных Azure для PostgreSQL."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 07/06/2017
ms.openlocfilehash: 9cc7816992f2ddedd76fdf906075a723b97720a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-servers"></a>Серверы базы данных Azure для PostgreSQL
В этой статье приведены рекомендации и указания по работе с серверами базы данных Azure для PostgreSQL.

## <a name="what-is-an-azure-database-for-postgresql-server"></a>Что такое сервер базы данных Azure для PostgreSQL?
Сервер базы данных Azure для PostgreSQL является центральной точкой администрирования нескольких баз данных. Это же конструкции сервера PostgreSQL, вы не знакомы с в локальной Здравствуй, мир! hello. В частности hello PostgreSQL службы является управляемым, он предоставляет гарантии исполнения, предоставляет доступ и функций на уровне сервера.

Сервер базы данных Azure для PostgreSQL:

- создается в подписке Azure;
- — Hello родительского ресурса для базы данных.
- предоставляет пространство имен для баз данных;
- — Это контейнер, в соответствии с семантикой строгого время существования - удалить сервер, а также удаляет hello содержится баз данных.
- выравнивает ресурсы в регионе;
- предоставляет конечную точку подключения к серверу и базе данных (.postgresql.database.azure.com);
- Предоставляет область hello для применяемых баз данных tooits политик управления: имя входа, брандмауэр, пользователей, ролей, конфигурации, и т. д.
- доступен в нескольких версиях (дополнительные сведения см. в статье [Поддерживаемые версии в базе данных Azure для PostgreSQL](concepts-supported-versions.md));
- расширяется пользователями (дополнительные сведения см. в статье [Использование расширений PostgreSQL в базе данных Azure для PostgreSQL](concepts-extensions.md)).

На сервере базы данных Azure для PostgreSQL можно создать одну или несколько баз данных. Необязательно toocreate одной базы данных на сервере tooutilize все ресурсы hello или создать несколько баз данных tooshare hello ресурсы. цены Hello структурированных сервера, в зависимости от конфигурации hello данного ценового уровня вычислений единицы, служба хранилища (ГБ). Дополнительные сведения см. в разделе [Ценовые категории](./concepts-service-tiers.md).

## <a name="how-do-i-connect-and-authenticate-tooan-azure-database-for-postgresql-server"></a>Как подключения и проверки подлинности tooan базы данных Azure для сервера PostgreSQL?
Hello следующие элементы помогают обеспечить безопасный доступ к базе данных tooyour.

|||
| :-- | :-- |
| **Аутентификация и авторизация** | Сервер базы данных Azure для PostgreSQL поддерживает собственную аутентификацию PostgreSQL. Можно подключиться и проверки подлинности tooserver с именем входа администратора сервера hello. |
| **Протокол** | Служба Hello поддерживает протокол на уровне сообщений, используемый PostgreSQL. |
| **TCP/IP** | протокол Hello поддерживается по протоколу TCP/IP, а также через сокеты домена Unix. |
| **Брандмауэр** | toohelp защиты данных, все сервера базы данных access tooyour предотвращает правило брандмауэра или tooits базы данных, пока вы не укажете какие компьютеры имеют разрешение. Ознакомьтесь со статьей [Правила брандмауэра сервера базы данных Azure для PostgreSQL](concepts-firewall-rules.md). |
|||

## <a name="how-do-i-manage-a-server"></a>Как управлять сервером?
Вы можете управлять базы данных Azure для hello PostgreSQL серверов с помощью портала Azure или hello [Azure CLI](/cli/azure/postgres).

## <a name="next-steps"></a>Дальнейшие действия
- Общие сведения о службе hello. в статье [базы данных Azure для обзора PostgreSQL](overview.md)
- Сведения о квотах и ограничениях для конкретных ресурсов с учетом вашего **уровня служб** представлены в статье [Уровни служб в базе данных Azure для MySQL](concepts-service-tiers.md).
- Сведения о подключении toohello службе см. в разделе [библиотеки подключений к базе данных Azure для PostgreSQL](concepts-connection-libraries.md).
