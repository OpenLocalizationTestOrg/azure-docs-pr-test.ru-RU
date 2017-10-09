---
title: "разделы aaaAll для службы хранилища данных SQL | Документы Microsoft"
description: "Таблица всех разделов по hello службы Azure имя хранилища данных SQL, которые существуют в http://azure.microsoft.com/documentation/articles/, заголовка и описания."
services: sql-data-warehouse
documentationcenter: 
author: barbkess
manager: jhubbard
editor: 
ms.assetid: a26a6dec-9c08-4415-8f58-4ee1dd41f718
ms.service: sql-data-warehouse
ms.workload: sql-data-warehouse
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: reference
ms.date: 03/30/2017
ms.author: barbkess
ms.openlocfilehash: 6f71d35b76b50764a5904525445675dafaa56b85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="all-topics-for-azure-sql-data-warehouse-service"></a>Все разделы о службе хранилища данных SQL Azure
В этом разделе перечислены каждый раздел, который применяется непосредственно toohello **хранилище данных SQL** службу Azure. Веб-страница для ключевых слов можно найти с помощью **Ctrl + F**, toofind hello вопросах, текущей.

## <a name="new"></a>Создать
| &nbsp; | Название | Описание |
| ---:|:--- |:--- |
| 1 |[Архивация хранилища данных SQL](sql-data-warehouse-backups.md) |Дополнительные сведения о резервных копиях встроенной базой данных хранилища данных SQL, позволяющих toorestore точку восстановления tooa хранилище данных SQL Azure или другом географическом регионе. |

## <a name="updated-articles-sql-data-warehouse"></a>Обновляемые статьи, хранилище данных SQL
В этом разделе перечислены статей, которые были недавно обновлены, когда обновлять hello велик или значительные. Для каждой статьи обновленные грубого фрагмент hello добавить текст разметки. Hello статьи были обновлены в диапазон дат hello **2016-08-22** слишком**2016-10-05**.

| &nbsp; | Статья | Обновленный текст, фрагмент | Дата обновления |
| ---:|:--- |:--- |:--- |
| 2 |[Загрузка данных из хранилища BLOB-объектов Azure в хранилище данных SQL (PolyBase)](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md) |/ tootrack байт и файлы ВЫБЕРИТЕ r.command, s.request_id, r.status, count (distinct input_name) как nbr_files, sum (s.bytes_processed) или 1024/1024 как gb_processed из sys.dm_pdw_exec_requests r внутреннее соединение sys.dm_pdw_dms_external_work s на r.request_id = s.request_id WHERE r. label  = 'CTAS : Load  cso . DimProduct  '  OR r. label  = 'CTAS : Load  cso . FactOnlineSales  ' GROUP BY  r.command,  s.request_id,  r.status ORDER BY  nbr_files desc,  gb_processed desc; |07.09.2016 |
| 3 |[Восстановление хранилища данных SQL](sql-data-warehouse-restore-database-overview.md) |** Можно восстановить в хранилище данных приостановлена? ** toorestore приостановленных хранилища данных требуется toofirst снова подключить его. После hello хранилища данных вернется в оперативный режим, вы сможете toochoose точек восстановления из семи дней. ** Восстановить tooa географически избыточная области ** при использовании географически избыточное хранилище hello можно восстановить hello данные хранилища tooyour парной ЦОД в разных географических регионах. хранилище данных Hello восстанавливается из резервной копии последней ежедневной hello. ** Восстановите временная шкала ** вы сможете восстановить точки восстановления tooany базы данных в пределах hello последних семи дней. Моментальные снимки запуск каждые четыре часа tooeight и доступны в течение семи дней. Если моментальный снимок старше семи дней, то срок его действия истекает и его точка восстановления перестает быть доступной. ** Для хранилища данных восстановлена hello оплачивается по тарифу хранилища Azure Premium hello восстановите затраты ** hello издержки хранения. Если навести на складе восстановленных данных взимается плата для хранилища по тарифу хранилища Azure Premium hello. Приостановка Hello преимущество состоит в вы не взимается |29.09.2016 |

