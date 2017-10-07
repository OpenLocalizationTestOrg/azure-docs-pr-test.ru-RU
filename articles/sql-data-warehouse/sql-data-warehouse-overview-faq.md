---
title: "aaaAzure SQL данные хранилища часто задаваемые вопросы | Документы Microsoft"
description: "В этой статье собраны вопросы о хранилище данных SQL Azure, часто задаваемые пользователями и разработчиками."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: 812CA525-3BF3-49DF-8DF3-FB4342464F4F
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: overview
ms.date: 3/1/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: 09fd3f65d9507b09fcb8f477742c7d020add2755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-frequently-asked-questions"></a>Часто задаваемые вопросы о хранилище данных SQL

## <a name="general"></a>Общие сведения

В. Какие возможности защиты данных предлагаются в хранилище данных SQL?

О. Хранилище данных SQL предлагает несколько решений для защиты данных, таких как прозрачное шифрование данных (TDE) и аудит. Дополнительные сведения см. в статье [Безопасность].

В. Где можно выяснить, каким правовым нормам или бизнес-стандартам соответствует хранилище данных SQL?

О. Посетите hello [соответствия Microsoft] страницы для различных предложений соответствия по продукту, например SOC и ISO. Сначала выберите соответствия наименования, а затем разверните Azure hello корпорации Майкрософт в области облачных служб hello правой стороны из раздела toosee страницы приветствия список служб, служб Azure являются совместимыми.

В. Можно ли подключить PowerBI?

О. Да! Служба PowerBI поддерживает прямые запросы, выполняемые из хранилища данных SQL, но она не предназначена для большого количества пользователей или данных в режиме реального времени. В рабочей среде PowerBI рекомендуется использовать службу PowerBI поверх служб Azure Analysis Services или Analysis Service IaaS. 

В. Какие ограничения емкости имеет хранилище данных SQL?

О. Текущие ограничения см. на странице [Ограничения емкости хранилища данных SQL]. 

В. Почему операция масштабирования, приостановки или возобновления занимает так много времени?

О. Ряд факторов может влиять на время hello для вычислительных операций управления. Как правило, продолжительность операций обусловлена откатом транзакций. При инициации операции масштабирования или приостановки блокируются все входящие сеансы, и запросы утрачиваются. В системе hello tooleave заказа в стабильном состоянии транзакции должен быть выполнен до может начаться операция. Здравствуйте, количество больше hello и больший размер hello журнала транзакций, hello дольше hello операции будут остановлены восстановление hello системы tooa стабильного состояния.

## <a name="user-support"></a>Поддержка пользователей

В. Куда я могу отправить свой запрос на функцию?

О. Если у вас есть запрос на функцию, отправьте его на нашей странице [UserVoice].

В. Как я могу разрабатывать свои решения?

О. Для получения помощи при разработке с помощью хранилища данных SQL задайте свои вопросы на нашей странице [Stack Overflow]. 

В. Как отправить запрос в службу поддержки?

О. [Запросы в службу поддержки] можно отправить на портале Azure.

## <a name="sql-languagefeature-support"></a>Поддержка языка или функций SQL 

В. Какие типы данных поддерживает хранилище данных SQL?

О. Типы данных, поддерживаемые хранилищем данных SQL, перечислены [здесь].

В. Какие функции таблиц поддерживаются?

О. Хранилище данных SQL поддерживает множество функций, а те немногие функции, которые не поддерживаются, перечислены в разделе [Неподдерживаемые функции таблиц].

## <a name="tooling-and-administration"></a>Инструментарий и администрирование

В. Поддерживается ли создание проектов Базы данных в Visual Studio?

О. В настоящее время создание в Visual Studio проектов Базы данных для хранилища данных SQL не поддерживается. Если вы хотите toocast tooget голос эту возможность, посетите наш User Voice [проекты базы данных компонентов запроса].

В. Поддерживает ли хранилище данных SQL интерфейсы REST API?

О. Да. Большинство функции REST, которые могут использоваться в Базе данных SQL, также доступны в хранилище данных SQL. Сведения об API можно найти в документации REST или на сайте [MSDN].


## <a name="loading"></a>Загрузка

В. Какие драйверы клиента поддерживаются?

О. Поддержка драйверов для хранилища данных можно найти на hello [строки подключения] страницы

В. Какие форматы файлов поддерживает PolyBase при работе с хранилищем данных SQL?

О. Orc, RC, Parquet и неструктурированный текст с разделителями.

Вопрос. что можно подключиться с помощью PolyBase хранилища данных SQL toofrom? 

О. К [Azure Data Lake Store] и [большим двоичным объектам службы хранилища Azure].

Вопрос. есть вычисление pushdown возможно при подключении tooAzure хранилища больших двоичных объектов или ADLS? 

Ответ PolyBase хранилища данных SQL, нет, взаимодействует только компоненты хранения hello. 

Вопрос. можно ли подключиться tooHDI?

Ответ HDI можно использовать ADLS или WASB как слой HDFS hello. Если одна из этих служб используется в качестве уровня HDFS, то можно загрузить данные в хранилище данных SQL. Тем не менее не удается создать экземпляр HDI toohello вычисление pushdown. 

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о хранилище данных SQL в целом см. на [этой странице].


<!-- Article references -->
[UserVoice]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[строки подключения]: ./sql-data-warehouse-connection-strings.md
[Stack Overflow]: http://stackoverflow.com/questions/tagged/azure-sqldw
[Запросы в службу поддержки]: ./sql-data-warehouse-get-started-create-support-ticket.md
[Безопасность]: ./sql-data-warehouse-overview-manage-security.md
[соответствия Microsoft]: https://www.microsoft.com/en-us/trustcenter/compliance/complianceofferings
[Ограничения емкости хранилища данных SQL]: ./sql-data-warehouse-service-capacity-limits.md
[здесь]: ./sql-data-warehouse-tables-data-types.md
[Неподдерживаемые функции таблиц]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[Azure Data Lake Store]: ./sql-data-warehouse-load-from-azure-data-lake-store.md
[большим двоичным объектам службы хранилища Azure]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[проекты базы данных компонентов запроса]: https://feedback.azure.com/forums/307516-sql-data-warehouse/suggestions/13313247-database-project-from-visual-studio-to-support-azu
[MSDN]: https://msdn.microsoft.com/en-us/library/azure/mt163685.aspx
[этой странице]: ./sql-data-warehouse-overview-faq.md