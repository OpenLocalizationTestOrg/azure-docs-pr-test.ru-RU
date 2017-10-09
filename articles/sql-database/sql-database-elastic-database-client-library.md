---
title: "базы данных масштабируемых облачных aaaBuilding | Документы Microsoft"
description: "Создание масштабируемых приложений .NET базы данных с помощью клиентской библиотеки hello эластичной базы данных"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 1f11c52d-13c1-4994-b9b1-5b1ae2f9255f
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: ddove
ms.openlocfilehash: ca34eff2078c0700dee1bc587f264bbfca979eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="building-scalable-cloud-databases"></a>Создание масштабируемых облачных баз данных
Масштабирование баз данных можно легко выполнить с помощью средств и функций масштабирования для базы данных SQL Azure. В частности, можно использовать hello **клиентской библиотеке эластичной базы данных** toocreate и управление базами данных с горизонтальным масштабированием. Она позволяет легко разрабатывать сегментированные приложения с сотнями — или даже тысячами — баз данных SQL Azure. [Эластичный задания](sql-database-elastic-jobs-powershell.md) затем можно облегчить управление используется toohelp этих баз данных.

Библиотека tooinstall hello, перейдите в слишком[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/). 

## <a name="documentation"></a>Документация
1. [Приступая к работе с инструментами эластичных баз данных](sql-database-elastic-scale-get-started.md)
2. [Функции эластичных баз данных](sql-database-elastic-scale-introduction.md)
3. [Управление размещением сегментов](sql-database-elastic-scale-shard-map-management.md)
4. [Миграция существующих баз данных tooscale масштабированием](sql-database-elastic-convert-to-use-elastic-tools.md)
5. [Маршрутизация, зависящая от данных](sql-database-elastic-scale-data-dependent-routing.md)
6. [Запросы к нескольким сегментам](sql-database-elastic-scale-multishard-querying.md)
7. [Добавление сегмента с использованием средств эластичных баз данных](sql-database-elastic-scale-add-a-shard.md)
8. [Мультитенантные приложения со средствами эластичных баз данных и безопасностью на уровне строк](sql-database-elastic-tools-multi-tenant-row-level-security.md)
9. [Обновление библиотеки клиентских приложений](sql-database-elastic-scale-upgrade-client-library.md) 
10. [Обзор эластичных запросов](sql-database-elastic-query-overview.md)
11. [Глоссарий по средствам работы с эластичными базами данных](sql-database-elastic-scale-glossary.md)
12. [Использование клиентской библиотеки эластичных баз данных с Entity Framework](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md)
13. [Использование клиентской библиотеки эластичной базы данных с Dapper](sql-database-elastic-scale-working-with-dapper.md)
14. [Средство разбиения и слияния](sql-database-elastic-scale-overview-split-and-merge.md)
15. [Счетчики производительности для диспетчера карты сегментов](sql-database-elastic-database-client-library.md) 
16. [Часто задаваемые вопросы об инструментах эластичных баз данных](sql-database-elastic-scale-faq.md)

## <a name="client-capabilities"></a>Возможности клиента
Горизонтальное масштабирование приложений с помощью *сегментирования* представляет трудности для разработчиков hello как, так и Здравствуйте, администратор. Hello клиентская библиотека упрощает задачи по управлению hello, предоставляя средства, которые позволяют разработчикам оба и Администраторы управляют масштабируемых баз данных. Типичный пример существует много баз данных, известных как «сегменты» toomanage. Клиенты расположены в hello одной базе данных, и существует одна база данных каждого клиента (схему одного клиента). Hello клиентская библиотека включает следующие возможности.

- **Управление карты сегментов**: специальные база данных с именем «диспетчера карты сегментов» hello. Управление карты сегментов — способность hello метаданные toomanage приложение по его сегментов. Разработчики могут использовать в качестве сегментов баз данных tooregister этой функции, описываются сопоставления ключей отдельных сегментирования или баз данных toothose диапазонов ключей и поддерживать эти метаданные, сколько hello и изменения емкости tooreflect развития композиции баз данных. Библиотека клиента hello эластичной базы данных потребовалось бы toospend много времени, написание кода hello управления при реализации сегментирования. Дополнительные сведения см. в статье [Развертывание баз данных с использованием диспетчера карты сегментов](sql-database-elastic-scale-shard-map-management.md).

- **Управляемой данными маршрутизацией**: представьте запросов, поступающих в приложение hello. В зависимости от значения ключа сегментирования hello запроса hello hello приложению toodetermine hello правильный базы данных на основе hello значения ключа. После этого он открывает соединения toohello запроса к базе данных tooprocess hello. Управляемой данными маршрутизацией предоставляет возможность hello tooopen подключений в одном вызове легко в карте сегментов hello приложения hello. Управляемой данными маршрутизацией был другой области код инфраструктуры, который закрывается по функциональным возможностям в клиентской библиотеке эластичной базы данных hello. Дополнительные сведения см. в статье [Маршрутизация, зависящая от данных](sql-database-elastic-scale-data-dependent-routing.md).
- **Многосегментные запросы (MSQ).** Многосегментное формирование запросов применяется в том случае, когда запрос относится к нескольким (или всем) сегментам. Запрос нескольких сегментов выполняет hello же код T-SQL для всех сегментов или набор сегментов. результаты Hello hello участия сегментов объединяются в общий результат, заданные с помощью семантики UNION ALL. Hello функциональные возможности, предоставляемые через клиентскую библиотеку hello обрабатывает многие задачи, включая: управление соединениями, управление потоками, обработки ошибок и обработки промежуточных результатов. MSQ можно запрашивать вверх toohundreds сегментов. Дополнительные сведения см. в статье [Многосегментное формирование запросов](sql-database-elastic-scale-multishard-querying.md).

В общем случае клиенты, использующие средства эластичной базы данных может ожидать tooget полной функциональности T-SQL при отправке сегментов локальной операции в виде операций противоположность toocross сегментов, которые имеют свои собственные семантики.

## <a name="next-steps"></a>Дальнейшие действия
Повторите hello [пример приложения](sql-database-elastic-scale-get-started.md) с демонстрацией hello клиентских функций. 

Библиотека tooinstall hello, перейдите в слишком[клиентской библиотеке эластичной базы данных](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).

Инструкции по использованию средства hello разделения слияния, см. в разделе hello [Общие сведения о средстве разбиения слияния](sql-database-elastic-scale-overview-split-and-merge.md).

[Теперь исходный код клиентской библиотеки эластичной базы данных является открытым!](https://azure.microsoft.com/blog/elastic-database-client-library-is-now-open-sourced/)

Используйте [запросы к эластичной БД](sql-database-elastic-query-overview.md).

Hello библиотека доступна как по открытым исходным кодом на [GitHub](https://github.com/Azure/elastic-db-tools). 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->
[1]:./media/sql-database-elastic-database-client-library/glossary.png