## <a name="get-started"></a>Приступая к работе
| &nbsp; | Название | Описание |
| ---:|:--- |:--- |
| 4. |[Проверка подлинности tooAzure хранилище данных SQL](sql-data-warehouse-authentication.md) |Azure Active Directory (AAD) и SQL Server authentication tooAzure хранилище данных SQL. |
| 5 |[Рекомендации по использованию хранилища данных SQL Azure](sql-data-warehouse-best-practices.md) |Рекомендации, которые следует учитывать при разработке решений для хранилища данных SQL Azure. Они помогут вам обеспечить эффективную работу. |
| 6 |[Драйверы для хранилища данных SQL Azure](sql-data-warehouse-connection-strings.md) |Строки подключения и драйверы для хранилища данных SQL. |
| 7 |[Подключение tooAzure хранилище данных SQL](sql-data-warehouse-connect-overview.md) |Строка как имя сервера toofind hello и подключение для вашей tooAzure хранилище данных SQL |
| 8 |[Анализ данных с помощью машинного обучения Azure](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md) |Используйте машинного обучения Azure toobuild прогнозной модели машинного обучения на основе данных, хранимых в хранилище данных SQL Azure. |
| 9 |[Запросы к хранилищу данных SQL Azure (sqlcmd)](sql-data-warehouse-get-started-connect-sqlcmd.md) |Выполнение запросов хранилища данных SQL Azure с помощью служебной программы командной строки sqlcmd hello. |
| 10 |[Создание базы данных хранилища данных SQL с помощью Transact-SQL (TSQL)](sql-data-warehouse-get-started-create-database-tsql.md) |Узнайте, как toocreate Azure хранилище данных SQL с помощью TSQL |
| 11 |[Как билета toocreate технической поддержки для хранилища данных SQL](sql-data-warehouse-get-started-create-support-ticket.md) |Как toocreate поддержка билета в хранилище данных SQL Azure. |
| 12 |[Загрузка данных с помощью фабрики данных Azure](sql-data-warehouse-get-started-load-with-azure-data-factory.md) |Дополнительные сведения tooload данных с помощью фабрики данных Azure |
| 13. |[Загрузка данных в хранилище данных SQL с помощью PolyBase](sql-data-warehouse-get-started-load-with-polybase.md) |Сведения о возможностях PolyBase и как toouse его для сценариев хранилища данных. |
| 14 |[Создание хранилища данных SQL Azure](sql-data-warehouse-get-started-provision.md) |Узнайте, как toocreate в хранилище данных SQL Azure в hello портал Azure |
| 15 |[Создание хранилища данных SQL с помощью PowerShell](sql-data-warehouse-get-started-provision-powershell.md) |Создание хранилища данных SQL с помощью PowerShell |
| 16 |[Визуализация данных с помощью Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md) |Визуализация данных хранилища данных SQL с помощью Power BI |
| 17 |[Запросы к хранилищу данных SQL Azure (Visual Studio)](sql-data-warehouse-query-visual-studio.md) |Отправка запросов к хранилищу данных SQL с помощью Visual Studio. |

