---
title: "tooan aaaMove данных базы данных SQL Azure для машинного обучения Azure | Документы Microsoft"
description: "Создать таблицу SQL и загрузить tooSQL данных таблицы"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 50f8b862-4d32-44b2-a1e2-4fbc8024acaa
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: b33ef836f42c17a56794baf763281e9998b16bef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooan-azure-sql-database-for-azure-machine-learning"></a>Перемещение данных tooan базы данных SQL Azure для машинного обучения Azure
В этом разделе описаны параметры hello для перемещения данных из неструктурированных файлов (форматы CSV или TSV) или из данных, хранящихся в базе данных Azure SQL tooan в локальной среде SQL Server. Эти задачи для облака toohello перемещение данных являются частью hello командного процесса обработки и анализа данных.

Раздел, описывающий параметры hello tooan перемещение данных в локальной среде SQL Server для машинного обучения см. в разделе [перемещение данных tooSQL Server на виртуальной машине Azure](machine-learning-data-science-move-sql-server-virtual-machine.md).

следующие Hello **меню** связывает tootopics, описывающие, каким образом данные tooingest в целевых средах, где hello данные могут храниться и обрабатываться во время hello процесса обработки и анализа данных Team (TDSP).

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

Hello следующей таблице перечислены параметры hello tooan перемещения данных базы данных SQL Azure.

| <b>ИСТОЧНИК</b> | <b>Назначение: база данных SQL Azure</b> |
| --- | --- |
| <b>Неструктурированный файл (в формате CSV или TSV)</b> |<a href="#bulk-insert-sql-query">SQL-запрос на массовую вставку |
| <b>Локальный сервер SQL Server</b> |1. <a href="#export-flat-file">Экспорт файла tooFlat<br> 2. <a href="#insert-tables-bcp">Мастер миграции баз данных SQL<br> 3. <a href="#db-migration">Архивация и восстановление базы данных<br> 4. <a href="#adf"> Фабрика данных Azure |

## <a name="prereqs"></a>Предварительные требования
Приведенные ниже процедуры Hello требуют наличия:

* **Подписка Azure**. Если у вас нет подписки, вы можете зарегистрироваться для получения [бесплатной пробной версии](https://azure.microsoft.com/pricing/free-trial/).
* **Azure storage account**. Использовать учетную запись хранилища Azure для хранения данных hello в этом учебнике. При отсутствии учетной записи хранилища Azure в разделе hello [создать учетную запись хранилища](../storage/common/storage-create-storage-account.md#create-a-storage-account) статьи. После создания учетной записи хранилища hello необходимо tooobtain hello от имени учетной записи хранилища hello tooaccess использования ключа. Ознакомьтесь с разделом [Управление ключами доступа к хранилищу](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).
* Доступ tooan **базы данных SQL Azure**. Если необходимо настроить базы данных SQL Azure, [Приступая к работе с базой данных SQL Microsoft Azure](../sql-database/sql-database-get-started.md) предоставляет сведения о том, как tooprovision новый экземпляр базы данных SQL Azure.
* Установленная и настроенная локальная среда **Azure PowerShell**. Инструкции см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).

**Данные**: демонстрируются hello миграции процессов с помощью hello [NYC такси dataset](http://chriswhong.com/open-data/foil_nyc_taxi/). Hello такси NYC набор данных содержит сведения о данных маршрута и выставки и доступен в хранилище больших двоичных объектов: [NYC такси данных](http://www.andresmh.com/nyctaxitrips/). Пример и описание этих файлов приведены в [описании набора данных «Поездки такси Нью-Йорка»](machine-learning-data-science-process-sql-walkthrough.md#dataset).

Можно адаптировать hello процедуры описанных здесь tooa набор данных или действуйте hello, как описано с помощью hello такси NYC набора данных. hello tooupload такси NYC набора данных в базу данных SQL Server в локальной среде, выполните процедуру hello, описанные в [массового импорта данных в базу данных SQL Server](machine-learning-data-science-process-sql-walkthrough.md#dbload). Эти инструкции относятся к SQL Server на виртуальной машине Azure, но hello процедур для передачи toohello находится на локальном сервере SQL Server hello таким же.

## <a name="file-to-azure-sql-database"></a>Перемещение данных из источника неструктурированного файла tooan базы данных Azure SQL
Данные в неструктурированные файлы (CSV или TSV в формате) могут быть tooan перемещенной базы данных Azure SQL с помощью Bulk Insert SQL-запроса.

### <a name="bulk-insert-sql-query"></a>SQL-запрос на массовую вставку
Hello hello процедурой hello массовой вставки запроса выполняется аналогично toothose, описаны в разделах hello для переноса данных из неструктурированного файла источника tooSQL Server на Виртуальной машине Azure. Дополнительные сведения см. в разделе [SQL-запрос на массовую вставку](machine-learning-data-science-move-sql-server-virtual-machine.md#insert-tables-bulkquery).

## <a name="sql-on-prem-to-sazure-sql-database"></a>Перемещение данных из базы данных Azure SQL в локальной среде SQL Server tooan
Если hello исходных данных хранится в SQL Server в локальной среде, есть различные возможности для перемещения hello данных tooan базы данных Azure SQL:

1. [Экспорт файла tooFlat](#export-flat-file)
2. [Мастер миграции баз данных SQL](#insert-tables-bcp)
3. [Архивация и восстановление базы данных](#db-migration)
4. [Фабрика данных Azure](#adf)

Hello действия для первых трех hello, схожий toothose подразделы [перемещение данных tooSQL Server на виртуальной машине Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) , которые охватывают эти же процедуры. Ссылки toohello соответствующие разделы в этом разделе приведены в hello, следуйте инструкциям.

### <a name="export-flat-file"></a>Экспорт файла tooFlat
Hello действия для этого экспорта tooa неструктурированного файла, аналогичные toothose охваченных [tooFlat файл экспорта](machine-learning-data-science-move-sql-server-virtual-machine.md#export-flat-file).

### <a name="insert-tables-bcp"></a>Мастер миграции баз данных SQL
Hello действия по использованию hello мастер миграции баз данных SQL, аналогичные toothose, охваченных [мастер миграции баз данных SQL](machine-learning-data-science-move-sql-server-virtual-machine.md#sql-migration).

### <a name="db-migration"></a>Архивация и восстановление базы данных
Hello действия по использованию базы данных резервного копирования и восстановления, аналогичные toothose охваченных [базы данных резервное копирование и восстановление](machine-learning-data-science-move-sql-server-virtual-machine.md#sql-backup).

### <a name="adf"></a>Фабрика данных Azure
в разделе hello приведен Hello процедуры для перемещения данных tooan базы данных SQL Azure с фабрикой данных Azure (ADF) [перемещения данных из локальной tooSQL сервера SQL Azure с фабрикой данных Azure](machine-learning-data-science-move-sql-azure-adf.md). В этом разделе показано, как базы данных toomove данные из локальной tooan базы данных SQL Server Azure SQL через хранилище больших двоичных объектов Azure использование ADF.

Рассмотрите возможность использования ADF при toobe потребностей данных постоянно миграции в гибридном сценарии, который обращается к локально облачные ресурсы и hello данных в рамках транзакции или необходима toobe изменен или бизнес-логики добавили tooit при переносе. ADF позволяет hello планирования и отслеживания заданий, используя простые сценарии JSON, управлять hello перемещение данных на периодической основе. ADF также обладает другими возможностями, такими как поддержка сложных операций.
