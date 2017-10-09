---
title: "Обзор разработки приложений баз данных aaaSQL | Документы Microsoft"
description: "Дополнительные сведения о доступности подключения библиотеки и рекомендации для приложений, соединяющихся tooSQL базы данных."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: genemi
ms.assetid: 67c02204-d1bd-4622-acce-92115a7cde03
ms.service: sql-database
ms.custom: develop apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: sstein
ms.openlocfilehash: 17f04db600828f90c42c750c9abdb92cfa4ca817
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sql-database-application-development-overview"></a>Обзор разработки приложений базы данных SQL
В этой статье рассматриваются hello основные вопросы, которые разработчик следует учитывать при написании кода tooconnect tooAzure базы данных SQL.

> [!TIP]
> Отображение учебника, toocreate server, создать брандмауэр на основе сервера, просмотр свойств сервера, подключитесь с помощью SQL Server Management Studio, запрос базы данных master hello, Создание образца базы данных и новая база данных, запрашивать свойства базы данных, подключения с помощью SQL Server Management Studio и образец hello запрос к базе данных, в разделе [получить учебник работы](sql-database-get-started-portal.md).
>

## <a name="language-and-platform"></a>Язык и платформа
Доступны примеры кода на разных языках программирования и для разных платформ. Можно найти примеры кода toohello ссылки на: 

* Дополнительные сведения: [Библиотеки подключений для базы данных SQL и SQL Server](sql-database-libraries.md)

## <a name="tools"></a>Средства 
Вы можете использовать инструменты с открытым кодом, такие как [cheetah](https://github.com/wunderlist/cheetah), [sql-cli](https://www.npmjs.com/package/sql-cli) и [VS Code](https://code.visualstudio.com/). Кроме того, база данных SQL Azure поддерживает инструменты Майкрософт, например [Visual Studio](https://www.visualstudio.com/downloads/) и [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx).  Можно также использовать hello портала управления Azure PowerShell, и API-интерфейс REST позволяют получить дополнительную производительность.

## <a name="resource-limitations"></a>Ограничения ресурсов
База данных SQL Azure управляет hello ресурсах tooa доступны в базе данных с помощью двух разных механизмов: управление ресурсами и принудительного применения ограничения.

* Дополнительные сведения: [Ограничения ресурсов базы данных SQL Azure](sql-database-resource-limits.md)

## <a name="security"></a>Безопасность
База данных SQL Azure предоставляет ресурсы для ограничения доступа, защиты данных и мониторинга действий в базе данных SQL.

* Дополнительные сведения: [Защита базы данных SQL](sql-database-security-overview.md)

## <a name="authentication"></a>Аутентификация
* База данных SQL Azure поддерживает пользователей и имена для входа аутентификации SQL Server, а также пользователей и имена для входа [аутентификации Azure Active Directory](sql-database-aad-authentication.md) .
* Требуется toospecify определенной базе данных, а не по умолчанию toohello *master* базы данных.
* Нельзя использовать hello Transact-SQL **используйте имяБазыДанных;** инструкцию в базе данных tooanother tooswitch базы данных SQL.
* More information: [Безопасность баз данных SQL: управление доступом к базе данных и защита входа в систему](sql-database-manage-logins.md)

## <a name="resiliency"></a>Устойчивость
В случае временная ошибка при подключении базы данных tooSQL кода следует повторить вызов hello.  Рекомендуется логика повторных попыток использовать логики отсрочки, чтобы он не перегрузки hello базы данных SQL с повтором одновременно несколькими клиентами.

* Примеры кода: образцы кода, иллюстрирующие логику повторных попыток, в разделе примеров для hello язык в: [библиотеки подключений к базе данных SQL и SQL Server](sql-database-libraries.md)
* More information: [Сообщения об ошибках для клиентских программ базы данных SQL](sql-database-develop-error-messages.md)

## <a name="managing-connections"></a>Управление подключениями
* В логике подключения клиента переопределите toobe время ожидания по умолчанию hello 30 секунд.  по умолчанию Hello 15 секунд — слишком мало для подключений, которые зависят от hello Интернета.
* При использовании [пул соединений](http://msdn.microsoft.com/library/8xx3tyca.aspx), что tooclose hello подключения hello мгновенных программа, не использует активно его и не выполняет подготовку tooreuse его.

## <a name="network-considerations"></a>Рекомендации относительно сети
* На компьютере hello, на котором размещается клиентская программа убедитесь, что hello брандмауэр разрешает исходящие соединения TCP на порту 1433.  More information: [Практическое руководство. Настройка брандмауэра базы данных SQL Azure с помощью портала Azure](sql-database-configure-firewall-settings.md)
* Если клиентская программа подключается tooSQL базы данных, пока клиент работает на виртуальной машине Azure (ВМ), необходимо открыть определенные диапазоны портов на hello виртуальной Машины. Дополнительные сведения см. в статье [Порты для ADO.NET 4.5, отличные от порта 1433](sql-database-develop-direct-route-ports-adonet-v12.md).
* Иногда tooAzure клиентских подключений базы данных SQL использование прокси-сервера hello и взаимодействовать непосредственно с базой данных hello. Порты, отличные от 1433, становятся важными. Дополнительные сведения см. в статьях [Архитектура подключений к базе данных SQL Azure](sql-database-connectivity-architecture.md) и [Порты для ADO.NET 4.5, отличные от порта 1433](sql-database-develop-direct-route-ports-adonet-v12.md).

## <a name="data-sharding-with-elastic-scale"></a>Сегментирование данных с помощью эластичного масштабирования
Гибкое масштабирование упрощает процесс hello масштабирования out (/). 

* [Шаблоны разработки для мультитенантных приложений SaaS с использованием базы данных Azure SQL](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* [Маршрутизация, зависящая от данных](sql-database-elastic-scale-data-dependent-routing.md)
* [Начало работы с эластичным масштабированием базы данных SQL Azure (предварительная версия)](sql-database-elastic-scale-get-started.md)

## <a name="next-steps"></a>Дальнейшие действия
Просмотр всех hello [возможностей базы данных SQL](sql-database-technical-overview.md)