## <a name="develop"></a>Разработка
| &nbsp; | Название | Описание |
| ---:|:--- |:--- |
| 18 |[Оптимизация транзакций для хранилища данных SQL](sql-data-warehouse-develop-best-practices-transactions.md) |В этой статье вы найдете рекомендации по написанию эффективного кода для обновлений транзакций в хранилище данных SQL Azure. |
| 19 |[Управление параллелизмом и рабочей нагрузкой в хранилище данных SQL](sql-data-warehouse-develop-concurrency.md) |Общие сведения управлении параллелизмом и рабочей нагрузкой в хранилище данных SQL Azure для разработки решений. |
| 20 |[Функция Create Table As Select (CTAS) в хранилище данных SQL](sql-data-warehouse-develop-ctas.md) |Советы для создания кода с hello создание таблицы как select, инструкция (CTAS) в хранилище данных SQL Azure для разработки решений. |
| 21 |[Динамический SQL в хранилище данных SQL](sql-data-warehouse-develop-dynamic-sql.md) |Рекомендации по использованию динамического SQL в хранилище данных SQL для разработки решений. |
| 22 |[Группировка по параметрам в хранилище данных SQL](sql-data-warehouse-develop-group-by-options.md) |Советы по реализации параметров предложения Group By в хранилище данных SQL Azure для разработки решений. |
| 23 |[Использовать запросы tooinstrument метки в хранилище данных SQL](sql-data-warehouse-develop-label.md) |Советы по использованию метки tooinstrument запросов в хранилище данных SQL Azure для разработки решений. |
| 24 |[Циклы в хранилище данных SQL](sql-data-warehouse-develop-loops.md) |Рекомендации по применению циклов Transact-SQL и замене курсоров в хранилище данных SQL Azure для разработки решений. |
| 25 |[Хранимые процедуры в хранилище данных SQL](sql-data-warehouse-develop-stored-procedures.md) |Советы по реализации хранимых процедур в хранилище данных SQL Azure для разработки решений. |
| 26 |[Транзакции в хранилище данных SQL](sql-data-warehouse-develop-transactions.md) |Советы по реализации транзакций Transact-SQL в хранилище данных SQL Azure для разработки решений. |
| 27 |[Определяемые пользователем схемы в хранилище данных SQL](sql-data-warehouse-develop-user-defined-schemas.md) |Советы по использованию схем Transact-SQL в хранилище данных SQL Azure для разработки решений. |
| 28 |[Назначение переменных в хранилище данных SQL](sql-data-warehouse-develop-variable-assignment.md) |Советы по присваиванию значений переменных Transact-SQL в хранилище данных SQL Azure для разработки решений. |
| 29 |[Представления в хранилище данных SQL](sql-data-warehouse-develop-views.md) |Советы по использованию представлений Transact-SQL в хранилище данных SQL Azure для разработки решений. |
| 30 |[Проектные решения и методики программирования для хранилища данных SQL](sql-data-warehouse-overview-develop.md) |Основные понятия разработки, проектные решения, рекомендации и методики программирования для хранилища данных SQL. |

## <a name="manage"></a>Управление
| &nbsp; | Название | Описание |
| ---:|:--- |:--- |
| 31 |[Управление вычислительными ресурсами в хранилище данных SQL Azure (обзор)](sql-data-warehouse-manage-compute-overview.md) |Возможности масштабирования производительности в хранилище данных SQL Azure. Горизонтальное масштабирование, перемещая Dwu или приостанавливать и возобновлять toosave затраты вычислительных ресурсов. |
| 32 |[Управление вычислительными ресурсами в хранилище данных SQL Azure (портал Azure)](sql-data-warehouse-manage-compute-portal.md) |Задачи на портале Azure toomanage вычислительной мощности. Масштабирование вычислительных ресурсов путем изменения числа единиц DWU. Или, приостанавливать и возобновлять toosave затраты вычислительных ресурсов. |
| 33 |[Управление вычислительными ресурсами в хранилище данных SQL Azure (PowerShell)](sql-data-warehouse-manage-compute-powershell.md) |PowerShell задачи toomanage вычислительной мощности. Масштабирование вычислительных ресурсов путем изменения числа единиц DWU. Или, приостанавливать и возобновлять toosave затраты вычислительных ресурсов. |
| 34 |[Управление вычислительными ресурсами в хранилище данных SQL Azure (REST)](sql-data-warehouse-manage-compute-rest-api.md) |PowerShell задачи toomanage вычислительной мощности. Масштабирование вычислительных ресурсов путем изменения числа единиц DWU. Или, приостанавливать и возобновлять toosave затраты вычислительных ресурсов. |
| 35 |[Управление вычислительными ресурсами в хранилище данных SQL (T-SQL)](sql-data-warehouse-manage-compute-tsql.md) |Transact-SQL (T-SQL) задачи tooscale производительности путем настройки Dwu. Сокращение затрат путем свертывания ресурсов в периоды низкой загрузки. |
| 36 |[Мониторинг рабочей нагрузки с помощью динамических административных представлений](sql-data-warehouse-manage-monitor.md) |Узнайте, как toomonitor рабочей нагрузки с помощью динамических административных представлений. |
| 37 |[Управление базами данных в хранилище данных SQL Azure](sql-data-warehouse-overview-manage.md) |Общие сведения об управлении базами данных в хранилище данных SQL. Рассматриваются средства управления, динамические административные представления и масштабирование производительности, устранение неполадок с запросами, создание надлежащих политик безопасности и восстановление базы данных после повреждения данных или регионального сбоя. |
| 38 |[Мониторинг запросов пользователей в хранилище данных SQL Azure](sql-data-warehouse-overview-manage-user-queries.md) |Общие сведения о hello вопросы, рекомендации и задачи для отслеживания запросов пользователя в хранилище данных SQL Azure |
| 11,9 |[Восстановление хранилища данных SQL](sql-data-warehouse-restore-database-overview.md) |Общие сведения о параметрах восстановления hello базы данных для восстановления базы данных в хранилище данных SQL Azure. |
| 40 |[Восстановление хранилища данных SQL Azure (портал)](sql-data-warehouse-restore-database-portal.md) |Задачи портала Azure для восстановления хранилища данных SQL. |
| 41 |[Восстановление хранилища данных SQL Azure (PowerShell)](sql-data-warehouse-restore-database-powershell.md) |Задачи PowerShell для восстановления хранилища данных SQL. |
| 42 |[Восстановление хранилища данных SQL Azure (REST API)](sql-data-warehouse-restore-database-rest-api.md) |Задачи REST API для восстановления хранилища данных SQL. |

## <a name="tables-and-indexes"></a>Таблицы и индексы
| &nbsp; | Название | Описание |
| ---:|:--- |:--- |
| 43 |[Типы данных таблиц в хранилище данных SQL](sql-data-warehouse-tables-data-types.md) |Начало работы с типами данных таблиц хранилища данных SQL Azure. |
| 44 |[Распределение таблиц в хранилище данных SQL](sql-data-warehouse-tables-distribute.md) |Начало работы с распределением таблиц в хранилище данных SQL Azure. |
| 45 |[Индексирование таблиц в хранилище данных SQL](sql-data-warehouse-tables-index.md) |Начало работы с индексированием таблиц в хранилище данных SQL Azure. |
| 46 |[Общие сведения о таблицах в хранилище данных SQL](sql-data-warehouse-tables-overview.md) |Начало работы с таблицами хранилища данных SQL Azure. |
| 47 |[Секционирование таблиц в хранилище данных SQL](sql-data-warehouse-tables-partition.md) |Начало работы с секционированием таблиц в хранилище данных SQL Azure. |
| 48 |[Управление статистикой таблиц в хранилище данных SQL](sql-data-warehouse-tables-statistics.md) |Начало работы со статистикой таблиц в хранилище данных SQL Azure. |
| 49 |[Временные таблицы в хранилище данных SQL](sql-data-warehouse-tables-temporary.md) |Начало работы с временными таблицами в хранилище данных SQL Azure. |

## <a name="integrate"></a>Интеграция
| &nbsp; | Название | Описание |
| ---:|:--- |:--- |
| 50 |[Работа с фабрикой данных Azure и хранилищем данных SQL](sql-data-warehouse-integrate-azure-data-factory.md) |Советы по использованию фабрики данных Azure (ADF) с хранилищем данных SQL для разработки решений. |
| 51 |[Использование машинного обучения Azure с хранилищем данных SQL](sql-data-warehouse-integrate-azure-machine-learning.md) |Учебник по использованию машинного обучения Azure с хранилищем данных SQL Azure для разработки решений. |
| 52 |[Работа со службой Azure Stream Analytics и хранилищем данных SQL](sql-data-warehouse-integrate-azure-stream-analytics.md) |Советы по использованию службы Azure Stream Analytics и хранилища данных SQL для разработки решений. |
| 53 |[Использование Power BI с хранилищем данных SQL](sql-data-warehouse-integrate-power-bi.md) |Советы по использованию Power BI с хранилищем данных SQL Azure для разработки решений. |
| 54 |[Интеграция других служб с хранилищем данных SQL](sql-data-warehouse-overview-integrate.md) |Инструменты и партнерские решения, которые интегрируются с хранилищем данных SQL |

## <a name="load"></a>загрузить
| &nbsp; | Название | Описание |
| ---:|:--- |:--- |
| 55 |[Загрузка данных из хранилища больших двоичных объектов Azure в хранилище данных SQL Azure (фабрика данных Azure).](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md) |Дополнительные сведения tooload данных с помощью фабрики данных Azure |
| 56 |[Загрузка данных из хранилища BLOB-объектов Azure в хранилище данных SQL (PolyBase)](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md) |Узнайте, как данные tooload toouse PolyBase из Azure хранилище больших двоичных объектов в хранилище данных SQL. Загрузить несколько таблиц из открытых данных в схему хранилища данных Contoso Retail hello. |
| 57 |[Загрузка данных из SQL Server в хранилище данных SQL Azure (AZCopy)](sql-data-warehouse-load-from-sql-server-with-azcopy.md) |Использует данные bcp tooexport tooflat файлов и SQL Server, хранилище больших двоичных объектов tooAzure данных tooimport AZCopy, PolyBase tooingest hello данных в хранилище данных SQL Azure. |
| 58 |[Загрузка данных из SQL Server в хранилище данных SQL Azure (неструктурированные файлы)](sql-data-warehouse-load-from-sql-server-with-bcp.md) |Для данных небольшого объема использует bcp tooexport данные из файлов tooflat SQL Server и импортировать hello данные непосредственно в хранилище данных SQL Azure. |
| 59 |[Загрузка данных из SQL Server в хранилище данных SQL Azure (SSIS)](sql-data-warehouse-load-from-sql-server-with-integration-services.md) |Показывает, как toocreate toomove данные пакета служб SQL Server Integration Services (SSIS) из самых разнообразных данных источники tooSQL хранилища данных. |
| 60 |[Загрузка данных в хранилище данных SQL с помощью PolyBase](sql-data-warehouse-load-from-sql-server-with-polybase.md) |Использует данные bcp tooexport tooflat файлов и SQL Server, хранилище больших двоичных объектов tooAzure данных tooimport AZCopy, PolyBase tooingest hello данных в хранилище данных SQL Azure. |
| 61 |[Руководство по использованию PolyBase в хранилище данных SQL](sql-data-warehouse-load-polybase-guide.md) |Правила и рекомендации по использованию PolyBase в сценариях с хранилищем данных SQL. |
| 62 |[Загрузка образца данных в хранилище данных SQL](sql-data-warehouse-load-sample-databases.md) |Загрузка образца данных в хранилище данных SQL |
| 63 |[Загрузка данных с помощью bcp](sql-data-warehouse-load-with-bcp.md) |Узнать, какие bcp и как toouse его для сценариев хранилища данных. |
| 64 |[Загрузка данных в хранилище данных Azure SQL](sql-data-warehouse-overview-load.md) |Узнайте hello распространенные сценарии загрузку данных в хранилище данных SQL. Они включают использование PolyBase, хранилища BLOB-объектов Azure, неструктурированных файлов и доставки диска. Кроме того, можно использовать сторонние средства. |

## <a name="migrate"></a>Миграция
| &nbsp; | Название | Описание |
| ---:|:--- |:--- |
| 65 |[Перенос вашей tooSQL кода SQL хранилища данных](sql-data-warehouse-migrate-code.md) |Советы по миграции SQL кода tooAzure хранилище данных SQL для разработки решений. |
| 66 |[Перенос данных](sql-data-warehouse-migrate-data.md) |Советы по переносу вашей tooAzure данных хранилища данных SQL для разработки решений. |
| 67 |[Служебная программа для миграции в хранилище данных (предварительная версия)](sql-data-warehouse-migrate-migration-utility.md) |Перенос tooSQL хранилища данных. |
| 68 |[Перенос вашей tooSQL схемы хранилища данных](sql-data-warehouse-migrate-schema.md) |Советы по переносу tooAzure вашей схемы хранилища данных SQL для разработки решений. |
| 69 |[Перенос tooSQL вашего решения хранилища данных](sql-data-warehouse-overview-migrate.md) |Руководство по миграции для переноса вашей платформы решения tooAzure хранилище данных SQL. |

## <a name="partners"></a>Партнеры
| &nbsp; | Название | Описание |
| ---:|:--- |:--- |
| 70 |[Партнеры по бизнес-аналитике хранилища данных SQL](sql-data-warehouse-partner-business-intelligence.md) |Содержит список сторонних партнерских решений для бизнес-аналитики с поддержкой хранилища данных SQL. |
| 71 |[Партнеры по интеграции данных хранилища данных SQL](sql-data-warehouse-partner-data-integration.md) |Содержит список сторонних партнерских решений для интеграции данных с поддержкой хранилища данных SQL Azure. |
| 72 |[Партнеры по управлению данными хранилища данных SQL](sql-data-warehouse-partner-data-management.md) |Содержит список сторонних партнерских решений для перемещения данных с поддержкой хранилища данных SQL. |

## <a name="reference"></a>Справочные материалы
| &nbsp; | Название | Описание |
| ---:|:--- |:--- |
| 73 |[Справочные темы по хранилищу данных SQL](sql-data-warehouse-overview-reference.md) |Ссылки на статьи, содержащие справочную информацию о хранилище данных SQL. |
| 74 |[Использование командлетов PowerShell и интерфейсов REST API при работе с хранилищем данных SQL](sql-data-warehouse-reference-powershell-cmdlets.md) |Найти hello top командлеты PowerShell для хранилища данных SQL Azure включая то, как toopause и возобновление базы данных. |
| 75 |[Элементы языка](sql-data-warehouse-reference-tsql-language-elements.md) |Список ссылок tooreference содержимого элементов языка Transact-SQL hello, используемый для хранилища данных SQL. |
| 76 |[Темы, связанные с языком Transact-SQL](sql-data-warehouse-reference-tsql-statements.md) |Ссылки tooreference содержимое разделов hello Transact-SQL, используемых в хранилище данных SQL. |
| 77 |[Системные представления](sql-data-warehouse-reference-tsql-system-views.md) |Содержимое представления toosystem ссылки для хранилища данных SQL. |

## <a name="security"></a>Безопасность
| &nbsp; | Название | Описание |
| ---:|:--- |:--- |
| 78 |[Хранилище данных SQL. Поддержка клиентов прежних версий для аудита и динамического маскирования данных](sql-data-warehouse-auditing-downlevel-clients.md) |Сведения о поддержке клиентов прежних версий хранилища данных SQL для аудита данных |
| 79 |[Аудит в хранилище данных SQL Azure](sql-data-warehouse-auditing-overview.md) |Приступая к работе с аудитом в хранилище данных SQL Azure |
| 80 |[Начало работы с прозрачным шифрованием данных (TDE) в хранилище данных SQL](sql-data-warehouse-encryption-tde.md) |Прозрачное шифрование данных в хранилище данных SQL на портале |
| 81 |[Начало работы с прозрачным шифрованием данных (TDE)](sql-data-warehouse-encryption-tde-tsql.md) |Прозрачное шифрование данных в хранилище данных SQL (T-SQL) |
| 82 |[Защита базы данных в хранилище данных SQL](sql-data-warehouse-overview-manage-security.md) |Советы по защите базы данных в хранилище данных SQL для разработки решений. |

## <a name="miscellaneous"></a>Разное
| &nbsp; | Название | Описание |
| ---:|:--- |:--- |
| 83 |[Установка Visual Studio и SSDT для хранилища данных SQL](sql-data-warehouse-install-visual-studio.md) |Установка Visual Studio и SQL Server Data Tools (SSDT) для хранилища данных SQL Azure. |
| 84 |[Миграция tooPremium сведения о хранилище](sql-data-warehouse-migrate-to-premium-storage.md) |Инструкции по переносу существующего хранилища toopremium хранилище данных SQL |
| 85 |[Приступая к работе с системой обнаружения угроз](sql-data-warehouse-security-threat-detection.md) |Как tooget запущена с обнаружением угроз |
| 86 |[Ограничения емкости хранилища данных SQL](sql-data-warehouse-service-capacity-limits.md) |Максимальные значения для подключений, баз данных, таблиц и запросов для хранилища данных SQL. |
| 87 |[Устранение неполадок хранилища данных SQL Azure](sql-data-warehouse-troubleshoot.md) |Диагностика и устранение неполадок хранилища данных SQL Azure. |

